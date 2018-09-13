---
title: Customize the operator's views in Azure IoT Central | Microsoft Docs
description: As a builder, customize the operator's views in your Azure IoT Central application.
author: sandeeppujar
ms.author: sandeepu
ms.date: 04/16/2018
ms.topic: tutorial
ms.service: iot-central
services: iot-central
ms.custom: mvc
ms.openlocfilehash: 3be35214390eca428efcd3a693dce286b4ba64f2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968890"
---
# <a name="tutorial-customize-the-azure-iot-central-operators-view"></a><span data-ttu-id="d6986-103">Tutorial: Customize the Azure IoT Central operator's view</span><span class="sxs-lookup"><span data-stu-id="d6986-103">Tutorial: Customize the Azure IoT Central operator's view</span></span>

<span data-ttu-id="d6986-104">This tutorial shows you, as a builder, how to customize the operator's view of your application.</span><span class="sxs-lookup"><span data-stu-id="d6986-104">This tutorial shows you, as a builder, how to customize the operator's view of your application.</span></span> <span data-ttu-id="d6986-105">When you make a change to the application as a builder, you can preview the operator's view in the Microsoft Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="d6986-105">When you make a change to the application as a builder, you can preview the operator's view in the Microsoft Azure IoT Central application.</span></span>

<span data-ttu-id="d6986-106">In this tutorial, you customize the application to display relevant information about the connected air conditioner device to an operator.</span><span class="sxs-lookup"><span data-stu-id="d6986-106">In this tutorial, you customize the application to display relevant information about the connected air conditioner device to an operator.</span></span> <span data-ttu-id="d6986-107">Your customizations enable the operator to manage the air conditioner devices connected to the application.</span><span class="sxs-lookup"><span data-stu-id="d6986-107">Your customizations enable the operator to manage the air conditioner devices connected to the application.</span></span>

<span data-ttu-id="d6986-108">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="d6986-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d6986-109">Configure your device dashboard</span><span class="sxs-lookup"><span data-stu-id="d6986-109">Configure your device dashboard</span></span>
> * <span data-ttu-id="d6986-110">Configure your device settings layout</span><span class="sxs-lookup"><span data-stu-id="d6986-110">Configure your device settings layout</span></span>
> * <span data-ttu-id="d6986-111">Configure your device properties layout</span><span class="sxs-lookup"><span data-stu-id="d6986-111">Configure your device properties layout</span></span>
> * <span data-ttu-id="d6986-112">Preview the device as an operator</span><span class="sxs-lookup"><span data-stu-id="d6986-112">Preview the device as an operator</span></span>
> * <span data-ttu-id="d6986-113">Configure your default home page</span><span class="sxs-lookup"><span data-stu-id="d6986-113">Configure your default home page</span></span>
> * <span data-ttu-id="d6986-114">Preview the default home page as an operator</span><span class="sxs-lookup"><span data-stu-id="d6986-114">Preview the default home page as an operator</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6986-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d6986-115">Prerequisites</span></span>

<span data-ttu-id="d6986-116">Before you begin, you should complete the two previous tutorials:</span><span class="sxs-lookup"><span data-stu-id="d6986-116">Before you begin, you should complete the two previous tutorials:</span></span>

* <span data-ttu-id="d6986-117">[Define a new device type in your Azure IoT Central application](tutorial-define-device-type.md).</span><span class="sxs-lookup"><span data-stu-id="d6986-117">[Define a new device type in your Azure IoT Central application](tutorial-define-device-type.md).</span></span>
* <span data-ttu-id="d6986-118">[Configure rules and actions for your device](tutorial-configure-rules.md).</span><span class="sxs-lookup"><span data-stu-id="d6986-118">[Configure rules and actions for your device](tutorial-configure-rules.md).</span></span>

## <a name="configure-your-device-dashboard"></a><span data-ttu-id="d6986-119">Configure your device dashboard</span><span class="sxs-lookup"><span data-stu-id="d6986-119">Configure your device dashboard</span></span>

<span data-ttu-id="d6986-120">As a builder, you can define what information displays on a device dashboard.</span><span class="sxs-lookup"><span data-stu-id="d6986-120">As a builder, you can define what information displays on a device dashboard.</span></span> <span data-ttu-id="d6986-121">In the [Define a new device type in your application](tutorial-define-device-type.md) tutorial, you added a line-chart and other information to the **Connected Air Conditioner-1** dashboard.</span><span class="sxs-lookup"><span data-stu-id="d6986-121">In the [Define a new device type in your application](tutorial-define-device-type.md) tutorial, you added a line-chart and other information to the **Connected Air Conditioner-1** dashboard.</span></span>

