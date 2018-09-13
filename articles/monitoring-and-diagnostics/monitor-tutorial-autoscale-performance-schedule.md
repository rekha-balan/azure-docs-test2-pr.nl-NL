---
title: Autoscale Azure resources based on performance data or a schedule
description: Create an autoscale setting for an app service plan using metric data and a schedule
author: anirudhcavale
services: azure-monitor
ms.service: azure-monitor
ms.topic: tutorial
ms.date: 12/11/2017
ms.author: ancav
ms.custom: mvc
ms.component: autoscale
ms.openlocfilehash: b63e1fa316e9ebeaa564731b8bb0bc3ed5ba9036
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966093"
---
# <a name="create-an-autoscale-setting-for--azure-resources-based-on-performance-data-or-a-schedule"></a><span data-ttu-id="e27f0-103">Create an Autoscale Setting for  Azure resources based on performance data or a schedule</span><span class="sxs-lookup"><span data-stu-id="e27f0-103">Create an Autoscale Setting for  Azure resources based on performance data or a schedule</span></span>

<span data-ttu-id="e27f0-104">Autoscale settings enable you to add/remove instances of service based on preset conditions.</span><span class="sxs-lookup"><span data-stu-id="e27f0-104">Autoscale settings enable you to add/remove instances of service based on preset conditions.</span></span> <span data-ttu-id="e27f0-105">These settings can be created through the portal.</span><span class="sxs-lookup"><span data-stu-id="e27f0-105">These settings can be created through the portal.</span></span> <span data-ttu-id="e27f0-106">This method provides a browser-based user interface for creating and configuring an autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="e27f0-106">This method provides a browser-based user interface for creating and configuring an autoscale setting.</span></span> 

<span data-ttu-id="e27f0-107">In this tutorial, you will</span><span class="sxs-lookup"><span data-stu-id="e27f0-107">In this tutorial, you will</span></span> 
> [!div class="checklist"]
> * <span data-ttu-id="e27f0-108">Create a Web App and App Service Plan</span><span class="sxs-lookup"><span data-stu-id="e27f0-108">Create a Web App and App Service Plan</span></span>
> * <span data-ttu-id="e27f0-109">Configure autoscale rules for scale-in and scale out based on the number of requests a Web App receives</span><span class="sxs-lookup"><span data-stu-id="e27f0-109">Configure autoscale rules for scale-in and scale out based on the number of requests a Web App receives</span></span>
> * <span data-ttu-id="e27f0-110">Trigger a scale-out action and watch the number of instances increase</span><span class="sxs-lookup"><span data-stu-id="e27f0-110">Trigger a scale-out action and watch the number of instances increase</span></span>
> * <span data-ttu-id="e27f0-111">Trigger a scale-in action and watch the number of instances decrease</span><span class="sxs-lookup"><span data-stu-id="e27f0-111">Trigger a scale-in action and watch the number of instances decrease</span></span>
> * <span data-ttu-id="e27f0-112">Clean up your resources</span><span class="sxs-lookup"><span data-stu-id="e27f0-112">Clean up your resources</span></span>

<span data-ttu-id="e27f0-113">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="e27f0-113">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="e27f0-114">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="e27f0-114">Log in to the Azure portal</span></span>

<span data-ttu-id="e27f0-115">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="e27f0-115">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-a-web-app-and-app-service-plan"></a><span data-ttu-id="e27f0-116">Create a Web App and App Service Plan</span><span class="sxs-lookup"><span data-stu-id="e27f0-116">Create a Web App and App Service Plan</span></span>
1. <span data-ttu-id="e27f0-117">Click the **Create a resource** option from the left-hand navigation pane.</span><span class="sxs-lookup"><span data-stu-id="e27f0-117">Click the **Create a resource** option from the left-hand navigation pane.</span></span>
2. <span data-ttu-id="e27f0-118">Search for and select the *Web App* item and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="e27f0-118">Search for and select the *Web App* item and click **Create**.</span></span>
3. <span data-ttu-id="e27f0-119">Select an app name like *MyTestScaleWebApp*.</span><span class="sxs-lookup"><span data-stu-id="e27f0-119">Select an app name like *MyTestScaleWebApp*.</span></span> <span data-ttu-id="e27f0-120">Create a new resource group \*myResourceGroup' and place it into the resource group of your choosing.</span><span class="sxs-lookup"><span data-stu-id="e27f0-120">Create a new resource group \*myResourceGroup' and place it into the resource group of your choosing.</span></span>

