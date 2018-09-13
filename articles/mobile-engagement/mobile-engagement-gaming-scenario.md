---
title: Azure Mobile Engagement implementation for Gaming App
description: Gaming app scenario to implement Azure Mobile Engagement
services: mobile-engagement
documentationcenter: mobile
author: piyushjo
manager: erikre
editor: ''
ms.assetid: 2cafc044-4902-4058-8037-49399bf6bf7f
ms.service: mobile-engagement
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: mobile-multiple
ms.workload: mobile
ms.date: 08/19/2016
ms.author: piyushjo
ms.openlocfilehash: 3798a31aa6343d2cecbe61a81c0f01d742ce2334
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671432"
---
# <a name="implement-mobile-engagement-with-gaming-app"></a><span data-ttu-id="ff803-103">Implement Mobile Engagement with Gaming App</span><span class="sxs-lookup"><span data-stu-id="ff803-103">Implement Mobile Engagement with Gaming App</span></span>
## <a name="overview"></a><span data-ttu-id="ff803-104">Overview</span><span class="sxs-lookup"><span data-stu-id="ff803-104">Overview</span></span>
<span data-ttu-id="ff803-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span><span class="sxs-lookup"><span data-stu-id="ff803-105">A gaming start-up has launched a new fishing based role-play/strategy game app.</span></span> <span data-ttu-id="ff803-106">The game has been up and running for 6 months.</span><span class="sxs-lookup"><span data-stu-id="ff803-106">The game has been up and running for 6 months.</span></span> <span data-ttu-id="ff803-107">This game is a huge success, and it has millions of downloads and the retention is very high compared to other start-up game apps.</span><span class="sxs-lookup"><span data-stu-id="ff803-107">This game is a huge success, and it has millions of downloads and the retention is very high compared to other start-up game apps.</span></span> <span data-ttu-id="ff803-108">At the quarterly review meeting, stakeholders agree they need to increase average revenue per user (ARPU).</span><span class="sxs-lookup"><span data-stu-id="ff803-108">At the quarterly review meeting, stakeholders agree they need to increase average revenue per user (ARPU).</span></span> <span data-ttu-id="ff803-109">Premium in-game packages are available as special offers.</span><span class="sxs-lookup"><span data-stu-id="ff803-109">Premium in-game packages are available as special offers.</span></span> <span data-ttu-id="ff803-110">These game packs allow users to upgrade the appearance and performance of their fishing lines and lures or tackles in the game.</span><span class="sxs-lookup"><span data-stu-id="ff803-110">These game packs allow users to upgrade the appearance and performance of their fishing lines and lures or tackles in the game.</span></span> <span data-ttu-id="ff803-111">However, package sales are very low.</span><span class="sxs-lookup"><span data-stu-id="ff803-111">However, package sales are very low.</span></span> <span data-ttu-id="ff803-112">So they decide first to analyze the customer experience with an analytics tool, and then to develop an engagement program to increase sales using advanced segmentation.</span><span class="sxs-lookup"><span data-stu-id="ff803-112">So they decide first to analyze the customer experience with an analytics tool, and then to develop an engagement program to increase sales using advanced segmentation.</span></span>

<span data-ttu-id="ff803-113">Based on the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span><span class="sxs-lookup"><span data-stu-id="ff803-113">Based on the [Azure Mobile Engagement - Getting Started Guide with Best practices](mobile-engagement-getting-started-best-practices.md) they build an engagement strategy.</span></span>

## <a name="objectives-and-kpis"></a><span data-ttu-id="ff803-114">Objectives and KPIs</span><span class="sxs-lookup"><span data-stu-id="ff803-114">Objectives and KPIs</span></span>
<span data-ttu-id="ff803-115">Key stakeholders for the game meet.</span><span class="sxs-lookup"><span data-stu-id="ff803-115">Key stakeholders for the game meet.</span></span> <span data-ttu-id="ff803-116">All agree on one main objective - to increase premium package sales by 15%.</span><span class="sxs-lookup"><span data-stu-id="ff803-116">All agree on one main objective - to increase premium package sales by 15%.</span></span> <span data-ttu-id="ff803-117">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span><span class="sxs-lookup"><span data-stu-id="ff803-117">They create Business Key Performance Indicators (KPIs) to measure and drive this objective</span></span>

* <span data-ttu-id="ff803-118">On which level of the game are these packages purchased?</span><span class="sxs-lookup"><span data-stu-id="ff803-118">On which level of the game are these packages purchased?</span></span>
* <span data-ttu-id="ff803-119">What is the revenue per user, per session, per week, and per month?</span><span class="sxs-lookup"><span data-stu-id="ff803-119">What is the revenue per user, per session, per week, and per month?</span></span>
* <span data-ttu-id="ff803-120">What are the favorite purchase types?</span><span class="sxs-lookup"><span data-stu-id="ff803-120">What are the favorite purchase types?</span></span>

