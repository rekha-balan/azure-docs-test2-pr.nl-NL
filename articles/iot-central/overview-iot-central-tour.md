---
title: Take a tour of the Azure IoT Central UI | Microsoft Docs
description: As a builder, become familiar with the key areas of the Azure IoT Central UI that you use to create an IoT solution.
author: tbhagwat3
ms.author: tanmayb
ms.date: 04/13/2018
ms.topic: overview
ms.service: iot-central
services: iot-central
ms.custom: mvc
manager: peterpr
ms.openlocfilehash: 69898358026eab716c057f339d8594df43db136f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857513"
---
# <a name="take-a-tour-of-the-azure-iot-central-ui"></a><span data-ttu-id="3861b-103">Take a tour of the Azure IoT Central UI</span><span class="sxs-lookup"><span data-stu-id="3861b-103">Take a tour of the Azure IoT Central UI</span></span>

<span data-ttu-id="3861b-104">This article introduces you to the Microsoft Azure IoT Central UI.</span><span class="sxs-lookup"><span data-stu-id="3861b-104">This article introduces you to the Microsoft Azure IoT Central UI.</span></span> <span data-ttu-id="3861b-105">You can use the UI to create, manage, and use an Azure IoT Central solution and its connected devices.</span><span class="sxs-lookup"><span data-stu-id="3861b-105">You can use the UI to create, manage, and use an Azure IoT Central solution and its connected devices.</span></span>

<span data-ttu-id="3861b-106">As a _builder_, you use the Azure IoT Central UI to define your Azure IoT Central solution.</span><span class="sxs-lookup"><span data-stu-id="3861b-106">As a _builder_, you use the Azure IoT Central UI to define your Azure IoT Central solution.</span></span> <span data-ttu-id="3861b-107">You can use the UI to:</span><span class="sxs-lookup"><span data-stu-id="3861b-107">You can use the UI to:</span></span>

- <span data-ttu-id="3861b-108">Define the types of device that connect to your solution.</span><span class="sxs-lookup"><span data-stu-id="3861b-108">Define the types of device that connect to your solution.</span></span>
- <span data-ttu-id="3861b-109">Configure the rules and actions for your devices.</span><span class="sxs-lookup"><span data-stu-id="3861b-109">Configure the rules and actions for your devices.</span></span>
- <span data-ttu-id="3861b-110">Customize the UI for an _operator_ who uses your solution.</span><span class="sxs-lookup"><span data-stu-id="3861b-110">Customize the UI for an _operator_ who uses your solution.</span></span>

<span data-ttu-id="3861b-111">As an _operator_, you use the Azure IoT Central UI to manage your Azure IoT Central solution.</span><span class="sxs-lookup"><span data-stu-id="3861b-111">As an _operator_, you use the Azure IoT Central UI to manage your Azure IoT Central solution.</span></span> <span data-ttu-id="3861b-112">You can use the UI to:</span><span class="sxs-lookup"><span data-stu-id="3861b-112">You can use the UI to:</span></span>

- <span data-ttu-id="3861b-113">Monitor your devices.</span><span class="sxs-lookup"><span data-stu-id="3861b-113">Monitor your devices.</span></span>
- <span data-ttu-id="3861b-114">Configure your devices.</span><span class="sxs-lookup"><span data-stu-id="3861b-114">Configure your devices.</span></span>
- <span data-ttu-id="3861b-115">Troubleshoot and remediate issues with your devices.</span><span class="sxs-lookup"><span data-stu-id="3861b-115">Troubleshoot and remediate issues with your devices.</span></span>
- <span data-ttu-id="3861b-116">Provision new devices.</span><span class="sxs-lookup"><span data-stu-id="3861b-116">Provision new devices.</span></span>

## <a name="use-the-left-navigation-menu"></a><span data-ttu-id="3861b-117">Use the left navigation menu</span><span class="sxs-lookup"><span data-stu-id="3861b-117">Use the left navigation menu</span></span>

