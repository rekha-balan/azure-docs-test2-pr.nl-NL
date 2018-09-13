---
title: Azure Diagnostics 1.0 Configuration Schema | Microsoft Docs
description: ONLY relevant if you are using Azure SDK 2.4 and below with Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, or Cloud Services.
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
ms.date: 03/21/2017
ms.author: robb
ms.openlocfilehash: 47a6bcdf2b7edceb4b7dc8ab7f9d5b1c62f578c1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669735"
---
# <a name="azure-diagnostics-10-configuration-schema"></a><span data-ttu-id="d7184-103">Azure Diagnostics 1.0 Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="d7184-103">Azure Diagnostics 1.0 Configuration Schema</span></span>
> [!NOTE]
> <span data-ttu-id="d7184-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span><span class="sxs-lookup"><span data-stu-id="d7184-104">Azure Diagnostics is the component used to collect performance counters and other statistics from Azure Virtual Machines, Virtual Machine Scale Sets, Service Fabric, and Cloud Services.</span></span>  <span data-ttu-id="d7184-105">This page is only relevant if you are using one of these services.</span><span class="sxs-lookup"><span data-stu-id="d7184-105">This page is only relevant if you are using one of these services.</span></span>
>

<span data-ttu-id="d7184-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="d7184-106">Azure Diagnostics is used with other Microsoft diagnostics products like Azure Monitor, Application Insights, and Log Analytics.</span></span>

