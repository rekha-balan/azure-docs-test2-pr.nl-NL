---
title: Create and manage telemetry rules in your Azure IoT Central application | Microsoft Docs
description: Azure IoT Central telemetry rules enable you to monitor your devices in near real time and to automatically invoke actions, such as sending an email, when the rule triggers.
author: ankitgupta
ms.author: ankitgup
ms.date: 08/14/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 5913df2d4dc286fad63760c95f54e0dbc717acdc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867155"
---
# <a name="create-a-telemetry-rule-and-set-up-notifications-in-your-azure-iot-central-application"></a><span data-ttu-id="eaaec-103">Create a telemetry rule and set up notifications in your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="eaaec-103">Create a telemetry rule and set up notifications in your Azure IoT Central application</span></span>

<span data-ttu-id="eaaec-104">You can use Azure IoT Central to remotely monitor your connected devices.</span><span class="sxs-lookup"><span data-stu-id="eaaec-104">You can use Azure IoT Central to remotely monitor your connected devices.</span></span> <span data-ttu-id="eaaec-105">Azure IoT Central rules enable you to monitor your devices in near real time and automatically invoke actions, such as send an email or trigger Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="eaaec-105">Azure IoT Central rules enable you to monitor your devices in near real time and automatically invoke actions, such as send an email or trigger Microsoft Flow.</span></span> <span data-ttu-id="eaaec-106">In just a few clicks, you can define the condition for which to monitor your device data and configure the corresponding action.</span><span class="sxs-lookup"><span data-stu-id="eaaec-106">In just a few clicks, you can define the condition for which to monitor your device data and configure the corresponding action.</span></span> <span data-ttu-id="eaaec-107">This article explains how to create rules to monitor telemetry sent by the device.</span><span class="sxs-lookup"><span data-stu-id="eaaec-107">This article explains how to create rules to monitor telemetry sent by the device.</span></span>

<span data-ttu-id="eaaec-108">Devices can use telemetry measurement to send numerical data from the device.</span><span class="sxs-lookup"><span data-stu-id="eaaec-108">Devices can use telemetry measurement to send numerical data from the device.</span></span> <span data-ttu-id="eaaec-109">A telemetry rule triggers when the selected device telemetry crosses a specified threshold.</span><span class="sxs-lookup"><span data-stu-id="eaaec-109">A telemetry rule triggers when the selected device telemetry crosses a specified threshold.</span></span>

## <a name="create-a-telemetry-rule"></a><span data-ttu-id="eaaec-110">Create a telemetry rule</span><span class="sxs-lookup"><span data-stu-id="eaaec-110">Create a telemetry rule</span></span>

<span data-ttu-id="eaaec-111">To create a telemetry rule, the device template must have at least one telemetry measurement defined.</span><span class="sxs-lookup"><span data-stu-id="eaaec-111">To create a telemetry rule, the device template must have at least one telemetry measurement defined.</span></span> <span data-ttu-id="eaaec-112">This example uses a refrigerated vending machine device that sends temperature and humidity telemetry.</span><span class="sxs-lookup"><span data-stu-id="eaaec-112">This example uses a refrigerated vending machine device that sends temperature and humidity telemetry.</span></span> <span data-ttu-id="eaaec-113">The rule monitors the temperature reported by the device and sends an email when it goes above 80 degrees.</span><span class="sxs-lookup"><span data-stu-id="eaaec-113">The rule monitors the temperature reported by the device and sends an email when it goes above 80 degrees.</span></span>

1. <span data-ttu-id="eaaec-114">Using Device Explorer, navigate to the device template for which you are adding the rule for.</span><span class="sxs-lookup"><span data-stu-id="eaaec-114">Using Device Explorer, navigate to the device template for which you are adding the rule for.</span></span>

1. <span data-ttu-id="eaaec-115">Under the selected template, click on an existing device.</span><span class="sxs-lookup"><span data-stu-id="eaaec-115">Under the selected template, click on an existing device.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="eaaec-116">If the template doesn't have any devices then add a new device first.</span><span class="sxs-lookup"><span data-stu-id="eaaec-116">If the template doesn't have any devices then add a new device first.</span></span>