<span data-ttu-id="3861b-118">Use the left navigation menu to access the different areas of the application:</span><span class="sxs-lookup"><span data-stu-id="3861b-118">Use the left navigation menu to access the different areas of the application:</span></span>

| <span data-ttu-id="3861b-119">Menu</span><span class="sxs-lookup"><span data-stu-id="3861b-119">Menu</span></span> | <span data-ttu-id="3861b-120">Description</span><span class="sxs-lookup"><span data-stu-id="3861b-120">Description</span></span> |
| ---- | ----------- |
| ![Left navigation menu](media/overview-iot-central-tour/navigationbar.png) | <ul><li><span data-ttu-id="3861b-122">The **Home** button displays the home page of your application.</span><span class="sxs-lookup"><span data-stu-id="3861b-122">The **Home** button displays the home page of your application.</span></span> <span data-ttu-id="3861b-123">As a builder, you can customize this home page for your operators.</span><span class="sxs-lookup"><span data-stu-id="3861b-123">As a builder, you can customize this home page for your operators.</span></span></li><li><span data-ttu-id="3861b-124">The **Device Explorer** button lists both the device templates defined in your application, and the simulated and real devices associated with each device template.</span><span class="sxs-lookup"><span data-stu-id="3861b-124">The **Device Explorer** button lists both the device templates defined in your application, and the simulated and real devices associated with each device template.</span></span> <span data-ttu-id="3861b-125">As an operator, you use the **Device Explorer** to manage your connected devices.</span><span class="sxs-lookup"><span data-stu-id="3861b-125">As an operator, you use the **Device Explorer** to manage your connected devices.</span></span></li><li><span data-ttu-id="3861b-126">The **Device Sets** button enables you to view and create device sets.</span><span class="sxs-lookup"><span data-stu-id="3861b-126">The **Device Sets** button enables you to view and create device sets.</span></span> <span data-ttu-id="3861b-127">As an operator, you can create device sets as a logical collection of devices specified by a query.</span><span class="sxs-lookup"><span data-stu-id="3861b-127">As an operator, you can create device sets as a logical collection of devices specified by a query.</span></span></li><li><span data-ttu-id="3861b-128">The **Analytics** button shows analytics derived from device telemetry for devices and device sets.</span><span class="sxs-lookup"><span data-stu-id="3861b-128">The **Analytics** button shows analytics derived from device telemetry for devices and device sets.</span></span> <span data-ttu-id="3861b-129">As an operator, you can create custom views on top of device data to derive insights from your application.</span><span class="sxs-lookup"><span data-stu-id="3861b-129">As an operator, you can create custom views on top of device data to derive insights from your application.</span></span></li><li><span data-ttu-id="3861b-130">The **Application Builder** button shows the tools a builder uses, such as the **Create Device Template** tool.</span><span class="sxs-lookup"><span data-stu-id="3861b-130">The **Application Builder** button shows the tools a builder uses, such as the **Create Device Template** tool.</span></span></li><li><span data-ttu-id="3861b-131">The **Administration** button shows the application administration pages where an administrator can manage application settings, users, and roles.</span><span class="sxs-lookup"><span data-stu-id="3861b-131">The **Administration** button shows the application administration pages where an administrator can manage application settings, users, and roles.</span></span></li></ul> |

## <a name="search-help-and-support"></a><span data-ttu-id="3861b-132">Search, help, and support</span><span class="sxs-lookup"><span data-stu-id="3861b-132">Search, help, and support</span></span>

<span data-ttu-id="3861b-133">The top menu appears on every page:</span><span class="sxs-lookup"><span data-stu-id="3861b-133">The top menu appears on every page:</span></span>

![Toolbar](media/overview-iot-central-tour/toolbar.png)

- <span data-ttu-id="3861b-135">To search for device templates and devices, choose the **Search** icon.</span><span class="sxs-lookup"><span data-stu-id="3861b-135">To search for device templates and devices, choose the **Search** icon.</span></span>
- <span data-ttu-id="3861b-136">To get help and support, choose the **Help** drop-down for a list of resources.</span><span class="sxs-lookup"><span data-stu-id="3861b-136">To get help and support, choose the **Help** drop-down for a list of resources.</span></span>
- <span data-ttu-id="3861b-137">To control the tutorials, change the UI theme, or sign out of the application, choose the **Account** icon.</span><span class="sxs-lookup"><span data-stu-id="3861b-137">To control the tutorials, change the UI theme, or sign out of the application, choose the **Account** icon.</span></span>

