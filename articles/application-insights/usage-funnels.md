---
title: Azure Application Insights Funnels
description: Learn how you can use Funnels to discover how customers are interacting with your application.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: conceptual
ms.date: 07/17/2017
ms.author: mbullwin
ms.openlocfilehash: 8478106fd68f6fcc65dff832b5cb27ca8db5f5bd
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870669"
---
# <a name="discover-how-customers-are-using-your-application-with-application-insights-funnels"></a><span data-ttu-id="af5c9-103">Discover how customers are using your application with Application Insights Funnels</span><span class="sxs-lookup"><span data-stu-id="af5c9-103">Discover how customers are using your application with Application Insights Funnels</span></span>

<span data-ttu-id="af5c9-104">Understanding the customer experience is of the utmost importance to your business.</span><span class="sxs-lookup"><span data-stu-id="af5c9-104">Understanding the customer experience is of the utmost importance to your business.</span></span> <span data-ttu-id="af5c9-105">If your application involves multiple stages, you need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span><span class="sxs-lookup"><span data-stu-id="af5c9-105">If your application involves multiple stages, you need to know if most customers are progressing through the entire process, or if they are ending the process at some point.</span></span> <span data-ttu-id="af5c9-106">The progression through a series of steps in a web application is known as a *funnel*.</span><span class="sxs-lookup"><span data-stu-id="af5c9-106">The progression through a series of steps in a web application is known as a *funnel*.</span></span> <span data-ttu-id="af5c9-107">You can use Azure Application Insights Funnels to gain insights into your users, and monitor step-by-step conversion rates.</span><span class="sxs-lookup"><span data-stu-id="af5c9-107">You can use Azure Application Insights Funnels to gain insights into your users, and monitor step-by-step conversion rates.</span></span> 

## <a name="create-your-funnel"></a><span data-ttu-id="af5c9-108">Create your funnel</span><span class="sxs-lookup"><span data-stu-id="af5c9-108">Create your funnel</span></span>
<span data-ttu-id="af5c9-109">Before you create your funnel, decide on the question you want to answer.</span><span class="sxs-lookup"><span data-stu-id="af5c9-109">Before you create your funnel, decide on the question you want to answer.</span></span> <span data-ttu-id="af5c9-110">For example, you might want to know how many users are viewing the home page, viewing a customer profile, and creating a ticket.</span><span class="sxs-lookup"><span data-stu-id="af5c9-110">For example, you might want to know how many users are viewing the home page, viewing a customer profile, and creating a ticket.</span></span> <span data-ttu-id="af5c9-111">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who successfully create a customer ticket.</span><span class="sxs-lookup"><span data-stu-id="af5c9-111">In this example, the owners of the Fabrikam Fiber company want to know the percentage of customers who successfully create a customer ticket.</span></span>

<span data-ttu-id="af5c9-112">Here are the steps they take to create their funnel.</span><span class="sxs-lookup"><span data-stu-id="af5c9-112">Here are the steps they take to create their funnel.</span></span>

1. <span data-ttu-id="af5c9-113">In the Application Insights Funnels tool, select **New**.</span><span class="sxs-lookup"><span data-stu-id="af5c9-113">In the Application Insights Funnels tool, select **New**.</span></span>
1. <span data-ttu-id="af5c9-114">From the **Time Range** drop-down menu, select **Last 90 days**.</span><span class="sxs-lookup"><span data-stu-id="af5c9-114">From the **Time Range** drop-down menu, select **Last 90 days**.</span></span> <span data-ttu-id="af5c9-115">Select either **My funnels** or **Shared funnels**.</span><span class="sxs-lookup"><span data-stu-id="af5c9-115">Select either **My funnels** or **Shared funnels**.</span></span>
1. <span data-ttu-id="af5c9-116">From the **Step 1** drop-down list, select **Index**.</span><span class="sxs-lookup"><span data-stu-id="af5c9-116">From the **Step 1** drop-down list, select **Index**.</span></span> 
1. <span data-ttu-id="af5c9-117">From the **Step 2** list, select **Customer**.</span><span class="sxs-lookup"><span data-stu-id="af5c9-117">From the **Step 2** list, select **Customer**.</span></span>
1. <span data-ttu-id="af5c9-118">From the **Step 3** list, select **Create**.</span><span class="sxs-lookup"><span data-stu-id="af5c9-118">From the **Step 3** list, select **Create**.</span></span>
1. <span data-ttu-id="af5c9-119">Add a name to the funnel, and select **Save**.</span><span class="sxs-lookup"><span data-stu-id="af5c9-119">Add a name to the funnel, and select **Save**.</span></span>