1. <span data-ttu-id="eaaec-117">If you haven’t created any rules yet, you will see the following screen:</span><span class="sxs-lookup"><span data-stu-id="eaaec-117">If you haven’t created any rules yet, you will see the following screen:</span></span>

    ![No rules yet](media\howto-create-telemetry-rules\Rules_Landing_Page.png)

1. <span data-ttu-id="eaaec-119">On the **Rules** tab, click **+ New Rule** to see the types of rules you can create.</span><span class="sxs-lookup"><span data-stu-id="eaaec-119">On the **Rules** tab, click **+ New Rule** to see the types of rules you can create.</span></span>

1. <span data-ttu-id="eaaec-120">Click on the **Telemetry** tile to create a rule to monitor device telemetry.</span><span class="sxs-lookup"><span data-stu-id="eaaec-120">Click on the **Telemetry** tile to create a rule to monitor device telemetry.</span></span>

    ![Rule Types](media\howto-create-telemetry-rules\Rule_Types.png)

1. <span data-ttu-id="eaaec-122">Enter a name that helps you to identify the rule in this device template.</span><span class="sxs-lookup"><span data-stu-id="eaaec-122">Enter a name that helps you to identify the rule in this device template.</span></span>

1. <span data-ttu-id="eaaec-123">To immediately enable the rule for all the devices created for this template, toggle **Enable rule for all devices for this template**.</span><span class="sxs-lookup"><span data-stu-id="eaaec-123">To immediately enable the rule for all the devices created for this template, toggle **Enable rule for all devices for this template**.</span></span>

   ![Rule Detail](media\howto-create-telemetry-rules\Rule_Detail.png)
    
    <span data-ttu-id="eaaec-125">The rule automatically applies to all the devices under the device template.</span><span class="sxs-lookup"><span data-stu-id="eaaec-125">The rule automatically applies to all the devices under the device template.</span></span>
    

### <a name="configure-the-rule-conditions"></a><span data-ttu-id="eaaec-126">Configure the rule conditions</span><span class="sxs-lookup"><span data-stu-id="eaaec-126">Configure the rule conditions</span></span>

<span data-ttu-id="eaaec-127">Condition defines the criteria that is monitored by the rule.</span><span class="sxs-lookup"><span data-stu-id="eaaec-127">Condition defines the criteria that is monitored by the rule.</span></span>

1. <span data-ttu-id="eaaec-128">Click **+** next to **Conditions** to add a new condition.</span><span class="sxs-lookup"><span data-stu-id="eaaec-128">Click **+** next to **Conditions** to add a new condition.</span></span>

1. <span data-ttu-id="eaaec-129">Select the telemetry you want to monitor from the **Measurement** dropdown.</span><span class="sxs-lookup"><span data-stu-id="eaaec-129">Select the telemetry you want to monitor from the **Measurement** dropdown.</span></span>

   ![Condition](media\howto-create-telemetry-rules\Aggregate_Condition_Filled_Out.png)