<span data-ttu-id="e27f0-121">Within a few minutes, your resources should be provisioned.</span><span class="sxs-lookup"><span data-stu-id="e27f0-121">Within a few minutes, your resources should be provisioned.</span></span> <span data-ttu-id="e27f0-122">Use the Web App and corresponding App Service Plan in the remainder of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e27f0-122">Use the Web App and corresponding App Service Plan in the remainder of this tutorial.</span></span>

   ![Create a new app service in the portal](./media/monitor-tutorial-autoscale-performance-schedule/Web-App-Create.png)

## <a name="navigate-to-autoscale-settings"></a><span data-ttu-id="e27f0-124">Navigate to Autoscale settings</span><span class="sxs-lookup"><span data-stu-id="e27f0-124">Navigate to Autoscale settings</span></span>
1. <span data-ttu-id="e27f0-125">From the left-hand navigation pane, select the **Monitor** option.</span><span class="sxs-lookup"><span data-stu-id="e27f0-125">From the left-hand navigation pane, select the **Monitor** option.</span></span> <span data-ttu-id="e27f0-126">Once the page loads, select the **Autoscale** tab.</span><span class="sxs-lookup"><span data-stu-id="e27f0-126">Once the page loads, select the **Autoscale** tab.</span></span>
2. <span data-ttu-id="e27f0-127">A list of the resources under your subscription that support autoscale are listed here.</span><span class="sxs-lookup"><span data-stu-id="e27f0-127">A list of the resources under your subscription that support autoscale are listed here.</span></span> <span data-ttu-id="e27f0-128">Identify the App Service Plan that was created earlier in the tutorial, and click on it.</span><span class="sxs-lookup"><span data-stu-id="e27f0-128">Identify the App Service Plan that was created earlier in the tutorial, and click on it.</span></span>

    ![Navigate to autoscale settings](./media/monitor-tutorial-autoscale-performance-schedule/monitor-blade-autoscale.png)

3. <span data-ttu-id="e27f0-130">On the autoscale setting, click the **Enable Autoscale** button.</span><span class="sxs-lookup"><span data-stu-id="e27f0-130">On the autoscale setting, click the **Enable Autoscale** button.</span></span>

<span data-ttu-id="e27f0-131">The next few steps help you fill the autoscale screen to look like following picture:</span><span class="sxs-lookup"><span data-stu-id="e27f0-131">The next few steps help you fill the autoscale screen to look like following picture:</span></span>

   ![Save autoscale setting](./media/monitor-tutorial-autoscale-performance-schedule/Autoscale-Setting-Save.png)

 ## <a name="configure-default-profile"></a><span data-ttu-id="e27f0-133">Configure default profile</span><span class="sxs-lookup"><span data-stu-id="e27f0-133">Configure default profile</span></span>
1. <span data-ttu-id="e27f0-134">Provide a **Name** for the autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="e27f0-134">Provide a **Name** for the autoscale setting.</span></span>
2. <span data-ttu-id="e27f0-135">In the default profile, ensure the **Scale mode** is set to 'Scale to a specific instance count'.</span><span class="sxs-lookup"><span data-stu-id="e27f0-135">In the default profile, ensure the **Scale mode** is set to 'Scale to a specific instance count'.</span></span>
3. <span data-ttu-id="e27f0-136">Set the instance count to **1**.</span><span class="sxs-lookup"><span data-stu-id="e27f0-136">Set the instance count to **1**.</span></span> <span data-ttu-id="e27f0-137">This setting ensures that when no other profile is active, or in effect, the default profile returns the instance count to 1.</span><span class="sxs-lookup"><span data-stu-id="e27f0-137">This setting ensures that when no other profile is active, or in effect, the default profile returns the instance count to 1.</span></span>

  ![Navigate to autoscale settings](./media/monitor-tutorial-autoscale-performance-schedule/autoscale-setting-profile.png)


## <a name="create-recurrance-profile"></a><span data-ttu-id="e27f0-139">Create recurrance profile</span><span class="sxs-lookup"><span data-stu-id="e27f0-139">Create recurrance profile</span></span>

1. <span data-ttu-id="e27f0-140">Click on the **Add a scale condition** link under the default profile.</span><span class="sxs-lookup"><span data-stu-id="e27f0-140">Click on the **Add a scale condition** link under the default profile.</span></span>