<span data-ttu-id="d7184-107">The Azure Diagnostics configuration file defines values that are used to initialize the Diagnostics Monitor.</span><span class="sxs-lookup"><span data-stu-id="d7184-107">The Azure Diagnostics configuration file defines values that are used to initialize the Diagnostics Monitor.</span></span> <span data-ttu-id="d7184-108">This file is used to initialize diagnostic configuration settings when the diagnostics monitor starts.</span><span class="sxs-lookup"><span data-stu-id="d7184-108">This file is used to initialize diagnostic configuration settings when the diagnostics monitor starts.</span></span>  

 <span data-ttu-id="d7184-109">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span><span class="sxs-lookup"><span data-stu-id="d7184-109">By default, the Azure Diagnostics configuration schema file is installed to the `C:\Program Files\Microsoft SDKs\Azure\.NET SDK\<version>\schemas` directory.</span></span> <span data-ttu-id="d7184-110">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span><span class="sxs-lookup"><span data-stu-id="d7184-110">Replace `<version>` with the installed version of the [Azure SDK](http://www.windowsazure.com/develop/downloads/).</span></span>  

> [!NOTE]
>  <span data-ttu-id="d7184-111">The diagnostics configuration file is typically used with startup tasks that require diagnostic data to be collected earlier in the startup process.</span><span class="sxs-lookup"><span data-stu-id="d7184-111">The diagnostics configuration file is typically used with startup tasks that require diagnostic data to be collected earlier in the startup process.</span></span> <span data-ttu-id="d7184-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span><span class="sxs-lookup"><span data-stu-id="d7184-112">For more information about using Azure Diagnostics, see [Collect Logging Data by Using Azure Diagnostics](assetId:///83a91c23-5ca2-4fc9-8df3-62036c37a3d7).</span></span>  

## <a name="example-of-the-diagnostics-configuration-file"></a><span data-ttu-id="d7184-113">Example of the diagnostics configuration file</span><span class="sxs-lookup"><span data-stu-id="d7184-113">Example of the diagnostics configuration file</span></span>  
 <span data-ttu-id="d7184-114">The following example shows a typical diagnostics configuration file:</span><span class="sxs-lookup"><span data-stu-id="d7184-114">The following example shows a typical diagnostics configuration file:</span></span>  

```xml  
<?xml version="1.0" encoding="utf-8"?>
<DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"  
      configurationChangePollInterval="PT1M"  
      overallQuotaInMB="4096">  
   <DiagnosticInfrastructureLogs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  
   <Logs bufferQuotaInMB="1024"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M" />  

   <Directories bufferQuotaInMB="1024"   
      scheduledTransferPeriod="PT1M">  

      <!-- These three elements specify the special directories   
           that are set up for the log types -->  
      <CrashDumps container="wad-crash-dumps" directoryQuotaInMB="256" />  
      <FailedRequestLogs container="wad-frq" directoryQuotaInMB="256" />  
      <IISLogs container="wad-iis" directoryQuotaInMB="256" />  

      <!-- For regular directories the DataSources element is used -->  
      <DataSources>  
         <DirectoryConfiguration container="wad-panther" directoryQuotaInMB="128">  
            <!-- Absolute specifies an absolute path with optional environment expansion -->  
            <Absolute expandEnvironment="true" path="%SystemRoot%\system32\sysprep\Panther" />  
         </DirectoryConfiguration>  
         <DirectoryConfiguration container="wad-custom" directoryQuotaInMB="128">  
            <!-- LocalResource specifies a path relative to a local   
                 resource defined in the service definition -->  
            <LocalResource name="MyLoggingLocalResource" relativePath="logs" />  
         </DirectoryConfiguration>  
      </DataSources>  
   </Directories>  

   <PerformanceCounters bufferQuotaInMB="512" scheduledTransferPeriod="PT1M">  
      <!-- The counter specifier is in the same format as the imperative   
           diagnostics configuration API -->  
      <PerformanceCounterConfiguration   
         counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT5S" />  
   </PerformanceCounters>  

   <WindowsEventLog bufferQuotaInMB="512"  
      scheduledTransferLogLevelFilter="Verbose"  
      scheduledTransferPeriod="PT1M">  
      <!-- The event log name is in the same format as the imperative   
           diagnostics configuration API -->  
      <DataSource name="System!*" />  
   </WindowsEventLog>  
</DiagnosticMonitorConfiguration>  
```  

## <a name="diagnosticsconfiguration-namespace"></a><span data-ttu-id="d7184-115">DiagnosticsConfiguration Namespace</span><span class="sxs-lookup"><span data-stu-id="d7184-115">DiagnosticsConfiguration Namespace</span></span>  
 <span data-ttu-id="d7184-116">The XML namespace for the diagnostics configuration file is:</span><span class="sxs-lookup"><span data-stu-id="d7184-116">The XML namespace for the diagnostics configuration file is:</span></span>  

```  
http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration  
```  

## <a name="schema-elements"></a><span data-ttu-id="d7184-117">Schema Elements</span><span class="sxs-lookup"><span data-stu-id="d7184-117">Schema Elements</span></span>  
 <span data-ttu-id="d7184-118">The diagnostics configuration file includes the following elements.</span><span class="sxs-lookup"><span data-stu-id="d7184-118">The diagnostics configuration file includes the following elements.</span></span>


## <a name="diagnosticmonitorconfiguration-element"></a><span data-ttu-id="d7184-119">DiagnosticMonitorConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="d7184-119">DiagnosticMonitorConfiguration Element</span></span>  
<span data-ttu-id="d7184-120">The top-level element of the diagnostics configuration file.</span><span class="sxs-lookup"><span data-stu-id="d7184-120">The top-level element of the diagnostics configuration file.</span></span>  

<span data-ttu-id="d7184-121">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-121">Attributes:</span></span>

|<span data-ttu-id="d7184-122">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-122">Attribute</span></span>  |<span data-ttu-id="d7184-123">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-123">Type</span></span>   |<span data-ttu-id="d7184-124">Required</span><span class="sxs-lookup"><span data-stu-id="d7184-124">Required</span></span>| <span data-ttu-id="d7184-125">Default</span><span class="sxs-lookup"><span data-stu-id="d7184-125">Default</span></span> | <span data-ttu-id="d7184-126">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-126">Description</span></span>|  
|-----------|-------|--------|---------|------------|  
|<span data-ttu-id="d7184-127">**configurationChangePollInterval**</span><span class="sxs-lookup"><span data-stu-id="d7184-127">**configurationChangePollInterval**</span></span>|<span data-ttu-id="d7184-128">duration</span><span class="sxs-lookup"><span data-stu-id="d7184-128">duration</span></span>|<span data-ttu-id="d7184-129">Optional</span><span class="sxs-lookup"><span data-stu-id="d7184-129">Optional</span></span> | <span data-ttu-id="d7184-130">PT1M</span><span class="sxs-lookup"><span data-stu-id="d7184-130">PT1M</span></span>| <span data-ttu-id="d7184-131">Specifies the interval at which the diagnostic monitor polls for diagnostic configuration changes.</span><span class="sxs-lookup"><span data-stu-id="d7184-131">Specifies the interval at which the diagnostic monitor polls for diagnostic configuration changes.</span></span>|  
|<span data-ttu-id="d7184-132">**overallQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d7184-132">**overallQuotaInMB**</span></span>|<span data-ttu-id="d7184-133">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="d7184-133">unsignedInt</span></span>|<span data-ttu-id="d7184-134">Optional</span><span class="sxs-lookup"><span data-stu-id="d7184-134">Optional</span></span>| <span data-ttu-id="d7184-135">4000 MB.</span><span class="sxs-lookup"><span data-stu-id="d7184-135">4000 MB.</span></span> <span data-ttu-id="d7184-136">If you provide a value, it must not exceed this amount</span><span class="sxs-lookup"><span data-stu-id="d7184-136">If you provide a value, it must not exceed this amount</span></span> |<span data-ttu-id="d7184-137">The total amount of file system storage allocated for all logging buffers.</span><span class="sxs-lookup"><span data-stu-id="d7184-137">The total amount of file system storage allocated for all logging buffers.</span></span>|  

## <a name="diagnosticinfrastructurelogs-element"></a><span data-ttu-id="d7184-138">DiagnosticInfrastructureLogs Element</span><span class="sxs-lookup"><span data-stu-id="d7184-138">DiagnosticInfrastructureLogs Element</span></span>  
<span data-ttu-id="d7184-139">Defines the buffer configuration for the logs that are generated by the underlying diagnostics infrastructure.</span><span class="sxs-lookup"><span data-stu-id="d7184-139">Defines the buffer configuration for the logs that are generated by the underlying diagnostics infrastructure.</span></span>

<span data-ttu-id="d7184-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="d7184-140">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="d7184-141">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-141">Attributes:</span></span>

|<span data-ttu-id="d7184-142">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-142">Attribute</span></span>|<span data-ttu-id="d7184-143">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-143">Type</span></span>|<span data-ttu-id="d7184-144">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-144">Description</span></span>|  
|---------|----|-----------------|  
|<span data-ttu-id="d7184-145">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d7184-145">**bufferQuotaInMB**</span></span>|<span data-ttu-id="d7184-146">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="d7184-146">unsignedInt</span></span>|<span data-ttu-id="d7184-147">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-147">Optional.</span></span> <span data-ttu-id="d7184-148">Specifies the maximum amount of file system storage that is available for the specified data.</span><span class="sxs-lookup"><span data-stu-id="d7184-148">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="d7184-149">The default is 0.</span><span class="sxs-lookup"><span data-stu-id="d7184-149">The default is 0.</span></span>|  
|<span data-ttu-id="d7184-150">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="d7184-150">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="d7184-151">string</span><span class="sxs-lookup"><span data-stu-id="d7184-151">string</span></span>|<span data-ttu-id="d7184-152">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-152">Optional.</span></span> <span data-ttu-id="d7184-153">Specifies the minimum severity level for log entries that are transferred.</span><span class="sxs-lookup"><span data-stu-id="d7184-153">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="d7184-154">The default value is **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="d7184-154">The default value is **Undefined**.</span></span> <span data-ttu-id="d7184-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span><span class="sxs-lookup"><span data-stu-id="d7184-155">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="d7184-156">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="d7184-156">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="d7184-157">duration</span><span class="sxs-lookup"><span data-stu-id="d7184-157">duration</span></span>|<span data-ttu-id="d7184-158">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-158">Optional.</span></span> <span data-ttu-id="d7184-159">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="d7184-159">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="d7184-160">The default is PT0S.</span><span class="sxs-lookup"><span data-stu-id="d7184-160">The default is PT0S.</span></span>|  

## <a name="logs-element"></a><span data-ttu-id="d7184-161">Logs Element</span><span class="sxs-lookup"><span data-stu-id="d7184-161">Logs Element</span></span>  
 <span data-ttu-id="d7184-162">Defines the buffer configuration for basic Azure logs.</span><span class="sxs-lookup"><span data-stu-id="d7184-162">Defines the buffer configuration for basic Azure logs.</span></span>

 <span data-ttu-id="d7184-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="d7184-163">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  

<span data-ttu-id="d7184-164">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-164">Attributes:</span></span>  

|<span data-ttu-id="d7184-165">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-165">Attribute</span></span>|<span data-ttu-id="d7184-166">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-166">Type</span></span>|<span data-ttu-id="d7184-167">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-167">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-168">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d7184-168">**bufferQuotaInMB**</span></span>|<span data-ttu-id="d7184-169">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="d7184-169">unsignedInt</span></span>|<span data-ttu-id="d7184-170">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-170">Optional.</span></span> <span data-ttu-id="d7184-171">Specifies the maximum amount of file system storage that is available for the specified data.</span><span class="sxs-lookup"><span data-stu-id="d7184-171">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="d7184-172">The default is 0.</span><span class="sxs-lookup"><span data-stu-id="d7184-172">The default is 0.</span></span>|  
|<span data-ttu-id="d7184-173">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="d7184-173">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="d7184-174">string</span><span class="sxs-lookup"><span data-stu-id="d7184-174">string</span></span>|<span data-ttu-id="d7184-175">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-175">Optional.</span></span> <span data-ttu-id="d7184-176">Specifies the minimum severity level for log entries that are transferred.</span><span class="sxs-lookup"><span data-stu-id="d7184-176">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="d7184-177">The default value is **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="d7184-177">The default value is **Undefined**.</span></span> <span data-ttu-id="d7184-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span><span class="sxs-lookup"><span data-stu-id="d7184-178">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="d7184-179">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="d7184-179">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="d7184-180">duration</span><span class="sxs-lookup"><span data-stu-id="d7184-180">duration</span></span>|<span data-ttu-id="d7184-181">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-181">Optional.</span></span> <span data-ttu-id="d7184-182">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="d7184-182">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="d7184-183">The default is PT0S.</span><span class="sxs-lookup"><span data-stu-id="d7184-183">The default is PT0S.</span></span>|  

## <a name="directories-element"></a><span data-ttu-id="d7184-184">Directories Element</span><span class="sxs-lookup"><span data-stu-id="d7184-184">Directories Element</span></span>  
<span data-ttu-id="d7184-185">Defines the buffer configuration for file-based logs that you can define.</span><span class="sxs-lookup"><span data-stu-id="d7184-185">Defines the buffer configuration for file-based logs that you can define.</span></span>

<span data-ttu-id="d7184-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="d7184-186">Parent element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>  


<span data-ttu-id="d7184-187">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-187">Attributes:</span></span>  

|<span data-ttu-id="d7184-188">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-188">Attribute</span></span>|<span data-ttu-id="d7184-189">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-189">Type</span></span>|<span data-ttu-id="d7184-190">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-190">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-191">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d7184-191">**bufferQuotaInMB**</span></span>|<span data-ttu-id="d7184-192">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="d7184-192">unsignedInt</span></span>|<span data-ttu-id="d7184-193">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-193">Optional.</span></span> <span data-ttu-id="d7184-194">Specifies the maximum amount of file system storage that is available for the specified data.</span><span class="sxs-lookup"><span data-stu-id="d7184-194">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="d7184-195">The default is 0.</span><span class="sxs-lookup"><span data-stu-id="d7184-195">The default is 0.</span></span>|  
|<span data-ttu-id="d7184-196">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="d7184-196">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="d7184-197">duration</span><span class="sxs-lookup"><span data-stu-id="d7184-197">duration</span></span>|<span data-ttu-id="d7184-198">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-198">Optional.</span></span> <span data-ttu-id="d7184-199">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="d7184-199">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="d7184-200">The default is PT0S.</span><span class="sxs-lookup"><span data-stu-id="d7184-200">The default is PT0S.</span></span>|  

## <a name="crashdumps-element"></a><span data-ttu-id="d7184-201">CrashDumps Element</span><span class="sxs-lookup"><span data-stu-id="d7184-201">CrashDumps Element</span></span>  
 <span data-ttu-id="d7184-202">Defines the crash dumps directory.</span><span class="sxs-lookup"><span data-stu-id="d7184-202">Defines the crash dumps directory.</span></span>

 <span data-ttu-id="d7184-203">Parent Element: [Directories Element](#Directories).</span><span class="sxs-lookup"><span data-stu-id="d7184-203">Parent Element: [Directories Element](#Directories).</span></span>  

<span data-ttu-id="d7184-204">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-204">Attributes:</span></span>  

|<span data-ttu-id="d7184-205">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-205">Attribute</span></span>|<span data-ttu-id="d7184-206">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-206">Type</span></span>|<span data-ttu-id="d7184-207">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-207">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-208">**container**</span><span class="sxs-lookup"><span data-stu-id="d7184-208">**container**</span></span>|<span data-ttu-id="d7184-209">string</span><span class="sxs-lookup"><span data-stu-id="d7184-209">string</span></span>|<span data-ttu-id="d7184-210">The name of the container where the contents of the directory is to be transferred.</span><span class="sxs-lookup"><span data-stu-id="d7184-210">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="d7184-211">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d7184-211">**directoryQuotaInMB**</span></span>|<span data-ttu-id="d7184-212">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="d7184-212">unsignedInt</span></span>|<span data-ttu-id="d7184-213">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-213">Optional.</span></span> <span data-ttu-id="d7184-214">Specifies the maximum size of the directory in megabytes.</span><span class="sxs-lookup"><span data-stu-id="d7184-214">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="d7184-215">The default is 0.</span><span class="sxs-lookup"><span data-stu-id="d7184-215">The default is 0.</span></span>|  

## <a name="failedrequestlogs-element"></a><span data-ttu-id="d7184-216">FailedRequestLogs Element</span><span class="sxs-lookup"><span data-stu-id="d7184-216">FailedRequestLogs Element</span></span>  
 <span data-ttu-id="d7184-217">Defines the failed request log directory.</span><span class="sxs-lookup"><span data-stu-id="d7184-217">Defines the failed request log directory.</span></span>

 <span data-ttu-id="d7184-218">Parent Element [Directories Element](#Directories).</span><span class="sxs-lookup"><span data-stu-id="d7184-218">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="d7184-219">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-219">Attributes:</span></span>  

|<span data-ttu-id="d7184-220">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-220">Attribute</span></span>|<span data-ttu-id="d7184-221">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-221">Type</span></span>|<span data-ttu-id="d7184-222">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-222">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-223">**container**</span><span class="sxs-lookup"><span data-stu-id="d7184-223">**container**</span></span>|<span data-ttu-id="d7184-224">string</span><span class="sxs-lookup"><span data-stu-id="d7184-224">string</span></span>|<span data-ttu-id="d7184-225">The name of the container where the contents of the directory is to be transferred.</span><span class="sxs-lookup"><span data-stu-id="d7184-225">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="d7184-226">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d7184-226">**directoryQuotaInMB**</span></span>|<span data-ttu-id="d7184-227">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="d7184-227">unsignedInt</span></span>|<span data-ttu-id="d7184-228">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-228">Optional.</span></span> <span data-ttu-id="d7184-229">Specifies the maximum size of the directory in megabytes.</span><span class="sxs-lookup"><span data-stu-id="d7184-229">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="d7184-230">The default is 0.</span><span class="sxs-lookup"><span data-stu-id="d7184-230">The default is 0.</span></span>|  

##  <a name="iislogs-element"></a><span data-ttu-id="d7184-231">IISLogs Element</span><span class="sxs-lookup"><span data-stu-id="d7184-231">IISLogs Element</span></span>  
 <span data-ttu-id="d7184-232">Defines the IIS log directory.</span><span class="sxs-lookup"><span data-stu-id="d7184-232">Defines the IIS log directory.</span></span>

 <span data-ttu-id="d7184-233">Parent Element [Directories Element](#Directories).</span><span class="sxs-lookup"><span data-stu-id="d7184-233">Parent Element [Directories Element](#Directories).</span></span>  

<span data-ttu-id="d7184-234">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-234">Attributes:</span></span>  

|<span data-ttu-id="d7184-235">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-235">Attribute</span></span>|<span data-ttu-id="d7184-236">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-236">Type</span></span>|<span data-ttu-id="d7184-237">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-237">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-238">**container**</span><span class="sxs-lookup"><span data-stu-id="d7184-238">**container**</span></span>|<span data-ttu-id="d7184-239">string</span><span class="sxs-lookup"><span data-stu-id="d7184-239">string</span></span>|<span data-ttu-id="d7184-240">The name of the container where the contents of the directory is to be transferred.</span><span class="sxs-lookup"><span data-stu-id="d7184-240">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="d7184-241">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d7184-241">**directoryQuotaInMB**</span></span>|<span data-ttu-id="d7184-242">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="d7184-242">unsignedInt</span></span>|<span data-ttu-id="d7184-243">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-243">Optional.</span></span> <span data-ttu-id="d7184-244">Specifies the maximum size of the directory in megabytes.</span><span class="sxs-lookup"><span data-stu-id="d7184-244">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="d7184-245">The default is 0.</span><span class="sxs-lookup"><span data-stu-id="d7184-245">The default is 0.</span></span>|  

## <a name="datasources-element"></a><span data-ttu-id="d7184-246">DataSources Element</span><span class="sxs-lookup"><span data-stu-id="d7184-246">DataSources Element</span></span>  
 <span data-ttu-id="d7184-247">Defines zero or more additional log directories.</span><span class="sxs-lookup"><span data-stu-id="d7184-247">Defines zero or more additional log directories.</span></span>

 <span data-ttu-id="d7184-248">Parent Element: [Directories Element](#Directories).</span><span class="sxs-lookup"><span data-stu-id="d7184-248">Parent Element: [Directories Element](#Directories).</span></span>

## <a name="directoryconfiguration-element"></a><span data-ttu-id="d7184-249">DirectoryConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="d7184-249">DirectoryConfiguration Element</span></span>  
 <span data-ttu-id="d7184-250">Defines the directory of log files to monitor.</span><span class="sxs-lookup"><span data-stu-id="d7184-250">Defines the directory of log files to monitor.</span></span>

 <span data-ttu-id="d7184-251">Parent Element: [DataSources Element](#DataSources).</span><span class="sxs-lookup"><span data-stu-id="d7184-251">Parent Element: [DataSources Element](#DataSources).</span></span>

<span data-ttu-id="d7184-252">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-252">Attributes:</span></span>

|<span data-ttu-id="d7184-253">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-253">Attribute</span></span>|<span data-ttu-id="d7184-254">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-254">Type</span></span>|<span data-ttu-id="d7184-255">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-255">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-256">**container**</span><span class="sxs-lookup"><span data-stu-id="d7184-256">**container**</span></span>|<span data-ttu-id="d7184-257">string</span><span class="sxs-lookup"><span data-stu-id="d7184-257">string</span></span>|<span data-ttu-id="d7184-258">The name of the container where the contents of the directory is to be transferred.</span><span class="sxs-lookup"><span data-stu-id="d7184-258">The name of the container where the contents of the directory is to be transferred.</span></span>|  
|<span data-ttu-id="d7184-259">**directoryQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d7184-259">**directoryQuotaInMB**</span></span>|<span data-ttu-id="d7184-260">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="d7184-260">unsignedInt</span></span>|<span data-ttu-id="d7184-261">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-261">Optional.</span></span> <span data-ttu-id="d7184-262">Specifies the maximum size of the directory in megabytes.</span><span class="sxs-lookup"><span data-stu-id="d7184-262">Specifies the maximum size of the directory in megabytes.</span></span><br /><br /> <span data-ttu-id="d7184-263">The default is 0.</span><span class="sxs-lookup"><span data-stu-id="d7184-263">The default is 0.</span></span>|  

## <a name="absolute-element"></a><span data-ttu-id="d7184-264">Absolute Element</span><span class="sxs-lookup"><span data-stu-id="d7184-264">Absolute Element</span></span>  
 <span data-ttu-id="d7184-265">Defines an absolute path of the directory to monitor with optional environment expansion.</span><span class="sxs-lookup"><span data-stu-id="d7184-265">Defines an absolute path of the directory to monitor with optional environment expansion.</span></span>

 <span data-ttu-id="d7184-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="d7184-266">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="d7184-267">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-267">Attributes:</span></span>  

|<span data-ttu-id="d7184-268">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-268">Attribute</span></span>|<span data-ttu-id="d7184-269">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-269">Type</span></span>|<span data-ttu-id="d7184-270">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-270">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-271">**path**</span><span class="sxs-lookup"><span data-stu-id="d7184-271">**path**</span></span>|<span data-ttu-id="d7184-272">string</span><span class="sxs-lookup"><span data-stu-id="d7184-272">string</span></span>|<span data-ttu-id="d7184-273">Required.</span><span class="sxs-lookup"><span data-stu-id="d7184-273">Required.</span></span> <span data-ttu-id="d7184-274">The absolute path to the directory to monitor.</span><span class="sxs-lookup"><span data-stu-id="d7184-274">The absolute path to the directory to monitor.</span></span>|  
|<span data-ttu-id="d7184-275">**expandEnvironment**</span><span class="sxs-lookup"><span data-stu-id="d7184-275">**expandEnvironment**</span></span>|<span data-ttu-id="d7184-276">boolean</span><span class="sxs-lookup"><span data-stu-id="d7184-276">boolean</span></span>|<span data-ttu-id="d7184-277">Required.</span><span class="sxs-lookup"><span data-stu-id="d7184-277">Required.</span></span> <span data-ttu-id="d7184-278">If set to **true**, environment variables in the path are expanded.</span><span class="sxs-lookup"><span data-stu-id="d7184-278">If set to **true**, environment variables in the path are expanded.</span></span>|  

## <a name="localresource-element"></a><span data-ttu-id="d7184-279">LocalResource Element</span><span class="sxs-lookup"><span data-stu-id="d7184-279">LocalResource Element</span></span>  
 <span data-ttu-id="d7184-280">Defines a path relative to a local resource defined in the service definition.</span><span class="sxs-lookup"><span data-stu-id="d7184-280">Defines a path relative to a local resource defined in the service definition.</span></span>

 <span data-ttu-id="d7184-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span><span class="sxs-lookup"><span data-stu-id="d7184-281">Parent Element: [DirectoryConfiguration Element](#DirectoryConfiguration).</span></span>  

<span data-ttu-id="d7184-282">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-282">Attributes:</span></span>  

|<span data-ttu-id="d7184-283">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-283">Attribute</span></span>|<span data-ttu-id="d7184-284">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-284">Type</span></span>|<span data-ttu-id="d7184-285">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-285">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-286">**name**</span><span class="sxs-lookup"><span data-stu-id="d7184-286">**name**</span></span>|<span data-ttu-id="d7184-287">string</span><span class="sxs-lookup"><span data-stu-id="d7184-287">string</span></span>|<span data-ttu-id="d7184-288">Required.</span><span class="sxs-lookup"><span data-stu-id="d7184-288">Required.</span></span> <span data-ttu-id="d7184-289">The name of the local resource that contains the directory to monitor.</span><span class="sxs-lookup"><span data-stu-id="d7184-289">The name of the local resource that contains the directory to monitor.</span></span>|  
|<span data-ttu-id="d7184-290">**relativePath**</span><span class="sxs-lookup"><span data-stu-id="d7184-290">**relativePath**</span></span>|<span data-ttu-id="d7184-291">string</span><span class="sxs-lookup"><span data-stu-id="d7184-291">string</span></span>|<span data-ttu-id="d7184-292">Required.</span><span class="sxs-lookup"><span data-stu-id="d7184-292">Required.</span></span> <span data-ttu-id="d7184-293">The path relative to the local resource to monitor.</span><span class="sxs-lookup"><span data-stu-id="d7184-293">The path relative to the local resource to monitor.</span></span>|  

## <a name="performancecounters-element"></a><span data-ttu-id="d7184-294">PerformanceCounters Element</span><span class="sxs-lookup"><span data-stu-id="d7184-294">PerformanceCounters Element</span></span>  
 <span data-ttu-id="d7184-295">Defines the path to the performance counter to collect.</span><span class="sxs-lookup"><span data-stu-id="d7184-295">Defines the path to the performance counter to collect.</span></span>

 <span data-ttu-id="d7184-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="d7184-296">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>


 <span data-ttu-id="d7184-297">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-297">Attributes:</span></span>  

|<span data-ttu-id="d7184-298">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-298">Attribute</span></span>|<span data-ttu-id="d7184-299">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-299">Type</span></span>|<span data-ttu-id="d7184-300">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-300">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-301">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d7184-301">**bufferQuotaInMB**</span></span>|<span data-ttu-id="d7184-302">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="d7184-302">unsignedInt</span></span>|<span data-ttu-id="d7184-303">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-303">Optional.</span></span> <span data-ttu-id="d7184-304">Specifies the maximum amount of file system storage that is available for the specified data.</span><span class="sxs-lookup"><span data-stu-id="d7184-304">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="d7184-305">The default is 0.</span><span class="sxs-lookup"><span data-stu-id="d7184-305">The default is 0.</span></span>|  
|<span data-ttu-id="d7184-306">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="d7184-306">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="d7184-307">duration</span><span class="sxs-lookup"><span data-stu-id="d7184-307">duration</span></span>|<span data-ttu-id="d7184-308">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-308">Optional.</span></span> <span data-ttu-id="d7184-309">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="d7184-309">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="d7184-310">The default is PT0S.</span><span class="sxs-lookup"><span data-stu-id="d7184-310">The default is PT0S.</span></span>|  

## <a name="performancecounterconfiguration-element"></a><span data-ttu-id="d7184-311">PerformanceCounterConfiguration Element</span><span class="sxs-lookup"><span data-stu-id="d7184-311">PerformanceCounterConfiguration Element</span></span>  
 <span data-ttu-id="d7184-312">Defines the performance counter to collect.</span><span class="sxs-lookup"><span data-stu-id="d7184-312">Defines the performance counter to collect.</span></span>

 <span data-ttu-id="d7184-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span><span class="sxs-lookup"><span data-stu-id="d7184-313">Parent Element: [PerformanceCounters Element](#PerformanceCounters).</span></span>  

 <span data-ttu-id="d7184-314">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-314">Attributes:</span></span>  

|<span data-ttu-id="d7184-315">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-315">Attribute</span></span>|<span data-ttu-id="d7184-316">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-316">Type</span></span>|<span data-ttu-id="d7184-317">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-317">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-318">**counterSpecifier**</span><span class="sxs-lookup"><span data-stu-id="d7184-318">**counterSpecifier**</span></span>|<span data-ttu-id="d7184-319">string</span><span class="sxs-lookup"><span data-stu-id="d7184-319">string</span></span>|<span data-ttu-id="d7184-320">Required.</span><span class="sxs-lookup"><span data-stu-id="d7184-320">Required.</span></span> <span data-ttu-id="d7184-321">The path to the performance counter to collect.</span><span class="sxs-lookup"><span data-stu-id="d7184-321">The path to the performance counter to collect.</span></span>|  
|<span data-ttu-id="d7184-322">**sampleRate**</span><span class="sxs-lookup"><span data-stu-id="d7184-322">**sampleRate**</span></span>|<span data-ttu-id="d7184-323">duration</span><span class="sxs-lookup"><span data-stu-id="d7184-323">duration</span></span>|<span data-ttu-id="d7184-324">Required.</span><span class="sxs-lookup"><span data-stu-id="d7184-324">Required.</span></span> <span data-ttu-id="d7184-325">The rate at which the performance counter should be collected.</span><span class="sxs-lookup"><span data-stu-id="d7184-325">The rate at which the performance counter should be collected.</span></span>|  

## <a name="windowseventlog-element"></a><span data-ttu-id="d7184-326">WindowsEventLog Element</span><span class="sxs-lookup"><span data-stu-id="d7184-326">WindowsEventLog Element</span></span>  
 <span data-ttu-id="d7184-327">Defines the event logs to monitor.</span><span class="sxs-lookup"><span data-stu-id="d7184-327">Defines the event logs to monitor.</span></span>

 <span data-ttu-id="d7184-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span><span class="sxs-lookup"><span data-stu-id="d7184-328">Parent Element: [DiagnosticMonitorConfiguration Element](#DiagnosticMonitorConfiguration).</span></span>

  <span data-ttu-id="d7184-329">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-329">Attributes:</span></span>

|<span data-ttu-id="d7184-330">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-330">Attribute</span></span>|<span data-ttu-id="d7184-331">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-331">Type</span></span>|<span data-ttu-id="d7184-332">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-332">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-333">**bufferQuotaInMB**</span><span class="sxs-lookup"><span data-stu-id="d7184-333">**bufferQuotaInMB**</span></span>|<span data-ttu-id="d7184-334">unsignedInt</span><span class="sxs-lookup"><span data-stu-id="d7184-334">unsignedInt</span></span>|<span data-ttu-id="d7184-335">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-335">Optional.</span></span> <span data-ttu-id="d7184-336">Specifies the maximum amount of file system storage that is available for the specified data.</span><span class="sxs-lookup"><span data-stu-id="d7184-336">Specifies the maximum amount of file system storage that is available for the specified data.</span></span><br /><br /> <span data-ttu-id="d7184-337">The default is 0.</span><span class="sxs-lookup"><span data-stu-id="d7184-337">The default is 0.</span></span>|  
|<span data-ttu-id="d7184-338">**scheduledTransferLogLevelFilter**</span><span class="sxs-lookup"><span data-stu-id="d7184-338">**scheduledTransferLogLevelFilter**</span></span>|<span data-ttu-id="d7184-339">string</span><span class="sxs-lookup"><span data-stu-id="d7184-339">string</span></span>|<span data-ttu-id="d7184-340">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-340">Optional.</span></span> <span data-ttu-id="d7184-341">Specifies the minimum severity level for log entries that are transferred.</span><span class="sxs-lookup"><span data-stu-id="d7184-341">Specifies the minimum severity level for log entries that are transferred.</span></span> <span data-ttu-id="d7184-342">The default value is **Undefined**.</span><span class="sxs-lookup"><span data-stu-id="d7184-342">The default value is **Undefined**.</span></span> <span data-ttu-id="d7184-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span><span class="sxs-lookup"><span data-stu-id="d7184-343">Other possible values are **Verbose**, **Information**, **Warning**, **Error**, and **Critical**.</span></span>|  
|<span data-ttu-id="d7184-344">**scheduledTransferPeriod**</span><span class="sxs-lookup"><span data-stu-id="d7184-344">**scheduledTransferPeriod**</span></span>|<span data-ttu-id="d7184-345">duration</span><span class="sxs-lookup"><span data-stu-id="d7184-345">duration</span></span>|<span data-ttu-id="d7184-346">Optional.</span><span class="sxs-lookup"><span data-stu-id="d7184-346">Optional.</span></span> <span data-ttu-id="d7184-347">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span><span class="sxs-lookup"><span data-stu-id="d7184-347">Specifies the interval between scheduled transfers of data, rounded up to the nearest minute.</span></span><br /><br /> <span data-ttu-id="d7184-348">The default is PT0S.</span><span class="sxs-lookup"><span data-stu-id="d7184-348">The default is PT0S.</span></span>|  

## <a name="datasource-element"></a><span data-ttu-id="d7184-349">DataSource Element</span><span class="sxs-lookup"><span data-stu-id="d7184-349">DataSource Element</span></span>  
 <span data-ttu-id="d7184-350">Defines the event log to monitor.</span><span class="sxs-lookup"><span data-stu-id="d7184-350">Defines the event log to monitor.</span></span>

 <span data-ttu-id="d7184-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span><span class="sxs-lookup"><span data-stu-id="d7184-351">Parent Element: [WindowsEventLog Element](#windowsEventLog).</span></span>  

 <span data-ttu-id="d7184-352">Attributes:</span><span class="sxs-lookup"><span data-stu-id="d7184-352">Attributes:</span></span>

|<span data-ttu-id="d7184-353">Attribute</span><span class="sxs-lookup"><span data-stu-id="d7184-353">Attribute</span></span>|<span data-ttu-id="d7184-354">Type</span><span class="sxs-lookup"><span data-stu-id="d7184-354">Type</span></span>|<span data-ttu-id="d7184-355">Description</span><span class="sxs-lookup"><span data-stu-id="d7184-355">Description</span></span>|  
|---------------|----------|-----------------|  
|<span data-ttu-id="d7184-356">**name**</span><span class="sxs-lookup"><span data-stu-id="d7184-356">**name**</span></span>|<span data-ttu-id="d7184-357">string</span><span class="sxs-lookup"><span data-stu-id="d7184-357">string</span></span>|<span data-ttu-id="d7184-358">Required.</span><span class="sxs-lookup"><span data-stu-id="d7184-358">Required.</span></span> <span data-ttu-id="d7184-359">An XPath expression specifying the log to collect.</span><span class="sxs-lookup"><span data-stu-id="d7184-359">An XPath expression specifying the log to collect.</span></span>|  
