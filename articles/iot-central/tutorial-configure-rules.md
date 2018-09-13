---
title: Configure rules and actions in Azure IoT Central | Microsoft Docs
description: This tutorial shows you, as a builder, how to configure telemetry-based rules and actions in your Azure IoT Central application.
author: ankitgupta
ms.author: ankitgup
ms.date: 04/16/2018
ms.topic: tutorial
ms.service: iot-central
services: iot-central
ms.custom: mvc
manager: peterpr
ms.openlocfilehash: b2be066d0d52aedb415be7c1541663333f16b039
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868756"
---
# <a name="tutorial-configure-rules-and-actions-for-your-device-in-azure-iot-central"></a><span data-ttu-id="1296b-103">Tutorial: Configure rules and actions for your device in Azure IoT Central</span><span class="sxs-lookup"><span data-stu-id="1296b-103">Tutorial: Configure rules and actions for your device in Azure IoT Central</span></span>

<span data-ttu-id="1296b-104">This tutorial shows you, as a builder, how to configure telemetry-based rules and actions in your Microsoft Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="1296b-104">This tutorial shows you, as a builder, how to configure telemetry-based rules and actions in your Microsoft Azure IoT Central application.</span></span>

<span data-ttu-id="1296b-105">In this tutorial, you create a rule that sends an email when the temperature in a connected air conditioner device exceeds 90&deg; F.</span><span class="sxs-lookup"><span data-stu-id="1296b-105">In this tutorial, you create a rule that sends an email when the temperature in a connected air conditioner device exceeds 90&deg; F.</span></span>

<span data-ttu-id="1296b-106">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="1296b-106">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1296b-107">Create a telemetry-based rule</span><span class="sxs-lookup"><span data-stu-id="1296b-107">Create a telemetry-based rule</span></span>
> * <span data-ttu-id="1296b-108">Add an action</span><span class="sxs-lookup"><span data-stu-id="1296b-108">Add an action</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1296b-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="1296b-109">Prerequisites</span></span>

<span data-ttu-id="1296b-110">Before you begin, you should complete the [Define a new device type in your application](tutorial-define-device-type.md) tutorial to create the **Connected Air Conditioner** device template to work with.</span><span class="sxs-lookup"><span data-stu-id="1296b-110">Before you begin, you should complete the [Define a new device type in your application](tutorial-define-device-type.md) tutorial to create the **Connected Air Conditioner** device template to work with.</span></span>

## <a name="create-a-telemetry-based-rule"></a><span data-ttu-id="1296b-111">Create a telemetry-based rule</span><span class="sxs-lookup"><span data-stu-id="1296b-111">Create a telemetry-based rule</span></span>

1. <span data-ttu-id="1296b-112">To add a new telemetry-based rule to your application, in the left navigation menu, choose **Device Explorer**:</span><span class="sxs-lookup"><span data-stu-id="1296b-112">To add a new telemetry-based rule to your application, in the left navigation menu, choose **Device Explorer**:</span></span>

    ![Device Explorer page](media/tutorial-configure-rules/explorerpage.png)

    <span data-ttu-id="1296b-114">You see the **Connected Air Conditioner (1.0.0)** device template and the **Connected Air Conditioner-1** device you created in the previous tutorial.</span><span class="sxs-lookup"><span data-stu-id="1296b-114">You see the **Connected Air Conditioner (1.0.0)** device template and the **Connected Air Conditioner-1** device you created in the previous tutorial.</span></span>

2. <span data-ttu-id="1296b-115">To start customizing your connected air conditioner device, choose the device you created in the previous tutorial:</span><span class="sxs-lookup"><span data-stu-id="1296b-115">To start customizing your connected air conditioner device, choose the device you created in the previous tutorial:</span></span>

    ![Connected air conditioner page](media/tutorial-configure-rules/builderdevicelist.png)

