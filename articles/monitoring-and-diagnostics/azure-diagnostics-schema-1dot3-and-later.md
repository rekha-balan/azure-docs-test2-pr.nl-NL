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
# <a name="azure-diagnostics-13-14-15-configuration-schema"></a>Azure Diagnostics 1.3, 1.4, 1.5 Configuration Schema
> [!NOTE]
> Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.  This page is only relevant if you are using one of these services.
>

Azure Diagnostics is used in conjunction with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.

The Azure Diagnostics configuration file is used to set diagnostic configuration settings when the diagnostics monitor starts.  

This page is valid for versions 1.3, 1.4 and 1.5 (Azure SDK 2.4 and newer). Newer configuration sections are commented to show in what version they were added.  

 Download the public configuration file schema definition by executing the following PowerShell command:  

```powershell  
(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File –Encoding utf8 -FilePath 'C:\temp\WadConfig.xsd'  
```  

 For more information about using Azure Diagnostics, see [Enabling Diagnostics in Azure Cloud Services](http://azure.microsoft.com/documentation/articles/cloud-services-dotnet-diagnostics/).  

## <a name="example-of-the-diagnostics-configuration-file"></a>Example of the diagnostics configuration file  
 The following example shows a typical diagnostics configuration file:  

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

Here is the JSON equivalent of the previous XML configuration file.  
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

## <a name="reading-this-page"></a>Reading this page  
 The tags following are roughly in order shown in the preceding example.  If you don't see a full description where you expect it, search the page for the element or attribute.  

## <a name="common-attribute-types"></a>Common Attribute Types  
 **scheduledTransferPeriod** attribute appears in several elements. It is the interval between scheduled transfers to storage rounded up to the nearest minute. The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp)

## <a name="diagnostics-configuration-namespace"></a>Diagnostics Configuration Namespace  
 The XML namespace for the diagnostics configuration file is:  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="diagnosticsconfiguration-element"></a>DiagnosticsConfiguration Element  
 Added in version 1.3.  

 The top-level element of the diagnostics configuration file.  

|Child Elements|Description|  
|--------------------|-----------------|  
|**PublicConfig**|Required. See description elsewhere on this page.|  
|**PrivateConfig**|Optional. See description elsewhere on this page.|  
|**IsEnabled**|Boolean. See description elsewhere on this page.|  

## <a name="publicconfig-element"></a>PublicConfig Element  
 Describes the public diagnostics configuration.  