<span data-ttu-id="3861b-138">You can choose between a light theme or a dark theme for the UI:</span><span class="sxs-lookup"><span data-stu-id="3861b-138">You can choose between a light theme or a dark theme for the UI:</span></span>

![Choose a theme for the UI](media/overview-iot-central-tour/themes.png)

## <a name="home-page"></a><span data-ttu-id="3861b-140">Home page</span><span class="sxs-lookup"><span data-stu-id="3861b-140">Home page</span></span>

![Home page](media/overview-iot-central-tour/homepage.png)

<span data-ttu-id="3861b-142">The home page is the first page you see when you sign in to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="3861b-142">The home page is the first page you see when you sign in to your Azure IoT Central application.</span></span> <span data-ttu-id="3861b-143">As a builder, you can customize the home page for other users of the application by adding tiles.</span><span class="sxs-lookup"><span data-stu-id="3861b-143">As a builder, you can customize the home page for other users of the application by adding tiles.</span></span> <span data-ttu-id="3861b-144">To learn more, see the [Customize the Azure IoT Central operator's view](tutorial-customize-operator.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="3861b-144">To learn more, see the [Customize the Azure IoT Central operator's view](tutorial-customize-operator.md) tutorial.</span></span>

## <a name="device-explorer"></a><span data-ttu-id="3861b-145">Device explorer</span><span class="sxs-lookup"><span data-stu-id="3861b-145">Device explorer</span></span>

![Explorer page](media/overview-iot-central-tour/explorer.png)

<span data-ttu-id="3861b-147">The explorer page shows the _device templates_ and _devices_ in your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="3861b-147">The explorer page shows the _device templates_ and _devices_ in your Azure IoT Central application.</span></span>

* <span data-ttu-id="3861b-148">A device template defines a type of device that can connect to your application.</span><span class="sxs-lookup"><span data-stu-id="3861b-148">A device template defines a type of device that can connect to your application.</span></span> <span data-ttu-id="3861b-149">To learn more, see the [Define a new device type in your Azure IoT Central application](tutorial-define-device-type.md).</span><span class="sxs-lookup"><span data-stu-id="3861b-149">To learn more, see the [Define a new device type in your Azure IoT Central application](tutorial-define-device-type.md).</span></span>
* <span data-ttu-id="3861b-150">A device represents either a real or simulated device in your application.</span><span class="sxs-lookup"><span data-stu-id="3861b-150">A device represents either a real or simulated device in your application.</span></span> <span data-ttu-id="3861b-151">To learn more, see the [Add a new device to your Azure IoT Central application](tutorial-add-device.md).</span><span class="sxs-lookup"><span data-stu-id="3861b-151">To learn more, see the [Add a new device to your Azure IoT Central application](tutorial-add-device.md).</span></span>

## <a name="device-sets"></a><span data-ttu-id="3861b-152">Device sets</span><span class="sxs-lookup"><span data-stu-id="3861b-152">Device sets</span></span>

![Device Sets page](media/overview-iot-central-tour/devicesets.png)

<span data-ttu-id="3861b-154">The _device sets_ page shows device sets created by the builder.</span><span class="sxs-lookup"><span data-stu-id="3861b-154">The _device sets_ page shows device sets created by the builder.</span></span> <span data-ttu-id="3861b-155">A device set is a collection of related devices.</span><span class="sxs-lookup"><span data-stu-id="3861b-155">A device set is a collection of related devices.</span></span> <span data-ttu-id="3861b-156">A builder defines a query to identify the devices that are included in a device set.</span><span class="sxs-lookup"><span data-stu-id="3861b-156">A builder defines a query to identify the devices that are included in a device set.</span></span> <span data-ttu-id="3861b-157">You use device sets when you customize the analytics in your application.</span><span class="sxs-lookup"><span data-stu-id="3861b-157">You use device sets when you customize the analytics in your application.</span></span> <span data-ttu-id="3861b-158">To learn more, see the [Use device sets in your Azure IoT Central application](howto-use-device-sets.md) article.</span><span class="sxs-lookup"><span data-stu-id="3861b-158">To learn more, see the [Use device sets in your Azure IoT Central application](howto-use-device-sets.md) article.</span></span>

