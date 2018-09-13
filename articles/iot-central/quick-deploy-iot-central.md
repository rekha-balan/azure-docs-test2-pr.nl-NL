---
title: Create an Azure IoT Central application | Microsoft Docs
description: Create a new Azure IoT Central application to manage refigerated vending devices. View the telemetry data generated from your simulated devices.
author: tbhagwat3
ms.author: tanmayb
ms.date: 04/15/2018
ms.topic: quickstart
ms.service: iot-central
services: iot-central
ms.custom: mvc
manager: peterpr
ms.openlocfilehash: 51c6753b1e4f2b08e93214abfcd7e18cb2e66613
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856794"
---
# <a name="create-an-azure-iot-central-application"></a><span data-ttu-id="f7edf-104">Create an Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="f7edf-104">Create an Azure IoT Central application</span></span>

<span data-ttu-id="f7edf-105">As a _builder_, you use the Azure IoT Central UI to define your Microsoft Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="f7edf-105">As a _builder_, you use the Azure IoT Central UI to define your Microsoft Azure IoT Central application.</span></span> <span data-ttu-id="f7edf-106">This quickstart shows you how to:</span><span class="sxs-lookup"><span data-stu-id="f7edf-106">This quickstart shows you how to:</span></span>

- <span data-ttu-id="f7edf-107">Create an Azure IoT Central application that contains a sample _device template_ and simulated _devices_.</span><span class="sxs-lookup"><span data-stu-id="f7edf-107">Create an Azure IoT Central application that contains a sample _device template_ and simulated _devices_.</span></span>
- <span data-ttu-id="f7edf-108">View the features of the **Refrigerated Vending Machine** device template in your application.</span><span class="sxs-lookup"><span data-stu-id="f7edf-108">View the features of the **Refrigerated Vending Machine** device template in your application.</span></span>
- <span data-ttu-id="f7edf-109">View the telemetry and analytics from your simulated **Refrigerator** devices.</span><span class="sxs-lookup"><span data-stu-id="f7edf-109">View the telemetry and analytics from your simulated **Refrigerator** devices.</span></span>

<span data-ttu-id="f7edf-110">In this quickstart, you view a simulated **Refrigerator** device from a device template.</span><span class="sxs-lookup"><span data-stu-id="f7edf-110">In this quickstart, you view a simulated **Refrigerator** device from a device template.</span></span> <span data-ttu-id="f7edf-111">The simulated device:</span><span class="sxs-lookup"><span data-stu-id="f7edf-111">The simulated device:</span></span>

* <span data-ttu-id="f7edf-112">Sends telemetry, such as temperature and pressure, to your application.</span><span class="sxs-lookup"><span data-stu-id="f7edf-112">Sends telemetry, such as temperature and pressure, to your application.</span></span>
* <span data-ttu-id="f7edf-113">Reports device property values, such as a motion alert, to your application.</span><span class="sxs-lookup"><span data-stu-id="f7edf-113">Reports device property values, such as a motion alert, to your application.</span></span>
* <span data-ttu-id="f7edf-114">Has device settings, such as fan speed, that you can set in the application.</span><span class="sxs-lookup"><span data-stu-id="f7edf-114">Has device settings, such as fan speed, that you can set in the application.</span></span>

<span data-ttu-id="f7edf-115">When you create a simulated device from a device template in an Azure IoT Central application, the simulated device enables you to test your application before you connect a real device.</span><span class="sxs-lookup"><span data-stu-id="f7edf-115">When you create a simulated device from a device template in an Azure IoT Central application, the simulated device enables you to test your application before you connect a real device.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="f7edf-116">Create the application</span><span class="sxs-lookup"><span data-stu-id="f7edf-116">Create the application</span></span>

<span data-ttu-id="f7edf-117">To complete this quickstart, you need to create an Azure IoT Central application from the **Sample Contoso** application template.</span><span class="sxs-lookup"><span data-stu-id="f7edf-117">To complete this quickstart, you need to create an Azure IoT Central application from the **Sample Contoso** application template.</span></span>

