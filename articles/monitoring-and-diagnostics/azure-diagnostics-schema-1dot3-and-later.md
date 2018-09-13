---
title: Azure Diagnostics 1.3, 1.4, 1.5, 1.6, 1.7 Configuration Schema | Microsoft Docs
description: Schema version 1.3 and later Azure diagnostics shipped as part of the Microsoft Azure SDK.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/09/2017
ms.author: robb
ms.openlocfilehash: b5d800db47284ca9fa82fc07ed67617ab32cd143
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564555"
---
# <a name="azure-diagnostics-13-14-15-configuration-schema"></a><span data-ttu-id="2b3de-103">Azure Diagnostics 1.3, 1.4, 1.5 Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="2b3de-103">Azure Diagnostics 1.3, 1.4, 1.5 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="2b3de-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="2b3de-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="2b3de-105">This page is only relevant if you are using one of these services.</span><span class="sxs-lookup"><span data-stu-id="2b3de-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="2b3de-106">Azure Diagnostics is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="2b3de-106">Azure Diagnostics is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="2b3de-107">The Azure Diagnostics configuration file is used to set diagnostic configuration settings when the diagnostics monitor starts.</span><span class="sxs-lookup"><span data-stu-id="2b3de-107">The Azure Diagnostics configuration file is used to set diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

