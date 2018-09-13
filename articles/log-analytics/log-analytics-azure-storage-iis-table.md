---
title: Use blob storage for IIS and table storage for events in Azure Log Analytics | Microsoft Docs
description: Log Analytics can read the logs for Azure services that write diagnostics to table storage or IIS logs written to blob storage.
services: log-analytics
documentationcenter: ''
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: bf444752-ecc1-4306-9489-c29cb37d6045
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 04/12/2017
ms.author: magoedte
ms.component: na
ms.openlocfilehash: 26599a47847dafa0c5aae6519479d2f29318001d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44784269"
---
# <a name="use-azure-blob-storage-for-iis-and-azure-table-storage-for-events-with-log-analytics"></a><span data-ttu-id="07dc4-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span><span class="sxs-lookup"><span data-stu-id="07dc4-103">Use Azure blob storage for IIS and Azure table storage for events with Log Analytics</span></span>

<span data-ttu-id="07dc4-104">Log Analytics can read the logs for the following services that write diagnostics to table storage or IIS logs written to blob storage:</span><span class="sxs-lookup"><span data-stu-id="07dc4-104">Log Analytics can read the logs for the following services that write diagnostics to table storage or IIS logs written to blob storage:</span></span>

* <span data-ttu-id="07dc4-105">Service Fabric clusters (Preview)</span><span class="sxs-lookup"><span data-stu-id="07dc4-105">Service Fabric clusters (Preview)</span></span>
* <span data-ttu-id="07dc4-106">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="07dc4-106">Virtual Machines</span></span>
* <span data-ttu-id="07dc4-107">Web/Worker Roles</span><span class="sxs-lookup"><span data-stu-id="07dc4-107">Web/Worker Roles</span></span>

<span data-ttu-id="07dc4-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span><span class="sxs-lookup"><span data-stu-id="07dc4-108">Before Log Analytics can collect data for these resources, Azure diagnostics must be enabled.</span></span>

<span data-ttu-id="07dc4-109">Once diagnostics are enabled, you can use the Azure portal or PowerShell configure Log Analytics to collect the logs.</span><span class="sxs-lookup"><span data-stu-id="07dc4-109">Once diagnostics are enabled, you can use the Azure portal or PowerShell configure Log Analytics to collect the logs.</span></span>

<span data-ttu-id="07dc4-110">Azure Diagnostics is an Azure extension that enables you to collect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span><span class="sxs-lookup"><span data-stu-id="07dc4-110">Azure Diagnostics is an Azure extension that enables you to collect diagnostic data from a worker role, web role, or virtual machine running in Azure.</span></span> <span data-ttu-id="07dc4-111">The data is stored in an Azure storage account and can then be collected by Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="07dc4-111">The data is stored in an Azure storage account and can then be collected by Log Analytics.</span></span>

<span data-ttu-id="07dc4-112">For Log Analytics to collect these Azure Diagnostics logs, the logs must be in the following locations:</span><span class="sxs-lookup"><span data-stu-id="07dc4-112">For Log Analytics to collect these Azure Diagnostics logs, the logs must be in the following locations:</span></span>

