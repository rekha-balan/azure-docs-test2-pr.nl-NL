---
title: Restrict Azure CDN content by country | Microsoft Docs
description: Learn how to restrict access to your Azure CDN content using the Geo-Filtering feature.
services: cdn
documentationcenter: ''
author: lichard
manager: akucer
editor: ''
ms.assetid: 12c17cc5-28ee-4b0b-ba22-2266be2e786a
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: rli
ms.openlocfilehash: 7286283e5372244b633d0ed3513cab985ce40385
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556393"
---
# <a name="restrict-azure-cdn-content-by-country"></a><span data-ttu-id="8746f-103">Restrict Azure CDN content by country</span><span class="sxs-lookup"><span data-stu-id="8746f-103">Restrict Azure CDN content by country</span></span>

## <a name="overview"></a><span data-ttu-id="8746f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="8746f-104">Overview</span></span>
<span data-ttu-id="8746f-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span><span class="sxs-lookup"><span data-stu-id="8746f-105">When a user requests your content, by default, the content is served regardless of where the user made this request from.</span></span> <span data-ttu-id="8746f-106">In some cases, you may want to restrict access to your content by country.</span><span class="sxs-lookup"><span data-stu-id="8746f-106">In some cases, you may want to restrict access to your content by country.</span></span> <span data-ttu-id="8746f-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span><span class="sxs-lookup"><span data-stu-id="8746f-107">This topic explains how to use the **Geo-Filtering** feature in order to configure the service to allow or block access by country.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8746f-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span><span class="sxs-lookup"><span data-stu-id="8746f-108">The Verizon and Akamai products provide the same geo-filtering functionality but have a small difference in te country codes they support.</span></span> <span data-ttu-id="8746f-109">See Step 3 for a link to the differences.</span><span class="sxs-lookup"><span data-stu-id="8746f-109">See Step 3 for a link to the differences.</span></span>


<span data-ttu-id="8746f-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span><span class="sxs-lookup"><span data-stu-id="8746f-110">For information about considerations that apply to configuring this type of restriction, see the [Considerations](cdn-restrict-access-by-country.md#considerations) section at the end of the topic.</span></span>  

![Country filtering](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-filtering/cdn-country-filtering-akamai.png)

## <a name="step-1-define-the-directory-path"></a><span data-ttu-id="8746f-112">Step 1: Define the directory path</span><span class="sxs-lookup"><span data-stu-id="8746f-112">Step 1: Define the directory path</span></span>
<span data-ttu-id="8746f-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span><span class="sxs-lookup"><span data-stu-id="8746f-113">Select your endpoint within the portal, and find the Geo-Filtering tab on the left-hand navigation to find this feature.</span></span>

<span data-ttu-id="8746f-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span><span class="sxs-lookup"><span data-stu-id="8746f-114">When configuring a country filter, you must specify the relative path to the location to which users will be allowed or denied access.</span></span> <span data-ttu-id="8746f-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span><span class="sxs-lookup"><span data-stu-id="8746f-115">You can apply geo-filtering for all your files with "/" or selected folders by specifying directory paths "/pictures/".</span></span> <span data-ttu-id="8746f-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span><span class="sxs-lookup"><span data-stu-id="8746f-116">You can also apply geo-filtering to a single file by specifying the file, and leaving out the trailing slash "/pictures/city.png".</span></span>

<span data-ttu-id="8746f-117">Example directory path filter:</span><span class="sxs-lookup"><span data-stu-id="8746f-117">Example directory path filter:</span></span>

    /                                 
    /Photos/
    /Photos/Strasbourg/
      /Photos/Strasbourg/city.png

## <a name="step-2-define-the-action-block-or-allow"></a><span data-ttu-id="8746f-118">Step 2: Define the action: block or allow</span><span class="sxs-lookup"><span data-stu-id="8746f-118">Step 2: Define the action: block or allow</span></span>
<span data-ttu-id="8746f-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span><span class="sxs-lookup"><span data-stu-id="8746f-119">**Block:** Users from the specified countries will be denied access to assets requested from that recursive path.</span></span> <span data-ttu-id="8746f-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span><span class="sxs-lookup"><span data-stu-id="8746f-120">If no other country filtering options have been configured for that location, then all other users will be allowed access.</span></span>

<span data-ttu-id="8746f-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span><span class="sxs-lookup"><span data-stu-id="8746f-121">**Allow:** Only users from the specified countries will be allowed access to assets requested from that recursive path.</span></span>

## <a name="step-3-define-the-countries"></a><span data-ttu-id="8746f-122">Step 3: Define the countries</span><span class="sxs-lookup"><span data-stu-id="8746f-122">Step 3: Define the countries</span></span>
<span data-ttu-id="8746f-123">Select the countries that you want to block or allow for the path.</span><span class="sxs-lookup"><span data-stu-id="8746f-123">Select the countries that you want to block or allow for the path.</span></span> 

<span data-ttu-id="8746f-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span><span class="sxs-lookup"><span data-stu-id="8746f-124">For example, the rule of blocking /Photos/Strasbourg/ will filter files including:</span></span>

    http://<endpoint>.azureedge.net/Photos/Strasbourg/1000.jpg
    http://<endpoint>.azureedge.net/Photos/Strasbourg/Cathedral/1000.jpg


### <a name="country-codes"></a><span data-ttu-id="8746f-125">Country codes</span><span class="sxs-lookup"><span data-stu-id="8746f-125">Country codes</span></span>
<span data-ttu-id="8746f-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span><span class="sxs-lookup"><span data-stu-id="8746f-126">The **Geo-Filtering** feature uses country codes to define the countries from which a request will be allowed or blocked for a secured directory.</span></span> <span data-ttu-id="8746f-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span><span class="sxs-lookup"><span data-stu-id="8746f-127">You will find the country codes in [Azure CDN  Country Codes](https://msdn.microsoft.com/library/mt761717.aspx).</span></span> 

## <a id="considerations"></a><span data-ttu-id="8746f-128">Considerations</span><span class="sxs-lookup"><span data-stu-id="8746f-128">Considerations</span></span>
* <span data-ttu-id="8746f-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span><span class="sxs-lookup"><span data-stu-id="8746f-129">It may take up to 90 minutes for Verizon, or a couple minutes with Akamai, for changes to your country filtering configuration to take effect.</span></span>
* <span data-ttu-id="8746f-130">This feature does not support wildcard characters (for example, ‘\*’).</span><span class="sxs-lookup"><span data-stu-id="8746f-130">This feature does not support wildcard characters (for example, ‘\*’).</span></span>
* <span data-ttu-id="8746f-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span><span class="sxs-lookup"><span data-stu-id="8746f-131">The geo-filtering configuration associated with the relative path will be applied recursively to that path.</span></span>
* <span data-ttu-id="8746f-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span><span class="sxs-lookup"><span data-stu-id="8746f-132">Only one rule can be applied to the same relative path (you cannot create multiple country filters that point to the same relative path.</span></span> <span data-ttu-id="8746f-133">However, a folder may have multiple country filters.</span><span class="sxs-lookup"><span data-stu-id="8746f-133">However, a folder may have multiple country filters.</span></span> <span data-ttu-id="8746f-134">This is due to the recursive nature of country filters.</span><span class="sxs-lookup"><span data-stu-id="8746f-134">This is due to the recursive nature of country filters.</span></span> <span data-ttu-id="8746f-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span><span class="sxs-lookup"><span data-stu-id="8746f-135">In other words, a subfolder of a previously configured folder can be assigned a different country filter.</span></span>


