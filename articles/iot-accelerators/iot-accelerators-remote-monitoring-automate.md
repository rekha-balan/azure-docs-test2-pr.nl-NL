---
title: Detect device issues in an Azure-based remote monitoring solution tutorial | Microsoft Docs
description: This tutorial shows you how to use rules and actions to automatically detect threshold-based device issues in the Remote Monitoring solution.
author: dominicbetts
manager: timlt
ms.author: dobett
ms.service: iot-accelerators
services: iot-accelerators
ms.date: 07/19/2018
ms.topic: tutorial
ms.custom: mvc
ms.openlocfilehash: 6759568a678394f7cec4ac9f0bdd99d8ed1db9de
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857884"
---
# <a name="tutorial-detect-issues-with-devices-connected-to-your-monitoring-solution"></a><span data-ttu-id="b796b-103">Tutorial: Detect issues with devices connected to your monitoring solution</span><span class="sxs-lookup"><span data-stu-id="b796b-103">Tutorial: Detect issues with devices connected to your monitoring solution</span></span>

<span data-ttu-id="b796b-104">In this tutorial, you configure the Remote Monitoring solution accelerator to detect issues with your connected IoT devices.</span><span class="sxs-lookup"><span data-stu-id="b796b-104">In this tutorial, you configure the Remote Monitoring solution accelerator to detect issues with your connected IoT devices.</span></span> <span data-ttu-id="b796b-105">To detect the issues with your devices, you add rules that generate alerts on the solution dashboard.</span><span class="sxs-lookup"><span data-stu-id="b796b-105">To detect the issues with your devices, you add rules that generate alerts on the solution dashboard.</span></span>

<span data-ttu-id="b796b-106">To introduce rules and alerts, the tutorial uses a simulated chiller device.</span><span class="sxs-lookup"><span data-stu-id="b796b-106">To introduce rules and alerts, the tutorial uses a simulated chiller device.</span></span> <span data-ttu-id="b796b-107">The chiller is managed by an organization called Contoso and is connected to the Remote Monitoring solution accelerator.</span><span class="sxs-lookup"><span data-stu-id="b796b-107">The chiller is managed by an organization called Contoso and is connected to the Remote Monitoring solution accelerator.</span></span> <span data-ttu-id="b796b-108">Contoso already has a rule that generates a critical alert when the pressure in a chiller goes above 298 PSI.</span><span class="sxs-lookup"><span data-stu-id="b796b-108">Contoso already has a rule that generates a critical alert when the pressure in a chiller goes above 298 PSI.</span></span> <span data-ttu-id="b796b-109">As an operator at Contoso, you want to identify chiller devices that may have problematic sensors by looking for initial pressure spikes.</span><span class="sxs-lookup"><span data-stu-id="b796b-109">As an operator at Contoso, you want to identify chiller devices that may have problematic sensors by looking for initial pressure spikes.</span></span> <span data-ttu-id="b796b-110">To identify such devices, you add a rule that generates a warning alert when the pressure in the chiller goes above 150 PSI.</span><span class="sxs-lookup"><span data-stu-id="b796b-110">To identify such devices, you add a rule that generates a warning alert when the pressure in the chiller goes above 150 PSI.</span></span>

<span data-ttu-id="b796b-111">You have also been asked to create a critical alert for a chiller when, over the last five minutes, the average humidity in the device was greater than 80% and the temperature of the device was greater than 75 degrees fahrenheit.</span><span class="sxs-lookup"><span data-stu-id="b796b-111">You have also been asked to create a critical alert for a chiller when, over the last five minutes, the average humidity in the device was greater than 80% and the temperature of the device was greater than 75 degrees fahrenheit.</span></span>

<span data-ttu-id="b796b-112">In this tutorial, you:</span><span class="sxs-lookup"><span data-stu-id="b796b-112">In this tutorial, you:</span></span>

