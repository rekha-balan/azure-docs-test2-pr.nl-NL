---
title: Upgrading to the Azure Search Service REST API version 2016-09-01 | Microsoft Docs
description: Upgrading to the Azure Search Service REST API version 2016-09-01
services: search
documentationcenter: ''
author: brjohnstmsft
manager: pablocas
editor: ''
ms.assetid: 6183fa6c-48bb-4af7-adae-4be3bc43c3ed
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 10/27/2016
ms.author: brjohnst
ms.openlocfilehash: f6a189c2e314b91c490583a86d8bacca8ec78a0f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551353"
---
# <a name="upgrading-to-the-azure-search-service-rest-api-version-2016-09-01"></a><span data-ttu-id="b8643-103">Upgrading to the Azure Search Service REST API version 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="b8643-103">Upgrading to the Azure Search Service REST API version 2016-09-01</span></span>
<span data-ttu-id="b8643-104">If you're using version 2015-02-28 or 2015-02-28-Preview of the [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application to use the next generally available API version, 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="b8643-104">If you're using version 2015-02-28 or 2015-02-28-Preview of the [Azure Search Service REST API](https://msdn.microsoft.com/library/azure/dn798935.aspx), this article will help you upgrade your application to use the next generally available API version, 2016-09-01.</span></span>

<span data-ttu-id="b8643-105">Version 2016-09-01 of the REST API contains some changes from earlier versions.</span><span class="sxs-lookup"><span data-stu-id="b8643-105">Version 2016-09-01 of the REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="b8643-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span><span class="sxs-lookup"><span data-stu-id="b8643-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="b8643-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span><span class="sxs-lookup"><span data-stu-id="b8643-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="b8643-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span><span class="sxs-lookup"><span data-stu-id="b8643-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="b8643-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span><span class="sxs-lookup"><span data-stu-id="b8643-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2016-09-01"></a><span data-ttu-id="b8643-110">What's new in version 2016-09-01</span><span class="sxs-lookup"><span data-stu-id="b8643-110">What's new in version 2016-09-01</span></span>
<span data-ttu-id="b8643-111">Version 2016-09-01 is the second generally available release of the Azure Search Service REST API.</span><span class="sxs-lookup"><span data-stu-id="b8643-111">Version 2016-09-01 is the second generally available release of the Azure Search Service REST API.</span></span> <span data-ttu-id="b8643-112">New features in this API version include:</span><span class="sxs-lookup"><span data-stu-id="b8643-112">New features in this API version include:</span></span>

* <span data-ttu-id="b8643-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you to take control over the process of converting text into indexable and searchable tokens.</span><span class="sxs-lookup"><span data-stu-id="b8643-113">[Custom analyzers](https://aka.ms/customanalyzers), which allow you to take control over the process of converting text into indexable and searchable tokens.</span></span>
* <span data-ttu-id="b8643-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you to easily import data from Azure storage into Azure Search on a schedule or on-demand.</span><span class="sxs-lookup"><span data-stu-id="b8643-114">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexers, which allow you to easily import data from Azure storage into Azure Search on a schedule or on-demand.</span></span>
* <span data-ttu-id="b8643-115">[Field mappings](search-indexer-field-mappings.md), which allow you to customize how indexers import data into Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b8643-115">[Field mappings](search-indexer-field-mappings.md), which allow you to customize how indexers import data into Azure Search.</span></span>
* <span data-ttu-id="b8643-116">ETags, which allow you to update the definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span><span class="sxs-lookup"><span data-stu-id="b8643-116">ETags, which allow you to update the definitions of indexes, indexers, and data sources in a concurrency-safe manner.</span></span> 

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="b8643-117">Steps to upgrade</span><span class="sxs-lookup"><span data-stu-id="b8643-117">Steps to upgrade</span></span>
<span data-ttu-id="b8643-118">If you are upgrading from version 2015-02-28, you probably won't have to make any changes to your code, other than to change the version number.</span><span class="sxs-lookup"><span data-stu-id="b8643-118">If you are upgrading from version 2015-02-28, you probably won't have to make any changes to your code, other than to change the version number.</span></span> <span data-ttu-id="b8643-119">The only situations in which you may need to change code are when:</span><span class="sxs-lookup"><span data-stu-id="b8643-119">The only situations in which you may need to change code are when:</span></span>

* <span data-ttu-id="b8643-120">Your code fails when unrecognized properties are returned in an API response.</span><span class="sxs-lookup"><span data-stu-id="b8643-120">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="b8643-121">By default your application should ignore properties that it does not understand.</span><span class="sxs-lookup"><span data-stu-id="b8643-121">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="b8643-122">Your code persists API requests and tries to resend them to the new API version.</span><span class="sxs-lookup"><span data-stu-id="b8643-122">Your code persists API requests and tries to resend them to the new API version.</span></span> <span data-ttu-id="b8643-123">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span><span class="sxs-lookup"><span data-stu-id="b8643-123">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://msdn.microsoft.com/library/azure/dn798927.aspx#Anchor_1)).</span></span>

<span data-ttu-id="b8643-124">If either of these situations apply to you, then you may need to change your code accordingly.</span><span class="sxs-lookup"><span data-stu-id="b8643-124">If either of these situations apply to you, then you may need to change your code accordingly.</span></span> <span data-ttu-id="b8643-125">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="b8643-125">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2016-09-01.</span></span>

<span data-ttu-id="b8643-126">If you are upgrading from version 2015-02-28-Preview, the above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span><span class="sxs-lookup"><span data-stu-id="b8643-126">If you are upgrading from version 2015-02-28-Preview, the above also applies, but you must also be aware that some preview features are not available in version 2016-09-01:</span></span>

* <span data-ttu-id="b8643-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span><span class="sxs-lookup"><span data-stu-id="b8643-127">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="b8643-128">Synonyms</span><span class="sxs-lookup"><span data-stu-id="b8643-128">Synonyms</span></span>
* <span data-ttu-id="b8643-129">"More like this" queries</span><span class="sxs-lookup"><span data-stu-id="b8643-129">"More like this" queries</span></span>

<span data-ttu-id="b8643-130">If your code uses these features, you will not be able to upgrade to 2016-09-01 without removing your usage of them.</span><span class="sxs-lookup"><span data-stu-id="b8643-130">If your code uses these features, you will not be able to upgrade to 2016-09-01 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b8643-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span><span class="sxs-lookup"><span data-stu-id="b8643-131">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="b8643-132">Conclusion</span><span class="sxs-lookup"><span data-stu-id="b8643-132">Conclusion</span></span>
<span data-ttu-id="b8643-133">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span><span class="sxs-lookup"><span data-stu-id="b8643-133">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://msdn.microsoft.com/library/azure/dn798935.aspx) on MSDN.</span></span>

<span data-ttu-id="b8643-134">We welcome your feedback on Azure Search.</span><span class="sxs-lookup"><span data-stu-id="b8643-134">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="b8643-135">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="b8643-135">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="b8643-136">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="b8643-136">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span></span>

<span data-ttu-id="b8643-137">Thank you for using Azure Search!</span><span class="sxs-lookup"><span data-stu-id="b8643-137">Thank you for using Azure Search!</span></span>

