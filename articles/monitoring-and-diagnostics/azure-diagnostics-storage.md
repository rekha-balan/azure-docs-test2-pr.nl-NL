---
title: Store and View Diagnostic Data in Azure Storage
description: Get Azure diagnostics data into Azure Storage and view it
services: azure-monitor
author: thraka
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 08/01/2016
ms.author: adegeo
ms.component: diagnostic-extension
ms.openlocfilehash: 6590e6991f07b7315c09a995152879c991fafcef
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871170"
---
# <a name="store-and-view-diagnostic-data-in-azure-storage"></a><span data-ttu-id="5be7b-103">Store and view diagnostic data in Azure Storage</span><span class="sxs-lookup"><span data-stu-id="5be7b-103">Store and view diagnostic data in Azure Storage</span></span>
<span data-ttu-id="5be7b-104">Diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span><span class="sxs-lookup"><span data-stu-id="5be7b-104">Diagnostic data is not permanently stored unless you transfer it to the Microsoft Azure storage emulator or to Azure storage.</span></span> <span data-ttu-id="5be7b-105">Once in storage, it can be viewed with one of several available tools.</span><span class="sxs-lookup"><span data-stu-id="5be7b-105">Once in storage, it can be viewed with one of several available tools.</span></span>

## <a name="specify-a-storage-account"></a><span data-ttu-id="5be7b-106">Specify a storage account</span><span class="sxs-lookup"><span data-stu-id="5be7b-106">Specify a storage account</span></span>
<span data-ttu-id="5be7b-107">You specify the storage account that you want to use in the ServiceConfiguration.cscfg file.</span><span class="sxs-lookup"><span data-stu-id="5be7b-107">You specify the storage account that you want to use in the ServiceConfiguration.cscfg file.</span></span> <span data-ttu-id="5be7b-108">The account information is defined as a connection string in a configuration setting.</span><span class="sxs-lookup"><span data-stu-id="5be7b-108">The account information is defined as a connection string in a configuration setting.</span></span> <span data-ttu-id="5be7b-109">The following example shows the default connection string created for a new Cloud Service project in  Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="5be7b-109">The following example shows the default connection string created for a new Cloud Service project in  Visual Studio:</span></span>

```
    <ConfigurationSettings>
       <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true" />
    </ConfigurationSettings>
```

<span data-ttu-id="5be7b-110">You can change this connection string to provide account information for an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="5be7b-110">You can change this connection string to provide account information for an Azure storage account.</span></span>

<span data-ttu-id="5be7b-111">Depending on the type of diagnostic data that is being collected, Azure Diagnostics uses either the Blob service or the Table service.</span><span class="sxs-lookup"><span data-stu-id="5be7b-111">Depending on the type of diagnostic data that is being collected, Azure Diagnostics uses either the Blob service or the Table service.</span></span> <span data-ttu-id="5be7b-112">The following table shows the data sources that are persisted and their format.</span><span class="sxs-lookup"><span data-stu-id="5be7b-112">The following table shows the data sources that are persisted and their format.</span></span>

| <span data-ttu-id="5be7b-113">Data source</span><span class="sxs-lookup"><span data-stu-id="5be7b-113">Data source</span></span> | <span data-ttu-id="5be7b-114">Storage format</span><span class="sxs-lookup"><span data-stu-id="5be7b-114">Storage format</span></span> |
| --- | --- |
| <span data-ttu-id="5be7b-115">Azure logs</span><span class="sxs-lookup"><span data-stu-id="5be7b-115">Azure logs</span></span> |<span data-ttu-id="5be7b-116">Table</span><span class="sxs-lookup"><span data-stu-id="5be7b-116">Table</span></span> |
| <span data-ttu-id="5be7b-117">IIS 7.0 logs</span><span class="sxs-lookup"><span data-stu-id="5be7b-117">IIS 7.0 logs</span></span> |<span data-ttu-id="5be7b-118">Blob</span><span class="sxs-lookup"><span data-stu-id="5be7b-118">Blob</span></span> |
| <span data-ttu-id="5be7b-119">Azure Diagnostics infrastructure logs</span><span class="sxs-lookup"><span data-stu-id="5be7b-119">Azure Diagnostics infrastructure logs</span></span> |<span data-ttu-id="5be7b-120">Table</span><span class="sxs-lookup"><span data-stu-id="5be7b-120">Table</span></span> |
| <span data-ttu-id="5be7b-121">Failed Request Trace logs</span><span class="sxs-lookup"><span data-stu-id="5be7b-121">Failed Request Trace logs</span></span> |<span data-ttu-id="5be7b-122">Blob</span><span class="sxs-lookup"><span data-stu-id="5be7b-122">Blob</span></span> |
| <span data-ttu-id="5be7b-123">Windows Event logs</span><span class="sxs-lookup"><span data-stu-id="5be7b-123">Windows Event logs</span></span> |<span data-ttu-id="5be7b-124">Table</span><span class="sxs-lookup"><span data-stu-id="5be7b-124">Table</span></span> |
| <span data-ttu-id="5be7b-125">Performance counters</span><span class="sxs-lookup"><span data-stu-id="5be7b-125">Performance counters</span></span> |<span data-ttu-id="5be7b-126">Table</span><span class="sxs-lookup"><span data-stu-id="5be7b-126">Table</span></span> |
| <span data-ttu-id="5be7b-127">Crash dumps</span><span class="sxs-lookup"><span data-stu-id="5be7b-127">Crash dumps</span></span> |<span data-ttu-id="5be7b-128">Blob</span><span class="sxs-lookup"><span data-stu-id="5be7b-128">Blob</span></span> |
| <span data-ttu-id="5be7b-129">Custom error logs</span><span class="sxs-lookup"><span data-stu-id="5be7b-129">Custom error logs</span></span> |<span data-ttu-id="5be7b-130">Blob</span><span class="sxs-lookup"><span data-stu-id="5be7b-130">Blob</span></span> |