1. <span data-ttu-id="d6986-122">To edit the **Connected Air Conditioner** device template, choose **Explorer** on the left navigation menu:</span><span class="sxs-lookup"><span data-stu-id="d6986-122">To edit the **Connected Air Conditioner** device template, choose **Explorer** on the left navigation menu:</span></span>

    ![Explorer page](media/tutorial-customize-operator/explorer.png)

2. <span data-ttu-id="d6986-124">To start customizing your connected air conditioner device dashboard, select the **Connected Air Conditioner (1.0.0)** device template.</span><span class="sxs-lookup"><span data-stu-id="d6986-124">To start customizing your connected air conditioner device dashboard, select the **Connected Air Conditioner (1.0.0)** device template.</span></span> <span data-ttu-id="d6986-125">Choose the **Connected Air Conditioner-1** device you created in the [Define a new device type in your application](tutorial-define-device-type.md) tutorial:</span><span class="sxs-lookup"><span data-stu-id="d6986-125">Choose the **Connected Air Conditioner-1** device you created in the [Define a new device type in your application](tutorial-define-device-type.md) tutorial:</span></span>

    ![Select the connected air conditioner device](media/tutorial-customize-operator/selectdevice.png)

    <span data-ttu-id="d6986-127">When inside a device, such as **Connected Air Conditioner-1**, you can select **Edit Template** to make a change to the underlying template.</span><span class="sxs-lookup"><span data-stu-id="d6986-127">When inside a device, such as **Connected Air Conditioner-1**, you can select **Edit Template** to make a change to the underlying template.</span></span> <span data-ttu-id="d6986-128">For more information, see [Create a new device template version](howto-version-devicetemplate.md).</span><span class="sxs-lookup"><span data-stu-id="d6986-128">For more information, see [Create a new device template version](howto-version-devicetemplate.md).</span></span>

3. <span data-ttu-id="d6986-129">To edit the dashboard, choose **Dashboard**, and select **Edit      Template**:</span><span class="sxs-lookup"><span data-stu-id="d6986-129">To edit the dashboard, choose **Dashboard**, and select **Edit      Template**:</span></span>

    ![Device template dashboard page](media/tutorial-customize-operator/dashboard.png)

4. <span data-ttu-id="d6986-131">To add a KPI tile to the dashboard, choose **KPI**:</span><span class="sxs-lookup"><span data-stu-id="d6986-131">To add a KPI tile to the dashboard, choose **KPI**:</span></span>

    ![Add KPI](media/tutorial-customize-operator/addkpi.png)

    <span data-ttu-id="d6986-133">To define the KPI, use the information in the following table:</span><span class="sxs-lookup"><span data-stu-id="d6986-133">To define the KPI, use the information in the following table:</span></span>

    | <span data-ttu-id="d6986-134">Setting</span><span class="sxs-lookup"><span data-stu-id="d6986-134">Setting</span></span>     | <span data-ttu-id="d6986-135">Value</span><span class="sxs-lookup"><span data-stu-id="d6986-135">Value</span></span> |
    | ----------- | ----- |
    | <span data-ttu-id="d6986-136">Name</span><span class="sxs-lookup"><span data-stu-id="d6986-136">Name</span></span>        | <span data-ttu-id="d6986-137">Maximum temperature</span><span class="sxs-lookup"><span data-stu-id="d6986-137">Maximum temperature</span></span> |
    | <span data-ttu-id="d6986-138">Measurement</span><span class="sxs-lookup"><span data-stu-id="d6986-138">Measurement</span></span> | <span data-ttu-id="d6986-139">temperature</span><span class="sxs-lookup"><span data-stu-id="d6986-139">temperature</span></span> |
    | <span data-ttu-id="d6986-140">Aggregation</span><span class="sxs-lookup"><span data-stu-id="d6986-140">Aggregation</span></span> | <span data-ttu-id="d6986-141">Maximum</span><span class="sxs-lookup"><span data-stu-id="d6986-141">Maximum</span></span> |
    | <span data-ttu-id="d6986-142">Time range</span><span class="sxs-lookup"><span data-stu-id="d6986-142">Time range</span></span>  | <span data-ttu-id="d6986-143">Past 1 week</span><span class="sxs-lookup"><span data-stu-id="d6986-143">Past 1 week</span></span> |

5. <span data-ttu-id="d6986-144">Choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="d6986-144">Choose **Save**.</span></span> <span data-ttu-id="d6986-145">You can now see the KPI tile on the dashboard:</span><span class="sxs-lookup"><span data-stu-id="d6986-145">You can now see the KPI tile on the dashboard:</span></span>

    ![KPI tile](media/tutorial-customize-operator/temperaturekpi.png)

