---
title: Azure Diagnostics extension configuration schema version history
description: Relevant to collecting perf counters in Azure Virtual Machines, VM Scale Sets, Service Fabric, and Cloud Services.
services: azure-monitor
author: rboucher
ms.service: azure-monitor
ms.devlang: dotnet
ms.topic: reference
ms.date: 05/16/2017
ms.author: robb
ms.component: diagnostic-extension
ms.openlocfilehash: 47fb598e9a0e722d51493fda1ff5180d4b022524
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828815"
---
# <a name="azure-diagnostics-extension-configuration-schema-versions-and-history"></a><span data-ttu-id="a57ee-103">Azure Diagnostics extension configuration schema versions and history</span><span class="sxs-lookup"><span data-stu-id="a57ee-103">Azure Diagnostics extension configuration schema versions and history</span></span>
<span data-ttu-id="a57ee-104">This page indexes Azure Diagnostics extension schema versions shipped as part of the Microsoft Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="a57ee-104">This page indexes Azure Diagnostics extension schema versions shipped as part of the Microsoft Azure SDK.</span></span>  

> [!NOTE]
> <span data-ttu-id="a57ee-105">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span><span class="sxs-lookup"><span data-stu-id="a57ee-105">The Azure Diagnostics extension is the component used to collect performance counters and other statistics from:</span></span>
> - <span data-ttu-id="a57ee-106">Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="a57ee-106">Azure Virtual Machines</span></span> 
> - <span data-ttu-id="a57ee-107">Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="a57ee-107">Virtual Machine Scale Sets</span></span>
> - <span data-ttu-id="a57ee-108">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="a57ee-108">Service Fabric</span></span> 
> - <span data-ttu-id="a57ee-109">Cloud Services</span><span class="sxs-lookup"><span data-stu-id="a57ee-109">Cloud Services</span></span> 
> - <span data-ttu-id="a57ee-110">Network Security Groups</span><span class="sxs-lookup"><span data-stu-id="a57ee-110">Network Security Groups</span></span>
> 
> <span data-ttu-id="a57ee-111">This page is only relevant if you are using one of these services.</span><span class="sxs-lookup"><span data-stu-id="a57ee-111">This page is only relevant if you are using one of these services.</span></span>

