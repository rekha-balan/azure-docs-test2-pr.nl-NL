---
title: Azure Content Moderator code samples | Microsoft Docs
description: Use Content Moderator in your applications
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 01/10/2018
ms.author: sajagtap
ms.openlocfilehash: a7f5b0a7433631e303de47667871cc1354053c08
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869254"
---
# <a name="net-sdk-samples"></a><span data-ttu-id="c4db4-103">.NET SDK samples</span><span class="sxs-lookup"><span data-stu-id="c4db4-103">.NET SDK samples</span></span>

<span data-ttu-id="c4db4-104">The following list includes links to the code samples built using the Azure Content Moderator SDK for .NET.</span><span class="sxs-lookup"><span data-stu-id="c4db4-104">The following list includes links to the code samples built using the Azure Content Moderator SDK for .NET.</span></span>

- <span data-ttu-id="c4db4-105">**Helper library**: [Create a Content Moderator client for use in other samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/ModeratorHelper/Clients.cs).</span><span class="sxs-lookup"><span data-stu-id="c4db4-105">**Helper library**: [Create a Content Moderator client for use in other samples](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/ModeratorHelper/Clients.cs).</span></span> <span data-ttu-id="c4db4-106">See [quickstart](content-moderator-helper-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c4db4-106">See [quickstart](content-moderator-helper-quickstart-dotnet.md).</span></span>

## <a name="moderation"></a><span data-ttu-id="c4db4-107">Moderation</span><span class="sxs-lookup"><span data-stu-id="c4db4-107">Moderation</span></span>

- <span data-ttu-id="c4db4-108">**Image moderation**: [Evaluate an image for adult and racy content, text, and faces](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/ImageModeration/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="c4db4-108">**Image moderation**: [Evaluate an image for adult and racy content, text, and faces](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/ImageModeration/Program.cs).</span></span> <span data-ttu-id="c4db4-109">See [quickstart](image-moderation-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c4db4-109">See [quickstart](image-moderation-quickstart-dotnet.md).</span></span>
- <span data-ttu-id="c4db4-110">**Custom images**: [Moderate with custom image lists](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/ImageListManagement/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="c4db4-110">**Custom images**: [Moderate with custom image lists](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/ImageListManagement/Program.cs).</span></span> <span data-ttu-id="c4db4-111">See [quickstart](image-lists-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c4db4-111">See [quickstart](image-lists-quickstart-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c4db4-112">There is a maximum limit of **5 image lists** with each list to **not exceed 10,000 images**.</span><span class="sxs-lookup"><span data-stu-id="c4db4-112">There is a maximum limit of **5 image lists** with each list to **not exceed 10,000 images**.</span></span>
>

- <span data-ttu-id="c4db4-113">**Text moderation**: [Screen text for profanity and personally identifiable information (PII)](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/TextModeration/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="c4db4-113">**Text moderation**: [Screen text for profanity and personally identifiable information (PII)](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/TextModeration/Program.cs).</span></span> <span data-ttu-id="c4db4-114">See [quickstart](text-moderation-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c4db4-114">See [quickstart](text-moderation-quickstart-dotnet.md).</span></span>
- <span data-ttu-id="c4db4-115">**Custom terms**: [Moderate with custom term lists](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/TermListManagement/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="c4db4-115">**Custom terms**: [Moderate with custom term lists](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/TermListManagement/Program.cs).</span></span> <span data-ttu-id="c4db4-116">See [quickstart](term-lists-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c4db4-116">See [quickstart](term-lists-quickstart-dotnet.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c4db4-117">There is a maximum limit of **5 term lists** with each list to **not exceed 10,000 terms**.</span><span class="sxs-lookup"><span data-stu-id="c4db4-117">There is a maximum limit of **5 term lists** with each list to **not exceed 10,000 terms**.</span></span>
>

- <span data-ttu-id="c4db4-118">**Video moderation**: [Scan a video for adult and racy content and get results](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/VideoModeration/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="c4db4-118">**Video moderation**: [Scan a video for adult and racy content and get results](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/VideoModeration/Program.cs).</span></span> <span data-ttu-id="c4db4-119">See [quickstart](video-moderation-api.md).</span><span class="sxs-lookup"><span data-stu-id="c4db4-119">See [quickstart](video-moderation-api.md).</span></span>

## <a name="review"></a><span data-ttu-id="c4db4-120">Review</span><span class="sxs-lookup"><span data-stu-id="c4db4-120">Review</span></span>

- <span data-ttu-id="c4db4-121">**Image jobs**: [Start a moderation job that scans and creates reviews](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/ImageJobs/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="c4db4-121">**Image jobs**: [Start a moderation job that scans and creates reviews](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/ImageJobs/Program.cs).</span></span> <span data-ttu-id="c4db4-122">See [quickstart](moderation-jobs-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c4db4-122">See [quickstart](moderation-jobs-quickstart-dotnet.md).</span></span>
- <span data-ttu-id="c4db4-123">**Image reviews**: [Create reviews for human-in-the-loop](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/ImageReviews/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="c4db4-123">**Image reviews**: [Create reviews for human-in-the-loop](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/ImageReviews/Program.cs).</span></span> <span data-ttu-id="c4db4-124">See [quickstart](moderation-reviews-quickstart-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c4db4-124">See [quickstart](moderation-reviews-quickstart-dotnet.md).</span></span>
- <span data-ttu-id="c4db4-125">**Video reviews**: [Create video reviews for human-in-the-loop](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/VideoReviews/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="c4db4-125">**Video reviews**: [Create video reviews for human-in-the-loop](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/VideoReviews/Program.cs).</span></span> <span data-ttu-id="c4db4-126">See [quickstart](video-reviews-quickstart-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="c4db4-126">See [quickstart](video-reviews-quickstart-dotnet.md)</span></span>
- <span data-ttu-id="c4db4-127">**Video transcript reviews**: [Create video transcript reviews for human-in-the-loop](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/VideoTranscriptReviews/Program.cs) See [quickstart](video-reviews-quickstart-dotnet.md)</span><span class="sxs-lookup"><span data-stu-id="c4db4-127">**Video transcript reviews**: [Create video transcript reviews for human-in-the-loop](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/blob/master/ContentModerator/VideoTranscriptReviews/Program.cs) See [quickstart](video-reviews-quickstart-dotnet.md)</span></span>

<span data-ttu-id="c4db4-128">See all .NET samples at the [Content Moderator .NET samples on GitHub](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator).</span><span class="sxs-lookup"><span data-stu-id="c4db4-128">See all .NET samples at the [Content Moderator .NET samples on GitHub](https://github.com/Azure-Samples/cognitive-services-dotnet-sdk-samples/tree/master/ContentModerator).</span></span>
