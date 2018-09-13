---
title: Monitor your devices in Azure IoT Central | Microsoft Docs
description: As an operator, use your Azure IoT Central application to monitor your devices.
author: tbhagwat3
ms.author: tanmayb
ms.date: 04/16/2018
ms.topic: tutorial
ms.service: iot-central
services: iot-central
ms.custom: mvc
manager: peterpr
ms.openlocfilehash: 9a3b7383651d679b079818fb32bd8f98160d0a4c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871586"
---
# <a name="tutorial-use-azure-iot-central-to-monitor-your-devices"></a><span data-ttu-id="e6f14-103">Tutorial: Use Azure IoT Central to monitor your devices</span><span class="sxs-lookup"><span data-stu-id="e6f14-103">Tutorial: Use Azure IoT Central to monitor your devices</span></span>

<span data-ttu-id="e6f14-104">This tutorial shows you, as an operator, how to use your Microsoft Azure IoT Central application to monitor your devices and change settings.</span><span class="sxs-lookup"><span data-stu-id="e6f14-104">This tutorial shows you, as an operator, how to use your Microsoft Azure IoT Central application to monitor your devices and change settings.</span></span>

<span data-ttu-id="e6f14-105">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="e6f14-105">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e6f14-106">Receive a notification</span><span class="sxs-lookup"><span data-stu-id="e6f14-106">Receive a notification</span></span>
> * <span data-ttu-id="e6f14-107">Investigate an issue</span><span class="sxs-lookup"><span data-stu-id="e6f14-107">Investigate an issue</span></span>
> * <span data-ttu-id="e6f14-108">Remediate an issue</span><span class="sxs-lookup"><span data-stu-id="e6f14-108">Remediate an issue</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6f14-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e6f14-109">Prerequisites</span></span>

<span data-ttu-id="e6f14-110">Before you begin, the builder should complete the three builder tutorials to create the Azure IoT Central application:</span><span class="sxs-lookup"><span data-stu-id="e6f14-110">Before you begin, the builder should complete the three builder tutorials to create the Azure IoT Central application:</span></span>

* [<span data-ttu-id="e6f14-111">Define a new device type</span><span class="sxs-lookup"><span data-stu-id="e6f14-111">Define a new device type</span></span>](tutorial-define-device-type.md)
* [<span data-ttu-id="e6f14-112">Configure rules and actions for your device</span><span class="sxs-lookup"><span data-stu-id="e6f14-112">Configure rules and actions for your device</span></span>](tutorial-configure-rules.md)
* [<span data-ttu-id="e6f14-113">Customize the operator's views</span><span class="sxs-lookup"><span data-stu-id="e6f14-113">Customize the operator's views</span></span>](tutorial-customize-operator.md)

## <a name="receive-a-notification"></a><span data-ttu-id="e6f14-114">Receive a notification</span><span class="sxs-lookup"><span data-stu-id="e6f14-114">Receive a notification</span></span>

<span data-ttu-id="e6f14-115">Azure IoT Central sends notifications about devices as email messages.</span><span class="sxs-lookup"><span data-stu-id="e6f14-115">Azure IoT Central sends notifications about devices as email messages.</span></span> <span data-ttu-id="e6f14-116">The builder added a rule to send a notification when the temperature in a connected air conditioner device exceeded a threshold.</span><span class="sxs-lookup"><span data-stu-id="e6f14-116">The builder added a rule to send a notification when the temperature in a connected air conditioner device exceeded a threshold.</span></span> <span data-ttu-id="e6f14-117">Check the emails sent to the account the builder chose to receive notifications.</span><span class="sxs-lookup"><span data-stu-id="e6f14-117">Check the emails sent to the account the builder chose to receive notifications.</span></span>

