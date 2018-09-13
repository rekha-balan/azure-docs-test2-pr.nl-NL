---
title: How to use Azure diagnostics in Virtual Machines  | Microsoft Docs
description: Using Azure diagnostics to gather data from Azure Virtual Machines for debugging, measuring performance, monitoring, traffic analysis, and more.
services: virtual-machines
documentationcenter: .net
author: davidmu1
manager: ''
editor: ''
ms.assetid: dfaabc7a-23e7-4af0-8369-f504d2915b3d
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 02/16/2016
ms.author: davidmu
ms.openlocfilehash: 69d4966840c21a4c596a0e2f70661e821c623c8c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550252"
---
# <a name="enabling-diagnostics-in-azure-virtual-machines"></a><span data-ttu-id="704c9-103">Enabling Diagnostics in Azure Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="704c9-103">Enabling Diagnostics in Azure Virtual Machines</span></span>
<span data-ttu-id="704c9-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="704c9-104">See [Azure Diagnostics Overview](../monitoring-and-diagnostics/azure-diagnostics.md) for a background on Azure Diagnostics.</span></span>

## <a name="how-to-enable-diagnostics-in-a-virtual-machine"></a><span data-ttu-id="704c9-105">How to Enable Diagnostics in a Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="704c9-105">How to Enable Diagnostics in a Virtual Machine</span></span>
<span data-ttu-id="704c9-106">This walk through describes how to remotely install Diagnostics to an Azure virtual machine from a development computer.</span><span class="sxs-lookup"><span data-stu-id="704c9-106">This walk through describes how to remotely install Diagnostics to an Azure virtual machine from a development computer.</span></span> <span data-ttu-id="704c9-107">You also learn how to implement an application that runs on that Azure virtual machine and emits telemetry data using the .NET [EventSource Class][EventSource Class].</span><span class="sxs-lookup"><span data-stu-id="704c9-107">You also learn how to implement an application that runs on that Azure virtual machine and emits telemetry data using the .NET [EventSource Class][EventSource Class].</span></span> <span data-ttu-id="704c9-108">Azure Diagnostics is used to collect the telemetry and store it in an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="704c9-108">Azure Diagnostics is used to collect the telemetry and store it in an Azure storage account.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="704c9-109">Pre-requisites</span><span class="sxs-lookup"><span data-stu-id="704c9-109">Pre-requisites</span></span>
<span data-ttu-id="704c9-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2013 with the Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="704c9-110">This walk through assumes you have an Azure subscription and are using Visual Studio 2013 with the Azure SDK.</span></span> <span data-ttu-id="704c9-111">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span><span class="sxs-lookup"><span data-stu-id="704c9-111">If you do not have an Azure subscription, you can sign up for the [Free Trial][Free Trial].</span></span> <span data-ttu-id="704c9-112">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span><span class="sxs-lookup"><span data-stu-id="704c9-112">Make sure to [Install and configure Azure PowerShell version 0.8.7 or later][Install and configure Azure PowerShell version 0.8.7 or later].</span></span>

### <a name="step-1-create-a-virtual-machine"></a><span data-ttu-id="704c9-113">Step 1: Create a Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="704c9-113">Step 1: Create a Virtual Machine</span></span>
1. <span data-ttu-id="704c9-114">On your development computer, launch Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="704c9-114">On your development computer, launch Visual Studio 2013.</span></span>
2. <span data-ttu-id="704c9-115">In the Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span><span class="sxs-lookup"><span data-stu-id="704c9-115">In the Visual Studio **Server Explorer** expand **Azure**, right-click **Virtual Machines** then select **Create Virtual Machine**.</span></span>
3. <span data-ttu-id="704c9-116">Select your Azure subscription in the **Choose a Subscription** dialog and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="704c9-116">Select your Azure subscription in the **Choose a Subscription** dialog and click **Next**.</span></span>
4. <span data-ttu-id="704c9-117">Select **Windows Server 2012 R2 Datacenter, November 2014** in the **Select a Virtual Machine Image** dialog and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="704c9-117">Select **Windows Server 2012 R2 Datacenter, November 2014** in the **Select a Virtual Machine Image** dialog and click **Next**.</span></span>
5. <span data-ttu-id="704c9-118">In the **Virtual Machine Basic Settings**, set the virtual machine name to "wadexample".</span><span class="sxs-lookup"><span data-stu-id="704c9-118">In the **Virtual Machine Basic Settings**, set the virtual machine name to "wadexample".</span></span> <span data-ttu-id="704c9-119">Set your Administrator user name and password and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="704c9-119">Set your Administrator user name and password and click **Next**.</span></span>
6. <span data-ttu-id="704c9-120">In the **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span><span class="sxs-lookup"><span data-stu-id="704c9-120">In the **Cloud Service Settings** dialog create a new cloud service named "wadexampleVM".</span></span> <span data-ttu-id="704c9-121">Create a new Storage account named "wadexample" and click **Next**.</span><span class="sxs-lookup"><span data-stu-id="704c9-121">Create a new Storage account named "wadexample" and click **Next**.</span></span>
7. <span data-ttu-id="704c9-122">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="704c9-122">Click **Create**.</span></span>