<span data-ttu-id="2b3de-108">This page is valid for versions 1.3, 1.4 and 1.5 (Azure SDK 2.4 and newer).</span><span class="sxs-lookup"><span data-stu-id="2b3de-108">This page is valid for versions 1.3, 1.4 and 1.5 (Azure SDK 2.4 and newer).</span></span> <span data-ttu-id="2b3de-109">Newer configuration sections are commented to show in what version they were added.</span><span class="sxs-lookup"><span data-stu-id="2b3de-109">Newer configuration sections are commented to show in what version they were added.</span></span>  

 <span data-ttu-id="2b3de-110">Download the public configuration file schema definition by executing the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="2b3de-110">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 <span data-ttu-id="2b3de-111">For more information about using Azure Diagnostics, see [Enabling Diagnostics in Azure Cloud Services](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/).</span><span class="sxs-lookup"><span data-stu-id="2b3de-111">For more information about using Azure Diagnostics, see [Enabling Diagnostics in Azure Cloud Services](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="2b3de-112">Example of the diagnostics configuration file</span><span class="sxs-lookup"><span data-stu-id="2b3de-112">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="2b3de-113">The following example shows a typical diagnostics configuration file:</span><span class="sxs-lookup"><span data-stu-id="2b3de-113">The following example shows a typical diagnostics configuration file:</span></span>  

```xml  
<?xml version="1.0" encoding="utf-8"?>  
<DiagnosticsConfiguration  xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">   
  <PublicConfig>  
    <WadCfg>  
      <DiagnosticMonitorConfiguration overallQuotaInMB="10000">  

        <PerformanceCounters scheduledTransferPeriod="PT1M">  
          <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />  
        </PerformanceCounters>  

        <Directories scheduledTransferPeriod="PT5M">  
          <IISLogs containerName="iislogs" />  
          <FailedRequestLogs containerName="iisfailed" />  

          <DataSources>  
            <DirectoryConfiguration containerName="mynewprocess">  
              <Absolute path="C:\MyNewProcess" expandEnvironment="false" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="badapp">  
              <Absolute path="%SYSTEMDRIVE%\BadApp" expandEnvironment="true" />  
            </DirectoryConfiguration>  
            <DirectoryConfiguration containerName="goodapp">  
              <LocalResource name="Skippy" relativePath="..\PeanutButter"/>  
            </DirectoryConfiguration>  
          </DataSources>  

        </Directories>  

        <EtwProviders>  
          <EtwEventSourceProviderConfiguration   
                       provider="MyProviderClass"   
                       scheduledTransferPeriod="PT5M">  
            <Event id="0"/>  
            <Event id="1" eventDestination="errorTable"/>  
            <DefaultEvents />  
          </EtwEventSourceProviderConfiguration>  
          <EtwManifestProviderConfiguration provider="5974b00b-84c2-44bc-9e58-3a2451b4e3ad" scheduledTransferLogLevelFilter="Information" scheduledTransferPeriod="PT2M">  
            <Event id="0"/>  
            <DefaultEvents eventDestination="defaultTable"/>  
          </EtwManifestProviderConfiguration>  
        </EtwProviders>  

        <WindowsEventLog scheduledTransferPeriod="PT5M">  
          <DataSource name="System!*[System[Provider[@Name='Microsoft Antimalware']]]"/>  
          <DataSource name="System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]" />  
          <DataSource name="System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]" />  
        </WindowsEventLog>  

        <Logs  bufferQuotaInMB="1024"   
             scheduledTransferPeriod="PT1M"   
             scheduledTransferLogLevelFilter="Verbose"   
             sinks="ApplicationInsights.AppLogs"/>  <!-- sinks attribute added in 1.5 -->  

        <CrashDumps containerName="wad-crashdumps" directoryQuotaPercentage="30" dumpType="Mini">  
          <CrashDumpConfiguration processName="mynewprocess.exe" />  
          <CrashDumpConfiguration processName="badapp.exe"/>  
        </CrashDumps>  

      </DiagnosticMonitorConfiguration>  

      <SinksConfig>   <!-- Added in 1.5 -->  
        <Sink name="ApplicationInsights">   
          <ApplicationInsights>{Insert InstrumentationKey}</ApplicationInsights>   
          <Channels>   
            <Channel logLevel="Error" name="Errors"  />   
            <Channel logLevel="Verbose" name="AppLogs"  />   
          </Channels>   
        </Sink>   
        <Sink name="EventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryEventHub"> <!-- Added in 1.7 -->
          <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" usePublisherId="false" />
        </Sink>
        <Sink name="secondaryStorageAccount"> <!-- Added in 1.7 -->
          <StorageAccount name="secondarydiagstorageaccount" endpoint="https://core.windows.net" />
        </Sink>
   </SinksConfig>

    </WadCfg>  
  </PublicConfig>  

  <PrivateConfig>  <!-- Added in 1.3 -->  
    <StorageAccount name="" key="" endpoint="" />
    <EventHub Url="https://myeventhub-ns.servicebus.windows.net/diageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    <SecondaryStorageAccounts>
       <StorageAccount name="secondarydiagstorageaccount" key="{base64 encoded key}" endpoint="https://core.windows.net" />
    </SecondaryStorageAccounts>
    <SecondaryEventHubs>
       <EventHub Url="https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub" SharedAccessKeyName="SendRule" SharedAccessKey="{base64 encoded key}" />
    </SecondaryEventHubs>

  </PrivateConfig>  
  <IsEnabled>true</IsEnabled>  
</DiagnosticsConfiguration>  

```  

<span data-ttu-id="2b3de-114">Here is the JSON equivalent of the previous XML configuration file.</span><span class="sxs-lookup"><span data-stu-id="2b3de-114">Here is the JSON equivalent of the previous XML configuration file.</span></span>  
```json
{
    "WadCfg": {
        "DiagnosticMonitorConfiguration": {
            "overallQuotaInMB": 10000,
            "DiagnosticInfrastructureLogs": {
                "scheduledTransferLogLevelFilter": "Error"
            },
            "PerformanceCounters": {
                "scheduledTransferPeriod": "PT1M",
                "PerformanceCounterConfiguration": [
                    {
                        "counterSpecifier": "\\Processor(_Total)\\% Processor Time",
                        "sampleRate": "PT1M",
                        "unit": "percent"
                    }
                ]
            },
            "Directories": {
                "scheduledTransferPeriod": "PT5M",
                "IISLogs": {
                    "containerName": "iislogs"
                },
                "FailedRequestLogs": {
                    "containerName": "iisfailed"
                },
                "DataSources": [
                    {
                        "containerName": "mynewprocess",
                        "Absolute": {
                            "path": "C:\\MyNewProcess",
                            "expandEnvironment": false
                        }
                    },
                    {
                        "containerName": "badapp",
                        "Absolute": {
                            "path": "%SYSTEMDRIVE%\\BadApp",
                            "expandEnvironment": true
                        }
                    },
                    {
                        "containerName": "goodapp",
                        "LocalResource": {
                            "relativePath": "..\\PeanutButter",
                            "name": "Skippy"
                        }
                    }
                ]
            },
            "EtwProviders": {
                "sinks": "",
                "EtwEventSourceProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT5M",
                        "provider": "MyProviderClass",
                        "Event": [
                            {
                                "id": 0
                            },
                            {
                                "id": 1,
                                "eventDestination": "errorTable"
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ],
                "EtwManifestProviderConfiguration": [
                    {
                        "scheduledTransferPeriod": "PT2M",
                        "scheduledTransferLogLevelFilter": "Information",
                        "provider": "5974b00b-84c2-44bc-9e58-3a2451b4e3ad",
                        "Event": [
                            {
                                "id": 0
                            }
                        ],
                        "DefaultEvents": {
                        }
                    }
                ]
            },
            "WindowsEventLog": {
                "scheduledTransferPeriod": "PT5M",
                "DataSource": [
                    {
                        "name": "System!*[System[Provider[@Name='Microsoft Antimalware']]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='NTFS'] and (EventID=55)]]"
                    },
                    {
                        "name": "System!*[System[Provider[@Name='disk'] and (EventID=7 or EventID=52 or EventID=55)]]"
                    }
                ]
            },
            "Logs": {
                "scheduledTransferPeriod": "PT1M",
                "scheduledTransferLogLevelFilter": "Verbose",
                "sinks": "ApplicationInsights.AppLogs"
            },
            "CrashDumps": {
                "directoryQuotaPercentage": 30,
                "dumpType": "Mini",
                "containerName": "wad-crashdumps",
                "CrashDumpConfiguration": [
                    {
                        "processName": "mynewprocess.exe"
                    },
                    {
                        "processName": "badapp.exe"
                    }
                ]
            }
        },
        "SinksConfig": {
            "Sink": [
                {
                    "name": "ApplicationInsights",
                    "ApplicationInsights": "{Insert InstrumentationKey}",
                    "Channels": {
                        "Channel": [
                            {
                                "logLevel": "Error",
                                "name": "Errors"
                            },
                            {
                                "logLevel": "Verbose",
                                "name": "AppLogs"
                            }
                        ]
                    }
                },
                {
                    "name": "EventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryEventHub",
                    "EventHub": {
                        "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                        "SharedAccessKeyName": "SendRule",
                        "usePublisherId": false
                    }
                },
                {
                    "name": "secondaryStorageAccount",
                    "StorageAccount": {
                        "name": "secondarydiagstorageaccount",
                        "endpoint": "https://core.windows.net"
                    }
                }
            ]
        }
    },
    "StorageAccount": "diagstorageaccount"
}


{
    "storageAccountName": "diagstorageaccount",
    "storageAccountKey": "{base64 encoded key}",
    "storageAccountEndPoint": "https://core.windows.net",
    "EventHub": {
        "Url": "https://myeventhub-ns.servicebus.windows.net/diageventhub",
        "SharedAccessKeyName": "SendRule",
        "SharedAccessKey": "{base64 encoded key}"
    },
    "SecondaryStorageAccounts": {
        "StorageAccount": [
            {
                "name": "secondarydiagstorageaccount",
                "key": "{base64 encoded key}",
                "endpoint": "https://core.windows.net"
            }
        ]
    },
    "SecondaryEventHubs": {
        "EventHub": [
            {
                "Url": "https://myeventhub-ns.servicebus.windows.net/secondarydiageventhub",
                "SharedAccessKeyName": "SendRule",
                "SharedAccessKey": "{base64 encoded key}"
            }
        ]
    }
}

```

## <a name="reading-this-page"></a><span data-ttu-id="2b3de-115">Reading this page</span><span class="sxs-lookup"><span data-stu-id="2b3de-115">Reading this page</span></span>  
 <span data-ttu-id="2b3de-116">The tags following are roughly in order shown in the preceding example.</span><span class="sxs-lookup"><span data-stu-id="2b3de-116">The tags following are roughly in order shown in the preceding example.</span></span>  <span data-ttu-id="2b3de-117">If you don't see a full description where you expect it, search the page for the element or attribute.</span><span class="sxs-lookup"><span data-stu-id="2b3de-117">If you don't see a full description where you expect it, search the page for the element or attribute.</span></span>  

## <a name="common-attribute-types"></a><span data-ttu-id="2b3de-118">Common Attribute Types</span><span class="sxs-lookup"><span data-stu-id="2b3de-118">Common Attribute Types</span></span>  
 <span data-ttu-id="2b3de-119">**scheduledTransferPeriod** attribute appears in several elements.</span><span class="sxs-lookup"><span data-stu-id="2b3de-119">**scheduledTransferPeriod** attribute appears in several elements.</span></span> <span data-ttu-id="2b3de-120">It is the interval between scheduled transfers to storage rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="2b3de-120">It is the interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="2b3de-121">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="2b3de-121">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span>

## <a name="diagnostics-configuration-namespace"></a><span data-ttu-id="2b3de-122">Diagnostics Configuration Namespace</span><span class="sxs-lookup"><span data-stu-id="2b3de-122">Diagnostics Configuration Namespace</span></span>  
 <span data-ttu-id="2b3de-123">The XML namespace for the diagnostics configuration file is:</span><span class="sxs-lookup"><span data-stu-id="2b3de-123">The XML namespace for the diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="diagnosticsconfiguration-element"></a><span data-ttu-id="2b3de-124">DiagnosticsConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-124">DiagnosticsConfiguration Element</span></span>  
 <span data-ttu-id="2b3de-125">Added in version 1.3.</span><span class="sxs-lookup"><span data-stu-id="2b3de-125">Added in version 1.3.</span></span>  

 <span data-ttu-id="2b3de-126">The top-level element of the diagnostics configuration file.</span><span class="sxs-lookup"><span data-stu-id="2b3de-126">The top-level element of the diagnostics configuration file.</span></span>  

|<span data-ttu-id="2b3de-127">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-127">Child Elements</span></span>|<span data-ttu-id="2b3de-128">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-128">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-129">**PublicConfig**</span><span class="sxs-lookup"><span data-stu-id="2b3de-129">**PublicConfig**</span></span>|<span data-ttu-id="2b3de-130">Required.</span><span class="sxs-lookup"><span data-stu-id="2b3de-130">Required.</span></span> <span data-ttu-id="2b3de-131">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-131">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2b3de-132">**PrivateConfig**</span><span class="sxs-lookup"><span data-stu-id="2b3de-132">**PrivateConfig**</span></span>|<span data-ttu-id="2b3de-133">Optional.</span><span class="sxs-lookup"><span data-stu-id="2b3de-133">Optional.</span></span> <span data-ttu-id="2b3de-134">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-134">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2b3de-135">**IsEnabled**</span><span class="sxs-lookup"><span data-stu-id="2b3de-135">**IsEnabled**</span></span>|<span data-ttu-id="2b3de-136">Boolean.</span><span class="sxs-lookup"><span data-stu-id="2b3de-136">Boolean.</span></span> <span data-ttu-id="2b3de-137">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-137">See description elsewhere on this page.</span></span>|  

## <a name="publicconfig-element"></a><span data-ttu-id="2b3de-138">PublicConfig Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-138">PublicConfig Element</span></span>  
 <span data-ttu-id="2b3de-139">Describes the public diagnostics configuration.</span><span class="sxs-lookup"><span data-stu-id="2b3de-139">Describes the public diagnostics configuration.</span></span>  

|<span data-ttu-id="2b3de-140">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-140">Child Elements</span></span>|<span data-ttu-id="2b3de-141">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-141">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-142">**WadCfg**</span><span class="sxs-lookup"><span data-stu-id="2b3de-142">**WadCfg**</span></span>|<span data-ttu-id="2b3de-143">Required.</span><span class="sxs-lookup"><span data-stu-id="2b3de-143">Required.</span></span> <span data-ttu-id="2b3de-144">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-144">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2b3de-145">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="2b3de-145">**StorageAccount**</span></span>|<span data-ttu-id="2b3de-146">The name of the Azure Storage account to store the data in.</span><span class="sxs-lookup"><span data-stu-id="2b3de-146">The name of the Azure Storage account to store the data in.</span></span> <span data-ttu-id="2b3de-147">This may also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2b3de-147">This may also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.</span></span>|  
|<span data-ttu-id="2b3de-148">**LocalResourceDirectory**</span><span class="sxs-lookup"><span data-stu-id="2b3de-148">**LocalResourceDirectory**</span></span>|<span data-ttu-id="2b3de-149">The directory on the virtual machine where the Monitoring Agent stores event data.</span><span class="sxs-lookup"><span data-stu-id="2b3de-149">The directory on the virtual machine where the Monitoring Agent stores event data.</span></span> <span data-ttu-id="2b3de-150">If not, set, the default directory is used:</span><span class="sxs-lookup"><span data-stu-id="2b3de-150">If not, set, the default directory is used:</span></span><br /><br /> <span data-ttu-id="2b3de-151">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span><span class="sxs-lookup"><span data-stu-id="2b3de-151">For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`</span></span><br /><br /> <span data-ttu-id="2b3de-152">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span><span class="sxs-lookup"><span data-stu-id="2b3de-152">For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`</span></span><br /><br /> <span data-ttu-id="2b3de-153">Required attributes are:</span><span class="sxs-lookup"><span data-stu-id="2b3de-153">Required attributes are:</span></span><br /><br /> <span data-ttu-id="2b3de-154">- **path** - The directory on the system to be used by Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="2b3de-154">- **path** - The directory on the system to be used by Azure Diagnostics.</span></span><br /><br /> <span data-ttu-id="2b3de-155">- **expandEnvironment** - Controls whether or not environment variables are expanded in the path name.</span><span class="sxs-lookup"><span data-stu-id="2b3de-155">- **expandEnvironment** - Controls whether or not environment variables are expanded in the path name.</span></span>|  

## <a name="wadcfg-element"></a><span data-ttu-id="2b3de-156">WadCFG Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-156">WadCFG Element</span></span>  
 <span data-ttu-id="2b3de-157">Identifies and configures the telemetry data to be collected.</span><span class="sxs-lookup"><span data-stu-id="2b3de-157">Identifies and configures the telemetry data to be collected.</span></span>  

|<span data-ttu-id="2b3de-158">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-158">Child Elements</span></span>|<span data-ttu-id="2b3de-159">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-159">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-160">**DiagnosticMonitorConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2b3de-160">**DiagnosticMonitorConfiguration**</span></span>|<span data-ttu-id="2b3de-161">Required element.</span><span class="sxs-lookup"><span data-stu-id="2b3de-161">Required element.</span></span><br /><br /> <span data-ttu-id="2b3de-162">Optional attributes are:</span><span class="sxs-lookup"><span data-stu-id="2b3de-162">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="2b3de-163">- **overallQuotaInMB** - The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="2b3de-163">- **overallQuotaInMB** - The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics.</span></span> <span data-ttu-id="2b3de-164">The default setting is 5120 MB.</span><span class="sxs-lookup"><span data-stu-id="2b3de-164">The default setting is 5120 MB.</span></span><br /><br /> <span data-ttu-id="2b3de-165">- **useProxyServer** - Configure Azure Diagnostics to use the proxy server settings as set in IE settings.</span><span class="sxs-lookup"><span data-stu-id="2b3de-165">- **useProxyServer** - Configure Azure Diagnostics to use the proxy server settings as set in IE settings.</span></span>|  
|<span data-ttu-id="2b3de-166">**CrashDumps**</span><span class="sxs-lookup"><span data-stu-id="2b3de-166">**CrashDumps**</span></span>|<span data-ttu-id="2b3de-167">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-167">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2b3de-168">**DiagnosticInfrastructureLogs**</span><span class="sxs-lookup"><span data-stu-id="2b3de-168">**DiagnosticInfrastructureLogs**</span></span>|<span data-ttu-id="2b3de-169">Enable collection of logs generated by Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="2b3de-169">Enable collection of logs generated by Azure Diagnostics.</span></span> <span data-ttu-id="2b3de-170">The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself.</span><span class="sxs-lookup"><span data-stu-id="2b3de-170">The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself.</span></span> <span data-ttu-id="2b3de-171">Optional attributes are:</span><span class="sxs-lookup"><span data-stu-id="2b3de-171">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="2b3de-172">- **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.</span><span class="sxs-lookup"><span data-stu-id="2b3de-172">- **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.</span></span><br /><br /> <span data-ttu-id="2b3de-173">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="2b3de-173">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="2b3de-174">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="2b3de-174">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="2b3de-175">**Directories**</span><span class="sxs-lookup"><span data-stu-id="2b3de-175">**Directories**</span></span>|<span data-ttu-id="2b3de-176">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-176">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2b3de-177">**EtwProviders**</span><span class="sxs-lookup"><span data-stu-id="2b3de-177">**EtwProviders**</span></span>|<span data-ttu-id="2b3de-178">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-178">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2b3de-179">**Metrics**</span><span class="sxs-lookup"><span data-stu-id="2b3de-179">**Metrics**</span></span>|<span data-ttu-id="2b3de-180">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-180">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2b3de-181">**PerformanceCounters**</span><span class="sxs-lookup"><span data-stu-id="2b3de-181">**PerformanceCounters**</span></span>|<span data-ttu-id="2b3de-182">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-182">See description elsewhere on this page.</span></span>|  
|<span data-ttu-id="2b3de-183">**WindowsEventLog**</span><span class="sxs-lookup"><span data-stu-id="2b3de-183">**WindowsEventLog**</span></span>|<span data-ttu-id="2b3de-184">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-184">See description elsewhere on this page.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="2b3de-185">CrashDumps Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-185">CrashDumps Element</span></span>  
 <span data-ttu-id="2b3de-186">Enable the collection of crash dumps.</span><span class="sxs-lookup"><span data-stu-id="2b3de-186">Enable the collection of crash dumps.</span></span>  

|<span data-ttu-id="2b3de-187">Attributes</span><span class="sxs-lookup"><span data-stu-id="2b3de-187">Attributes</span></span>|<span data-ttu-id="2b3de-188">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-188">Description</span></span>|  
|----------------|-----------------|  
|<span data-ttu-id="2b3de-189">**containerName**</span><span class="sxs-lookup"><span data-stu-id="2b3de-189">**containerName**</span></span>|<span data-ttu-id="2b3de-190">Optional.</span><span class="sxs-lookup"><span data-stu-id="2b3de-190">Optional.</span></span> <span data-ttu-id="2b3de-191">The name of the blob container in your Azure Storage account to be used to store crash dumps.</span><span class="sxs-lookup"><span data-stu-id="2b3de-191">The name of the blob container in your Azure Storage account to be used to store crash dumps.</span></span>|  
|<span data-ttu-id="2b3de-192">**crashDumpType**</span><span class="sxs-lookup"><span data-stu-id="2b3de-192">**crashDumpType**</span></span>|<span data-ttu-id="2b3de-193">Optional.</span><span class="sxs-lookup"><span data-stu-id="2b3de-193">Optional.</span></span>  <span data-ttu-id="2b3de-194">Configures Azure Diagnostics to collect mini or full crash dumps.</span><span class="sxs-lookup"><span data-stu-id="2b3de-194">Configures Azure Diagnostics to collect mini or full crash dumps.</span></span>|  
|<span data-ttu-id="2b3de-195">**directoryQuotaPercentage**</span><span class="sxs-lookup"><span data-stu-id="2b3de-195">**directoryQuotaPercentage**</span></span>|<span data-ttu-id="2b3de-196">Optional.</span><span class="sxs-lookup"><span data-stu-id="2b3de-196">Optional.</span></span>  <span data-ttu-id="2b3de-197">Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.</span><span class="sxs-lookup"><span data-stu-id="2b3de-197">Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.</span></span>|  

|<span data-ttu-id="2b3de-198">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-198">Child Elements</span></span>|<span data-ttu-id="2b3de-199">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-199">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-200">**CrashDumpConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2b3de-200">**CrashDumpConfiguration**</span></span>|<span data-ttu-id="2b3de-201">Required.</span><span class="sxs-lookup"><span data-stu-id="2b3de-201">Required.</span></span> <span data-ttu-id="2b3de-202">Defines configuration values for each process.</span><span class="sxs-lookup"><span data-stu-id="2b3de-202">Defines configuration values for each process.</span></span><br /><br /> <span data-ttu-id="2b3de-203">The following attribute is also required:</span><span class="sxs-lookup"><span data-stu-id="2b3de-203">The following attribute is also required:</span></span><br /><br /> <span data-ttu-id="2b3de-204">**processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.</span><span class="sxs-lookup"><span data-stu-id="2b3de-204">**processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="2b3de-205">Directories Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-205">Directories Element</span></span>  
 <span data-ttu-id="2b3de-206">Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.</span><span class="sxs-lookup"><span data-stu-id="2b3de-206">Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.</span></span>  

 <span data-ttu-id="2b3de-207">Optional **scheduledTransferPeriod** attribute.</span><span class="sxs-lookup"><span data-stu-id="2b3de-207">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="2b3de-208">See explanation  earlier.</span><span class="sxs-lookup"><span data-stu-id="2b3de-208">See explanation  earlier.</span></span>  

|<span data-ttu-id="2b3de-209">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-209">Child Elements</span></span>|<span data-ttu-id="2b3de-210">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-210">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-211">**DataSources**</span><span class="sxs-lookup"><span data-stu-id="2b3de-211">**DataSources**</span></span>|<span data-ttu-id="2b3de-212">A list of directories to monitor.</span><span class="sxs-lookup"><span data-stu-id="2b3de-212">A list of directories to monitor.</span></span>|  
|<span data-ttu-id="2b3de-213">**FailedRequestLogs**</span><span class="sxs-lookup"><span data-stu-id="2b3de-213">**FailedRequestLogs**</span></span>|<span data-ttu-id="2b3de-214">Including this element in the configuration enables collection of logs about failed requests to an IIS site or application.</span><span class="sxs-lookup"><span data-stu-id="2b3de-214">Including this element in the configuration enables collection of logs about failed requests to an IIS site or application.</span></span> <span data-ttu-id="2b3de-215">You must also enable tracing options under **system.WebServer** in **Web.config**.</span><span class="sxs-lookup"><span data-stu-id="2b3de-215">You must also enable tracing options under **system.WebServer** in **Web.config**.</span></span>|  
|<span data-ttu-id="2b3de-216">**IISLogs**</span><span class="sxs-lookup"><span data-stu-id="2b3de-216">**IISLogs**</span></span>|<span data-ttu-id="2b3de-217">Including this element in the configuration enables the collection of IIS logs:</span><span class="sxs-lookup"><span data-stu-id="2b3de-217">Including this element in the configuration enables the collection of IIS logs:</span></span><br /><br /> <span data-ttu-id="2b3de-218">**containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.</span><span class="sxs-lookup"><span data-stu-id="2b3de-218">**containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="2b3de-219">DataSources Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-219">DataSources Element</span></span>  
 <span data-ttu-id="2b3de-220">A list of directories to monitor.</span><span class="sxs-lookup"><span data-stu-id="2b3de-220">A list of directories to monitor.</span></span>  

|<span data-ttu-id="2b3de-221">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-221">Child Elements</span></span>|<span data-ttu-id="2b3de-222">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-222">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-223">**DirectoryConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2b3de-223">**DirectoryConfiguration**</span></span>|<span data-ttu-id="2b3de-224">Required.</span><span class="sxs-lookup"><span data-stu-id="2b3de-224">Required.</span></span> <span data-ttu-id="2b3de-225">Required attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-225">Required attribute:</span></span><br /><br /> <span data-ttu-id="2b3de-226">**containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.</span><span class="sxs-lookup"><span data-stu-id="2b3de-226">**containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.</span></span>|  

## <a name="directoryconfiguration-element"></a><span data-ttu-id="2b3de-227">DirectoryConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-227">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="2b3de-228">May include either the **Absolute** or **LocalResource** element but not both.</span><span class="sxs-lookup"><span data-stu-id="2b3de-228">May include either the **Absolute** or **LocalResource** element but not both.</span></span>  

|<span data-ttu-id="2b3de-229">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-229">Child Elements</span></span>|<span data-ttu-id="2b3de-230">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-230">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-231">**Absolute**</span><span class="sxs-lookup"><span data-stu-id="2b3de-231">**Absolute**</span></span>|<span data-ttu-id="2b3de-232">The absolute path to the directory to monitor.</span><span class="sxs-lookup"><span data-stu-id="2b3de-232">The absolute path to the directory to monitor.</span></span> <span data-ttu-id="2b3de-233">The following attributes are required:</span><span class="sxs-lookup"><span data-stu-id="2b3de-233">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="2b3de-234">- **Path** - The absolute path to the directory to monitor.</span><span class="sxs-lookup"><span data-stu-id="2b3de-234">- **Path** - The absolute path to the directory to monitor.</span></span><br /><br /> <span data-ttu-id="2b3de-235">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span><span class="sxs-lookup"><span data-stu-id="2b3de-235">- **expandEnvironment** - Configures whether environment variables in Path are expanded.</span></span>|  
|<span data-ttu-id="2b3de-236">**LocalResource**</span><span class="sxs-lookup"><span data-stu-id="2b3de-236">**LocalResource**</span></span>|<span data-ttu-id="2b3de-237">The path relative to a local resource to monitor.</span><span class="sxs-lookup"><span data-stu-id="2b3de-237">The path relative to a local resource to monitor.</span></span> <span data-ttu-id="2b3de-238">Required attributes are:</span><span class="sxs-lookup"><span data-stu-id="2b3de-238">Required attributes are:</span></span><br /><br /> <span data-ttu-id="2b3de-239">- **Name** - The local resource that contains the directory to monitor</span><span class="sxs-lookup"><span data-stu-id="2b3de-239">- **Name** - The local resource that contains the directory to monitor</span></span><br /><br /> <span data-ttu-id="2b3de-240">- **relativePath** - The path relative to Name that contains the directory to monitor</span><span class="sxs-lookup"><span data-stu-id="2b3de-240">- **relativePath** - The path relative to Name that contains the directory to monitor</span></span>|  

## <a name="etwproviders-element"></a><span data-ttu-id="2b3de-241">EtwProviders Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-241">EtwProviders Element</span></span>  
 <span data-ttu-id="2b3de-242">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span><span class="sxs-lookup"><span data-stu-id="2b3de-242">Configures collection of ETW events from EventSource and/or ETW Manifest based providers.</span></span>  

|<span data-ttu-id="2b3de-243">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-243">Child Elements</span></span>|<span data-ttu-id="2b3de-244">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-244">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-245">**EtwEventSourceProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2b3de-245">**EtwEventSourceProviderConfiguration**</span></span>|<span data-ttu-id="2b3de-246">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="2b3de-246">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span> <span data-ttu-id="2b3de-247">Required attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-247">Required attribute:</span></span><br /><br /> <span data-ttu-id="2b3de-248">**provider** - The class name of the EventSource event.</span><span class="sxs-lookup"><span data-stu-id="2b3de-248">**provider** - The class name of the EventSource event.</span></span><br /><br /> <span data-ttu-id="2b3de-249">Optional attributes are:</span><span class="sxs-lookup"><span data-stu-id="2b3de-249">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="2b3de-250">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span><span class="sxs-lookup"><span data-stu-id="2b3de-250">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="2b3de-251">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="2b3de-251">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="2b3de-252">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="2b3de-252">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  
|<span data-ttu-id="2b3de-253">**EtwManifestProviderConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2b3de-253">**EtwManifestProviderConfiguration**</span></span>|<span data-ttu-id="2b3de-254">Required attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-254">Required attribute:</span></span><br /><br /> <span data-ttu-id="2b3de-255">**provider** - The GUID of the event provider</span><span class="sxs-lookup"><span data-stu-id="2b3de-255">**provider** - The GUID of the event provider</span></span><br /><br /> <span data-ttu-id="2b3de-256">Optional attributes are:</span><span class="sxs-lookup"><span data-stu-id="2b3de-256">Optional attributes are:</span></span><br /><br /> <span data-ttu-id="2b3de-257">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span><span class="sxs-lookup"><span data-stu-id="2b3de-257">- **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.</span></span><br /><br /> <span data-ttu-id="2b3de-258">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="2b3de-258">- **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="2b3de-259">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="2b3de-259">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  

## <a name="etweventsourceproviderconfiguration-element"></a><span data-ttu-id="2b3de-260">EtwEventSourceProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-260">EtwEventSourceProviderConfiguration Element</span></span>  
 <span data-ttu-id="2b3de-261">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span><span class="sxs-lookup"><span data-stu-id="2b3de-261">Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).</span></span>  

