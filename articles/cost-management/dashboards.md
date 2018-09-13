---
title: View key metrics in Azure Cost Management dashboards | Microsoft Docs
description: This article describes how view key metrics with dashboards in Azure Cost Management.
services: cost-management
keywords: ''
author: bandersmsft
ms.author: banders
ms.date: 06/12/2018
ms.topic: conceptual
ms.service: cost-management
manager: dougeby
ms.custom: ''
ms.openlocfilehash: 71fe8cca9bd60d75e2cc625cb12108324945e3c5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864680"
---
# <a name="view-key-cost-metrics-with-dashboards"></a><span data-ttu-id="a1d52-103">View key cost metrics with dashboards</span><span class="sxs-lookup"><span data-stu-id="a1d52-103">View key cost metrics with dashboards</span></span>

<span data-ttu-id="a1d52-104">Dashboards in Cloudyn provide a high-level view of reports.</span><span class="sxs-lookup"><span data-stu-id="a1d52-104">Dashboards in Cloudyn provide a high-level view of reports.</span></span> <span data-ttu-id="a1d52-105">Dashboards allow you to view key cost metrics in a single view.</span><span class="sxs-lookup"><span data-stu-id="a1d52-105">Dashboards allow you to view key cost metrics in a single view.</span></span> <span data-ttu-id="a1d52-106">They also provide business trend highlights to help you make important business decisions.</span><span class="sxs-lookup"><span data-stu-id="a1d52-106">They also provide business trend highlights to help you make important business decisions.</span></span>

<span data-ttu-id="a1d52-107">Dashboards are also used to create views for people with different responsibilities in your organization, which might include:</span><span class="sxs-lookup"><span data-stu-id="a1d52-107">Dashboards are also used to create views for people with different responsibilities in your organization, which might include:</span></span>

- <span data-ttu-id="a1d52-108">Financial controller</span><span class="sxs-lookup"><span data-stu-id="a1d52-108">Financial controller</span></span>
- <span data-ttu-id="a1d52-109">Application or project owner</span><span class="sxs-lookup"><span data-stu-id="a1d52-109">Application or project owner</span></span>
- <span data-ttu-id="a1d52-110">DevOps engineer</span><span class="sxs-lookup"><span data-stu-id="a1d52-110">DevOps engineer</span></span>
- <span data-ttu-id="a1d52-111">Executives</span><span class="sxs-lookup"><span data-stu-id="a1d52-111">Executives</span></span>

<span data-ttu-id="a1d52-112">Dashboards are made up of widgets and each widget is essentially a report thumbnail.</span><span class="sxs-lookup"><span data-stu-id="a1d52-112">Dashboards are made up of widgets and each widget is essentially a report thumbnail.</span></span> <span data-ttu-id="a1d52-113">Click a widget to open its report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-113">Click a widget to open its report.</span></span> <span data-ttu-id="a1d52-114">When you customize reports, you save them to My Reports and they're added to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-114">When you customize reports, you save them to My Reports and they're added to the dashboard.</span></span>