### <a name="step-2-create-your-application"></a><span data-ttu-id="704c9-123">Step 2: Create your Application</span><span class="sxs-lookup"><span data-stu-id="704c9-123">Step 2: Create your Application</span></span>
1. <span data-ttu-id="704c9-124">On your development computer, launch Visual Studio 2013.</span><span class="sxs-lookup"><span data-stu-id="704c9-124">On your development computer, launch Visual Studio 2013.</span></span>
2. <span data-ttu-id="704c9-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="704c9-125">Create a new Visual C# Console Application that targets .NET Framework 4.5.</span></span> <span data-ttu-id="704c9-126">Name the project "WadExampleVM".</span><span class="sxs-lookup"><span data-stu-id="704c9-126">Name the project "WadExampleVM".</span></span>
   <span data-ttu-id="704c9-127">![CloudServices_diag_new_project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/media/virtual-machines-dotnet-diagnostics/NewProject.png)</span><span class="sxs-lookup"><span data-stu-id="704c9-127">![CloudServices_diag_new_project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/media/virtual-machines-dotnet-diagnostics/NewProject.png)</span></span>
3. <span data-ttu-id="704c9-128">Replace the contents of Program.cs with the following code.</span><span class="sxs-lookup"><span data-stu-id="704c9-128">Replace the contents of Program.cs with the following code.</span></span> <span data-ttu-id="704c9-129">The class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span><span class="sxs-lookup"><span data-stu-id="704c9-129">The class **SampleEventSourceWriter** implements four logging methods: **SendEnums**, **MessageMethod**, **SetOther** and **HighFreq**.</span></span> <span data-ttu-id="704c9-130">The first parameter to the WriteEvent method defines the ID for the respective event.</span><span class="sxs-lookup"><span data-stu-id="704c9-130">The first parameter to the WriteEvent method defines the ID for the respective event.</span></span> <span data-ttu-id="704c9-131">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span><span class="sxs-lookup"><span data-stu-id="704c9-131">The Run method implements an infinite loop that calls each of the logging methods implemented in the **SampleEventSourceWriter** class every 10 seconds.</span></span>

    ```csharp
     using System;
     using System.Diagnostics;
     using System.Diagnostics.Tracing;
     using System.Threading;

     namespace WadExampleVM
     {
       sealed class SampleEventSourceWriter : EventSource {
         public static SampleEventSourceWriter Log = new SampleEventSourceWriter();
         public void SendEnums(MyColor color, MyFlags flags) { if (IsEnabled())  WriteEvent(1, (int)color, (int)flags); } // Cast enums to int for efficient logging.
         public void MessageMethod(string Message) { if (IsEnabled())  WriteEvent(2, Message); }
         public void SetOther(bool flag, int myInt) { if (IsEnabled())  WriteEvent(3, flag, myInt); }
         public void HighFreq(int value) { if (IsEnabled()) WriteEvent(4, value); }
       }

       enum MyColor {
         Red,
         Blue,
         Green
       }

       [Flags]
       enum MyFlags {
         Flag1 = 1,
         Flag2 = 2,
         Flag3 = 4
       }

       class Program
       {
         static void Main(string[] args) {
         Trace.TraceInformation("My application entry point called");

         int value = 0;

         while (true) {
             Thread.Sleep(10000);
             Trace.TraceInformation("Working");

             // Emit several events every time we go through the loop
             for (int i = 0; i < 6; i++) {
                 SampleEventSourceWriter.Log.SendEnums(MyColor.Blue, MyFlags.Flag2 | MyFlags.Flag3);
             }

             for (int i = 0; i < 3; i++) {
                 SampleEventSourceWriter.Log.MessageMethod("This is a message.");
                 SampleEventSourceWriter.Log.SetOther(true, 123456789);
             }

             if (value == int.MaxValue) value = 0;
             SampleEventSourceWriter.Log.HighFreq(value++);
         }

        }
      }
     }
     ```