|<span data-ttu-id="2b3de-262">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-262">Child Elements</span></span>|<span data-ttu-id="2b3de-263">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-263">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-264">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="2b3de-264">**DefaultEvents**</span></span>|<span data-ttu-id="2b3de-265">Optional attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-265">Optional attribute:</span></span><br/><br/> <span data-ttu-id="2b3de-266">**eventDestination** - The name of the table to store the events in</span><span class="sxs-lookup"><span data-stu-id="2b3de-266">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="2b3de-267">**Event**</span><span class="sxs-lookup"><span data-stu-id="2b3de-267">**Event**</span></span>|<span data-ttu-id="2b3de-268">Required attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-268">Required attribute:</span></span><br /><br /> <span data-ttu-id="2b3de-269">**id** - The id of the event.</span><span class="sxs-lookup"><span data-stu-id="2b3de-269">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="2b3de-270">Optional attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-270">Optional attribute:</span></span><br /><br /> <span data-ttu-id="2b3de-271">**eventDestination** - The name of the table to store the events in</span><span class="sxs-lookup"><span data-stu-id="2b3de-271">**eventDestination** - The name of the table to store the events in</span></span>|  

## <a name="etwmanifestproviderconfiguration-element"></a><span data-ttu-id="2b3de-272">EtwManifestProviderConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-272">EtwManifestProviderConfiguration Element</span></span>  