<span data-ttu-id="af5c9-120">The following screenshot shows an example of the kind of data the Funnels tool generates.</span><span class="sxs-lookup"><span data-stu-id="af5c9-120">The following screenshot shows an example of the kind of data the Funnels tool generates.</span></span> <span data-ttu-id="af5c9-121">The Fabrikam owners can see that during the last 90 days, 54.3 percent of their customers who visited the home page created a customer ticket.</span><span class="sxs-lookup"><span data-stu-id="af5c9-121">The Fabrikam owners can see that during the last 90 days, 54.3 percent of their customers who visited the home page created a customer ticket.</span></span> <span data-ttu-id="af5c9-122">They can also see that 2,700 of their customers came to the index from the home page.</span><span class="sxs-lookup"><span data-stu-id="af5c9-122">They can also see that 2,700 of their customers came to the index from the home page.</span></span> <span data-ttu-id="af5c9-123">This might indicate a refresh issue.</span><span class="sxs-lookup"><span data-stu-id="af5c9-123">This might indicate a refresh issue.</span></span>


![Screenshot of Funnels tool with data](./media/app-insights-understand-usage-patterns/funnel1.png)

### <a name="funnels-features"></a><span data-ttu-id="af5c9-125">Funnels features</span><span class="sxs-lookup"><span data-stu-id="af5c9-125">Funnels features</span></span>
<span data-ttu-id="af5c9-126">The preceding screenshot includes five highlighted areas.</span><span class="sxs-lookup"><span data-stu-id="af5c9-126">The preceding screenshot includes five highlighted areas.</span></span> <span data-ttu-id="af5c9-127">These are features of Funnels.</span><span class="sxs-lookup"><span data-stu-id="af5c9-127">These are features of Funnels.</span></span> <span data-ttu-id="af5c9-128">The following list explains more about each corresponding area in the screenshot:</span><span class="sxs-lookup"><span data-stu-id="af5c9-128">The following list explains more about each corresponding area in the screenshot:</span></span>
1. <span data-ttu-id="af5c9-129">If your app is sampled, you will see a sampling banner.</span><span class="sxs-lookup"><span data-stu-id="af5c9-129">If your app is sampled, you will see a sampling banner.</span></span> <span data-ttu-id="af5c9-130">Selecting the banner opens a context pane, explaining how to turn sampling off.</span><span class="sxs-lookup"><span data-stu-id="af5c9-130">Selecting the banner opens a context pane, explaining how to turn sampling off.</span></span> 
2. <span data-ttu-id="af5c9-131">You can export your funnel to [Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="af5c9-131">You can export your funnel to [Power BI](app-insights-export-power-bi.md).</span></span>
3. <span data-ttu-id="af5c9-132">Select a step to see more details on the right.</span><span class="sxs-lookup"><span data-stu-id="af5c9-132">Select a step to see more details on the right.</span></span> 
4. <span data-ttu-id="af5c9-133">The historical conversion graph shows the conversion rates over the last 90 days.</span><span class="sxs-lookup"><span data-stu-id="af5c9-133">The historical conversion graph shows the conversion rates over the last 90 days.</span></span> 
5. <span data-ttu-id="af5c9-134">Understand your users better by accessing the users tool.</span><span class="sxs-lookup"><span data-stu-id="af5c9-134">Understand your users better by accessing the users tool.</span></span> <span data-ttu-id="af5c9-135">You can use filters in each step.</span><span class="sxs-lookup"><span data-stu-id="af5c9-135">You can use filters in each step.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="af5c9-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="af5c9-136">Next steps</span></span>
  * [<span data-ttu-id="af5c9-137">Usage overview</span><span class="sxs-lookup"><span data-stu-id="af5c9-137">Usage overview</span></span>](app-insights-usage-overview.md)
  * [<span data-ttu-id="af5c9-138">Users, Sessions, and Events</span><span class="sxs-lookup"><span data-stu-id="af5c9-138">Users, Sessions, and Events</span></span>](app-insights-usage-segmentation.md)
  * [<span data-ttu-id="af5c9-139">Retention</span><span class="sxs-lookup"><span data-stu-id="af5c9-139">Retention</span></span>](app-insights-usage-retention.md)
  * [<span data-ttu-id="af5c9-140">Workbooks</span><span class="sxs-lookup"><span data-stu-id="af5c9-140">Workbooks</span></span>](app-insights-usage-workbooks.md)
  * [<span data-ttu-id="af5c9-141">Add user context</span><span class="sxs-lookup"><span data-stu-id="af5c9-141">Add user context</span></span>](app-insights-usage-send-user-context.md)
  * [<span data-ttu-id="af5c9-142">Export to Power BI</span><span class="sxs-lookup"><span data-stu-id="af5c9-142">Export to Power BI</span></span>](app-insights-export-power-bi.md)