4. <span data-ttu-id="704c9-132">Save the file and select **Build Solution** from the **Build** menu to build your code.</span><span class="sxs-lookup"><span data-stu-id="704c9-132">Save the file and select **Build Solution** from the **Build** menu to build your code.</span></span>

### <a name="step-3-deploy-your-application"></a><span data-ttu-id="704c9-133">Step 3: Deploy your Application</span><span class="sxs-lookup"><span data-stu-id="704c9-133">Step 3: Deploy your Application</span></span>
1. <span data-ttu-id="704c9-134">Right-click on the **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span><span class="sxs-lookup"><span data-stu-id="704c9-134">Right-click on the **WadExampleVM** project in **Solution Explorer** and choose **Open Folder in File Explorer**.</span></span>
2. <span data-ttu-id="704c9-135">Navigate to the *bin\Debug* folder and copy all the files (WadExampleVM.\*)</span><span class="sxs-lookup"><span data-stu-id="704c9-135">Navigate to the *bin\Debug* folder and copy all the files (WadExampleVM.\*)</span></span>
3. <span data-ttu-id="704c9-136">In **Server Explorer** right-click on the virtual machine and choose **Connect using Remote Desktop**.</span><span class="sxs-lookup"><span data-stu-id="704c9-136">In **Server Explorer** right-click on the virtual machine and choose **Connect using Remote Desktop**.</span></span>
4. <span data-ttu-id="704c9-137">Once connected to the VM create a folder named WadExampleVM and paste your application files into the folder.</span><span class="sxs-lookup"><span data-stu-id="704c9-137">Once connected to the VM create a folder named WadExampleVM and paste your application files into the folder.</span></span>
5. <span data-ttu-id="704c9-138">Launch the application WadExampleVM.exe.</span><span class="sxs-lookup"><span data-stu-id="704c9-138">Launch the application WadExampleVM.exe.</span></span> <span data-ttu-id="704c9-139">You should see a blank console window.</span><span class="sxs-lookup"><span data-stu-id="704c9-139">You should see a blank console window.</span></span>

### <a name="step-4-create-your-diagnostics-configuration-and-install-the-extension"></a><span data-ttu-id="704c9-140">Step 4: Create your Diagnostics configuration and install the Extension</span><span class="sxs-lookup"><span data-stu-id="704c9-140">Step 4: Create your Diagnostics configuration and install the Extension</span></span>
1. <span data-ttu-id="704c9-141">Download the public configuration file schema definition to your development computer by executing the following PowerShell command:</span><span class="sxs-lookup"><span data-stu-id="704c9-141">Download the public configuration file schema definition to your development computer by executing the following PowerShell command:</span></span>

     <span data-ttu-id="704c9-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span><span class="sxs-lookup"><span data-stu-id="704c9-142">(Get-AzureServiceAvailableExtension -ExtensionName 'PaaSDiagnostics' -ProviderNamespace 'Microsoft.Azure.Diagnostics').PublicConfigurationSchema | Out-File -Encoding utf8 -FilePath 'WadConfig.xsd'</span></span>
