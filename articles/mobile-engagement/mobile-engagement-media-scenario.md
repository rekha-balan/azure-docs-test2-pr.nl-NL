---
title: Azure Mobile Engagement implementation for Media App
description: Media app scenario to implement Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 48201cc8-4e04-485c-a8dc-d6406d23f3ed
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: b775452cc6da787bb9096dfce43481417c43ef59
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556594"
---
# <a name="implement-mobile-engagement-with-media-app"></a><span data-ttu-id="1ba3f-103">Implement Mobile Engagement with Media App</span><span class="sxs-lookup"><span data-stu-id="1ba3f-103">Implement Mobile Engagement with Media App</span></span>
## <a name="overview"></a><span data-ttu-id="1ba3f-104">Overview</span><span class="sxs-lookup"><span data-stu-id="1ba3f-104">Overview</span></span>
<span data-ttu-id="1ba3f-105">John is a mobile project manager for a big media company.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-105">John is a mobile project manager for a big media company.</span></span> <span data-ttu-id="1ba3f-106">He recently launched a new app that has a very high download count.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-106">He recently launched a new app that has a very high download count.</span></span> <span data-ttu-id="1ba3f-107">He has hit his goals for download but, still his Return On Investment(ROI) per user does not meet his requirements.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-107">He has hit his goals for download but, still his Return On Investment(ROI) per user does not meet his requirements.</span></span> 

<span data-ttu-id="1ba3f-108">John has already identified why his ROI is too low.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-108">John has already identified why his ROI is too low.</span></span> <span data-ttu-id="1ba3f-109">Users frequently stop using his app after only 2 weeks and most of them never come back.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-109">Users frequently stop using his app after only 2 weeks and most of them never come back.</span></span> <span data-ttu-id="1ba3f-110">He wants to increase the retention of his app.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-110">He wants to increase the retention of his app.</span></span>

<span data-ttu-id="1ba3f-111">After some initial testing, he has learned when he engages his users with push notifications, they tend to continue using his app.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-111">After some initial testing, he has learned when he engages his users with push notifications, they tend to continue using his app.</span></span> <span data-ttu-id="1ba3f-112">Also users that were inactive will often return to the app depending on notifications he sends them.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-112">Also users that were inactive will often return to the app depending on notifications he sends them.</span></span> <span data-ttu-id="1ba3f-113">John decides to invest in some kind of Engagement Program for his app which uses advanced targeting with push notifications.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-113">John decides to invest in some kind of Engagement Program for his app which uses advanced targeting with push notifications.</span></span>

<span data-ttu-id="1ba3f-114">John has recently read the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) and has decided to implement the recommendations from the guide.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-114">John has recently read the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) and has decided to implement the recommendations from the guide.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="1ba3f-115">Objectives and KPIs</span><span class="sxs-lookup"><span data-stu-id="1ba3f-115">Objectives and KPIs</span></span>
<span data-ttu-id="1ba3f-116">Key stakeholders for John's app meet.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-116">Key stakeholders for John's app meet.</span></span> <span data-ttu-id="1ba3f-117">Business is generated from ads as users consume his media.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-117">Business is generated from ads as users consume his media.</span></span> <span data-ttu-id="1ba3f-118">By increasing content consumed per user, John increases his revenues.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-118">By increasing content consumed per user, John increases his revenues.</span></span> <span data-ttu-id="1ba3f-119">All agree on one main objective: To increase sales from ads by 25%.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-119">All agree on one main objective: To increase sales from ads by 25%.</span></span> <span data-ttu-id="1ba3f-120">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span><span class="sxs-lookup"><span data-stu-id="1ba3f-120">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="1ba3f-121">Number of ads clicked per user</span><span class="sxs-lookup"><span data-stu-id="1ba3f-121">Number of ads clicked per user</span></span>
* <span data-ttu-id="1ba3f-122">How many article pages visited (per user/ per session/ per week / per month…)</span><span class="sxs-lookup"><span data-stu-id="1ba3f-122">How many article pages visited (per user/ per session/ per week / per month…)</span></span>
* <span data-ttu-id="1ba3f-123">What are favorite categories</span><span class="sxs-lookup"><span data-stu-id="1ba3f-123">What are favorite categories</span></span>

<span data-ttu-id="1ba3f-124">Based on John's meeting with key stakeholders he has defined his Business KPIs.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-124">Based on John's meeting with key stakeholders he has defined his Business KPIs.</span></span> <span data-ttu-id="1ba3f-125">He follows Part 1 of the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="1ba3f-125">He follows Part 1 of the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md).</span></span> 

<span data-ttu-id="1ba3f-126">Next, he creates the following Engagement KPIs to ensure that objectives are reached:</span><span class="sxs-lookup"><span data-stu-id="1ba3f-126">Next, he creates the following Engagement KPIs to ensure that objectives are reached:</span></span>