|Child Elements|Description|  
|--------------------|-----------------|  
|**WadCfg**|Required. See description elsewhere on this page.|  
|**StorageAccount**|The name of the Azure Storage account to store the data in. This may also be specified as a parameter when executing the Set-AzureServiceDiagnosticsExtension cmdlet.|  
|**LocalResourceDirectory**|The directory on the virtual machine where the Monitoring Agent stores event data. If not, set, the default directory is used:<br /><br /> For a Worker/web role: `C:\Resources\<guid>\directory\<guid>.<RoleName.DiagnosticStore\`<br /><br /> For a Virtual Machine: `C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<WADVersion>\WAD<WADVersion>`<br /><br /> Required attributes are:<br /><br /> - **path** - The directory on the system to be used by Azure Diagnostics.<br /><br /> - **expandEnvironment** - Controls whether or not environment variables are expanded in the path name.|  

## <a name="wadcfg-element"></a>WadCFG Element  
 Identifies and configures the telemetry data to be collected.  

|Child Elements|Description|  
|--------------------|-----------------|  
|**DiagnosticMonitorConfiguration**|Required element.<br /><br /> Optional attributes are:<br /><br /> - **overallQuotaInMB** - The maximum amount of local disk space that may be consumed by the various types of diagnostic data collected by Azure Diagnostics. The default setting is 5120 MB.<br /><br /> - **useProxyServer** - Configure Azure Diagnostics to use the proxy server settings as set in IE settings.|  
|**CrashDumps**|See description elsewhere on this page.|  
|**DiagnosticInfrastructureLogs**|Enable collection of logs generated by Azure Diagnostics. The diagnostic infrastructure logs are useful for troubleshooting the diagnostics system itself. Optional attributes are:<br /><br /> - **scheduledTransferLogLevelFilter** - Configures the minimum severity level of the logs collected.<br /><br /> - **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute. The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**Directories**|See description elsewhere on this page.|  
|**EtwProviders**|See description elsewhere on this page.|  
|**Metrics**|See description elsewhere on this page.|  
|**PerformanceCounters**|See description elsewhere on this page.|  
|**WindowsEventLog**|See description elsewhere on this page.|  

## <a name="crashdumps-element"></a>CrashDumps Element  
 Enable the collection of crash dumps.  

|Attributes|Description|  
|----------------|-----------------|  
|**containerName**|Optional. The name of the blob container in your Azure Storage account to be used to store crash dumps.|  
|**crashDumpType**|Optional.  Configures Azure Diagnostics to collect mini or full crash dumps.|  
|**directoryQuotaPercentage**|Optional.  Configures the percentage of **overallQuotaInMB** to be reserved for crash dumps on the VM.|  

|Child Elements|Description|  
|--------------------|-----------------|  
|**CrashDumpConfiguration**|Required. Defines configuration values for each process.<br /><br /> The following attribute is also required:<br /><br /> **processName** - The name of the process you want Azure Diagnostics to collect a crash dump for.|  

## <a name="directories-element"></a>Directories Element  
 Enables the collection of the contents of a directory, IIS failed access request logs and/or IIS logs.  

 Optional **scheduledTransferPeriod** attribute. See explanation  earlier.  

|Child Elements|Description|  
|--------------------|-----------------|  
|**DataSources**|A list of directories to monitor.|  
|**FailedRequestLogs**|Including this element in the configuration enables collection of logs about failed requests to an IIS site or application. You must also enable tracing options under **system.WebServer** in **Web.config**.|  
|**IISLogs**|Including this element in the configuration enables the collection of IIS logs:<br /><br /> **containerName** - The name of the blob container in your Azure Storage account to be used to store the IIS logs.|  

## <a name="datasources-element"></a>DataSources Element  
 A list of directories to monitor.  

|Child Elements|Description|  
|--------------------|-----------------|  
|**DirectoryConfiguration**|Required. Required attribute:<br /><br /> **containerName** - The name of the blob container in your Azure Storage account that to be used to store the log files.|  

## <a name="directoryconfiguration-element"></a>DirectoryConfiguration Element  
 May include either the **Absolute** or **LocalResource** element but not both.  

|Child Elements|Description|  
|--------------------|-----------------|  
|**Absolute**|The absolute path to the directory to monitor. The following attributes are required:<br /><br /> - **Path** - The absolute path to the directory to monitor.<br /><br /> - **expandEnvironment** - Configures whether environment variables in Path are expanded.|  
|**LocalResource**|The path relative to a local resource to monitor. Required attributes are:<br /><br /> - **Name** - The local resource that contains the directory to monitor<br /><br /> - **relativePath** - The path relative to Name that contains the directory to monitor|  

## <a name="etwproviders-element"></a>EtwProviders Element  
 Configures collection of ETW events from EventSource and/or ETW Manifest based providers.  

|Child Elements|Description|  
|--------------------|-----------------|  
|**EtwEventSourceProviderConfiguration**|Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx). Required attribute:<br /><br /> **provider** - The class name of the EventSource event.<br /><br /> Optional attributes are:<br /><br /> - **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.<br /><br /> - **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute. The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  
|**EtwManifestProviderConfiguration**|Required attribute:<br /><br /> **provider** - The GUID of the event provider<br /><br /> Optional attributes are:<br /><br /> - **scheduledTransferLogLevelFilter** - The minimum severity level to transfer to your storage account.<br /><br /> - **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute. The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  

## <a name="etweventsourceproviderconfiguration-element"></a>EtwEventSourceProviderConfiguration Element  
 Configures collection of events generated from [EventSource Class](http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource\(v=vs.110\).aspx).  

|Child Elements|Description|  
|--------------------|-----------------|  
|**DefaultEvents**|Optional attribute:<br/><br/> **eventDestination** - The name of the table to store the events in|  
|**Event**|Required attribute:<br /><br /> **id** - The id of the event.<br /><br /> Optional attribute:<br /><br /> **eventDestination** - The name of the table to store the events in|  

## <a name="etwmanifestproviderconfiguration-element"></a>EtwManifestProviderConfiguration Element  

|Child Elements|Description|  
|--------------------|-----------------|  
|**DefaultEvents**|Optional attribute:<br /><br /> **eventDestination** - The name of the table to store the events in|  
|**Event**|Required attribute:<br /><br /> **id** - The id of the event.<br /><br /> Optional attribute:<br /><br /> **eventDestination** - The name of the table to store the events in|  

## <a name="metrics-element"></a>Metrics Element  
 Enables you to generate a performance counter table that is optimized for fast queries. Each performance counter that is defined in the **PerformanceCounters** element is stored in the Metrics table in addition to the Performance Counter table.  

 The **resourceId** attribute is required.  This is the resource ID of the Virtual Machine you are deploying Azure Diagnostics to. Get the **resourceID** from the [Azure portal](https://portal.azure.com). Select **Browse** -> **Resource Groups** -> **<Name\>**. Click the **Properties** tile and copy the value from the **ID** field.  

|Child Elements|Description|  
|--------------------|-----------------|  
|**MetricAggregation**|Required attribute:<br /><br /> **scheduledTransferPeriod** - The interval between scheduled transfers to storage rounded up to the nearest minute. The value is an [XML “Duration Data Type.”](http://www.w3schools.com/schema/schema_dtypes_date.asp) |  

## <a name="performancecounters-element"></a>PerformanceCounters Element  
 Enables the collection of performance counters.  

 Optional attribute:  

 Optional **scheduledTransferPeriod** attribute. See explanation earlier.

|Child Element|Description|  
|-------------------|-----------------|  
|**PerformanceCounterConfiguration**|The following attributes are required:<br /><br /> - **counterSpecifier** - The name of the performance counter. For example, `\Processor(_Total)\% Processor Time`. To get a list of performance counters on your host run the command `typeperf`.<br /><br /> - **sampleRate** - How often the counter should be sampled.<br /><br /> Optional attribute:<br /><br /> **unit** - The unit of measure of the counter.|  

## <a name="windowseventlog-element"></a>WindowsEventLog Element  
 Enables the collection of Windows Event Logs.  

 Optional **scheduledTransferPeriod** attribute. See explanation  earlier.  

|Child Element|Description|  
|-------------------|-----------------|  
|**DataSource**|The Windows Event logs to collect. Required attribute:<br /><br /> **name** - The XPath query describing the windows events to be collected. For example:<br /><br /> `Application!*[Application[(Level <=3)]], System!*[System[(Level <=3)]], System!*[System[Provider[@Name='Microsoft Antimalware']]], Security!*[Security[(Level <= 3)]`<br /><br /> To collect all events, specify “*”.|  

## <a name="logs-element"></a>Logs Element  
 Present in version 1.0 and 1.1. Missing in 1.2. Added back in 1.3.  

 Defines the buffer configuration for basic Azure logs.  

|Attribute|Type|Description|  
|---------------|----------|-----------------|  
|**bufferQuotaInMB**|**unsignedInt**|Optional. Specifies the maximum amount of file system storage that is available for the specified data.<br /><br /> The default is 0.|  
|**scheduledTransferLogLevelFilterr**|**string**|Optional. Specifies the minimum severity level for log entries that are transferred. The default value is **Undefined**, which transfers all logs. Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.|  
|**scheduledTransferPeriod**|**duration**|Optional. Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.<br /><br /> The default is PT0S.|  
|**sinks** Added in 1.5|**string**|Optional. Points to a sink location to also send diagnostic data. For example, Application Insights.|  

## <a name="sinksconfig-element"></a>SinksConfig Element  
 A list of locations to send diagnostics data to and the configuration associated with those locations.  

|Element Name|Description|  
|------------------|-----------------|  
|**Sink**|See description elsewhere on this page.|  

## <a name="sink-element"></a>Sink Element  
 Added in version 1.5.  

 Defines locations to send diagnostic data to. For example, the Application Insights service.  

|Attribute|Type|Description|  
|---------------|----------|-----------------|  
|**name**|string|A string identifying the sinkname.|  

|Element|Type|Description|  
|-------------|----------|-----------------|  
|**Application Insights**|string|Used only when sending data to Application Insights. Contain the Instrumentation Key for an active Application Insights account that you have access to.|  
|**Channels**|string|One for each additional filtering that stream that you|  

## <a name="channels-element"></a>Channels Element  
 Added in version 1.5.  

 Defines filters for streams of log data passing through a sink.  

|Element|Type|Description|  
|-------------|----------|-----------------|  
|**Channel**|string|See description elsewhere on this page.|  

## <a name="channel-element"></a>Channel Element  
 Added in version 1.5.  

 Defines locations to send diagnostic data to. For example, the Application Insights service.  

|Attributes|Type|Description|  
|----------------|----------|-----------------|  
|**logLevel**|**string**|Specifies the minimum severity level for log entries that are transferred. The default value is **Undefined**, which transfers all logs. Other possible values (in order of most to least information) are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.|  
|**name**|**string**|A unique name of the channel to refer to|  

## <a name="privateconfig-element"></a>PrivateConfig Element  
 Added in version 1.3.  

 Optional  

 Stores the private details of the storage account (name, key, and endpoint). This information is sent to the virtual machine, but cannot be retrieved from it.  

|Child Elements|Description|  
|--------------------|-----------------|  
|**StorageAccount**|The storage account to use. The following attributes are required<br /><br /> - **name** - The name of the storage account.<br /><br /> - **key** - The key to the storage account.<br /><br /> - **endpoint** - The endpoint to access the storage account.|  

## <a name="isenabled-element"></a>IsEnabled Element  
 Boolean. Use `true` to enable the diagnostics or `false` to disable the diagnostics.