2. <span data-ttu-id="e27f0-141">Edit the **Name** of this profile to be 'Monday to Friday profile'.</span><span class="sxs-lookup"><span data-stu-id="e27f0-141">Edit the **Name** of this profile to be 'Monday to Friday profile'.</span></span>

3. <span data-ttu-id="e27f0-142">Ensure the **Scale mode** is set to 'Scale based on a metric'.</span><span class="sxs-lookup"><span data-stu-id="e27f0-142">Ensure the **Scale mode** is set to 'Scale based on a metric'.</span></span>

4. <span data-ttu-id="e27f0-143">For **Instance limits** set the **Minimum** as '1', the **Maximum** as '2' and the **Default** as '1'.</span><span class="sxs-lookup"><span data-stu-id="e27f0-143">For **Instance limits** set the **Minimum** as '1', the **Maximum** as '2' and the **Default** as '1'.</span></span> <span data-ttu-id="e27f0-144">This setting ensures that this profile does not autoscale the service plan to have less than 1 instance, or more than 2 instances.</span><span class="sxs-lookup"><span data-stu-id="e27f0-144">This setting ensures that this profile does not autoscale the service plan to have less than 1 instance, or more than 2 instances.</span></span> <span data-ttu-id="e27f0-145">If the profile does not have sufficient data to make a decision, it uses the default number of instances (in this case 1).</span><span class="sxs-lookup"><span data-stu-id="e27f0-145">If the profile does not have sufficient data to make a decision, it uses the default number of instances (in this case 1).</span></span>

5. <span data-ttu-id="e27f0-146">For **Schedule**, select 'Repeat specific days'.</span><span class="sxs-lookup"><span data-stu-id="e27f0-146">For **Schedule**, select 'Repeat specific days'.</span></span>

6. <span data-ttu-id="e27f0-147">Set the profile to repeat Monday through Friday, from 09:00 PST to 18:00 PST.</span><span class="sxs-lookup"><span data-stu-id="e27f0-147">Set the profile to repeat Monday through Friday, from 09:00 PST to 18:00 PST.</span></span> <span data-ttu-id="e27f0-148">This setting ensures that this profile is only active and applicable 9AM to 6PM, Monday through Friday.</span><span class="sxs-lookup"><span data-stu-id="e27f0-148">This setting ensures that this profile is only active and applicable 9AM to 6PM, Monday through Friday.</span></span> <span data-ttu-id="e27f0-149">During all other times, the 'Default' profile is the profile the autoscale setting uses.</span><span class="sxs-lookup"><span data-stu-id="e27f0-149">During all other times, the 'Default' profile is the profile the autoscale setting uses.</span></span>

## <a name="create-a-scale-out-rule"></a><span data-ttu-id="e27f0-150">Create a scale-out rule</span><span class="sxs-lookup"><span data-stu-id="e27f0-150">Create a scale-out rule</span></span>

1. <span data-ttu-id="e27f0-151">In the 'Monday to Friday profile'.</span><span class="sxs-lookup"><span data-stu-id="e27f0-151">In the 'Monday to Friday profile'.</span></span>

2. <span data-ttu-id="e27f0-152">Click the **Add a rule** link.</span><span class="sxs-lookup"><span data-stu-id="e27f0-152">Click the **Add a rule** link.</span></span>

3. <span data-ttu-id="e27f0-153">Set the **Metric source** to be 'other resource'.</span><span class="sxs-lookup"><span data-stu-id="e27f0-153">Set the **Metric source** to be 'other resource'.</span></span> <span data-ttu-id="e27f0-154">Set the **Resource type** as 'App Services' and the **Resource** as the Web App created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e27f0-154">Set the **Resource type** as 'App Services' and the **Resource** as the Web App created earlier in this tutorial.</span></span>

4. <span data-ttu-id="e27f0-155">Set the **Time aggregation** as 'Total', the **Metric name** as 'Requests', and the **Time grain statistic** as 'Sum'.</span><span class="sxs-lookup"><span data-stu-id="e27f0-155">Set the **Time aggregation** as 'Total', the **Metric name** as 'Requests', and the **Time grain statistic** as 'Sum'.</span></span>

5. <span data-ttu-id="e27f0-156">Set the **Operator** as 'Greater than', the **Threshold** as '10' and the **Duration** as '5' minutes.</span><span class="sxs-lookup"><span data-stu-id="e27f0-156">Set the **Operator** as 'Greater than', the **Threshold** as '10' and the **Duration** as '5' minutes.</span></span>