* <span data-ttu-id="1ba3f-127">Monitor retention across the following intervals: daily, weekly, bi-weekly and monthly.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-127">Monitor retention across the following intervals: daily, weekly, bi-weekly and monthly.</span></span>
* <span data-ttu-id="1ba3f-128">Active users counts</span><span class="sxs-lookup"><span data-stu-id="1ba3f-128">Active users counts</span></span>
* <span data-ttu-id="1ba3f-129">The app rating in the app stores</span><span class="sxs-lookup"><span data-stu-id="1ba3f-129">The app rating in the app stores</span></span>

<span data-ttu-id="1ba3f-130">Based on recommendations from the IT team, the following Technical KPIs were added to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="1ba3f-130">Based on recommendations from the IT team, the following Technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="1ba3f-131">What is my user path (which page is visited, how many time users spend on it)</span><span class="sxs-lookup"><span data-stu-id="1ba3f-131">What is my user path (which page is visited, how many time users spend on it)</span></span>
* <span data-ttu-id="1ba3f-132">Number of crashes or bugs encountered per session?</span><span class="sxs-lookup"><span data-stu-id="1ba3f-132">Number of crashes or bugs encountered per session?</span></span>
* <span data-ttu-id="1ba3f-133">What OS versions are my users running?</span><span class="sxs-lookup"><span data-stu-id="1ba3f-133">What OS versions are my users running?</span></span>
* <span data-ttu-id="1ba3f-134">What is the average size of screen for my users?</span><span class="sxs-lookup"><span data-stu-id="1ba3f-134">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="1ba3f-135">What kind of internet connections do my users have?</span><span class="sxs-lookup"><span data-stu-id="1ba3f-135">What kind of internet connections do my users have?</span></span>

<span data-ttu-id="1ba3f-136">For each KPI, he classifies the data required and he records it in the proper location of his playbook.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-136">For each KPI, he classifies the data required and he records it in the proper location of his playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="1ba3f-137">Engagement program and integration</span><span class="sxs-lookup"><span data-stu-id="1ba3f-137">Engagement program and integration</span></span>
<span data-ttu-id="1ba3f-138">Now that John has finished defining his KPIs, he starts his Engagement strategy phase by defining 4 engagement programs and their objectives: ![][1]</span><span class="sxs-lookup"><span data-stu-id="1ba3f-138">Now that John has finished defining his KPIs, he starts his Engagement strategy phase by defining 4 engagement programs and their objectives: ![][1]</span></span>

<span data-ttu-id="1ba3f-139">Then John goes deeper by detailing push notifications for each program.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-139">Then John goes deeper by detailing push notifications for each program.</span></span> <span data-ttu-id="1ba3f-140">Push notification are defined by five elements:</span><span class="sxs-lookup"><span data-stu-id="1ba3f-140">Push notification are defined by five elements:</span></span>

1. <span data-ttu-id="1ba3f-141">Objective: what is the objective of the notification</span><span class="sxs-lookup"><span data-stu-id="1ba3f-141">Objective: what is the objective of the notification</span></span>
2. <span data-ttu-id="1ba3f-142">How the objective will be reached</span><span class="sxs-lookup"><span data-stu-id="1ba3f-142">How the objective will be reached</span></span>
3. <span data-ttu-id="1ba3f-143">Target: who will receive the notification?</span><span class="sxs-lookup"><span data-stu-id="1ba3f-143">Target: who will receive the notification?</span></span>
4. <span data-ttu-id="1ba3f-144">Content: What is the wording and the format of the notification (In App/Out of App)</span><span class="sxs-lookup"><span data-stu-id="1ba3f-144">Content: What is the wording and the format of the notification (In App/Out of App)</span></span>
5. <span data-ttu-id="1ba3f-145">When: what is the best moment to send this push notification</span><span class="sxs-lookup"><span data-stu-id="1ba3f-145">When: what is the best moment to send this push notification</span></span>
   
    ![][2]

<span data-ttu-id="1ba3f-146">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).</span><span class="sxs-lookup"><span data-stu-id="1ba3f-146">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks).</span></span>

<span data-ttu-id="1ba3f-147">According to the part 2 of the white paper John uses target section to define what data he has to collect and writes his Tag Plan jointly with IT team to implement the solution.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-147">According to the part 2 of the white paper John uses target section to define what data he has to collect and writes his Tag Plan jointly with IT team to implement the solution.</span></span> <span data-ttu-id="1ba3f-148">After 1 week of implementation and user acceptance testing, John can finally launch his programs.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-148">After 1 week of implementation and user acceptance testing, John can finally launch his programs.</span></span>

## <a name="program-results"></a><span data-ttu-id="1ba3f-149">Program Results</span><span class="sxs-lookup"><span data-stu-id="1ba3f-149">Program Results</span></span>
<span data-ttu-id="1ba3f-150">4 months later, John reviews performances of programs.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-150">4 months later, John reviews performances of programs.</span></span> <span data-ttu-id="1ba3f-151">The Welcome Program and the Weekly Program are meeting his goals.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-151">The Welcome Program and the Weekly Program are meeting his goals.</span></span> <span data-ttu-id="1ba3f-152">The number of user with only one session decreases, more features of the app are being used and the number of connections per week has doubled.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-152">The number of user with only one session decreases, more features of the app are being used and the number of connections per week has doubled.</span></span>