|<span data-ttu-id="2b3de-273">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-273">Child Elements</span></span>|<span data-ttu-id="2b3de-274">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-274">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-275">**DefaultEvents**</span><span class="sxs-lookup"><span data-stu-id="2b3de-275">**DefaultEvents**</span></span>|<span data-ttu-id="2b3de-276">Optional attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-276">Optional attribute:</span></span><br /><br /> <span data-ttu-id="2b3de-277">**eventDestination** - The name of the table to store the events in</span><span class="sxs-lookup"><span data-stu-id="2b3de-277">**eventDestination** - The name of the table to store the events in</span></span>|  
|<span data-ttu-id="2b3de-278">**Event**</span><span class="sxs-lookup"><span data-stu-id="2b3de-278">**Event**</span></span>|<span data-ttu-id="2b3de-279">Required attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-279">Required attribute:</span></span><br /><br /> <span data-ttu-id="2b3de-280">**id** - The id of the event.</span><span class="sxs-lookup"><span data-stu-id="2b3de-280">**id** - The id of the event.</span></span><br /><br /> <span data-ttu-id="2b3de-281">Optional attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-281">Optional attribute:</span></span><br /><br /> <span data-ttu-id="2b3de-282">**eventDestination** - The name of the table to store the events in</span><span class="sxs-lookup"><span data-stu-id="2b3de-282">**eventDestination** - The name of the table to store the events in</span></span>|  

