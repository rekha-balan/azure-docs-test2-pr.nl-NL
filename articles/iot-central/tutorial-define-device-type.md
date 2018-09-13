---
title: Define a new device type in Azure IoT Central | Microsoft Docs
description: This tutorial shows you, as a builder, how to define a new device type in your Azure IoT Central application. You define the telemetry, state, properties and settings for your type.
author: tbhagwat3
ms.author: tanmayb
ms.date: 04/16/2018
ms.topic: tutorial
ms.service: iot-central
services: iot-central
ms.custom: mvc
manager: peterpr
ms.openlocfilehash: a2601f55bbc7e99321689afdafcab3135b94bd5b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856386"
---
# <a name="tutorial-define-a-new-device-type-in-your-azure-iot-central-application"></a><span data-ttu-id="a3d40-104">Tutorial: Define a new device type in your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="a3d40-104">Tutorial: Define a new device type in your Azure IoT Central application</span></span>

<span data-ttu-id="a3d40-105">This tutorial shows you, as a builder, how to use a device template to define a new type of device in your Microsoft Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="a3d40-105">This tutorial shows you, as a builder, how to use a device template to define a new type of device in your Microsoft Azure IoT Central application.</span></span> <span data-ttu-id="a3d40-106">A device template defines the telemetry, state, properties, and settings for your device type.</span><span class="sxs-lookup"><span data-stu-id="a3d40-106">A device template defines the telemetry, state, properties, and settings for your device type.</span></span>

<span data-ttu-id="a3d40-107">To enable you to test your application before you connect a real device, Azure IoT Central generates a simulated device from the device template when you create it.</span><span class="sxs-lookup"><span data-stu-id="a3d40-107">To enable you to test your application before you connect a real device, Azure IoT Central generates a simulated device from the device template when you create it.</span></span>

<span data-ttu-id="a3d40-108">In this tutorial, you create a **Connected Air Conditioner** device template.</span><span class="sxs-lookup"><span data-stu-id="a3d40-108">In this tutorial, you create a **Connected Air Conditioner** device template.</span></span> <span data-ttu-id="a3d40-109">A connected air conditioner device:</span><span class="sxs-lookup"><span data-stu-id="a3d40-109">A connected air conditioner device:</span></span>

* <span data-ttu-id="a3d40-110">Sends telemetry such as temperature and humidity.</span><span class="sxs-lookup"><span data-stu-id="a3d40-110">Sends telemetry such as temperature and humidity.</span></span>
* <span data-ttu-id="a3d40-111">Reports state such as whether it is on or off.</span><span class="sxs-lookup"><span data-stu-id="a3d40-111">Reports state such as whether it is on or off.</span></span>
* <span data-ttu-id="a3d40-112">Has properties such as firmware version and serial number.</span><span class="sxs-lookup"><span data-stu-id="a3d40-112">Has properties such as firmware version and serial number.</span></span>
* <span data-ttu-id="a3d40-113">Has settings such as target temperature and fan speed.</span><span class="sxs-lookup"><span data-stu-id="a3d40-113">Has settings such as target temperature and fan speed.</span></span>

<span data-ttu-id="a3d40-114">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="a3d40-114">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a3d40-115">Create a new device template</span><span class="sxs-lookup"><span data-stu-id="a3d40-115">Create a new device template</span></span>
> * <span data-ttu-id="a3d40-116">Add telemetry to your device</span><span class="sxs-lookup"><span data-stu-id="a3d40-116">Add telemetry to your device</span></span>
> * <span data-ttu-id="a3d40-117">View simulated telemetry</span><span class="sxs-lookup"><span data-stu-id="a3d40-117">View simulated telemetry</span></span>
> * <span data-ttu-id="a3d40-118">Define event measurement</span><span class="sxs-lookup"><span data-stu-id="a3d40-118">Define event measurement</span></span>
> * <span data-ttu-id="a3d40-119">View simulated events</span><span class="sxs-lookup"><span data-stu-id="a3d40-119">View simulated events</span></span>
> * <span data-ttu-id="a3d40-120">Define state measurement</span><span class="sxs-lookup"><span data-stu-id="a3d40-120">Define state measurement</span></span>
> * <span data-ttu-id="a3d40-121">View simulated state</span><span class="sxs-lookup"><span data-stu-id="a3d40-121">View simulated state</span></span>
> * <span data-ttu-id="a3d40-122">Use device properties</span><span class="sxs-lookup"><span data-stu-id="a3d40-122">Use device properties</span></span>
> * <span data-ttu-id="a3d40-123">Use device settings</span><span class="sxs-lookup"><span data-stu-id="a3d40-123">Use device settings</span></span>
> * <span data-ttu-id="a3d40-124">Use commands</span><span class="sxs-lookup"><span data-stu-id="a3d40-124">Use commands</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3d40-125">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a3d40-125">Prerequisites</span></span>

<span data-ttu-id="a3d40-126">To complete this tutorial, you need an Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="a3d40-126">To complete this tutorial, you need an Azure IoT Central application.</span></span> <span data-ttu-id="a3d40-127">If you completed the [Create an Azure IoT Central application](quick-deploy-iot-central.md) quickstart, you can reuse the application you created in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="a3d40-127">If you completed the [Create an Azure IoT Central application](quick-deploy-iot-central.md) quickstart, you can reuse the application you created in the quickstart.</span></span> <span data-ttu-id="a3d40-128">Otherwise, complete the following steps to create an empty Azure IoT Central application:</span><span class="sxs-lookup"><span data-stu-id="a3d40-128">Otherwise, complete the following steps to create an empty Azure IoT Central application:</span></span>

