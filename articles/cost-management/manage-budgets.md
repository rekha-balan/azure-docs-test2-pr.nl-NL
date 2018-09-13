---
title: Manage budgets in Azure Cost Management | Microsoft Docs
description: This article helps you create and manage budgets in Cost Management.
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 06/25/2018
ms.topic: conceptual
ms.service: cost-management
manager: dougeby
ms.custom: ''
ms.openlocfilehash: fac0b80e51b0963f26aaf1b59a81d2203d641c73
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966049"
---
# <a name="manage-budgets"></a><span data-ttu-id="04a10-103">Manage budgets</span><span class="sxs-lookup"><span data-stu-id="04a10-103">Manage budgets</span></span>

<span data-ttu-id="04a10-104">Setting up budgets and budget-based alerts help to improve your cloud governance and accountability.</span><span class="sxs-lookup"><span data-stu-id="04a10-104">Setting up budgets and budget-based alerts help to improve your cloud governance and accountability.</span></span> <span data-ttu-id="04a10-105">This article helps you quickly create budgets and start managing them in Cost Management.</span><span class="sxs-lookup"><span data-stu-id="04a10-105">This article helps you quickly create budgets and start managing them in Cost Management.</span></span>

<span data-ttu-id="04a10-106">When you have an Enterprise or MSP account, you can use your hierarchical cost entity structure to assign monthly budget quotas to different business units, departments, or any other cost entity.</span><span class="sxs-lookup"><span data-stu-id="04a10-106">When you have an Enterprise or MSP account, you can use your hierarchical cost entity structure to assign monthly budget quotas to different business units, departments, or any other cost entity.</span></span> <span data-ttu-id="04a10-107">When you have a Premium account, you can use the budget management functionality, which is then applied to your entire cloud expenditure.</span><span class="sxs-lookup"><span data-stu-id="04a10-107">When you have a Premium account, you can use the budget management functionality, which is then applied to your entire cloud expenditure.</span></span> <span data-ttu-id="04a10-108">All budgets are manually assigned.</span><span class="sxs-lookup"><span data-stu-id="04a10-108">All budgets are manually assigned.</span></span>

<span data-ttu-id="04a10-109">Based on assigned budgets, you can set threshold alerts based on the percentage of your budget that's consumed and define the severity of each threshold.</span><span class="sxs-lookup"><span data-stu-id="04a10-109">Based on assigned budgets, you can set threshold alerts based on the percentage of your budget that's consumed and define the severity of each threshold.</span></span>

<span data-ttu-id="04a10-110">Budget reports show the assigned budget.</span><span class="sxs-lookup"><span data-stu-id="04a10-110">Budget reports show the assigned budget.</span></span> <span data-ttu-id="04a10-111">Users can view when their spending is over, under, or at par with their consumption over time.</span><span class="sxs-lookup"><span data-stu-id="04a10-111">Users can view when their spending is over, under, or at par with their consumption over time.</span></span> <span data-ttu-id="04a10-112">When you select **Show/Hide Fields** at the top of a budget report, you can view cost, budget, accumulated cost, or total budget.</span><span class="sxs-lookup"><span data-stu-id="04a10-112">When you select **Show/Hide Fields** at the top of a budget report, you can view cost, budget, accumulated cost, or total budget.</span></span>

## <a name="create-budgets"></a><span data-ttu-id="04a10-113">Create budgets</span><span class="sxs-lookup"><span data-stu-id="04a10-113">Create budgets</span></span>

<span data-ttu-id="04a10-114">When you create a budget, you set it for your fiscal year and it applies to a specific entity.</span><span class="sxs-lookup"><span data-stu-id="04a10-114">When you create a budget, you set it for your fiscal year and it applies to a specific entity.</span></span>

<span data-ttu-id="04a10-115">To create a budget and assign it to an entity:</span><span class="sxs-lookup"><span data-stu-id="04a10-115">To create a budget and assign it to an entity:</span></span>

1. <span data-ttu-id="04a10-116">Navigate to **Costs** &gt; **Cost Management** &gt; **Budget**.</span><span class="sxs-lookup"><span data-stu-id="04a10-116">Navigate to **Costs** &gt; **Cost Management** &gt; **Budget**.</span></span>
2. <span data-ttu-id="04a10-117">On the Budget Management page, under **Entities**, select the entity where you want to create the budget.</span><span class="sxs-lookup"><span data-stu-id="04a10-117">On the Budget Management page, under **Entities**, select the entity where you want to create the budget.</span></span>
3. <span data-ttu-id="04a10-118">In the budget year, select the year where you want to create the budget.</span><span class="sxs-lookup"><span data-stu-id="04a10-118">In the budget year, select the year where you want to create the budget.</span></span>
4. <span data-ttu-id="04a10-119">For each month, set a budget value.</span><span class="sxs-lookup"><span data-stu-id="04a10-119">For each month, set a budget value.</span></span> <span data-ttu-id="04a10-120">When you're done, click  **Save**.</span><span class="sxs-lookup"><span data-stu-id="04a10-120">When you're done, click  **Save**.</span></span>
<span data-ttu-id="04a10-121">In this example, the monthly budget for June 2018 is set to $135,000.</span><span class="sxs-lookup"><span data-stu-id="04a10-121">In this example, the monthly budget for June 2018 is set to $135,000.</span></span> <span data-ttu-id="04a10-122">The total budget for the year is $1,615,000.00.</span><span class="sxs-lookup"><span data-stu-id="04a10-122">The total budget for the year is $1,615,000.00.</span></span>
<span data-ttu-id="04a10-123">![Create a budget](./media/manage-budgets/set-budget.png)</span><span class="sxs-lookup"><span data-stu-id="04a10-123">![Create a budget](./media/manage-budgets/set-budget.png)</span></span>