## <a name="metrics-element"></a><span data-ttu-id="2b3de-283">Metrics Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-283">Metrics Element</span></span>  
 <span data-ttu-id="2b3de-284">Enables you to generate a performance counter table that is optimized for fast queries.</span><span class="sxs-lookup"><span data-stu-id="2b3de-284">Enables you to generate a performance counter table that is optimized for fast queries.</span></span> <span data-ttu-id="2b3de-285">Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.</span><span class="sxs-lookup"><span data-stu-id="2b3de-285">Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.</span></span>  

 <span data-ttu-id="2b3de-286">The **resourceId** attribute is required.</span><span class="sxs-lookup"><span data-stu-id="2b3de-286">The **resourceId** attribute is required.</span></span>  <span data-ttu-id="2b3de-287">This is the resource ID of the Virtual Machine you are deploying Azure Diagnostics to.</span><span class="sxs-lookup"><span data-stu-id="2b3de-287">This is the resource ID of the Virtual Machine you are deploying Azure Diagnostics to.</span></span> <span data-ttu-id="2b3de-288">Get the **resourceID** from the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="2b3de-288">Get the **resourceID** from the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="2b3de-289">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span><span class="sxs-lookup"><span data-stu-id="2b3de-289">Select **Browse** -> **Resource Groups** -> **<Name\>**.</span></span> <span data-ttu-id="2b3de-290">Click the **Properties** tile and copy the value from the **ID** field.</span><span class="sxs-lookup"><span data-stu-id="2b3de-290">Click the **Properties** tile and copy the value from the **ID** field.</span></span>  