<span data-ttu-id="e6f14-118">Open the email message you received at the end of the [Configure rules and actions for your device](tutorial-configure-rules.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="e6f14-118">Open the email message you received at the end of the [Configure rules and actions for your device](tutorial-configure-rules.md) tutorial.</span></span> <span data-ttu-id="e6f14-119">In the email, choose **Click here to open your device**:</span><span class="sxs-lookup"><span data-stu-id="e6f14-119">In the email, choose **Click here to open your device**:</span></span>

![Application Builder rules](media/tutorial-monitor-devices/email.png)

<span data-ttu-id="e6f14-121">The **Device** page for the **Connected Air Conditioner-1** simulated device you created in the previous tutorials opens in your browser:</span><span class="sxs-lookup"><span data-stu-id="e6f14-121">The **Device** page for the **Connected Air Conditioner-1** simulated device you created in the previous tutorials opens in your browser:</span></span>

![Device that triggered the notification email message](media/tutorial-monitor-devices/sourcedevice.png)

## <a name="investigate-an-issue"></a><span data-ttu-id="e6f14-123">Investigate an issue</span><span class="sxs-lookup"><span data-stu-id="e6f14-123">Investigate an issue</span></span>

<span data-ttu-id="e6f14-124">As an operator, you can view information about the device on the **Measurements**, **Settings**, **Properties**, **Rules**, and **Dashboard** pages.</span><span class="sxs-lookup"><span data-stu-id="e6f14-124">As an operator, you can view information about the device on the **Measurements**, **Settings**, **Properties**, **Rules**, and **Dashboard** pages.</span></span> <span data-ttu-id="e6f14-125">The builder customized the **Dashboard** to display important information about a connected air conditioner device.</span><span class="sxs-lookup"><span data-stu-id="e6f14-125">The builder customized the **Dashboard** to display important information about a connected air conditioner device.</span></span>

<span data-ttu-id="e6f14-126">Choose the **Dashboard** view to see information about the device.</span><span class="sxs-lookup"><span data-stu-id="e6f14-126">Choose the **Dashboard** view to see information about the device.</span></span>

![Device dashboard](media/tutorial-monitor-devices/initial_screen.png)

<span data-ttu-id="e6f14-128">The chart on the dashboard shows a plot of the device temperature.</span><span class="sxs-lookup"><span data-stu-id="e6f14-128">The chart on the dashboard shows a plot of the device temperature.</span></span> <span data-ttu-id="e6f14-129">You can also see the current target temperature for the device in the **Set target temperature** tile.</span><span class="sxs-lookup"><span data-stu-id="e6f14-129">You can also see the current target temperature for the device in the **Set target temperature** tile.</span></span> <span data-ttu-id="e6f14-130">You decide that the target temperature is too high.</span><span class="sxs-lookup"><span data-stu-id="e6f14-130">You decide that the target temperature is too high.</span></span>

## <a name="remediate-an-issue"></a><span data-ttu-id="e6f14-131">Remediate an issue</span><span class="sxs-lookup"><span data-stu-id="e6f14-131">Remediate an issue</span></span>

<span data-ttu-id="e6f14-132">To change the target temperature of the device, use the **Settings** page:</span><span class="sxs-lookup"><span data-stu-id="e6f14-132">To change the target temperature of the device, use the **Settings** page:</span></span>

1. <span data-ttu-id="e6f14-133">Choose **Settings**.</span><span class="sxs-lookup"><span data-stu-id="e6f14-133">Choose **Settings**.</span></span> <span data-ttu-id="e6f14-134">Change **Set Temperature** to 100.</span><span class="sxs-lookup"><span data-stu-id="e6f14-134">Change **Set Temperature** to 100.</span></span> <span data-ttu-id="e6f14-135">Choose **Update** to send the new target temperature to the device.</span><span class="sxs-lookup"><span data-stu-id="e6f14-135">Choose **Update** to send the new target temperature to the device.</span></span> <span data-ttu-id="e6f14-136">When the device acknowledges the settings change, the status of the setting value changes to **synced**:</span><span class="sxs-lookup"><span data-stu-id="e6f14-136">When the device acknowledges the settings change, the status of the setting value changes to **synced**:</span></span>

    ![Update settings](media/tutorial-monitor-devices/change_settings.png)

2. <span data-ttu-id="e6f14-138">Choose **Dashboard** and verify the new setting value:</span><span class="sxs-lookup"><span data-stu-id="e6f14-138">Choose **Dashboard** and verify the new setting value:</span></span>

    ![Updated device dashboard](media/tutorial-monitor-devices/new_settings.png)

## <a name="next-steps"></a><span data-ttu-id="e6f14-140">Next steps</span><span class="sxs-lookup"><span data-stu-id="e6f14-140">Next steps</span></span>

<span data-ttu-id="e6f14-141">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="e6f14-141">In this tutorial, you learned how to:</span></span>

> [!div class="nextstepaction"]
> * <span data-ttu-id="e6f14-142">Receive a notification</span><span class="sxs-lookup"><span data-stu-id="e6f14-142">Receive a notification</span></span>
> * <span data-ttu-id="e6f14-143">Investigate an issue</span><span class="sxs-lookup"><span data-stu-id="e6f14-143">Investigate an issue</span></span>
> * <span data-ttu-id="e6f14-144">Remediate an issue</span><span class="sxs-lookup"><span data-stu-id="e6f14-144">Remediate an issue</span></span>

<span data-ttu-id="e6f14-145">Now that you know now to monitor your device, the suggested next step is to [Add a device](tutorial-add-device.md).</span><span class="sxs-lookup"><span data-stu-id="e6f14-145">Now that you know now to monitor your device, the suggested next step is to [Add a device](tutorial-add-device.md).</span></span>