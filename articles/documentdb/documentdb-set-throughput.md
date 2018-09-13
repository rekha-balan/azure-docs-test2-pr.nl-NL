---
title: Provision throughput for Azure DocumentDB | Microsoft Docs
description: Learn  how to set provisioned throughput for your DocumentDB collection.
services: documentdb
author: mimig1
manager: jhubbard
editor: ''
documentationcenter: ''
ms.assetid: f98def7f-f012-4592-be03-f6fa185e1b1e
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/15/2017
ms.author: mimig
ms.openlocfilehash: 837fc1adda8356e43afada3b866bd639fa98b1b7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553488"
---
# <a name="set-throughput-for-azure-documentdb-collections"></a><span data-ttu-id="0d432-103">Set throughput for Azure DocumentDB collections</span><span class="sxs-lookup"><span data-stu-id="0d432-103">Set throughput for Azure DocumentDB collections</span></span>

<span data-ttu-id="0d432-104">You can set throughput for your DocumentDB collections in the Azure portal or by using the client SDKs.</span><span class="sxs-lookup"><span data-stu-id="0d432-104">You can set throughput for your DocumentDB collections in the Azure portal or by using the client SDKs.</span></span> 

<span data-ttu-id="0d432-105">The following table lists the throughput available for collections:</span><span class="sxs-lookup"><span data-stu-id="0d432-105">The following table lists the throughput available for collections:</span></span>

<table border="0" cellspacing="0" cellpadding="0">
    <tbody>
        <tr>
            <td valign="top"><p></p></td>
            <td valign="top"><p><span data-ttu-id="0d432-106"><strong>Single Partition Collection</strong></span><span class="sxs-lookup"><span data-stu-id="0d432-106"><strong>Single Partition Collection</strong></span></span></p></td>
            <td valign="top"><p><span data-ttu-id="0d432-107"><strong>Partitioned Collection</strong></span><span class="sxs-lookup"><span data-stu-id="0d432-107"><strong>Partitioned Collection</strong></span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="0d432-108">Minimum Throughput</span><span class="sxs-lookup"><span data-stu-id="0d432-108">Minimum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="0d432-109">400 request units per second</span><span class="sxs-lookup"><span data-stu-id="0d432-109">400 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="0d432-110">2,500 request units per second</span><span class="sxs-lookup"><span data-stu-id="0d432-110">2,500 request units per second</span></span></p></td>
        </tr>
        <tr>
            <td valign="top"><p><span data-ttu-id="0d432-111">Maximum Throughput</span><span class="sxs-lookup"><span data-stu-id="0d432-111">Maximum Throughput</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="0d432-112">10,000 request units per second</span><span class="sxs-lookup"><span data-stu-id="0d432-112">10,000 request units per second</span></span></p></td>
            <td valign="top"><p><span data-ttu-id="0d432-113">Unlimited</span><span class="sxs-lookup"><span data-stu-id="0d432-113">Unlimited</span></span></p></td>
        </tr>
    </tbody>
</table>

> [!NOTE] 
> <span data-ttu-id="0d432-114">To set partitioned collections to a throughput value betweeen 2,500 RU/s and 10,000 RU/s, you must temporarily use the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0d432-114">To set partitioned collections to a throughput value betweeen 2,500 RU/s and 10,000 RU/s, you must temporarily use the Azure portal.</span></span> <span data-ttu-id="0d432-115">This functionality is not yet available in the SDKs.</span><span class="sxs-lookup"><span data-stu-id="0d432-115">This functionality is not yet available in the SDKs.</span></span>

## <a name="to-set-the-throughput-by-using-the-azure-portal"></a><span data-ttu-id="0d432-116">To set the throughput by using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="0d432-116">To set the throughput by using the Azure portal</span></span>

1. <span data-ttu-id="0d432-117">In a new window, open the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0d432-117">In a new window, open the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0d432-118">On the left bar, click **NoSQL (DocumentDB)**, or click **More Services** at the bottom, then scroll to **Databases**, and then click **NoSQL (DocumentDB)**.</span><span class="sxs-lookup"><span data-stu-id="0d432-118">On the left bar, click **NoSQL (DocumentDB)**, or click **More Services** at the bottom, then scroll to **Databases**, and then click **NoSQL (DocumentDB)**.</span></span>
3. <span data-ttu-id="0d432-119">Select your DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="0d432-119">Select your DocumentDB account.</span></span>
4. <span data-ttu-id="0d432-120">In the new window, under **Collections**, click **Scale** as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="0d432-120">In the new window, under **Collections**, click **Scale** as shown in the following screenshot.</span></span>
5. <span data-ttu-id="0d432-121">In the new window, select your collection from the drop-down, change the **Throughput** value, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="0d432-121">In the new window, select your collection from the drop-down, change the **Throughput** value, and then click **Save**.</span></span>

    ![Screenshot showing how to change throughput for a collection in the Azure portal by navigating to your account and clicking Scale](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-set-throughput/azure-documentdb-change-throughput-value.png)

<a id="set-throughput-sdk"></a>

## <a name="to-set-the-throughput-by-using-the-net-sdk"></a><span data-ttu-id="0d432-123">To set the throughput by using the .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0d432-123">To set the throughput by using the .NET SDK</span></span>

```C#
//Fetch the resource to be updated
Offer offer = client.CreateOfferQuery()
    .Where(r => r.ResourceLink == collection.SelfLink)    
    .AsEnumerable()
    .SingleOrDefault();

// Set the throughput to the new value, for example 12,000 request units per second
offer = new OfferV2(offer, 12000);

//Now persist these changes to the database by replacing the original resource
await client.ReplaceOfferAsync(offer);
```

## <a name="throughput-faq"></a><span data-ttu-id="0d432-124">Throughput FAQ</span><span class="sxs-lookup"><span data-stu-id="0d432-124">Throughput FAQ</span></span>

<span data-ttu-id="0d432-125">**Can I set my throughput to less than 400 RU/s?**</span><span class="sxs-lookup"><span data-stu-id="0d432-125">**Can I set my throughput to less than 400 RU/s?**</span></span>

<span data-ttu-id="0d432-126">400 RU/s is the minimum throughput available on DocumentDB single partition collections (2500 RU/s is the minimum for partitioned collections).</span><span class="sxs-lookup"><span data-stu-id="0d432-126">400 RU/s is the minimum throughput available on DocumentDB single partition collections (2500 RU/s is the minimum for partitioned collections).</span></span> <span data-ttu-id="0d432-127">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span><span class="sxs-lookup"><span data-stu-id="0d432-127">Request units are set in 100 RU/s intervals, but throughput cannot be set to 100 RU/s or any value smaller than 400 RU/s.</span></span> <span data-ttu-id="0d432-128">If you're looking for a cost effective method to develop and test DocumentDB, you can use the free [DocumentDB Emulator](documentdb-nosql-local-emulator.md), which you can deploy locally at no cost.</span><span class="sxs-lookup"><span data-stu-id="0d432-128">If you're looking for a cost effective method to develop and test DocumentDB, you can use the free [DocumentDB Emulator](documentdb-nosql-local-emulator.md), which you can deploy locally at no cost.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0d432-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="0d432-129">Next steps</span></span>

<span data-ttu-id="0d432-130">To learn more about provisioning and going planet-scale with DocumentDB, see [Partitioning and scaling with DocumentDB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="0d432-130">To learn more about provisioning and going planet-scale with DocumentDB, see [Partitioning and scaling with DocumentDB](documentdb-partition-data.md).</span></span>

