---
title: Azure Media Services v3 frequently asked questions| Microsoft Docs
description: This article gives answers to Azure Media Services v3 frequently asked questions.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 05/29/2018
ms.author: juliako
ms.openlocfilehash: 098a34aba8e5ce23f64d4bb07e3b9622aa2adb8e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865254"
---
# <a name="azure-media-services-v3-preview-frequently-asked-questions"></a><span data-ttu-id="633ee-103">Azure Media Services v3 (preview) frequently asked questions</span><span class="sxs-lookup"><span data-stu-id="633ee-103">Azure Media Services v3 (preview) frequently asked questions</span></span>

<span data-ttu-id="633ee-104">This article gives answers to Azure Media Services (AMS) v3 frequently asked questions.</span><span class="sxs-lookup"><span data-stu-id="633ee-104">This article gives answers to Azure Media Services (AMS) v3 frequently asked questions.</span></span>

## <a name="can-i-use-the-azure-portal-to-manage-v3-resources"></a><span data-ttu-id="633ee-105">Can I use the Azure portal to manage v3 resources?</span><span class="sxs-lookup"><span data-stu-id="633ee-105">Can I use the Azure portal to manage v3 resources?</span></span>

<span data-ttu-id="633ee-106">Not yet.</span><span class="sxs-lookup"><span data-stu-id="633ee-106">Not yet.</span></span> <span data-ttu-id="633ee-107">You can use one of the supported SDKs.</span><span class="sxs-lookup"><span data-stu-id="633ee-107">You can use one of the supported SDKs.</span></span> <span data-ttu-id="633ee-108">See tutorials and samples in this doc set.</span><span class="sxs-lookup"><span data-stu-id="633ee-108">See tutorials and samples in this doc set.</span></span>

## <a name="is-there-an-api-for-configuring-media-reserved-units"></a><span data-ttu-id="633ee-109">Is there an API for configuring Media Reserved Units?</span><span class="sxs-lookup"><span data-stu-id="633ee-109">Is there an API for configuring Media Reserved Units?</span></span>

