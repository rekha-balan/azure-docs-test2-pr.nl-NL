---
title: Resize and crop Bing thumbnails | Microsoft Docs
description: Shows how to resize and crop thumbnails included in a Bing response.
services: cognitive-services
author: swhite-msft
manager: ehansen
ms.assetid: F4FFAE91-A003-4F7C-8E60-83A142485E28
ms.service: cognitive-services
ms.component: bing-image-search
ms.topic: article
ms.date: 04/15/2017
ms.author: scottwhi
ms.openlocfilehash: 98c4caa50ca5e861f4276e26983ef501d17bd349
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865597"
---
# <a name="resizing-and-cropping-thumbnail-images"></a><span data-ttu-id="32fc8-103">Resizing and cropping thumbnail images</span><span class="sxs-lookup"><span data-stu-id="32fc8-103">Resizing and cropping thumbnail images</span></span>

<span data-ttu-id="32fc8-104">Upon processing a search query, Bing will generate thumbnail information for all images in its [response](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/concepts/bing-image-search-get-images#bing-image-search-response-format).</span><span class="sxs-lookup"><span data-stu-id="32fc8-104">Upon processing a search query, Bing will generate thumbnail information for all images in its [response](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/concepts/bing-image-search-get-images#bing-image-search-response-format).</span></span> <span data-ttu-id="32fc8-105">This information can be used to display all, or a subset of the returned thumbnails.</span><span class="sxs-lookup"><span data-stu-id="32fc8-105">This information can be used to display all, or a subset of the returned thumbnails.</span></span> <span data-ttu-id="32fc8-106">If you display a subset, provide a option to view the remaining images.</span><span class="sxs-lookup"><span data-stu-id="32fc8-106">If you display a subset, provide a option to view the remaining images.</span></span> 


<!-- Removing image until we can replace it with a sanatized version.
![Expanded view of thumbnail image](../bing-web-search/media/cognitive-services-bing-web-api/bing-web-image-thumbnail-expansion.PNG)
-->

<span data-ttu-id="32fc8-107">If the user clicks the thumbnail, you can use [contentUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image-contenturl) to display the full-size image to the user.</span><span class="sxs-lookup"><span data-stu-id="32fc8-107">If the user clicks the thumbnail, you can use [contentUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image-contenturl) to display the full-size image to the user.</span></span> <span data-ttu-id="32fc8-108">Be sure to attribute the image.</span><span class="sxs-lookup"><span data-stu-id="32fc8-108">Be sure to attribute the image.</span></span>

<span data-ttu-id="32fc8-109">If `shoppingSourcesCount` or `recipeSourcesCount` are greater than zero, add badging, such as a shopping cart, to the thumbnail to indicate that shopping or recipes exist for the item in the image.</span><span class="sxs-lookup"><span data-stu-id="32fc8-109">If `shoppingSourcesCount` or `recipeSourcesCount` are greater than zero, add badging, such as a shopping cart, to the thumbnail to indicate that shopping or recipes exist for the item in the image.</span></span>

<!-- this is a sanitized version but we're removing all images for now until everything is sanitized.
![Shopping sources badge](./media/cognitive-services-bing-images-api/bing-images-shopping-source.PNG)
-->

<span data-ttu-id="32fc8-110">To get insights about the image, such as web pages that include the image or people that were recognized in the image, use [imageInsightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image-imageinsightstoken).</span><span class="sxs-lookup"><span data-stu-id="32fc8-110">To get insights about the image, such as web pages that include the image or people that were recognized in the image, use [imageInsightsToken](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image-imageinsightstoken).</span></span> <span data-ttu-id="32fc8-111">For details, see [Image Insights](image-insights.md).</span><span class="sxs-lookup"><span data-stu-id="32fc8-111">For details, see [Image Insights](image-insights.md).</span></span>

## <a name="resizing-and-cropping-thumbnails"></a><span data-ttu-id="32fc8-112">Resizing and cropping thumbnails</span><span class="sxs-lookup"><span data-stu-id="32fc8-112">Resizing and cropping thumbnails</span></span>

<span data-ttu-id="32fc8-113">You can also resize and expand thumbnails, such as when a user's cursor hovers above it.</span><span class="sxs-lookup"><span data-stu-id="32fc8-113">You can also resize and expand thumbnails, such as when a user's cursor hovers above it.</span></span> 
> [!NOTE]
> <span data-ttu-id="32fc8-114">Be sure to attribute the image if you expand it.</span><span class="sxs-lookup"><span data-stu-id="32fc8-114">Be sure to attribute the image if you expand it.</span></span> <span data-ttu-id="32fc8-115">For example, by extracting the host from [hostPageDisplayUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image-hostpagedisplayurl) and displaying it below the image.</span><span class="sxs-lookup"><span data-stu-id="32fc8-115">For example, by extracting the host from [hostPageDisplayUrl](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference#image-hostpagedisplayurl) and displaying it below the image.</span></span> 

[!INCLUDE [cognitive-services-bing-resize-crop-thumbnails](../../../includes/cognitive-services-bing-resize-crop-thumbnails.md)]