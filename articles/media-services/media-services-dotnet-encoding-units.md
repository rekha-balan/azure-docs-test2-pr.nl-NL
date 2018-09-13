---
title: Scale media processing by adding encoding units - Azure |  Microsoft Docs
description: Learn how to how to add encoding units with .NET
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: 33f7625a-966a-4f06-bc09-bccd6e2a42b5
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: juliako;milangada;
ms.openlocfilehash: ee40b92c48d91a391fe72582c7ea5e244907747f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553331"
---
# <a name="how-to-scale-encoding-with-net-sdk"></a><span data-ttu-id="11559-103">How to scale encoding with .NET SDK</span><span class="sxs-lookup"><span data-stu-id="11559-103">How to scale encoding with .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [Portal](media-services-portal-scale-media-processing.md)
> * [.NET](media-services-dotnet-encoding-units.md)
> * [REST](https://docs.microsoft.com/rest/api/media/operations/encodingreservedunittype)
> * [Java](https://github.com/southworkscom/azure-sdk-for-media-services-java-samples)
> * [PHP](https://github.com/Azure/azure-sdk-for-php/tree/master/examples/MediaServices)
> 
> 

## <a name="overview"></a><span data-ttu-id="11559-109">Overview</span><span class="sxs-lookup"><span data-stu-id="11559-109">Overview</span></span>
> [!IMPORTANT]
> Make sure to review the [overview](media-services-scale-media-processing-overview.md) topic to get more information about scaling media processing topic.
> 
> 

<span data-ttu-id="11559-111">To change the reserved unit type and the number of encoding reserved units using .NET SDK, do the following:</span><span class="sxs-lookup"><span data-stu-id="11559-111">To change the reserved unit type and the number of encoding reserved units using .NET SDK, do the following:</span></span>

    IEncodingReservedUnit encodingS1ReservedUnit = _context.EncodingReservedUnits.FirstOrDefault();
    encodingS1ReservedUnit.ReservedUnitType = ReservedUnitType.Basic; // Corresponds to S1
    encodingS1ReservedUnit.Update();
    Console.WriteLine("Reserved Unit Type: {0}", encodingS1ReservedUnit.ReservedUnitType);

    encodingS1ReservedUnit.CurrentReservedUnits = 2;
    encodingS1ReservedUnit.Update();

    Console.WriteLine("Number of reserved units: {0}", encodingS1ReservedUnit.CurrentReservedUnits);

## <a name="opening-a-support-ticket"></a><span data-ttu-id="11559-112">Opening a Support Ticket</span><span class="sxs-lookup"><span data-stu-id="11559-112">Opening a Support Ticket</span></span>
<span data-ttu-id="11559-113">By default every Media Services account can scale to up to 25 Encoding and 5 On-Demand Streaming Reserved Units.</span><span class="sxs-lookup"><span data-stu-id="11559-113">By default every Media Services account can scale to up to 25 Encoding and 5 On-Demand Streaming Reserved Units.</span></span> <span data-ttu-id="11559-114">You can request a higher limit by opening a support ticket.</span><span class="sxs-lookup"><span data-stu-id="11559-114">You can request a higher limit by opening a support ticket.</span></span>

### <a name="open-a-support-ticket"></a><span data-ttu-id="11559-115">Open a support ticket</span><span class="sxs-lookup"><span data-stu-id="11559-115">Open a support ticket</span></span>
<span data-ttu-id="11559-116">To open a support ticket do the following:</span><span class="sxs-lookup"><span data-stu-id="11559-116">To open a support ticket do the following:</span></span>

1. <span data-ttu-id="11559-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span><span class="sxs-lookup"><span data-stu-id="11559-117">Click [Get Support](https://manage.windowsazure.com/?getsupport=true).</span></span> <span data-ttu-id="11559-118">If you are not logged in, you will be prompted to enter your credentials.</span><span class="sxs-lookup"><span data-stu-id="11559-118">If you are not logged in, you will be prompted to enter your credentials.</span></span>
2. <span data-ttu-id="11559-119">Select your subscription.</span><span class="sxs-lookup"><span data-stu-id="11559-119">Select your subscription.</span></span>
3. <span data-ttu-id="11559-120">Under support type, select "Technical".</span><span class="sxs-lookup"><span data-stu-id="11559-120">Under support type, select "Technical".</span></span>
4. <span data-ttu-id="11559-121">Click on "Create Ticket".</span><span class="sxs-lookup"><span data-stu-id="11559-121">Click on "Create Ticket".</span></span>
5. <span data-ttu-id="11559-122">Select "Azure Media Services" in the product list presented on the next page.</span><span class="sxs-lookup"><span data-stu-id="11559-122">Select "Azure Media Services" in the product list presented on the next page.</span></span>
6. <span data-ttu-id="11559-123">Select a "Problem type" that is appropriate for your issue.</span><span class="sxs-lookup"><span data-stu-id="11559-123">Select a "Problem type" that is appropriate for your issue.</span></span>
7. <span data-ttu-id="11559-124">Click Continue.</span><span class="sxs-lookup"><span data-stu-id="11559-124">Click Continue.</span></span>
8. <span data-ttu-id="11559-125">Follow instructions on next page and then enter details about your issue.</span><span class="sxs-lookup"><span data-stu-id="11559-125">Follow instructions on next page and then enter details about your issue.</span></span>
9. <span data-ttu-id="11559-126">Click submit to open the ticket.</span><span class="sxs-lookup"><span data-stu-id="11559-126">Click submit to open the ticket.</span></span>

## <a name="media-services-learning-paths"></a><span data-ttu-id="11559-127">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="11559-127">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="11559-128">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="11559-128">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