6. <span data-ttu-id="d6986-147">To move or resize a tile on the dashboard, move the mouse pointer over the tile.</span><span class="sxs-lookup"><span data-stu-id="d6986-147">To move or resize a tile on the dashboard, move the mouse pointer over the tile.</span></span> <span data-ttu-id="d6986-148">You can drag the tile to a new location or resize it:</span><span class="sxs-lookup"><span data-stu-id="d6986-148">You can drag the tile to a new location or resize it:</span></span>

    ![Edit dashboard layout](media/tutorial-customize-operator/dashboardlayout.png)

## <a name="configure-your-settings-layout"></a><span data-ttu-id="d6986-150">Configure your settings layout</span><span class="sxs-lookup"><span data-stu-id="d6986-150">Configure your settings layout</span></span>

<span data-ttu-id="d6986-151">As a builder, you can also configure the operator's view of the device settings.</span><span class="sxs-lookup"><span data-stu-id="d6986-151">As a builder, you can also configure the operator's view of the device settings.</span></span> <span data-ttu-id="d6986-152">An operator uses the device settings page to configure a device.</span><span class="sxs-lookup"><span data-stu-id="d6986-152">An operator uses the device settings page to configure a device.</span></span> <span data-ttu-id="d6986-153">For example, an operator uses the settings page to set the target temperature for the refrigerator.</span><span class="sxs-lookup"><span data-stu-id="d6986-153">For example, an operator uses the settings page to set the target temperature for the refrigerator.</span></span>

1. <span data-ttu-id="d6986-154">To edit the settings layout for your connected air conditioner, choose **Settings**, and select **Edit Template**:</span><span class="sxs-lookup"><span data-stu-id="d6986-154">To edit the settings layout for your connected air conditioner, choose **Settings**, and select **Edit Template**:</span></span>

    ![Settings page](media/tutorial-customize-operator/settings.png)

2. <span data-ttu-id="d6986-156">You can move and resize the settings tiles:</span><span class="sxs-lookup"><span data-stu-id="d6986-156">You can move and resize the settings tiles:</span></span>

    ![Edit the settings layout](media/tutorial-customize-operator/settingslayout.png)

> [!NOTE]
> <span data-ttu-id="d6986-158">In **Edit Template** mode, you can't edit the values of the settings.</span><span class="sxs-lookup"><span data-stu-id="d6986-158">In **Edit Template** mode, you can't edit the values of the settings.</span></span>

## <a name="configure-your-properties-layout"></a><span data-ttu-id="d6986-159">Configure your properties layout</span><span class="sxs-lookup"><span data-stu-id="d6986-159">Configure your properties layout</span></span>

<span data-ttu-id="d6986-160">In addition to the dashboard and settings, you can also configure the operator's view of the device properties.</span><span class="sxs-lookup"><span data-stu-id="d6986-160">In addition to the dashboard and settings, you can also configure the operator's view of the device properties.</span></span> <span data-ttu-id="d6986-161">An operator uses the device properties page to manage device metadata.</span><span class="sxs-lookup"><span data-stu-id="d6986-161">An operator uses the device properties page to manage device metadata.</span></span> <span data-ttu-id="d6986-162">For example, an operator uses the properties page to view a device serial number or update contact details for the manufacturer.</span><span class="sxs-lookup"><span data-stu-id="d6986-162">For example, an operator uses the properties page to view a device serial number or update contact details for the manufacturer.</span></span>

1. <span data-ttu-id="d6986-163">To edit the properties layout for your connected air conditioner, choose **Properties**, and select **Edit Template**:</span><span class="sxs-lookup"><span data-stu-id="d6986-163">To edit the properties layout for your connected air conditioner, choose **Properties**, and select **Edit Template**:</span></span>

    ![Properties page](media/tutorial-customize-operator/properties.png)

2. <span data-ttu-id="d6986-165">You can move and resize the properties fields:</span><span class="sxs-lookup"><span data-stu-id="d6986-165">You can move and resize the properties fields:</span></span>

    ![Edit the properties layout](media/tutorial-customize-operator/propertieslayout.png)

> [!NOTE]
> <span data-ttu-id="d6986-167">In **Edit Template** mode, you can't edit the values of the properties.</span><span class="sxs-lookup"><span data-stu-id="d6986-167">In **Edit Template** mode, you can't edit the values of the properties.</span></span>

