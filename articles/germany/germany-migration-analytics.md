---
title: Migration of analytics resources from Azure Germany to global Azure
description: This article provides help for migrating analytics resources from Azure Germany to global Azure
author: gitralf
services: germany
cloud: Azure Germany
ms.author: ralfwi
ms.service: germany
ms.date: 8/15/2018
ms.topic: article
ms.custom: bfmigrate
ms.openlocfilehash: 2a64d0f1b9379b58c0e4ec348ad81ba8ec4d6746
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966081"
---
# <a name="migration-of-analytics-resources-from-azure-germany-to-global-azure"></a><span data-ttu-id="11483-103">Migration of analytics resources from Azure Germany to global Azure</span><span class="sxs-lookup"><span data-stu-id="11483-103">Migration of analytics resources from Azure Germany to global Azure</span></span>

<span data-ttu-id="11483-104">This article will provide you some help for the migration of Azure Analytics resources from Azure Germany to global Azure.</span><span class="sxs-lookup"><span data-stu-id="11483-104">This article will provide you some help for the migration of Azure Analytics resources from Azure Germany to global Azure.</span></span>
  
## <a name="event-hubs"></a><span data-ttu-id="11483-105">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="11483-105">Event Hubs</span></span>

<span data-ttu-id="11483-106">YOu can't migrate Event Hubs from Azure Germany to global Azure directly, since Event Hub services don't provide data export or import capabilities.</span><span class="sxs-lookup"><span data-stu-id="11483-106">YOu can't migrate Event Hubs from Azure Germany to global Azure directly, since Event Hub services don't provide data export or import capabilities.</span></span> <span data-ttu-id="11483-107">However, you can export the Event Hub resources [as a template](../azure-resource-manager/resource-manager-export-template-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="11483-107">However, you can export the Event Hub resources [as a template](../azure-resource-manager/resource-manager-export-template-powershell.md).</span></span> <span data-ttu-id="11483-108">Then adopt the exported template for global Azure and recreate the resources.</span><span class="sxs-lookup"><span data-stu-id="11483-108">Then adopt the exported template for global Azure and recreate the resources.</span></span>

> [!NOTE]
> <span data-ttu-id="11483-109">This doesn't copy the data (for example messages), it's only recreating the metadata.</span><span class="sxs-lookup"><span data-stu-id="11483-109">This doesn't copy the data (for example messages), it's only recreating the metadata.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="11483-110">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span><span class="sxs-lookup"><span data-stu-id="11483-110">Change location, Key Vault secrets, certs, and other GUIDs to be consistent with the new region.</span></span>

### <a name="metadata-event-hubs"></a><span data-ttu-id="11483-111">Metadata Event Hubs</span><span class="sxs-lookup"><span data-stu-id="11483-111">Metadata Event Hubs</span></span>

- <span data-ttu-id="11483-112">Namespaces</span><span class="sxs-lookup"><span data-stu-id="11483-112">Namespaces</span></span>
- <span data-ttu-id="11483-113">event hubs</span><span class="sxs-lookup"><span data-stu-id="11483-113">event hubs</span></span>
- <span data-ttu-id="11483-114">consumer groups</span><span class="sxs-lookup"><span data-stu-id="11483-114">consumer groups</span></span>
- <span data-ttu-id="11483-115">Authorization Rules (see also below)</span><span class="sxs-lookup"><span data-stu-id="11483-115">Authorization Rules (see also below)</span></span>

### <a name="next-steps"></a><span data-ttu-id="11483-116">Next Steps</span><span class="sxs-lookup"><span data-stu-id="11483-116">Next Steps</span></span>

- <span data-ttu-id="11483-117">Refresh your knowledge about Event Hubs by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/event-hubs/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="11483-117">Refresh your knowledge about Event Hubs by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/event-hubs/#step-by-step-tutorials).</span></span>
- <span data-ttu-id="11483-118">check the migration steps for [ServiceBus](./germany-migration-integration.md#service-bus)</span><span class="sxs-lookup"><span data-stu-id="11483-118">check the migration steps for [ServiceBus](./germany-migration-integration.md#service-bus)</span></span>
- <span data-ttu-id="11483-119">Make yourself familiar how to [export an Anzure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="11483-119">Make yourself familiar how to [export an Anzure Resource Manager template](../azure-resource-manager/resource-manager-export-template.md) or read the overview about [the Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span></span>


### <a name="references"></a><span data-ttu-id="11483-120">References</span><span class="sxs-lookup"><span data-stu-id="11483-120">References</span></span>

- [<span data-ttu-id="11483-121">Event Hubs overview</span><span class="sxs-lookup"><span data-stu-id="11483-121">Event Hubs overview</span></span>](../event-hubs/event-hubs-about.md)










## <a name="hdinsight"></a><span data-ttu-id="11483-122">HDInsight</span><span class="sxs-lookup"><span data-stu-id="11483-122">HDInsight</span></span>

<span data-ttu-id="11483-123">HDInsight clusters can be migrated from Azure Germany to global Azure by following these steps:</span><span class="sxs-lookup"><span data-stu-id="11483-123">HDInsight clusters can be migrated from Azure Germany to global Azure by following these steps:</span></span>

- <span data-ttu-id="11483-124">Stop HDI cluster</span><span class="sxs-lookup"><span data-stu-id="11483-124">Stop HDI cluster</span></span>
- <span data-ttu-id="11483-125">Migrate the data in the storage to the new region using AzCopy or a similar tool</span><span class="sxs-lookup"><span data-stu-id="11483-125">Migrate the data in the storage to the new region using AzCopy or a similar tool</span></span>
- <span data-ttu-id="11483-126">Create new Compute resources in Azure global and attach the migrated storage resources as the primary attached storage</span><span class="sxs-lookup"><span data-stu-id="11483-126">Create new Compute resources in Azure global and attach the migrated storage resources as the primary attached storage</span></span>

<span data-ttu-id="11483-127">For more specialized, long running clusters (Kafka, Spark streaming, Storm, or HBase) it's recommended to orchestrate transition of workloads to the new region.</span><span class="sxs-lookup"><span data-stu-id="11483-127">For more specialized, long running clusters (Kafka, Spark streaming, Storm, or HBase) it's recommended to orchestrate transition of workloads to the new region.</span></span>

### <a name="next-steps"></a><span data-ttu-id="11483-128">Next Steps</span><span class="sxs-lookup"><span data-stu-id="11483-128">Next Steps</span></span>

- <span data-ttu-id="11483-129">Refresh your knowledge about HDInsight by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/hdinsight/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="11483-129">Refresh your knowledge about HDInsight by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/hdinsight/#step-by-step-tutorials).</span></span>
- <span data-ttu-id="11483-130">[Administer HDInsight using PowerShell](../hdinsight/hdinsight-administer-use-powershell.md) for additional help in [scaling HDInsight clusters](../hdinsight/hdinsight-administer-use-powershell.md#scale-clusters)</span><span class="sxs-lookup"><span data-stu-id="11483-130">[Administer HDInsight using PowerShell](../hdinsight/hdinsight-administer-use-powershell.md) for additional help in [scaling HDInsight clusters](../hdinsight/hdinsight-administer-use-powershell.md#scale-clusters)</span></span>
- <span data-ttu-id="11483-131">Read how to use [AzCopy](../storage/common/storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="11483-131">Read how to use [AzCopy](../storage/common/storage-use-azcopy.md).</span></span>

### <a name="references"></a><span data-ttu-id="11483-132">References</span><span class="sxs-lookup"><span data-stu-id="11483-132">References</span></span>

- [<span data-ttu-id="11483-133">Azure HD Insight Documentation</span><span class="sxs-lookup"><span data-stu-id="11483-133">Azure HD Insight Documentation</span></span>](https://docs.microsoft.com/azure/hdinsight/)







## <a name="stream-analytics"></a><span data-ttu-id="11483-134">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="11483-134">Stream Analytics</span></span>

<span data-ttu-id="11483-135">To migrate Stream Analytics services from Azure Germany to Azure global, manually recreate the entire setup in a global Azure region using either the portal or PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11483-135">To migrate Stream Analytics services from Azure Germany to Azure global, manually recreate the entire setup in a global Azure region using either the portal or PowerShell.</span></span> <span data-ttu-id="11483-136">The ingress and egress sources for any Stream Analytics job can be in any region.</span><span class="sxs-lookup"><span data-stu-id="11483-136">The ingress and egress sources for any Stream Analytics job can be in any region.</span></span>

### <a name="next-steps"></a><span data-ttu-id="11483-137">Next Steps</span><span class="sxs-lookup"><span data-stu-id="11483-137">Next Steps</span></span>

- <span data-ttu-id="11483-138">Refresh your knowledge about Stream Analytics by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/stream-analytics/#step-by-step-tutorials).</span><span class="sxs-lookup"><span data-stu-id="11483-138">Refresh your knowledge about Stream Analytics by following these [Step-by-Step tutorials](https://docs.microsoft.com/azure/stream-analytics/#step-by-step-tutorials).</span></span>

### <a name="references"></a><span data-ttu-id="11483-139">References</span><span class="sxs-lookup"><span data-stu-id="11483-139">References</span></span>
- [<span data-ttu-id="11483-140">Stream Analytics overview</span><span class="sxs-lookup"><span data-stu-id="11483-140">Stream Analytics overview</span></span>](../stream-analytics/stream-analytics-introduction.md)
- [<span data-ttu-id="11483-141">Create a Stream Analytics job using PowerShell</span><span class="sxs-lookup"><span data-stu-id="11483-141">Create a Stream Analytics job using PowerShell</span></span>](../stream-analytics/stream-analytics-quick-create-powershell.md)






## <a name="sql-data-warehouse"></a><span data-ttu-id="11483-142">SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="11483-142">SQL Data Warehouse</span></span>

<span data-ttu-id="11483-143">To migrate Azure SQL databases, you can use (for smaller workloads) the export function to create a BACPAC file.</span><span class="sxs-lookup"><span data-stu-id="11483-143">To migrate Azure SQL databases, you can use (for smaller workloads) the export function to create a BACPAC file.</span></span> <span data-ttu-id="11483-144">BaACPAC file is a compressed (zip'ed) file with metadata and data from the SQL Server database.</span><span class="sxs-lookup"><span data-stu-id="11483-144">BaACPAC file is a compressed (zip'ed) file with metadata and data from the SQL Server database.</span></span> <span data-ttu-id="11483-145">Once created, you can copy it to the target environment (for example with AzCopy) and use the import function to rebuild the database.</span><span class="sxs-lookup"><span data-stu-id="11483-145">Once created, you can copy it to the target environment (for example with AzCopy) and use the import function to rebuild the database.</span></span> <span data-ttu-id="11483-146">Be aware of the following considerations (see more in the links provided below):</span><span class="sxs-lookup"><span data-stu-id="11483-146">Be aware of the following considerations (see more in the links provided below):</span></span>

- <span data-ttu-id="11483-147">For an export to be transactionally consistent, make sure either</span><span class="sxs-lookup"><span data-stu-id="11483-147">For an export to be transactionally consistent, make sure either</span></span>
  - <span data-ttu-id="11483-148">no write activity is occurring during the export, or</span><span class="sxs-lookup"><span data-stu-id="11483-148">no write activity is occurring during the export, or</span></span>
  - <span data-ttu-id="11483-149">you're exporting from a transactionally consistent copy of your Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="11483-149">you're exporting from a transactionally consistent copy of your Azure SQL database.</span></span>
- <span data-ttu-id="11483-150">For export to blob storage, the BACPAC file is limited to 200 GB.</span><span class="sxs-lookup"><span data-stu-id="11483-150">For export to blob storage, the BACPAC file is limited to 200 GB.</span></span> <span data-ttu-id="11483-151">For a larger BACPAC file, export to local storage.</span><span class="sxs-lookup"><span data-stu-id="11483-151">For a larger BACPAC file, export to local storage.</span></span>
- <span data-ttu-id="11483-152">If the export operation from Azure SQL Database takes longer than 20 hours, it may be canceled.</span><span class="sxs-lookup"><span data-stu-id="11483-152">If the export operation from Azure SQL Database takes longer than 20 hours, it may be canceled.</span></span> <span data-ttu-id="11483-153">Look for hints how to increase performance in the links below.</span><span class="sxs-lookup"><span data-stu-id="11483-153">Look for hints how to increase performance in the links below.</span></span>

> [!NOTE]
> <span data-ttu-id="11483-154">The connection string will change since the DNS name of the server will change.</span><span class="sxs-lookup"><span data-stu-id="11483-154">The connection string will change since the DNS name of the server will change.</span></span>

### <a name="next-steps"></a><span data-ttu-id="11483-155">Next Steps</span><span class="sxs-lookup"><span data-stu-id="11483-155">Next Steps</span></span>

- [<span data-ttu-id="11483-156">Export DB to Bacpac file</span><span class="sxs-lookup"><span data-stu-id="11483-156">Export DB to Bacpac file</span></span>](../sql-database/sql-database-export.md)
- [<span data-ttu-id="11483-157">Import Bacpac file to a DB</span><span class="sxs-lookup"><span data-stu-id="11483-157">Import Bacpac file to a DB</span></span>](../sql-database/sql-database-import.md)

### <a name="references"></a><span data-ttu-id="11483-158">References</span><span class="sxs-lookup"><span data-stu-id="11483-158">References</span></span>

- [<span data-ttu-id="11483-159">Azure SQL Database documentation</span><span class="sxs-lookup"><span data-stu-id="11483-159">Azure SQL Database documentation</span></span>](https://docs.microsoft.com/azure/sql-database/)













## <a name="azure-analysis-service"></a><span data-ttu-id="11483-160">Azure Analysis Service</span><span class="sxs-lookup"><span data-stu-id="11483-160">Azure Analysis Service</span></span>

<span data-ttu-id="11483-161">To migrate your models from Azure Germany to global Azure, you can use backup/restore as described [in this document](../analysis-services/analysis-services-backup.md).</span><span class="sxs-lookup"><span data-stu-id="11483-161">To migrate your models from Azure Germany to global Azure, you can use backup/restore as described [in this document](../analysis-services/analysis-services-backup.md).</span></span>

<span data-ttu-id="11483-162">If you only want to migrate the model metadata and not the data, an alternative could be to [redeploy the model from SSDT](../analysis-services/analysis-services-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="11483-162">If you only want to migrate the model metadata and not the data, an alternative could be to [redeploy the model from SSDT](../analysis-services/analysis-services-deploy.md).</span></span>

### <a name="next-steps"></a><span data-ttu-id="11483-163">Next Steps</span><span class="sxs-lookup"><span data-stu-id="11483-163">Next Steps</span></span>
- [<span data-ttu-id="11483-164">Analysis Service backup</span><span class="sxs-lookup"><span data-stu-id="11483-164">Analysis Service backup</span></span>](../analysis-services/analysis-services-backup.md)

### <a name="references"></a><span data-ttu-id="11483-165">References</span><span class="sxs-lookup"><span data-stu-id="11483-165">References</span></span>
- [<span data-ttu-id="11483-166">Analysis Services overview</span><span class="sxs-lookup"><span data-stu-id="11483-166">Analysis Services overview</span></span>](../analysis-services/analysis-services-overview.md)