|<span data-ttu-id="2b3de-291">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-291">Child Elements</span></span>|<span data-ttu-id="2b3de-292">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-292">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-293">**MetricAggregation**</span><span class="sxs-lookup"><span data-stu-id="2b3de-293">**MetricAggregation**</span></span>|<span data-ttu-id="2b3de-294">Required attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-294">Required attribute:</span></span><br /><br /> <span data-ttu-id="2b3de-295">**scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="2b3de-295">**scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute.</span></span> <span data-ttu-id="2b3de-296">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span><span class="sxs-lookup"><span data-stu-id="2b3de-296">The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)</span></span> |  

## <a name="performancecounters-element"></a><span data-ttu-id="2b3de-297">PerformanceCounters Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-297">PerformanceCounters Element</span></span>  
 <span data-ttu-id="2b3de-298">Enables the collection of performance counters.</span><span class="sxs-lookup"><span data-stu-id="2b3de-298">Enables the collection of performance counters.</span></span>  

 <span data-ttu-id="2b3de-299">Optional attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-299">Optional attribute:</span></span>  

 <span data-ttu-id="2b3de-300">Optional **scheduledTransferPeriod** attribute.</span><span class="sxs-lookup"><span data-stu-id="2b3de-300">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="2b3de-301">See explanation earlier.</span><span class="sxs-lookup"><span data-stu-id="2b3de-301">See explanation earlier.</span></span>

|<span data-ttu-id="2b3de-302">Child Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-302">Child Element</span></span>|<span data-ttu-id="2b3de-303">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-303">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="2b3de-304">**PerformanceCounterConfiguration**</span><span class="sxs-lookup"><span data-stu-id="2b3de-304">**PerformanceCounterConfiguration**</span></span>|<span data-ttu-id="2b3de-305">The following attributes are required:</span><span class="sxs-lookup"><span data-stu-id="2b3de-305">The following attributes are required:</span></span><br /><br /> <span data-ttu-id="2b3de-306">- **counterSpecifier** - The name of the performance counter.</span><span class="sxs-lookup"><span data-stu-id="2b3de-306">- **counterSpecifier** - The name of the performance counter.</span></span> <span data-ttu-id="2b3de-307">For example, `\Processor(_Total)\% Processor Time`.</span><span class="sxs-lookup"><span data-stu-id="2b3de-307">For example, `\Processor(_Total)\% Processor Time`.</span></span> <span data-ttu-id="2b3de-308">To get a list of performance counters on your host run the command `typeperf`.</span><span class="sxs-lookup"><span data-stu-id="2b3de-308">To get a list of performance counters on your host run the command `typeperf`.</span></span><br /><br /> <span data-ttu-id="2b3de-309">- **sampleRate** - How often the counter should be sampled.</span><span class="sxs-lookup"><span data-stu-id="2b3de-309">- **sampleRate** - How often the counter should be sampled.</span></span><br /><br /> <span data-ttu-id="2b3de-310">Optional attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-310">Optional attribute:</span></span><br /><br /> <span data-ttu-id="2b3de-311">**unit** - The unit of measure of the counter.</span><span class="sxs-lookup"><span data-stu-id="2b3de-311">**unit** - The unit of measure of the counter.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="2b3de-312">WindowsEventLog Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-312">WindowsEventLog Element</span></span>  
 <span data-ttu-id="2b3de-313">Enables the collection of Windows Event Logs.</span><span class="sxs-lookup"><span data-stu-id="2b3de-313">Enables the collection of Windows Event Logs.</span></span>  

 <span data-ttu-id="2b3de-314">Optional **scheduledTransferPeriod** attribute.</span><span class="sxs-lookup"><span data-stu-id="2b3de-314">Optional **scheduledTransferPeriod** attribute.</span></span> <span data-ttu-id="2b3de-315">See explanation  earlier.</span><span class="sxs-lookup"><span data-stu-id="2b3de-315">See explanation  earlier.</span></span>  

|<span data-ttu-id="2b3de-316">Child Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-316">Child Element</span></span>|<span data-ttu-id="2b3de-317">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-317">Description</span></span>|  
|-------------------|-----------------|  
|<span data-ttu-id="2b3de-318">**DataSource**</span><span class="sxs-lookup"><span data-stu-id="2b3de-318">**DataSource**</span></span>|<span data-ttu-id="2b3de-319">The Windows Event logs to collect.</span><span class="sxs-lookup"><span data-stu-id="2b3de-319">The Windows Event logs to collect.</span></span> <span data-ttu-id="2b3de-320">Required attribute:</span><span class="sxs-lookup"><span data-stu-id="2b3de-320">Required attribute:</span></span><br /><br /> <span data-ttu-id="2b3de-321">**name** - The XPath query describing the windows events to be collected.</span><span class="sxs-lookup"><span data-stu-id="2b3de-321">**name** - The XPath query describing the windows events to be collected.</span></span> <span data-ttu-id="2b3de-322">For example:</span><span class="sxs-lookup"><span data-stu-id="2b3de-322">For example:</span></span><br /><br /> `Application!*[Application[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[Security[(Level <= 3)]`<br /><br /> <span data-ttu-id="2b3de-323">To collect all events, specify “\*”.</span><span class="sxs-lookup"><span data-stu-id="2b3de-323">To collect all events, specify “\*”.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="2b3de-324">Logs Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-324">Logs Element</span></span>  
 <span data-ttu-id="2b3de-325">Present in version 1.0 and 1.1.</span><span class="sxs-lookup"><span data-stu-id="2b3de-325">Present in version 1.0 and 1.1.</span></span> <span data-ttu-id="2b3de-326">Missing in 1.2.</span><span class="sxs-lookup"><span data-stu-id="2b3de-326">Missing in 1.2.</span></span> <span data-ttu-id="2b3de-327">Added back in 1.3.</span><span class="sxs-lookup"><span data-stu-id="2b3de-327">Added back in 1.3.</span></span>  

 <span data-ttu-id="2b3de-328">Defines the buffer configuration for basic Azure logs.</span><span class="sxs-lookup"><span data-stu-id="2b3de-328">Defines the buffer configuration for basic Azure logs.</span></span>  

