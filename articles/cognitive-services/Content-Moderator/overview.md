---
title: Content Moderator overview | Microsoft Docs
description: Content moderation monitors user-generated content so that you can track, flag, assess, and filter inappropriate content.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.technology: content-moderator
ms.topic: article
ms.date: 02/21/2017
ms.author: sajagtap
ms.openlocfilehash: 58764db97f44715a278214e0fe3c54c0c845b2b3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553288"
---
# <a name="overview"></a><span data-ttu-id="6ee88-103">Overview</span><span class="sxs-lookup"><span data-stu-id="6ee88-103">Overview</span></span>
<span data-ttu-id="6ee88-104">Content moderation is the process of monitoring User Generated Content (UGC) on online and social media web sites, chat and messaging platforms, and peer communication platforms to track, flag, assess and filter out offensive and unwanted content that creates risks for businesses.</span><span class="sxs-lookup"><span data-stu-id="6ee88-104">Content moderation is the process of monitoring User Generated Content (UGC) on online and social media web sites, chat and messaging platforms, and peer communication platforms to track, flag, assess and filter out offensive and unwanted content that creates risks for businesses.</span></span> <span data-ttu-id="6ee88-105">The content can include text, images, and videos.</span><span class="sxs-lookup"><span data-stu-id="6ee88-105">The content can include text, images, and videos.</span></span>

## <a name="where-would-you-use-it"></a><span data-ttu-id="6ee88-106">Where would you use it</span><span class="sxs-lookup"><span data-stu-id="6ee88-106">Where would you use it</span></span>
<span data-ttu-id="6ee88-107">Content moderation for all three types of content has several benefits.They are</span><span class="sxs-lookup"><span data-stu-id="6ee88-107">Content moderation for all three types of content has several benefits.They are</span></span>

- <span data-ttu-id="6ee88-108">Image moderation works great for profile pictures, social media, business documents, and image sharing sites.</span><span class="sxs-lookup"><span data-stu-id="6ee88-108">Image moderation works great for profile pictures, social media, business documents, and image sharing sites.</span></span>
- <span data-ttu-id="6ee88-109">Text moderation benefits communities, family-based web sites, in-game communities, chat and messaging platforms, and user-generated content marketing.</span><span class="sxs-lookup"><span data-stu-id="6ee88-109">Text moderation benefits communities, family-based web sites, in-game communities, chat and messaging platforms, and user-generated content marketing.</span></span>
- <span data-ttu-id="6ee88-110">Video moderation is used for video publishing sites, news sites, and video content sites, to take a few examples.</span><span class="sxs-lookup"><span data-stu-id="6ee88-110">Video moderation is used for video publishing sites, news sites, and video content sites, to take a few examples.</span></span>

## <a name="three-ways-to-moderate-content"></a><span data-ttu-id="6ee88-111">Three ways to moderate content</span><span class="sxs-lookup"><span data-stu-id="6ee88-111">Three ways to moderate content</span></span>
- <span data-ttu-id="6ee88-112">Automated moderation applies machine learning and AI to cost-effectively moderate at scale</span><span class="sxs-lookup"><span data-stu-id="6ee88-112">Automated moderation applies machine learning and AI to cost-effectively moderate at scale</span></span>
- <span data-ttu-id="6ee88-113">Human moderation uses teams and the community to moderate all content.</span><span class="sxs-lookup"><span data-stu-id="6ee88-113">Human moderation uses teams and the community to moderate all content.</span></span>
- <span data-ttu-id="6ee88-114">Hybrid moderation combines automated moderation augmented by the human-in-the-loop (human oversight).</span><span class="sxs-lookup"><span data-stu-id="6ee88-114">Hybrid moderation combines automated moderation augmented by the human-in-the-loop (human oversight).</span></span>

<span data-ttu-id="6ee88-115">Microsoft Content Moderator enables all three scenarios.</span><span class="sxs-lookup"><span data-stu-id="6ee88-115">Microsoft Content Moderator enables all three scenarios.</span></span>

## <a name="get-started-with-the-human-review-tool"></a><span data-ttu-id="6ee88-116">Get started with the human review tool</span><span class="sxs-lookup"><span data-stu-id="6ee88-116">Get started with the human review tool</span></span>
<span data-ttu-id="6ee88-117">The online [human review tool](quick-start.md) makes it easy to try the automated moderation APIs.</span><span class="sxs-lookup"><span data-stu-id="6ee88-117">The online [human review tool](quick-start.md) makes it easy to try the automated moderation APIs.</span></span> <span data-ttu-id="6ee88-118">It helps augment automated moderation with human-in-the-loop capabilities.</span><span class="sxs-lookup"><span data-stu-id="6ee88-118">It helps augment automated moderation with human-in-the-loop capabilities.</span></span> <span data-ttu-id="6ee88-119">It internally calls the automated moderation APIs and make the reviews available right within your web browser.</span><span class="sxs-lookup"><span data-stu-id="6ee88-119">It internally calls the automated moderation APIs and make the reviews available right within your web browser.</span></span> <span data-ttu-id="6ee88-120">You can invite other users, track pending invites, and assign permissions to your team members.</span><span class="sxs-lookup"><span data-stu-id="6ee88-120">You can invite other users, track pending invites, and assign permissions to your team members.</span></span> 

<span data-ttu-id="6ee88-121">Use the [review API](review-api.md) to auto-moderate content in bulk and review the tagged images or text within the review tool.</span><span class="sxs-lookup"><span data-stu-id="6ee88-121">Use the [review API](review-api.md) to auto-moderate content in bulk and review the tagged images or text within the review tool.</span></span> <span data-ttu-id="6ee88-122">Provide your API callback point so that you get notified when the reviewers submit their decisions.</span><span class="sxs-lookup"><span data-stu-id="6ee88-122">Provide your API callback point so that you get notified when the reviewers submit their decisions.</span></span> <span data-ttu-id="6ee88-123">This allows you to automate the post-review workflow by integrating with your own systems.</span><span class="sxs-lookup"><span data-stu-id="6ee88-123">This allows you to automate the post-review workflow by integrating with your own systems.</span></span>

## <a name="directly-use-the-automated-moderation-apis"></a><span data-ttu-id="6ee88-124">Directly use the automated moderation APIs</span><span class="sxs-lookup"><span data-stu-id="6ee88-124">Directly use the automated moderation APIs</span></span>
<span data-ttu-id="6ee88-125">You can sign up for the free tiers of [text moderation](text-moderation-api.md) and [image moderation](image-moderation-api.md) APIs and apply to use the private preview of the [video moderation](video-moderation-api.md) APIs to automatically moderate large amount of content and integrate with your review tools and processes.</span><span class="sxs-lookup"><span data-stu-id="6ee88-125">You can sign up for the free tiers of [text moderation](text-moderation-api.md) and [image moderation](image-moderation-api.md) APIs and apply to use the private preview of the [video moderation](video-moderation-api.md) APIs to automatically moderate large amount of content and integrate with your review tools and processes.</span></span> 