1. <span data-ttu-id="eaaec-131">Next, choose **Aggregation**, **Operator**, and provide a **Threshold** value.</span><span class="sxs-lookup"><span data-stu-id="eaaec-131">Next, choose **Aggregation**, **Operator**, and provide a **Threshold** value.</span></span>
    - <span data-ttu-id="eaaec-132">Aggregation is optional.</span><span class="sxs-lookup"><span data-stu-id="eaaec-132">Aggregation is optional.</span></span> <span data-ttu-id="eaaec-133">Without aggregation, the rule triggers for each telemetry data point that meets the condition.</span><span class="sxs-lookup"><span data-stu-id="eaaec-133">Without aggregation, the rule triggers for each telemetry data point that meets the condition.</span></span> <span data-ttu-id="eaaec-134">For example, if the rule is configured to trigger when temperature is above 80 then the rule will trigger almost instantly when the device reports temperature > 80.</span><span class="sxs-lookup"><span data-stu-id="eaaec-134">For example, if the rule is configured to trigger when temperature is above 80 then the rule will trigger almost instantly when the device reports temperature > 80.</span></span>
    - <span data-ttu-id="eaaec-135">If an aggregate function like Average, Min, Max, Count is chosen then, the user must provide an **Aggregate time window** over which the condition needs to be evaluated.</span><span class="sxs-lookup"><span data-stu-id="eaaec-135">If an aggregate function like Average, Min, Max, Count is chosen then, the user must provide an **Aggregate time window** over which the condition needs to be evaluated.</span></span> <span data-ttu-id="eaaec-136">For example, if you set the period as "5 minutes" and your rule looks for Average temperature above 80, the rule triggers when the average temperature is above 80 for at least 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="eaaec-136">For example, if you set the period as "5 minutes" and your rule looks for Average temperature above 80, the rule triggers when the average temperature is above 80 for at least 5 minutes.</span></span> <span data-ttu-id="eaaec-137">The rule evaluation frequency is the same as the **Aggregate time window**, which means, in this example, the rule is evaluated once every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="eaaec-137">The rule evaluation frequency is the same as the **Aggregate time window**, which means, in this example, the rule is evaluated once every 5 minutes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="eaaec-138">More than one telemetry measurement can be added under **Condition**.</span><span class="sxs-lookup"><span data-stu-id="eaaec-138">More than one telemetry measurement can be added under **Condition**.</span></span> <span data-ttu-id="eaaec-139">When multiple conditions are specified, all the conditions must be met for the rule to trigger.</span><span class="sxs-lookup"><span data-stu-id="eaaec-139">When multiple conditions are specified, all the conditions must be met for the rule to trigger.</span></span> <span data-ttu-id="eaaec-140">Each conditon gets joined by an 'AND' clause implicitly.</span><span class="sxs-lookup"><span data-stu-id="eaaec-140">Each conditon gets joined by an 'AND' clause implicitly.</span></span> <span data-ttu-id="eaaec-141">When using aggregate, every measurement must be aggregated.</span><span class="sxs-lookup"><span data-stu-id="eaaec-141">When using aggregate, every measurement must be aggregated.</span></span>
    
    

### <a name="configure-actions"></a><span data-ttu-id="eaaec-142">Configure actions</span><span class="sxs-lookup"><span data-stu-id="eaaec-142">Configure actions</span></span>

<span data-ttu-id="eaaec-143">This section shows you how to set up actions to take when the rule is fired.</span><span class="sxs-lookup"><span data-stu-id="eaaec-143">This section shows you how to set up actions to take when the rule is fired.</span></span> <span data-ttu-id="eaaec-144">Actions get invoked when all the conditions specified in the rule evaluate to true.</span><span class="sxs-lookup"><span data-stu-id="eaaec-144">Actions get invoked when all the conditions specified in the rule evaluate to true.</span></span>

1. <span data-ttu-id="eaaec-145">Choose the **+** next to **Actions**.</span><span class="sxs-lookup"><span data-stu-id="eaaec-145">Choose the **+** next to **Actions**.</span></span> <span data-ttu-id="eaaec-146">Here you see the list of available actions.</span><span class="sxs-lookup"><span data-stu-id="eaaec-146">Here you see the list of available actions.</span></span>  

    ![Add Action](media\howto-create-telemetry-rules\Add_Action.png)

1. <span data-ttu-id="eaaec-148">Choose the **Email** action, enter a valid email address in the **To** field, and provide a note to appear in the body of the email when the rule triggers.</span><span class="sxs-lookup"><span data-stu-id="eaaec-148">Choose the **Email** action, enter a valid email address in the **To** field, and provide a note to appear in the body of the email when the rule triggers.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eaaec-149">Emails are only sent to the users that have been added to the application and have logged in at least once.</span><span class="sxs-lookup"><span data-stu-id="eaaec-149">Emails are only sent to the users that have been added to the application and have logged in at least once.</span></span> <span data-ttu-id="eaaec-150">Learn more about [user management](howto-administer.md) in Azure IoT Central.</span><span class="sxs-lookup"><span data-stu-id="eaaec-150">Learn more about [user management](howto-administer.md) in Azure IoT Central.</span></span>

   ![Configure Action](media\howto-create-telemetry-rules\Configure_Action.png)