<span data-ttu-id="f7edf-118">Navigate to the Azure IoT Central [Application Manager](https://aka.ms/iotcentral) page.</span><span class="sxs-lookup"><span data-stu-id="f7edf-118">Navigate to the Azure IoT Central [Application Manager](https://aka.ms/iotcentral) page.</span></span> <span data-ttu-id="f7edf-119">Then enter the email address and password you use to access your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="f7edf-119">Then enter the email address and password you use to access your Azure subscription:</span></span>

![Enter your organization account](media/quick-deploy-iot-central/sign-in.png)

<span data-ttu-id="f7edf-121">To start creating a new Azure IoT Central application, choose **New Application**:</span><span class="sxs-lookup"><span data-stu-id="f7edf-121">To start creating a new Azure IoT Central application, choose **New Application**:</span></span>

![Azure IoT Central Application Manager page](media/quick-deploy-iot-central/iotcentralhome.png)

<span data-ttu-id="f7edf-123">To create a new Azure IoT Central application:</span><span class="sxs-lookup"><span data-stu-id="f7edf-123">To create a new Azure IoT Central application:</span></span>

1. <span data-ttu-id="f7edf-124">Choose the **Free Trial Application** payment plan.</span><span class="sxs-lookup"><span data-stu-id="f7edf-124">Choose the **Free Trial Application** payment plan.</span></span>
1. <span data-ttu-id="f7edf-125">Choose a friendly application name, such as **Contoso IoT**.</span><span class="sxs-lookup"><span data-stu-id="f7edf-125">Choose a friendly application name, such as **Contoso IoT**.</span></span> <span data-ttu-id="f7edf-126">Azure IoT Central generates a unique URL prefix for you.</span><span class="sxs-lookup"><span data-stu-id="f7edf-126">Azure IoT Central generates a unique URL prefix for you.</span></span> <span data-ttu-id="f7edf-127">You can change this URL prefix to something more memorable.</span><span class="sxs-lookup"><span data-stu-id="f7edf-127">You can change this URL prefix to something more memorable.</span></span>
1. <span data-ttu-id="f7edf-128">Choose the **Sample Contoso** application template.</span><span class="sxs-lookup"><span data-stu-id="f7edf-128">Choose the **Sample Contoso** application template.</span></span>
1. <span data-ttu-id="f7edf-129">Then choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="f7edf-129">Then choose **Create**.</span></span>

![Azure IoT Central Create Application page](media/quick-deploy-iot-central/iotcentralcreate.png)

## <a name="navigate-to-the-application"></a><span data-ttu-id="f7edf-131">Navigate to the application</span><span class="sxs-lookup"><span data-stu-id="f7edf-131">Navigate to the application</span></span>

<span data-ttu-id="f7edf-132">When your application is ready, the **Homepage** of your application displays.</span><span class="sxs-lookup"><span data-stu-id="f7edf-132">When your application is ready, the **Homepage** of your application displays.</span></span> <span data-ttu-id="f7edf-133">The _Design Mode_ on the top right can be toggled to edit the Homepage.</span><span class="sxs-lookup"><span data-stu-id="f7edf-133">The _Design Mode_ on the top right can be toggled to edit the Homepage.</span></span> <span data-ttu-id="f7edf-134">The application URL is the URL you specified in the previous step:</span><span class="sxs-lookup"><span data-stu-id="f7edf-134">The application URL is the URL you specified in the previous step:</span></span>

![Application Builder page](media/quick-deploy-iot-central/apphome.png)

<span data-ttu-id="f7edf-136">Use the _left navigation menu_ to access the different areas of your new Azure IoT Central application:</span><span class="sxs-lookup"><span data-stu-id="f7edf-136">Use the _left navigation menu_ to access the different areas of your new Azure IoT Central application:</span></span>

![Left navigation menu](media/quick-deploy-iot-central/navbar.png)

<span data-ttu-id="f7edf-138">To view the device templates and devices in your application, choose **Device Explorer** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="f7edf-138">To view the device templates and devices in your application, choose **Device Explorer** on the left navigation menu.</span></span> <span data-ttu-id="f7edf-139">The sample application includes the **Refrigerated Vending Machine** device template.</span><span class="sxs-lookup"><span data-stu-id="f7edf-139">The sample application includes the **Refrigerated Vending Machine** device template.</span></span> <span data-ttu-id="f7edf-140">There are three simulated devices already created from this device template:</span><span class="sxs-lookup"><span data-stu-id="f7edf-140">There are three simulated devices already created from this device template:</span></span>

![Device explorer](media/quick-deploy-iot-central/deviceexplorer.png)

## <a name="view-the-device-template-and-devices"></a><span data-ttu-id="f7edf-142">View the device template and devices</span><span class="sxs-lookup"><span data-stu-id="f7edf-142">View the device template and devices</span></span>

<span data-ttu-id="f7edf-143">Use the following steps to view a refrigerator device that was created from the **Refrigerated Vending Machine** device template.</span><span class="sxs-lookup"><span data-stu-id="f7edf-143">Use the following steps to view a refrigerator device that was created from the **Refrigerated Vending Machine** device template.</span></span> <span data-ttu-id="f7edf-144">A device template defines:</span><span class="sxs-lookup"><span data-stu-id="f7edf-144">A device template defines:</span></span>

* <span data-ttu-id="f7edf-145">_Measurements_, such as temperature telemetry, sent from a device.</span><span class="sxs-lookup"><span data-stu-id="f7edf-145">_Measurements_, such as temperature telemetry, sent from a device.</span></span>
* <span data-ttu-id="f7edf-146">_Settings_, such as fan speed, that enable you to control the device.</span><span class="sxs-lookup"><span data-stu-id="f7edf-146">_Settings_, such as fan speed, that enable you to control the device.</span></span>
* <span data-ttu-id="f7edf-147">_Properties_, such as serial number, that store information about the device.</span><span class="sxs-lookup"><span data-stu-id="f7edf-147">_Properties_, such as serial number, that store information about the device.</span></span>
* <span data-ttu-id="f7edf-148">[Rules](howto-create-telemetry-rules.md) that enable you to automate actions based on the behavior of the device.</span><span class="sxs-lookup"><span data-stu-id="f7edf-148">[Rules](howto-create-telemetry-rules.md) that enable you to automate actions based on the behavior of the device.</span></span>
* <span data-ttu-id="f7edf-149">A customizable _dashboard_ that displays information about the device.</span><span class="sxs-lookup"><span data-stu-id="f7edf-149">A customizable _dashboard_ that displays information about the device.</span></span>

<span data-ttu-id="f7edf-150">You can create both simulated and real devices from a device template.</span><span class="sxs-lookup"><span data-stu-id="f7edf-150">You can create both simulated and real devices from a device template.</span></span>

### <a name="measurements"></a><span data-ttu-id="f7edf-151">Measurements</span><span class="sxs-lookup"><span data-stu-id="f7edf-151">Measurements</span></span>

<span data-ttu-id="f7edf-152">The **Measurements** page for the **Refrigerator 1** device displays.</span><span class="sxs-lookup"><span data-stu-id="f7edf-152">The **Measurements** page for the **Refrigerator 1** device displays.</span></span> <span data-ttu-id="f7edf-153">You can see the list of measurements sent from the simulated device.</span><span class="sxs-lookup"><span data-stu-id="f7edf-153">You can see the list of measurements sent from the simulated device.</span></span> <span data-ttu-id="f7edf-154">The page also displays a customizable chart of the visible measurements:</span><span class="sxs-lookup"><span data-stu-id="f7edf-154">The page also displays a customizable chart of the visible measurements:</span></span>

![Measurements page](media/quick-deploy-iot-central/measurements.png)

<span data-ttu-id="f7edf-156">You can toggle the visibility of individual elements and customize the chart.</span><span class="sxs-lookup"><span data-stu-id="f7edf-156">You can toggle the visibility of individual elements and customize the chart.</span></span> <span data-ttu-id="f7edf-157">The current chart shows telemetry from a simulated device.</span><span class="sxs-lookup"><span data-stu-id="f7edf-157">The current chart shows telemetry from a simulated device.</span></span> <span data-ttu-id="f7edf-158">You can add new measurements to the device template if you have appropriate permissions.</span><span class="sxs-lookup"><span data-stu-id="f7edf-158">You can add new measurements to the device template if you have appropriate permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="f7edf-159">You may need to wait for a short while before the simulated data appears on the chart.</span><span class="sxs-lookup"><span data-stu-id="f7edf-159">You may need to wait for a short while before the simulated data appears on the chart.</span></span>

### <a name="settings"></a><span data-ttu-id="f7edf-160">Settings</span><span class="sxs-lookup"><span data-stu-id="f7edf-160">Settings</span></span>

<span data-ttu-id="f7edf-161">Choose **Settings**.</span><span class="sxs-lookup"><span data-stu-id="f7edf-161">Choose **Settings**.</span></span> <span data-ttu-id="f7edf-162">On the **Settings** page, you can control the device.</span><span class="sxs-lookup"><span data-stu-id="f7edf-162">On the **Settings** page, you can control the device.</span></span> <span data-ttu-id="f7edf-163">For example, you can update the fan speed on the refrigerator:</span><span class="sxs-lookup"><span data-stu-id="f7edf-163">For example, you can update the fan speed on the refrigerator:</span></span>

![Settings](media/quick-deploy-iot-central/settings.png)

<span data-ttu-id="f7edf-165">A setting shows as **synced** when a device acknowledges the change.</span><span class="sxs-lookup"><span data-stu-id="f7edf-165">A setting shows as **synced** when a device acknowledges the change.</span></span>

### <a name="properties"></a><span data-ttu-id="f7edf-166">Properties</span><span class="sxs-lookup"><span data-stu-id="f7edf-166">Properties</span></span>

<span data-ttu-id="f7edf-167">Choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="f7edf-167">Choose **Properties**.</span></span> <span data-ttu-id="f7edf-168">On the **Properties** page, you can:</span><span class="sxs-lookup"><span data-stu-id="f7edf-168">On the **Properties** page, you can:</span></span>

* <span data-ttu-id="f7edf-169">Maintain information about your device, such as the customer name.</span><span class="sxs-lookup"><span data-stu-id="f7edf-169">Maintain information about your device, such as the customer name.</span></span>
* <span data-ttu-id="f7edf-170">View property values reported by the device, such as a motion alert.</span><span class="sxs-lookup"><span data-stu-id="f7edf-170">View property values reported by the device, such as a motion alert.</span></span>

![Properties](media/quick-deploy-iot-central/properties.png)

### <a name="dashboard"></a><span data-ttu-id="f7edf-172">Dashboard</span><span class="sxs-lookup"><span data-stu-id="f7edf-172">Dashboard</span></span>

<span data-ttu-id="f7edf-173">Choose **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="f7edf-173">Choose **Dashboard**.</span></span> <span data-ttu-id="f7edf-174">The dashboard is a customizable view of information about your device such as measurements, properties, and KPIs:</span><span class="sxs-lookup"><span data-stu-id="f7edf-174">The dashboard is a customizable view of information about your device such as measurements, properties, and KPIs:</span></span>

![Dashboard](media/quick-deploy-iot-central/dashboard.png)

## <a name="view-analytics"></a><span data-ttu-id="f7edf-176">View analytics</span><span class="sxs-lookup"><span data-stu-id="f7edf-176">View analytics</span></span>

<span data-ttu-id="f7edf-177">The previous section showed you how to view information about an individual device.</span><span class="sxs-lookup"><span data-stu-id="f7edf-177">The previous section showed you how to view information about an individual device.</span></span> <span data-ttu-id="f7edf-178">You can use [device sets](howto-use-device-sets.md) and [analytics](howto-create-analytics.md) to view consolidated information from multiple devices.</span><span class="sxs-lookup"><span data-stu-id="f7edf-178">You can use [device sets](howto-use-device-sets.md) and [analytics](howto-create-analytics.md) to view consolidated information from multiple devices.</span></span>

<span data-ttu-id="f7edf-179">A device set uses a query to dynamically select a set of devices that match a criteria.</span><span class="sxs-lookup"><span data-stu-id="f7edf-179">A device set uses a query to dynamically select a set of devices that match a criteria.</span></span> <span data-ttu-id="f7edf-180">For example, the **Machines in Seattle** device set selects refrigerator devices whose location is Seattle.</span><span class="sxs-lookup"><span data-stu-id="f7edf-180">For example, the **Machines in Seattle** device set selects refrigerator devices whose location is Seattle.</span></span> <span data-ttu-id="f7edf-181">To view the **Machines in Seattle** device set, choose **Device Sets** in the left navigation menu, and then choose **Machines in Seattle**:</span><span class="sxs-lookup"><span data-stu-id="f7edf-181">To view the **Machines in Seattle** device set, choose **Device Sets** in the left navigation menu, and then choose **Machines in Seattle**:</span></span>

![Machines in Seattle device set](media/quick-deploy-iot-central/deviceset.png)

<span data-ttu-id="f7edf-183">You can view analytics data for the devices in a device set on the **Analytics** page:</span><span class="sxs-lookup"><span data-stu-id="f7edf-183">You can view analytics data for the devices in a device set on the **Analytics** page:</span></span>

![Analytics for machines in Seattle](media/quick-deploy-iot-central/analytics.png)

## <a name="next-steps"></a><span data-ttu-id="f7edf-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="f7edf-185">Next steps</span></span>

<span data-ttu-id="f7edf-186">In this quickstart, you created a pre-populated Azure IoT Central application that contains a **Refrigerated Vending Machine** device template and simulated devices.</span><span class="sxs-lookup"><span data-stu-id="f7edf-186">In this quickstart, you created a pre-populated Azure IoT Central application that contains a **Refrigerated Vending Machine** device template and simulated devices.</span></span> <span data-ttu-id="f7edf-187">See [Define a new device template in your application](tutorial-define-device-type.md) to learn more, as a builder, about how to define your own device templates.</span><span class="sxs-lookup"><span data-stu-id="f7edf-187">See [Define a new device template in your application](tutorial-define-device-type.md) to learn more, as a builder, about how to define your own device templates.</span></span>