## <a name="preview-the-connected-air-conditioner-device-as-an-operator"></a><span data-ttu-id="d6986-168">Preview the connected air conditioner device as an operator</span><span class="sxs-lookup"><span data-stu-id="d6986-168">Preview the connected air conditioner device as an operator</span></span>

<span data-ttu-id="d6986-169">In **Edit Template** mode, you can customize the dashboard, settings, and properties pages for an operator.</span><span class="sxs-lookup"><span data-stu-id="d6986-169">In **Edit Template** mode, you can customize the dashboard, settings, and properties pages for an operator.</span></span> <span data-ttu-id="d6986-170">If you are not in **Edit Template** mode, you can view the application as an operator.</span><span class="sxs-lookup"><span data-stu-id="d6986-170">If you are not in **Edit Template** mode, you can view the application as an operator.</span></span>

1. <span data-ttu-id="d6986-171">To view your connected air conditioner device as an operator, you need to click **Done** in order to stop editing the template.</span><span class="sxs-lookup"><span data-stu-id="d6986-171">To view your connected air conditioner device as an operator, you need to click **Done** in order to stop editing the template.</span></span> <span data-ttu-id="d6986-172">This will return you to an operator view of the device.</span><span class="sxs-lookup"><span data-stu-id="d6986-172">This will return you to an operator view of the device.</span></span>

2. <span data-ttu-id="d6986-173">To update the serial number of this device, edit the value  in the serial number tile and choose **Save**:</span><span class="sxs-lookup"><span data-stu-id="d6986-173">To update the serial number of this device, edit the value  in the serial number tile and choose **Save**:</span></span>

    ![Edit a property value](media/tutorial-customize-operator/editproperty.png)

3. <span data-ttu-id="d6986-175">To send a setting to your connected air conditioner, choose **Settings**, change a setting value in a tile, and choose **Update**:</span><span class="sxs-lookup"><span data-stu-id="d6986-175">To send a setting to your connected air conditioner, choose **Settings**, change a setting value in a tile, and choose **Update**:</span></span>

    ![Send setting to device](media/tutorial-customize-operator/sendsetting.png)

    <span data-ttu-id="d6986-177">When the device acknowledges the new setting value, the setting shows as **synced** on the tile.</span><span class="sxs-lookup"><span data-stu-id="d6986-177">When the device acknowledges the new setting value, the setting shows as **synced** on the tile.</span></span>

