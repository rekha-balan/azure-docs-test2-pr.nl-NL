---
title: Create and manage event rules in your Azure IoT Central application | Microsoft Docs
description: Azure IoT Central event rules enable you to monitor your devices in near real time and to automatically invoke actions, such as sending an email, when the rule triggers.
author: ankitgupta
ms.author: ankitgup
ms.date: 08/14/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: 40c7b2865795f8c6a5cfbabe4d59aea1715d4a57
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857821"
---
# <a name="create-an-eevent-rule-and-set-up-notifications-in-your-azure-iot-central-application"></a><span data-ttu-id="18f7d-103">Create an eEvent rule and set up notifications in your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="18f7d-103">Create an eEvent rule and set up notifications in your Azure IoT Central application</span></span>

<span data-ttu-id="18f7d-104">You can use Azure IoT Central to remotely monitor your connected devices.</span><span class="sxs-lookup"><span data-stu-id="18f7d-104">You can use Azure IoT Central to remotely monitor your connected devices.</span></span> <span data-ttu-id="18f7d-105">Azure IoT Central rules enable you to monitor your devices in near real time and automatically invoke actions, such as send an email or trigger Microsoft Flow.</span><span class="sxs-lookup"><span data-stu-id="18f7d-105">Azure IoT Central rules enable you to monitor your devices in near real time and automatically invoke actions, such as send an email or trigger Microsoft Flow.</span></span> <span data-ttu-id="18f7d-106">In just a few clicks, you can define the condition for which to monitor your device data and configure the corresponding action.</span><span class="sxs-lookup"><span data-stu-id="18f7d-106">In just a few clicks, you can define the condition for which to monitor your device data and configure the corresponding action.</span></span> <span data-ttu-id="18f7d-107">This article explains how to create rules to monitor events sent by the device.</span><span class="sxs-lookup"><span data-stu-id="18f7d-107">This article explains how to create rules to monitor events sent by the device.</span></span>

<span data-ttu-id="18f7d-108">Devices can use event measurement to send important or informational device events.</span><span class="sxs-lookup"><span data-stu-id="18f7d-108">Devices can use event measurement to send important or informational device events.</span></span> <span data-ttu-id="18f7d-109">An event rule triggers when the selected device event is reported by the device.</span><span class="sxs-lookup"><span data-stu-id="18f7d-109">An event rule triggers when the selected device event is reported by the device.</span></span>

## <a name="create-an-event-rule"></a><span data-ttu-id="18f7d-110">Create an event rule</span><span class="sxs-lookup"><span data-stu-id="18f7d-110">Create an event rule</span></span>

<span data-ttu-id="18f7d-111">To create an event rule, the device template must have at least one event measurement defined.</span><span class="sxs-lookup"><span data-stu-id="18f7d-111">To create an event rule, the device template must have at least one event measurement defined.</span></span> <span data-ttu-id="18f7d-112">This example uses a refrigerated vending machine device that reports a fan motor error event.</span><span class="sxs-lookup"><span data-stu-id="18f7d-112">This example uses a refrigerated vending machine device that reports a fan motor error event.</span></span> <span data-ttu-id="18f7d-113">The rule monitors the event reported by the device and sends an email whenever the event is reported.</span><span class="sxs-lookup"><span data-stu-id="18f7d-113">The rule monitors the event reported by the device and sends an email whenever the event is reported.</span></span>

1. <span data-ttu-id="18f7d-114">Using Device Explorer, navigate to the device template for which you are adding the rule for.</span><span class="sxs-lookup"><span data-stu-id="18f7d-114">Using Device Explorer, navigate to the device template for which you are adding the rule for.</span></span>