6. <span data-ttu-id="e27f0-157">Select the **Operation** as 'Increase count by', the **Instance count** as '1', and the **Cool down** as '5' minutes.</span><span class="sxs-lookup"><span data-stu-id="e27f0-157">Select the **Operation** as 'Increase count by', the **Instance count** as '1', and the **Cool down** as '5' minutes.</span></span>

7. <span data-ttu-id="e27f0-158">Click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e27f0-158">Click the **Add** button.</span></span>

<span data-ttu-id="e27f0-159">This rule ensures that if your Web App receives more than 10 requests within 5 minutes or less, one additional instance is added to your App Service Plan to manage load.</span><span class="sxs-lookup"><span data-stu-id="e27f0-159">This rule ensures that if your Web App receives more than 10 requests within 5 minutes or less, one additional instance is added to your App Service Plan to manage load.</span></span>

   ![Create a scale-out rule](./media/monitor-tutorial-autoscale-performance-schedule/Scale-Out-Rule.png)

## <a name="create-a-scale-in-rule"></a><span data-ttu-id="e27f0-161">Create a scale-in rule</span><span class="sxs-lookup"><span data-stu-id="e27f0-161">Create a scale-in rule</span></span>
<span data-ttu-id="e27f0-162">We recommended you always to have a scale-in rule to accompany a scale-out rule.</span><span class="sxs-lookup"><span data-stu-id="e27f0-162">We recommended you always to have a scale-in rule to accompany a scale-out rule.</span></span> <span data-ttu-id="e27f0-163">Having both ensures that your resources are not over provisioned.</span><span class="sxs-lookup"><span data-stu-id="e27f0-163">Having both ensures that your resources are not over provisioned.</span></span> <span data-ttu-id="e27f0-164">Over provisioning means you have more instances running than needed to handle the current load.</span><span class="sxs-lookup"><span data-stu-id="e27f0-164">Over provisioning means you have more instances running than needed to handle the current load.</span></span> 

1. <span data-ttu-id="e27f0-165">In the 'Monday to Friday profile'.</span><span class="sxs-lookup"><span data-stu-id="e27f0-165">In the 'Monday to Friday profile'.</span></span>

2. <span data-ttu-id="e27f0-166">Click the **Add a rule** link.</span><span class="sxs-lookup"><span data-stu-id="e27f0-166">Click the **Add a rule** link.</span></span>

3. <span data-ttu-id="e27f0-167">Set the **Metric source** to be 'other resource'.</span><span class="sxs-lookup"><span data-stu-id="e27f0-167">Set the **Metric source** to be 'other resource'.</span></span> <span data-ttu-id="e27f0-168">Set the **Resource type** as 'App Services' and the **Resource** as the Web App created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e27f0-168">Set the **Resource type** as 'App Services' and the **Resource** as the Web App created earlier in this tutorial.</span></span>

4. <span data-ttu-id="e27f0-169">Set the **Time aggregation** as 'Total', the **Metric name** as 'Requests', and the **Time grain statistic** as 'Average'.</span><span class="sxs-lookup"><span data-stu-id="e27f0-169">Set the **Time aggregation** as 'Total', the **Metric name** as 'Requests', and the **Time grain statistic** as 'Average'.</span></span>

5. <span data-ttu-id="e27f0-170">Set the **Operator** as 'Less than', the **Threshold** as '5' and the **Duration** as '5' minutes.</span><span class="sxs-lookup"><span data-stu-id="e27f0-170">Set the **Operator** as 'Less than', the **Threshold** as '5' and the **Duration** as '5' minutes.</span></span>

6. <span data-ttu-id="e27f0-171">Select the **Operation** as 'Decrease count by', the **Instance count** as '1', and the **Cool down** as '5' minutes.</span><span class="sxs-lookup"><span data-stu-id="e27f0-171">Select the **Operation** as 'Decrease count by', the **Instance count** as '1', and the **Cool down** as '5' minutes.</span></span>

7. <span data-ttu-id="e27f0-172">Click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="e27f0-172">Click the **Add** button.</span></span>

    ![Create a scale-in rule](./media/monitor-tutorial-autoscale-performance-schedule/Scale-In-Rule.png)