1. <span data-ttu-id="a3d40-129">Navigate to the Azure IoT Central [Application Manager](https://aka.ms/iotcentral) page.</span><span class="sxs-lookup"><span data-stu-id="a3d40-129">Navigate to the Azure IoT Central [Application Manager](https://aka.ms/iotcentral) page.</span></span>

2. <span data-ttu-id="a3d40-130">Enter the email address and password you use to access your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="a3d40-130">Enter the email address and password you use to access your Azure subscription:</span></span>

   ![Enter your organization account](./media/tutorial-define-device-type/sign-in.png)

3. <span data-ttu-id="a3d40-132">To start creating a new Azure IoT Central application, choose **New Application**:</span><span class="sxs-lookup"><span data-stu-id="a3d40-132">To start creating a new Azure IoT Central application, choose **New Application**:</span></span>

    ![Azure IoT Central Application Manager page](./media/tutorial-define-device-type/iotcentralhome.png)

4. <span data-ttu-id="a3d40-134">To create a new Azure IoT Central application:</span><span class="sxs-lookup"><span data-stu-id="a3d40-134">To create a new Azure IoT Central application:</span></span>

    * <span data-ttu-id="a3d40-135">Choose a friendly application name, such as **Contoso Air Conditioners**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-135">Choose a friendly application name, such as **Contoso Air Conditioners**.</span></span> <span data-ttu-id="a3d40-136">Azure IoT Central generates a unique URL prefix for you.</span><span class="sxs-lookup"><span data-stu-id="a3d40-136">Azure IoT Central generates a unique URL prefix for you.</span></span> <span data-ttu-id="a3d40-137">You can change this URL prefix to something more memorable.</span><span class="sxs-lookup"><span data-stu-id="a3d40-137">You can change this URL prefix to something more memorable.</span></span>
    
    * <span data-ttu-id="a3d40-138">Choose an Azure Active Directory and Azure subscription to use.</span><span class="sxs-lookup"><span data-stu-id="a3d40-138">Choose an Azure Active Directory and Azure subscription to use.</span></span> <span data-ttu-id="a3d40-139">For more information about directories and subscriptions, see [Create an Azure IoT Central application](howto-create-application.md).</span><span class="sxs-lookup"><span data-stu-id="a3d40-139">For more information about directories and subscriptions, see [Create an Azure IoT Central application](howto-create-application.md).</span></span>
    
    * <span data-ttu-id="a3d40-140">Either use an existing resource group, or create a new resource group with a name of your choice.</span><span class="sxs-lookup"><span data-stu-id="a3d40-140">Either use an existing resource group, or create a new resource group with a name of your choice.</span></span> <span data-ttu-id="a3d40-141">For example, **contoso-rg**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-141">For example, **contoso-rg**.</span></span>
    
    * <span data-ttu-id="a3d40-142">Choose the region geographically closest to you.</span><span class="sxs-lookup"><span data-stu-id="a3d40-142">Choose the region geographically closest to you.</span></span>
    
    * <span data-ttu-id="a3d40-143">Choose the **Custom Application** application template.</span><span class="sxs-lookup"><span data-stu-id="a3d40-143">Choose the **Custom Application** application template.</span></span>
    
    * <span data-ttu-id="a3d40-144">Choose the **Free 30 Day Trial Application** payment plan.</span><span class="sxs-lookup"><span data-stu-id="a3d40-144">Choose the **Free 30 Day Trial Application** payment plan.</span></span>
    
    * <span data-ttu-id="a3d40-145">Choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-145">Choose **Create**.</span></span>

    ![Azure IoT Central Create Application page](./media/tutorial-define-device-type/iotcentralcreate.png)

<span data-ttu-id="a3d40-147">For more information, see [How to create an Azure IoT Central application](howto-create-application.md).</span><span class="sxs-lookup"><span data-stu-id="a3d40-147">For more information, see [How to create an Azure IoT Central application](howto-create-application.md).</span></span>

## <a name="create-a-new-custom-device-template"></a><span data-ttu-id="a3d40-148">Create a new custom device template</span><span class="sxs-lookup"><span data-stu-id="a3d40-148">Create a new custom device template</span></span>

<span data-ttu-id="a3d40-149">As a builder, you can create and edit the device templates in your application.</span><span class="sxs-lookup"><span data-stu-id="a3d40-149">As a builder, you can create and edit the device templates in your application.</span></span> <span data-ttu-id="a3d40-150">When you create a device template, Azure IoT Central generates a simulated device from the template.</span><span class="sxs-lookup"><span data-stu-id="a3d40-150">When you create a device template, Azure IoT Central generates a simulated device from the template.</span></span> <span data-ttu-id="a3d40-151">The simulated device generates telemetry that enables you to test the behavior of your application before you connect a physical device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-151">The simulated device generates telemetry that enables you to test the behavior of your application before you connect a physical device.</span></span>

<span data-ttu-id="a3d40-152">To add a new device template to your application, you need to go to the **Application Builder** page.</span><span class="sxs-lookup"><span data-stu-id="a3d40-152">To add a new device template to your application, you need to go to the **Application Builder** page.</span></span> <span data-ttu-id="a3d40-153">To do so choose the **Application builder** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="a3d40-153">To do so choose the **Application builder** on the left navigation menu.</span></span>

![Application Builder page](./media/tutorial-define-device-type/builderhome.png)

## <a name="add-a-device-and-define-telemetry"></a><span data-ttu-id="a3d40-155">Add a device and define telemetry</span><span class="sxs-lookup"><span data-stu-id="a3d40-155">Add a device and define telemetry</span></span>

<span data-ttu-id="a3d40-156">The following steps show you how to create a new **Connected Air Conditioner** device template for devices that send temperature telemetry to your application:</span><span class="sxs-lookup"><span data-stu-id="a3d40-156">The following steps show you how to create a new **Connected Air Conditioner** device template for devices that send temperature telemetry to your application:</span></span>

1. <span data-ttu-id="a3d40-157">On the **Application Builder** page, choose **Create Device Template**:</span><span class="sxs-lookup"><span data-stu-id="a3d40-157">On the **Application Builder** page, choose **Create Device Template**:</span></span>

    ![Application Builder page, Create Device Template](./media/tutorial-define-device-type/builderhomedevices.png)

2. <span data-ttu-id="a3d40-159">On the **Device Templates** page, choose **Custom**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-159">On the **Device Templates** page, choose **Custom**.</span></span> <span data-ttu-id="a3d40-160">A **Custom** device template enables you to define all the characteristics and behaviors of your connected air conditioner:</span><span class="sxs-lookup"><span data-stu-id="a3d40-160">A **Custom** device template enables you to define all the characteristics and behaviors of your connected air conditioner:</span></span>

    ![Devices](./media/tutorial-define-device-type/builderhomedevicescustom.png)

3. <span data-ttu-id="a3d40-162">On the **New Device Template** page, enter **Connected Air Conditioner** as the name of your device, and then choose **Create**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-162">On the **New Device Template** page, enter **Connected Air Conditioner** as the name of your device, and then choose **Create**.</span></span> <span data-ttu-id="a3d40-163">You can also upload an image of your device that's visible to operators in the device explorer:</span><span class="sxs-lookup"><span data-stu-id="a3d40-163">You can also upload an image of your device that's visible to operators in the device explorer:</span></span>

    ![Custom Device](./media/tutorial-define-device-type/createcustomdevice.png)

4. <span data-ttu-id="a3d40-165">In the **Connected Air Conditioner** device template, make sure you are on the **Measurements** page where you define the telemetry.</span><span class="sxs-lookup"><span data-stu-id="a3d40-165">In the **Connected Air Conditioner** device template, make sure you are on the **Measurements** page where you define the telemetry.</span></span> <span data-ttu-id="a3d40-166">Each device template you define has separate pages for you to:</span><span class="sxs-lookup"><span data-stu-id="a3d40-166">Each device template you define has separate pages for you to:</span></span>

    * <span data-ttu-id="a3d40-167">Specify the measurements, such as telemetry, event, and state, sent by the device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-167">Specify the measurements, such as telemetry, event, and state, sent by the device.</span></span>
    
    * <span data-ttu-id="a3d40-168">Define the settings used to control the device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-168">Define the settings used to control the device.</span></span>
    
    * <span data-ttu-id="a3d40-169">Define the properties used to record information about the device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-169">Define the properties used to record information about the device.</span></span>
    
    * <span data-ttu-id="a3d40-170">Define the rules associated with the device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-170">Define the rules associated with the device.</span></span>
    
    * <span data-ttu-id="a3d40-171">Customize the device dashboard for your operators.</span><span class="sxs-lookup"><span data-stu-id="a3d40-171">Customize the device dashboard for your operators.</span></span>

    ![Air conditioner measurements](./media/tutorial-define-device-type/airconmeasurements.png)

    > [!NOTE]
    > <span data-ttu-id="a3d40-173">To change the name of the device or device template, click on the text at the top of the page.</span><span class="sxs-lookup"><span data-stu-id="a3d40-173">To change the name of the device or device template, click on the text at the top of the page.</span></span>

5. <span data-ttu-id="a3d40-174">To add the temperature telemetry measurement, choose **New Measurement**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-174">To add the temperature telemetry measurement, choose **New Measurement**.</span></span> <span data-ttu-id="a3d40-175">Then choose **Telemetry** as the measurement type:</span><span class="sxs-lookup"><span data-stu-id="a3d40-175">Then choose **Telemetry** as the measurement type:</span></span>

    ![Connected air conditioner measurements](./media/tutorial-define-device-type/airconmeasurementsnew.png)

6. <span data-ttu-id="a3d40-177">Each type of telemetry you define for a device template includes [configuration options](howto-set-up-template.md) such as:</span><span class="sxs-lookup"><span data-stu-id="a3d40-177">Each type of telemetry you define for a device template includes [configuration options](howto-set-up-template.md) such as:</span></span>

    * <span data-ttu-id="a3d40-178">Display options.</span><span class="sxs-lookup"><span data-stu-id="a3d40-178">Display options.</span></span>

    * <span data-ttu-id="a3d40-179">Details of the telemetry.</span><span class="sxs-lookup"><span data-stu-id="a3d40-179">Details of the telemetry.</span></span>

    * <span data-ttu-id="a3d40-180">Simulation parameters.</span><span class="sxs-lookup"><span data-stu-id="a3d40-180">Simulation parameters.</span></span>

    <span data-ttu-id="a3d40-181">To configure your **Temperature** telemetry, use the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-181">To configure your **Temperature** telemetry, use the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-182">Setting</span><span class="sxs-lookup"><span data-stu-id="a3d40-182">Setting</span></span>              | <span data-ttu-id="a3d40-183">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-183">Value</span></span>         |
    | -------------------- | -----------   |
    | <span data-ttu-id="a3d40-184">Display Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-184">Display Name</span></span>         | <span data-ttu-id="a3d40-185">Temperature</span><span class="sxs-lookup"><span data-stu-id="a3d40-185">Temperature</span></span>   |
    | <span data-ttu-id="a3d40-186">Field Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-186">Field Name</span></span>           | <span data-ttu-id="a3d40-187">temperature</span><span class="sxs-lookup"><span data-stu-id="a3d40-187">temperature</span></span>   |
    | <span data-ttu-id="a3d40-188">Units</span><span class="sxs-lookup"><span data-stu-id="a3d40-188">Units</span></span>                | <span data-ttu-id="a3d40-189">F</span><span class="sxs-lookup"><span data-stu-id="a3d40-189">F</span></span>             |
    | <span data-ttu-id="a3d40-190">Min</span><span class="sxs-lookup"><span data-stu-id="a3d40-190">Min</span></span>                  | <span data-ttu-id="a3d40-191">60</span><span class="sxs-lookup"><span data-stu-id="a3d40-191">60</span></span>            |
    | <span data-ttu-id="a3d40-192">Max</span><span class="sxs-lookup"><span data-stu-id="a3d40-192">Max</span></span>                  | <span data-ttu-id="a3d40-193">110</span><span class="sxs-lookup"><span data-stu-id="a3d40-193">110</span></span>           |
    | <span data-ttu-id="a3d40-194">Decimal places</span><span class="sxs-lookup"><span data-stu-id="a3d40-194">Decimal places</span></span>       | <span data-ttu-id="a3d40-195">0</span><span class="sxs-lookup"><span data-stu-id="a3d40-195">0</span></span>             |

    <span data-ttu-id="a3d40-196">You can also choose a color for the telemetry display.</span><span class="sxs-lookup"><span data-stu-id="a3d40-196">You can also choose a color for the telemetry display.</span></span> <span data-ttu-id="a3d40-197">To save the telemetry definition, choose **Save**:</span><span class="sxs-lookup"><span data-stu-id="a3d40-197">To save the telemetry definition, choose **Save**:</span></span>

    ![Configure Temperature simulation](./media/tutorial-define-device-type/temperaturesimulation.png)

7. <span data-ttu-id="a3d40-199">After a short while, the **Measurements** page shows a chart of the temperature telemetry from your simulated connected air conditioner device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-199">After a short while, the **Measurements** page shows a chart of the temperature telemetry from your simulated connected air conditioner device.</span></span> <span data-ttu-id="a3d40-200">Use the controls to manage visibility, aggregation, or to edit the telemetry definition:</span><span class="sxs-lookup"><span data-stu-id="a3d40-200">Use the controls to manage visibility, aggregation, or to edit the telemetry definition:</span></span>

    ![View temperature simulation](./media/tutorial-define-device-type/viewsimulation.png)

8. <span data-ttu-id="a3d40-202">You can also customize the chart using the **Line**, **Stacked**, and **Edit Time Range** controls:</span><span class="sxs-lookup"><span data-stu-id="a3d40-202">You can also customize the chart using the **Line**, **Stacked**, and **Edit Time Range** controls:</span></span>

    ![Customize the chart](./media/tutorial-define-device-type/customizechart.png)

## <a name="define-event-measurement"></a><span data-ttu-id="a3d40-204">Define Event measurement</span><span class="sxs-lookup"><span data-stu-id="a3d40-204">Define Event measurement</span></span>

<span data-ttu-id="a3d40-205">You can use Event to define point-in-time data that is sent by the device to signify something of significance like an error or a component failure.</span><span class="sxs-lookup"><span data-stu-id="a3d40-205">You can use Event to define point-in-time data that is sent by the device to signify something of significance like an error or a component failure.</span></span> <span data-ttu-id="a3d40-206">Like telemetry measurements, Azure IoT Central can simulate device events to enable you to test the behavior of your application before you connect a physical device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-206">Like telemetry measurements, Azure IoT Central can simulate device events to enable you to test the behavior of your application before you connect a physical device.</span></span> <span data-ttu-id="a3d40-207">You define event measurements for your device type in the **Measurements** view.</span><span class="sxs-lookup"><span data-stu-id="a3d40-207">You define event measurements for your device type in the **Measurements** view.</span></span>

1. <span data-ttu-id="a3d40-208">To add the **Fan Motor Error** event measurement, choose **New Measurement**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-208">To add the **Fan Motor Error** event measurement, choose **New Measurement**.</span></span> <span data-ttu-id="a3d40-209">Then choose **Event** as the measurement type:</span><span class="sxs-lookup"><span data-stu-id="a3d40-209">Then choose **Event** as the measurement type:</span></span>

    ![Connected air conditioner measurements](./media/tutorial-define-device-type/eventnew.png)

2. <span data-ttu-id="a3d40-211">Each type of Event you define for a device template includes [configuration options](howto-set-up-template.md) such as:</span><span class="sxs-lookup"><span data-stu-id="a3d40-211">Each type of Event you define for a device template includes [configuration options](howto-set-up-template.md) such as:</span></span>

   * <span data-ttu-id="a3d40-212">Display Name.</span><span class="sxs-lookup"><span data-stu-id="a3d40-212">Display Name.</span></span>

   * <span data-ttu-id="a3d40-213">Field Name.</span><span class="sxs-lookup"><span data-stu-id="a3d40-213">Field Name.</span></span>

   * <span data-ttu-id="a3d40-214">Severity.</span><span class="sxs-lookup"><span data-stu-id="a3d40-214">Severity.</span></span>

    <span data-ttu-id="a3d40-215">To configure your **Fan Motor Error** event, use the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-215">To configure your **Fan Motor Error** event, use the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-216">Setting</span><span class="sxs-lookup"><span data-stu-id="a3d40-216">Setting</span></span>              | <span data-ttu-id="a3d40-217">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-217">Value</span></span>             |
    | -------------------- | -----------       |
    | <span data-ttu-id="a3d40-218">Display Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-218">Display Name</span></span>         | <span data-ttu-id="a3d40-219">Fan Motor Error</span><span class="sxs-lookup"><span data-stu-id="a3d40-219">Fan Motor Error</span></span>   |
    | <span data-ttu-id="a3d40-220">Field Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-220">Field Name</span></span>           | <span data-ttu-id="a3d40-221">fanmotorerr</span><span class="sxs-lookup"><span data-stu-id="a3d40-221">fanmotorerr</span></span>       |
    | <span data-ttu-id="a3d40-222">Severity</span><span class="sxs-lookup"><span data-stu-id="a3d40-222">Severity</span></span>             | <span data-ttu-id="a3d40-223">Error</span><span class="sxs-lookup"><span data-stu-id="a3d40-223">Error</span></span>             |

    <span data-ttu-id="a3d40-224">To save the event definition, choose **Save**:</span><span class="sxs-lookup"><span data-stu-id="a3d40-224">To save the event definition, choose **Save**:</span></span>

    ![Configure Event measurement](./media/tutorial-define-device-type/eventconfiguration.png)

3. <span data-ttu-id="a3d40-226">After a short while, the **Measurements** page shows a chart of the events randomly generated from your simulated connected air conditioner device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-226">After a short while, the **Measurements** page shows a chart of the events randomly generated from your simulated connected air conditioner device.</span></span> <span data-ttu-id="a3d40-227">Use the controls to manage visibility, or to edit the event definition:</span><span class="sxs-lookup"><span data-stu-id="a3d40-227">Use the controls to manage visibility, or to edit the event definition:</span></span>

    ![View event simulation](./media/tutorial-define-device-type/eventview.png)

1. <span data-ttu-id="a3d40-229">To see additional details about the event, click the event on the chart:</span><span class="sxs-lookup"><span data-stu-id="a3d40-229">To see additional details about the event, click the event on the chart:</span></span>

    ![View Event Details](./media/tutorial-define-device-type/eventviewdetail.png)

## <a name="define-state-measurement"></a><span data-ttu-id="a3d40-231">Define State measurement</span><span class="sxs-lookup"><span data-stu-id="a3d40-231">Define State measurement</span></span>

<span data-ttu-id="a3d40-232">You can use State to define and visualize the state of the device or its component over a period of time.</span><span class="sxs-lookup"><span data-stu-id="a3d40-232">You can use State to define and visualize the state of the device or its component over a period of time.</span></span> <span data-ttu-id="a3d40-233">Like telemetry measurements, Azure IoT Central can simulate device state to enable you to test the behavior of your application before you connect a physical device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-233">Like telemetry measurements, Azure IoT Central can simulate device state to enable you to test the behavior of your application before you connect a physical device.</span></span> <span data-ttu-id="a3d40-234">You define state measurements for your device type in the **Measurements** view.</span><span class="sxs-lookup"><span data-stu-id="a3d40-234">You define state measurements for your device type in the **Measurements** view.</span></span>

1. <span data-ttu-id="a3d40-235">To add **Fan Mode** measurement, choose **New Measurement**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-235">To add **Fan Mode** measurement, choose **New Measurement**.</span></span> <span data-ttu-id="a3d40-236">Then choose **State** as the measurement type:</span><span class="sxs-lookup"><span data-stu-id="a3d40-236">Then choose **State** as the measurement type:</span></span>

    ![Connected air conditioner state measurements](./media/tutorial-define-device-type/statenew.png)

2. <span data-ttu-id="a3d40-238">Each type of State you define for a device template includes [configuration options](howto-set-up-template.md) such as:</span><span class="sxs-lookup"><span data-stu-id="a3d40-238">Each type of State you define for a device template includes [configuration options](howto-set-up-template.md) such as:</span></span>

   * <span data-ttu-id="a3d40-239">Display Name.</span><span class="sxs-lookup"><span data-stu-id="a3d40-239">Display Name.</span></span>

   * <span data-ttu-id="a3d40-240">Field Name.</span><span class="sxs-lookup"><span data-stu-id="a3d40-240">Field Name.</span></span>

   * <span data-ttu-id="a3d40-241">Values with optional display labels.</span><span class="sxs-lookup"><span data-stu-id="a3d40-241">Values with optional display labels.</span></span>

   * <span data-ttu-id="a3d40-242">Color for each value.</span><span class="sxs-lookup"><span data-stu-id="a3d40-242">Color for each value.</span></span>

    <span data-ttu-id="a3d40-243">To configure your **Fan Mode** state, use the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-243">To configure your **Fan Mode** state, use the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-244">Setting</span><span class="sxs-lookup"><span data-stu-id="a3d40-244">Setting</span></span>              | <span data-ttu-id="a3d40-245">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-245">Value</span></span>             |
    | -------------------- | -----------       |
    | <span data-ttu-id="a3d40-246">Display Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-246">Display Name</span></span>         | <span data-ttu-id="a3d40-247">Fan Mode</span><span class="sxs-lookup"><span data-stu-id="a3d40-247">Fan Mode</span></span>          |
    | <span data-ttu-id="a3d40-248">Field Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-248">Field Name</span></span>           | <span data-ttu-id="a3d40-249">fanmode</span><span class="sxs-lookup"><span data-stu-id="a3d40-249">fanmode</span></span>           |
    | <span data-ttu-id="a3d40-250">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-250">Value</span></span>                | <span data-ttu-id="a3d40-251">1</span><span class="sxs-lookup"><span data-stu-id="a3d40-251">1</span></span>                 |
    | <span data-ttu-id="a3d40-252">Display label</span><span class="sxs-lookup"><span data-stu-id="a3d40-252">Display label</span></span>        | <span data-ttu-id="a3d40-253">Operating</span><span class="sxs-lookup"><span data-stu-id="a3d40-253">Operating</span></span>         |
    | <span data-ttu-id="a3d40-254">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-254">Value</span></span>                | <span data-ttu-id="a3d40-255">0</span><span class="sxs-lookup"><span data-stu-id="a3d40-255">0</span></span>                 |
    | <span data-ttu-id="a3d40-256">Display label</span><span class="sxs-lookup"><span data-stu-id="a3d40-256">Display label</span></span>        | <span data-ttu-id="a3d40-257">Stopped</span><span class="sxs-lookup"><span data-stu-id="a3d40-257">Stopped</span></span>           |

    <span data-ttu-id="a3d40-258">To save the state measurement definition, choose **Save**:</span><span class="sxs-lookup"><span data-stu-id="a3d40-258">To save the state measurement definition, choose **Save**:</span></span>

    ![Configure State measurement](./media/tutorial-define-device-type/stateconfiguration.png)

3. <span data-ttu-id="a3d40-260">After a short while, the **Measurements** page shows a chart of the states randomly generated from your simulated connected air conditioner device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-260">After a short while, the **Measurements** page shows a chart of the states randomly generated from your simulated connected air conditioner device.</span></span> <span data-ttu-id="a3d40-261">Use the controls to manage visibility, or to edit the state definition:</span><span class="sxs-lookup"><span data-stu-id="a3d40-261">Use the controls to manage visibility, or to edit the state definition:</span></span>

    ![View state simulation](./media/tutorial-define-device-type/stateview.png)

4. <span data-ttu-id="a3d40-263">In case, there are too many data points sent by the device within a small duration, the state measurement is shown with a different visual as shown below.</span><span class="sxs-lookup"><span data-stu-id="a3d40-263">In case, there are too many data points sent by the device within a small duration, the state measurement is shown with a different visual as shown below.</span></span> <span data-ttu-id="a3d40-264">If you click on the chart, then all the data points within that time period are displayed in a chronological order.</span><span class="sxs-lookup"><span data-stu-id="a3d40-264">If you click on the chart, then all the data points within that time period are displayed in a chronological order.</span></span> <span data-ttu-id="a3d40-265">You can also narrow down the time range so see the measurement plotted on the chart.</span><span class="sxs-lookup"><span data-stu-id="a3d40-265">You can also narrow down the time range so see the measurement plotted on the chart.</span></span>

    ![View state Details](./media/tutorial-define-device-type/stateviewdetail.png)

## <a name="settings-properties-and-commands"></a><span data-ttu-id="a3d40-267">Settings, properties, and commands</span><span class="sxs-lookup"><span data-stu-id="a3d40-267">Settings, properties, and commands</span></span>

<span data-ttu-id="a3d40-268">Settings, properties and device properties, and commands are different values defined in a device template and associated with each individual device:</span><span class="sxs-lookup"><span data-stu-id="a3d40-268">Settings, properties and device properties, and commands are different values defined in a device template and associated with each individual device:</span></span>

* <span data-ttu-id="a3d40-269">You use _settings_ to send configuration data to a device from your application.</span><span class="sxs-lookup"><span data-stu-id="a3d40-269">You use _settings_ to send configuration data to a device from your application.</span></span> <span data-ttu-id="a3d40-270">For example, an operator could use a setting to change the device's telemetry interval from two seconds to five seconds.</span><span class="sxs-lookup"><span data-stu-id="a3d40-270">For example, an operator could use a setting to change the device's telemetry interval from two seconds to five seconds.</span></span> <span data-ttu-id="a3d40-271">When an operator changes a setting, the setting is marked as pending in the UI until the device acknowledges that it has actioned the setting change.</span><span class="sxs-lookup"><span data-stu-id="a3d40-271">When an operator changes a setting, the setting is marked as pending in the UI until the device acknowledges that it has actioned the setting change.</span></span>

* <span data-ttu-id="a3d40-272">You use _properties_ to record information about your device in your application.</span><span class="sxs-lookup"><span data-stu-id="a3d40-272">You use _properties_ to record information about your device in your application.</span></span> <span data-ttu-id="a3d40-273">For example, you can use properties to record a device's serial number or the device manufacturer's phone number.</span><span class="sxs-lookup"><span data-stu-id="a3d40-273">For example, you can use properties to record a device's serial number or the device manufacturer's phone number.</span></span> <span data-ttu-id="a3d40-274">Properties are stored in the application and do not synchronize with the device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-274">Properties are stored in the application and do not synchronize with the device.</span></span> <span data-ttu-id="a3d40-275">An operator can assign values to properties.</span><span class="sxs-lookup"><span data-stu-id="a3d40-275">An operator can assign values to properties.</span></span>

* <span data-ttu-id="a3d40-276">You use _device properties_ to enable a device to send property values to your application.</span><span class="sxs-lookup"><span data-stu-id="a3d40-276">You use _device properties_ to enable a device to send property values to your application.</span></span> <span data-ttu-id="a3d40-277">These properties can only be changed by the device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-277">These properties can only be changed by the device.</span></span> <span data-ttu-id="a3d40-278">For an operator, device properties are read-only.</span><span class="sxs-lookup"><span data-stu-id="a3d40-278">For an operator, device properties are read-only.</span></span>

* <span data-ttu-id="a3d40-279">You use _commands_ to remotely manage your device from your application.</span><span class="sxs-lookup"><span data-stu-id="a3d40-279">You use _commands_ to remotely manage your device from your application.</span></span> <span data-ttu-id="a3d40-280">You can directly run commands on the device from the cloud to control the devices.</span><span class="sxs-lookup"><span data-stu-id="a3d40-280">You can directly run commands on the device from the cloud to control the devices.</span></span> <span data-ttu-id="a3d40-281">For example, an operator can run commands such as reboot, to instantly reboot the device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-281">For example, an operator can run commands such as reboot, to instantly reboot the device.</span></span>

## <a name="use-settings"></a><span data-ttu-id="a3d40-282">Use settings</span><span class="sxs-lookup"><span data-stu-id="a3d40-282">Use settings</span></span>

<span data-ttu-id="a3d40-283">You use *settings* to enable an operator to send configuration data to a device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-283">You use *settings* to enable an operator to send configuration data to a device.</span></span> <span data-ttu-id="a3d40-284">In this section, you add a setting to your **Connected Air Conditioner** device template that enables an operator to set the target temperature of the connected air conditioner.</span><span class="sxs-lookup"><span data-stu-id="a3d40-284">In this section, you add a setting to your **Connected Air Conditioner** device template that enables an operator to set the target temperature of the connected air conditioner.</span></span>

1. <span data-ttu-id="a3d40-285">Navigate to the **Settings** page for your **Connected Air Conditioner** device template:</span><span class="sxs-lookup"><span data-stu-id="a3d40-285">Navigate to the **Settings** page for your **Connected Air Conditioner** device template:</span></span>

    ![Prepare to add a setting](./media/tutorial-define-device-type/deviceaddsetting.png)

    <span data-ttu-id="a3d40-287">You can create settings of different types such as numbers or text.</span><span class="sxs-lookup"><span data-stu-id="a3d40-287">You can create settings of different types such as numbers or text.</span></span>

2. <span data-ttu-id="a3d40-288">Choose **Number** to add a number setting to your device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-288">Choose **Number** to add a number setting to your device.</span></span>

3. <span data-ttu-id="a3d40-289">To configure your **Set Temperature** setting, use the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-289">To configure your **Set Temperature** setting, use the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-290">Field</span><span class="sxs-lookup"><span data-stu-id="a3d40-290">Field</span></span>                | <span data-ttu-id="a3d40-291">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-291">Value</span></span>           |
    | -------------------- | -----------     |
    | <span data-ttu-id="a3d40-292">Display Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-292">Display Name</span></span>         | <span data-ttu-id="a3d40-293">Set Temperature</span><span class="sxs-lookup"><span data-stu-id="a3d40-293">Set Temperature</span></span> |
    | <span data-ttu-id="a3d40-294">Field Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-294">Field Name</span></span>           | <span data-ttu-id="a3d40-295">setTemperature</span><span class="sxs-lookup"><span data-stu-id="a3d40-295">setTemperature</span></span>  |
    | <span data-ttu-id="a3d40-296">Unit of measurement</span><span class="sxs-lookup"><span data-stu-id="a3d40-296">Unit of measurement</span></span>  | <span data-ttu-id="a3d40-297">F</span><span class="sxs-lookup"><span data-stu-id="a3d40-297">F</span></span>               |
    | <span data-ttu-id="a3d40-298">Decimal places</span><span class="sxs-lookup"><span data-stu-id="a3d40-298">Decimal places</span></span>       | <span data-ttu-id="a3d40-299">1</span><span class="sxs-lookup"><span data-stu-id="a3d40-299">1</span></span>               |
    | <span data-ttu-id="a3d40-300">Minimum value</span><span class="sxs-lookup"><span data-stu-id="a3d40-300">Minimum value</span></span>        | <span data-ttu-id="a3d40-301">20</span><span class="sxs-lookup"><span data-stu-id="a3d40-301">20</span></span>              |
    | <span data-ttu-id="a3d40-302">Maximum value</span><span class="sxs-lookup"><span data-stu-id="a3d40-302">Maximum value</span></span>        | <span data-ttu-id="a3d40-303">200</span><span class="sxs-lookup"><span data-stu-id="a3d40-303">200</span></span>             |
    | <span data-ttu-id="a3d40-304">Initial value</span><span class="sxs-lookup"><span data-stu-id="a3d40-304">Initial value</span></span>        | <span data-ttu-id="a3d40-305">80</span><span class="sxs-lookup"><span data-stu-id="a3d40-305">80</span></span>              |
    | <span data-ttu-id="a3d40-306">Description</span><span class="sxs-lookup"><span data-stu-id="a3d40-306">Description</span></span>          | <span data-ttu-id="a3d40-307">Set the target temperature for the air conditioner</span><span class="sxs-lookup"><span data-stu-id="a3d40-307">Set the target temperature for the air conditioner</span></span> |

    <span data-ttu-id="a3d40-308">Then choose **Save**:</span><span class="sxs-lookup"><span data-stu-id="a3d40-308">Then choose **Save**:</span></span>

    ![Configure Set Temperature setting](./media/tutorial-define-device-type/configuresetting.png)

    > [!NOTE]
    > <span data-ttu-id="a3d40-310">When the device acknowledges a setting change, the status of the setting changes to **synced**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-310">When the device acknowledges a setting change, the status of the setting changes to **synced**.</span></span>

4. <span data-ttu-id="a3d40-311">You can customize the layout of the **Settings** page by moving and resizing settings tiles:</span><span class="sxs-lookup"><span data-stu-id="a3d40-311">You can customize the layout of the **Settings** page by moving and resizing settings tiles:</span></span>

    ![Customize settings layout](./media/tutorial-define-device-type/settingslayout.png)

## <a name="use-properties--device-properties"></a><span data-ttu-id="a3d40-313">Use properties / device properties</span><span class="sxs-lookup"><span data-stu-id="a3d40-313">Use properties / device properties</span></span>

<span data-ttu-id="a3d40-314">You use *properties* to store information about your device in the application.</span><span class="sxs-lookup"><span data-stu-id="a3d40-314">You use *properties* to store information about your device in the application.</span></span> <span data-ttu-id="a3d40-315">In this section, you add cloud properties to your **Connected Air Conditioner** device template to store the location of the device and the last service date.</span><span class="sxs-lookup"><span data-stu-id="a3d40-315">In this section, you add cloud properties to your **Connected Air Conditioner** device template to store the location of the device and the last service date.</span></span> <span data-ttu-id="a3d40-316">Note that both of these are editable properties of the device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-316">Note that both of these are editable properties of the device.</span></span> <span data-ttu-id="a3d40-317">There are also read-only properties reported by the device that cannot be changed such as the device serial number and firmware version.</span><span class="sxs-lookup"><span data-stu-id="a3d40-317">There are also read-only properties reported by the device that cannot be changed such as the device serial number and firmware version.</span></span>
 
1. <span data-ttu-id="a3d40-318">Navigate to the **Properties** page for your **Connected Air Conditioner** device template:</span><span class="sxs-lookup"><span data-stu-id="a3d40-318">Navigate to the **Properties** page for your **Connected Air Conditioner** device template:</span></span>

    ![Prepare to add a property](./media/tutorial-define-device-type/deviceaddproperty.png)

    <span data-ttu-id="a3d40-320">You can create device properties of different types such as numbers or text.</span><span class="sxs-lookup"><span data-stu-id="a3d40-320">You can create device properties of different types such as numbers or text.</span></span> <span data-ttu-id="a3d40-321">To add a location property to your device template, choose **Location**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-321">To add a location property to your device template, choose **Location**.</span></span>

2. <span data-ttu-id="a3d40-322">To configure your location property, use the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-322">To configure your location property, use the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-323">Field</span><span class="sxs-lookup"><span data-stu-id="a3d40-323">Field</span></span>                | <span data-ttu-id="a3d40-324">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-324">Value</span></span>                |
    | -------------------- | -------------------- |
    | <span data-ttu-id="a3d40-325">Display Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-325">Display Name</span></span>         | <span data-ttu-id="a3d40-326">Location</span><span class="sxs-lookup"><span data-stu-id="a3d40-326">Location</span></span>             |
    | <span data-ttu-id="a3d40-327">Field Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-327">Field Name</span></span>           | <span data-ttu-id="a3d40-328">location</span><span class="sxs-lookup"><span data-stu-id="a3d40-328">location</span></span>             |
    | <span data-ttu-id="a3d40-329">Initial Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-329">Initial Value</span></span>        | <span data-ttu-id="a3d40-330">Seattle, WA</span><span class="sxs-lookup"><span data-stu-id="a3d40-330">Seattle, WA</span></span>          |
    | <span data-ttu-id="a3d40-331">Description</span><span class="sxs-lookup"><span data-stu-id="a3d40-331">Description</span></span>          | <span data-ttu-id="a3d40-332">Device location</span><span class="sxs-lookup"><span data-stu-id="a3d40-332">Device location</span></span>      |

    <span data-ttu-id="a3d40-333">Leave other fields with their default values.</span><span class="sxs-lookup"><span data-stu-id="a3d40-333">Leave other fields with their default values.</span></span>

    ![Configure the device properties](./media/tutorial-define-device-type/configureproperties.png)

    <span data-ttu-id="a3d40-335">Choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-335">Choose **Save**.</span></span>

3. <span data-ttu-id="a3d40-336">To add a last service date property to your device template, choose **Date**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-336">To add a last service date property to your device template, choose **Date**.</span></span>

4. <span data-ttu-id="a3d40-337">To configure your last service date property, use the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-337">To configure your last service date property, use the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-338">Field</span><span class="sxs-lookup"><span data-stu-id="a3d40-338">Field</span></span>                | <span data-ttu-id="a3d40-339">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-339">Value</span></span>                   |
    | -------------------- | ----------------------- |
    | <span data-ttu-id="a3d40-340">Display Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-340">Display Name</span></span>         | <span data-ttu-id="a3d40-341">Last Service Date</span><span class="sxs-lookup"><span data-stu-id="a3d40-341">Last Service Date</span></span>       |
    | <span data-ttu-id="a3d40-342">Field Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-342">Field Name</span></span>           | <span data-ttu-id="a3d40-343">serviceDate</span><span class="sxs-lookup"><span data-stu-id="a3d40-343">serviceDate</span></span>             |
    | <span data-ttu-id="a3d40-344">Initial Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-344">Initial Value</span></span>        | <span data-ttu-id="a3d40-345">1/1/2018</span><span class="sxs-lookup"><span data-stu-id="a3d40-345">1/1/2018</span></span>                |
    | <span data-ttu-id="a3d40-346">Description</span><span class="sxs-lookup"><span data-stu-id="a3d40-346">Description</span></span>          | <span data-ttu-id="a3d40-347">Last serviced</span><span class="sxs-lookup"><span data-stu-id="a3d40-347">Last serviced</span></span>           |

    ![Configure the device properties](./media/tutorial-define-device-type/configureproperties2.png)

    <span data-ttu-id="a3d40-349">Choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-349">Choose **Save**.</span></span>

5. <span data-ttu-id="a3d40-350">You can customize the layout of the **Properties** page by moving and resizing property tiles:</span><span class="sxs-lookup"><span data-stu-id="a3d40-350">You can customize the layout of the **Properties** page by moving and resizing property tiles:</span></span>

    ![Customize properties layout](./media/tutorial-define-device-type/propertieslayout.png)


## <a name="use-commands"></a><span data-ttu-id="a3d40-352">Use commands</span><span class="sxs-lookup"><span data-stu-id="a3d40-352">Use commands</span></span>

<span data-ttu-id="a3d40-353">You use _commands_ to enable an operator to run commands directly on the device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-353">You use _commands_ to enable an operator to run commands directly on the device.</span></span> <span data-ttu-id="a3d40-354">In this section, you add a command to your **Connected Air Conditioner** device template that enables an operator to echo a certain message on the connected air conditioner display (this works with MxChip sample code).</span><span class="sxs-lookup"><span data-stu-id="a3d40-354">In this section, you add a command to your **Connected Air Conditioner** device template that enables an operator to echo a certain message on the connected air conditioner display (this works with MxChip sample code).</span></span>

1. <span data-ttu-id="a3d40-355">Navigate to the **Commands** page for your **Connected Air Conditioner** device template:</span><span class="sxs-lookup"><span data-stu-id="a3d40-355">Navigate to the **Commands** page for your **Connected Air Conditioner** device template:</span></span>

    ![Prepare to add a setting](media/tutorial-define-device-type/commandsecho.png)

    <span data-ttu-id="a3d40-357">You can create commands of different types based on your requirements.</span><span class="sxs-lookup"><span data-stu-id="a3d40-357">You can create commands of different types based on your requirements.</span></span> 

1. <span data-ttu-id="a3d40-358">Click **New Command** to add a command to your device.</span><span class="sxs-lookup"><span data-stu-id="a3d40-358">Click **New Command** to add a command to your device.</span></span>

1. <span data-ttu-id="a3d40-359">To configure your new command, use the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-359">To configure your new command, use the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-360">Field</span><span class="sxs-lookup"><span data-stu-id="a3d40-360">Field</span></span>                | <span data-ttu-id="a3d40-361">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-361">Value</span></span>           |
    | -------------------- | -----------     |
    | <span data-ttu-id="a3d40-362">Display Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-362">Display Name</span></span>         | <span data-ttu-id="a3d40-363">Echo Command</span><span class="sxs-lookup"><span data-stu-id="a3d40-363">Echo Command</span></span>    |
    | <span data-ttu-id="a3d40-364">Field Name</span><span class="sxs-lookup"><span data-stu-id="a3d40-364">Field Name</span></span>           | <span data-ttu-id="a3d40-365">echo</span><span class="sxs-lookup"><span data-stu-id="a3d40-365">echo</span></span>            |
    | <span data-ttu-id="a3d40-366">Default Timeout</span><span class="sxs-lookup"><span data-stu-id="a3d40-366">Default Timeout</span></span>      | <span data-ttu-id="a3d40-367">30</span><span class="sxs-lookup"><span data-stu-id="a3d40-367">30</span></span>              |
    | <span data-ttu-id="a3d40-368">Display Type</span><span class="sxs-lookup"><span data-stu-id="a3d40-368">Display Type</span></span>         | <span data-ttu-id="a3d40-369">text</span><span class="sxs-lookup"><span data-stu-id="a3d40-369">text</span></span>            |
    | <span data-ttu-id="a3d40-370">Description</span><span class="sxs-lookup"><span data-stu-id="a3d40-370">Description</span></span>          | <span data-ttu-id="a3d40-371">Device Command</span><span class="sxs-lookup"><span data-stu-id="a3d40-371">Device Command</span></span>  |  

<span data-ttu-id="a3d40-372">You can add additional inputs to the command by clicking **+** for inputs.</span><span class="sxs-lookup"><span data-stu-id="a3d40-372">You can add additional inputs to the command by clicking **+** for inputs.</span></span>

2. <span data-ttu-id="a3d40-373">Choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-373">Choose **Save**.</span></span>

3. <span data-ttu-id="a3d40-374">You can customize the layout of the **Commands** page by moving and resizing commands tiles:</span><span class="sxs-lookup"><span data-stu-id="a3d40-374">You can customize the layout of the **Commands** page by moving and resizing commands tiles:</span></span>

    ![Customize settings layout](media/tutorial-define-device-type/commandstileresize.png)

## <a name="view-your-simulated-device"></a><span data-ttu-id="a3d40-376">View your simulated device</span><span class="sxs-lookup"><span data-stu-id="a3d40-376">View your simulated device</span></span>

<span data-ttu-id="a3d40-377">Now you have defined your **Connected Air Conditioner** device template, you can customize its **Dashboard** to include the measurements, settings, and properties you defined.</span><span class="sxs-lookup"><span data-stu-id="a3d40-377">Now you have defined your **Connected Air Conditioner** device template, you can customize its **Dashboard** to include the measurements, settings, and properties you defined.</span></span> <span data-ttu-id="a3d40-378">Then you can preview the dashboard as an operator:</span><span class="sxs-lookup"><span data-stu-id="a3d40-378">Then you can preview the dashboard as an operator:</span></span>

1. <span data-ttu-id="a3d40-379">Choose the **Dashboard** page for your **Connected Air Conditioner** device template:</span><span class="sxs-lookup"><span data-stu-id="a3d40-379">Choose the **Dashboard** page for your **Connected Air Conditioner** device template:</span></span>

    ![Connected air conditioner dashboards](./media/tutorial-define-device-type/aircondashboards.png)

2. <span data-ttu-id="a3d40-381">Choose **Line Chart** to add the component onto the **Dashboard**:</span><span class="sxs-lookup"><span data-stu-id="a3d40-381">Choose **Line Chart** to add the component onto the **Dashboard**:</span></span>

    ![Dashboard components](./media/tutorial-define-device-type/dashboardcomponents1.png)

3. <span data-ttu-id="a3d40-383">Configure the **Line Chart** component using the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-383">Configure the **Line Chart** component using the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-384">Setting</span><span class="sxs-lookup"><span data-stu-id="a3d40-384">Setting</span></span>      | <span data-ttu-id="a3d40-385">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-385">Value</span></span>       |
    | ------------ | ----------- |
    | <span data-ttu-id="a3d40-386">Title</span><span class="sxs-lookup"><span data-stu-id="a3d40-386">Title</span></span>        | <span data-ttu-id="a3d40-387">Temperature</span><span class="sxs-lookup"><span data-stu-id="a3d40-387">Temperature</span></span> |
    | <span data-ttu-id="a3d40-388">Time Range</span><span class="sxs-lookup"><span data-stu-id="a3d40-388">Time Range</span></span>   | <span data-ttu-id="a3d40-389">Past 30 minutes</span><span class="sxs-lookup"><span data-stu-id="a3d40-389">Past 30 minutes</span></span> |
    | <span data-ttu-id="a3d40-390">Measurements</span><span class="sxs-lookup"><span data-stu-id="a3d40-390">Measurements</span></span> | <span data-ttu-id="a3d40-391">temperature (choose **Visibility** next to **temperature**)</span><span class="sxs-lookup"><span data-stu-id="a3d40-391">temperature (choose **Visibility** next to **temperature**)</span></span> |

    ![Line chart settings](./media/tutorial-define-device-type/linechartsettings.png)

    <span data-ttu-id="a3d40-393">Then choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-393">Then choose **Save**.</span></span>

4. <span data-ttu-id="a3d40-394">Configure the **Event Chart** component using the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-394">Configure the **Event Chart** component using the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-395">Setting</span><span class="sxs-lookup"><span data-stu-id="a3d40-395">Setting</span></span>      | <span data-ttu-id="a3d40-396">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-396">Value</span></span>       |
    | ------------ | ----------- |
    | <span data-ttu-id="a3d40-397">Title</span><span class="sxs-lookup"><span data-stu-id="a3d40-397">Title</span></span>        | <span data-ttu-id="a3d40-398">Events</span><span class="sxs-lookup"><span data-stu-id="a3d40-398">Events</span></span> |
    | <span data-ttu-id="a3d40-399">Time Range</span><span class="sxs-lookup"><span data-stu-id="a3d40-399">Time Range</span></span>   | <span data-ttu-id="a3d40-400">Past 30 minutes</span><span class="sxs-lookup"><span data-stu-id="a3d40-400">Past 30 minutes</span></span> |
    | <span data-ttu-id="a3d40-401">Measurements</span><span class="sxs-lookup"><span data-stu-id="a3d40-401">Measurements</span></span> | <span data-ttu-id="a3d40-402">Fan Motor Error (choose **Visibility** next to **Fan Motor Error**)</span><span class="sxs-lookup"><span data-stu-id="a3d40-402">Fan Motor Error (choose **Visibility** next to **Fan Motor Error**)</span></span> |

    ![Line chart settings](./media/tutorial-define-device-type/dashboardeventchartsetting.png)

    <span data-ttu-id="a3d40-404">Then choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-404">Then choose **Save**.</span></span>

5. <span data-ttu-id="a3d40-405">Configure the **State Chart** component using the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-405">Configure the **State Chart** component using the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-406">Setting</span><span class="sxs-lookup"><span data-stu-id="a3d40-406">Setting</span></span>      | <span data-ttu-id="a3d40-407">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-407">Value</span></span>       |
    | ------------ | ----------- |
    | <span data-ttu-id="a3d40-408">Title</span><span class="sxs-lookup"><span data-stu-id="a3d40-408">Title</span></span>        | <span data-ttu-id="a3d40-409">Fan Mode</span><span class="sxs-lookup"><span data-stu-id="a3d40-409">Fan Mode</span></span> |
    | <span data-ttu-id="a3d40-410">Time Range</span><span class="sxs-lookup"><span data-stu-id="a3d40-410">Time Range</span></span>   | <span data-ttu-id="a3d40-411">Past 30 minutes</span><span class="sxs-lookup"><span data-stu-id="a3d40-411">Past 30 minutes</span></span> |
    | <span data-ttu-id="a3d40-412">Measurements</span><span class="sxs-lookup"><span data-stu-id="a3d40-412">Measurements</span></span> | <span data-ttu-id="a3d40-413">Fan Mode (choose **Visibility** next to **Fan Mode**)</span><span class="sxs-lookup"><span data-stu-id="a3d40-413">Fan Mode (choose **Visibility** next to **Fan Mode**)</span></span> |

    ![Line chart settings](./media/tutorial-define-device-type/dashboardstatechartsetting.png)

    <span data-ttu-id="a3d40-415">Then choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-415">Then choose **Save**.</span></span>

6. <span data-ttu-id="a3d40-416">To add the set temperature setting to the dashboard, choose **Settings and Properties**:</span><span class="sxs-lookup"><span data-stu-id="a3d40-416">To add the set temperature setting to the dashboard, choose **Settings and Properties**:</span></span>

    ![Dashboard components](./media/tutorial-define-device-type/dashboardcomponents4.png)

7. <span data-ttu-id="a3d40-418">Configure the **Settings and Properties** component using the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-418">Configure the **Settings and Properties** component using the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-419">Setting</span><span class="sxs-lookup"><span data-stu-id="a3d40-419">Setting</span></span>                 | <span data-ttu-id="a3d40-420">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-420">Value</span></span>         |
    | ----------------------- | ------------- |
    | <span data-ttu-id="a3d40-421">Title</span><span class="sxs-lookup"><span data-stu-id="a3d40-421">Title</span></span>                   | <span data-ttu-id="a3d40-422">Set target temperature</span><span class="sxs-lookup"><span data-stu-id="a3d40-422">Set target temperature</span></span> |
    | <span data-ttu-id="a3d40-423">Settings and Properties</span><span class="sxs-lookup"><span data-stu-id="a3d40-423">Settings and Properties</span></span> | <span data-ttu-id="a3d40-424">Set Temperature</span><span class="sxs-lookup"><span data-stu-id="a3d40-424">Set Temperature</span></span> |

    ![Serial number property settings](./media/tutorial-define-device-type/propertysettings3.png)

    <span data-ttu-id="a3d40-426">Then choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-426">Then choose **Save**.</span></span>

8. <span data-ttu-id="a3d40-427">To add to the device serial number to the dashboard, choose **Settings and Properties**:</span><span class="sxs-lookup"><span data-stu-id="a3d40-427">To add to the device serial number to the dashboard, choose **Settings and Properties**:</span></span>

    ![Dashboard components](./media/tutorial-define-device-type/dashboardcomponents3.png)

9. <span data-ttu-id="a3d40-429">Configure the **Settings and Properties** component using the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-429">Configure the **Settings and Properties** component using the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-430">Setting</span><span class="sxs-lookup"><span data-stu-id="a3d40-430">Setting</span></span>                 | <span data-ttu-id="a3d40-431">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-431">Value</span></span>         |
    | ----------------------- | ------------- |
    | <span data-ttu-id="a3d40-432">Title</span><span class="sxs-lookup"><span data-stu-id="a3d40-432">Title</span></span>                   | <span data-ttu-id="a3d40-433">Serial number</span><span class="sxs-lookup"><span data-stu-id="a3d40-433">Serial number</span></span> |
    | <span data-ttu-id="a3d40-434">Settings and Properties</span><span class="sxs-lookup"><span data-stu-id="a3d40-434">Settings and Properties</span></span> | <span data-ttu-id="a3d40-435">Serial Number</span><span class="sxs-lookup"><span data-stu-id="a3d40-435">Serial Number</span></span> |

    ![Serial number property settings](./media/tutorial-define-device-type/propertysettings1.png)

    <span data-ttu-id="a3d40-437">Then choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-437">Then choose **Save**.</span></span>

10. <span data-ttu-id="a3d40-438">To add to the device firmware version to the dashboard, choose **Settings and Properties**:</span><span class="sxs-lookup"><span data-stu-id="a3d40-438">To add to the device firmware version to the dashboard, choose **Settings and Properties**:</span></span>

    ![Dashboard components](./media/tutorial-define-device-type/dashboardcomponents4.png)

11. <span data-ttu-id="a3d40-440">Configure the **Settings and Properties** component using the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="a3d40-440">Configure the **Settings and Properties** component using the information in the following table:</span></span>

    | <span data-ttu-id="a3d40-441">Setting</span><span class="sxs-lookup"><span data-stu-id="a3d40-441">Setting</span></span>                 | <span data-ttu-id="a3d40-442">Value</span><span class="sxs-lookup"><span data-stu-id="a3d40-442">Value</span></span>            |
    | ----------------------- | ---------------- |
    | <span data-ttu-id="a3d40-443">Title</span><span class="sxs-lookup"><span data-stu-id="a3d40-443">Title</span></span>                   | <span data-ttu-id="a3d40-444">Firmware version</span><span class="sxs-lookup"><span data-stu-id="a3d40-444">Firmware version</span></span> |
    | <span data-ttu-id="a3d40-445">Settings and Properties</span><span class="sxs-lookup"><span data-stu-id="a3d40-445">Settings and Properties</span></span> | <span data-ttu-id="a3d40-446">Firmware Version</span><span class="sxs-lookup"><span data-stu-id="a3d40-446">Firmware Version</span></span> |

    ![Serial number property settings](./media/tutorial-define-device-type/propertysettings2.png)

    <span data-ttu-id="a3d40-448">Then choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="a3d40-448">Then choose **Save**.</span></span>

12. <span data-ttu-id="a3d40-449">To view the dashboard as an operator, switch off **Design Mode** on the top right of the page.</span><span class="sxs-lookup"><span data-stu-id="a3d40-449">To view the dashboard as an operator, switch off **Design Mode** on the top right of the page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a3d40-450">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3d40-450">Next steps</span></span>

<span data-ttu-id="a3d40-451">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="a3d40-451">In this tutorial, you learned how to:</span></span>

<!-- Repeat task list from intro -->
> [!div class="nextstepaction"]
> * <span data-ttu-id="a3d40-452">Create a new device template</span><span class="sxs-lookup"><span data-stu-id="a3d40-452">Create a new device template</span></span>
> * <span data-ttu-id="a3d40-453">Add telemetry to your device</span><span class="sxs-lookup"><span data-stu-id="a3d40-453">Add telemetry to your device</span></span>
> * <span data-ttu-id="a3d40-454">View simulated telemetry</span><span class="sxs-lookup"><span data-stu-id="a3d40-454">View simulated telemetry</span></span>
> * <span data-ttu-id="a3d40-455">Define device events</span><span class="sxs-lookup"><span data-stu-id="a3d40-455">Define device events</span></span>
> * <span data-ttu-id="a3d40-456">View simulated events</span><span class="sxs-lookup"><span data-stu-id="a3d40-456">View simulated events</span></span>
> * <span data-ttu-id="a3d40-457">Define your state</span><span class="sxs-lookup"><span data-stu-id="a3d40-457">Define your state</span></span>
> * <span data-ttu-id="a3d40-458">View simulated state</span><span class="sxs-lookup"><span data-stu-id="a3d40-458">View simulated state</span></span>
> * <span data-ttu-id="a3d40-459">Use device properties</span><span class="sxs-lookup"><span data-stu-id="a3d40-459">Use device properties</span></span>
> * <span data-ttu-id="a3d40-460">Use device settings</span><span class="sxs-lookup"><span data-stu-id="a3d40-460">Use device settings</span></span>

<span data-ttu-id="a3d40-461">Now that you have defined a device template in your Azure IoT Central application, here are the suggested next steps:</span><span class="sxs-lookup"><span data-stu-id="a3d40-461">Now that you have defined a device template in your Azure IoT Central application, here are the suggested next steps:</span></span>

* [<span data-ttu-id="a3d40-462">Configure rules and actions for your device</span><span class="sxs-lookup"><span data-stu-id="a3d40-462">Configure rules and actions for your device</span></span>](tutorial-configure-rules.md)
* [<span data-ttu-id="a3d40-463">Customize the operator's views</span><span class="sxs-lookup"><span data-stu-id="a3d40-463">Customize the operator's views</span></span>](tutorial-customize-operator.md)