1. <span data-ttu-id="18f7d-115">Under the selected template, click on an existing device.</span><span class="sxs-lookup"><span data-stu-id="18f7d-115">Under the selected template, click on an existing device.</span></span> 

    >[!TIP] 
    ><span data-ttu-id="18f7d-116">If the template doesn't have any devices then add a new device first.</span><span class="sxs-lookup"><span data-stu-id="18f7d-116">If the template doesn't have any devices then add a new device first.</span></span>

1. <span data-ttu-id="18f7d-117">If you haven’t created any rules yet, you see the following screen:</span><span class="sxs-lookup"><span data-stu-id="18f7d-117">If you haven’t created any rules yet, you see the following screen:</span></span>

    ![No rules yet](media\howto-create-event-rules\Rules_Landing_Page.png)


1. <span data-ttu-id="18f7d-119">On the **Rules** tab, click **+ New Rule** to see the types of rules you can create.</span><span class="sxs-lookup"><span data-stu-id="18f7d-119">On the **Rules** tab, click **+ New Rule** to see the types of rules you can create.</span></span>


1. <span data-ttu-id="18f7d-120">Click on the **Event** tile to create a rule.</span><span class="sxs-lookup"><span data-stu-id="18f7d-120">Click on the **Event** tile to create a rule.</span></span>

    ![Rule types](media\howto-create-event-rules\Rule_Types.png)

    
1. <span data-ttu-id="18f7d-122">Enter a name that helps you to identify the rule in this device template.</span><span class="sxs-lookup"><span data-stu-id="18f7d-122">Enter a name that helps you to identify the rule in this device template.</span></span>

1. <span data-ttu-id="18f7d-123">To immediately enable the rule for all the devices created from this template, toggle **Enable rule for all devices for this template**.</span><span class="sxs-lookup"><span data-stu-id="18f7d-123">To immediately enable the rule for all the devices created from this template, toggle **Enable rule for all devices for this template**.</span></span>

    ![Rule Detail](media\howto-create-event-rules\Rule_Detail.png)

    <span data-ttu-id="18f7d-125">The rule automatically applies to all the devices under the device template.</span><span class="sxs-lookup"><span data-stu-id="18f7d-125">The rule automatically applies to all the devices under the device template.</span></span>

### <a name="configure-the-rule-conditions"></a><span data-ttu-id="18f7d-126">Configure the rule conditions</span><span class="sxs-lookup"><span data-stu-id="18f7d-126">Configure the rule conditions</span></span>

<span data-ttu-id="18f7d-127">Condition defines the criteria that is monitored by the rule.</span><span class="sxs-lookup"><span data-stu-id="18f7d-127">Condition defines the criteria that is monitored by the rule.</span></span>

1. <span data-ttu-id="18f7d-128">Choose the **+** next to **Conditions** to add a new condition.</span><span class="sxs-lookup"><span data-stu-id="18f7d-128">Choose the **+** next to **Conditions** to add a new condition.</span></span>

1. <span data-ttu-id="18f7d-129">Choose the event that you want to monitor from the Measurement dropdown.</span><span class="sxs-lookup"><span data-stu-id="18f7d-129">Choose the event that you want to monitor from the Measurement dropdown.</span></span> <span data-ttu-id="18f7d-130">In this example, **Fan Motor Error** event has been selected.</span><span class="sxs-lookup"><span data-stu-id="18f7d-130">In this example, **Fan Motor Error** event has been selected.</span></span>

   ![Condition](media\howto-create-event-rules\Condition_Filled_Out.png) 