>[!div class="checklist"]
> * <span data-ttu-id="b796b-113">View the rules in your solution</span><span class="sxs-lookup"><span data-stu-id="b796b-113">View the rules in your solution</span></span>
> * <span data-ttu-id="b796b-114">Create a rule</span><span class="sxs-lookup"><span data-stu-id="b796b-114">Create a rule</span></span>
> * <span data-ttu-id="b796b-115">Create a rule with multiple conditions</span><span class="sxs-lookup"><span data-stu-id="b796b-115">Create a rule with multiple conditions</span></span>
> * <span data-ttu-id="b796b-116">Edit an existing rule</span><span class="sxs-lookup"><span data-stu-id="b796b-116">Edit an existing rule</span></span>
> * <span data-ttu-id="b796b-117">Switch rules on and off</span><span class="sxs-lookup"><span data-stu-id="b796b-117">Switch rules on and off</span></span>

<span data-ttu-id="b796b-118">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="b796b-118">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [iot-accelerators-tutorial-prereqs](../../includes/iot-accelerators-tutorial-prereqs.md)]

## <a name="review-the-existing-rules"></a><span data-ttu-id="b796b-119">Review the existing rules</span><span class="sxs-lookup"><span data-stu-id="b796b-119">Review the existing rules</span></span>

<span data-ttu-id="b796b-120">The **Rules** page in the solution accelerator displays a list of all the current rules:</span><span class="sxs-lookup"><span data-stu-id="b796b-120">The **Rules** page in the solution accelerator displays a list of all the current rules:</span></span>

