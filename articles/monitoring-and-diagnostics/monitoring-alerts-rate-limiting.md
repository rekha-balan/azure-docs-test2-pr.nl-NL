---
title: Rate Limiting for SMS, Emails and Webhooks | Microsoft Docs
description: Be notified via SMS, webhook, and email when certain events occur in the Activity log.
author: anirudhcavale
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: ''
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: ancav
ms.openlocfilehash: 93f8d0f32a851d530df84186d419bd8e2d47f1bc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662767"
---
# <a name="rate-limiting-for-sms-emails-and-webhooks"></a><span data-ttu-id="734a7-103">Rate Limiting for SMS, Emails and Webhooks</span><span class="sxs-lookup"><span data-stu-id="734a7-103">Rate Limiting for SMS, Emails and Webhooks</span></span>
<span data-ttu-id="734a7-104">Rate limiting is a suspension of notifications that occurs when too many are sent to a particular phone number or email.</span><span class="sxs-lookup"><span data-stu-id="734a7-104">Rate limiting is a suspension of notifications that occurs when too many are sent to a particular phone number or email.</span></span> <span data-ttu-id="734a7-105">Limiting ensures that communication around activity log alerts and service health alerts are manageable and actionable</span><span class="sxs-lookup"><span data-stu-id="734a7-105">Limiting ensures that communication around activity log alerts and service health alerts are manageable and actionable</span></span>

<span data-ttu-id="734a7-106">The rules for SMS and Email are the same.</span><span class="sxs-lookup"><span data-stu-id="734a7-106">The rules for SMS and Email are the same.</span></span> <span data-ttu-id="734a7-107">The rate limit threshold for</span><span class="sxs-lookup"><span data-stu-id="734a7-107">The rate limit threshold for</span></span>
 - <span data-ttu-id="734a7-108">SMS - 10 messages in an hour</span><span class="sxs-lookup"><span data-stu-id="734a7-108">SMS - 10 messages in an hour</span></span>
 - <span data-ttu-id="734a7-109">Email - 100 messages in and hour</span><span class="sxs-lookup"><span data-stu-id="734a7-109">Email - 100 messages in and hour</span></span>

## <a name="rate-limit-rules"></a><span data-ttu-id="734a7-110">Rate Limit rules</span><span class="sxs-lookup"><span data-stu-id="734a7-110">Rate Limit rules</span></span>
- <span data-ttu-id="734a7-111">A particular phone number or email is rate limited when it receives more than the threshold</span><span class="sxs-lookup"><span data-stu-id="734a7-111">A particular phone number or email is rate limited when it receives more than the threshold</span></span>
- <span data-ttu-id="734a7-112">A phone number or email can be part of action groups across many subscriptions.</span><span class="sxs-lookup"><span data-stu-id="734a7-112">A phone number or email can be part of action groups across many subscriptions.</span></span> <span data-ttu-id="734a7-113">Rate limiting applies across all subscriptions, that is, it applies as soon as the threshold is reached even if sent from multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="734a7-113">Rate limiting applies across all subscriptions, that is, it applies as soon as the threshold is reached even if sent from multiple subscriptions.</span></span>  
- <span data-ttu-id="734a7-114">When a phone number or email is rate limited, an additional message of the same type is sent to communicate the rate limiting.</span><span class="sxs-lookup"><span data-stu-id="734a7-114">When a phone number or email is rate limited, an additional message of the same type is sent to communicate the rate limiting.</span></span> <span data-ttu-id="734a7-115">The SMS or email states when the rate limiting expires.</span><span class="sxs-lookup"><span data-stu-id="734a7-115">The SMS or email states when the rate limiting expires.</span></span>

## <a name="rate-limit-of-webhooks"></a><span data-ttu-id="734a7-116">Rate Limit of Webhooks</span><span class="sxs-lookup"><span data-stu-id="734a7-116">Rate Limit of Webhooks</span></span> ##
<span data-ttu-id="734a7-117">There is no rate limiting in place for webhooks today.</span><span class="sxs-lookup"><span data-stu-id="734a7-117">There is no rate limiting in place for webhooks today.</span></span>

## <a name="next-steps"></a><span data-ttu-id="734a7-118">Next Steps</span><span class="sxs-lookup"><span data-stu-id="734a7-118">Next Steps</span></span> ##
<span data-ttu-id="734a7-119">Learn more on [SMS alert behavior](monitoring-sms-alert-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="734a7-119">Learn more on [SMS alert behavior](monitoring-sms-alert-behavior.md)</span></span>  
<span data-ttu-id="734a7-120">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span><span class="sxs-lookup"><span data-stu-id="734a7-120">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span></span>  
<span data-ttu-id="734a7-121">How to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md)</span><span class="sxs-lookup"><span data-stu-id="734a7-121">How to [configure alerts whenever a service health notification is posted](monitoring-activity-log-alerts-on-service-notifications.md)</span></span>