1. <span data-ttu-id="18f7d-132">Optionally, you can also set **Count** as **Aggregation** and provide the corresponding threshold.</span><span class="sxs-lookup"><span data-stu-id="18f7d-132">Optionally, you can also set **Count** as **Aggregation** and provide the corresponding threshold.</span></span>

    - <span data-ttu-id="18f7d-133">Without aggregation, the rule triggers for each event data point that meets the condition.</span><span class="sxs-lookup"><span data-stu-id="18f7d-133">Without aggregation, the rule triggers for each event data point that meets the condition.</span></span> <span data-ttu-id="18f7d-134">For example, if you configure the rule's condition to trigger when a 'Fan Motor Error' event occurs then the rule will trigger almost immediately when the device reports that event.</span><span class="sxs-lookup"><span data-stu-id="18f7d-134">For example, if you configure the rule's condition to trigger when a 'Fan Motor Error' event occurs then the rule will trigger almost immediately when the device reports that event.</span></span>
    - <span data-ttu-id="18f7d-135">If Count is used as an aggregate function, then you have to  provide a **Threshold** and an **Aggregate time window** over which the condition needs to be evaluated.</span><span class="sxs-lookup"><span data-stu-id="18f7d-135">If Count is used as an aggregate function, then you have to  provide a **Threshold** and an **Aggregate time window** over which the condition needs to be evaluated.</span></span> <span data-ttu-id="18f7d-136">In this case, the count of events is aggregated and the rule will trigger only if the aggregated event count matches the threshold.</span><span class="sxs-lookup"><span data-stu-id="18f7d-136">In this case, the count of events is aggregated and the rule will trigger only if the aggregated event count matches the threshold.</span></span>
 
    <span data-ttu-id="18f7d-137">For example, if you want to alert when there are more than three device events within 5 minutes, then select the event and set the aggregate function as "count",  operator as "greater than", and "threshold" as 3.</span><span class="sxs-lookup"><span data-stu-id="18f7d-137">For example, if you want to alert when there are more than three device events within 5 minutes, then select the event and set the aggregate function as "count",  operator as "greater than", and "threshold" as 3.</span></span> <span data-ttu-id="18f7d-138">Set "Aggregation time period" as "5 minutes".</span><span class="sxs-lookup"><span data-stu-id="18f7d-138">Set "Aggregation time period" as "5 minutes".</span></span> <span data-ttu-id="18f7d-139">The rule triggers when more than three events are sent by the device within 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="18f7d-139">The rule triggers when more than three events are sent by the device within 5 minutes.</span></span> <span data-ttu-id="18f7d-140">The rule evaluation frequency is the same as the **Aggregate time window**, which means, in this example, the rule is  evaluated once every 5 minutes.</span><span class="sxs-lookup"><span data-stu-id="18f7d-140">The rule evaluation frequency is the same as the **Aggregate time window**, which means, in this example, the rule is  evaluated once every 5 minutes.</span></span> 

    ![Add Event Condition](media\howto-create-event-rules\Aggregate_Condition_Filled_Out.png)

    >[!NOTE] 
    ><span data-ttu-id="18f7d-142">More than one event measurement can be added under **Condition**.</span><span class="sxs-lookup"><span data-stu-id="18f7d-142">More than one event measurement can be added under **Condition**.</span></span> <span data-ttu-id="18f7d-143">When multiple conditions are specified, all the conditions must be met for the rule to trigger.</span><span class="sxs-lookup"><span data-stu-id="18f7d-143">When multiple conditions are specified, all the conditions must be met for the rule to trigger.</span></span> <span data-ttu-id="18f7d-144">Each conditon gets joined by an 'AND' clause implicitly.</span><span class="sxs-lookup"><span data-stu-id="18f7d-144">Each conditon gets joined by an 'AND' clause implicitly.</span></span> <span data-ttu-id="18f7d-145">When using aggregate, every measurement must be aggregated.</span><span class="sxs-lookup"><span data-stu-id="18f7d-145">When using aggregate, every measurement must be aggregated.</span></span>

### <a name="configure-actions"></a><span data-ttu-id="18f7d-146">Configure actions</span><span class="sxs-lookup"><span data-stu-id="18f7d-146">Configure actions</span></span>

