---
title: DocumentDB global database replication | Microsoft Docs
description: Learn how to manage the global replication of your DocumentDB account via the Azure portal.
services: documentdb
keywords: global database, replication
documentationcenter: ''
author: mimig1
manager: jhubbard
editor: cgronlun
ms.assetid: 8b815047-2868-4b10-af1d-40a1af419a70
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/14/2017
ms.author: mimig
ms.openlocfilehash: 1ebb0374339f586ad4c97e408a4cd8c7b4f876bc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662054"
---
# <a name="how-to-perform-global-database-replication-using-the-azure-portal"></a><span data-ttu-id="ff75f-104">How to perform global database replication using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ff75f-104">How to perform global database replication using the Azure portal</span></span>

<span data-ttu-id="ff75f-105">Learn how to use the Azure portal to replicate data in multiple regions for global availability of data in Azure DocumentDB and API for MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ff75f-105">Learn how to use the Azure portal to replicate data in multiple regions for global availability of data in Azure DocumentDB and API for MongoDB.</span></span>

<span data-ttu-id="ff75f-106">For information about how global database replication works in DocumentDB, see [Distribute data globally with DocumentDB](documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="ff75f-106">For information about how global database replication works in DocumentDB, see [Distribute data globally with DocumentDB](documentdb-distribute-data-globally.md).</span></span> <span data-ttu-id="ff75f-107">For information about performing global database replication programmatically, see [Developing with multi-region DocumentDB accounts](documentdb-developing-with-multiple-regions.md).</span><span class="sxs-lookup"><span data-stu-id="ff75f-107">For information about performing global database replication programmatically, see [Developing with multi-region DocumentDB accounts](documentdb-developing-with-multiple-regions.md).</span></span>

## <a id="addregion"></a><span data-ttu-id="ff75f-108">Add global database regions</span><span class="sxs-lookup"><span data-stu-id="ff75f-108">Add global database regions</span></span>
<span data-ttu-id="ff75f-109">DocumentDB is available in most [Azure regions][azureregions].</span><span class="sxs-lookup"><span data-stu-id="ff75f-109">DocumentDB is available in most [Azure regions][azureregions].</span></span> <span data-ttu-id="ff75f-110">After selecting the default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span><span class="sxs-lookup"><span data-stu-id="ff75f-110">After selecting the default consistency level for your database account, you can associate one or more regions (depending on your choice of default consistency level and global distribution needs).</span></span>

1. <span data-ttu-id="ff75f-111">In the [Azure portal](https://portal.azure.com/), in the left bar, click **NoSQL (DocumentDB)**.</span><span class="sxs-lookup"><span data-stu-id="ff75f-111">In the [Azure portal](https://portal.azure.com/), in the left bar, click **NoSQL (DocumentDB)**.</span></span>
2. <span data-ttu-id="ff75f-112">In the **NoSQL (DocumentDB)** blade, select the database account to modify.</span><span class="sxs-lookup"><span data-stu-id="ff75f-112">In the **NoSQL (DocumentDB)** blade, select the database account to modify.</span></span>
3. <span data-ttu-id="ff75f-113">In the account blade, click **Replicate data globally** from the menu.</span><span class="sxs-lookup"><span data-stu-id="ff75f-113">In the account blade, click **Replicate data globally** from the menu.</span></span>
4. <span data-ttu-id="ff75f-114">In the **Replicate data globally** blade, select the regions to add or remove, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="ff75f-114">In the **Replicate data globally** blade, select the regions to add or remove, and then click **Save**.</span></span> <span data-ttu-id="ff75f-115">There is a cost to adding regions, see the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or the [Distribute data globally with DocumentDB](documentdb-distribute-data-globally.md) article for more information.</span><span class="sxs-lookup"><span data-stu-id="ff75f-115">There is a cost to adding regions, see the [pricing page](https://azure.microsoft.com/pricing/details/documentdb/) or the [Distribute data globally with DocumentDB](documentdb-distribute-data-globally.md) article for more information.</span></span>
   
    ![Click the regions in the map to add or remove them][1]
    
<span data-ttu-id="ff75f-117">Once you add a second region, the **Manual Failover** option is enabled on the **Replicate data locally** blade in the portal.</span><span class="sxs-lookup"><span data-stu-id="ff75f-117">Once you add a second region, the **Manual Failover** option is enabled on the **Replicate data locally** blade in the portal.</span></span> <span data-ttu-id="ff75f-118">You can use this option to test the failover process.</span><span class="sxs-lookup"><span data-stu-id="ff75f-118">You can use this option to test the failover process.</span></span> <span data-ttu-id="ff75f-119">Once you add a third region, the **Failover Priorities** option is enabled on the same blade so that you can change the failover order for reads.</span><span class="sxs-lookup"><span data-stu-id="ff75f-119">Once you add a third region, the **Failover Priorities** option is enabled on the same blade so that you can change the failover order for reads.</span></span>  

### <a name="selecting-global-database-regions"></a><span data-ttu-id="ff75f-120">Selecting global database regions</span><span class="sxs-lookup"><span data-stu-id="ff75f-120">Selecting global database regions</span></span>
<span data-ttu-id="ff75f-121">When configuring two or more regions, it is recommended that regions are selected based on the region pairs described in the [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span><span class="sxs-lookup"><span data-stu-id="ff75f-121">When configuring two or more regions, it is recommended that regions are selected based on the region pairs described in the [Business continuity and disaster recovery (BCDR): Azure Paired Regions][bcdr] article.</span></span>

<span data-ttu-id="ff75f-122">Specifically, when configuring to multiple regions, make sure to select the same number of regions (+/-1 for odd/even) from each of the paired region columns.</span><span class="sxs-lookup"><span data-stu-id="ff75f-122">Specifically, when configuring to multiple regions, make sure to select the same number of regions (+/-1 for odd/even) from each of the paired region columns.</span></span> <span data-ttu-id="ff75f-123">For example, if you want to deploy to four US regions, you select two US regions from the left column and two from the right.</span><span class="sxs-lookup"><span data-stu-id="ff75f-123">For example, if you want to deploy to four US regions, you select two US regions from the left column and two from the right.</span></span> <span data-ttu-id="ff75f-124">So, the following would be an appropriate set: West US, East US, North Central US, and South Central US.</span><span class="sxs-lookup"><span data-stu-id="ff75f-124">So, the following would be an appropriate set: West US, East US, North Central US, and South Central US.</span></span>

<span data-ttu-id="ff75f-125">This guidance is important to follow when only two regions are configured for disaster recovery scenarios.</span><span class="sxs-lookup"><span data-stu-id="ff75f-125">This guidance is important to follow when only two regions are configured for disaster recovery scenarios.</span></span> <span data-ttu-id="ff75f-126">For more than two regions, following this guidance is good practice, but not critical as long as some of the selected regions adhere to this pairing.</span><span class="sxs-lookup"><span data-stu-id="ff75f-126">For more than two regions, following this guidance is good practice, but not critical as long as some of the selected regions adhere to this pairing.</span></span>

<!---
## <a id="selectwriteregion"></a>Select the write region

While all regions associated with your DocumentDB database account can serve reads (both, single item as well as multi-item paginated reads) and queries, only one region can actively receive the write (insert, upsert, replace, delete) requests. To set the active write region, do the following  


1. In the **NoSQL (DocumentDB)** blade, select the database account to modify.
2. In the account blade, if the **All Settings** blade is not already opened, click **All Settings**.
3. In the **All Settings** blade, click **Write Region Priority**.
    ![Change the write region under DocumentDB Account > Settings > Add/Remove Regions][2]
4. Click and drag regions to order the list of regions. The first region in the list of regions is the active write region.
    ![Change the write region by reordering the region list under DocumentDB Account > Settings > Change Write Regions][3]
-->

### <a name="verifying-your-regional-setup-in-api-for-mongodb"></a><span data-ttu-id="ff75f-127">Verifying your regional setup in API for MongoDB</span><span class="sxs-lookup"><span data-stu-id="ff75f-127">Verifying your regional setup in API for MongoDB</span></span>
<span data-ttu-id="ff75f-128">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span><span class="sxs-lookup"><span data-stu-id="ff75f-128">The simplest way of double checking your global configuration within API for MongoDB is to run the *isMaster()* command from the Mongo Shell.</span></span>

<span data-ttu-id="ff75f-129">From your Mongo Shell:</span><span class="sxs-lookup"><span data-stu-id="ff75f-129">From your Mongo Shell:</span></span>

   ```
      db.isMaster()
   ```
   
<span data-ttu-id="ff75f-130">Example results:</span><span class="sxs-lookup"><span data-stu-id="ff75f-130">Example results:</span></span>

   ```JSON
      {
         "_t": "IsMasterResponse",
         "ok": 1,
         "ismaster": true,
         "maxMessageSizeBytes": 4194304,
         "maxWriteBatchSize": 1000,
         "minWireVersion": 0,
         "maxWireVersion": 2,
         "tags": {
            "region": "South India"
         },
         "hosts": [
            "vishi-api-for-mongodb-southcentralus.documents.azure.com:10250",
            "vishi-api-for-mongodb-westeurope.documents.azure.com:10250",
            "vishi-api-for-mongodb-southindia.documents.azure.com:10250"
         ],
         "setName": "globaldb",
         "setVersion": 1,
         "primary": "vishi-api-for-mongodb-southindia.documents.azure.com:10250",
         "me": "vishi-api-for-mongodb-southindia.documents.azure.com:10250"
      }
   ```

## <a id="next"></a><span data-ttu-id="ff75f-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff75f-131">Next steps</span></span>
<span data-ttu-id="ff75f-132">Learn how to manage the consistency of your globally replicated account by reading [Consistency levels in DocumentDB](documentdb-consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="ff75f-132">Learn how to manage the consistency of your globally replicated account by reading [Consistency levels in DocumentDB](documentdb-consistency-levels.md).</span></span>

<span data-ttu-id="ff75f-133">For information about how global database replication works in DocumentDB, see [Distribute data globally with DocumentDB](documentdb-distribute-data-globally.md).</span><span class="sxs-lookup"><span data-stu-id="ff75f-133">For information about how global database replication works in DocumentDB, see [Distribute data globally with DocumentDB](documentdb-distribute-data-globally.md).</span></span> <span data-ttu-id="ff75f-134">For information about programmatically replicating data in multiple regions, see [Developing with multi-region DocumentDB accounts](documentdb-developing-with-multiple-regions.md).</span><span class="sxs-lookup"><span data-stu-id="ff75f-134">For information about programmatically replicating data in multiple regions, see [Developing with multi-region DocumentDB accounts](documentdb-developing-with-multiple-regions.md).</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-portal-global-replication/documentdb-add-region.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-portal-global-replication/documentdb_change_write_region-1.png
[3]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-portal-global-replication/documentdb_change_write_region-2.png

<!--Reference style links - using these makes the source content way more readable than using inline links-->
[bcdr]: https://azure.microsoft.com/documentation/articles/best-practices-availability-paired-regions/
[consistency]: https://azure.microsoft.com/documentation/articles/documentdb-consistency-levels/
[azureregions]: https://azure.microsoft.com/en-us/regions/#services
[offers]: https://azure.microsoft.com/en-us/pricing/details/documentdb/