<span data-ttu-id="a1d52-115">Dashboard versions differ for Management (MSP), Enterprise, and Premium Cloudyn users.</span><span class="sxs-lookup"><span data-stu-id="a1d52-115">Dashboard versions differ for Management (MSP), Enterprise, and Premium Cloudyn users.</span></span> <span data-ttu-id="a1d52-116">The differences are determined by entity access levels.</span><span class="sxs-lookup"><span data-stu-id="a1d52-116">The differences are determined by entity access levels.</span></span> <span data-ttu-id="a1d52-117">For more information about access levels, see [Entity access levels](tutorial-user-access.md#entity-access-levels).</span><span class="sxs-lookup"><span data-stu-id="a1d52-117">For more information about access levels, see [Entity access levels](tutorial-user-access.md#entity-access-levels).</span></span>

<span data-ttu-id="a1d52-118">Dashboard availability depends on the type of cloud service provider account that is used when viewing dashboards.</span><span class="sxs-lookup"><span data-stu-id="a1d52-118">Dashboard availability depends on the type of cloud service provider account that is used when viewing dashboards.</span></span> <span data-ttu-id="a1d52-119">The type of information available and collected by Cloudyn affects reports in dashboards.</span><span class="sxs-lookup"><span data-stu-id="a1d52-119">The type of information available and collected by Cloudyn affects reports in dashboards.</span></span> <span data-ttu-id="a1d52-120">For example, if you don't have an AWS account then you won't see the S3 Tracker dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-120">For example, if you don't have an AWS account then you won't see the S3 Tracker dashboard.</span></span> <span data-ttu-id="a1d52-121">Similarly, if you don't enable Azure Resource Manager access to Cloudyn then you won't see any Azure-specific information in Optimizer dashboard widgets.</span><span class="sxs-lookup"><span data-stu-id="a1d52-121">Similarly, if you don't enable Azure Resource Manager access to Cloudyn then you won't see any Azure-specific information in Optimizer dashboard widgets.</span></span>

<span data-ttu-id="a1d52-122">You can use any of the premade dashboards or you can create your own dashboard with customized reports.</span><span class="sxs-lookup"><span data-stu-id="a1d52-122">You can use any of the premade dashboards or you can create your own dashboard with customized reports.</span></span> <span data-ttu-id="a1d52-123">If you're unfamiliar with Cloudyn reports, see [Use Cost Management reports](use-reports.md).</span><span class="sxs-lookup"><span data-stu-id="a1d52-123">If you're unfamiliar with Cloudyn reports, see [Use Cost Management reports](use-reports.md).</span></span>

## <a name="create-a-custom-dashboard"></a><span data-ttu-id="a1d52-124">Create a custom dashboard</span><span class="sxs-lookup"><span data-stu-id="a1d52-124">Create a custom dashboard</span></span>

<span data-ttu-id="a1d52-125">To quickly get started with a custom dashboard, you can duplicate an existing one to use its properties.</span><span class="sxs-lookup"><span data-stu-id="a1d52-125">To quickly get started with a custom dashboard, you can duplicate an existing one to use its properties.</span></span> <span data-ttu-id="a1d52-126">Then you can modify it to suit your needs.</span><span class="sxs-lookup"><span data-stu-id="a1d52-126">Then you can modify it to suit your needs.</span></span> <span data-ttu-id="a1d52-127">On the dashboard you want to copy, click **Save As**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-127">On the dashboard you want to copy, click **Save As**.</span></span> <span data-ttu-id="a1d52-128">You can only duplicate customized dashboards — you can't duplicate the dashboards that are included with Cloudyn.</span><span class="sxs-lookup"><span data-stu-id="a1d52-128">You can only duplicate customized dashboards — you can't duplicate the dashboards that are included with Cloudyn.</span></span>

<span data-ttu-id="a1d52-129">To create a custom dashboard:</span><span class="sxs-lookup"><span data-stu-id="a1d52-129">To create a custom dashboard:</span></span>

1. <span data-ttu-id="a1d52-130">On the homepage, click **Add New +**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-130">On the homepage, click **Add New +**.</span></span> <span data-ttu-id="a1d52-131">The My Dashboard page is displayed.</span><span class="sxs-lookup"><span data-stu-id="a1d52-131">The My Dashboard page is displayed.</span></span>  
    <span data-ttu-id="a1d52-132">![My dashboard](./media/dashboards/my-dashboard.png)</span><span class="sxs-lookup"><span data-stu-id="a1d52-132">![My dashboard](./media/dashboards/my-dashboard.png)</span></span>
2. <span data-ttu-id="a1d52-133">Click **Add New Report**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-133">Click **Add New Report**.</span></span> <span data-ttu-id="a1d52-134">The Add Report box is displayed.</span><span class="sxs-lookup"><span data-stu-id="a1d52-134">The Add Report box is displayed.</span></span>
3. <span data-ttu-id="a1d52-135">Select the report that you want to add to the dashboard widget.</span><span class="sxs-lookup"><span data-stu-id="a1d52-135">Select the report that you want to add to the dashboard widget.</span></span> <span data-ttu-id="a1d52-136">The widget is added to the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-136">The widget is added to the dashboard.</span></span>
4. <span data-ttu-id="a1d52-137">Repeat the preceding steps until the dashboard is complete.</span><span class="sxs-lookup"><span data-stu-id="a1d52-137">Repeat the preceding steps until the dashboard is complete.</span></span>
5. <span data-ttu-id="a1d52-138">To change the name of the dashboard, click the name of the dashboard on the Dashboard home page and type the new name.</span><span class="sxs-lookup"><span data-stu-id="a1d52-138">To change the name of the dashboard, click the name of the dashboard on the Dashboard home page and type the new name.</span></span>

## <a name="modify-a-custom-dashboard"></a><span data-ttu-id="a1d52-139">Modify a custom dashboard</span><span class="sxs-lookup"><span data-stu-id="a1d52-139">Modify a custom dashboard</span></span>

<span data-ttu-id="a1d52-140">Like creating a custom dashboard, you can't modify the dashboards included with Cloudyn.</span><span class="sxs-lookup"><span data-stu-id="a1d52-140">Like creating a custom dashboard, you can't modify the dashboards included with Cloudyn.</span></span> <span data-ttu-id="a1d52-141">To modify a custom dashboard report:</span><span class="sxs-lookup"><span data-stu-id="a1d52-141">To modify a custom dashboard report:</span></span>

1. <span data-ttu-id="a1d52-142">In the dashboard, find the report you want to modify and click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-142">In the dashboard, find the report you want to modify and click **Edit**.</span></span> <span data-ttu-id="a1d52-143">The report is displayed.</span><span class="sxs-lookup"><span data-stu-id="a1d52-143">The report is displayed.</span></span>
2. <span data-ttu-id="a1d52-144">Make any changes that you want to the report and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-144">Make any changes that you want to the report and click **Save**.</span></span> <span data-ttu-id="a1d52-145">The report is updated and displays your changes.</span><span class="sxs-lookup"><span data-stu-id="a1d52-145">The report is updated and displays your changes.</span></span>

## <a name="share-a-custom-dashboard"></a><span data-ttu-id="a1d52-146">Share a custom dashboard</span><span class="sxs-lookup"><span data-stu-id="a1d52-146">Share a custom dashboard</span></span>

<span data-ttu-id="a1d52-147">You can share a custom dashboard with others to _Public_ or _My Entity_.</span><span class="sxs-lookup"><span data-stu-id="a1d52-147">You can share a custom dashboard with others to _Public_ or _My Entity_.</span></span> <span data-ttu-id="a1d52-148">When you share to Public, all users can view the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-148">When you share to Public, all users can view the dashboard.</span></span> <span data-ttu-id="a1d52-149">Only users with access to the current entity can view the dashboard when you share to My Entity.</span><span class="sxs-lookup"><span data-stu-id="a1d52-149">Only users with access to the current entity can view the dashboard when you share to My Entity.</span></span> <span data-ttu-id="a1d52-150">The steps to share a custom dashboard with Public and My Entity are similar.</span><span class="sxs-lookup"><span data-stu-id="a1d52-150">The steps to share a custom dashboard with Public and My Entity are similar.</span></span>

<span data-ttu-id="a1d52-151">To share a custom dashboard to Public:</span><span class="sxs-lookup"><span data-stu-id="a1d52-151">To share a custom dashboard to Public:</span></span>

1. <span data-ttu-id="a1d52-152">In a dashboard, click **Dashboard Settings**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-152">In a dashboard, click **Dashboard Settings**.</span></span> <span data-ttu-id="a1d52-153">The Dashboard Settings box is displayed.</span><span class="sxs-lookup"><span data-stu-id="a1d52-153">The Dashboard Settings box is displayed.</span></span>  
    <span data-ttu-id="a1d52-154">![dashboard options](./media/dashboards/dashboard-options.png)</span><span class="sxs-lookup"><span data-stu-id="a1d52-154">![dashboard options](./media/dashboards/dashboard-options.png)</span></span>
2. <span data-ttu-id="a1d52-155">In the Dashboard Settings box, click the arrow symbol and then click **Public**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-155">In the Dashboard Settings box, click the arrow symbol and then click **Public**.</span></span> <span data-ttu-id="a1d52-156">The Public Dashboard confirmation dialog box is displayed.</span><span class="sxs-lookup"><span data-stu-id="a1d52-156">The Public Dashboard confirmation dialog box is displayed.</span></span>
3. <span data-ttu-id="a1d52-157">Click  **Yes**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-157">Click  **Yes**.</span></span> <span data-ttu-id="a1d52-158">The dashboard is now available to others.</span><span class="sxs-lookup"><span data-stu-id="a1d52-158">The dashboard is now available to others.</span></span>

## <a name="delete-a-custom-dashboard-report"></a><span data-ttu-id="a1d52-159">Delete a custom dashboard report</span><span class="sxs-lookup"><span data-stu-id="a1d52-159">Delete a custom dashboard report</span></span>

<span data-ttu-id="a1d52-160">You can delete a custom report component from the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-160">You can delete a custom report component from the dashboard.</span></span> <span data-ttu-id="a1d52-161">Deleting the report from the dashboard doesn't delete the report from the reports list.</span><span class="sxs-lookup"><span data-stu-id="a1d52-161">Deleting the report from the dashboard doesn't delete the report from the reports list.</span></span> <span data-ttu-id="a1d52-162">Instead, deleting the report removes it from the dashboard only.</span><span class="sxs-lookup"><span data-stu-id="a1d52-162">Instead, deleting the report removes it from the dashboard only.</span></span>

<span data-ttu-id="a1d52-163">To delete a dashboard component, on the dashboard component, click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-163">To delete a dashboard component, on the dashboard component, click **Delete**.</span></span> <span data-ttu-id="a1d52-164">Clicking **Delete**  immediately deletes the dashboard component.</span><span class="sxs-lookup"><span data-stu-id="a1d52-164">Clicking **Delete**  immediately deletes the dashboard component.</span></span>

## <a name="share-a-dashboard-enterprise"></a><span data-ttu-id="a1d52-165">Share a dashboard (Enterprise)</span><span class="sxs-lookup"><span data-stu-id="a1d52-165">Share a dashboard (Enterprise)</span></span>

<span data-ttu-id="a1d52-166">You can share custom dashboards to all users in your organization or with the users of the current entity.</span><span class="sxs-lookup"><span data-stu-id="a1d52-166">You can share custom dashboards to all users in your organization or with the users of the current entity.</span></span> <span data-ttu-id="a1d52-167">Sharing a dashboard can give others a quick high-level view of your KPI.</span><span class="sxs-lookup"><span data-stu-id="a1d52-167">Sharing a dashboard can give others a quick high-level view of your KPI.</span></span> <span data-ttu-id="a1d52-168">When you share a dashboard, it automatically replicates the dashboard to all your Cloudyn entities/customers.</span><span class="sxs-lookup"><span data-stu-id="a1d52-168">When you share a dashboard, it automatically replicates the dashboard to all your Cloudyn entities/customers.</span></span> <span data-ttu-id="a1d52-169">Changes to the shared dashboard are automatically updated.</span><span class="sxs-lookup"><span data-stu-id="a1d52-169">Changes to the shared dashboard are automatically updated.</span></span>

<span data-ttu-id="a1d52-170">To share a dashboard with all users including subentities:</span><span class="sxs-lookup"><span data-stu-id="a1d52-170">To share a dashboard with all users including subentities:</span></span>

1. <span data-ttu-id="a1d52-171">On the dashboard home page, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-171">On the dashboard home page, click **Edit**.</span></span>
2. <span data-ttu-id="a1d52-172">Click **Share** and then select **Public**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-172">Click **Share** and then select **Public**.</span></span>
3. <span data-ttu-id="a1d52-173">The Global Public Dashboard confirmation box is displayed.</span><span class="sxs-lookup"><span data-stu-id="a1d52-173">The Global Public Dashboard confirmation box is displayed.</span></span>
4. <span data-ttu-id="a1d52-174">Click **Yes** to set the dashboard as a global public dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-174">Click **Yes** to set the dashboard as a global public dashboard.</span></span>

<span data-ttu-id="a1d52-175">To share a dashboard with all users of a current entity:</span><span class="sxs-lookup"><span data-stu-id="a1d52-175">To share a dashboard with all users of a current entity:</span></span>

1. <span data-ttu-id="a1d52-176">From the Dashboard home page, click **Edit**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-176">From the Dashboard home page, click **Edit**.</span></span>
2. <span data-ttu-id="a1d52-177">Click **Share** and then select **My Entity**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-177">Click **Share** and then select **My Entity**.</span></span>
3. <span data-ttu-id="a1d52-178">Click **Yes** to set the dashboard as a public dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-178">Click **Yes** to set the dashboard as a public dashboard.</span></span>

## <a name="duplicate-a-custom-dashboard"></a><span data-ttu-id="a1d52-179">Duplicate a custom dashboard</span><span class="sxs-lookup"><span data-stu-id="a1d52-179">Duplicate a custom dashboard</span></span>

<span data-ttu-id="a1d52-180">When you create a new dashboard, you might want to use similar properties from an existing dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-180">When you create a new dashboard, you might want to use similar properties from an existing dashboard.</span></span> <span data-ttu-id="a1d52-181">You can duplicate the dashboard to create a new one.</span><span class="sxs-lookup"><span data-stu-id="a1d52-181">You can duplicate the dashboard to create a new one.</span></span>

<span data-ttu-id="a1d52-182">You can only duplicate custom dashboards.</span><span class="sxs-lookup"><span data-stu-id="a1d52-182">You can only duplicate custom dashboards.</span></span> <span data-ttu-id="a1d52-183">You can't duplicate standard dashboards.</span><span class="sxs-lookup"><span data-stu-id="a1d52-183">You can't duplicate standard dashboards.</span></span>

<span data-ttu-id="a1d52-184">To duplicate (clone) a custom dashboard:</span><span class="sxs-lookup"><span data-stu-id="a1d52-184">To duplicate (clone) a custom dashboard:</span></span>

1. <span data-ttu-id="a1d52-185">On the Dashboard that you want to duplicate, click **Save As**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-185">On the Dashboard that you want to duplicate, click **Save As**.</span></span> <span data-ttu-id="a1d52-186">A new dashboard opens with the same name and a number.</span><span class="sxs-lookup"><span data-stu-id="a1d52-186">A new dashboard opens with the same name and a number.</span></span>
2. <span data-ttu-id="a1d52-187">Rename the duplicated dashboard and modify it as you like.</span><span class="sxs-lookup"><span data-stu-id="a1d52-187">Rename the duplicated dashboard and modify it as you like.</span></span>

<span data-ttu-id="a1d52-188">-Or-</span><span class="sxs-lookup"><span data-stu-id="a1d52-188">-Or-</span></span>

1. <span data-ttu-id="a1d52-189">In Dashboard Settings, click **Save As**  on the line of the dashboard that you want to duplicate.</span><span class="sxs-lookup"><span data-stu-id="a1d52-189">In Dashboard Settings, click **Save As**  on the line of the dashboard that you want to duplicate.</span></span>
2. <span data-ttu-id="a1d52-190">The duplicated dashboard opens.</span><span class="sxs-lookup"><span data-stu-id="a1d52-190">The duplicated dashboard opens.</span></span>
3. <span data-ttu-id="a1d52-191">Rename the dashboard and modify it as you like.</span><span class="sxs-lookup"><span data-stu-id="a1d52-191">Rename the dashboard and modify it as you like.</span></span>

## <a name="set-a-default-dashboard"></a><span data-ttu-id="a1d52-192">Set a default dashboard</span><span class="sxs-lookup"><span data-stu-id="a1d52-192">Set a default dashboard</span></span>

<span data-ttu-id="a1d52-193">You can set any dashboard as your default.</span><span class="sxs-lookup"><span data-stu-id="a1d52-193">You can set any dashboard as your default.</span></span> <span data-ttu-id="a1d52-194">Setting it to your default makes it appear as the left-most tab in the dashboard tab list.</span><span class="sxs-lookup"><span data-stu-id="a1d52-194">Setting it to your default makes it appear as the left-most tab in the dashboard tab list.</span></span> <span data-ttu-id="a1d52-195">The default dashboard displays when open the Cloudyn portal.</span><span class="sxs-lookup"><span data-stu-id="a1d52-195">The default dashboard displays when open the Cloudyn portal.</span></span>

- <span data-ttu-id="a1d52-196">Click the dashboard tab you would like to set as default, then click **Default** on the right.</span><span class="sxs-lookup"><span data-stu-id="a1d52-196">Click the dashboard tab you would like to set as default, then click **Default** on the right.</span></span>

<span data-ttu-id="a1d52-197">-Or-</span><span class="sxs-lookup"><span data-stu-id="a1d52-197">-Or-</span></span>

1. <span data-ttu-id="a1d52-198">Click **Dashboard Settings** to see the list of available dashboards and select the dashboard that you want to set as the default.</span><span class="sxs-lookup"><span data-stu-id="a1d52-198">Click **Dashboard Settings** to see the list of available dashboards and select the dashboard that you want to set as the default.</span></span>  
    <span data-ttu-id="a1d52-199">![dashboard options](./media/dashboards/dashboard-options.png)</span><span class="sxs-lookup"><span data-stu-id="a1d52-199">![dashboard options](./media/dashboards/dashboard-options.png)</span></span>
2. <span data-ttu-id="a1d52-200">Click **Default** in the line of the dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-200">Click **Default** in the line of the dashboard.</span></span> <span data-ttu-id="a1d52-201">The Default Dashboard confirmation box is displayed.</span><span class="sxs-lookup"><span data-stu-id="a1d52-201">The Default Dashboard confirmation box is displayed.</span></span>
3. <span data-ttu-id="a1d52-202">Click **Yes**.</span><span class="sxs-lookup"><span data-stu-id="a1d52-202">Click **Yes**.</span></span> <span data-ttu-id="a1d52-203">The dashboard is set to default.</span><span class="sxs-lookup"><span data-stu-id="a1d52-203">The dashboard is set to default.</span></span>

## <a name="management-dashboard"></a><span data-ttu-id="a1d52-204">Management dashboard</span><span class="sxs-lookup"><span data-stu-id="a1d52-204">Management dashboard</span></span>
<span data-ttu-id="a1d52-205">The Management (or MSP dashboard for MSP users) dashboard includes highlights of the main report types.</span><span class="sxs-lookup"><span data-stu-id="a1d52-205">The Management (or MSP dashboard for MSP users) dashboard includes highlights of the main report types.</span></span>  
![Management dashboard](./media/dashboards/management-dash.png)

### <a name="cost-entity-summary-enterprise-only"></a><span data-ttu-id="a1d52-207">Cost Entity Summary (Enterprise only)</span><span class="sxs-lookup"><span data-stu-id="a1d52-207">Cost Entity Summary (Enterprise only)</span></span>
<span data-ttu-id="a1d52-208">This widget summarizes the managed cost entities, including the number of entities and number of accounts.</span><span class="sxs-lookup"><span data-stu-id="a1d52-208">This widget summarizes the managed cost entities, including the number of entities and number of accounts.</span></span>
- <span data-ttu-id="a1d52-209">Click the widget to open the Enterprise Details report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-209">Click the widget to open the Enterprise Details report.</span></span>

### <a name="cost-over-time"></a><span data-ttu-id="a1d52-210">Cost Over Time</span><span class="sxs-lookup"><span data-stu-id="a1d52-210">Cost Over Time</span></span>
<span data-ttu-id="a1d52-211">This widget can help you spot cost trends.</span><span class="sxs-lookup"><span data-stu-id="a1d52-211">This widget can help you spot cost trends.</span></span> <span data-ttu-id="a1d52-212">It highlights the cost for the last day, based on the trend of the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-212">It highlights the cost for the last day, based on the trend of the last 30 days.</span></span>
- <span data-ttu-id="a1d52-213">Click the widget to open the Actual Cost Over Time report to view and filter additional details.</span><span class="sxs-lookup"><span data-stu-id="a1d52-213">Click the widget to open the Actual Cost Over Time report to view and filter additional details.</span></span>

### <a name="asset-controller"></a><span data-ttu-id="a1d52-214">Asset Controller</span><span class="sxs-lookup"><span data-stu-id="a1d52-214">Asset Controller</span></span>
<span data-ttu-id="a1d52-215">This widget highlights the number of running instances from the previous day, above the usage trend over the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-215">This widget highlights the number of running instances from the previous day, above the usage trend over the last 30 days.</span></span>
- <span data-ttu-id="a1d52-216">Click the widget to open the Asset Controller dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-216">Click the widget to open the Asset Controller dashboard.</span></span>

### <a name="unused-ri-detector"></a><span data-ttu-id="a1d52-217">Unused RI Detector</span><span class="sxs-lookup"><span data-stu-id="a1d52-217">Unused RI Detector</span></span>
<span data-ttu-id="a1d52-218">This widget highlights the number of Amazon EC2 unused reservations.</span><span class="sxs-lookup"><span data-stu-id="a1d52-218">This widget highlights the number of Amazon EC2 unused reservations.</span></span>
- <span data-ttu-id="a1d52-219">Click the widget to open the Currently Unused Reservations report where you can view the unused reservations you can modify.</span><span class="sxs-lookup"><span data-stu-id="a1d52-219">Click the widget to open the Currently Unused Reservations report where you can view the unused reservations you can modify.</span></span>

### <a name="cost-by-service"></a><span data-ttu-id="a1d52-220">Cost by Service</span><span class="sxs-lookup"><span data-stu-id="a1d52-220">Cost by Service</span></span>
<span data-ttu-id="a1d52-221">This widget highlights amortized costs by service for the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-221">This widget highlights amortized costs by service for the last 30 days.</span></span> <span data-ttu-id="a1d52-222">Hover over the pie chart to see the costs per service.</span><span class="sxs-lookup"><span data-stu-id="a1d52-222">Hover over the pie chart to see the costs per service.</span></span>
- <span data-ttu-id="a1d52-223">Click the widget to open the Actual Cost Analysis report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-223">Click the widget to open the Actual Cost Analysis report.</span></span>

### <a name="potential-savings"></a><span data-ttu-id="a1d52-224">Potential savings</span><span class="sxs-lookup"><span data-stu-id="a1d52-224">Potential savings</span></span>
<span data-ttu-id="a1d52-225">This widget shows instance type pricing recommendations for Amazon EC2 and Amazon RDS.</span><span class="sxs-lookup"><span data-stu-id="a1d52-225">This widget shows instance type pricing recommendations for Amazon EC2 and Amazon RDS.</span></span>
- <span data-ttu-id="a1d52-226">Click the widget open the Savings Analysis report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-226">Click the widget open the Savings Analysis report.</span></span> <span data-ttu-id="a1d52-227">It lists your costs by instance types with potential savings.</span><span class="sxs-lookup"><span data-stu-id="a1d52-227">It lists your costs by instance types with potential savings.</span></span>

### <a name="compute-instances---daily-trend"></a><span data-ttu-id="a1d52-228">Compute Instances - Daily Trend</span><span class="sxs-lookup"><span data-stu-id="a1d52-228">Compute Instances - Daily Trend</span></span>
<span data-ttu-id="a1d52-229">This widget displays the active instances by type, for the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-229">This widget displays the active instances by type, for the last 30 days.</span></span>
- <span data-ttu-id="a1d52-230">Click the widget to open the Instances Over Time report, where you can view a breakdown of all instances running during the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-230">Click the widget to open the Instances Over Time report, where you can view a breakdown of all instances running during the last 30 days.</span></span>

### <a name="storage-by-department"></a><span data-ttu-id="a1d52-231">Storage by department</span><span class="sxs-lookup"><span data-stu-id="a1d52-231">Storage by department</span></span>
<span data-ttu-id="a1d52-232">This widget displays the storage services used by departments.</span><span class="sxs-lookup"><span data-stu-id="a1d52-232">This widget displays the storage services used by departments.</span></span> <span data-ttu-id="a1d52-233">Hover over the pie chart to see your storage consumption by department.</span><span class="sxs-lookup"><span data-stu-id="a1d52-233">Hover over the pie chart to see your storage consumption by department.</span></span>
- <span data-ttu-id="a1d52-234">Click the widget to open the S3 Tracker dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-234">Click the widget to open the S3 Tracker dashboard.</span></span>

## <a name="cost-controller-dashboard"></a><span data-ttu-id="a1d52-235">Cost Controller dashboard</span><span class="sxs-lookup"><span data-stu-id="a1d52-235">Cost Controller dashboard</span></span>
<span data-ttu-id="a1d52-236">The Cost Controller dashboard shows pre-set cost allocation highlights.</span><span class="sxs-lookup"><span data-stu-id="a1d52-236">The Cost Controller dashboard shows pre-set cost allocation highlights.</span></span>  
![Cost Controller dashboard](./media/dashboards/cost-controller-dashboard.png)

### <a name="cost-over-time"></a><span data-ttu-id="a1d52-238">Cost Over Time</span><span class="sxs-lookup"><span data-stu-id="a1d52-238">Cost Over Time</span></span>
<span data-ttu-id="a1d52-239">This widget helps you spot cost trends.</span><span class="sxs-lookup"><span data-stu-id="a1d52-239">This widget helps you spot cost trends.</span></span> <span data-ttu-id="a1d52-240">It highlights the cost for the last day, based on the trend of the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-240">It highlights the cost for the last day, based on the trend of the last 30 days.</span></span>
- <span data-ttu-id="a1d52-241">Click the widget to open the Actual Cost Over Time report to view and filter additional details.</span><span class="sxs-lookup"><span data-stu-id="a1d52-241">Click the widget to open the Actual Cost Over Time report to view and filter additional details.</span></span>

### <a name="monthly-cost-trends"></a><span data-ttu-id="a1d52-242">Monthly Cost Trends</span><span class="sxs-lookup"><span data-stu-id="a1d52-242">Monthly Cost Trends</span></span>
<span data-ttu-id="a1d52-243">This widget highlights projected amortized spending and your actual spend since the beginning of the month.</span><span class="sxs-lookup"><span data-stu-id="a1d52-243">This widget highlights projected amortized spending and your actual spend since the beginning of the month.</span></span>
- <span data-ttu-id="a1d52-244">Click the widget to open the Current Month Projected Cost report, which provides a month-to-date cost summary.</span><span class="sxs-lookup"><span data-stu-id="a1d52-244">Click the widget to open the Current Month Projected Cost report, which provides a month-to-date cost summary.</span></span>

<span data-ttu-id="a1d52-245">This report shows the cost from the beginning of month, the cost of previous month, and the current month projected cost.</span><span class="sxs-lookup"><span data-stu-id="a1d52-245">This report shows the cost from the beginning of month, the cost of previous month, and the current month projected cost.</span></span> <span data-ttu-id="a1d52-246">The current month projected cost is calculated by adding the up-to-date monthly cost and projection.</span><span class="sxs-lookup"><span data-stu-id="a1d52-246">The current month projected cost is calculated by adding the up-to-date monthly cost and projection.</span></span> <span data-ttu-id="a1d52-247">The projection is based on the cost monitored over the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-247">The projection is based on the cost monitored over the last 30 days.</span></span>

### <a name="12-month-planner"></a><span data-ttu-id="a1d52-248">12 Month Planner</span><span class="sxs-lookup"><span data-stu-id="a1d52-248">12 Month Planner</span></span>
<span data-ttu-id="a1d52-249">This widget highlights the projected costs over the next 12 months and the potential savings.</span><span class="sxs-lookup"><span data-stu-id="a1d52-249">This widget highlights the projected costs over the next 12 months and the potential savings.</span></span>
- <span data-ttu-id="a1d52-250">Click the widget to open the Annual Projected Cost report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-250">Click the widget to open the Annual Projected Cost report.</span></span>

### <a name="cost-by-service"></a><span data-ttu-id="a1d52-251">Cost by Service</span><span class="sxs-lookup"><span data-stu-id="a1d52-251">Cost by Service</span></span>
<span data-ttu-id="a1d52-252">This widget highlights amortized costs by service for the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-252">This widget highlights amortized costs by service for the last 30 days.</span></span>
- <span data-ttu-id="a1d52-253">Hover over the pie chart to see the costs per service.</span><span class="sxs-lookup"><span data-stu-id="a1d52-253">Hover over the pie chart to see the costs per service.</span></span>
- <span data-ttu-id="a1d52-254">Click the widget to open the Actual Cost Analysis report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-254">Click the widget to open the Actual Cost Analysis report.</span></span>

### <a name="cost-by-account"></a><span data-ttu-id="a1d52-255">Cost by Account</span><span class="sxs-lookup"><span data-stu-id="a1d52-255">Cost by Account</span></span>
<span data-ttu-id="a1d52-256">This widget highlights amortized costs by account for the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-256">This widget highlights amortized costs by account for the last 30 days.</span></span>
- <span data-ttu-id="a1d52-257">Hover over the pie chart to see the costs per account.</span><span class="sxs-lookup"><span data-stu-id="a1d52-257">Hover over the pie chart to see the costs per account.</span></span>
- <span data-ttu-id="a1d52-258">Click the widget to open the Actual Cost Analysis report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-258">Click the widget to open the Actual Cost Analysis report.</span></span>

### <a name="cost-trend-by-day"></a><span data-ttu-id="a1d52-259">Cost Trend by Day</span><span class="sxs-lookup"><span data-stu-id="a1d52-259">Cost Trend by Day</span></span>
<span data-ttu-id="a1d52-260">This widget highlights spend over the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-260">This widget highlights spend over the last 30 days.</span></span>
- <span data-ttu-id="a1d52-261">Hover over the bar graph to see costs per day.</span><span class="sxs-lookup"><span data-stu-id="a1d52-261">Hover over the bar graph to see costs per day.</span></span>
- <span data-ttu-id="a1d52-262">Click the widget to open the Actual Cost Over Time report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-262">Click the widget to open the Actual Cost Over Time report.</span></span>

### <a name="cost-trend-by-month---last-6-months"></a><span data-ttu-id="a1d52-263">Cost Trend by Month - Last 6 months</span><span class="sxs-lookup"><span data-stu-id="a1d52-263">Cost Trend by Month - Last 6 months</span></span>

<span data-ttu-id="a1d52-264">This widget highlights spend over the last six months.</span><span class="sxs-lookup"><span data-stu-id="a1d52-264">This widget highlights spend over the last six months.</span></span>
- <span data-ttu-id="a1d52-265">Hover over the bar graph to see costs per month.</span><span class="sxs-lookup"><span data-stu-id="a1d52-265">Hover over the bar graph to see costs per month.</span></span>
- <span data-ttu-id="a1d52-266">Click the widget to open the Actual Cost Over Time report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-266">Click the widget to open the Actual Cost Over Time report.</span></span>

## <a name="asset-controller-dashboard"></a><span data-ttu-id="a1d52-267">Asset Controller dashboard</span><span class="sxs-lookup"><span data-stu-id="a1d52-267">Asset Controller dashboard</span></span>

<span data-ttu-id="a1d52-268">This dashboard displays the number of running instances, available and in-use disks, distribution of instance types, and storage information.</span><span class="sxs-lookup"><span data-stu-id="a1d52-268">This dashboard displays the number of running instances, available and in-use disks, distribution of instance types, and storage information.</span></span>  
![Asset Controller dashboard](./media/dashboards/asset-controller-dashboard.png)

### <a name="compute-instances"></a><span data-ttu-id="a1d52-270">Compute Instances</span><span class="sxs-lookup"><span data-stu-id="a1d52-270">Compute Instances</span></span>
<span data-ttu-id="a1d52-271">This widget displays the number of running instances based on the usage trend over the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-271">This widget displays the number of running instances based on the usage trend over the last 30 days.</span></span>
- <span data-ttu-id="a1d52-272">Click the widget to open the Instances Over Time report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-272">Click the widget to open the Instances Over Time report.</span></span>

### <a name="disks"></a><span data-ttu-id="a1d52-273">Disks</span><span class="sxs-lookup"><span data-stu-id="a1d52-273">Disks</span></span>
<span data-ttu-id="a1d52-274">This widget highlights the total number and volume of disks, that are in-use and available.</span><span class="sxs-lookup"><span data-stu-id="a1d52-274">This widget highlights the total number and volume of disks, that are in-use and available.</span></span>
- <span data-ttu-id="a1d52-275">Click the widget to open the Active Disks report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-275">Click the widget to open the Active Disks report.</span></span>

### <a name="instance-type-distribution"></a><span data-ttu-id="a1d52-276">Instance Type Distribution</span><span class="sxs-lookup"><span data-stu-id="a1d52-276">Instance Type Distribution</span></span>
<span data-ttu-id="a1d52-277">This widget highlights the instance types in a pie chart.</span><span class="sxs-lookup"><span data-stu-id="a1d52-277">This widget highlights the instance types in a pie chart.</span></span>
- <span data-ttu-id="a1d52-278">Click on the widget to open the Instance Distribution report, which provides a breakdown of your active instances by the selected aggregation.</span><span class="sxs-lookup"><span data-stu-id="a1d52-278">Click on the widget to open the Instance Distribution report, which provides a breakdown of your active instances by the selected aggregation.</span></span>

### <a name="compute-instances---daily-trend"></a><span data-ttu-id="a1d52-279">Compute Instances - Daily Trend</span><span class="sxs-lookup"><span data-stu-id="a1d52-279">Compute Instances - Daily Trend</span></span>
<span data-ttu-id="a1d52-280">This widget highlights the compute instances (spot, reserved, and on-demand) per day for the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-280">This widget highlights the compute instances (spot, reserved, and on-demand) per day for the last 30 days.</span></span>
- <span data-ttu-id="a1d52-281">Hover over the graph to view the number of compute instances, per type per day.</span><span class="sxs-lookup"><span data-stu-id="a1d52-281">Hover over the graph to view the number of compute instances, per type per day.</span></span>
- <span data-ttu-id="a1d52-282">Click the widget to open the Instances Over Time report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-282">Click the widget to open the Instances Over Time report.</span></span>

### <a name="all-buckets-s3"></a><span data-ttu-id="a1d52-283">All Buckets (S3)</span><span class="sxs-lookup"><span data-stu-id="a1d52-283">All Buckets (S3)</span></span>
<span data-ttu-id="a1d52-284">This widget highlights the total S3 storage and number of objects stored.</span><span class="sxs-lookup"><span data-stu-id="a1d52-284">This widget highlights the total S3 storage and number of objects stored.</span></span>
- <span data-ttu-id="a1d52-285">Click the widget to open the S3 Tracker Dashboard.</span><span class="sxs-lookup"><span data-stu-id="a1d52-285">Click the widget to open the S3 Tracker Dashboard.</span></span> <span data-ttu-id="a1d52-286">The dashboard helps you find, analyze, and display your current storage usage and trends.</span><span class="sxs-lookup"><span data-stu-id="a1d52-286">The dashboard helps you find, analyze, and display your current storage usage and trends.</span></span>

### <a name="sql-db-instances-rds"></a><span data-ttu-id="a1d52-287">SQL DB Instances (RDS)</span><span class="sxs-lookup"><span data-stu-id="a1d52-287">SQL DB Instances (RDS)</span></span>
<span data-ttu-id="a1d52-288">This widget highlights the number of running Amazon RDS instances based on the trend of the last 30 days.</span><span class="sxs-lookup"><span data-stu-id="a1d52-288">This widget highlights the number of running Amazon RDS instances based on the trend of the last 30 days.</span></span>
- <span data-ttu-id="a1d52-289">Click the widget to open the RDS Instance Over Time report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-289">Click the widget to open the RDS Instance Over Time report.</span></span>

## <a name="optimizer-dashboard"></a><span data-ttu-id="a1d52-290">Optimizer Dashboard</span><span class="sxs-lookup"><span data-stu-id="a1d52-290">Optimizer Dashboard</span></span>
<span data-ttu-id="a1d52-291">This dashboard displays downsizing recommendations, unused resources, and potential savings.</span><span class="sxs-lookup"><span data-stu-id="a1d52-291">This dashboard displays downsizing recommendations, unused resources, and potential savings.</span></span>  
![Optimizer dashboard](./media/dashboards/optimizer-dashboard.png)

### <a name="ri-calculator"></a><span data-ttu-id="a1d52-293">RI Calculator</span><span class="sxs-lookup"><span data-stu-id="a1d52-293">RI Calculator</span></span>
<span data-ttu-id="a1d52-294">This widget displays the number of RI buying recommendations and highlights the potential annual savings.</span><span class="sxs-lookup"><span data-stu-id="a1d52-294">This widget displays the number of RI buying recommendations and highlights the potential annual savings.</span></span>
- <span data-ttu-id="a1d52-295">Click the widget to open the Reserved Instance Calculator where you can determine when to use on-demand vs. reserved pricing plans.</span><span class="sxs-lookup"><span data-stu-id="a1d52-295">Click the widget to open the Reserved Instance Calculator where you can determine when to use on-demand vs. reserved pricing plans.</span></span>

### <a name="sizing"></a><span data-ttu-id="a1d52-296">Sizing</span><span class="sxs-lookup"><span data-stu-id="a1d52-296">Sizing</span></span>
<span data-ttu-id="a1d52-297">This widget highlights the sizing recommended and potential savings, if implemented.</span><span class="sxs-lookup"><span data-stu-id="a1d52-297">This widget highlights the sizing recommended and potential savings, if implemented.</span></span>
- <span data-ttu-id="a1d52-298">Click the widget to open the EC2 Cost Effective Sizing Recommendations report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-298">Click the widget to open the EC2 Cost Effective Sizing Recommendations report.</span></span>

### <a name="unused-ri-detector"></a><span data-ttu-id="a1d52-299">Unused RI Detector</span><span class="sxs-lookup"><span data-stu-id="a1d52-299">Unused RI Detector</span></span>
<span data-ttu-id="a1d52-300">This widget highlights the number of Amazon EC2 unused reservations.</span><span class="sxs-lookup"><span data-stu-id="a1d52-300">This widget highlights the number of Amazon EC2 unused reservations.</span></span>
- <span data-ttu-id="a1d52-301">Click the widget to open the Currently Unused Reservations report where you can view the unused reservations that you can modify.</span><span class="sxs-lookup"><span data-stu-id="a1d52-301">Click the widget to open the Currently Unused Reservations report where you can view the unused reservations that you can modify.</span></span>

###  <a name="available-disks"></a><span data-ttu-id="a1d52-302">Available Disks</span><span class="sxs-lookup"><span data-stu-id="a1d52-302">Available Disks</span></span>
<span data-ttu-id="a1d52-303">This widget highlights the number of unattached disks in your deployment.</span><span class="sxs-lookup"><span data-stu-id="a1d52-303">This widget highlights the number of unattached disks in your deployment.</span></span>
- <span data-ttu-id="a1d52-304">Click the widget to open the Unattached Disks report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-304">Click the widget to open the Unattached Disks report.</span></span>

### <a name="rds-ri-calculator"></a><span data-ttu-id="a1d52-305">RDS RI Calculator</span><span class="sxs-lookup"><span data-stu-id="a1d52-305">RDS RI Calculator</span></span>
<span data-ttu-id="a1d52-306">This widget highlights the number of reservation recommendations for your Amazon RDS instances and the potential savings.</span><span class="sxs-lookup"><span data-stu-id="a1d52-306">This widget highlights the number of reservation recommendations for your Amazon RDS instances and the potential savings.</span></span>
- <span data-ttu-id="a1d52-307">Click the widget to open the RDS RI Buying Recommendations report where you can see Cloudyn recommendations to use reserved instances instead of on-demand Instances.</span><span class="sxs-lookup"><span data-stu-id="a1d52-307">Click the widget to open the RDS RI Buying Recommendations report where you can see Cloudyn recommendations to use reserved instances instead of on-demand Instances.</span></span>

### <a name="rds-sizing"></a><span data-ttu-id="a1d52-308">RDS Sizing</span><span class="sxs-lookup"><span data-stu-id="a1d52-308">RDS Sizing</span></span>
<span data-ttu-id="a1d52-309">This widget shows the number of sizing recommendations and the potential savings.</span><span class="sxs-lookup"><span data-stu-id="a1d52-309">This widget shows the number of sizing recommendations and the potential savings.</span></span>
- <span data-ttu-id="a1d52-310">Click the widget to open the RDS Sizing Recommendations report, which displays detailed Amazon RDS sizing recommendations.</span><span class="sxs-lookup"><span data-stu-id="a1d52-310">Click the widget to open the RDS Sizing Recommendations report, which displays detailed Amazon RDS sizing recommendations.</span></span>

<span data-ttu-id="a1d52-311">The optimization recommendations are based on the usage and performance data monitored in the last month.</span><span class="sxs-lookup"><span data-stu-id="a1d52-311">The optimization recommendations are based on the usage and performance data monitored in the last month.</span></span>

## <a name="s3-tracker-dashboard"></a><span data-ttu-id="a1d52-312">S3 Tracker dashboard</span><span class="sxs-lookup"><span data-stu-id="a1d52-312">S3 Tracker dashboard</span></span>
<span data-ttu-id="a1d52-313">The S3 Tracker dashboard helps you find, analyze, and display your current storage usage and trends.</span><span class="sxs-lookup"><span data-stu-id="a1d52-313">The S3 Tracker dashboard helps you find, analyze, and display your current storage usage and trends.</span></span>  
![S3 Tracker dashboard](./media/dashboards/s3-tracker-dashboard.png)

### <a name="all-buckets"></a><span data-ttu-id="a1d52-315">All Buckets</span><span class="sxs-lookup"><span data-stu-id="a1d52-315">All Buckets</span></span>
<span data-ttu-id="a1d52-316">This widget highlights the total size of all your buckets, in GB, and the total number of objects in your buckets.</span><span class="sxs-lookup"><span data-stu-id="a1d52-316">This widget highlights the total size of all your buckets, in GB, and the total number of objects in your buckets.</span></span>
- <span data-ttu-id="a1d52-317">Click the widget to open the Distribution of S3 Size report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-317">Click the widget to open the Distribution of S3 Size report.</span></span> <span data-ttu-id="a1d52-318">The report helps you analyze your S3 size by bucket, top-level folder, storage class, and versioning state.</span><span class="sxs-lookup"><span data-stu-id="a1d52-318">The report helps you analyze your S3 size by bucket, top-level folder, storage class, and versioning state.</span></span>

### <a name="bucket-properties"></a><span data-ttu-id="a1d52-319">Bucket Properties</span><span class="sxs-lookup"><span data-stu-id="a1d52-319">Bucket Properties</span></span>
<span data-ttu-id="a1d52-320">This widget highlights the total number of storage buckets.</span><span class="sxs-lookup"><span data-stu-id="a1d52-320">This widget highlights the total number of storage buckets.</span></span>
- <span data-ttu-id="a1d52-321">Click the widget to view the S3 Bucket Properties report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-321">Click the widget to view the S3 Bucket Properties report.</span></span>

### <a name="scan-status"></a><span data-ttu-id="a1d52-322">Scan Status</span><span class="sxs-lookup"><span data-stu-id="a1d52-322">Scan Status</span></span>
<span data-ttu-id="a1d52-323">This widget highlights when the last S3 scan was done and when the next one will start.</span><span class="sxs-lookup"><span data-stu-id="a1d52-323">This widget highlights when the last S3 scan was done and when the next one will start.</span></span>
- <span data-ttu-id="a1d52-324">Click the widget to open the S3 Scan Status report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-324">Click the widget to open the S3 Scan Status report.</span></span>

### <a name="storage-by-bucket"></a><span data-ttu-id="a1d52-325">Storage by Bucket</span><span class="sxs-lookup"><span data-stu-id="a1d52-325">Storage by Bucket</span></span>
<span data-ttu-id="a1d52-326">This widget highlights the percentage that each bucket storage class is using.</span><span class="sxs-lookup"><span data-stu-id="a1d52-326">This widget highlights the percentage that each bucket storage class is using.</span></span>
- <span data-ttu-id="a1d52-327">Click the widget to open the Distribution of S3 Size report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-327">Click the widget to open the Distribution of S3 Size report.</span></span> <span data-ttu-id="a1d52-328">The report helps you analyze your S3 size by bucket, top-level folder, storage class, and versioning state.</span><span class="sxs-lookup"><span data-stu-id="a1d52-328">The report helps you analyze your S3 size by bucket, top-level folder, storage class, and versioning state.</span></span>

### <a name="number-of-objects-by-bucket"></a><span data-ttu-id="a1d52-329">Number of Objects by Bucket</span><span class="sxs-lookup"><span data-stu-id="a1d52-329">Number of Objects by Bucket</span></span>
<span data-ttu-id="a1d52-330">This widget highlights the number of objects per bucket in actual number and percentage.</span><span class="sxs-lookup"><span data-stu-id="a1d52-330">This widget highlights the number of objects per bucket in actual number and percentage.</span></span> <span data-ttu-id="a1d52-331">Hover over the bucket to see the total objects.</span><span class="sxs-lookup"><span data-stu-id="a1d52-331">Hover over the bucket to see the total objects.</span></span>
- <span data-ttu-id="a1d52-332">Click the widget to open the Distribution of S3 Size report (Scan based).</span><span class="sxs-lookup"><span data-stu-id="a1d52-332">Click the widget to open the Distribution of S3 Size report (Scan based).</span></span>

## <a name="cloud-comparison-dashboard"></a><span data-ttu-id="a1d52-333">Cloud Comparison Dashboard</span><span class="sxs-lookup"><span data-stu-id="a1d52-333">Cloud Comparison Dashboard</span></span>
<span data-ttu-id="a1d52-334">The Cloud Comparison dashboard helps you compare costs from different cloud providers based on pricing, CPU type, and RAM size.</span><span class="sxs-lookup"><span data-stu-id="a1d52-334">The Cloud Comparison dashboard helps you compare costs from different cloud providers based on pricing, CPU type, and RAM size.</span></span>  
![Cloud Comparison dashboard](./media/dashboards/cloud-comparison-dashboard.png)

### <a name="ec2-cost-in-azure-by-instance-type"></a><span data-ttu-id="a1d52-336">EC2 Cost in Azure by Instance Type</span><span class="sxs-lookup"><span data-stu-id="a1d52-336">EC2 Cost in Azure by Instance Type</span></span>
<span data-ttu-id="a1d52-337">This widget highlights the last 30 days of usage in on-demand rates.</span><span class="sxs-lookup"><span data-stu-id="a1d52-337">This widget highlights the last 30 days of usage in on-demand rates.</span></span> <span data-ttu-id="a1d52-338">It compares the cost with the current Amazon EC2 cost vs the potential cost in Azure.</span><span class="sxs-lookup"><span data-stu-id="a1d52-338">It compares the cost with the current Amazon EC2 cost vs the potential cost in Azure.</span></span>
- <span data-ttu-id="a1d52-339">Hover over the bars to compare costs per instance type.</span><span class="sxs-lookup"><span data-stu-id="a1d52-339">Hover over the bars to compare costs per instance type.</span></span>
- <span data-ttu-id="a1d52-340">Click the widget to open the Porting Your Deployment – Cost Analysis report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-340">Click the widget to open the Porting Your Deployment – Cost Analysis report.</span></span>

### <a name="ec2-cost-in-azure"></a><span data-ttu-id="a1d52-341">EC2 Cost in Azure</span><span class="sxs-lookup"><span data-stu-id="a1d52-341">EC2 Cost in Azure</span></span>
<span data-ttu-id="a1d52-342">This widget shows your current Amazon EC2 costs and compares them to Azure.</span><span class="sxs-lookup"><span data-stu-id="a1d52-342">This widget shows your current Amazon EC2 costs and compares them to Azure.</span></span> <span data-ttu-id="a1d52-343">The comparison is based on the last 30 days of usage in on-demand rates.</span><span class="sxs-lookup"><span data-stu-id="a1d52-343">The comparison is based on the last 30 days of usage in on-demand rates.</span></span>
- <span data-ttu-id="a1d52-344">Click the widget to open the Porting Your Deployment - Cost Analysis report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-344">Click the widget to open the Porting Your Deployment - Cost Analysis report.</span></span>

### <a name="ec2azure-instance-type-mapping"></a><span data-ttu-id="a1d52-345">EC2/Azure Instance Type Mapping</span><span class="sxs-lookup"><span data-stu-id="a1d52-345">EC2/Azure Instance Type Mapping</span></span>
<span data-ttu-id="a1d52-346">This widget highlights the best mapping of elastic compute units between Amazon EC2 and Azure.</span><span class="sxs-lookup"><span data-stu-id="a1d52-346">This widget highlights the best mapping of elastic compute units between Amazon EC2 and Azure.</span></span>
- <span data-ttu-id="a1d52-347">Click the widget to open the Instances Type Mapping report.</span><span class="sxs-lookup"><span data-stu-id="a1d52-347">Click the widget to open the Instances Type Mapping report.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1d52-348">Next steps</span><span class="sxs-lookup"><span data-stu-id="a1d52-348">Next steps</span></span>
- <span data-ttu-id="a1d52-349">Read the [Use Cost Management reports](use-reports.md) article to learn more about reports.</span><span class="sxs-lookup"><span data-stu-id="a1d52-349">Read the [Use Cost Management reports](use-reports.md) article to learn more about reports.</span></span>