<span data-ttu-id="18f7d-147">This section shows you how to set up actions to take when the rule is fired.</span><span class="sxs-lookup"><span data-stu-id="18f7d-147">This section shows you how to set up actions to take when the rule is fired.</span></span> <span data-ttu-id="18f7d-148">Actions get invoked when all the conditions specified in the rule evaluate to true.</span><span class="sxs-lookup"><span data-stu-id="18f7d-148">Actions get invoked when all the conditions specified in the rule evaluate to true.</span></span>

1. <span data-ttu-id="18f7d-149">Choose the **+** next to **Actions**.</span><span class="sxs-lookup"><span data-stu-id="18f7d-149">Choose the **+** next to **Actions**.</span></span> <span data-ttu-id="18f7d-150">Here you see the list of available actions.</span><span class="sxs-lookup"><span data-stu-id="18f7d-150">Here you see the list of available actions.</span></span> 

    ![Add Action](media\howto-create-event-rules\Add_Action.png)

1. <span data-ttu-id="18f7d-152">Choose the **Email** action, enter a valid email address in the **To** field, and provide a note to appear in the body of the email when the rule triggers.</span><span class="sxs-lookup"><span data-stu-id="18f7d-152">Choose the **Email** action, enter a valid email address in the **To** field, and provide a note to appear in the body of the email when the rule triggers.</span></span>

    > [!NOTE]
    > <span data-ttu-id="18f7d-153">Emails are only sent to the users that have been added to the application and have logged in at least once.</span><span class="sxs-lookup"><span data-stu-id="18f7d-153">Emails are only sent to the users that have been added to the application and have logged in at least once.</span></span> <span data-ttu-id="18f7d-154">Learn more about [user management](howto-administer.md) in Azure IoT Central.</span><span class="sxs-lookup"><span data-stu-id="18f7d-154">Learn more about [user management](howto-administer.md) in Azure IoT Central.</span></span>

   ![Configure Action](media\howto-create-event-rules\Configure_Action.png)

1. <span data-ttu-id="18f7d-156">To save the rule, choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="18f7d-156">To save the rule, choose **Save**.</span></span> <span data-ttu-id="18f7d-157">The rule goes live within a few minutes and starts monitoring the events being sent to your application.</span><span class="sxs-lookup"><span data-stu-id="18f7d-157">The rule goes live within a few minutes and starts monitoring the events being sent to your application.</span></span> <span data-ttu-id="18f7d-158">When the condition specified in the rule matches, the rule triggers the configured email action.</span><span class="sxs-lookup"><span data-stu-id="18f7d-158">When the condition specified in the rule matches, the rule triggers the configured email action.</span></span>

<span data-ttu-id="18f7d-159">You can add other actions to the rule such as Microsoft Flow and webhooks.</span><span class="sxs-lookup"><span data-stu-id="18f7d-159">You can add other actions to the rule such as Microsoft Flow and webhooks.</span></span> <span data-ttu-id="18f7d-160">You can add up to 5 actions per rule.</span><span class="sxs-lookup"><span data-stu-id="18f7d-160">You can add up to 5 actions per rule.</span></span>

- <span data-ttu-id="18f7d-161">[Microsoft Flow action](howto-add-microsoft-flow.md) to kick off a workflow in Microsoft Flow when a rule is triggered</span><span class="sxs-lookup"><span data-stu-id="18f7d-161">[Microsoft Flow action](howto-add-microsoft-flow.md) to kick off a workflow in Microsoft Flow when a rule is triggered</span></span> 
- <span data-ttu-id="18f7d-162">[Webhook action](howto-create-webhooks.md) to notify other services when a rule is triggered</span><span class="sxs-lookup"><span data-stu-id="18f7d-162">[Webhook action](howto-create-webhooks.md) to notify other services when a rule is triggered</span></span>

## <a name="parameterize-the-rule"></a><span data-ttu-id="18f7d-163">Parameterize the rule</span><span class="sxs-lookup"><span data-stu-id="18f7d-163">Parameterize the rule</span></span>