4. <span data-ttu-id="d6986-178">As an operator, you can view the device dashboard as configured by the builder:</span><span class="sxs-lookup"><span data-stu-id="d6986-178">As an operator, you can view the device dashboard as configured by the builder:</span></span>

    ![Operator's view of the device dashboard](media/tutorial-customize-operator/operatordashboard.png)

## <a name="configure-the-default-home-page"></a><span data-ttu-id="d6986-180">Configure the default home page</span><span class="sxs-lookup"><span data-stu-id="d6986-180">Configure the default home page</span></span>

<span data-ttu-id="d6986-181">When a builder or operator signs in to an Azure IoT Central application, they see a home page.</span><span class="sxs-lookup"><span data-stu-id="d6986-181">When a builder or operator signs in to an Azure IoT Central application, they see a home page.</span></span> <span data-ttu-id="d6986-182">As a builder, you can configure the content of this home page to include the most useful and relevant content for an operator.</span><span class="sxs-lookup"><span data-stu-id="d6986-182">As a builder, you can configure the content of this home page to include the most useful and relevant content for an operator.</span></span>

1. <span data-ttu-id="d6986-183">To customize the default home page, navigate to the **Home** page and select **Edit**, on the top right of the page.</span><span class="sxs-lookup"><span data-stu-id="d6986-183">To customize the default home page, navigate to the **Home** page and select **Edit**, on the top right of the page.</span></span> <span data-ttu-id="d6986-184">Upon selecting **Edit**, a panel will slide out from the right with a list of objects you can add to your Homepage.</span><span class="sxs-lookup"><span data-stu-id="d6986-184">Upon selecting **Edit**, a panel will slide out from the right with a list of objects you can add to your Homepage.</span></span>

    ![Application Builder page](media/tutorial-customize-operator/builderhome.png)

2. <span data-ttu-id="d6986-186">To customize the home page, add tiles from the **Library**.</span><span class="sxs-lookup"><span data-stu-id="d6986-186">To customize the home page, add tiles from the **Library**.</span></span> <span data-ttu-id="d6986-187">Choose **Link**, and add details of your organization's web site.</span><span class="sxs-lookup"><span data-stu-id="d6986-187">Choose **Link**, and add details of your organization's web site.</span></span> <span data-ttu-id="d6986-188">Then choose **Save**:</span><span class="sxs-lookup"><span data-stu-id="d6986-188">Then choose **Save**:</span></span>

    ![Add link to home page](media/tutorial-customize-operator/addlink.png)

    > [!NOTE]
    > <span data-ttu-id="d6986-190">You can also add links to pages within your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="d6986-190">You can also add links to pages within your Azure IoT Central application.</span></span> <span data-ttu-id="d6986-191">For example, you could add a link to a device dashboard or settings page.</span><span class="sxs-lookup"><span data-stu-id="d6986-191">For example, you could add a link to a device dashboard or settings page.</span></span>

3. <span data-ttu-id="d6986-192">Optionally, choose **Image** and upload an image to display on your home page.</span><span class="sxs-lookup"><span data-stu-id="d6986-192">Optionally, choose **Image** and upload an image to display on your home page.</span></span> <span data-ttu-id="d6986-193">An image can have a URL to which you navigate when you click on it:</span><span class="sxs-lookup"><span data-stu-id="d6986-193">An image can have a URL to which you navigate when you click on it:</span></span>

    ![Add image to home page](media/tutorial-customize-operator/addimage.png)

    <span data-ttu-id="d6986-195">To learn more, see [How to prepare and upload images to your Azure IoT Central application](howto-prepare-images.md).</span><span class="sxs-lookup"><span data-stu-id="d6986-195">To learn more, see [How to prepare and upload images to your Azure IoT Central application](howto-prepare-images.md).</span></span>

## <a name="preview-the-default-home-page-as-an-operator"></a><span data-ttu-id="d6986-196">Preview the default home page as an operator</span><span class="sxs-lookup"><span data-stu-id="d6986-196">Preview the default home page as an operator</span></span>

<span data-ttu-id="d6986-197">To preview the home page as an operator and no longer edit, select **Done** on the top right of the page</span><span class="sxs-lookup"><span data-stu-id="d6986-197">To preview the home page as an operator and no longer edit, select **Done** on the top right of the page</span></span>

![Toggle Design Mode](media/tutorial-customize-operator/operatorviewhome.png)

<span data-ttu-id="d6986-199">You can click on the link and image tiles to navigate to the URLs you set as a builder.</span><span class="sxs-lookup"><span data-stu-id="d6986-199">You can click on the link and image tiles to navigate to the URLs you set as a builder.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6986-200">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6986-200">Next steps</span></span>

<span data-ttu-id="d6986-201">In this tutorial, you learned how to customize the operator's view of the application.</span><span class="sxs-lookup"><span data-stu-id="d6986-201">In this tutorial, you learned how to customize the operator's view of the application.</span></span>

<!-- Repeat task list from intro -->
> [!div class="nextstepaction"]
> * <span data-ttu-id="d6986-202">Configure your device dashboard</span><span class="sxs-lookup"><span data-stu-id="d6986-202">Configure your device dashboard</span></span>
> * <span data-ttu-id="d6986-203">Configure your device settings layout</span><span class="sxs-lookup"><span data-stu-id="d6986-203">Configure your device settings layout</span></span>
> * <span data-ttu-id="d6986-204">Configure your device properties layout</span><span class="sxs-lookup"><span data-stu-id="d6986-204">Configure your device properties layout</span></span>
> * <span data-ttu-id="d6986-205">Preview the device as an operator</span><span class="sxs-lookup"><span data-stu-id="d6986-205">Preview the device as an operator</span></span>
> * <span data-ttu-id="d6986-206">Configure your default home page</span><span class="sxs-lookup"><span data-stu-id="d6986-206">Configure your default home page</span></span>
> * <span data-ttu-id="d6986-207">Preview the default home page as an operator</span><span class="sxs-lookup"><span data-stu-id="d6986-207">Preview the default home page as an operator</span></span>

<span data-ttu-id="d6986-208">Now that you have learned how to customize the operator's view of the application, the suggested next steps are:</span><span class="sxs-lookup"><span data-stu-id="d6986-208">Now that you have learned how to customize the operator's view of the application, the suggested next steps are:</span></span>

* [<span data-ttu-id="d6986-209">Monitor your devices (as an operator)</span><span class="sxs-lookup"><span data-stu-id="d6986-209">Monitor your devices (as an operator)</span></span>](tutorial-monitor-devices.md)
* [<span data-ttu-id="d6986-210">Add a new device to your application (as an operator and device developer)</span><span class="sxs-lookup"><span data-stu-id="d6986-210">Add a new device to your application (as an operator and device developer)</span></span>](tutorial-add-device.md)