3. <span data-ttu-id="1296b-117">To start adding a rule in the **Rules** view, choose **Rules**:</span><span class="sxs-lookup"><span data-stu-id="1296b-117">To start adding a rule in the **Rules** view, choose **Rules**:</span></span>

    ![Rules view](media/tutorial-configure-rules/builderrulesview.png)

4. <span data-ttu-id="1296b-119">To start creating the threshold-based telemetry rule, select **Edit Template**, click **New Rule**, and then **Telemetry**.</span><span class="sxs-lookup"><span data-stu-id="1296b-119">To start creating the threshold-based telemetry rule, select **Edit Template**, click **New Rule**, and then **Telemetry**.</span></span>

5. <span data-ttu-id="1296b-120">To define your rule, use the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="1296b-120">To define your rule, use the information in the following table:</span></span>

    | <span data-ttu-id="1296b-121">Setting</span><span class="sxs-lookup"><span data-stu-id="1296b-121">Setting</span></span>     | <span data-ttu-id="1296b-122">Value</span><span class="sxs-lookup"><span data-stu-id="1296b-122">Value</span></span>                          |
    | ----------- | ------------------------------ |
    | <span data-ttu-id="1296b-123">Name</span><span class="sxs-lookup"><span data-stu-id="1296b-123">Name</span></span>        | <span data-ttu-id="1296b-124">Air conditioner temperature</span><span class="sxs-lookup"><span data-stu-id="1296b-124">Air conditioner temperature</span></span>    |
    | <span data-ttu-id="1296b-125">Enable rule</span><span class="sxs-lookup"><span data-stu-id="1296b-125">Enable rule</span></span> | <span data-ttu-id="1296b-126">On</span><span class="sxs-lookup"><span data-stu-id="1296b-126">On</span></span>                             |
    | <span data-ttu-id="1296b-127">Condition</span><span class="sxs-lookup"><span data-stu-id="1296b-127">Condition</span></span>   | <span data-ttu-id="1296b-128">Temperature is greater than 90</span><span class="sxs-lookup"><span data-stu-id="1296b-128">Temperature is greater than 90</span></span> |

    ![Temperature rule condition](media/tutorial-configure-rules/buildertemperaturerule.png)

## <a name="add-an-action"></a><span data-ttu-id="1296b-130">Add an action</span><span class="sxs-lookup"><span data-stu-id="1296b-130">Add an action</span></span>

<span data-ttu-id="1296b-131">When you define a rule, you also define an action to run when the rule conditions are met.</span><span class="sxs-lookup"><span data-stu-id="1296b-131">When you define a rule, you also define an action to run when the rule conditions are met.</span></span> <span data-ttu-id="1296b-132">In this tutorial, you add an action to send an email as a notification that the rule triggered.</span><span class="sxs-lookup"><span data-stu-id="1296b-132">In this tutorial, you add an action to send an email as a notification that the rule triggered.</span></span>

1. <span data-ttu-id="1296b-133">To add an **Action**, scroll down on the **Configure Telemetry Rule** panel and choose the **+** next to **Actions**, then choose **Email**:</span><span class="sxs-lookup"><span data-stu-id="1296b-133">To add an **Action**, scroll down on the **Configure Telemetry Rule** panel and choose the **+** next to **Actions**, then choose **Email**:</span></span>

    ![Temperature rule action](media/tutorial-configure-rules/builderaddaction.png)

