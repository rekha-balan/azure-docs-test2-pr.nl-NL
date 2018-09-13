---
title: Recommendations API | Microsoft Docs
description: Use the Recommendations API, built with Microsoft Azure Machine Learning, to help your customer discover items in your catalog in Cognitive Services.
services: cognitive-services
author: LuisCabrer
manager: mwinkle
ms.service: cognitive-services
ms.technology: recommendations
ms.topic: article
ms.date: 06/18/2016
ms.author: luisca
ms.openlocfilehash: 55d37e18886cc7ef4e7116091fd06f5775e89375
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564599"
---
# <a name="recommendations"></a><span data-ttu-id="8fcb6-103">Recommendations</span><span class="sxs-lookup"><span data-stu-id="8fcb6-103">Recommendations</span></span>

<span data-ttu-id="8fcb6-104">The Recommendations API built with Microsoft Azure Machine Learning helps your customer discover items in your catalog.</span><span class="sxs-lookup"><span data-stu-id="8fcb6-104">The Recommendations API built with Microsoft Azure Machine Learning helps your customer discover items in your catalog.</span></span> <span data-ttu-id="8fcb6-105">Customer activity in your digital store is used to recommend items and to improve conversion in your digital store.</span><span class="sxs-lookup"><span data-stu-id="8fcb6-105">Customer activity in your digital store is used to recommend items and to improve conversion in your digital store.</span></span>

<span data-ttu-id="8fcb6-106">The recommendation engine may be trained by uploading data about past customer activity or by collecting data directly from your digital store.</span><span class="sxs-lookup"><span data-stu-id="8fcb6-106">The recommendation engine may be trained by uploading data about past customer activity or by collecting data directly from your digital store.</span></span> <span data-ttu-id="8fcb6-107">When the customer returns to your store you will be able to feature recommended items from your catalog that may increase your conversion rate.</span><span class="sxs-lookup"><span data-stu-id="8fcb6-107">When the customer returns to your store you will be able to feature recommended items from your catalog that may increase your conversion rate.</span></span>

## <a name="resources"></a><span data-ttu-id="8fcb6-108">Resources</span><span class="sxs-lookup"><span data-stu-id="8fcb6-108">Resources</span></span> ##

[<span data-ttu-id="8fcb6-109">Getting Started Guide</span><span class="sxs-lookup"><span data-stu-id="8fcb6-109">Getting Started Guide</span></span>](../../../articles/cognitive-services/cognitive-services-recommendations-quick-start.md)

[<span data-ttu-id="8fcb6-110">Collecting Data to Train your Model</span><span class="sxs-lookup"><span data-stu-id="8fcb6-110">Collecting Data to Train your Model</span></span>](../../../articles/cognitive-services/cognitive-services-recommendations-collecting-data.md)

[<span data-ttu-id="8fcb6-111">Build Types and Model Quality</span><span class="sxs-lookup"><span data-stu-id="8fcb6-111">Build Types and Model Quality</span></span>](../../../articles/cognitive-services/cognitive-services-recommendations-buildtypes.md)

[<span data-ttu-id="8fcb6-112">API Reference</span><span class="sxs-lookup"><span data-stu-id="8fcb6-112">API Reference</span></span>](https://westus.dev.cognitive.microsoft.com/docs/services/Recommendations.V4.0)

## <a name="common-scenarios-supported-by-recommendations"></a><span data-ttu-id="8fcb6-113">Common Scenarios Supported By Recommendations</span><span class="sxs-lookup"><span data-stu-id="8fcb6-113">Common Scenarios Supported By Recommendations</span></span>

<span data-ttu-id="8fcb6-114">**Frequently Bought Together (FBT) Recommendations**</span><span class="sxs-lookup"><span data-stu-id="8fcb6-114">**Frequently Bought Together (FBT) Recommendations**</span></span>

<span data-ttu-id="8fcb6-115">In this scenario the recommendations engine will recommend items that are likely to be purchased together in the same transaction with a particular item.</span><span class="sxs-lookup"><span data-stu-id="8fcb6-115">In this scenario the recommendations engine will recommend items that are likely to be purchased together in the same transaction with a particular item.</span></span>

<span data-ttu-id="8fcb6-116">For instance, in the example below, customers who bought the Wedge Touch Mouse were also likely to buy the at least one of the following product in the same transaction: Wedge Mobile Keyboard, the Surface VGA Adapter and Surface 2.</span><span class="sxs-lookup"><span data-stu-id="8fcb6-116">For instance, in the example below, customers who bought the Wedge Touch Mouse were also likely to buy the at least one of the following product in the same transaction: Wedge Mobile Keyboard, the Surface VGA Adapter and Surface 2.</span></span>

<span data-ttu-id="8fcb6-117">**Item to Item Recommendations**</span><span class="sxs-lookup"><span data-stu-id="8fcb6-117">**Item to Item Recommendations**</span></span>

<span data-ttu-id="8fcb6-118">A common scenario that uses this capability, is "people who visited/clicked on this item, also visited/clicked on this item".</span><span class="sxs-lookup"><span data-stu-id="8fcb6-118">A common scenario that uses this capability, is "people who visited/clicked on this item, also visited/clicked on this item".</span></span>

<span data-ttu-id="8fcb6-119">For instance, in the example below, most people who visited the "Wedge Touch Mouse" details page also visited the pages related to other mouse devices.</span><span class="sxs-lookup"><span data-stu-id="8fcb6-119">For instance, in the example below, most people who visited the "Wedge Touch Mouse" details page also visited the pages related to other mouse devices.</span></span>

<span data-ttu-id="8fcb6-120">**Customer to Item Recommendations**</span><span class="sxs-lookup"><span data-stu-id="8fcb6-120">**Customer to Item Recommendations**</span></span>

<span data-ttu-id="8fcb6-121">Given a customer's prior activity, it is possible to recommend items that the customer may be interested in.</span><span class="sxs-lookup"><span data-stu-id="8fcb6-121">Given a customer's prior activity, it is possible to recommend items that the customer may be interested in.</span></span>

<span data-ttu-id="8fcb6-122">For instance, given all movies watched by a customer, it is possible to recommend additional content that may be of interest to the customer.</span><span class="sxs-lookup"><span data-stu-id="8fcb6-122">For instance, given all movies watched by a customer, it is possible to recommend additional content that may be of interest to the customer.</span></span>

## <a name="questions"></a><span data-ttu-id="8fcb6-123">Questions?</span><span class="sxs-lookup"><span data-stu-id="8fcb6-123">Questions?</span></span>
<span data-ttu-id="8fcb6-124">Feel free to contacts us at mlapi@microsoft.com</span><span class="sxs-lookup"><span data-stu-id="8fcb6-124">Feel free to contacts us at mlapi@microsoft.com</span></span>