## <a name="transfer-diagnostic-data"></a><span data-ttu-id="5be7b-131">Transfer diagnostic data</span><span class="sxs-lookup"><span data-stu-id="5be7b-131">Transfer diagnostic data</span></span>
<span data-ttu-id="5be7b-132">For SDK 2.5 and later, the request to transfer diagnostic data can occur through the configuration file.</span><span class="sxs-lookup"><span data-stu-id="5be7b-132">For SDK 2.5 and later, the request to transfer diagnostic data can occur through the configuration file.</span></span> <span data-ttu-id="5be7b-133">You can transfer diagnostic data at scheduled intervals as specified in the configuration.</span><span class="sxs-lookup"><span data-stu-id="5be7b-133">You can transfer diagnostic data at scheduled intervals as specified in the configuration.</span></span>

<span data-ttu-id="5be7b-134">For SDK 2.4 and previous you can request to transfer the diagnostic data through the configuration file as well as programmatically.</span><span class="sxs-lookup"><span data-stu-id="5be7b-134">For SDK 2.4 and previous you can request to transfer the diagnostic data through the configuration file as well as programmatically.</span></span> <span data-ttu-id="5be7b-135">The programmatic approach also allows you to do on-demand transfers.</span><span class="sxs-lookup"><span data-stu-id="5be7b-135">The programmatic approach also allows you to do on-demand transfers.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5be7b-136">When you transfer diagnostic data to an Azure storage account, you incur costs for the storage resources that your diagnostic data uses.</span><span class="sxs-lookup"><span data-stu-id="5be7b-136">When you transfer diagnostic data to an Azure storage account, you incur costs for the storage resources that your diagnostic data uses.</span></span>
> 
> 

## <a name="store-diagnostic-data"></a><span data-ttu-id="5be7b-137">Store diagnostic data</span><span class="sxs-lookup"><span data-stu-id="5be7b-137">Store diagnostic data</span></span>
<span data-ttu-id="5be7b-138">Log data is stored in either Blob or Table storage with the following names:</span><span class="sxs-lookup"><span data-stu-id="5be7b-138">Log data is stored in either Blob or Table storage with the following names:</span></span>

<span data-ttu-id="5be7b-139">**Tables**</span><span class="sxs-lookup"><span data-stu-id="5be7b-139">**Tables**</span></span>

* <span data-ttu-id="5be7b-140">**WadLogsTable** - Logs written in code using the trace listener.</span><span class="sxs-lookup"><span data-stu-id="5be7b-140">**WadLogsTable** - Logs written in code using the trace listener.</span></span>
* <span data-ttu-id="5be7b-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span><span class="sxs-lookup"><span data-stu-id="5be7b-141">**WADDiagnosticInfrastructureLogsTable** - Diagnostic monitor and configuration changes.</span></span>
* <span data-ttu-id="5be7b-142">**WADDirectoriesTable** – Directories that the diagnostic monitor is monitoring.</span><span class="sxs-lookup"><span data-stu-id="5be7b-142">**WADDirectoriesTable** – Directories that the diagnostic monitor is monitoring.</span></span>  <span data-ttu-id="5be7b-143">This includes IIS logs, IIS failed request logs, and custom directories.</span><span class="sxs-lookup"><span data-stu-id="5be7b-143">This includes IIS logs, IIS failed request logs, and custom directories.</span></span>  <span data-ttu-id="5be7b-144">The location of the blob log file is specified in the Container field and the name of the blob is in the RelativePath field.</span><span class="sxs-lookup"><span data-stu-id="5be7b-144">The location of the blob log file is specified in the Container field and the name of the blob is in the RelativePath field.</span></span>  <span data-ttu-id="5be7b-145">The AbsolutePath field indicates the location and name of the file as it existed on the Azure virtual machine.</span><span class="sxs-lookup"><span data-stu-id="5be7b-145">The AbsolutePath field indicates the location and name of the file as it existed on the Azure virtual machine.</span></span>
* <span data-ttu-id="5be7b-146">**WADPerformanceCountersTable** – Performance counters.</span><span class="sxs-lookup"><span data-stu-id="5be7b-146">**WADPerformanceCountersTable** – Performance counters.</span></span>
* <span data-ttu-id="5be7b-147">**WADWindowsEventLogsTable** – Windows Event logs.</span><span class="sxs-lookup"><span data-stu-id="5be7b-147">**WADWindowsEventLogsTable** – Windows Event logs.</span></span>

