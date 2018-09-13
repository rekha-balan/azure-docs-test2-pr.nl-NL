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
# <a name="overview"></a>Overview
Content moderation is the process of monitoring User Generated Content (UGC) on online and social media web sites, chat and messaging platforms, and peer communication platforms to track, flag, assess and filter out offensive and unwanted content that creates risks for businesses. The content can include text, images, and videos.

## <a name="where-would-you-use-it"></a>Where would you use it
Content moderation for all three types of content has several benefits.They are

- Image moderation works great for profile pictures, social media, business documents, and image sharing sites.
- Text moderation benefits communities, family-based web sites, in-game communities, chat and messaging platforms, and user-generated content marketing.
- Video moderation is used for video publishing sites, news sites, and video content sites, to take a few examples.

## <a name="three-ways-to-moderate-content"></a>Three ways to moderate content
- Automated moderation applies machine learning and AI to cost-effectively moderate at scale
- Human moderation uses teams and the community to moderate all content.
- Hybrid moderation combines automated moderation augmented by the human-in-the-loop (human oversight).

Microsoft Content Moderator enables all three scenarios.

## <a name="get-started-with-the-human-review-tool"></a>Get started with the human review tool
The online [human review tool](quick-start.md) makes it easy to try the automated moderation APIs. It helps augment automated moderation with human-in-the-loop capabilities. It internally calls the automated moderation APIs and make the reviews available right within your web browser. You can invite other users, track pending invites, and assign permissions to your team members. 

Use the [review API](review-api.md) to auto-moderate content in bulk and review the tagged images or text within the review tool. Provide your API callback point so that you get notified when the reviewers submit their decisions. This allows you to automate the post-review workflow by integrating with your own systems.

## <a name="directly-use-the-automated-moderation-apis"></a>Directly use the automated moderation APIs
You can sign up for the free tiers of [text moderation](text-moderation-api.md) and [image moderation](image-moderation-api.md) APIs and apply to use the private preview of the [video moderation](video-moderation-api.md) APIs to automatically moderate large amount of content and integrate with your review tools and processes. 