|<span data-ttu-id="2b3de-329">Attribute</span><span class="sxs-lookup"><span data-stu-id="2b3de-329">Attribute</span></span>|<span data-ttu-id="2b3de-330">Type</span><span class="sxs-lookup"><span data-stu-id="2b3de-330">Type</span></span>|<span data-ttu-id="2b3de-331">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-331">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2b3de-332">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="2b3de-332">**bufferQuotaInMB**</span></span>|<span data-ttu-id="2b3de-333">**unsignedInt**</span><span class="sxs-lookup"><span data-stu-id="2b3de-333">**unsignedInt**</span></span>|<span data-ttu-id="2b3de-334">Optional.</span><span class="sxs-lookup"><span data-stu-id="2b3de-334">Optional.</span></span> <span data-ttu-id="2b3de-335">Specifies the maximum amount of file system storage that is available for the specified data.</span><span class="sxs-lookup"><span data-stu-id="2b3de-335">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="2b3de-336">The default is 0.</span><span class="sxs-lookup"><span data-stu-id="2b3de-336">The default is 0.</span></span>|  
|<span data-ttu-id="2b3de-337">**scheduledTransferLogLevelFilterr**</span><span class="sxs-lookup"><span data-stu-id="2b3de-337">**scheduledTransferLogLevelFilterr**</span></span>|<span data-ttu-id="2b3de-338">**string**</span><span class="sxs-lookup"><span data-stu-id="2b3de-338">**string**</span></span>|<span data-ttu-id="2b3de-339">Optional.</span><span class="sxs-lookup"><span data-stu-id="2b3de-339">Optional.</span></span> <span data-ttu-id="2b3de-340">Specifies the minimum severity level for log entries that are transferred.</span><span class="sxs-lookup"><span data-stu-id="2b3de-340">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="2b3de-341">The default value is **Undefined**, which transfers all logs.</span><span class="sxs-lookup"><span data-stu-id="2b3de-341">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="2b3de-342">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span><span class="sxs-lookup"><span data-stu-id="2b3de-342">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="2b3de-343">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="2b3de-343">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="2b3de-344">**duration**</span><span class="sxs-lookup"><span data-stu-id="2b3de-344">**duration**</span></span>|<span data-ttu-id="2b3de-345">Optional.</span><span class="sxs-lookup"><span data-stu-id="2b3de-345">Optional.</span></span> <span data-ttu-id="2b3de-346">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="2b3de-346">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="2b3de-347">The default is PT0S.</span><span class="sxs-lookup"><span data-stu-id="2b3de-347">The default is PT0S.</span></span>|  
|<span data-ttu-id="2b3de-348">**sinks** Added in 1.5</span><span class="sxs-lookup"><span data-stu-id="2b3de-348">**sinks** Added in 1.5</span></span>|<span data-ttu-id="2b3de-349">**string**</span><span class="sxs-lookup"><span data-stu-id="2b3de-349">**string**</span></span>|<span data-ttu-id="2b3de-350">Optional.</span><span class="sxs-lookup"><span data-stu-id="2b3de-350">Optional.</span></span> <span data-ttu-id="2b3de-351">Points to a sink location to also send diagnostic data.</span><span class="sxs-lookup"><span data-stu-id="2b3de-351">Points to a sink location to also send diagnostic data.</span></span> <span data-ttu-id="2b3de-352">For example, Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2b3de-352">For example, Application Insights.</span></span>|  

## <a name="sinksconfig-element"></a><span data-ttu-id="2b3de-353">SinksConfig Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-353">SinksConfig Element</span></span>  
 <span data-ttu-id="2b3de-354">A list of locations to send diagnostics data to and the configuration associated with those locations.</span><span class="sxs-lookup"><span data-stu-id="2b3de-354">A list of locations to send diagnostics data to and the configuration associated with those locations.</span></span>  

|<span data-ttu-id="2b3de-355">Element Name</span><span class="sxs-lookup"><span data-stu-id="2b3de-355">Element Name</span></span>|<span data-ttu-id="2b3de-356">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-356">Description</span></span>|  
|------------------|-----------------|  
|<span data-ttu-id="2b3de-357">**Sink**</span><span class="sxs-lookup"><span data-stu-id="2b3de-357">**Sink**</span></span>|<span data-ttu-id="2b3de-358">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-358">See description elsewhere on this page.</span></span>|  

## <a name="sink-element"></a><span data-ttu-id="2b3de-359">Sink Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-359">Sink Element</span></span>  
 <span data-ttu-id="2b3de-360">Added in version 1.5.</span><span class="sxs-lookup"><span data-stu-id="2b3de-360">Added in version 1.5.</span></span>  

 <span data-ttu-id="2b3de-361">Defines locations to send diagnostic data to.</span><span class="sxs-lookup"><span data-stu-id="2b3de-361">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="2b3de-362">For example, the Application Insights service.</span><span class="sxs-lookup"><span data-stu-id="2b3de-362">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="2b3de-363">Attribute</span><span class="sxs-lookup"><span data-stu-id="2b3de-363">Attribute</span></span>|<span data-ttu-id="2b3de-364">Type</span><span class="sxs-lookup"><span data-stu-id="2b3de-364">Type</span></span>|<span data-ttu-id="2b3de-365">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-365">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="2b3de-366">**name**</span><span class="sxs-lookup"><span data-stu-id="2b3de-366">**name**</span></span>|<span data-ttu-id="2b3de-367">string</span><span class="sxs-lookup"><span data-stu-id="2b3de-367">string</span></span>|<span data-ttu-id="2b3de-368">A string identifying the sinkname.</span><span class="sxs-lookup"><span data-stu-id="2b3de-368">A string identifying the sinkname.</span></span>|  

|<span data-ttu-id="2b3de-369">Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-369">Element</span></span>|<span data-ttu-id="2b3de-370">Type</span><span class="sxs-lookup"><span data-stu-id="2b3de-370">Type</span></span>|<span data-ttu-id="2b3de-371">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-371">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="2b3de-372">**Application Insights**</span><span class="sxs-lookup"><span data-stu-id="2b3de-372">**Application Insights**</span></span>|<span data-ttu-id="2b3de-373">string</span><span class="sxs-lookup"><span data-stu-id="2b3de-373">string</span></span>|<span data-ttu-id="2b3de-374">Used only when sending data to Application Insights.</span><span class="sxs-lookup"><span data-stu-id="2b3de-374">Used only when sending data to Application Insights.</span></span> <span data-ttu-id="2b3de-375">Contain the Instrumentation Key for an active Application Insights account that you have access to.</span><span class="sxs-lookup"><span data-stu-id="2b3de-375">Contain the Instrumentation Key for an active Application Insights account that you have access to.</span></span>|  
|<span data-ttu-id="2b3de-376">**Channels**</span><span class="sxs-lookup"><span data-stu-id="2b3de-376">**Channels**</span></span>|<span data-ttu-id="2b3de-377">string</span><span class="sxs-lookup"><span data-stu-id="2b3de-377">string</span></span>|<span data-ttu-id="2b3de-378">One for each additional filtering that stream that you</span><span class="sxs-lookup"><span data-stu-id="2b3de-378">One for each additional filtering that stream that you</span></span>|  

