---
title: Upgrading to the latest Azure Search Service REST API version | Microsoft Docs
description: Upgrading to the latest Azure Search Service REST API version
author: brjohnstmsft
manager: jlembicz
services: search
ms.service: search
ms.devlang: rest-api
ms.topic: conceptual
ms.date: 04/20/2018
ms.author: brjohnst
ms.openlocfilehash: 2efe7769f68988f3c0d52c8806b78c1b96d8c639
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44789196"
---
# <a name="upgrading-to-the-latest-azure-search-service-rest-api-version"></a><span data-ttu-id="3e96a-103">Upgrading to the latest Azure Search Service REST API version</span><span class="sxs-lookup"><span data-stu-id="3e96a-103">Upgrading to the latest Azure Search Service REST API version</span></span>
<span data-ttu-id="3e96a-104">If you're using a previous version of the [Azure Search Service REST API](https://docs.microsoft.com/rest/api/searchservice/), this article will help you upgrade your application to use the latest generally available API version, 2017-11-11.</span><span class="sxs-lookup"><span data-stu-id="3e96a-104">If you're using a previous version of the [Azure Search Service REST API](https://docs.microsoft.com/rest/api/searchservice/), this article will help you upgrade your application to use the latest generally available API version, 2017-11-11.</span></span>

<span data-ttu-id="3e96a-105">Version 2017-11-11 of the REST API contains some changes from earlier versions.</span><span class="sxs-lookup"><span data-stu-id="3e96a-105">Version 2017-11-11 of the REST API contains some changes from earlier versions.</span></span> <span data-ttu-id="3e96a-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span><span class="sxs-lookup"><span data-stu-id="3e96a-106">These are mostly backward compatible, so changing your code should require only minimal effort, depending on which version you were using before.</span></span> <span data-ttu-id="3e96a-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span><span class="sxs-lookup"><span data-stu-id="3e96a-107">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new API version.</span></span>

> [!NOTE]
> <span data-ttu-id="3e96a-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span><span class="sxs-lookup"><span data-stu-id="3e96a-108">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="3e96a-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span><span class="sxs-lookup"><span data-stu-id="3e96a-109">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-2017-11-11"></a><span data-ttu-id="3e96a-110">What's new in version 2017-11-11</span><span class="sxs-lookup"><span data-stu-id="3e96a-110">What's new in version 2017-11-11</span></span>
<span data-ttu-id="3e96a-111">Version 2017-11-11 is the latest generally available release of the Azure Search Service REST API.</span><span class="sxs-lookup"><span data-stu-id="3e96a-111">Version 2017-11-11 is the latest generally available release of the Azure Search Service REST API.</span></span> <span data-ttu-id="3e96a-112">New features in this API version include:</span><span class="sxs-lookup"><span data-stu-id="3e96a-112">New features in this API version include:</span></span>

* <span data-ttu-id="3e96a-113">[Synonyms](search-synonyms.md).</span><span class="sxs-lookup"><span data-stu-id="3e96a-113">[Synonyms](search-synonyms.md).</span></span> <span data-ttu-id="3e96a-114">The new synonyms feature allows you to define equivalent terms and expand the scope of the query.</span><span class="sxs-lookup"><span data-stu-id="3e96a-114">The new synonyms feature allows you to define equivalent terms and expand the scope of the query.</span></span>
* <span data-ttu-id="3e96a-115">[Support for efficiently indexing text blobs](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage#IndexingPlainText).</span><span class="sxs-lookup"><span data-stu-id="3e96a-115">[Support for efficiently indexing text blobs](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage#IndexingPlainText).</span></span> <span data-ttu-id="3e96a-116">The new `text` parsing mode for Azure Blob indexers significantly improves indexing performance.</span><span class="sxs-lookup"><span data-stu-id="3e96a-116">The new `text` parsing mode for Azure Blob indexers significantly improves indexing performance.</span></span>
* <span data-ttu-id="3e96a-117">[Service Statistics API](https://docs.microsoft.com/rest/api/searchservice/get-service-statistics).</span><span class="sxs-lookup"><span data-stu-id="3e96a-117">[Service Statistics API](https://docs.microsoft.com/rest/api/searchservice/get-service-statistics).</span></span> <span data-ttu-id="3e96a-118">View the current usage and limits of resources in Azure Search with this new API.</span><span class="sxs-lookup"><span data-stu-id="3e96a-118">View the current usage and limits of resources in Azure Search with this new API.</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="3e96a-119">Steps to upgrade</span><span class="sxs-lookup"><span data-stu-id="3e96a-119">Steps to upgrade</span></span>
<span data-ttu-id="3e96a-120">If you are upgrading from a GA version, 2015-02-28 or 2016-09-01, you probably won't have to make any changes to your code, other than to change the version number.</span><span class="sxs-lookup"><span data-stu-id="3e96a-120">If you are upgrading from a GA version, 2015-02-28 or 2016-09-01, you probably won't have to make any changes to your code, other than to change the version number.</span></span> <span data-ttu-id="3e96a-121">The only situations in which you may need to change code are when:</span><span class="sxs-lookup"><span data-stu-id="3e96a-121">The only situations in which you may need to change code are when:</span></span>

* <span data-ttu-id="3e96a-122">Your code fails when unrecognized properties are returned in an API response.</span><span class="sxs-lookup"><span data-stu-id="3e96a-122">Your code fails when unrecognized properties are returned in an API response.</span></span> <span data-ttu-id="3e96a-123">By default your application should ignore properties that it does not understand.</span><span class="sxs-lookup"><span data-stu-id="3e96a-123">By default your application should ignore properties that it does not understand.</span></span>
* <span data-ttu-id="3e96a-124">Your code persists API requests and tries to resend them to the new API version.</span><span class="sxs-lookup"><span data-stu-id="3e96a-124">Your code persists API requests and tries to resend them to the new API version.</span></span> <span data-ttu-id="3e96a-125">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)).</span><span class="sxs-lookup"><span data-stu-id="3e96a-125">For example, this might happen if your application persists continuation tokens returned from the Search API (for more information, look for `@search.nextPageParameters` in the [Search API Reference](https://docs.microsoft.com/rest/api/searchservice/Search-Documents)).</span></span>

<span data-ttu-id="3e96a-126">If either of these situations apply to you, then you may need to change your code accordingly.</span><span class="sxs-lookup"><span data-stu-id="3e96a-126">If either of these situations apply to you, then you may need to change your code accordingly.</span></span> <span data-ttu-id="3e96a-127">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2017-11-11.</span><span class="sxs-lookup"><span data-stu-id="3e96a-127">Otherwise, no changes should be necessary unless you want to start using the [new features](#WhatsNew) of version 2017-11-11.</span></span>

<span data-ttu-id="3e96a-128">If you are upgrading from a preview api-version, the above also applies, but you must also be aware that some preview features are not available in version 2017-11-11:</span><span class="sxs-lookup"><span data-stu-id="3e96a-128">If you are upgrading from a preview api-version, the above also applies, but you must also be aware that some preview features are not available in version 2017-11-11:</span></span>

* <span data-ttu-id="3e96a-129">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span><span class="sxs-lookup"><span data-stu-id="3e96a-129">Azure Blob Storage indexer support for CSV files and blobs containing JSON arrays.</span></span>
* <span data-ttu-id="3e96a-130">"More like this" queries</span><span class="sxs-lookup"><span data-stu-id="3e96a-130">"More like this" queries</span></span>

<span data-ttu-id="3e96a-131">If your code uses these features, you will not be able to upgrade to 2017-11-11 without removing your usage of them.</span><span class="sxs-lookup"><span data-stu-id="3e96a-131">If your code uses these features, you will not be able to upgrade to 2017-11-11 without removing your usage of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3e96a-132">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span><span class="sxs-lookup"><span data-stu-id="3e96a-132">Please remember, preview APIs are intended for testing and evaluation, and should not be used in production environments.</span></span>
> 
> 

## <a name="conclusion"></a><span data-ttu-id="3e96a-133">Conclusion</span><span class="sxs-lookup"><span data-stu-id="3e96a-133">Conclusion</span></span>
<span data-ttu-id="3e96a-134">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://docs.microsoft.com/rest/api/searchservice/) on MSDN.</span><span class="sxs-lookup"><span data-stu-id="3e96a-134">If you need more details on using the Azure Search Service REST API, see the recently updated [API Reference](https://docs.microsoft.com/rest/api/searchservice/) on MSDN.</span></span>

<span data-ttu-id="3e96a-135">We welcome your feedback on Azure Search.</span><span class="sxs-lookup"><span data-stu-id="3e96a-135">We welcome your feedback on Azure Search.</span></span> <span data-ttu-id="3e96a-136">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span><span class="sxs-lookup"><span data-stu-id="3e96a-136">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch) or [StackOverflow](http://stackoverflow.com/).</span></span> <span data-ttu-id="3e96a-137">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span><span class="sxs-lookup"><span data-stu-id="3e96a-137">If you're asking a question about Azure Search on StackOverflow, make sure to tag it with `azure-search`.</span></span>

<span data-ttu-id="3e96a-138">Thank you for using Azure Search!</span><span class="sxs-lookup"><span data-stu-id="3e96a-138">Thank you for using Azure Search!</span></span>