<span data-ttu-id="1ba3f-153">The **Inactive Program** is helping John understand user tendencies.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-153">The **Inactive Program** is helping John understand user tendencies.</span></span> <span data-ttu-id="1ba3f-154">It appears that 15% of the inactive users come back to the app.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-154">It appears that 15% of the inactive users come back to the app.</span></span> <span data-ttu-id="1ba3f-155">However most of them don’t stay active more than 1 month.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-155">However most of them don’t stay active more than 1 month.</span></span> <span data-ttu-id="1ba3f-156">John foresees a potential optimization of this sequence with additional notifications and expanding his content choices.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-156">John foresees a potential optimization of this sequence with additional notifications and expanding his content choices.</span></span>

<span data-ttu-id="1ba3f-157">The **Discover Program** doesn’t work well.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-157">The **Discover Program** doesn’t work well.</span></span> <span data-ttu-id="1ba3f-158">It increases cross selling but not enough to reach his objectives.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-158">It increases cross selling but not enough to reach his objectives.</span></span> <span data-ttu-id="1ba3f-159">John identifies that he doesn’t have enough data to make relevant targeting and propose appropriate content.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-159">John identifies that he doesn’t have enough data to make relevant targeting and propose appropriate content.</span></span> <span data-ttu-id="1ba3f-160">He stops this program and focuses on sending “editorial push notifications” with Azure Mobile Engagement.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-160">He stops this program and focuses on sending “editorial push notifications” with Azure Mobile Engagement.</span></span> <span data-ttu-id="1ba3f-161">His journalists already have a CMS solution to send push notifications and they don’t want to change.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-161">His journalists already have a CMS solution to send push notifications and they don’t want to change.</span></span>

<span data-ttu-id="1ba3f-162">John decides to use the Reach API which is an HTTP REST API that allows managing Reach campaigns without having to use AZME Web interface.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-162">John decides to use the Reach API which is an HTTP REST API that allows managing Reach campaigns without having to use AZME Web interface.</span></span> <span data-ttu-id="1ba3f-163">With this approach John can collect the data he needs and allow his writers to keep using the CMS solution.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-163">With this approach John can collect the data he needs and allow his writers to keep using the CMS solution.</span></span>

<span data-ttu-id="1ba3f-164">To ensure that feature works correctly, John asks IT team to be vigilant on the following points:</span><span class="sxs-lookup"><span data-stu-id="1ba3f-164">To ensure that feature works correctly, John asks IT team to be vigilant on the following points:</span></span>

1. <span data-ttu-id="1ba3f-165">**Operation Systems** : They all have their own rules to administrate push notifications, so John decides to list all cases and checks if the APIs handle it.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-165">**Operation Systems** : They all have their own rules to administrate push notifications, so John decides to list all cases and checks if the APIs handle it.</span></span>
   <span data-ttu-id="1ba3f-166">E.g : Android push system allows big picture which is not the case with iOS.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-166">E.g : Android push system allows big picture which is not the case with iOS.</span></span>
2. <span data-ttu-id="1ba3f-167">**Time frame**: John wants an API, which set the time frame and set an end to campaigns.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-167">**Time frame**: John wants an API, which set the time frame and set an end to campaigns.</span></span> <span data-ttu-id="1ba3f-168">He wants to preserve users from any disruptive notification bombing.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-168">He wants to preserve users from any disruptive notification bombing.</span></span>
3. <span data-ttu-id="1ba3f-169">**Categories**: Marketing team prepares template for each type of alerting.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-169">**Categories**: Marketing team prepares template for each type of alerting.</span></span> <span data-ttu-id="1ba3f-170">John asks IT team to set categories inside the API.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-170">John asks IT team to set categories inside the API.</span></span>

<span data-ttu-id="1ba3f-171">After some tests John is satisfied.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-171">After some tests John is satisfied.</span></span> <span data-ttu-id="1ba3f-172">Thanks to this API, journalists can still send push notifications with their CMS and Azure Mobile Engagement collects all behavioral data for them</span><span class="sxs-lookup"><span data-stu-id="1ba3f-172">Thanks to this API, journalists can still send push notifications with their CMS and Azure Mobile Engagement collects all behavioral data for them</span></span>

<span data-ttu-id="1ba3f-173">After these 4 first months, results reflect a good overall performance and gives confidence for John and his board, ROI per user increases per 15% and mobile sales represent 17.5 % of total sales, an increase of 7.5% in only four months.</span><span class="sxs-lookup"><span data-stu-id="1ba3f-173">After these 4 first months, results reflect a good overall performance and gives confidence for John and his board, ROI per user increases per 15% and mobile sales represent 17.5 % of total sales, an increase of 7.5% in only four months.</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-media-scenario/engagement-strategy.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-media-scenario/push-scenarios.png

<!--Link references-->
[Media Playbook link]: https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks


