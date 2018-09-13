---
title: Using PowerShell to setup Application Insights in an Azure  | Microsoft Docs
description: Automate configuring Azure Diagnostics to pipe to Application Insights.
services: application-insights
documentationcenter: .net
author: sbtron
manager: douge
ms.assetid: 4ac803a8-f424-4c0c-b18f-4b9c189a64a5
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 11/17/2015
ms.author: awills
ms.openlocfilehash: b85fb9bc355a496e563c945cc91e8198d4f50d00
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669607"
---
# <a name="using-powershell-to-set-up-application-insights-for-an-azure-web-app"></a>Using PowerShell to set up Application Insights for an Azure web app
[Microsoft Azure](https://azure.com) can be [configured to send Azure Diagnostics](app-insights-azure-diagnostics.md) to [Azure Application Insights](app-insights-overview.md). The diagnostics relate to Azure Cloud Services and Azure VMs. They complement the telemetry that you send from within the app using the Application Insights SDK. As part of automating the process of creating new resources in Azure, you can configure diagnostics using PowerShell.

## <a name="azure-template"></a>Azure template
If the web app is in Azure and you create your resources using an Azure Resource Manager template, you can configure Application Insights by adding this to the resources node:

    {
      resources: [
        /* Create Application Insights resource */
        {
          "apiVersion": "2015-05-01",
          "type": "microsoft.insights/components",
          "name": "nameOfAIAppResource",
          "location": "centralus",
          "kind": "web",
          "properties": { "ApplicationId": "nameOfAIAppResource" },
          "dependsOn": [
            "[concat('Microsoft.Web/sites/', myWebAppName)]"
          ]
        }
       ]
     } 

* `nameOfAIAppResource` - a name for the Application Insights resource
* `myWebAppName` - the id of the web app

## <a name="enable-diagnostics-extension-as-part-of-deploying-a-cloud-service"></a>Enable diagnostics extension as part of deploying a Cloud Service
The `New-AzureDeployment` cmdlet has a parameter `ExtensionConfiguration`, which takes an array of diagnostics configurations. These can be created using the `New-AzureServiceDiagnosticsExtensionConfig` cmdlet. For example:

```ps

    $service_package = "CloudService.cspkg"
    $service_config = "ServiceConfiguration.Cloud.cscfg"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"

    $primary_storagekey = (Get-AzureStorageKey `
     -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
       -StorageAccountName $diagnostics_storagename `
       -StorageAccountKey $primary_storagekey

    $webrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WebRole" -Storage_context $storageContext `
      -DiagnosticsConfigurationPath $webrole_diagconfigpath
    $workerrole_diagconfig = `
     New-AzureServiceDiagnosticsExtensionConfig `
      -Role "WorkerRole" `
      -StorageContext $storage_context `
      -DiagnosticsConfigurationPath $workerrole_diagconfigpath

    New-AzureDeployment `
      -ServiceName $service_name `
      -Slot Production `
      -Package $service_package `
      -Configuration $service_config `
      -ExtensionConfiguration @($webrole_diagconfig,$workerrole_diagconfig)

``` 

## <a name="enable-diagnostics-extension-on-an-existing-cloud-service"></a>Enable diagnostics extension on an existing Cloud Service
On an existing service, use `Set-AzureServiceDiagnosticsExtension`.

```ps

    $service_name = "MyService"
    $diagnostics_storagename = "myservicediagnostics"
    $webrole_diagconfigpath = "MyService.WebRole.PubConfig.xml" 
    $workerrole_diagconfigpath = "MyService.WorkerRole.PubConfig.xml"
    $primary_storagekey = (Get-AzureStorageKey `
         -StorageAccountName "$diagnostics_storagename").Primary
    $storage_context = New-AzureStorageContext `
        -StorageAccountName $diagnostics_storagename `
        -StorageAccountKey $primary_storagekey

    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $webrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WebRole" 
    Set-AzureServiceDiagnosticsExtension `
        -StorageContext $storage_context `
        -DiagnosticsConfigurationPath $workerrole_diagconfigpath `
        -ServiceName $service_name `
        -Slot Production `
        -Role "WorkerRole"
```

## <a name="get-current-diagnostics-extension-configuration"></a>Get current diagnostics extension configuration
```ps

    Get-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```


## <a name="remove-diagnostics-extension"></a>Remove diagnostics extension
```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService"
```

If you enabled the diagnostics extension using either `Set-AzureServiceDiagnosticsExtension` or `New-AzureServiceDiagnosticsExtensionConfig` without the Role parameter, then you can remove the extension using `Remove-AzureServiceDiagnosticsExtension` without the Role parameter. If the Role parameter was used when enabling the extension then it must also be used when removing the extension.

To remove the diagnostics extension from each individual role:

```ps

    Remove-AzureServiceDiagnosticsExtension -ServiceName "MyService" -Role "WebRole"
```


## <a name="see-also"></a>See also
* [Monitor Azure Cloud Services apps with Application Insights](app-insights-cloudservices.md)
* [Send Azure Diagnostics to Application Insights](app-insights-azure-diagnostics.md)
* [Automate configuring alerts](app-insights-powershell-alerts.md)