<span data-ttu-id="04a10-124">To import a file for the annual budget:</span><span class="sxs-lookup"><span data-stu-id="04a10-124">To import a file for the annual budget:</span></span>

1. <span data-ttu-id="04a10-125">Under **Actions**, select **Export** to download an empty CSV template to use as your basis for the budget.</span><span class="sxs-lookup"><span data-stu-id="04a10-125">Under **Actions**, select **Export** to download an empty CSV template to use as your basis for the budget.</span></span>
2. <span data-ttu-id="04a10-126">Fill in the CSV file with your budget entries and save it locally.</span><span class="sxs-lookup"><span data-stu-id="04a10-126">Fill in the CSV file with your budget entries and save it locally.</span></span>
3. <span data-ttu-id="04a10-127">Under **Actions**, select **Import**.</span><span class="sxs-lookup"><span data-stu-id="04a10-127">Under **Actions**, select **Import**.</span></span>
4. <span data-ttu-id="04a10-128">Select your saved file and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="04a10-128">Select your saved file and then click **OK**.</span></span>

<span data-ttu-id="04a10-129">To export your completed budget as a CSV file, under **Actions**, select **Export** to download the file.</span><span class="sxs-lookup"><span data-stu-id="04a10-129">To export your completed budget as a CSV file, under **Actions**, select **Export** to download the file.</span></span>

## <a name="view-budget-in-reports"></a><span data-ttu-id="04a10-130">View budget in reports</span><span class="sxs-lookup"><span data-stu-id="04a10-130">View budget in reports</span></span>

<span data-ttu-id="04a10-131">When completed, your budget is shown in most Cost reports under **Costs** &gt; **Cost Analysis** and in the Cost vs. Budget Over Time report.</span><span class="sxs-lookup"><span data-stu-id="04a10-131">When completed, your budget is shown in most Cost reports under **Costs** &gt; **Cost Analysis** and in the Cost vs. Budget Over Time report.</span></span> <span data-ttu-id="04a10-132">You can also schedule reports based on budget thresholds using **Actions**.</span><span class="sxs-lookup"><span data-stu-id="04a10-132">You can also schedule reports based on budget thresholds using **Actions**.</span></span>

<span data-ttu-id="04a10-133">Here's an example of the Cost Analysis report.</span><span class="sxs-lookup"><span data-stu-id="04a10-133">Here's an example of the Cost Analysis report.</span></span> <span data-ttu-id="04a10-134">It shows the total budget and cost by workload and usage types since the beginning of the year.</span><span class="sxs-lookup"><span data-stu-id="04a10-134">It shows the total budget and cost by workload and usage types since the beginning of the year.</span></span>

![Example Cost Analysis report with budget](./media/manage-budgets/cost-analysis-budget-example.png)

<span data-ttu-id="04a10-136">In this example, assume the current date is June 22.</span><span class="sxs-lookup"><span data-stu-id="04a10-136">In this example, assume the current date is June 22.</span></span> <span data-ttu-id="04a10-137">The cost for June 2018 is $71,611.28 compared to the monthly budget of $135,000.</span><span class="sxs-lookup"><span data-stu-id="04a10-137">The cost for June 2018 is $71,611.28 compared to the monthly budget of $135,000.</span></span> <span data-ttu-id="04a10-138">The cost is much lower than the monthly budget because there are still eight days of spending before the end of the month.</span><span class="sxs-lookup"><span data-stu-id="04a10-138">The cost is much lower than the monthly budget because there are still eight days of spending before the end of the month.</span></span>

<span data-ttu-id="04a10-139">Another way to view the report is to look at accumulated cost vs your budget.</span><span class="sxs-lookup"><span data-stu-id="04a10-139">Another way to view the report is to look at accumulated cost vs your budget.</span></span> <span data-ttu-id="04a10-140">To see accumulated costs, under **Show/Hide Fields**, select **Accumulated Cost** and **Total Budget**.</span><span class="sxs-lookup"><span data-stu-id="04a10-140">To see accumulated costs, under **Show/Hide Fields**, select **Accumulated Cost** and **Total Budget**.</span></span> <span data-ttu-id="04a10-141">Here's an example showing the accumulated cost since the beginning of the year.</span><span class="sxs-lookup"><span data-stu-id="04a10-141">Here's an example showing the accumulated cost since the beginning of the year.</span></span>