## <a name="channels-element"></a><span data-ttu-id="2b3de-379">Channels Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-379">Channels Element</span></span>  
 <span data-ttu-id="2b3de-380">Added in version 1.5.</span><span class="sxs-lookup"><span data-stu-id="2b3de-380">Added in version 1.5.</span></span>  

 <span data-ttu-id="2b3de-381">Defines filters for streams of log data passing through a sink.</span><span class="sxs-lookup"><span data-stu-id="2b3de-381">Defines filters for streams of log data passing through a sink.</span></span>  

|<span data-ttu-id="2b3de-382">Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-382">Element</span></span>|<span data-ttu-id="2b3de-383">Type</span><span class="sxs-lookup"><span data-stu-id="2b3de-383">Type</span></span>|<span data-ttu-id="2b3de-384">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-384">Description</span></span>|  
|-------------|----------|-----------------|  
|<span data-ttu-id="2b3de-385">**Channel**</span><span class="sxs-lookup"><span data-stu-id="2b3de-385">**Channel**</span></span>|<span data-ttu-id="2b3de-386">string</span><span class="sxs-lookup"><span data-stu-id="2b3de-386">string</span></span>|<span data-ttu-id="2b3de-387">See description elsewhere on this page.</span><span class="sxs-lookup"><span data-stu-id="2b3de-387">See description elsewhere on this page.</span></span>|  

## <a name="channel-element"></a><span data-ttu-id="2b3de-388">Channel Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-388">Channel Element</span></span>  
 <span data-ttu-id="2b3de-389">Added in version 1.5.</span><span class="sxs-lookup"><span data-stu-id="2b3de-389">Added in version 1.5.</span></span>  

 <span data-ttu-id="2b3de-390">Defines locations to send diagnostic data to.</span><span class="sxs-lookup"><span data-stu-id="2b3de-390">Defines locations to send diagnostic data to.</span></span> <span data-ttu-id="2b3de-391">For example, the Application Insights service.</span><span class="sxs-lookup"><span data-stu-id="2b3de-391">For example, the Application Insights service.</span></span>  

|<span data-ttu-id="2b3de-392">Attributes</span><span class="sxs-lookup"><span data-stu-id="2b3de-392">Attributes</span></span>|<span data-ttu-id="2b3de-393">Type</span><span class="sxs-lookup"><span data-stu-id="2b3de-393">Type</span></span>|<span data-ttu-id="2b3de-394">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-394">Description</span></span>|  
|----------------|----------|-----------------|  
|<span data-ttu-id="2b3de-395">**logLevel**</span><span class="sxs-lookup"><span data-stu-id="2b3de-395">**logLevel**</span></span>|<span data-ttu-id="2b3de-396">**string**</span><span class="sxs-lookup"><span data-stu-id="2b3de-396">**string**</span></span>|<span data-ttu-id="2b3de-397">Specifies the minimum severity level for log entries that are transferred.</span><span class="sxs-lookup"><span data-stu-id="2b3de-397">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="2b3de-398">The default value is **Undefined**, which transfers all logs.</span><span class="sxs-lookup"><span data-stu-id="2b3de-398">The default value is **Undefined**, which transfers all logs.</span></span> <span data-ttu-id="2b3de-399">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span><span class="sxs-lookup"><span data-stu-id="2b3de-399">Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="2b3de-400">**name**</span><span class="sxs-lookup"><span data-stu-id="2b3de-400">**name**</span></span>|<span data-ttu-id="2b3de-401">**string**</span><span class="sxs-lookup"><span data-stu-id="2b3de-401">**string**</span></span>|<span data-ttu-id="2b3de-402">A unique name of the channel to refer to</span><span class="sxs-lookup"><span data-stu-id="2b3de-402">A unique name of the channel to refer to</span></span>|  

## <a name="privateconfig-element"></a><span data-ttu-id="2b3de-403">PrivateConfig Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-403">PrivateConfig Element</span></span>  
 <span data-ttu-id="2b3de-404">Added in version 1.3.</span><span class="sxs-lookup"><span data-stu-id="2b3de-404">Added in version 1.3.</span></span>  

 <span data-ttu-id="2b3de-405">Optional</span><span class="sxs-lookup"><span data-stu-id="2b3de-405">Optional</span></span>  

 <span data-ttu-id="2b3de-406">Stores the private details of the storage account (name, key, and endpoint).</span><span class="sxs-lookup"><span data-stu-id="2b3de-406">Stores the private details of the storage account (name, key, and endpoint).</span></span> <span data-ttu-id="2b3de-407">This information is sent to the virtual machine, but cannot be retrieved from it.</span><span class="sxs-lookup"><span data-stu-id="2b3de-407">This information is sent to the virtual machine, but cannot be retrieved from it.</span></span>  

|<span data-ttu-id="2b3de-408">Child Elements</span><span class="sxs-lookup"><span data-stu-id="2b3de-408">Child Elements</span></span>|<span data-ttu-id="2b3de-409">Description</span><span class="sxs-lookup"><span data-stu-id="2b3de-409">Description</span></span>|  
|--------------------|-----------------|  
|<span data-ttu-id="2b3de-410">**StorageAccount**</span><span class="sxs-lookup"><span data-stu-id="2b3de-410">**StorageAccount**</span></span>|<span data-ttu-id="2b3de-411">The storage account to use.</span><span class="sxs-lookup"><span data-stu-id="2b3de-411">The storage account to use.</span></span> <span data-ttu-id="2b3de-412">The following attributes are required</span><span class="sxs-lookup"><span data-stu-id="2b3de-412">The following attributes are required</span></span><br /><br /> <span data-ttu-id="2b3de-413">- **name** - The name of the storage account.</span><span class="sxs-lookup"><span data-stu-id="2b3de-413">- **name** - The name of the storage account.</span></span><br /><br /> <span data-ttu-id="2b3de-414">- **key** - The key to the storage account.</span><span class="sxs-lookup"><span data-stu-id="2b3de-414">- **key** - The key to the storage account.</span></span><br /><br /> <span data-ttu-id="2b3de-415">- **endpoint** - The endpoint to access the storage account.</span><span class="sxs-lookup"><span data-stu-id="2b3de-415">- **endpoint** - The endpoint to access the storage account.</span></span>|  

## <a name="isenabled-element"></a><span data-ttu-id="2b3de-416">IsEnabled Element</span><span class="sxs-lookup"><span data-stu-id="2b3de-416">IsEnabled Element</span></span>  
 <span data-ttu-id="2b3de-417">Boolean.</span><span class="sxs-lookup"><span data-stu-id="2b3de-417">Boolean.</span></span> <span data-ttu-id="2b3de-418">Use `true` to enable the diagnostics or `false` to disable the diagnostics.</span><span class="sxs-lookup"><span data-stu-id="2b3de-418">Use `true` to enable the diagnostics or `false` to disable the diagnostics.</span></span>