| <span data-ttu-id="07dc4-113">Log Type</span><span class="sxs-lookup"><span data-stu-id="07dc4-113">Log Type</span></span> | <span data-ttu-id="07dc4-114">Resource Type</span><span class="sxs-lookup"><span data-stu-id="07dc4-114">Resource Type</span></span> | <span data-ttu-id="07dc4-115">Location</span><span class="sxs-lookup"><span data-stu-id="07dc4-115">Location</span></span> |
| --- | --- | --- |
| <span data-ttu-id="07dc4-116">IIS logs</span><span class="sxs-lookup"><span data-stu-id="07dc4-116">IIS logs</span></span> |<span data-ttu-id="07dc4-117">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="07dc4-117">Virtual Machines</span></span> <br> <span data-ttu-id="07dc4-118">Web roles</span><span class="sxs-lookup"><span data-stu-id="07dc4-118">Web roles</span></span> <br> <span data-ttu-id="07dc4-119">Worker roles</span><span class="sxs-lookup"><span data-stu-id="07dc4-119">Worker roles</span></span> |<span data-ttu-id="07dc4-120">wad-iis-logfiles (Blob Storage)</span><span class="sxs-lookup"><span data-stu-id="07dc4-120">wad-iis-logfiles (Blob Storage)</span></span> |
| <span data-ttu-id="07dc4-121">Syslog</span><span class="sxs-lookup"><span data-stu-id="07dc4-121">Syslog</span></span> |<span data-ttu-id="07dc4-122">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="07dc4-122">Virtual Machines</span></span> |<span data-ttu-id="07dc4-123">LinuxsyslogVer2v0 (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="07dc4-123">LinuxsyslogVer2v0 (Table Storage)</span></span> |
| <span data-ttu-id="07dc4-124">Service Fabric Operational Events</span><span class="sxs-lookup"><span data-stu-id="07dc4-124">Service Fabric Operational Events</span></span> |<span data-ttu-id="07dc4-125">Service Fabric nodes</span><span class="sxs-lookup"><span data-stu-id="07dc4-125">Service Fabric nodes</span></span> |<span data-ttu-id="07dc4-126">WADServiceFabricSystemEventTable</span><span class="sxs-lookup"><span data-stu-id="07dc4-126">WADServiceFabricSystemEventTable</span></span> |
| <span data-ttu-id="07dc4-127">Service Fabric Reliable Actor Events</span><span class="sxs-lookup"><span data-stu-id="07dc4-127">Service Fabric Reliable Actor Events</span></span> |<span data-ttu-id="07dc4-128">Service Fabric nodes</span><span class="sxs-lookup"><span data-stu-id="07dc4-128">Service Fabric nodes</span></span> |<span data-ttu-id="07dc4-129">WADServiceFabricReliableActorEventTable</span><span class="sxs-lookup"><span data-stu-id="07dc4-129">WADServiceFabricReliableActorEventTable</span></span> |
| <span data-ttu-id="07dc4-130">Service Fabric Reliable Service Events</span><span class="sxs-lookup"><span data-stu-id="07dc4-130">Service Fabric Reliable Service Events</span></span> |<span data-ttu-id="07dc4-131">Service Fabric nodes</span><span class="sxs-lookup"><span data-stu-id="07dc4-131">Service Fabric nodes</span></span> |<span data-ttu-id="07dc4-132">WADServiceFabricReliableServiceEventTable</span><span class="sxs-lookup"><span data-stu-id="07dc4-132">WADServiceFabricReliableServiceEventTable</span></span> |
| <span data-ttu-id="07dc4-133">Windows Event logs</span><span class="sxs-lookup"><span data-stu-id="07dc4-133">Windows Event logs</span></span> |<span data-ttu-id="07dc4-134">Service Fabric nodes</span><span class="sxs-lookup"><span data-stu-id="07dc4-134">Service Fabric nodes</span></span> <br> <span data-ttu-id="07dc4-135">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="07dc4-135">Virtual Machines</span></span> <br> <span data-ttu-id="07dc4-136">Web roles</span><span class="sxs-lookup"><span data-stu-id="07dc4-136">Web roles</span></span> <br> <span data-ttu-id="07dc4-137">Worker roles</span><span class="sxs-lookup"><span data-stu-id="07dc4-137">Worker roles</span></span> |<span data-ttu-id="07dc4-138">WADWindowsEventLogsTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="07dc4-138">WADWindowsEventLogsTable (Table Storage)</span></span> |
| <span data-ttu-id="07dc4-139">Windows ETW logs</span><span class="sxs-lookup"><span data-stu-id="07dc4-139">Windows ETW logs</span></span> |<span data-ttu-id="07dc4-140">Service Fabric nodes</span><span class="sxs-lookup"><span data-stu-id="07dc4-140">Service Fabric nodes</span></span> <br> <span data-ttu-id="07dc4-141">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="07dc4-141">Virtual Machines</span></span> <br> <span data-ttu-id="07dc4-142">Web roles</span><span class="sxs-lookup"><span data-stu-id="07dc4-142">Web roles</span></span> <br> <span data-ttu-id="07dc4-143">Worker roles</span><span class="sxs-lookup"><span data-stu-id="07dc4-143">Worker roles</span></span> |<span data-ttu-id="07dc4-144">WADETWEventTable (Table Storage)</span><span class="sxs-lookup"><span data-stu-id="07dc4-144">WADETWEventTable (Table Storage)</span></span> |

> [!NOTE]
> <span data-ttu-id="07dc4-145">IIS logs from Azure Websites are not currently supported.</span><span class="sxs-lookup"><span data-stu-id="07dc4-145">IIS logs from Azure Websites are not currently supported.</span></span>
>
>

<span data-ttu-id="07dc4-146">For virtual machines, you have the option of installing the [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine to enable additional insights.</span><span class="sxs-lookup"><span data-stu-id="07dc4-146">For virtual machines, you have the option of installing the [Log Analytics agent](log-analytics-azure-vm-extension.md) into your virtual machine to enable additional insights.</span></span> <span data-ttu-id="07dc4-147">In addition to being able to analyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span><span class="sxs-lookup"><span data-stu-id="07dc4-147">In addition to being able to analyze IIS logs and Event Logs, you can perform additional analysis including configuration change tracking, SQL assessment, and update assessment.</span></span>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection"></a><span data-ttu-id="07dc4-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span><span class="sxs-lookup"><span data-stu-id="07dc4-148">Enable Azure diagnostics in a virtual machine for event log and IIS log collection</span></span>
<span data-ttu-id="07dc4-149">Use the following procedure to enable Azure diagnostics in a virtual machine for Event Log and IIS log collection using the Microsoft Azure portal.</span><span class="sxs-lookup"><span data-stu-id="07dc4-149">Use the following procedure to enable Azure diagnostics in a virtual machine for Event Log and IIS log collection using the Microsoft Azure portal.</span></span>

### <a name="to-enable-azure-diagnostics-in-a-virtual-machine-with-the-azure-portal"></a><span data-ttu-id="07dc4-150">To enable Azure diagnostics in a virtual machine with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="07dc4-150">To enable Azure diagnostics in a virtual machine with the Azure portal</span></span>
1. <span data-ttu-id="07dc4-151">Install the VM Agent when you create a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="07dc4-151">Install the VM Agent when you create a virtual machine.</span></span> <span data-ttu-id="07dc4-152">If the virtual machine already exists, verify that the VM Agent is already installed.</span><span class="sxs-lookup"><span data-stu-id="07dc4-152">If the virtual machine already exists, verify that the VM Agent is already installed.</span></span>

   * <span data-ttu-id="07dc4-153">In the Azure portal, navigate to the virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** to **On**.</span><span class="sxs-lookup"><span data-stu-id="07dc4-153">In the Azure portal, navigate to the virtual machine, select **Optional Configuration**, then **Diagnostics** and set **Status** to **On**.</span></span>

     <span data-ttu-id="07dc4-154">Upon completion, the VM has the Azure Diagnostics extension installed and running.</span><span class="sxs-lookup"><span data-stu-id="07dc4-154">Upon completion, the VM has the Azure Diagnostics extension installed and running.</span></span> <span data-ttu-id="07dc4-155">This extension is responsible for collecting your diagnostics data.</span><span class="sxs-lookup"><span data-stu-id="07dc4-155">This extension is responsible for collecting your diagnostics data.</span></span>
2. <span data-ttu-id="07dc4-156">Enable monitoring and configure event logging on an existing VM.</span><span class="sxs-lookup"><span data-stu-id="07dc4-156">Enable monitoring and configure event logging on an existing VM.</span></span> <span data-ttu-id="07dc4-157">You can enable diagnostics at the VM level.</span><span class="sxs-lookup"><span data-stu-id="07dc4-157">You can enable diagnostics at the VM level.</span></span> <span data-ttu-id="07dc4-158">To enable diagnostics and then configure event logging, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="07dc4-158">To enable diagnostics and then configure event logging, perform the following steps:</span></span>

   1. <span data-ttu-id="07dc4-159">Select the VM.</span><span class="sxs-lookup"><span data-stu-id="07dc4-159">Select the VM.</span></span>
   2. <span data-ttu-id="07dc4-160">Click **Monitoring**.</span><span class="sxs-lookup"><span data-stu-id="07dc4-160">Click **Monitoring**.</span></span>
   3. <span data-ttu-id="07dc4-161">Click **Diagnostics**.</span><span class="sxs-lookup"><span data-stu-id="07dc4-161">Click **Diagnostics**.</span></span>
   4. <span data-ttu-id="07dc4-162">Set the **Status** to **ON**.</span><span class="sxs-lookup"><span data-stu-id="07dc4-162">Set the **Status** to **ON**.</span></span>
   5. <span data-ttu-id="07dc4-163">Select each diagnostics log that you want to collect.</span><span class="sxs-lookup"><span data-stu-id="07dc4-163">Select each diagnostics log that you want to collect.</span></span>
   6. <span data-ttu-id="07dc4-164">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="07dc4-164">Click **OK**.</span></span>

## <a name="enable-azure-diagnostics-in-a-web-role-for-iis-log-and-event-collection"></a><span data-ttu-id="07dc4-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span><span class="sxs-lookup"><span data-stu-id="07dc4-165">Enable Azure diagnostics in a Web role for IIS log and event collection</span></span>
<span data-ttu-id="07dc4-166">Refer to [How To Enable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span><span class="sxs-lookup"><span data-stu-id="07dc4-166">Refer to [How To Enable Diagnostics in a Cloud Service](../cloud-services/cloud-services-dotnet-diagnostics.md) for general steps on enabling Azure diagnostics.</span></span> <span data-ttu-id="07dc4-167">The instructions below use this information and customize it for use with Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="07dc4-167">The instructions below use this information and customize it for use with Log Analytics.</span></span>

<span data-ttu-id="07dc4-168">With Azure diagnostics enabled:</span><span class="sxs-lookup"><span data-stu-id="07dc4-168">With Azure diagnostics enabled:</span></span>

* <span data-ttu-id="07dc4-169">IIS logs are stored by default, with log data transferred at the scheduledTransferPeriod transfer interval.</span><span class="sxs-lookup"><span data-stu-id="07dc4-169">IIS logs are stored by default, with log data transferred at the scheduledTransferPeriod transfer interval.</span></span>
* <span data-ttu-id="07dc4-170">Windows Event Logs are not transferred by default.</span><span class="sxs-lookup"><span data-stu-id="07dc4-170">Windows Event Logs are not transferred by default.</span></span>

### <a name="to-enable-diagnostics"></a><span data-ttu-id="07dc4-171">To enable diagnostics</span><span class="sxs-lookup"><span data-stu-id="07dc4-171">To enable diagnostics</span></span>
<span data-ttu-id="07dc4-172">To enable Windows Event Logs, or to change the scheduledTransferPeriod, configure Azure Diagnostics using the XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install the extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span><span class="sxs-lookup"><span data-stu-id="07dc4-172">To enable Windows Event Logs, or to change the scheduledTransferPeriod, configure Azure Diagnostics using the XML configuration file (diagnostics.wadcfg), as shown in [Step 4: Create your Diagnostics configuration file and install the extension](../cloud-services/cloud-services-dotnet-diagnostics.md)</span></span>

<span data-ttu-id="07dc4-173">The following example configuration file collects IIS Logs and all Events from the Application and System logs:</span><span class="sxs-lookup"><span data-stu-id="07dc4-173">The following example configuration file collects IIS Logs and all Events from the Application and System logs:</span></span>

```
    <?xml version="1.0" encoding="utf-8" ?>
    <DiagnosticMonitorConfiguration xmlns="http://schemas.microsoft.com/ServiceHosting/2010/10/DiagnosticsConfiguration"
          configurationChangePollInterval="PT1M"
          overallQuotaInMB="4096">

      <Directories bufferQuotaInMB="0"
         scheduledTransferPeriod="PT10M">  
        <!-- IISLogs are only relevant to Web roles -->
        <IISLogs container="wad-iis" directoryQuotaInMB="0" />
      </Directories>

      <WindowsEventLog bufferQuotaInMB="0"
         scheduledTransferLogLevelFilter="Verbose"
         scheduledTransferPeriod="PT10M">
        <DataSource name="Application!*" />
        <DataSource name="System!*" />
      </WindowsEventLog>

    </DiagnosticMonitorConfiguration>
```

<span data-ttu-id="07dc4-174">Ensure that your ConfigurationSettings specifies a storage account, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="07dc4-174">Ensure that your ConfigurationSettings specifies a storage account, as in the following example:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<AccountName>;AccountKey=<AccountKey>"/>
    </ConfigurationSettings>
```

<span data-ttu-id="07dc4-175">The **AccountName** and **AccountKey** values are found in the Azure portal in the storage account dashboard, under Manage Access Keys.</span><span class="sxs-lookup"><span data-stu-id="07dc4-175">The **AccountName** and **AccountKey** values are found in the Azure portal in the storage account dashboard, under Manage Access Keys.</span></span> <span data-ttu-id="07dc4-176">The protocol for the connection string must be **https**.</span><span class="sxs-lookup"><span data-stu-id="07dc4-176">The protocol for the connection string must be **https**.</span></span>

<span data-ttu-id="07dc4-177">Once the updated diagnostic configuration is applied to your cloud service and it is writing diagnostics to Azure Storage, then you are ready to configure Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="07dc4-177">Once the updated diagnostic configuration is applied to your cloud service and it is writing diagnostics to Azure Storage, then you are ready to configure Log Analytics.</span></span>

## <a name="use-the-azure-portal-to-collect-logs-from-azure-storage"></a><span data-ttu-id="07dc4-178">Use the Azure portal to collect logs from Azure Storage</span><span class="sxs-lookup"><span data-stu-id="07dc4-178">Use the Azure portal to collect logs from Azure Storage</span></span>
<span data-ttu-id="07dc4-179">You can use the Azure portal to configure Log Analytics to collect the logs for the following Azure services:</span><span class="sxs-lookup"><span data-stu-id="07dc4-179">You can use the Azure portal to configure Log Analytics to collect the logs for the following Azure services:</span></span>

* <span data-ttu-id="07dc4-180">Service Fabric clusters</span><span class="sxs-lookup"><span data-stu-id="07dc4-180">Service Fabric clusters</span></span>
* <span data-ttu-id="07dc4-181">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="07dc4-181">Virtual Machines</span></span>
* <span data-ttu-id="07dc4-182">Web/Worker Roles</span><span class="sxs-lookup"><span data-stu-id="07dc4-182">Web/Worker Roles</span></span>

<span data-ttu-id="07dc4-183">In the Azure portal, navigate to your Log Analytics workspace and perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="07dc4-183">In the Azure portal, navigate to your Log Analytics workspace and perform the following tasks:</span></span>

1. <span data-ttu-id="07dc4-184">Click *Storage accounts logs*</span><span class="sxs-lookup"><span data-stu-id="07dc4-184">Click *Storage accounts logs*</span></span>
2. <span data-ttu-id="07dc4-185">Click the *Add* task</span><span class="sxs-lookup"><span data-stu-id="07dc4-185">Click the *Add* task</span></span>
3. <span data-ttu-id="07dc4-186">Select the Storage account that contains the diagnostics logs</span><span class="sxs-lookup"><span data-stu-id="07dc4-186">Select the Storage account that contains the diagnostics logs</span></span>
   * <span data-ttu-id="07dc4-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span><span class="sxs-lookup"><span data-stu-id="07dc4-187">This account can be either a classic storage account or an Azure Resource Manager storage account</span></span>
4. <span data-ttu-id="07dc4-188">Select the Data Type you want to collect logs for</span><span class="sxs-lookup"><span data-stu-id="07dc4-188">Select the Data Type you want to collect logs for</span></span>
   * <span data-ttu-id="07dc4-189">The choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span><span class="sxs-lookup"><span data-stu-id="07dc4-189">The choices are IIS Logs; Events; Syslog (Linux); ETW Logs; Service Fabric Events</span></span>
5. <span data-ttu-id="07dc4-190">The value for Source is automatically populated based on the data type and cannot be changed</span><span class="sxs-lookup"><span data-stu-id="07dc4-190">The value for Source is automatically populated based on the data type and cannot be changed</span></span>
6. <span data-ttu-id="07dc4-191">Click OK to save the configuration</span><span class="sxs-lookup"><span data-stu-id="07dc4-191">Click OK to save the configuration</span></span>

<span data-ttu-id="07dc4-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics to collect.</span><span class="sxs-lookup"><span data-stu-id="07dc4-192">Repeat steps 2-6 for additional storage accounts and data types that you want Log Analytics to collect.</span></span>

<span data-ttu-id="07dc4-193">In approximately 30 minutes, you are able to see data from the storage account in Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="07dc4-193">In approximately 30 minutes, you are able to see data from the storage account in Log Analytics.</span></span> <span data-ttu-id="07dc4-194">You will only see data that is written to storage after the configuration is applied.</span><span class="sxs-lookup"><span data-stu-id="07dc4-194">You will only see data that is written to storage after the configuration is applied.</span></span> <span data-ttu-id="07dc4-195">Log Analytics does not read the pre-existing data from the storage account.</span><span class="sxs-lookup"><span data-stu-id="07dc4-195">Log Analytics does not read the pre-existing data from the storage account.</span></span>

> [!NOTE]
> <span data-ttu-id="07dc4-196">The portal does not validate that the Source exists in the storage account or if new data is being written.</span><span class="sxs-lookup"><span data-stu-id="07dc4-196">The portal does not validate that the Source exists in the storage account or if new data is being written.</span></span>
>
>

## <a name="enable-azure-diagnostics-in-a-virtual-machine-for-event-log-and-iis-log-collection-using-powershell"></a><span data-ttu-id="07dc4-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span><span class="sxs-lookup"><span data-stu-id="07dc4-197">Enable Azure diagnostics in a virtual machine for event log and IIS log collection using PowerShell</span></span>
<span data-ttu-id="07dc4-198">Use the steps in [Configuring Log Analytics to index Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) to use PowerShell to read from Azure diagnostics that are written to table storage.</span><span class="sxs-lookup"><span data-stu-id="07dc4-198">Use the steps in [Configuring Log Analytics to index Azure diagnostics](log-analytics-powershell-workspace-configuration.md#configuring-log-analytics-to-index-azure-diagnostics) to use PowerShell to read from Azure diagnostics that are written to table storage.</span></span>

<span data-ttu-id="07dc4-199">Using Azure PowerShell you can more precisely specify the events that are written to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="07dc4-199">Using Azure PowerShell you can more precisely specify the events that are written to Azure Storage.</span></span>
<span data-ttu-id="07dc4-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="07dc4-200">For more information, see [Enabling Diagnostics in Azure Virtual Machines](../virtual-machines-dotnet-diagnostics.md).</span></span>

<span data-ttu-id="07dc4-201">You can enable and update Azure diagnostics using the following PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="07dc4-201">You can enable and update Azure diagnostics using the following PowerShell script.</span></span>
<span data-ttu-id="07dc4-202">You can also use this script with a custom logging configuration.</span><span class="sxs-lookup"><span data-stu-id="07dc4-202">You can also use this script with a custom logging configuration.</span></span>
<span data-ttu-id="07dc4-203">Modify the script to set the storage account, service name, and virtual machine name.</span><span class="sxs-lookup"><span data-stu-id="07dc4-203">Modify the script to set the storage account, service name, and virtual machine name.</span></span>
<span data-ttu-id="07dc4-204">The script uses cmdlets for classic virtual machines.</span><span class="sxs-lookup"><span data-stu-id="07dc4-204">The script uses cmdlets for classic virtual machines.</span></span>

<span data-ttu-id="07dc4-205">Review the following script sample, copy it, modify it as needed, save the sample as a PowerShell script file, and then run the script.</span><span class="sxs-lookup"><span data-stu-id="07dc4-205">Review the following script sample, copy it, modify it as needed, save the sample as a PowerShell script file, and then run the script.</span></span>

```
    #Connect to Azure
    Add-AzureAccount

    # settings to change:
    $wad_storage_account_name = "myStorageAccount"
    $service_name = "myService"
    $vm_name = "myVM"

    #Construct Azure Diagnostics public config and convert to config format

    # Collect just system error events:
    $wad_xml_config = "<WadCfg><DiagnosticMonitorConfiguration><WindowsEventLog scheduledTransferPeriod=""PT1M""><DataSource name=""System!* "" /></WindowsEventLog></DiagnosticMonitorConfiguration></WadCfg>"

    $wad_b64_config = [System.Convert]::ToBase64String([System.Text.Encoding]::UTF8.GetBytes($wad_xml_config))
    $wad_public_config = [string]::Format("{{""xmlCfg"":""{0}""}}",$wad_b64_config)

    #Construct Azure diagnostics private config

    $wad_storage_account_key = (Get-AzureStorageKey $wad_storage_account_name).Primary
    $wad_private_config = [string]::Format("{{""storageAccountName"":""{0}"",""storageAccountKey"":""{1}""}}",$wad_storage_account_name,$wad_storage_account_key)

    #Enable Diagnostics Extension for Virtual Machine

    $wad_extension_name = "IaaSDiagnostics"
    $wad_publisher = "Microsoft.Azure.Diagnostics"
    $wad_version = (Get-AzureVMAvailableExtension -Publisher $wad_publisher -ExtensionName $wad_extension_name).Version # Gets latest version of the extension

    (Get-AzureVM -ServiceName $service_name -Name $vm_name) | Set-AzureVMExtension -ExtensionName $wad_extension_name -Publisher $wad_publisher -PublicConfiguration $wad_public_config -PrivateConfiguration $wad_private_config -Version $wad_version | Update-AzureVM
```


## <a name="next-steps"></a><span data-ttu-id="07dc4-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="07dc4-206">Next steps</span></span>
* <span data-ttu-id="07dc4-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span><span class="sxs-lookup"><span data-stu-id="07dc4-207">[Collect logs and metrics for Azure services](log-analytics-azure-storage.md) for supported Azure services.</span></span>
* <span data-ttu-id="07dc4-208">[Enable Solutions](log-analytics-add-solutions.md) to provide insight into the data.</span><span class="sxs-lookup"><span data-stu-id="07dc4-208">[Enable Solutions](log-analytics-add-solutions.md) to provide insight into the data.</span></span>
* <span data-ttu-id="07dc4-209">[Use search queries](log-analytics-log-searches.md) to analyze the data.</span><span class="sxs-lookup"><span data-stu-id="07dc4-209">[Use search queries](log-analytics-log-searches.md) to analyze the data.</span></span>