![Accumulated budget](./media/manage-budgets/accumulated-budget.png)

<span data-ttu-id="04a10-143">Sometime in the future your accumulated cost might exceed your budget.</span><span class="sxs-lookup"><span data-stu-id="04a10-143">Sometime in the future your accumulated cost might exceed your budget.</span></span> <span data-ttu-id="04a10-144">You can more easily see that if you change the chart view to the _line_ type.</span><span class="sxs-lookup"><span data-stu-id="04a10-144">You can more easily see that if you change the chart view to the _line_ type.</span></span>

![Budget shown in line chart](./media/manage-budgets/budget-line.png)

## <a name="create-budget-alerts-for-a-filter"></a><span data-ttu-id="04a10-146">Create budget alerts for a filter</span><span class="sxs-lookup"><span data-stu-id="04a10-146">Create budget alerts for a filter</span></span>

<span data-ttu-id="04a10-147">In the previous example, you can see that the accumulated cost approached the budget.</span><span class="sxs-lookup"><span data-stu-id="04a10-147">In the previous example, you can see that the accumulated cost approached the budget.</span></span> <span data-ttu-id="04a10-148">You can create automatic budget alerts so that you're notified when spending approaches or exceeds your budget.</span><span class="sxs-lookup"><span data-stu-id="04a10-148">You can create automatic budget alerts so that you're notified when spending approaches or exceeds your budget.</span></span> <span data-ttu-id="04a10-149">Basically, the alert is a scheduled report with a threshold.</span><span class="sxs-lookup"><span data-stu-id="04a10-149">Basically, the alert is a scheduled report with a threshold.</span></span> <span data-ttu-id="04a10-150">Budget alert threshold metrics include:</span><span class="sxs-lookup"><span data-stu-id="04a10-150">Budget alert threshold metrics include:</span></span>

- <span data-ttu-id="04a10-151">Remaining cost vs. budget – to specify a currency value threshold</span><span class="sxs-lookup"><span data-stu-id="04a10-151">Remaining cost vs. budget – to specify a currency value threshold</span></span>
- <span data-ttu-id="04a10-152">Cost percentage vs. budget – to specify a percentage value threshold</span><span class="sxs-lookup"><span data-stu-id="04a10-152">Cost percentage vs. budget – to specify a percentage value threshold</span></span>

<span data-ttu-id="04a10-153">Let's look at an example.</span><span class="sxs-lookup"><span data-stu-id="04a10-153">Let's look at an example.</span></span>

<span data-ttu-id="04a10-154">In the Cost vs. Budget Over Time report, click **Actions** and then select **Schedule report**.</span><span class="sxs-lookup"><span data-stu-id="04a10-154">In the Cost vs. Budget Over Time report, click **Actions** and then select **Schedule report**.</span></span> <span data-ttu-id="04a10-155">On the Threshold tab, select a threshold metric.</span><span class="sxs-lookup"><span data-stu-id="04a10-155">On the Threshold tab, select a threshold metric.</span></span> <span data-ttu-id="04a10-156">For example, **Cost percentage vs budget**.</span><span class="sxs-lookup"><span data-stu-id="04a10-156">For example, **Cost percentage vs budget**.</span></span> <span data-ttu-id="04a10-157">Select an alert type and enter a percentage value of the budget.</span><span class="sxs-lookup"><span data-stu-id="04a10-157">Select an alert type and enter a percentage value of the budget.</span></span> <span data-ttu-id="04a10-158">If you want to get notified only once, select **Number of consecutive alerts** and then type _1_.</span><span class="sxs-lookup"><span data-stu-id="04a10-158">If you want to get notified only once, select **Number of consecutive alerts** and then type _1_.</span></span> <span data-ttu-id="04a10-159">Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="04a10-159">Click **Save**.</span></span>

![Budget alert](./media/manage-budgets/budget-alert.png)

## <a name="next-steps"></a><span data-ttu-id="04a10-161">Next steps</span><span class="sxs-lookup"><span data-stu-id="04a10-161">Next steps</span></span>

- <span data-ttu-id="04a10-162">If you haven't already completed the first tutorial for Cost Management, read it at  [Review usage and costs](https://docs.microsoft.com/en-us/azure/cost-management/tutorial-review-usage).</span><span class="sxs-lookup"><span data-stu-id="04a10-162">If you haven't already completed the first tutorial for Cost Management, read it at  [Review usage and costs](https://docs.microsoft.com/en-us/azure/cost-management/tutorial-review-usage).</span></span>
- <span data-ttu-id="04a10-163">Learn more about the [reports available in Cost Management](use-reports.md).</span><span class="sxs-lookup"><span data-stu-id="04a10-163">Learn more about the [reports available in Cost Management](use-reports.md).</span></span>