8. <span data-ttu-id="e27f0-174">**Save** the autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="e27f0-174">**Save** the autoscale setting.</span></span>

    ![Save autoscale setting](./media/monitor-tutorial-autoscale-performance-schedule/Autoscale-Setting-Save.png)

## <a name="trigger-scale-out-action"></a><span data-ttu-id="e27f0-176">Trigger scale-out action</span><span class="sxs-lookup"><span data-stu-id="e27f0-176">Trigger scale-out action</span></span>
<span data-ttu-id="e27f0-177">To trigger the scale-out condition in the autoscale setting just created, the Web App must have more than 10 requests in less than 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="e27f0-177">To trigger the scale-out condition in the autoscale setting just created, the Web App must have more than 10 requests in less than 5 minutes.</span></span>

1. <span data-ttu-id="e27f0-178">Open a browser window and navigate to the Web App created earlier in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e27f0-178">Open a browser window and navigate to the Web App created earlier in this tutorial.</span></span> <span data-ttu-id="e27f0-179">You can find the URL for your Web App in the Azure Portal by navigating to your Web App resource and clicking on the **Browse** button in the 'Overview' tab.</span><span class="sxs-lookup"><span data-stu-id="e27f0-179">You can find the URL for your Web App in the Azure Portal by navigating to your Web App resource and clicking on the **Browse** button in the 'Overview' tab.</span></span>

2. <span data-ttu-id="e27f0-180">In quick succession, reload the page more than 10 times.</span><span class="sxs-lookup"><span data-stu-id="e27f0-180">In quick succession, reload the page more than 10 times.</span></span>

3. <span data-ttu-id="e27f0-181">From the left-hand navigation pane, select the **Monitor** option.</span><span class="sxs-lookup"><span data-stu-id="e27f0-181">From the left-hand navigation pane, select the **Monitor** option.</span></span> <span data-ttu-id="e27f0-182">Once the page loads select the **Autoscale** tab.</span><span class="sxs-lookup"><span data-stu-id="e27f0-182">Once the page loads select the **Autoscale** tab.</span></span>

4. <span data-ttu-id="e27f0-183">From the list, select the App Service Plan used throughout this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e27f0-183">From the list, select the App Service Plan used throughout this tutorial.</span></span>

5. <span data-ttu-id="e27f0-184">On the autoscale setting, click the **Run history** tab.</span><span class="sxs-lookup"><span data-stu-id="e27f0-184">On the autoscale setting, click the **Run history** tab.</span></span>

6. <span data-ttu-id="e27f0-185">You see a chart reflecting the instance count of the App Service Plan over time.</span><span class="sxs-lookup"><span data-stu-id="e27f0-185">You see a chart reflecting the instance count of the App Service Plan over time.</span></span>

7. <span data-ttu-id="e27f0-186">In a few minutes, the instance count should rise from 1, to 2.</span><span class="sxs-lookup"><span data-stu-id="e27f0-186">In a few minutes, the instance count should rise from 1, to 2.</span></span>

8. <span data-ttu-id="e27f0-187">Under the chart, you see the activity log entries for each scale action taken by this autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="e27f0-187">Under the chart, you see the activity log entries for each scale action taken by this autoscale setting.</span></span>

## <a name="trigger-scale-in-action"></a><span data-ttu-id="e27f0-188">Trigger scale-in action</span><span class="sxs-lookup"><span data-stu-id="e27f0-188">Trigger scale-in action</span></span>
<span data-ttu-id="e27f0-189">The scale-in condition in the autoscale setting triggers if there are fewer than 5 requests to the Web App over a period of 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="e27f0-189">The scale-in condition in the autoscale setting triggers if there are fewer than 5 requests to the Web App over a period of 10 minutes.</span></span> 

1. <span data-ttu-id="e27f0-190">Ensure no requests are being sent to your Web App.</span><span class="sxs-lookup"><span data-stu-id="e27f0-190">Ensure no requests are being sent to your Web App.</span></span>

2. <span data-ttu-id="e27f0-191">Load the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="e27f0-191">Load the Azure Portal.</span></span>

3. <span data-ttu-id="e27f0-192">From the left-hand navigation pane, select the **Monitor** option.</span><span class="sxs-lookup"><span data-stu-id="e27f0-192">From the left-hand navigation pane, select the **Monitor** option.</span></span> <span data-ttu-id="e27f0-193">Once the page loads select the **Autoscale** tab.</span><span class="sxs-lookup"><span data-stu-id="e27f0-193">Once the page loads select the **Autoscale** tab.</span></span>