2. <span data-ttu-id="704c9-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span><span class="sxs-lookup"><span data-stu-id="704c9-143">Open a new XML file in Visual Studio, either in a project you already have open or in a Visual Studio instance with no open projects.</span></span> <span data-ttu-id="704c9-144">In Visual Studio, select **Add** -> **New Item…**</span><span class="sxs-lookup"><span data-stu-id="704c9-144">In Visual Studio, select **Add** -> **New Item…**</span></span><span data-ttu-id="704c9-145"> -> *\*Visual C# items** -> *\*Data** -> *\*XML File*\*.</span><span class="sxs-lookup"><span data-stu-id="704c9-145"> -> *\*Visual C# items** -> *\*Data** -> *\*XML File*\*.</span></span> <span data-ttu-id="704c9-146">Name the file "WadExample.xml"</span><span class="sxs-lookup"><span data-stu-id="704c9-146">Name the file "WadExample.xml"</span></span>
3. <span data-ttu-id="704c9-147">Associate the WadConfig.xsd with the configuration file.</span><span class="sxs-lookup"><span data-stu-id="704c9-147">Associate the WadConfig.xsd with the configuration file.</span></span> <span data-ttu-id="704c9-148">Make sure the WadExample.xml editor window is the active window.</span><span class="sxs-lookup"><span data-stu-id="704c9-148">Make sure the WadExample.xml editor window is the active window.</span></span> <span data-ttu-id="704c9-149">Press **F4** to open the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="704c9-149">Press **F4** to open the **Properties** window.</span></span> <span data-ttu-id="704c9-150">Click on the **Schemas** property in the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="704c9-150">Click on the **Schemas** property in the **Properties** window.</span></span> <span data-ttu-id="704c9-151">Click the **…**</span><span class="sxs-lookup"><span data-stu-id="704c9-151">Click the **…**</span></span> <span data-ttu-id="704c9-152">in the **Schemas** property.</span><span class="sxs-lookup"><span data-stu-id="704c9-152">in the **Schemas** property.</span></span> <span data-ttu-id="704c9-153">Click the **Add…**</span><span class="sxs-lookup"><span data-stu-id="704c9-153">Click the **Add…**</span></span> <span data-ttu-id="704c9-154">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span><span class="sxs-lookup"><span data-stu-id="704c9-154">button and navigate to the location where you saved the XSD file and select the file WadConfig.xsd.</span></span> <span data-ttu-id="704c9-155">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="704c9-155">Click **OK**.</span></span>
4. <span data-ttu-id="704c9-156">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span><span class="sxs-lookup"><span data-stu-id="704c9-156">Replace the contents of the WadExample.xml configuration file with the following XML and save the file.</span></span> <span data-ttu-id="704c9-157">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span><span class="sxs-lookup"><span data-stu-id="704c9-157">This configuration file defines a couple performance counters to collect: one for CPU utilization and one for memory utilization.</span></span> <span data-ttu-id="704c9-158">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span><span class="sxs-lookup"><span data-stu-id="704c9-158">Then the configuration defines the four events corresponding to the methods in the SampleEventSourceWriter class.</span></span>

