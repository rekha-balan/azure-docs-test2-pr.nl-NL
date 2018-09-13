---
title: How to use Azure diagnostics (.NET) with Cloud Services | Microsoft Docs
description: Using Azure diagnostics to gather data from Azure cloud Services for debugging, measuring performance, monitoring, traffic analysis, and more.
services: cloud-services
documentationcenter: .net
author: jpconnock
manager: timlt
editor: ''
ms.assetid: 89623a0e-4e78-4b67-a446-7d19a35a44be
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/22/2017
ms.author: jeconnoc
ms.openlocfilehash: f9f26f14944986bc673a3b7529adb055ad16d058
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784113"
---
# <a name="enabling-azure-diagnostics-in-azure-cloud-services"></a><span data-ttu-id="c408d-103">Enabling Azure Diagnostics in Azure Cloud Services</span><span class="sxs-lookup"><span data-stu-id="c408d-103">Enabling Azure Diagnostics in Azure Cloud Services</span></span>
<span data-ttu-id="c408d-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="c408d-104">See [Azure Diagnostics Overview](../azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-worker-role"></a><span data-ttu-id="c408d-105">How to Enable Diagnostics in a Worker Role</span><span class="sxs-lookup"><span data-stu-id="c408d-105">How to Enable Diagnostics in a Worker Role</span></span>
<span data-ttu-id="c408d-106">This walkthrough describes how to implement an Azure worker role that emits telemetry data using the .NET EventSource class.</span><span class="sxs-lookup"><span data-stu-id="c408d-106">This walkthrough describes how to implement an Azure worker role that emits telemetry data using the .NET EventSource class.</span></span> <span data-ttu-id="c408d-107">Azure Diagnostics is used to collect the telemetry data and store it in an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="c408d-107">Azure Diagnostics is used to collect the telemetry data and store it in an Azure storage account.</span></span> <span data-ttu-id="c408d-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of the solution in Azure SDKs for .NET 2.4 and earlier.</span><span class="sxs-lookup"><span data-stu-id="c408d-108">When creating a worker role, Visual Studio automatically enables Diagnostics 1.0 as part of the solution in Azure SDKs for .NET 2.4 and earlier.</span></span> <span data-ttu-id="c408d-109">The following instructions describe the process for creating the worker role, disabling Diagnostics 1.0 from the solution, and deploying Diagnostics 1.2 or 1.3 to your worker role.</span><span class="sxs-lookup"><span data-stu-id="c408d-109">The following instructions describe the process for creating the worker role, disabling Diagnostics 1.0 from the solution, and deploying Diagnostics 1.2 or 1.3 to your worker role.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c408d-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c408d-110">Prerequisites</span></span>
<span data-ttu-id="c408d-111">This article assumes you have an Azure subscription and are using Visual Studio with the Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="c408d-111">This article assumes you have an Azure subscription and are using Visual Studio with the Azure SDK.</span></span> <span data-ttu-id="c408d-112">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="c408d-112">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="c408d-113">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="c408d-113">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-worker-role"></a><span data-ttu-id="c408d-114">Step 1: Create a Worker Role</span><span class="sxs-lookup"><span data-stu-id="c408d-114">Step 1: Create a Worker Role</span></span>
1. <span data-ttu-id="c408d-115">Launch **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="c408d-115">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="c408d-116">Create an **Azure Cloud Service** project from the **Cloud** template that targets .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="c408d-116">Create an **Azure Cloud Service** project from the **Cloud** template that targets .NET Framework 4.5.</span></span>  <span data-ttu-id="c408d-117">Name the project "WadExample" and click Ok.</span><span class="sxs-lookup"><span data-stu-id="c408d-117">Name the project "WadExample" and click Ok.</span></span>
3. <span data-ttu-id="c408d-118">Select **Worker Role** and click Ok.</span><span class="sxs-lookup"><span data-stu-id="c408d-118">Select **Worker Role** and click Ok.</span></span> <span data-ttu-id="c408d-119">The project will be created.</span><span class="sxs-lookup"><span data-stu-id="c408d-119">The project will be created.</span></span>
4. <span data-ttu-id="c408d-120">In **Solution Explorer**, double-click the **WorkerRole1** properties file.</span><span class="sxs-lookup"><span data-stu-id="c408d-120">In **Solution Explorer**, double-click the **WorkerRole1** properties file.</span></span>
5. <span data-ttu-id="c408d-121">In the **Configuration** tab, un-check **Enable Diagnostics** to disable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span><span class="sxs-lookup"><span data-stu-id="c408d-121">In the **Configuration** tab, un-check **Enable Diagnostics** to disable Diagnostics 1.0 (Azure SDK 2.4 and earlier).</span></span>
6. <span data-ttu-id="c408d-122">Build your solution to verify that you have no errors.</span><span class="sxs-lookup"><span data-stu-id="c408d-122">Build your solution to verify that you have no errors.</span></span>