<span data-ttu-id="633ee-110">The Media Services team is eliminating RUs in v3.</span><span class="sxs-lookup"><span data-stu-id="633ee-110">The Media Services team is eliminating RUs in v3.</span></span> <span data-ttu-id="633ee-111">However the necessary service work is not complete.</span><span class="sxs-lookup"><span data-stu-id="633ee-111">However the necessary service work is not complete.</span></span> <span data-ttu-id="633ee-112">Until then, customers have to use the Azure portal or AMS v2 APIs to set RUs (as described in [Scaling media processing](../previous/media-services-scale-media-processing-overview.md).</span><span class="sxs-lookup"><span data-stu-id="633ee-112">Until then, customers have to use the Azure portal or AMS v2 APIs to set RUs (as described in [Scaling media processing](../previous/media-services-scale-media-processing-overview.md).</span></span> 

<span data-ttu-id="633ee-113">When using **VideoAnalyzerPreset** and/or **AudioAnalyzerPreset**, set your Media Services account to 10 S3 Media Reserved Units.</span><span class="sxs-lookup"><span data-stu-id="633ee-113">When using **VideoAnalyzerPreset** and/or **AudioAnalyzerPreset**, set your Media Services account to 10 S3 Media Reserved Units.</span></span>

## <a name="does-v3-asset-have-no-assetfile-concept"></a><span data-ttu-id="633ee-114">Does V3 Asset have no AssetFile concept?</span><span class="sxs-lookup"><span data-stu-id="633ee-114">Does V3 Asset have no AssetFile concept?</span></span>

<span data-ttu-id="633ee-115">The AssetFiles were removed from the AMS API in order to separate Media Services from Storage SDK dependency.</span><span class="sxs-lookup"><span data-stu-id="633ee-115">The AssetFiles were removed from the AMS API in order to separate Media Services from Storage SDK dependency.</span></span> <span data-ttu-id="633ee-116">Now Storage, not Media Services, keeps the information that belongs in Storage.</span><span class="sxs-lookup"><span data-stu-id="633ee-116">Now Storage, not Media Services, keeps the information that belongs in Storage.</span></span> 

## <a name="where-did-client-side-storage-encryption-go"></a><span data-ttu-id="633ee-117">Where did client-side storage encryption go?</span><span class="sxs-lookup"><span data-stu-id="633ee-117">Where did client-side storage encryption go?</span></span>

<span data-ttu-id="633ee-118">We now recommend server-side storage encryption (which is on by default).For more information, see [Azure Storage Service Encryption for Data at Rest](https://docs.microsoft.com/azure/storage/common/storage-service-encryption).</span><span class="sxs-lookup"><span data-stu-id="633ee-118">We now recommend server-side storage encryption (which is on by default).For more information, see [Azure Storage Service Encryption for Data at Rest](https://docs.microsoft.com/azure/storage/common/storage-service-encryption).</span></span>

## <a name="what-is-the-recommended-upload-method"></a><span data-ttu-id="633ee-119">What is the recommended upload method?</span><span class="sxs-lookup"><span data-stu-id="633ee-119">What is the recommended upload method?</span></span>

<span data-ttu-id="633ee-120">We recommend the use of HTTP(s) ingests.</span><span class="sxs-lookup"><span data-stu-id="633ee-120">We recommend the use of HTTP(s) ingests.</span></span> <span data-ttu-id="633ee-121">For more information, see [HTTP(s) ingest](job-input-from-http-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="633ee-121">For more information, see [HTTP(s) ingest](job-input-from-http-how-to.md).</span></span>

## <a name="how-does-pagination-work"></a><span data-ttu-id="633ee-122">How does pagination work?</span><span class="sxs-lookup"><span data-stu-id="633ee-122">How does pagination work?</span></span>

<span data-ttu-id="633ee-123">Media Services supports $top for resources that support OData but the value passed to $top must be less than 1000 (for example, the page size for pagination).</span><span class="sxs-lookup"><span data-stu-id="633ee-123">Media Services supports $top for resources that support OData but the value passed to $top must be less than 1000 (for example, the page size for pagination).</span></span>

<span data-ttu-id="633ee-124">This allows you to either get a small sample of items using $top (for example, the 100 most recent items) or to page though all items using pagination.</span><span class="sxs-lookup"><span data-stu-id="633ee-124">This allows you to either get a small sample of items using $top (for example, the 100 most recent items) or to page though all items using pagination.</span></span> 

<span data-ttu-id="633ee-125">Media Services does not support paging through the data with a user specified page size.</span><span class="sxs-lookup"><span data-stu-id="633ee-125">Media Services does not support paging through the data with a user specified page size.</span></span>

<span data-ttu-id="633ee-126">For more information, see [Filtering, ordering, paging](assets-concept.md#filtering-ordering-paging)</span><span class="sxs-lookup"><span data-stu-id="633ee-126">For more information, see [Filtering, ordering, paging](assets-concept.md#filtering-ordering-paging)</span></span>

## <a name="how-to-retrieve-an-entity-in-media-services-v3"></a><span data-ttu-id="633ee-127">How to retrieve an entity in Media Services v3?</span><span class="sxs-lookup"><span data-stu-id="633ee-127">How to retrieve an entity in Media Services v3?</span></span>

<span data-ttu-id="633ee-128">v3 is based on a unified API surface, which exposes both management and operations functionality built on **Azure Resource Manager**.</span><span class="sxs-lookup"><span data-stu-id="633ee-128">v3 is based on a unified API surface, which exposes both management and operations functionality built on **Azure Resource Manager**.</span></span> <span data-ttu-id="633ee-129">In accordance with **Azure Resource Manager**, the resource names are always unique.</span><span class="sxs-lookup"><span data-stu-id="633ee-129">In accordance with **Azure Resource Manager**, the resource names are always unique.</span></span> <span data-ttu-id="633ee-130">Thus, you can use any unique identifier strings (for example, GUIDs) for your resource names.</span><span class="sxs-lookup"><span data-stu-id="633ee-130">Thus, you can use any unique identifier strings (for example, GUIDs) for your resource names.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="633ee-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="633ee-131">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="633ee-132">Media Services v3 overview</span><span class="sxs-lookup"><span data-stu-id="633ee-132">Media Services v3 overview</span></span>](media-services-overview.md)
