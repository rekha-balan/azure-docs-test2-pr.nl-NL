---
title: Troubleshooting Azure Diagnostics | Microsoft Docs
description: Troubleshoot problems when using Azure diagnostics in Azure Virtual Machines, Service Fabric, or Cloud Services.
services: monitoring-and-diagnostics
documentationcenter: .net
author: rboucher
manager: carmonm
editor: ''
ms.assetid: 66469bce-d457-4d1e-b550-a08d2be4d28c
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/28/2017
ms.author: robb
ms.openlocfilehash: 81f9a5a8e5ce8389c12a40eb02dd554fc140e009
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552749"
---
# <a name="azure-diagnostics-troubleshooting"></a><span data-ttu-id="04f1e-103">Azure Diagnostics Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="04f1e-103">Azure Diagnostics Troubleshooting</span></span>
<span data-ttu-id="04f1e-104">Troubleshooting information relevant to using Azure Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="04f1e-104">Troubleshooting information relevant to using Azure Diagnostics.</span></span> <span data-ttu-id="04f1e-105">For more information on Azure diagnostics, see [Azure Diagnostics Overview](azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="04f1e-105">For more information on Azure diagnostics, see [Azure Diagnostics Overview](azure-diagnostics.md).</span></span>

## <a name="azure-diagnostics-is-not-starting"></a><span data-ttu-id="04f1e-106">Azure Diagnostics is not Starting</span><span class="sxs-lookup"><span data-stu-id="04f1e-106">Azure Diagnostics is not Starting</span></span>
<span data-ttu-id="04f1e-107">Diagnostics is composed of two components: A guest agent plugin and the monitoring agent.</span><span class="sxs-lookup"><span data-stu-id="04f1e-107">Diagnostics is composed of two components: A guest agent plugin and the monitoring agent.</span></span> <span data-ttu-id="04f1e-108">You can check the log files **DiagnosticsPluginLauncher.log** and **DiagnosticsPlugin.log** for information on why diagnostics fails to start.</span><span class="sxs-lookup"><span data-stu-id="04f1e-108">You can check the log files **DiagnosticsPluginLauncher.log** and **DiagnosticsPlugin.log** for information on why diagnostics fails to start.</span></span>  

<span data-ttu-id="04f1e-109">In a Cloud Service role, log files for the guest agent plugin are located in:</span><span class="sxs-lookup"><span data-stu-id="04f1e-109">In a Cloud Service role, log files for the guest agent plugin are located in:</span></span>

```
C:\Logs\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\1.7.4.0\
```

<span data-ttu-id="04f1e-110">In an Azure Virtual Machine, log files for the guest agent plugin are located in:</span><span class="sxs-lookup"><span data-stu-id="04f1e-110">In an Azure Virtual Machine, log files for the guest agent plugin are located in:</span></span>

```
C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\1.7.4.0\Logs\
```

<span data-ttu-id="04f1e-111">The last line of the log files contains the exit code.</span><span class="sxs-lookup"><span data-stu-id="04f1e-111">The last line of the log files contains the exit code.</span></span>  

```
DiagnosticsPluginLauncher.exe Information: 0 : [4/16/2016 6:24:15 AM] DiagnosticPlugin exited with code 0
```

<span data-ttu-id="04f1e-112">The plugin returns the following exit codes:</span><span class="sxs-lookup"><span data-stu-id="04f1e-112">The plugin returns the following exit codes:</span></span>

| <span data-ttu-id="04f1e-113">Exit Code</span><span class="sxs-lookup"><span data-stu-id="04f1e-113">Exit Code</span></span> | <span data-ttu-id="04f1e-114">Description</span><span class="sxs-lookup"><span data-stu-id="04f1e-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="04f1e-115">0</span><span class="sxs-lookup"><span data-stu-id="04f1e-115">0</span></span> |<span data-ttu-id="04f1e-116">Success.</span><span class="sxs-lookup"><span data-stu-id="04f1e-116">Success.</span></span> |
| <span data-ttu-id="04f1e-117">-1</span><span class="sxs-lookup"><span data-stu-id="04f1e-117">-1</span></span> |<span data-ttu-id="04f1e-118">Generic Error.</span><span class="sxs-lookup"><span data-stu-id="04f1e-118">Generic Error.</span></span> |
| <span data-ttu-id="04f1e-119">-2</span><span class="sxs-lookup"><span data-stu-id="04f1e-119">-2</span></span> |<span data-ttu-id="04f1e-120">Unable to load the rcf file.</span><span class="sxs-lookup"><span data-stu-id="04f1e-120">Unable to load the rcf file.</span></span><p><span data-ttu-id="04f1e-121">This internal error should only happen if the guest agent plugin launcher is manually invoked, incorrectly, on the VM.</span><span class="sxs-lookup"><span data-stu-id="04f1e-121">This internal error should only happen if the guest agent plugin launcher is manually invoked, incorrectly, on the VM.</span></span> |
| <span data-ttu-id="04f1e-122">-3</span><span class="sxs-lookup"><span data-stu-id="04f1e-122">-3</span></span> |<span data-ttu-id="04f1e-123">Cannot load the Diagnostics configuration file.</span><span class="sxs-lookup"><span data-stu-id="04f1e-123">Cannot load the Diagnostics configuration file.</span></span><p><p><span data-ttu-id="04f1e-124">Solution: Caused by a configuration file not passing schema validation.</span><span class="sxs-lookup"><span data-stu-id="04f1e-124">Solution: Caused by a configuration file not passing schema validation.</span></span> <span data-ttu-id="04f1e-125">The solution is to provide a configuration file that complies with the schema.</span><span class="sxs-lookup"><span data-stu-id="04f1e-125">The solution is to provide a configuration file that complies with the schema.</span></span> |
| <span data-ttu-id="04f1e-126">-4</span><span class="sxs-lookup"><span data-stu-id="04f1e-126">-4</span></span> |<span data-ttu-id="04f1e-127">Another instance of the monitoring agent Diagnostics is already using the local resource directory.</span><span class="sxs-lookup"><span data-stu-id="04f1e-127">Another instance of the monitoring agent Diagnostics is already using the local resource directory.</span></span><p><p><span data-ttu-id="04f1e-128">Solution: Specify a different value for **LocalResourceDirectory**.</span><span class="sxs-lookup"><span data-stu-id="04f1e-128">Solution: Specify a different value for **LocalResourceDirectory**.</span></span> |
| <span data-ttu-id="04f1e-129">-6</span><span class="sxs-lookup"><span data-stu-id="04f1e-129">-6</span></span> |<span data-ttu-id="04f1e-130">The guest agent plugin launcher attempted to launch Diagnostics with an invalid command line.</span><span class="sxs-lookup"><span data-stu-id="04f1e-130">The guest agent plugin launcher attempted to launch Diagnostics with an invalid command line.</span></span><p><p><span data-ttu-id="04f1e-131">This internal error should only happen if the guest agent plugin launcher is manually invoked, incorrectly, on the VM.</span><span class="sxs-lookup"><span data-stu-id="04f1e-131">This internal error should only happen if the guest agent plugin launcher is manually invoked, incorrectly, on the VM.</span></span> |
| <span data-ttu-id="04f1e-132">-10</span><span class="sxs-lookup"><span data-stu-id="04f1e-132">-10</span></span> |<span data-ttu-id="04f1e-133">The Diagnostics plugin exited with an unhandled exception.</span><span class="sxs-lookup"><span data-stu-id="04f1e-133">The Diagnostics plugin exited with an unhandled exception.</span></span> |
| <span data-ttu-id="04f1e-134">-11</span><span class="sxs-lookup"><span data-stu-id="04f1e-134">-11</span></span> |<span data-ttu-id="04f1e-135">The guest agent was unable to create the process responsible for launching and monitoring the monitoring agent.</span><span class="sxs-lookup"><span data-stu-id="04f1e-135">The guest agent was unable to create the process responsible for launching and monitoring the monitoring agent.</span></span><p><p><span data-ttu-id="04f1e-136">Solution: Verify that sufficient system resources are available to launch new processes.</span><span class="sxs-lookup"><span data-stu-id="04f1e-136">Solution: Verify that sufficient system resources are available to launch new processes.</span></span><p> |
| <span data-ttu-id="04f1e-137">-101</span><span class="sxs-lookup"><span data-stu-id="04f1e-137">-101</span></span> |<span data-ttu-id="04f1e-138">Invalid arguments when calling the Diagnostics plugin.</span><span class="sxs-lookup"><span data-stu-id="04f1e-138">Invalid arguments when calling the Diagnostics plugin.</span></span><p><p><span data-ttu-id="04f1e-139">This internal error should only happen if the guest agent plugin launcher is manually invoked, incorrectly, on the VM.</span><span class="sxs-lookup"><span data-stu-id="04f1e-139">This internal error should only happen if the guest agent plugin launcher is manually invoked, incorrectly, on the VM.</span></span> |
| <span data-ttu-id="04f1e-140">-102</span><span class="sxs-lookup"><span data-stu-id="04f1e-140">-102</span></span> |<span data-ttu-id="04f1e-141">The plugin process is unable to initialize itself.</span><span class="sxs-lookup"><span data-stu-id="04f1e-141">The plugin process is unable to initialize itself.</span></span><p><p><span data-ttu-id="04f1e-142">Solution: Verify that sufficient system resources are available to launch new processes.</span><span class="sxs-lookup"><span data-stu-id="04f1e-142">Solution: Verify that sufficient system resources are available to launch new processes.</span></span> |
| <span data-ttu-id="04f1e-143">-103</span><span class="sxs-lookup"><span data-stu-id="04f1e-143">-103</span></span> |<span data-ttu-id="04f1e-144">The plugin process is unable to initialize itself.</span><span class="sxs-lookup"><span data-stu-id="04f1e-144">The plugin process is unable to initialize itself.</span></span> <span data-ttu-id="04f1e-145">Specifically it is unable to create the logger object.</span><span class="sxs-lookup"><span data-stu-id="04f1e-145">Specifically it is unable to create the logger object.</span></span><p><p><span data-ttu-id="04f1e-146">Solution: Verify that sufficient system resources are available to launch new processes.</span><span class="sxs-lookup"><span data-stu-id="04f1e-146">Solution: Verify that sufficient system resources are available to launch new processes.</span></span> |
| <span data-ttu-id="04f1e-147">-104</span><span class="sxs-lookup"><span data-stu-id="04f1e-147">-104</span></span> |<span data-ttu-id="04f1e-148">Unable to load the rcf file provided by the guest agent.</span><span class="sxs-lookup"><span data-stu-id="04f1e-148">Unable to load the rcf file provided by the guest agent.</span></span><p><p><span data-ttu-id="04f1e-149">This internal error should only happen if the guest agent plugin launcher is manually invoked, incorrectly, on the VM.</span><span class="sxs-lookup"><span data-stu-id="04f1e-149">This internal error should only happen if the guest agent plugin launcher is manually invoked, incorrectly, on the VM.</span></span> |
| <span data-ttu-id="04f1e-150">-105</span><span class="sxs-lookup"><span data-stu-id="04f1e-150">-105</span></span> |<span data-ttu-id="04f1e-151">The Diagnostics plugin cannot open the Diagnostics configuration file.</span><span class="sxs-lookup"><span data-stu-id="04f1e-151">The Diagnostics plugin cannot open the Diagnostics configuration file.</span></span><p><p><span data-ttu-id="04f1e-152">This internal error should only happen if the Diagnostics plugin is manually invoked, incorrectly, on the VM.</span><span class="sxs-lookup"><span data-stu-id="04f1e-152">This internal error should only happen if the Diagnostics plugin is manually invoked, incorrectly, on the VM.</span></span> |
| <span data-ttu-id="04f1e-153">-106</span><span class="sxs-lookup"><span data-stu-id="04f1e-153">-106</span></span> |<span data-ttu-id="04f1e-154">Cannot read the Diagnostics configuration file.</span><span class="sxs-lookup"><span data-stu-id="04f1e-154">Cannot read the Diagnostics configuration file.</span></span><p><p><span data-ttu-id="04f1e-155">Solution: Caused by a configuration file not passing schema validation.</span><span class="sxs-lookup"><span data-stu-id="04f1e-155">Solution: Caused by a configuration file not passing schema validation.</span></span> <span data-ttu-id="04f1e-156">So the solution is to provide a configuration file that complies with the schema.</span><span class="sxs-lookup"><span data-stu-id="04f1e-156">So the solution is to provide a configuration file that complies with the schema.</span></span> <span data-ttu-id="04f1e-157">For Azure Virtual Machine, you can find the configuration that is delivered to the Diagnostics extension in the folder *%SystemDrive%\WindowsAzure\Config* on the VM.</span><span class="sxs-lookup"><span data-stu-id="04f1e-157">For Azure Virtual Machine, you can find the configuration that is delivered to the Diagnostics extension in the folder *%SystemDrive%\WindowsAzure\Config* on the VM.</span></span> <span data-ttu-id="04f1e-158">Open the appropriate XML file and search for **Microsoft.Azure.Diagnostics**, then for the **xmlCfg** or **WadCfg** field.</span><span class="sxs-lookup"><span data-stu-id="04f1e-158">Open the appropriate XML file and search for **Microsoft.Azure.Diagnostics**, then for the **xmlCfg** or **WadCfg** field.</span></span> <span data-ttu-id="04f1e-159">If the WadCfg field is present, it means the config is in JSON.</span><span class="sxs-lookup"><span data-stu-id="04f1e-159">If the WadCfg field is present, it means the config is in JSON.</span></span> <span data-ttu-id="04f1e-160">If the xmlCfg field is present, it means the config is in XML and is base64 encoded.</span><span class="sxs-lookup"><span data-stu-id="04f1e-160">If the xmlCfg field is present, it means the config is in XML and is base64 encoded.</span></span> <span data-ttu-id="04f1e-161">You need to decode it to see the XML that was loaded by Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="04f1e-161">You need to decode it to see the XML that was loaded by Diagnostics.</span></span> <span data-ttu-id="04f1e-162">For Cloud Service role, you can find the configuration that is delivered to the Diagnostics extension at C:\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\1.7.4.0\config.txt on the VM.</span><span class="sxs-lookup"><span data-stu-id="04f1e-162">For Cloud Service role, you can find the configuration that is delivered to the Diagnostics extension at C:\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\1.7.4.0\config.txt on the VM.</span></span> <span data-ttu-id="04f1e-163">The data is base64 encoded so you’ll need to [decode it](http://www.bing.com/search?q=base64+decoder) to see the XML that was loaded by Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="04f1e-163">The data is base64 encoded so you’ll need to [decode it](http://www.bing.com/search?q=base64+decoder) to see the XML that was loaded by Diagnostics.</span></span><p> |
| <span data-ttu-id="04f1e-164">-107</span><span class="sxs-lookup"><span data-stu-id="04f1e-164">-107</span></span> |<span data-ttu-id="04f1e-165">The resource directory pass to the monitoring agent is invalid.</span><span class="sxs-lookup"><span data-stu-id="04f1e-165">The resource directory pass to the monitoring agent is invalid.</span></span><p><p><span data-ttu-id="04f1e-166">This internal error should only happen if the monitoring agent is manually invoked, incorrectly, on the VM.</span><span class="sxs-lookup"><span data-stu-id="04f1e-166">This internal error should only happen if the monitoring agent is manually invoked, incorrectly, on the VM.</span></span></p> |
| <span data-ttu-id="04f1e-167">-108</span><span class="sxs-lookup"><span data-stu-id="04f1e-167">-108</span></span> |<span data-ttu-id="04f1e-168">Unable to convert the Diagnostics configuration file into the monitoring agent configuration file.</span><span class="sxs-lookup"><span data-stu-id="04f1e-168">Unable to convert the Diagnostics configuration file into the monitoring agent configuration file.</span></span><p><p><span data-ttu-id="04f1e-169">This internal error should only happen if the Diagnostics plugin is manually invoked with an invalid configuration file.</span><span class="sxs-lookup"><span data-stu-id="04f1e-169">This internal error should only happen if the Diagnostics plugin is manually invoked with an invalid configuration file.</span></span> |
| <span data-ttu-id="04f1e-170">-110</span><span class="sxs-lookup"><span data-stu-id="04f1e-170">-110</span></span> |<span data-ttu-id="04f1e-171">General Diagnostics configuration error.</span><span class="sxs-lookup"><span data-stu-id="04f1e-171">General Diagnostics configuration error.</span></span><p><p><span data-ttu-id="04f1e-172">This internal error should only happen if the Diagnostics plugin is manually invoked with an invalid configuration file.</span><span class="sxs-lookup"><span data-stu-id="04f1e-172">This internal error should only happen if the Diagnostics plugin is manually invoked with an invalid configuration file.</span></span> |
| <span data-ttu-id="04f1e-173">-111</span><span class="sxs-lookup"><span data-stu-id="04f1e-173">-111</span></span> |<span data-ttu-id="04f1e-174">Unable to start the monitoring agent.</span><span class="sxs-lookup"><span data-stu-id="04f1e-174">Unable to start the monitoring agent.</span></span><p><p><span data-ttu-id="04f1e-175">Solution: Verify that sufficient system resources are available.</span><span class="sxs-lookup"><span data-stu-id="04f1e-175">Solution: Verify that sufficient system resources are available.</span></span> |
| <span data-ttu-id="04f1e-176">-112</span><span class="sxs-lookup"><span data-stu-id="04f1e-176">-112</span></span> |<span data-ttu-id="04f1e-177">General error</span><span class="sxs-lookup"><span data-stu-id="04f1e-177">General error</span></span> |

## <a name="diagnostics-data-is-not-logged-to-azure-storage"></a><span data-ttu-id="04f1e-178">Diagnostics Data is Not Logged to Azure Storage</span><span class="sxs-lookup"><span data-stu-id="04f1e-178">Diagnostics Data is Not Logged to Azure Storage</span></span>
<span data-ttu-id="04f1e-179">Azure diagnostics stores all data in Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="04f1e-179">Azure diagnostics stores all data in Azure Storage.</span></span>

<span data-ttu-id="04f1e-180">The most common cause of missing event data is incorrectly defined storage account information.</span><span class="sxs-lookup"><span data-stu-id="04f1e-180">The most common cause of missing event data is incorrectly defined storage account information.</span></span>

<span data-ttu-id="04f1e-181">Solution: Correct your Diagnostics configuration file and reinstall Diagnostics.</span><span class="sxs-lookup"><span data-stu-id="04f1e-181">Solution: Correct your Diagnostics configuration file and reinstall Diagnostics.</span></span>
<span data-ttu-id="04f1e-182">If the issue persists after reinstalling the diagnostics extension, then you may have to debug further by looking through any monitoring agent errors.</span><span class="sxs-lookup"><span data-stu-id="04f1e-182">If the issue persists after reinstalling the diagnostics extension, then you may have to debug further by looking through any monitoring agent errors.</span></span> <span data-ttu-id="04f1e-183">Before event data is uploaded to your storage account, it is stored in the LocalResourceDirectory.</span><span class="sxs-lookup"><span data-stu-id="04f1e-183">Before event data is uploaded to your storage account, it is stored in the LocalResourceDirectory.</span></span>
<span data-ttu-id="04f1e-184">This directory path varies.</span><span class="sxs-lookup"><span data-stu-id="04f1e-184">This directory path varies.</span></span>

<span data-ttu-id="04f1e-185">For Cloud Service Roles:</span><span class="sxs-lookup"><span data-stu-id="04f1e-185">For Cloud Service Roles:</span></span>

    C:\Resources\Directory\<CloudServiceDeploymentID>.<RoleName>.DiagnosticStore\WAD<DiagnosticsMajorandMinorVersion>\Tables

<span data-ttu-id="04f1e-186">For Virtual Machines:</span><span class="sxs-lookup"><span data-stu-id="04f1e-186">For Virtual Machines:</span></span>

    C:\WindowsAzure\Logs\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\WAD<DiagnosticsMajorandMinorVersion>\Tables

<span data-ttu-id="04f1e-187">If there are no files in the LocalResourceDirectory folder, the monitoring agent is unable to launch.</span><span class="sxs-lookup"><span data-stu-id="04f1e-187">If there are no files in the LocalResourceDirectory folder, the monitoring agent is unable to launch.</span></span> <span data-ttu-id="04f1e-188">This is typically caused by an invalid configuration file, an event that should be reported in the CommandExecution.log.</span><span class="sxs-lookup"><span data-stu-id="04f1e-188">This is typically caused by an invalid configuration file, an event that should be reported in the CommandExecution.log.</span></span>

<span data-ttu-id="04f1e-189">If the Monitoring Agent is successfully collecting event data you see .tsf files for each event defined in your configuration file.</span><span class="sxs-lookup"><span data-stu-id="04f1e-189">If the Monitoring Agent is successfully collecting event data you see .tsf files for each event defined in your configuration file.</span></span> <span data-ttu-id="04f1e-190">The Monitoring Agent logs its errors in the file MaEventTable.tsf.</span><span class="sxs-lookup"><span data-stu-id="04f1e-190">The Monitoring Agent logs its errors in the file MaEventTable.tsf.</span></span> <span data-ttu-id="04f1e-191">To inspect the contents of this file, you can use the tabel2csv application to convert the .tsf file to a comma-separated (.csv) values file:</span><span class="sxs-lookup"><span data-stu-id="04f1e-191">To inspect the contents of this file, you can use the tabel2csv application to convert the .tsf file to a comma-separated (.csv) values file:</span></span>

<span data-ttu-id="04f1e-192">On a Cloud Service Role:</span><span class="sxs-lookup"><span data-stu-id="04f1e-192">On a Cloud Service Role:</span></span>

    %SystemDrive%\Packages\Plugins\Microsoft.Azure.Diagnostics.PaaSDiagnostics\<DiagnosticsVersion>\Monitor\x64\table2csv maeventtable.tsf

<span data-ttu-id="04f1e-193">*%SystemDrive%* on a Cloud Service Role is typically D:</span><span class="sxs-lookup"><span data-stu-id="04f1e-193">*%SystemDrive%* on a Cloud Service Role is typically D:</span></span>

<span data-ttu-id="04f1e-194">On a Virtual Machine:</span><span class="sxs-lookup"><span data-stu-id="04f1e-194">On a Virtual Machine:</span></span>

    C:\Packages\Plugins\Microsoft.Azure.Diagnostics.IaaSDiagnostics\<DiagnosticsVersion>\Monitor\x64\table2csv maeventtable.tsf

<span data-ttu-id="04f1e-195">The previous commands generate the log file *maeventtable.csv*, which you can open and inspect for failure messages.</span><span class="sxs-lookup"><span data-stu-id="04f1e-195">The previous commands generate the log file *maeventtable.csv*, which you can open and inspect for failure messages.</span></span>    

## <a name="diagnostics-data-tables-not-found"></a><span data-ttu-id="04f1e-196">Diagnostics data Tables not found</span><span class="sxs-lookup"><span data-stu-id="04f1e-196">Diagnostics data Tables not found</span></span>
<span data-ttu-id="04f1e-197">The tables in Azure storage holding Azure diagnostics data are named using the following code:</span><span class="sxs-lookup"><span data-stu-id="04f1e-197">The tables in Azure storage holding Azure diagnostics data are named using the following code:</span></span>

```csharp
        if (String.IsNullOrEmpty(eventDestination)) {
            if (e == "DefaultEvents")
                tableName = "WADDefault" + MD5(provider);
            else
                tableName = "WADEvent" + MD5(provider) + eventId;
        }
        else
            tableName = "WAD" + eventDestination;
```

<span data-ttu-id="04f1e-198">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="04f1e-198">Here is an example:</span></span>

```XML
        <EtwEventSourceProviderConfiguration provider=”prov1”>
          <Event id=”1” />
          <Event id=”2” eventDestination=”dest1” />
          <DefaultEvents />
        </EtwEventSourceProviderConfiguration>
        <EtwEventSourceProviderConfiguration provider=”prov2”>
          <DefaultEvents eventDestination=”dest2” />
        </EtwEventSourceProviderConfiguration>
```

<span data-ttu-id="04f1e-199">That generates 4 tables:</span><span class="sxs-lookup"><span data-stu-id="04f1e-199">That generates 4 tables:</span></span>

| <span data-ttu-id="04f1e-200">Event</span><span class="sxs-lookup"><span data-stu-id="04f1e-200">Event</span></span> | <span data-ttu-id="04f1e-201">Table Name</span><span class="sxs-lookup"><span data-stu-id="04f1e-201">Table Name</span></span> |
| --- | --- |
| <span data-ttu-id="04f1e-202">provider=”prov1” &lt;Event id=”1” /&gt;</span><span class="sxs-lookup"><span data-stu-id="04f1e-202">provider=”prov1” &lt;Event id=”1” /&gt;</span></span> |<span data-ttu-id="04f1e-203">WADEvent+MD5(“prov1”)+”1”</span><span class="sxs-lookup"><span data-stu-id="04f1e-203">WADEvent+MD5(“prov1”)+”1”</span></span> |
| <span data-ttu-id="04f1e-204">provider=”prov1” &lt;Event id=”2” eventDestination=”dest1” /&gt;</span><span class="sxs-lookup"><span data-stu-id="04f1e-204">provider=”prov1” &lt;Event id=”2” eventDestination=”dest1” /&gt;</span></span> |<span data-ttu-id="04f1e-205">WADdest1</span><span class="sxs-lookup"><span data-stu-id="04f1e-205">WADdest1</span></span> |
| <span data-ttu-id="04f1e-206">provider=”prov1” &lt;DefaultEvents /&gt;</span><span class="sxs-lookup"><span data-stu-id="04f1e-206">provider=”prov1” &lt;DefaultEvents /&gt;</span></span> |<span data-ttu-id="04f1e-207">WADDefault+MD5(“prov1”)</span><span class="sxs-lookup"><span data-stu-id="04f1e-207">WADDefault+MD5(“prov1”)</span></span> |
| <span data-ttu-id="04f1e-208">provider=”prov2” &lt;DefaultEvents eventDestination=”dest2” /&gt;</span><span class="sxs-lookup"><span data-stu-id="04f1e-208">provider=”prov2” &lt;DefaultEvents eventDestination=”dest2” /&gt;</span></span> |<span data-ttu-id="04f1e-209">WADdest2</span><span class="sxs-lookup"><span data-stu-id="04f1e-209">WADdest2</span></span> |