## <a name="analytics"></a><span data-ttu-id="3861b-159">Analytics</span><span class="sxs-lookup"><span data-stu-id="3861b-159">Analytics</span></span>

![Analytics page](media/overview-iot-central-tour/analytics.png)

<span data-ttu-id="3861b-161">The analytics page shows charts that help you understand how the devices connected to your application are behaving.</span><span class="sxs-lookup"><span data-stu-id="3861b-161">The analytics page shows charts that help you understand how the devices connected to your application are behaving.</span></span> <span data-ttu-id="3861b-162">An operator uses this page to monitor and investigate issues with connected devices.</span><span class="sxs-lookup"><span data-stu-id="3861b-162">An operator uses this page to monitor and investigate issues with connected devices.</span></span> <span data-ttu-id="3861b-163">The builder can define the charts shown on this page.</span><span class="sxs-lookup"><span data-stu-id="3861b-163">The builder can define the charts shown on this page.</span></span> <span data-ttu-id="3861b-164">To learn more, see the [Create custom analytics for your Azure IoT Central application](howto-create-analytics.md) article.</span><span class="sxs-lookup"><span data-stu-id="3861b-164">To learn more, see the [Create custom analytics for your Azure IoT Central application](howto-create-analytics.md) article.</span></span>

## <a name="application-builder"></a><span data-ttu-id="3861b-165">Application Builder</span><span class="sxs-lookup"><span data-stu-id="3861b-165">Application Builder</span></span>

![Application Builder page](media/overview-iot-central-tour/applicationbuilder.png)

<span data-ttu-id="3861b-167">The application builder page contains links to the tools a builder uses to create an Azure IoT Central application, such as creating device templates and configuring the home page.</span><span class="sxs-lookup"><span data-stu-id="3861b-167">The application builder page contains links to the tools a builder uses to create an Azure IoT Central application, such as creating device templates and configuring the home page.</span></span> <span data-ttu-id="3861b-168">To learn more, see the [Define a new device type in your Azure IoT Central application](tutorial-define-device-type.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="3861b-168">To learn more, see the [Define a new device type in your Azure IoT Central application](tutorial-define-device-type.md) tutorial.</span></span>

## <a name="administration"></a><span data-ttu-id="3861b-169">Administration</span><span class="sxs-lookup"><span data-stu-id="3861b-169">Administration</span></span>

![Administration page](media/overview-iot-central-tour/administration.png)

<span data-ttu-id="3861b-171">The administration page contains links to the tools an administrator uses such as defining users and roles in the application.</span><span class="sxs-lookup"><span data-stu-id="3861b-171">The administration page contains links to the tools an administrator uses such as defining users and roles in the application.</span></span> <span data-ttu-id="3861b-172">To learn more, see the [Administer your Azure IoT Central application](howto-administer.md) article.</span><span class="sxs-lookup"><span data-stu-id="3861b-172">To learn more, see the [Administer your Azure IoT Central application](howto-administer.md) article.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3861b-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="3861b-173">Next steps</span></span>

<span data-ttu-id="3861b-174">Now that you have an overview of Azure IoT Central and are familiar with the layout of the UI, the suggested next step is to complete the [Create an Azure IoT Central application](quick-deploy-iot-central.md) quickstart.</span><span class="sxs-lookup"><span data-stu-id="3861b-174">Now that you have an overview of Azure IoT Central and are familiar with the layout of the UI, the suggested next step is to complete the [Create an Azure IoT Central application](quick-deploy-iot-central.md) quickstart.</span></span>