<span data-ttu-id="18f7d-164">Actions can also be configured using **Device Property** as a parameter.</span><span class="sxs-lookup"><span data-stu-id="18f7d-164">Actions can also be configured using **Device Property** as a parameter.</span></span> <span data-ttu-id="18f7d-165">If an email address is stored as a device property, then it can be used when you define the **To** address.</span><span class="sxs-lookup"><span data-stu-id="18f7d-165">If an email address is stored as a device property, then it can be used when you define the **To** address.</span></span>

## <a name="delete-a-rule"></a><span data-ttu-id="18f7d-166">Delete a rule</span><span class="sxs-lookup"><span data-stu-id="18f7d-166">Delete a rule</span></span>

<span data-ttu-id="18f7d-167">If you no longer need a rule, delete it by opening the rule and choosing **Delete**.</span><span class="sxs-lookup"><span data-stu-id="18f7d-167">If you no longer need a rule, delete it by opening the rule and choosing **Delete**.</span></span> <span data-ttu-id="18f7d-168">Deleting the rule removes it from the device template and all the associated devices.</span><span class="sxs-lookup"><span data-stu-id="18f7d-168">Deleting the rule removes it from the device template and all the associated devices.</span></span>

## <a name="enable-or-disable-a-rule-for-a-device-template"></a><span data-ttu-id="18f7d-169">Enable or disable a rule for a device template</span><span class="sxs-lookup"><span data-stu-id="18f7d-169">Enable or disable a rule for a device template</span></span>

<span data-ttu-id="18f7d-170">Navigate to the device and choose the rule you want to enable or disable.</span><span class="sxs-lookup"><span data-stu-id="18f7d-170">Navigate to the device and choose the rule you want to enable or disable.</span></span> <span data-ttu-id="18f7d-171">Toggle the **Enable rule for all devices of this template** button to enable or disable the rule for all devices that are associated with the device template.</span><span class="sxs-lookup"><span data-stu-id="18f7d-171">Toggle the **Enable rule for all devices of this template** button to enable or disable the rule for all devices that are associated with the device template.</span></span>

## <a name="enable-or-disable-a-rule-for-a-device"></a><span data-ttu-id="18f7d-172">Enable or disable a rule for a device</span><span class="sxs-lookup"><span data-stu-id="18f7d-172">Enable or disable a rule for a device</span></span>

<span data-ttu-id="18f7d-173">Navigate to the device and choose the rule you want to enable or disable.</span><span class="sxs-lookup"><span data-stu-id="18f7d-173">Navigate to the device and choose the rule you want to enable or disable.</span></span> <span data-ttu-id="18f7d-174">Toggle the **Enable rule for this device** button to either enable or disable the rule for that device.</span><span class="sxs-lookup"><span data-stu-id="18f7d-174">Toggle the **Enable rule for this device** button to either enable or disable the rule for that device.</span></span>

## <a name="next-steps"></a><span data-ttu-id="18f7d-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="18f7d-175">Next steps</span></span>

<span data-ttu-id="18f7d-176">Now that you have learned how to create rules in your Azure IoT Central application, here are some next step:</span><span class="sxs-lookup"><span data-stu-id="18f7d-176">Now that you have learned how to create rules in your Azure IoT Central application, here are some next step:</span></span>

- [<span data-ttu-id="18f7d-177">Add Microsoft Flow action in rules</span><span class="sxs-lookup"><span data-stu-id="18f7d-177">Add Microsoft Flow action in rules</span></span>](howto-add-microsoft-flow.md)
- [<span data-ttu-id="18f7d-178">Add Webhook action in rules</span><span class="sxs-lookup"><span data-stu-id="18f7d-178">Add Webhook action in rules</span></span>](howto-create-webhooks.md)
- [<span data-ttu-id="18f7d-179">How to manage your devices</span><span class="sxs-lookup"><span data-stu-id="18f7d-179">How to manage your devices</span></span>](howto-manage-devices.md)