1. <span data-ttu-id="eaaec-152">To save the rule, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="eaaec-152">To save the rule, choose **Save**.</span></span> <span data-ttu-id="eaaec-153">The rule goes live within a few minutes and starts monitoring telemetry being sent to your application.</span><span class="sxs-lookup"><span data-stu-id="eaaec-153">The rule goes live within a few minutes and starts monitoring telemetry being sent to your application.</span></span> <span data-ttu-id="eaaec-154">When the condition specified in the rule matches, the rule triggers the configured email action.</span><span class="sxs-lookup"><span data-stu-id="eaaec-154">When the condition specified in the rule matches, the rule triggers the configured email action.</span></span>

<span data-ttu-id="eaaec-155">You can add other actions to the rule such as Microsoft Flow and webhooks.</span><span class="sxs-lookup"><span data-stu-id="eaaec-155">You can add other actions to the rule such as Microsoft Flow and webhooks.</span></span> <span data-ttu-id="eaaec-156">You can add up to 5 actions per rule.</span><span class="sxs-lookup"><span data-stu-id="eaaec-156">You can add up to 5 actions per rule.</span></span>

- <span data-ttu-id="eaaec-157">[Microsoft Flow action](howto-add-microsoft-flow.md) to kick off a workflow in Microsoft Flow when a rule is triggered</span><span class="sxs-lookup"><span data-stu-id="eaaec-157">[Microsoft Flow action](howto-add-microsoft-flow.md) to kick off a workflow in Microsoft Flow when a rule is triggered</span></span> 
- <span data-ttu-id="eaaec-158">[Webhook action](howto-create-webhooks.md) to notify other services when a rule is triggered</span><span class="sxs-lookup"><span data-stu-id="eaaec-158">[Webhook action](howto-create-webhooks.md) to notify other services when a rule is triggered</span></span>

## <a name="parameterize-the-rule"></a><span data-ttu-id="eaaec-159">Parameterize the rule</span><span class="sxs-lookup"><span data-stu-id="eaaec-159">Parameterize the rule</span></span>

<span data-ttu-id="eaaec-160">Rules can derive certain vales from **Device Properties** as parameters.</span><span class="sxs-lookup"><span data-stu-id="eaaec-160">Rules can derive certain vales from **Device Properties** as parameters.</span></span> <span data-ttu-id="eaaec-161">Using parameters is helpful in scenarios where telemetry thresholds vary for different devices.</span><span class="sxs-lookup"><span data-stu-id="eaaec-161">Using parameters is helpful in scenarios where telemetry thresholds vary for different devices.</span></span> <span data-ttu-id="eaaec-162">When you create the rule, choose a device property that specifies the threshold, such as **Maximum Ideal Threshold**, instead of providing an absolute value, such as 80 degrees.</span><span class="sxs-lookup"><span data-stu-id="eaaec-162">When you create the rule, choose a device property that specifies the threshold, such as **Maximum Ideal Threshold**, instead of providing an absolute value, such as 80 degrees.</span></span> <span data-ttu-id="eaaec-163">When the rule executes, it matches the device telemetry with the value set in the device property.</span><span class="sxs-lookup"><span data-stu-id="eaaec-163">When the rule executes, it matches the device telemetry with the value set in the device property.</span></span>

<span data-ttu-id="eaaec-164">Using parameters is an effective way to reduce the number of rules to manage per device template.</span><span class="sxs-lookup"><span data-stu-id="eaaec-164">Using parameters is an effective way to reduce the number of rules to manage per device template.</span></span>