<span data-ttu-id="ff803-121">Part 1 of the [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how to define the objectives and KPIs.</span><span class="sxs-lookup"><span data-stu-id="ff803-121">Part 1 of the [Getting Started Guide](mobile-engagement-getting-started-best-practices.md) explains how to define the objectives and KPIs.</span></span> 

<span data-ttu-id="ff803-122">With the Business KPIs now defined, the Mobile Product Manager creates Engagement KPIs to determine new user trends and retention.</span><span class="sxs-lookup"><span data-stu-id="ff803-122">With the Business KPIs now defined, the Mobile Product Manager creates Engagement KPIs to determine new user trends and retention.</span></span>

* <span data-ttu-id="ff803-123">Monitor retention and use across the following intervals: daily, every 2 days, weekly, monthly and every 3 months</span><span class="sxs-lookup"><span data-stu-id="ff803-123">Monitor retention and use across the following intervals: daily, every 2 days, weekly, monthly and every 3 months</span></span>
* <span data-ttu-id="ff803-124">Active user counts</span><span class="sxs-lookup"><span data-stu-id="ff803-124">Active user counts</span></span>
* <span data-ttu-id="ff803-125">The app rating in the store</span><span class="sxs-lookup"><span data-stu-id="ff803-125">The app rating in the store</span></span>

<span data-ttu-id="ff803-126">Based on recommendations from the IT team, the following technical KPIs were added to answer the following questions:</span><span class="sxs-lookup"><span data-stu-id="ff803-126">Based on recommendations from the IT team, the following technical KPIs were added to answer the following questions:</span></span>

* <span data-ttu-id="ff803-127">What is my user path (which page is visited, how much time users spend on it)</span><span class="sxs-lookup"><span data-stu-id="ff803-127">What is my user path (which page is visited, how much time users spend on it)</span></span>
* <span data-ttu-id="ff803-128">Number of crashes or bugs encountered per session</span><span class="sxs-lookup"><span data-stu-id="ff803-128">Number of crashes or bugs encountered per session</span></span>
* <span data-ttu-id="ff803-129">What OS versions are my users running?</span><span class="sxs-lookup"><span data-stu-id="ff803-129">What OS versions are my users running?</span></span>
* <span data-ttu-id="ff803-130">What is the average size of screen for my users?</span><span class="sxs-lookup"><span data-stu-id="ff803-130">What is the average size of screen for my users?</span></span>
* <span data-ttu-id="ff803-131">What kind of internet connectivity do my users have?</span><span class="sxs-lookup"><span data-stu-id="ff803-131">What kind of internet connectivity do my users have?</span></span>

<span data-ttu-id="ff803-132">For each KPI the Mobile Product Manager specifies the data she needs and where it is located in her playbook.</span><span class="sxs-lookup"><span data-stu-id="ff803-132">For each KPI the Mobile Product Manager specifies the data she needs and where it is located in her playbook.</span></span>

## <a name="engagement-program-and-integration"></a><span data-ttu-id="ff803-133">Engagement program and integration</span><span class="sxs-lookup"><span data-stu-id="ff803-133">Engagement program and integration</span></span>
<span data-ttu-id="ff803-134">Before building an advanced engagement program, the Mobile Project Director in charge of the project should have a deep understanding of how and when products are consumed by the users.</span><span class="sxs-lookup"><span data-stu-id="ff803-134">Before building an advanced engagement program, the Mobile Project Director in charge of the project should have a deep understanding of how and when products are consumed by the users.</span></span>

<span data-ttu-id="ff803-135">After 3 months, the Mobile Project Director has collected enough data to enhance his in-app push notification sales.</span><span class="sxs-lookup"><span data-stu-id="ff803-135">After 3 months, the Mobile Project Director has collected enough data to enhance his in-app push notification sales.</span></span> <span data-ttu-id="ff803-136">He learns that:</span><span class="sxs-lookup"><span data-stu-id="ff803-136">He learns that:</span></span>

* <span data-ttu-id="ff803-137">The first purchase generally happens at the level 14.</span><span class="sxs-lookup"><span data-stu-id="ff803-137">The first purchase generally happens at the level 14.</span></span> <span data-ttu-id="ff803-138">For 90% of those cases, the purchase is new legendary weapons for $3.</span><span class="sxs-lookup"><span data-stu-id="ff803-138">For 90% of those cases, the purchase is new legendary weapons for $3.</span></span>
* <span data-ttu-id="ff803-139">In 80 % of those cases, users who have made a purchase, continue with the product and make more purchases.</span><span class="sxs-lookup"><span data-stu-id="ff803-139">In 80 % of those cases, users who have made a purchase, continue with the product and make more purchases.</span></span>
* <span data-ttu-id="ff803-140">Users who have passed the level 20, start to spend more than $10/week.</span><span class="sxs-lookup"><span data-stu-id="ff803-140">Users who have passed the level 20, start to spend more than $10/week.</span></span>
* <span data-ttu-id="ff803-141">Users tend to buy premium packages at level 16, 24 and 32.</span><span class="sxs-lookup"><span data-stu-id="ff803-141">Users tend to buy premium packages at level 16, 24 and 32.</span></span>

<span data-ttu-id="ff803-142">Thanks to this analysis the Mobile Project Director decides to create specific push notification sequences to increase in app sales.</span><span class="sxs-lookup"><span data-stu-id="ff803-142">Thanks to this analysis the Mobile Project Director decides to create specific push notification sequences to increase in app sales.</span></span> <span data-ttu-id="ff803-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span><span class="sxs-lookup"><span data-stu-id="ff803-143">He creates three push sequences which he calls: Welcome program, Sales Program, and Inactive Program.</span></span> <span data-ttu-id="ff803-144">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span><span class="sxs-lookup"><span data-stu-id="ff803-144">For more information refer to the [Playbooks](https://github.com/Azure/azure-mobile-engagement-samples/tree/master/Playbooks) ![][1]</span></span>

<!--Image references-->

[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/mobile-engagement/media/mobile-engagement-game-scenario/notification-scenario.png

<!--Link references-->