<span data-ttu-id="a57ee-112">The Azure Diagnostics extension is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="a57ee-112">The Azure Diagnostics extension is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span> <span data-ttu-id="a57ee-113">For more information, see [Microsoft Monitoring Tools Overview](monitoring-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a57ee-113">For more information, see [Microsoft Monitoring Tools Overview](monitoring-overview.md).</span></span>

## <a name="azure-sdk-and-diagnostics-versions-shipping-chart"></a><span data-ttu-id="a57ee-114">Azure SDK and diagnostics versions shipping chart</span><span class="sxs-lookup"><span data-stu-id="a57ee-114">Azure SDK and diagnostics versions shipping chart</span></span>  

|<span data-ttu-id="a57ee-115">Azure SDK version</span><span class="sxs-lookup"><span data-stu-id="a57ee-115">Azure SDK version</span></span> | <span data-ttu-id="a57ee-116">Diagnostics extension version</span><span class="sxs-lookup"><span data-stu-id="a57ee-116">Diagnostics extension version</span></span> | <span data-ttu-id="a57ee-117">Model</span><span class="sxs-lookup"><span data-stu-id="a57ee-117">Model</span></span>|  
|------------------|-------------------------------|------|  
|<span data-ttu-id="a57ee-118">1.x</span><span class="sxs-lookup"><span data-stu-id="a57ee-118">1.x</span></span>               |<span data-ttu-id="a57ee-119">1.0</span><span class="sxs-lookup"><span data-stu-id="a57ee-119">1.0</span></span>                            |<span data-ttu-id="a57ee-120">plug-in</span><span class="sxs-lookup"><span data-stu-id="a57ee-120">plug-in</span></span>|  
|<span data-ttu-id="a57ee-121">2.0 - 2.4</span><span class="sxs-lookup"><span data-stu-id="a57ee-121">2.0 - 2.4</span></span>         |<span data-ttu-id="a57ee-122">1.0</span><span class="sxs-lookup"><span data-stu-id="a57ee-122">1.0</span></span>                            |<span data-ttu-id="a57ee-123">plug-in</span><span class="sxs-lookup"><span data-stu-id="a57ee-123">plug-in</span></span>|  
|<span data-ttu-id="a57ee-124">2.5</span><span class="sxs-lookup"><span data-stu-id="a57ee-124">2.5</span></span>               |<span data-ttu-id="a57ee-125">1.2</span><span class="sxs-lookup"><span data-stu-id="a57ee-125">1.2</span></span>                            |<span data-ttu-id="a57ee-126">extension</span><span class="sxs-lookup"><span data-stu-id="a57ee-126">extension</span></span>|  
|<span data-ttu-id="a57ee-127">2.6</span><span class="sxs-lookup"><span data-stu-id="a57ee-127">2.6</span></span>               |<span data-ttu-id="a57ee-128">1.3</span><span class="sxs-lookup"><span data-stu-id="a57ee-128">1.3</span></span>                            |<span data-ttu-id="a57ee-129">"</span><span class="sxs-lookup"><span data-stu-id="a57ee-129">"</span></span>|  
|<span data-ttu-id="a57ee-130">2.7</span><span class="sxs-lookup"><span data-stu-id="a57ee-130">2.7</span></span>               |<span data-ttu-id="a57ee-131">1.4</span><span class="sxs-lookup"><span data-stu-id="a57ee-131">1.4</span></span>                            |<span data-ttu-id="a57ee-132">"</span><span class="sxs-lookup"><span data-stu-id="a57ee-132">"</span></span>|  
|<span data-ttu-id="a57ee-133">2.8</span><span class="sxs-lookup"><span data-stu-id="a57ee-133">2.8</span></span>               |<span data-ttu-id="a57ee-134">1.5</span><span class="sxs-lookup"><span data-stu-id="a57ee-134">1.5</span></span>                            |<span data-ttu-id="a57ee-135">"</span><span class="sxs-lookup"><span data-stu-id="a57ee-135">"</span></span>|  
|<span data-ttu-id="a57ee-136">2.9</span><span class="sxs-lookup"><span data-stu-id="a57ee-136">2.9</span></span>               |<span data-ttu-id="a57ee-137">1.6</span><span class="sxs-lookup"><span data-stu-id="a57ee-137">1.6</span></span>                            |<span data-ttu-id="a57ee-138">"</span><span class="sxs-lookup"><span data-stu-id="a57ee-138">"</span></span>|
|<span data-ttu-id="a57ee-139">2.96</span><span class="sxs-lookup"><span data-stu-id="a57ee-139">2.96</span></span>              |<span data-ttu-id="a57ee-140">1.7</span><span class="sxs-lookup"><span data-stu-id="a57ee-140">1.7</span></span>                            |<span data-ttu-id="a57ee-141">"</span><span class="sxs-lookup"><span data-stu-id="a57ee-141">"</span></span>|
|<span data-ttu-id="a57ee-142">2.96</span><span class="sxs-lookup"><span data-stu-id="a57ee-142">2.96</span></span>              |<span data-ttu-id="a57ee-143">1.8</span><span class="sxs-lookup"><span data-stu-id="a57ee-143">1.8</span></span>                            |<span data-ttu-id="a57ee-144">"</span><span class="sxs-lookup"><span data-stu-id="a57ee-144">"</span></span>|
|<span data-ttu-id="a57ee-145">2.96</span><span class="sxs-lookup"><span data-stu-id="a57ee-145">2.96</span></span>              |<span data-ttu-id="a57ee-146">1.8.1</span><span class="sxs-lookup"><span data-stu-id="a57ee-146">1.8.1</span></span>                          |<span data-ttu-id="a57ee-147">"</span><span class="sxs-lookup"><span data-stu-id="a57ee-147">"</span></span>|
|<span data-ttu-id="a57ee-148">2.96</span><span class="sxs-lookup"><span data-stu-id="a57ee-148">2.96</span></span>              |<span data-ttu-id="a57ee-149">1.9</span><span class="sxs-lookup"><span data-stu-id="a57ee-149">1.9</span></span>                            |<span data-ttu-id="a57ee-150">"</span><span class="sxs-lookup"><span data-stu-id="a57ee-150">"</span></span>|



 <span data-ttu-id="a57ee-151">Azure Diagnostics version 1.0 first shipped in a plug-in model -- meaning that when you installed the Azure SDK, you got the version of Azure diagnostics shipped with it.</span><span class="sxs-lookup"><span data-stu-id="a57ee-151">Azure Diagnostics version 1.0 first shipped in a plug-in model -- meaning that when you installed the Azure SDK, you got the version of Azure diagnostics shipped with it.</span></span>  

 <span data-ttu-id="a57ee-152">Starting with SDK 2.5 (diagnostics version 1.2), Azure diagnostics went to an extension model.</span><span class="sxs-lookup"><span data-stu-id="a57ee-152">Starting with SDK 2.5 (diagnostics version 1.2), Azure diagnostics went to an extension model.</span></span> <span data-ttu-id="a57ee-153">The tools to utilize new features were only available in newer Azure SDKs, but any service using Azure diagnostics would pick up the latest shipping version directly from Azure.</span><span class="sxs-lookup"><span data-stu-id="a57ee-153">The tools to utilize new features were only available in newer Azure SDKs, but any service using Azure diagnostics would pick up the latest shipping version directly from Azure.</span></span> <span data-ttu-id="a57ee-154">For example, anyone still using SDK 2.5 would be loading the latest version shown in the previous table, regardless if they are using the newer features.</span><span class="sxs-lookup"><span data-stu-id="a57ee-154">For example, anyone still using SDK 2.5 would be loading the latest version shown in the previous table, regardless if they are using the newer features.</span></span>  

## <a name="schemas-index"></a><span data-ttu-id="a57ee-155">Schemas index</span><span class="sxs-lookup"><span data-stu-id="a57ee-155">Schemas index</span></span>  
<span data-ttu-id="a57ee-156">Different versions of Azure diagnostics use different configuration schemas.</span><span class="sxs-lookup"><span data-stu-id="a57ee-156">Different versions of Azure diagnostics use different configuration schemas.</span></span> 

[<span data-ttu-id="a57ee-157">Diagnostics 1.0 Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="a57ee-157">Diagnostics 1.0 Configuration Schema</span></span>](azure-diagnostics-schema-1dot0.md)  

[<span data-ttu-id="a57ee-158">Diagnostics 1.2 Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="a57ee-158">Diagnostics 1.2 Configuration Schema</span></span>](azure-diagnostics-schema-1dot2.md)  

[<span data-ttu-id="a57ee-159">Diagnostics 1.3 and later Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="a57ee-159">Diagnostics 1.3 and later Configuration Schema</span></span>](azure-diagnostics-schema-1dot3-and-later.md)  

## <a name="version-history"></a><span data-ttu-id="a57ee-160">Version history</span><span class="sxs-lookup"><span data-stu-id="a57ee-160">Version history</span></span>


### <a name="diagnostics-extension-19"></a><span data-ttu-id="a57ee-161">Diagnostics extension 1.9</span><span class="sxs-lookup"><span data-stu-id="a57ee-161">Diagnostics extension 1.9</span></span> 
<span data-ttu-id="a57ee-162">Added Docker support.</span><span class="sxs-lookup"><span data-stu-id="a57ee-162">Added Docker support.</span></span>


### <a name="diagnostics-extension-181"></a><span data-ttu-id="a57ee-163">Diagnostics extension 1.8.1</span><span class="sxs-lookup"><span data-stu-id="a57ee-163">Diagnostics extension 1.8.1</span></span> 
<span data-ttu-id="a57ee-164">Can specify a SAS token instead of a storage account key in the private config. If a SAS token is provided, the storage account key is ignored.</span><span class="sxs-lookup"><span data-stu-id="a57ee-164">Can specify a SAS token instead of a storage account key in the private config. If a SAS token is provided, the storage account key is ignored.</span></span>


```json
{
    "storageAccountName": "diagstorageaccount",
    "storageAccountEndPoint": "https://core.windows.net",
    "storageAccountSasToken": "{sas token}",
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "endpoint": "https://core.windows.net",
                "sasToken": "{sas token}"
            }
        ]
    }
}
```

```xml
<PrivateConfig>
    <StorageAccount name="diagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    <SecondaryStorageAccounts>
        <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" sasToken="{sas token}" />
    </SecondaryStorageAccounts>
</PrivateConfig>
```


### <a name="diagnostics-extension-18"></a><span data-ttu-id="a57ee-165">Diagnostics extension 1.8</span><span class="sxs-lookup"><span data-stu-id="a57ee-165">Diagnostics extension 1.8</span></span> 
<span data-ttu-id="a57ee-166">Added Storage Type to PublicConfig.</span><span class="sxs-lookup"><span data-stu-id="a57ee-166">Added Storage Type to PublicConfig.</span></span> <span data-ttu-id="a57ee-167">StorageType can be *Table*, *Blob*, *TableAndBlob*.</span><span class="sxs-lookup"><span data-stu-id="a57ee-167">StorageType can be *Table*, *Blob*, *TableAndBlob*.</span></span> <span data-ttu-id="a57ee-168">*Table* is the default.</span><span class="sxs-lookup"><span data-stu-id="a57ee-168">*Table* is the default.</span></span>


```json
{
    "WadCfg": {
    },
    "StorageAccount": "diagstorageaccount",
    "StorageType": "TableAndBlob"
}
```

```xml
<PublicConfig>
    <WadCfg />
    <StorageAccount>diagstorageaccount</StorageAccount>
    <StorageType>TableAndBlob</StorageType>
</PublicConfig>
```


### <a name="diagnostics-extension-17"></a><span data-ttu-id="a57ee-169">Diagnostics extension 1.7</span><span class="sxs-lookup"><span data-stu-id="a57ee-169">Diagnostics extension 1.7</span></span> 
<span data-ttu-id="a57ee-170">Added the ability to route to EventHub.</span><span class="sxs-lookup"><span data-stu-id="a57ee-170">Added the ability to route to EventHub.</span></span>

### <a name="diagnostics-extension-15"></a><span data-ttu-id="a57ee-171">Diagnostics extension 1.5</span><span class="sxs-lookup"><span data-stu-id="a57ee-171">Diagnostics extension 1.5</span></span>
<span data-ttu-id="a57ee-172">Added the sinks element and the ability to send diagnostics data to [Application Insights](../application-insights/app-insights-cloudservices.md) making it easier to diagnose issues across your application as well as the system and infrastructure level.</span><span class="sxs-lookup"><span data-stu-id="a57ee-172">Added the sinks element and the ability to send diagnostics data to [Application Insights](../application-insights/app-insights-cloudservices.md) making it easier to diagnose issues across your application as well as the system and infrastructure level.</span></span>

### <a name="azure-sdk-26-and-diagnostics-extension-13"></a><span data-ttu-id="a57ee-173">Azure SDK 2.6 and diagnostics extension 1.3</span><span class="sxs-lookup"><span data-stu-id="a57ee-173">Azure SDK 2.6 and diagnostics extension 1.3</span></span> 
<span data-ttu-id="a57ee-174">For Cloud Service projects in Visual Studio, the following changes were made.</span><span class="sxs-lookup"><span data-stu-id="a57ee-174">For Cloud Service projects in Visual Studio, the following changes were made.</span></span> <span data-ttu-id="a57ee-175">(These changes also apply to later versions of Azure SDK.)</span><span class="sxs-lookup"><span data-stu-id="a57ee-175">(These changes also apply to later versions of Azure SDK.)</span></span>

* <span data-ttu-id="a57ee-176">The local emulator now supports diagnostics.</span><span class="sxs-lookup"><span data-stu-id="a57ee-176">The local emulator now supports diagnostics.</span></span> <span data-ttu-id="a57ee-177">This change means you can collect diagnostics data and ensure your application is creating the right traces while you're developing and testing in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a57ee-177">This change means you can collect diagnostics data and ensure your application is creating the right traces while you're developing and testing in Visual Studio.</span></span> <span data-ttu-id="a57ee-178">The connection string `UseDevelopmentStorage=true` enables diagnostics data collection while you're running your cloud service project in Visual Studio by using the Azure storage emulator.</span><span class="sxs-lookup"><span data-stu-id="a57ee-178">The connection string `UseDevelopmentStorage=true` enables diagnostics data collection while you're running your cloud service project in Visual Studio by using the Azure storage emulator.</span></span> <span data-ttu-id="a57ee-179">All diagnostics data is collected in the (Development Storage) storage account.</span><span class="sxs-lookup"><span data-stu-id="a57ee-179">All diagnostics data is collected in the (Development Storage) storage account.</span></span>
* <span data-ttu-id="a57ee-180">The diagnostics storage account connection string (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) is stored once again in the service configuration (.cscfg) file.</span><span class="sxs-lookup"><span data-stu-id="a57ee-180">The diagnostics storage account connection string (Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString) is stored once again in the service configuration (.cscfg) file.</span></span> <span data-ttu-id="a57ee-181">In Azure SDK 2.5 the diagnostics storage account was specified in the diagnostics.wadcfgx file.</span><span class="sxs-lookup"><span data-stu-id="a57ee-181">In Azure SDK 2.5 the diagnostics storage account was specified in the diagnostics.wadcfgx file.</span></span>

<span data-ttu-id="a57ee-182">There are some notable differences between how the connection string worked in Azure SDK 2.4 and earlier and how it works in Azure SDK 2.6 and later.</span><span class="sxs-lookup"><span data-stu-id="a57ee-182">There are some notable differences between how the connection string worked in Azure SDK 2.4 and earlier and how it works in Azure SDK 2.6 and later.</span></span>

* <span data-ttu-id="a57ee-183">In Azure SDK 2.4 and earlier, the connection string was used at runtime by the diagnostics plugin to get the storage account information for transferring diagnostics logs.</span><span class="sxs-lookup"><span data-stu-id="a57ee-183">In Azure SDK 2.4 and earlier, the connection string was used at runtime by the diagnostics plugin to get the storage account information for transferring diagnostics logs.</span></span>
* <span data-ttu-id="a57ee-184">In Azure SDK 2.6 and later, Visual Studio uses the diagnostics connection string to configure the diagnostics extension with the appropriate storage account information during publishing.</span><span class="sxs-lookup"><span data-stu-id="a57ee-184">In Azure SDK 2.6 and later, Visual Studio uses the diagnostics connection string to configure the diagnostics extension with the appropriate storage account information during publishing.</span></span> <span data-ttu-id="a57ee-185">The connection string lets you define different storage accounts for different service configurations that Visual Studio will use when publishing.</span><span class="sxs-lookup"><span data-stu-id="a57ee-185">The connection string lets you define different storage accounts for different service configurations that Visual Studio will use when publishing.</span></span> <span data-ttu-id="a57ee-186">However, because the diagnostics plugin is no longer available (after Azure SDK 2.5), the .cscfg file by itself can't enable the Diagnostics Extension.</span><span class="sxs-lookup"><span data-stu-id="a57ee-186">However, because the diagnostics plugin is no longer available (after Azure SDK 2.5), the .cscfg file by itself can't enable the Diagnostics Extension.</span></span> <span data-ttu-id="a57ee-187">You have to enable the extension separately through tools such as Visual Studio or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a57ee-187">You have to enable the extension separately through tools such as Visual Studio or PowerShell.</span></span>
* <span data-ttu-id="a57ee-188">To simplify the process of configuring the diagnostics extension with PowerShell, the package output from Visual Studio also contains the public configuration XML for the diagnostics extension for each role.</span><span class="sxs-lookup"><span data-stu-id="a57ee-188">To simplify the process of configuring the diagnostics extension with PowerShell, the package output from Visual Studio also contains the public configuration XML for the diagnostics extension for each role.</span></span> <span data-ttu-id="a57ee-189">Visual Studio uses the diagnostics connection string to populate the storage account information present in the public configuration.</span><span class="sxs-lookup"><span data-stu-id="a57ee-189">Visual Studio uses the diagnostics connection string to populate the storage account information present in the public configuration.</span></span> <span data-ttu-id="a57ee-190">The public config files are created in the Extensions folder and follow the pattern PaaSDiagnostics.<RoleName>.PubConfig.xml.</span><span class="sxs-lookup"><span data-stu-id="a57ee-190">The public config files are created in the Extensions folder and follow the pattern PaaSDiagnostics.<RoleName>.PubConfig.xml.</span></span> <span data-ttu-id="a57ee-191">Any PowerShell based deployments can use this pattern to map each configuration to a Role.</span><span class="sxs-lookup"><span data-stu-id="a57ee-191">Any PowerShell based deployments can use this pattern to map each configuration to a Role.</span></span>
* <span data-ttu-id="a57ee-192">The connection string in the .cscfg file is also used by the Azure portal to access the diagnostics data so it can appear in the **Monitoring** tab. The connection string is needed to configure the service to show verbose monitoring data in the portal.</span><span class="sxs-lookup"><span data-stu-id="a57ee-192">The connection string in the .cscfg file is also used by the Azure portal to access the diagnostics data so it can appear in the **Monitoring** tab. The connection string is needed to configure the service to show verbose monitoring data in the portal.</span></span>

#### <a name="migrating-projects-to-azure-sdk-26-and-later"></a><span data-ttu-id="a57ee-193">Migrating projects to Azure SDK 2.6 and later</span><span class="sxs-lookup"><span data-stu-id="a57ee-193">Migrating projects to Azure SDK 2.6 and later</span></span>
<span data-ttu-id="a57ee-194">When migrating from Azure SDK 2.5 to Azure SDK 2.6 or later, if you had a diagnostics storage account specified in the .wadcfgx file, then it will stay there.</span><span class="sxs-lookup"><span data-stu-id="a57ee-194">When migrating from Azure SDK 2.5 to Azure SDK 2.6 or later, if you had a diagnostics storage account specified in the .wadcfgx file, then it will stay there.</span></span> <span data-ttu-id="a57ee-195">To take advantage of the flexibility of using different storage accounts for different storage configurations, you'll have to manually add the connection string to your project.</span><span class="sxs-lookup"><span data-stu-id="a57ee-195">To take advantage of the flexibility of using different storage accounts for different storage configurations, you'll have to manually add the connection string to your project.</span></span> <span data-ttu-id="a57ee-196">If you're migrating a project from Azure SDK 2.4 or earlier to Azure SDK 2.6, then the diagnostics connection strings are preserved.</span><span class="sxs-lookup"><span data-stu-id="a57ee-196">If you're migrating a project from Azure SDK 2.4 or earlier to Azure SDK 2.6, then the diagnostics connection strings are preserved.</span></span> <span data-ttu-id="a57ee-197">However, note the changes in how connection strings are treated in Azure SDK 2.6 as specified in the previous section.</span><span class="sxs-lookup"><span data-stu-id="a57ee-197">However, note the changes in how connection strings are treated in Azure SDK 2.6 as specified in the previous section.</span></span>

#### <a name="how-visual-studio-determines-the-diagnostics-storage-account"></a><span data-ttu-id="a57ee-198">How Visual Studio determines the diagnostics storage account</span><span class="sxs-lookup"><span data-stu-id="a57ee-198">How Visual Studio determines the diagnostics storage account</span></span>
* <span data-ttu-id="a57ee-199">If a diagnostics connection string is specified in the .cscfg file, Visual Studio uses it to configure the diagnostics extension when publishing, and when generating the public configuration xml files during packaging.</span><span class="sxs-lookup"><span data-stu-id="a57ee-199">If a diagnostics connection string is specified in the .cscfg file, Visual Studio uses it to configure the diagnostics extension when publishing, and when generating the public configuration xml files during packaging.</span></span>
* <span data-ttu-id="a57ee-200">If no diagnostics connection string is specified in the .cscfg file, then Visual Studio falls back to using the storage account specified in the .wadcfgx file to configure the diagnostics extension when publishing, and generating the public configuration xml files when packaging.</span><span class="sxs-lookup"><span data-stu-id="a57ee-200">If no diagnostics connection string is specified in the .cscfg file, then Visual Studio falls back to using the storage account specified in the .wadcfgx file to configure the diagnostics extension when publishing, and generating the public configuration xml files when packaging.</span></span>
* <span data-ttu-id="a57ee-201">The diagnostics connection string in the .cscfg file takes precedence over the storage account in the .wadcfgx file.</span><span class="sxs-lookup"><span data-stu-id="a57ee-201">The diagnostics connection string in the .cscfg file takes precedence over the storage account in the .wadcfgx file.</span></span> <span data-ttu-id="a57ee-202">If a diagnostics connection string is specified in the .cscfg file, then Visual Studio uses that and ignores the storage account in .wadcfgx.</span><span class="sxs-lookup"><span data-stu-id="a57ee-202">If a diagnostics connection string is specified in the .cscfg file, then Visual Studio uses that and ignores the storage account in .wadcfgx.</span></span>

#### <a name="what-does-the-update-development-storage-connection-strings-checkbox-do"></a><span data-ttu-id="a57ee-203">What does the "Update development storage connection strings…" checkbox do?</span><span class="sxs-lookup"><span data-stu-id="a57ee-203">What does the "Update development storage connection strings…" checkbox do?</span></span>
<span data-ttu-id="a57ee-204">The checkbox for **Update development storage connection strings for Diagnostics and Caching with Microsoft Azure storage account credentials when publishing to Microsoft Azure** gives you a convenient way to update any development storage account connection strings with the Azure storage account specified during publishing.</span><span class="sxs-lookup"><span data-stu-id="a57ee-204">The checkbox for **Update development storage connection strings for Diagnostics and Caching with Microsoft Azure storage account credentials when publishing to Microsoft Azure** gives you a convenient way to update any development storage account connection strings with the Azure storage account specified during publishing.</span></span>

<span data-ttu-id="a57ee-205">For example, suppose you select this checkbox and the diagnostics connection string specifies `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="a57ee-205">For example, suppose you select this checkbox and the diagnostics connection string specifies `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="a57ee-206">When you publish the project to Azure, Visual Studio will automatically update the diagnostics connection string with the storage account you specified in the Publish wizard.</span><span class="sxs-lookup"><span data-stu-id="a57ee-206">When you publish the project to Azure, Visual Studio will automatically update the diagnostics connection string with the storage account you specified in the Publish wizard.</span></span> <span data-ttu-id="a57ee-207">However, if a real storage account was specified as the diagnostics connection string, then that account is used instead.</span><span class="sxs-lookup"><span data-stu-id="a57ee-207">However, if a real storage account was specified as the diagnostics connection string, then that account is used instead.</span></span>

### <a name="diagnostics-functionality-differences-between-azure-sdk-24-and-earlier-and-azure-sdk-25-and-later"></a><span data-ttu-id="a57ee-208">Diagnostics functionality differences between Azure SDK 2.4 and earlier and Azure SDK 2.5 and later</span><span class="sxs-lookup"><span data-stu-id="a57ee-208">Diagnostics functionality differences between Azure SDK 2.4 and earlier and Azure SDK 2.5 and later</span></span>
<span data-ttu-id="a57ee-209">If you're upgrading your project from Azure SDK 2.4 to Azure SDK 2.5 or later, you should bear in mind the following diagnostics functionality differences.</span><span class="sxs-lookup"><span data-stu-id="a57ee-209">If you're upgrading your project from Azure SDK 2.4 to Azure SDK 2.5 or later, you should bear in mind the following diagnostics functionality differences.</span></span>

* <span data-ttu-id="a57ee-210">**Configuration APIs are deprecated** – Programmatic configuration of diagnostics is available in Azure SDK 2.4 or earlier versions, but is deprecated in Azure SDK 2.5 and later.</span><span class="sxs-lookup"><span data-stu-id="a57ee-210">**Configuration APIs are deprecated** – Programmatic configuration of diagnostics is available in Azure SDK 2.4 or earlier versions, but is deprecated in Azure SDK 2.5 and later.</span></span> <span data-ttu-id="a57ee-211">If your diagnostics configuration is currently defined in code, you'll need to reconfigure those settings from scratch in the migrated project in order for diagnostics to keep working.</span><span class="sxs-lookup"><span data-stu-id="a57ee-211">If your diagnostics configuration is currently defined in code, you'll need to reconfigure those settings from scratch in the migrated project in order for diagnostics to keep working.</span></span> <span data-ttu-id="a57ee-212">The diagnostics configuration file for Azure SDK 2.4 is diagnostics.wadcfg, and diagnostics.wadcfgx for Azure SDK 2.5 and later.</span><span class="sxs-lookup"><span data-stu-id="a57ee-212">The diagnostics configuration file for Azure SDK 2.4 is diagnostics.wadcfg, and diagnostics.wadcfgx for Azure SDK 2.5 and later.</span></span>
* <span data-ttu-id="a57ee-213">**Diagnostics for cloud service applications can only be configured at the role level, not at the instance level.**</span><span class="sxs-lookup"><span data-stu-id="a57ee-213">**Diagnostics for cloud service applications can only be configured at the role level, not at the instance level.**</span></span>
* <span data-ttu-id="a57ee-214">**Every time you deploy your app, the diagnostics configuration is updated** – This can cause parity issues if you change your diagnostics configuration from Server Explorer and then redeploy your app.</span><span class="sxs-lookup"><span data-stu-id="a57ee-214">**Every time you deploy your app, the diagnostics configuration is updated** – This can cause parity issues if you change your diagnostics configuration from Server Explorer and then redeploy your app.</span></span>
* <span data-ttu-id="a57ee-215">**In Azure SDK 2.5 and later, crash dumps are configured in the diagnostics configuration file, not in code** – If you have crash dumps configured in code, you'll have to manually transfer the configuration from code to the configuration file, because the crash dumps aren't transferred during the migration to Azure SDK 2.6.</span><span class="sxs-lookup"><span data-stu-id="a57ee-215">**In Azure SDK 2.5 and later, crash dumps are configured in the diagnostics configuration file, not in code** – If you have crash dumps configured in code, you'll have to manually transfer the configuration from code to the configuration file, because the crash dumps aren't transferred during the migration to Azure SDK 2.6.</span></span>