<span data-ttu-id="eaaec-165">Actions can also be configured using **Device Property** as a parameter.</span><span class="sxs-lookup"><span data-stu-id="eaaec-165">Actions can also be configured using **Device Property** as a parameter.</span></span> <span data-ttu-id="eaaec-166">If an email address is stored as a property, then it can be used when you define the **To** address.</span><span class="sxs-lookup"><span data-stu-id="eaaec-166">If an email address is stored as a property, then it can be used when you define the **To** address.</span></span>

## <a name="delete-a-rule"></a><span data-ttu-id="eaaec-167">Delete a rule</span><span class="sxs-lookup"><span data-stu-id="eaaec-167">Delete a rule</span></span>

<span data-ttu-id="eaaec-168">If you no longer need a rule, delete it by opening the rule and choosing **Delete**.</span><span class="sxs-lookup"><span data-stu-id="eaaec-168">If you no longer need a rule, delete it by opening the rule and choosing **Delete**.</span></span> <span data-ttu-id="eaaec-169">Deleting the rule removes it from the device template and all the associated devices.</span><span class="sxs-lookup"><span data-stu-id="eaaec-169">Deleting the rule removes it from the device template and all the associated devices.</span></span>

## <a name="enable-or-disable-a-rule-for-a-device-template"></a><span data-ttu-id="eaaec-170">Enable or disable a rule for a device template</span><span class="sxs-lookup"><span data-stu-id="eaaec-170">Enable or disable a rule for a device template</span></span>

<span data-ttu-id="eaaec-171">Navigate to the device and choose the rule you want to enable or disable.</span><span class="sxs-lookup"><span data-stu-id="eaaec-171">Navigate to the device and choose the rule you want to enable or disable.</span></span> <span data-ttu-id="eaaec-172">Toggle the **Enable rule for all devices of this template** button in the rule to enable or disable the rule for all devices that are associated with the device template.</span><span class="sxs-lookup"><span data-stu-id="eaaec-172">Toggle the **Enable rule for all devices of this template** button in the rule to enable or disable the rule for all devices that are associated with the device template.</span></span>

## <a name="enable-or-disable-a-rule-for-a-device"></a><span data-ttu-id="eaaec-173">Enable or disable a rule for a device</span><span class="sxs-lookup"><span data-stu-id="eaaec-173">Enable or disable a rule for a device</span></span>

<span data-ttu-id="eaaec-174">Navigate to the device and choose the rule you want to enable or disable.</span><span class="sxs-lookup"><span data-stu-id="eaaec-174">Navigate to the device and choose the rule you want to enable or disable.</span></span> <span data-ttu-id="eaaec-175">Toggle the **Enable rule for this device** button to either enable or disable the rule for that device.</span><span class="sxs-lookup"><span data-stu-id="eaaec-175">Toggle the **Enable rule for this device** button to either enable or disable the rule for that device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eaaec-176">Next steps</span><span class="sxs-lookup"><span data-stu-id="eaaec-176">Next steps</span></span>

<span data-ttu-id="eaaec-177">Now that you have learned how to create rules in your Azure IoT Central application, here are some next step:</span><span class="sxs-lookup"><span data-stu-id="eaaec-177">Now that you have learned how to create rules in your Azure IoT Central application, here are some next step:</span></span>

- [<span data-ttu-id="eaaec-178">Add Microsoft Flow action in rules</span><span class="sxs-lookup"><span data-stu-id="eaaec-178">Add Microsoft Flow action in rules</span></span>](howto-add-microsoft-flow.md)
- [<span data-ttu-id="eaaec-179">Add Webhook action in rules</span><span class="sxs-lookup"><span data-stu-id="eaaec-179">Add Webhook action in rules</span></span>](howto-create-webhooks.md)
- [<span data-ttu-id="eaaec-180">How to manage your devices</span><span class="sxs-lookup"><span data-stu-id="eaaec-180">How to manage your devices</span></span>](howto-manage-devices.md)