<span data-ttu-id="5be7b-148">**Blobs**</span><span class="sxs-lookup"><span data-stu-id="5be7b-148">**Blobs**</span></span>

* <span data-ttu-id="5be7b-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains the XML configuration files that controls the Azure diagnostics .</span><span class="sxs-lookup"><span data-stu-id="5be7b-149">**wad-control-container** – (Only for SDK 2.4 and previous) Contains the XML configuration files that controls the Azure diagnostics .</span></span>
* <span data-ttu-id="5be7b-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span><span class="sxs-lookup"><span data-stu-id="5be7b-150">**wad-iis-failedreqlogfiles** – Contains information from IIS Failed Request logs.</span></span>
* <span data-ttu-id="5be7b-151">**wad-iis-logfiles** – Contains information about IIS logs.</span><span class="sxs-lookup"><span data-stu-id="5be7b-151">**wad-iis-logfiles** – Contains information about IIS logs.</span></span>
* <span data-ttu-id="5be7b-152">**"custom"** – A custom container based on configuring directories that are monitored by the diagnostic monitor.</span><span class="sxs-lookup"><span data-stu-id="5be7b-152">**"custom"** – A custom container based on configuring directories that are monitored by the diagnostic monitor.</span></span>  <span data-ttu-id="5be7b-153">The name of this blob container will be specified in WADDirectoriesTable.</span><span class="sxs-lookup"><span data-stu-id="5be7b-153">The name of this blob container will be specified in WADDirectoriesTable.</span></span>

## <a name="tools-to-view-diagnostic-data"></a><span data-ttu-id="5be7b-154">Tools to view diagnostic data</span><span class="sxs-lookup"><span data-stu-id="5be7b-154">Tools to view diagnostic data</span></span>
<span data-ttu-id="5be7b-155">Several tools are available to view the data after it is transferred to storage.</span><span class="sxs-lookup"><span data-stu-id="5be7b-155">Several tools are available to view the data after it is transferred to storage.</span></span> <span data-ttu-id="5be7b-156">For example:</span><span class="sxs-lookup"><span data-stu-id="5be7b-156">For example:</span></span>

* <span data-ttu-id="5be7b-157">Server Explorer in Visual Studio - If you have installed the Azure Tools for Microsoft Visual Studio, you can use the Azure Storage node in Server Explorer to view read-only blob and table data from your Azure storage accounts.</span><span class="sxs-lookup"><span data-stu-id="5be7b-157">Server Explorer in Visual Studio - If you have installed the Azure Tools for Microsoft Visual Studio, you can use the Azure Storage node in Server Explorer to view read-only blob and table data from your Azure storage accounts.</span></span> <span data-ttu-id="5be7b-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span><span class="sxs-lookup"><span data-stu-id="5be7b-158">You can display data from your local storage emulator account and also from storage accounts you have created for Azure.</span></span> <span data-ttu-id="5be7b-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span><span class="sxs-lookup"><span data-stu-id="5be7b-159">For more information, see [Browsing and Managing Storage Resources with Server Explorer](../vs-azure-tools-storage-resources-server-explorer-browse-manage.md).</span></span>
* <span data-ttu-id="5be7b-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, OSX, and Linux.</span><span class="sxs-lookup"><span data-stu-id="5be7b-160">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a standalone app that enables you to easily work with Azure Storage data on Windows, OSX, and Linux.</span></span>
* <span data-ttu-id="5be7b-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you to view, download and manage the diagnostics data collected by the applications running on Azure.</span><span class="sxs-lookup"><span data-stu-id="5be7b-161">[Azure Management Studio](http://www.cerebrata.com/products/azure-management-studio/introduction) includes Azure Diagnostics Manager which allows you to view, download and manage the diagnostics data collected by the applications running on Azure.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5be7b-162">Next Steps</span><span class="sxs-lookup"><span data-stu-id="5be7b-162">Next Steps</span></span>
[<span data-ttu-id="5be7b-163">Trace the flow in a Cloud Services application with Azure Diagnostics</span><span class="sxs-lookup"><span data-stu-id="5be7b-163">Trace the flow in a Cloud Services application with Azure Diagnostics</span></span>](../cloud-services/cloud-services-dotnet-diagnostics-trace-flow.md)

