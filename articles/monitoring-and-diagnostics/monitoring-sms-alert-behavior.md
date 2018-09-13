---
title: SMS Alert behavior in Action Groups | Microsoft Docs
description: SMS message format and responding to SMS messages to unsubscribe, resubscribe or request help.
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
ms.openlocfilehash: 10f33898fb86bd2449994a153d99cb59dc6078d6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553361"
---
# <a name="sms-alert-behavior-in-action-groups"></a><span data-ttu-id="dfb02-103">SMS Alert Behavior in Action Groups</span><span class="sxs-lookup"><span data-stu-id="dfb02-103">SMS Alert Behavior in Action Groups</span></span>
## <a name="overview"></a><span data-ttu-id="dfb02-104">Overview</span><span class="sxs-lookup"><span data-stu-id="dfb02-104">Overview</span></span> ##
<span data-ttu-id="dfb02-105">Action groups enable you to configure a list of receivers.</span><span class="sxs-lookup"><span data-stu-id="dfb02-105">Action groups enable you to configure a list of receivers.</span></span> <span data-ttu-id="dfb02-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when the activity log alert is triggered.</span><span class="sxs-lookup"><span data-stu-id="dfb02-106">These groups can then be leveraged when defining activity log alerts; ensuring that a particular action group is notified when the activity log alert is triggered.</span></span> <span data-ttu-id="dfb02-107">One of the alerting mechanisms supported is SMS; the alerts support bi-directional communication.</span><span class="sxs-lookup"><span data-stu-id="dfb02-107">One of the alerting mechanisms supported is SMS; the alerts support bi-directional communication.</span></span> <span data-ttu-id="dfb02-108">A user can respond to an alert to:</span><span class="sxs-lookup"><span data-stu-id="dfb02-108">A user can respond to an alert to:</span></span>

- <span data-ttu-id="dfb02-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span><span class="sxs-lookup"><span data-stu-id="dfb02-109">**Unsubscribe from alerts:** A user can unsubscribe from all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="dfb02-110">**Resubscribe to alerts:** A user can resubscribe to all SMS alerts for all action groups, or a singular action group.</span><span class="sxs-lookup"><span data-stu-id="dfb02-110">**Resubscribe to alerts:** A user can resubscribe to all SMS alerts for all action groups, or a singular action group.</span></span>  
- <span data-ttu-id="dfb02-111">**Request help:** A user can ask for more information on the SMS.</span><span class="sxs-lookup"><span data-stu-id="dfb02-111">**Request help:** A user can ask for more information on the SMS.</span></span> <span data-ttu-id="dfb02-112">They will be redirected to this article</span><span class="sxs-lookup"><span data-stu-id="dfb02-112">They will be redirected to this article</span></span>

<span data-ttu-id="dfb02-113">This article covers the behavior of the SMS alerts and the response actions the user can take based on the locale of the user:</span><span class="sxs-lookup"><span data-stu-id="dfb02-113">This article covers the behavior of the SMS alerts and the response actions the user can take based on the locale of the user:</span></span>

## <a name="usacanada-sms-behavior"></a><span data-ttu-id="dfb02-114">USA/Canada SMS behavior</span><span class="sxs-lookup"><span data-stu-id="dfb02-114">USA/Canada SMS behavior</span></span>
### <a name="receiving-an-sms-alert"></a><span data-ttu-id="dfb02-115">Receiving an SMS Alert</span><span class="sxs-lookup"><span data-stu-id="dfb02-115">Receiving an SMS Alert</span></span>
<span data-ttu-id="dfb02-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span><span class="sxs-lookup"><span data-stu-id="dfb02-116">An SMS receiver, who is configured as part of an action group, will receive an SMS when an alert fires.</span></span> <span data-ttu-id="dfb02-117">The SMS will carry the following information:</span><span class="sxs-lookup"><span data-stu-id="dfb02-117">The SMS will carry the following information:</span></span>
* <span data-ttu-id="dfb02-118">Shortname of the action group this alert was sent to</span><span class="sxs-lookup"><span data-stu-id="dfb02-118">Shortname of the action group this alert was sent to</span></span>
- <span data-ttu-id="dfb02-119">Title of the alert</span><span class="sxs-lookup"><span data-stu-id="dfb02-119">Title of the alert</span></span>

### <a name="unsubscribing-from-sms-alerts-for-one-action-group"></a><span data-ttu-id="dfb02-120">Unsubscribing from SMS alerts for one action group</span><span class="sxs-lookup"><span data-stu-id="dfb02-120">Unsubscribing from SMS alerts for one action group</span></span>
<span data-ttu-id="dfb02-121">A user can unsubscribe from SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “DISABLE &lt;Shortname of action group&gt;”.</span><span class="sxs-lookup"><span data-stu-id="dfb02-121">A user can unsubscribe from SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “DISABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="dfb02-122">Ex.</span><span class="sxs-lookup"><span data-stu-id="dfb02-122">Ex.</span></span> <span data-ttu-id="dfb02-123">A user wishing to unsubscribe from alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “DISABLE Azure”</span><span class="sxs-lookup"><span data-stu-id="dfb02-123">A user wishing to unsubscribe from alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “DISABLE Azure”</span></span>