<span data-ttu-id="b796b-121">[![Rules page](./media/iot-accelerators-remote-monitoring-automate/rulesactions_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactions_v2-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="b796b-121">[![Rules page](./media/iot-accelerators-remote-monitoring-automate/rulesactions_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactions_v2-expanded.png#lightbox)</span></span>

<span data-ttu-id="b796b-122">To view only the rules that apply to chiller devices, apply a filter.</span><span class="sxs-lookup"><span data-stu-id="b796b-122">To view only the rules that apply to chiller devices, apply a filter.</span></span> <span data-ttu-id="b796b-123">You can view more information about a rule and edit it when you select it in the list:</span><span class="sxs-lookup"><span data-stu-id="b796b-123">You can view more information about a rule and edit it when you select it in the list:</span></span>

<span data-ttu-id="b796b-124">[![View rule details](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdetail_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdetail_v2-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="b796b-124">[![View rule details](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdetail_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdetail_v2-expanded.png#lightbox)</span></span>

## <a name="create-a-rule"></a><span data-ttu-id="b796b-125">Create a rule</span><span class="sxs-lookup"><span data-stu-id="b796b-125">Create a rule</span></span>

<span data-ttu-id="b796b-126">To create a rule that generates a warning when the pressure in a chiller device goes above 150 PSI, click **New rule**.</span><span class="sxs-lookup"><span data-stu-id="b796b-126">To create a rule that generates a warning when the pressure in a chiller device goes above 150 PSI, click **New rule**.</span></span> <span data-ttu-id="b796b-127">Use the following values to create the rule:</span><span class="sxs-lookup"><span data-stu-id="b796b-127">Use the following values to create the rule:</span></span>

| <span data-ttu-id="b796b-128">Setting</span><span class="sxs-lookup"><span data-stu-id="b796b-128">Setting</span></span>          | <span data-ttu-id="b796b-129">Value</span><span class="sxs-lookup"><span data-stu-id="b796b-129">Value</span></span>                                 |
| ---------------- | ------------------------------------- |
| <span data-ttu-id="b796b-130">Rule name</span><span class="sxs-lookup"><span data-stu-id="b796b-130">Rule name</span></span>        | <span data-ttu-id="b796b-131">Chiller warning</span><span class="sxs-lookup"><span data-stu-id="b796b-131">Chiller warning</span></span>                       |
| <span data-ttu-id="b796b-132">Description</span><span class="sxs-lookup"><span data-stu-id="b796b-132">Description</span></span>      | <span data-ttu-id="b796b-133">Chiller pressure has exceeded 150 PSI</span><span class="sxs-lookup"><span data-stu-id="b796b-133">Chiller pressure has exceeded 150 PSI</span></span> |
| <span data-ttu-id="b796b-134">Device group</span><span class="sxs-lookup"><span data-stu-id="b796b-134">Device group</span></span>     | <span data-ttu-id="b796b-135">**Chillers** device group</span><span class="sxs-lookup"><span data-stu-id="b796b-135">**Chillers** device group</span></span>             |
| <span data-ttu-id="b796b-136">Calculation</span><span class="sxs-lookup"><span data-stu-id="b796b-136">Calculation</span></span>      | <span data-ttu-id="b796b-137">Instant</span><span class="sxs-lookup"><span data-stu-id="b796b-137">Instant</span></span>                               |
| <span data-ttu-id="b796b-138">Condition 1 Field</span><span class="sxs-lookup"><span data-stu-id="b796b-138">Condition 1 Field</span></span>| <span data-ttu-id="b796b-139">pressure</span><span class="sxs-lookup"><span data-stu-id="b796b-139">pressure</span></span>                              |
| <span data-ttu-id="b796b-140">Condition 1 operator</span><span class="sxs-lookup"><span data-stu-id="b796b-140">Condition 1 operator</span></span> | <span data-ttu-id="b796b-141">Greater than</span><span class="sxs-lookup"><span data-stu-id="b796b-141">Greater than</span></span>                      |
| <span data-ttu-id="b796b-142">Condition 1 value</span><span class="sxs-lookup"><span data-stu-id="b796b-142">Condition 1 value</span></span>    | <span data-ttu-id="b796b-143">150</span><span class="sxs-lookup"><span data-stu-id="b796b-143">150</span></span>                               |
| <span data-ttu-id="b796b-144">Severity level</span><span class="sxs-lookup"><span data-stu-id="b796b-144">Severity level</span></span>  | <span data-ttu-id="b796b-145">Warning</span><span class="sxs-lookup"><span data-stu-id="b796b-145">Warning</span></span>                               |

<span data-ttu-id="b796b-146">[![Create warning rule](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_v2-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="b796b-146">[![Create warning rule](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_v2-expanded.png#lightbox)</span></span>

<span data-ttu-id="b796b-147">To save the new rule, click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="b796b-147">To save the new rule, click **Apply**.</span></span>

<span data-ttu-id="b796b-148">You can see when the rule is triggered on the **Rules** page or on the **Dashboard** page:</span><span class="sxs-lookup"><span data-stu-id="b796b-148">You can see when the rule is triggered on the **Rules** page or on the **Dashboard** page:</span></span>

<span data-ttu-id="b796b-149">[![Warning rule triggered](./media/iot-accelerators-remote-monitoring-automate/warningruletriggered-inline.png)](./media/iot-accelerators-remote-monitoring-automate/warningruletriggered-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="b796b-149">[![Warning rule triggered](./media/iot-accelerators-remote-monitoring-automate/warningruletriggered-inline.png)](./media/iot-accelerators-remote-monitoring-automate/warningruletriggered-expanded.png#lightbox)</span></span>

## <a name="create-an-advanced-rule"></a><span data-ttu-id="b796b-150">Create an advanced rule</span><span class="sxs-lookup"><span data-stu-id="b796b-150">Create an advanced rule</span></span>

<span data-ttu-id="b796b-151">To create a rule with multiple conditions that generates a critical alert when, over the last five minutes for a chiller device, the average humidity is greater than 80% and the average temperature is greater than 75 degrees fahrenheit, click **New rule**.</span><span class="sxs-lookup"><span data-stu-id="b796b-151">To create a rule with multiple conditions that generates a critical alert when, over the last five minutes for a chiller device, the average humidity is greater than 80% and the average temperature is greater than 75 degrees fahrenheit, click **New rule**.</span></span> <span data-ttu-id="b796b-152">Use the following values to create the rule:</span><span class="sxs-lookup"><span data-stu-id="b796b-152">Use the following values to create the rule:</span></span>

| <span data-ttu-id="b796b-153">Setting</span><span class="sxs-lookup"><span data-stu-id="b796b-153">Setting</span></span>          | <span data-ttu-id="b796b-154">Value</span><span class="sxs-lookup"><span data-stu-id="b796b-154">Value</span></span>                                 |
| ---------------- | ------------------------------------- |
| <span data-ttu-id="b796b-155">Rule name</span><span class="sxs-lookup"><span data-stu-id="b796b-155">Rule name</span></span>        | <span data-ttu-id="b796b-156">Chiller humidity and temp critical</span><span class="sxs-lookup"><span data-stu-id="b796b-156">Chiller humidity and temp critical</span></span>    |
| <span data-ttu-id="b796b-157">Description</span><span class="sxs-lookup"><span data-stu-id="b796b-157">Description</span></span>      | <span data-ttu-id="b796b-158">Humidity and temperature are critical</span><span class="sxs-lookup"><span data-stu-id="b796b-158">Humidity and temperature are critical</span></span> |
| <span data-ttu-id="b796b-159">Device group</span><span class="sxs-lookup"><span data-stu-id="b796b-159">Device group</span></span>     | <span data-ttu-id="b796b-160">**Chillers** device group</span><span class="sxs-lookup"><span data-stu-id="b796b-160">**Chillers** device group</span></span>             |
| <span data-ttu-id="b796b-161">Calculation</span><span class="sxs-lookup"><span data-stu-id="b796b-161">Calculation</span></span>      | <span data-ttu-id="b796b-162">Average</span><span class="sxs-lookup"><span data-stu-id="b796b-162">Average</span></span>                               |
| <span data-ttu-id="b796b-163">Time period</span><span class="sxs-lookup"><span data-stu-id="b796b-163">Time period</span></span>      | <span data-ttu-id="b796b-164">5</span><span class="sxs-lookup"><span data-stu-id="b796b-164">5</span></span>                                     |
| <span data-ttu-id="b796b-165">Condition 1 Field</span><span class="sxs-lookup"><span data-stu-id="b796b-165">Condition 1 Field</span></span>| <span data-ttu-id="b796b-166">humidity</span><span class="sxs-lookup"><span data-stu-id="b796b-166">humidity</span></span>                              |
| <span data-ttu-id="b796b-167">Condition 1 operator</span><span class="sxs-lookup"><span data-stu-id="b796b-167">Condition 1 operator</span></span> | <span data-ttu-id="b796b-168">Greater than</span><span class="sxs-lookup"><span data-stu-id="b796b-168">Greater than</span></span>                      |
| <span data-ttu-id="b796b-169">Condition 1 value</span><span class="sxs-lookup"><span data-stu-id="b796b-169">Condition 1 value</span></span>    | <span data-ttu-id="b796b-170">80</span><span class="sxs-lookup"><span data-stu-id="b796b-170">80</span></span>                                |
| <span data-ttu-id="b796b-171">Severity level</span><span class="sxs-lookup"><span data-stu-id="b796b-171">Severity level</span></span>  | <span data-ttu-id="b796b-172">Critical</span><span class="sxs-lookup"><span data-stu-id="b796b-172">Critical</span></span>                              |

<span data-ttu-id="b796b-173">[![Create multiple condition rule part one](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_mult_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_mult_v2-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="b796b-173">[![Create multiple condition rule part one](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_mult_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_mult_v2-expanded.png#lightbox)</span></span>

<span data-ttu-id="b796b-174">To add the second condition, click on "+ Add condition".</span><span class="sxs-lookup"><span data-stu-id="b796b-174">To add the second condition, click on "+ Add condition".</span></span> <span data-ttu-id="b796b-175">Use the following values for the new condition:</span><span class="sxs-lookup"><span data-stu-id="b796b-175">Use the following values for the new condition:</span></span>

| <span data-ttu-id="b796b-176">Setting</span><span class="sxs-lookup"><span data-stu-id="b796b-176">Setting</span></span>          | <span data-ttu-id="b796b-177">Value</span><span class="sxs-lookup"><span data-stu-id="b796b-177">Value</span></span>                                 |
| ---------------- | ------------------------------------- |
| <span data-ttu-id="b796b-178">Condition 2 Field</span><span class="sxs-lookup"><span data-stu-id="b796b-178">Condition 2 Field</span></span>| <span data-ttu-id="b796b-179">temperature</span><span class="sxs-lookup"><span data-stu-id="b796b-179">temperature</span></span>                           |
| <span data-ttu-id="b796b-180">Condition 2 operator</span><span class="sxs-lookup"><span data-stu-id="b796b-180">Condition 2 operator</span></span> | <span data-ttu-id="b796b-181">Greater than</span><span class="sxs-lookup"><span data-stu-id="b796b-181">Greater than</span></span>                      |
| <span data-ttu-id="b796b-182">Condition 2 value</span><span class="sxs-lookup"><span data-stu-id="b796b-182">Condition 2 value</span></span>    | <span data-ttu-id="b796b-183">75</span><span class="sxs-lookup"><span data-stu-id="b796b-183">75</span></span>                                |

<span data-ttu-id="b796b-184">[![Create multiple condition rule part two](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_mult_cond2_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_mult_cond2_v2-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="b796b-184">[![Create multiple condition rule part two](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_mult_cond2_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsnewrule_mult_cond2_v2-expanded.png#lightbox)</span></span>

<span data-ttu-id="b796b-185">To save the new rule, click **Apply**.</span><span class="sxs-lookup"><span data-stu-id="b796b-185">To save the new rule, click **Apply**.</span></span>

<span data-ttu-id="b796b-186">You can see when the rule is triggered on the **Rules** page or on the **Dashboard** page:</span><span class="sxs-lookup"><span data-stu-id="b796b-186">You can see when the rule is triggered on the **Rules** page or on the **Dashboard** page:</span></span>

<span data-ttu-id="b796b-187">[![Multiple condition rule triggered](./media/iot-accelerators-remote-monitoring-automate/criticalruletriggered-inline.png)](./media/iot-accelerators-remote-monitoring-automate/criticalruletriggered-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="b796b-187">[![Multiple condition rule triggered](./media/iot-accelerators-remote-monitoring-automate/criticalruletriggered-inline.png)](./media/iot-accelerators-remote-monitoring-automate/criticalruletriggered-expanded.png#lightbox)</span></span>

## <a name="edit-an-existing-rule"></a><span data-ttu-id="b796b-188">Edit an existing rule</span><span class="sxs-lookup"><span data-stu-id="b796b-188">Edit an existing rule</span></span>

<span data-ttu-id="b796b-189">To make a change to an existing rule, select it in the list of rules, and click **Edit**:</span><span class="sxs-lookup"><span data-stu-id="b796b-189">To make a change to an existing rule, select it in the list of rules, and click **Edit**:</span></span>

<span data-ttu-id="b796b-190">[![Edit rule](./media/iot-accelerators-remote-monitoring-automate/rulesactionsedit_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsedit_v2-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="b796b-190">[![Edit rule](./media/iot-accelerators-remote-monitoring-automate/rulesactionsedit_v2-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsedit_v2-expanded.png#lightbox)</span></span>

## <a name="disable-a-rule"></a><span data-ttu-id="b796b-191">Disable a rule</span><span class="sxs-lookup"><span data-stu-id="b796b-191">Disable a rule</span></span>

<span data-ttu-id="b796b-192">To temporarily switch off a rule, you can disable it in the list of rules.</span><span class="sxs-lookup"><span data-stu-id="b796b-192">To temporarily switch off a rule, you can disable it in the list of rules.</span></span> <span data-ttu-id="b796b-193">Select the rule to disable, and then choose **Disable**.</span><span class="sxs-lookup"><span data-stu-id="b796b-193">Select the rule to disable, and then choose **Disable**.</span></span> <span data-ttu-id="b796b-194">The **Status** of the rule in the list changes to indicate the rule is now disabled.</span><span class="sxs-lookup"><span data-stu-id="b796b-194">The **Status** of the rule in the list changes to indicate the rule is now disabled.</span></span> <span data-ttu-id="b796b-195">You can re-enable a rule that you previously disabled using the same procedure.</span><span class="sxs-lookup"><span data-stu-id="b796b-195">You can re-enable a rule that you previously disabled using the same procedure.</span></span>

<span data-ttu-id="b796b-196">[![Disable rule](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdisable-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdisable-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="b796b-196">[![Disable rule](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdisable-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdisable-expanded.png#lightbox)</span></span>

<span data-ttu-id="b796b-197">You can enable and disable multiple rules at the same time by selecting multiple rules in the list.</span><span class="sxs-lookup"><span data-stu-id="b796b-197">You can enable and disable multiple rules at the same time by selecting multiple rules in the list.</span></span>

## <a name="delete-a-rule"></a><span data-ttu-id="b796b-198">Delete a rule</span><span class="sxs-lookup"><span data-stu-id="b796b-198">Delete a rule</span></span>

<span data-ttu-id="b796b-199">To permanently delete a rule, you can delete it in the list of rules.</span><span class="sxs-lookup"><span data-stu-id="b796b-199">To permanently delete a rule, you can delete it in the list of rules.</span></span> <span data-ttu-id="b796b-200">Select the rule to delete, and then choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="b796b-200">Select the rule to delete, and then choose **Delete**.</span></span>

<span data-ttu-id="b796b-201">[![Delete rule](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdelete-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdelete-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="b796b-201">[![Delete rule](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdelete-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdelete-expanded.png#lightbox)</span></span>

<span data-ttu-id="b796b-202">After you confirm that you want to delete the rule, you are given the opportunity to delete any alerts associated with the rule from the **Maintenance** page.</span><span class="sxs-lookup"><span data-stu-id="b796b-202">After you confirm that you want to delete the rule, you are given the opportunity to delete any alerts associated with the rule from the **Maintenance** page.</span></span>

<span data-ttu-id="b796b-203">[![Delete rule](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdeletetidy-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdeletetidy-expanded.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="b796b-203">[![Delete rule](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdeletetidy-inline.png)](./media/iot-accelerators-remote-monitoring-automate/rulesactionsdeletetidy-expanded.png#lightbox)</span></span>

<span data-ttu-id="b796b-204">You can only delete one rule at a time.</span><span class="sxs-lookup"><span data-stu-id="b796b-204">You can only delete one rule at a time.</span></span>

[!INCLUDE [iot-accelerators-tutorial-cleanup](../../includes/iot-accelerators-tutorial-cleanup.md)]

## <a name="next-steps"></a><span data-ttu-id="b796b-205">Next steps</span><span class="sxs-lookup"><span data-stu-id="b796b-205">Next steps</span></span>

<span data-ttu-id="b796b-206">This tutorial showed you how to use the **Rules** page in the Remote Monitoring solution accelerator to create and manage rules that trigger alerts in the solution.</span><span class="sxs-lookup"><span data-stu-id="b796b-206">This tutorial showed you how to use the **Rules** page in the Remote Monitoring solution accelerator to create and manage rules that trigger alerts in the solution.</span></span> <span data-ttu-id="b796b-207">To learn how to use the solution accelerator to manage and configure your connected devices, continue to the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="b796b-207">To learn how to use the solution accelerator to manage and configure your connected devices, continue to the next tutorial.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b796b-208">Configure and manage devices connected to your monitoring solution</span><span class="sxs-lookup"><span data-stu-id="b796b-208">Configure and manage devices connected to your monitoring solution</span></span>](iot-accelerators-remote-monitoring-manage.md)