4. <span data-ttu-id="e27f0-194">From the list, select the App Service Plan used throughout this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e27f0-194">From the list, select the App Service Plan used throughout this tutorial.</span></span>

5. <span data-ttu-id="e27f0-195">On the autoscale setting, click the **Run history** tab.</span><span class="sxs-lookup"><span data-stu-id="e27f0-195">On the autoscale setting, click the **Run history** tab.</span></span>

6. <span data-ttu-id="e27f0-196">You see a chart reflecting the instance count of the App Service Plan over time.</span><span class="sxs-lookup"><span data-stu-id="e27f0-196">You see a chart reflecting the instance count of the App Service Plan over time.</span></span>

7. <span data-ttu-id="e27f0-197">In a few minutes, the instance count should drop from 2, to 1.</span><span class="sxs-lookup"><span data-stu-id="e27f0-197">In a few minutes, the instance count should drop from 2, to 1.</span></span> <span data-ttu-id="e27f0-198">The process takes at least 100 minutes.</span><span class="sxs-lookup"><span data-stu-id="e27f0-198">The process takes at least 100 minutes.</span></span>  

8. <span data-ttu-id="e27f0-199">Under the chart, are the corresponding set of activity log entries for each scale action taken by this autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="e27f0-199">Under the chart, are the corresponding set of activity log entries for each scale action taken by this autoscale setting.</span></span>

    ![View scale-in actions](./media/monitor-tutorial-autoscale-performance-schedule/Scale-In-Chart.png)

## <a name="clean-up-resources"></a><span data-ttu-id="e27f0-201">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="e27f0-201">Clean up resources</span></span>

1. <span data-ttu-id="e27f0-202">From the left-hand menu in the Azure portal, click **All resources** and then select the Web App created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="e27f0-202">From the left-hand menu in the Azure portal, click **All resources** and then select the Web App created in this tutorial.</span></span>

2. <span data-ttu-id="e27f0-203">On your resource page, click **Delete**, confirm delete by typing **yes** in the text box, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e27f0-203">On your resource page, click **Delete**, confirm delete by typing **yes** in the text box, and then click **Delete**.</span></span>

3. <span data-ttu-id="e27f0-204">Then select the App Service Plan resource and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e27f0-204">Then select the App Service Plan resource and click **Delete**.</span></span>

4. <span data-ttu-id="e27f0-205">Confirm delete by typing **yes** in the text box, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e27f0-205">Confirm delete by typing **yes** in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e27f0-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="e27f0-206">Next steps</span></span>

<span data-ttu-id="e27f0-207">In this tutorial, you</span><span class="sxs-lookup"><span data-stu-id="e27f0-207">In this tutorial, you</span></span>  
> [!div class="checklist"]
> * <span data-ttu-id="e27f0-208">Created a Web App and App Service Plan</span><span class="sxs-lookup"><span data-stu-id="e27f0-208">Created a Web App and App Service Plan</span></span>
> * <span data-ttu-id="e27f0-209">Configured autoscale rules for scale-in and scale out based on the number of requests the Web App received</span><span class="sxs-lookup"><span data-stu-id="e27f0-209">Configured autoscale rules for scale-in and scale out based on the number of requests the Web App received</span></span>
> * <span data-ttu-id="e27f0-210">Triggered a scale-out action and watched the number of instances increase</span><span class="sxs-lookup"><span data-stu-id="e27f0-210">Triggered a scale-out action and watched the number of instances increase</span></span>
> * <span data-ttu-id="e27f0-211">Triggered a scale-in action and watched the number of instances decrease</span><span class="sxs-lookup"><span data-stu-id="e27f0-211">Triggered a scale-in action and watched the number of instances decrease</span></span>
> * <span data-ttu-id="e27f0-212">Cleaned up your resources</span><span class="sxs-lookup"><span data-stu-id="e27f0-212">Cleaned up your resources</span></span>


<span data-ttu-id="e27f0-213">To learn more about autoscale settings, continue on to the [autoscale overview](monitoring-overview-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="e27f0-213">To learn more about autoscale settings, continue on to the [autoscale overview](monitoring-overview-autoscale.md).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e27f0-214">Archive your monitoring data</span><span class="sxs-lookup"><span data-stu-id="e27f0-214">Archive your monitoring data</span></span>](monitor-tutorial-archive-monitoring-data.md)