```
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

### <a name="step-5-remotely-install-diagnostics-on-your-azure-virtual-machine"></a><span data-ttu-id="704c9-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="704c9-159">Step 5: Remotely install Diagnostics on your Azure Virtual Machine</span></span>
<span data-ttu-id="704c9-160">The PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span><span class="sxs-lookup"><span data-stu-id="704c9-160">The PowerShell cmdlets for managing Diagnostics on a VM are: Set-AzureVMDiagnosticsExtension, Get-AzureVMDiagnosticsExtension, and Remove-AzureVMDiagnosticsExtension.</span></span>

1. <span data-ttu-id="704c9-161">On your developer computer, open Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="704c9-161">On your developer computer, open Azure PowerShell.</span></span>
2. <span data-ttu-id="704c9-162">Execute the script to remotely install Diagnostics on your VM (Replace *StorageAccountKey* with the storage account key for your wadexamplevm storage account):</span><span class="sxs-lookup"><span data-stu-id="704c9-162">Execute the script to remotely install Diagnostics on your VM (Replace *StorageAccountKey* with the storage account key for your wadexamplevm storage account):</span></span>

     <span data-ttu-id="704c9-163">$storage_name = "wadexamplevm"   $key = "<StorageAccountKey>"   $config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExampleVM\WadExampleVM\WadExample.xml"   $service_name="wadexamplevm"   $vm_name="WadExample"   $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key   $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name   $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.\*" -VM $VM1 -StorageContext $storageContext   $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM</span><span class="sxs-lookup"><span data-stu-id="704c9-163">$storage_name = "wadexamplevm"   $key = "<StorageAccountKey>"   $config_path="c:\users\<user>\documents\visual studio 2013\Projects\WadExampleVM\WadExampleVM\WadExample.xml"   $service_name="wadexamplevm"   $vm_name="WadExample"   $storageContext = New-AzureStorageContext -StorageAccountName $storage_name -StorageAccountKey $key   $VM1 = Get-AzureVM -ServiceName $service_name -Name $vm_name   $VM2 = Set-AzureVMDiagnosticsExtension -DiagnosticsConfigurationPath $config_path -Version "1.\*" -VM $VM1 -StorageContext $storageContext   $VM3 = Update-AzureVM -ServiceName $service_name -Name $vm_name -VM $VM2.VM</span></span>

### <a name="step-6-look-at-your-telemetry-data"></a><span data-ttu-id="704c9-164">Step 6: Look at your telemetry data</span><span class="sxs-lookup"><span data-stu-id="704c9-164">Step 6: Look at your telemetry data</span></span>
<span data-ttu-id="704c9-165">In the Visual Studio **Server Explorer** navigate to the wadexample storage account.</span><span class="sxs-lookup"><span data-stu-id="704c9-165">In the Visual Studio **Server Explorer** navigate to the wadexample storage account.</span></span> <span data-ttu-id="704c9-166">After the VM has been running about 5 minutes you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span><span class="sxs-lookup"><span data-stu-id="704c9-166">After the VM has been running about 5 minutes you should see the tables **WADEnumsTable**, **WADHighFreqTable**, **WADMessageTable**, **WADPerformanceCountersTable** and **WADSetOtherTable**.</span></span> <span data-ttu-id="704c9-167">Double-click on one of the tables to view the telemetry that has been collected.</span><span class="sxs-lookup"><span data-stu-id="704c9-167">Double-click on one of the tables to view the telemetry that has been collected.</span></span>

![CloudServices_diag_wadexamplevm_tables](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/media/virtual-machines-dotnet-diagnostics/WadExampleVMTables.png)

## <a name="configuration-file-schema"></a><span data-ttu-id="704c9-169">Configuration file schema</span><span class="sxs-lookup"><span data-stu-id="704c9-169">Configuration file schema</span></span>
<span data-ttu-id="704c9-170">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span><span class="sxs-lookup"><span data-stu-id="704c9-170">The Diagnostics configuration file defines values that are used to initialize diagnostic configuration settings when the diagnostics agent starts.</span></span> <span data-ttu-id="704c9-171">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span><span class="sxs-lookup"><span data-stu-id="704c9-171">See the [latest schema reference](https://msdn.microsoft.com/library/azure/mt634524.aspx) for valid values and examples.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="704c9-172">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="704c9-172">Troubleshooting</span></span>
<span data-ttu-id="704c9-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span><span class="sxs-lookup"><span data-stu-id="704c9-173">See [Troubleshooting Azure Diagnostics](../monitoring-and-diagnostics/azure-diagnostics-troubleshooting.md) for more information.</span></span>

## <a name="next-steps"></a><span data-ttu-id="704c9-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="704c9-174">Next steps</span></span>
<span data-ttu-id="704c9-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span><span class="sxs-lookup"><span data-stu-id="704c9-175">[See a list of virtual machine related Azure Diagnostics articles](../monitoring-and-diagnostics/azure-diagnostics.md#virtual-machines-using-azure-diagnostics) to change the data you are collecting, troubleshoot problems or learn more about diagnostics in general.</span></span>

[EventSource Class]: http://msdn.microsoft.com/library/system.diagnostics.tracing.eventsource(v=vs.110).aspx

[Debugging an Azure Application]: http://msdn.microsoft.com/library/windowsazure/ee405479.aspx   
[Collect Logging Data by Using Azure Diagnostics]: http://msdn.microsoft.com/library/windowsazure/gg433048.aspx
[Free Trial]: http://azure.microsoft.com/pricing/free-trial/
[Install and configure Azure PowerShell version 0.8.7 or later]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/