### <a name="unsubscribing-from-sms-alerts-for-all-action-groups"></a><span data-ttu-id="dfb02-124">Unsubscribing from SMS alerts for all action groups</span><span class="sxs-lookup"><span data-stu-id="dfb02-124">Unsubscribing from SMS alerts for all action groups</span></span>
<span data-ttu-id="dfb02-125">A user can unsubscribe from all SMS alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span><span class="sxs-lookup"><span data-stu-id="dfb02-125">A user can unsubscribe from all SMS alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="dfb02-126">STOP</span><span class="sxs-lookup"><span data-stu-id="dfb02-126">STOP</span></span>

<span data-ttu-id="dfb02-127">Ex.</span><span class="sxs-lookup"><span data-stu-id="dfb02-127">Ex.</span></span> <span data-ttu-id="dfb02-128">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “STOP”</span><span class="sxs-lookup"><span data-stu-id="dfb02-128">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “STOP”</span></span>

>[!NOTE]
><span data-ttu-id="dfb02-129">If a user has unsubscribed from SMS alerts, but is then added to a new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span><span class="sxs-lookup"><span data-stu-id="dfb02-129">If a user has unsubscribed from SMS alerts, but is then added to a new action group; they WILL receive SMS alerts for that new action group, but remain unsubscribed from all previous action groups.</span></span>
>
>

### <a name="resubscribing-to-sms-alerts-for-one-action-group"></a><span data-ttu-id="dfb02-130">Resubscribing to SMS alerts for one action group</span><span class="sxs-lookup"><span data-stu-id="dfb02-130">Resubscribing to SMS alerts for one action group</span></span>
<span data-ttu-id="dfb02-131">A user can resubscribe to SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “ENABLE &lt;Shortname of action group&gt;”.</span><span class="sxs-lookup"><span data-stu-id="dfb02-131">A user can resubscribe to SMS for alerts for one action group by responding to the shortcode 20873 with the keywords: “ENABLE &lt;Shortname of action group&gt;”.</span></span>

<span data-ttu-id="dfb02-132">Ex.</span><span class="sxs-lookup"><span data-stu-id="dfb02-132">Ex.</span></span> <span data-ttu-id="dfb02-133">A user wishing to resubscribe to alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “ENABLE Azure”</span><span class="sxs-lookup"><span data-stu-id="dfb02-133">A user wishing to resubscribe to alerts for an action group with the shortname “Azure”, would send an SMS to the shortcode 20873 that says “ENABLE Azure”</span></span>

### <a name="resubscribing-to-sms-alerts-for-all-action-groups"></a><span data-ttu-id="dfb02-134">Resubscribing to SMS alerts for all action groups</span><span class="sxs-lookup"><span data-stu-id="dfb02-134">Resubscribing to SMS alerts for all action groups</span></span>
<span data-ttu-id="dfb02-135">A user can resubscribe to all SMS for alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span><span class="sxs-lookup"><span data-stu-id="dfb02-135">A user can resubscribe to all SMS for alerts for all action groups by responding to the shortcode 20873 with any of the following keywords:</span></span>

* <span data-ttu-id="dfb02-136">START</span><span class="sxs-lookup"><span data-stu-id="dfb02-136">START</span></span>

<span data-ttu-id="dfb02-137">Ex.</span><span class="sxs-lookup"><span data-stu-id="dfb02-137">Ex.</span></span> <span data-ttu-id="dfb02-138">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “START”</span><span class="sxs-lookup"><span data-stu-id="dfb02-138">A user wishing to unsubscribe from all SMS alerts for all action groups, would send an SMS to the shortcode 20873 that says “START”</span></span>

### <a name="requesting-help-via-sms"></a><span data-ttu-id="dfb02-139">Requesting help via SMS</span><span class="sxs-lookup"><span data-stu-id="dfb02-139">Requesting help via SMS</span></span>
<span data-ttu-id="dfb02-140">A user can ask for more information about the SMS they have received by responding to the shortcode 20873 with any of the following keywords:</span><span class="sxs-lookup"><span data-stu-id="dfb02-140">A user can ask for more information about the SMS they have received by responding to the shortcode 20873 with any of the following keywords:</span></span>
* <span data-ttu-id="dfb02-141">HELP</span><span class="sxs-lookup"><span data-stu-id="dfb02-141">HELP</span></span>

<span data-ttu-id="dfb02-142">A response will be sent to the user with a link to this article.</span><span class="sxs-lookup"><span data-stu-id="dfb02-142">A response will be sent to the user with a link to this article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dfb02-143">Next Steps</span><span class="sxs-lookup"><span data-stu-id="dfb02-143">Next Steps</span></span>
<span data-ttu-id="dfb02-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span><span class="sxs-lookup"><span data-stu-id="dfb02-144">Get an [overview of activity log alerts](monitoring-overview-alerts.md) and learn how to get alerted</span></span>  
<span data-ttu-id="dfb02-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span><span class="sxs-lookup"><span data-stu-id="dfb02-145">Learn more about [SMS rate limiting](monitoring-alerts-rate-limiting.md)</span></span>  
<span data-ttu-id="dfb02-146">Learn more about [action groups](monitoring-action-groups.md)</span><span class="sxs-lookup"><span data-stu-id="dfb02-146">Learn more about [action groups](monitoring-action-groups.md)</span></span>