2. <span data-ttu-id="1296b-135">To define your action, use the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="1296b-135">To define your action, use the information in the following table:</span></span>

    | <span data-ttu-id="1296b-136">Setting</span><span class="sxs-lookup"><span data-stu-id="1296b-136">Setting</span></span>   | <span data-ttu-id="1296b-137">Value</span><span class="sxs-lookup"><span data-stu-id="1296b-137">Value</span></span>                          |
    | --------- | ------------------------------ |
    | <span data-ttu-id="1296b-138">To</span><span class="sxs-lookup"><span data-stu-id="1296b-138">To</span></span>        | <span data-ttu-id="1296b-139">Your email address</span><span class="sxs-lookup"><span data-stu-id="1296b-139">Your email address</span></span>             |
    | <span data-ttu-id="1296b-140">Notes</span><span class="sxs-lookup"><span data-stu-id="1296b-140">Notes</span></span>     | <span data-ttu-id="1296b-141">Temperature in air conditioner exceeded threshold.</span><span class="sxs-lookup"><span data-stu-id="1296b-141">Temperature in air conditioner exceeded threshold.</span></span> |

    > [!NOTE]
    > <span data-ttu-id="1296b-142">To receive an email notification, the email address must be a [user ID in the application](howto-administer.md), and that user must have signed in to the application at least once.</span><span class="sxs-lookup"><span data-stu-id="1296b-142">To receive an email notification, the email address must be a [user ID in the application](howto-administer.md), and that user must have signed in to the application at least once.</span></span>

    ![Application Builder Temperature action](media/tutorial-configure-rules/buildertemperatureaction.png)

3. <span data-ttu-id="1296b-144">Choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="1296b-144">Choose **Save**.</span></span> <span data-ttu-id="1296b-145">Your rule is listed on the **Rules** page:</span><span class="sxs-lookup"><span data-stu-id="1296b-145">Your rule is listed on the **Rules** page:</span></span>

    ![Application Builder rules](media/tutorial-configure-rules/builderrules.png)

## <a name="test-the-rule"></a><span data-ttu-id="1296b-147">Test the rule</span><span class="sxs-lookup"><span data-stu-id="1296b-147">Test the rule</span></span>

<span data-ttu-id="1296b-148">Shortly after you save the rule, it becomes live.</span><span class="sxs-lookup"><span data-stu-id="1296b-148">Shortly after you save the rule, it becomes live.</span></span> <span data-ttu-id="1296b-149">When the conditions defined in the rule are met, your application sends a message to the email address you specified in the action.</span><span class="sxs-lookup"><span data-stu-id="1296b-149">When the conditions defined in the rule are met, your application sends a message to the email address you specified in the action.</span></span>

![Email action](media/tutorial-configure-rules/email.png)

## <a name="next-steps"></a><span data-ttu-id="1296b-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="1296b-151">Next steps</span></span>

<span data-ttu-id="1296b-152">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="1296b-152">In this tutorial, you learned how to:</span></span>

<!-- Repeat task list from intro -->
> [!div class="nextstepaction"]
> * <span data-ttu-id="1296b-153">Create a telemetry-based rule</span><span class="sxs-lookup"><span data-stu-id="1296b-153">Create a telemetry-based rule</span></span>
> * <span data-ttu-id="1296b-154">Add an action</span><span class="sxs-lookup"><span data-stu-id="1296b-154">Add an action</span></span>

<span data-ttu-id="1296b-155">Now that you have defined a threshold-based rule the suggested next step is to [Customize the operator's views](tutorial-customize-operator.md).</span><span class="sxs-lookup"><span data-stu-id="1296b-155">Now that you have defined a threshold-based rule the suggested next step is to [Customize the operator's views](tutorial-customize-operator.md).</span></span>

<span data-ttu-id="1296b-156">To learn more about different types of rules in Azure IoT Central and how to parameterize the rule definition, see:</span><span class="sxs-lookup"><span data-stu-id="1296b-156">To learn more about different types of rules in Azure IoT Central and how to parameterize the rule definition, see:</span></span>
* <span data-ttu-id="1296b-157">[Create a telemetry rule and set up notifications](howto-create-telemetry-rules.md).</span><span class="sxs-lookup"><span data-stu-id="1296b-157">[Create a telemetry rule and set up notifications](howto-create-telemetry-rules.md).</span></span>
* <span data-ttu-id="1296b-158">[Create an event rule and set up notifications](howto-create-event-rules.md).</span><span class="sxs-lookup"><span data-stu-id="1296b-158">[Create an event rule and set up notifications](howto-create-event-rules.md).</span></span>

<!-- Next tutorials in the sequence -->