### <a name="step-2-instrument-your-code"></a><span data-ttu-id="c408d-123">Step 2: Instrument your code</span><span class="sxs-lookup"><span data-stu-id="c408d-123">Step 2: Instrument your code</span></span>
<span data-ttu-id="c408d-124">Replace the contents of WorkerRole.cs with the following code.</span><span class="sxs-lookup"><span data-stu-id="c408d-124">Replace the contents of WorkerRole.cs with the following code.</span></span> <span data-ttu-id="c408d-125">The class SampleEventSourceWriter, inherited from the [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="c408d-125">The class SampleEventSourceWriter, inherited from the [EventSource Class][EventSource Class], implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="c408d-126">The first parameter to the **WriteEvent** method defines the ID for the respective event.</span><span class="sxs-lookup"><span data-stu-id="c408d-126">The first parameter to the **WriteEvent** method defines the ID for the respective event.</span></span> <span data-ttu-id="c408d-127">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="c408d-127">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

```csharp
using Microsoft.WindowsAzure.ServiceRuntime;
using System;
using System.Diagnostics;
using System.Diagnostics.Tracing;
using System.Net;
using System.Threading;

namespace WorkerRole1
{
    sealed class SampleEventSourceWriter : EventSource
    {
        public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
        public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); }// Cast enums to int for efficient logging.
        public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
        public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
        public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }

    }

    enum MyColor
    {
        Red,
        Blue,
        Green
    }

    [Flags]
    enum MyFlags
    {
        Flag1 = 1,
        Flag2 = 2,
        Flag3 = 4
    }

    public class WorkerRole : RoleEntryPoint
    {
        public override void Run()
        {
            // This is a sample worker implementation. Replace with your logic.
            Trace.TraceInformation("WorkerRole1 entry point called");

            int value = 0;

            while (true)
            {
                Thread.Sleep(10000);
                Trace.TraceInformation("Working");

                // Emit several events every time we go through the loop
                for (int i = 0; i < 6; i++)
                {
                    SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
                }

                for (int i = 0; i < 3; i++)
                {
                    SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                    SampleEventSourceWriter.Log.SetOther(true, 123456789);
                }

                if (value == int.MaxValue) value = 0;
                SampleEventSourceWriter.Log.HighFreq(value++);
            }
        }

        public override bool OnStart()
        {
            // Set the maximum number of concurrent connections
            ServicePointManager.DefaultConnectionLimit = 12;

            // For information on handling configuration changes
            // see the MSDN topic at http://go.microsoft.com/fwlink/?LinkId=166357.

            return base.OnStart();
        }
    }
}
```


### <a name="step-3-deploy-your-worker-role"></a><span data-ttu-id="c408d-128">Step 3: Deploy your Worker Role</span><span class="sxs-lookup"><span data-stu-id="c408d-128">Step 3: Deploy your Worker Role</span></span>

[!INCLUDE [cloud-services-wad-warning](../../includes/cloud-services-wad-warning.md)]

1. <span data-ttu-id="c408d-129">Deploy your worker role to Azure from within Visual Studio by selecting the **WadExample** project in the Solution Explorer then **Publish** from the **Build** menu.</span><span class="sxs-lookup"><span data-stu-id="c408d-129">Deploy your worker role to Azure from within Visual Studio by selecting the **WadExample** project in the Solution Explorer then **Publish** from the **Build** menu.</span></span>
2. <span data-ttu-id="c408d-130">Choose your subscription.</span><span class="sxs-lookup"><span data-stu-id="c408d-130">Choose your subscription.</span></span>
3. <span data-ttu-id="c408d-131">In the **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span><span class="sxs-lookup"><span data-stu-id="c408d-131">In the **Microsoft Azure Publish Settings** dialog, select **Create New…**.</span></span>
4. <span data-ttu-id="c408d-132">In the **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span><span class="sxs-lookup"><span data-stu-id="c408d-132">In the **Create Cloud Service and Storage Account** dialog, enter a **Name** (for example, "WadExample") and select a region or affinity group.</span></span>
5. <span data-ttu-id="c408d-133">Set the **Environment** to **Staging**.</span><span class="sxs-lookup"><span data-stu-id="c408d-133">Set the **Environment** to **Staging**.</span></span>
6. <span data-ttu-id="c408d-134">Modify any other **Settings** as appropriate and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="c408d-134">Modify any other **Settings** as appropriate and click **Publish**.</span></span>
7. <span data-ttu-id="c408d-135">After deployment has completed, verify in the Azure portal that your cloud service is in a **Running** state.</span><span class="sxs-lookup"><span data-stu-id="c408d-135">After deployment has completed, verify in the Azure portal that your cloud service is in a **Running** state.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-file-and-install-the-extension"></a><span data-ttu-id="c408d-136">Step 4: Create your Diagnostics configuration file and install the extension</span><span class="sxs-lookup"><span data-stu-id="c408d-136">Step 4: Create your Diagnostics configuration file and install the extension</span></span>
1. <span data-ttu-id="c408d-137">Download the public configuration file schema definition by executing the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="c408d-137">Download the public configuration file schema definition by executing the following PowerShell command:</span></span>

    ```powershell
    (Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'
    ```
2. <span data-ttu-id="c408d-138">Add an XML file to your **WorkerRole1** project by right-clicking on the **WorkerRole1** project and select **Add** -> **New Item…**</span><span class="sxs-lookup"><span data-stu-id="c408d-138">Add an XML file to your **WorkerRole1** project by right-clicking on the **WorkerRole1** project and select **Add** -> **New Item…**</span></span><span data-ttu-id="c408d-139"> -> *\*Visual C# items** -> *\*Data** -> *\*XML File*\*.</span><span class="sxs-lookup"><span data-stu-id="c408d-139"> -> *\*Visual C# items** -> *\*Data** -> *\*XML File*\*.</span></span> <span data-ttu-id="c408d-140">Name the file "WadExample.xml".</span><span class="sxs-lookup"><span data-stu-id="c408d-140">Name the file "WadExample.xml".</span></span>

   ![CloudServices_diag_add_xml](./media/cloud-services-dotnet-diagnostics/AddXmlFile.png)
3. <span data-ttu-id="c408d-142">Associate the WadConfig.xsd with the configuration file.</span><span class="sxs-lookup"><span data-stu-id="c408d-142">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="c408d-143">Make sure the WadExample.xml editor window is the active window.</span><span class="sxs-lookup"><span data-stu-id="c408d-143">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="c408d-144">Press **F4** to open the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="c408d-144">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="c408d-145">Click the **Schemas** property in the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="c408d-145">Click the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="c408d-146">Click the **…**</span><span class="sxs-lookup"><span data-stu-id="c408d-146">Click the **…**</span></span> <span data-ttu-id="c408d-147">in the **Schemas** property.</span><span class="sxs-lookup"><span data-stu-id="c408d-147">in the **Schemas** property.</span></span> <span data-ttu-id="c408d-148">Click the **Add…**</span><span class="sxs-lookup"><span data-stu-id="c408d-148">Click the **Add…**</span></span> <span data-ttu-id="c408d-149">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="c408d-149">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="c408d-150">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c408d-150">Click **OK**.</span></span>

4. <span data-ttu-id="c408d-151">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span><span class="sxs-lookup"><span data-stu-id="c408d-151">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="c408d-152">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span><span class="sxs-lookup"><span data-stu-id="c408d-152">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="c408d-153">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span><span class="sxs-lookup"><span data-stu-id="c408d-153">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<PublicConfig xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration">
  <WadCfg>
    <DiagnosticMonitorConfiguration overallQuotaInMB="25000">
      <PerformanceCounters scheduledTransferPeriod="PT1M">
        <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT1M" unit="percent" />
        <PerformanceCounterConfiguration counterSpecifier="\Memory\Committed Bytes" sampleRate="PT1M" unit="bytes"/>
      </PerformanceCounters>
      <EtwProviders>
        <EtwEventSourceProviderConfiguration provider="SampleEventSourceWriter" scheduledTransferPeriod="PT5M">
          <Event id="1" eventDestination="EnumsTable"/>
          <Event id="2" eventDestination="MessageTable"/>
          <Event id="3" eventDestination="SetOtherTable"/>
          <Event id="4" eventDestination="HighFreqTable"/>
          <DefaultEvents eventDestination="DefaultTable" />
        </EtwEventSourceProviderConfiguration>
      </EtwProviders>
    </DiagnosticMonitorConfiguration>
  </WadCfg>
</PublicConfig>
```

### <a name="step-5-install-diagnostics-on-your-worker-role"></a><span data-ttu-id="c408d-154">Step 5: Install Diagnostics on your Worker Role</span><span class="sxs-lookup"><span data-stu-id="c408d-154">Step 5: Install Diagnostics on your Worker Role</span></span>
<span data-ttu-id="c408d-155">The PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="c408d-155">The PowerShell cmdlets for managing Diagnostics on a web or worker role are: Set-AzureServiceDiagnosticsExtension, Get-AzureServiceDiagnosticsExtension, and Remove-AzureServiceDiagnosticsExtension.</span></span>

1. <span data-ttu-id="c408d-156">Open Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c408d-156">Open Azure PowerShell.</span></span>
2. <span data-ttu-id="c408d-157">Execute the script to install Diagnostics on your worker role (replace *StorageAccountKey* with the storage account key for your wadexample storage account and *config_path* with the path to the *WadExample.xml* file):</span><span class="sxs-lookup"><span data-stu-id="c408d-157">Execute the script to install Diagnostics on your worker role (replace *StorageAccountKey* with the storage account key for your wadexample storage account and *config_path* with the path to the *WadExample.xml* file):</span></span>

```powershell
$storage_name = "wadexample"
$key = "<StorageAccountKey>"
$config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExample\WorkerRole1\WadExample.xml"
$service_name="wadexample"
$storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key
Set-AzureServiceDiagnosticsExtension -StorageContext $storageContext -DiagnosticsConfigurationPath $config_path -ServiceName $service_name -Slot Staging -Role WorkerRole1
```

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="c408d-158">Step 6: Look at your telemetry data</span><span class="sxs-lookup"><span data-stu-id="c408d-158">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="c408d-159">In the Visual Studio **Server Explorer**, navigate to the wadexample storage account.</span><span class="sxs-lookup"><span data-stu-id="c408d-159">In the Visual Studio **Server Explorer**, navigate to the wadexample storage account.</span></span> <span data-ttu-id="c408d-160">After the cloud service has been running about five (5) minutes, you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="c408d-160">After the cloud service has been running about five (5) minutes, you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="c408d-161">Double-click one of the tables to view the telemetry that has been collected.</span><span class="sxs-lookup"><span data-stu-id="c408d-161">Double-click one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_tables](./media/cloud-services-dotnet-diagnostics/WadExampleTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="c408d-163">Configuration File Schema</span><span class="sxs-lookup"><span data-stu-id="c408d-163">Configuration File Schema</span></span>
<span data-ttu-id="c408d-164">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span><span class="sxs-lookup"><span data-stu-id="c408d-164">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="c408d-165">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span><span class="sxs-lookup"><span data-stu-id="c408d-165">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c408d-166">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="c408d-166">Troubleshooting</span></span>
<span data-ttu-id="c408d-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span><span class="sxs-lookup"><span data-stu-id="c408d-167">If you have trouble, see [Troubleshooting Azure Diagnostics](../azure-diagnostics-troubleshooting.md) for help with common problems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c408d-168">Next Steps</span><span class="sxs-lookup"><span data-stu-id="c408d-168">Next Steps</span></span>
<span data-ttu-id="c408d-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span><span class="sxs-lookup"><span data-stu-id="c408d-169">[See a list of related Azure virtual-machine diagnostic articles](../monitoring-and-diagnostics/azure-diagnostics.md#cloud-services-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/
