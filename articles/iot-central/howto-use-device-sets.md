---
title: Use device sets in your Azure IoT Central application | Microsoft Docs
description: As an operator, how to use device sets in your Azure IoT Central application.
author: ellenfosborne
ms.author: elfarber
ms.date: 01/21/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpfr
ms.openlocfilehash: d0b802842d60d68bab36e87913a84c5e40b8e431
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855822"
---
# <a name="use-device-sets-in-your-azure-iot-central-application"></a><span data-ttu-id="67749-103">Use device sets in your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="67749-103">Use device sets in your Azure IoT Central application</span></span>

<span data-ttu-id="67749-104">This article describes how, as an operator, to use device sets in your Microsoft Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="67749-104">This article describes how, as an operator, to use device sets in your Microsoft Azure IoT Central application.</span></span>

<span data-ttu-id="67749-105">A device set is a list of devices that are grouped together because they all match some specified criteria.</span><span class="sxs-lookup"><span data-stu-id="67749-105">A device set is a list of devices that are grouped together because they all match some specified criteria.</span></span> <span data-ttu-id="67749-106">Device sets help you manage, visualize, and analyze devices at scale by grouping devices into smaller, logical groups.</span><span class="sxs-lookup"><span data-stu-id="67749-106">Device sets help you manage, visualize, and analyze devices at scale by grouping devices into smaller, logical groups.</span></span> <span data-ttu-id="67749-107">For example, you create a list of all the air conditioner devices in Seattle to enable the Seattle technician to find all the devices for which she is responsible.</span><span class="sxs-lookup"><span data-stu-id="67749-107">For example, you create a list of all the air conditioner devices in Seattle to enable the Seattle technician to find all the devices for which she is responsible.</span></span> <span data-ttu-id="67749-108">This article shows you how to create and configure device sets.</span><span class="sxs-lookup"><span data-stu-id="67749-108">This article shows you how to create and configure device sets.</span></span>

## <a name="create-a-device-set"></a><span data-ttu-id="67749-109">Create a device set</span><span class="sxs-lookup"><span data-stu-id="67749-109">Create a device set</span></span>

<span data-ttu-id="67749-110">To create a device set:</span><span class="sxs-lookup"><span data-stu-id="67749-110">To create a device set:</span></span>

1. <span data-ttu-id="67749-111">Choose **Device Sets** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="67749-111">Choose **Device Sets** on the left navigation menu.</span></span>

1. <span data-ttu-id="67749-112">Click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="67749-112">Click **+ New**.</span></span>

    ![New device set](media/howto-use-device-sets/image1.png)

1. <span data-ttu-id="67749-114">Give your device set a name that is unique across the entire application.</span><span class="sxs-lookup"><span data-stu-id="67749-114">Give your device set a name that is unique across the entire application.</span></span> <span data-ttu-id="67749-115">You can also add a description.</span><span class="sxs-lookup"><span data-stu-id="67749-115">You can also add a description.</span></span> <span data-ttu-id="67749-116">A device set can only contain devices from a single device template.</span><span class="sxs-lookup"><span data-stu-id="67749-116">A device set can only contain devices from a single device template.</span></span> <span data-ttu-id="67749-117">Choose the device template to use for this set.</span><span class="sxs-lookup"><span data-stu-id="67749-117">Choose the device template to use for this set.</span></span>

1. <span data-ttu-id="67749-118">Create the query to identify the devices for the device set by selecting a property, a comparison operator, and a value.</span><span class="sxs-lookup"><span data-stu-id="67749-118">Create the query to identify the devices for the device set by selecting a property, a comparison operator, and a value.</span></span> <span data-ttu-id="67749-119">You can add multiple queries and devices that meet **all** the criteria are placed in the device set.</span><span class="sxs-lookup"><span data-stu-id="67749-119">You can add multiple queries and devices that meet **all** the criteria are placed in the device set.</span></span> <span data-ttu-id="67749-120">The device set you create is accessible to anyone who has access to the application, so anyone can view, modify, or delete the device set.</span><span class="sxs-lookup"><span data-stu-id="67749-120">The device set you create is accessible to anyone who has access to the application, so anyone can view, modify, or delete the device set.</span></span>

    ![Device set query](media/howto-use-device-sets/image2.png)

    > [!NOTE]
    > <span data-ttu-id="67749-122">The device set is a dynamic query.</span><span class="sxs-lookup"><span data-stu-id="67749-122">The device set is a dynamic query.</span></span> <span data-ttu-id="67749-123">Every time you view the list of devices, there may be different devices in the list.</span><span class="sxs-lookup"><span data-stu-id="67749-123">Every time you view the list of devices, there may be different devices in the list.</span></span> <span data-ttu-id="67749-124">The list depends on which devices currently meet the criteria of the query.</span><span class="sxs-lookup"><span data-stu-id="67749-124">The list depends on which devices currently meet the criteria of the query.</span></span>

1. <span data-ttu-id="67749-125">Choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="67749-125">Choose **Save**.</span></span>

## <a name="configure-the-dashboard-for-your-device-set"></a><span data-ttu-id="67749-126">Configure the Dashboard for your device set</span><span class="sxs-lookup"><span data-stu-id="67749-126">Configure the Dashboard for your device set</span></span>

<span data-ttu-id="67749-127">After you create your device set, you can configure its **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="67749-127">After you create your device set, you can configure its **Dashboard**.</span></span> <span data-ttu-id="67749-128">The **Dashboard** is the homepage where you can place images and links.</span><span class="sxs-lookup"><span data-stu-id="67749-128">The **Dashboard** is the homepage where you can place images and links.</span></span> <span data-ttu-id="67749-129">You can also add grids that list the devices in the device set.</span><span class="sxs-lookup"><span data-stu-id="67749-129">You can also add grids that list the devices in the device set.</span></span>

1. <span data-ttu-id="67749-130">Choose **Device Sets** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="67749-130">Choose **Device Sets** on the left navigation menu.</span></span>

1. <span data-ttu-id="67749-131">Choose the **Dashboard** tab.</span><span class="sxs-lookup"><span data-stu-id="67749-131">Choose the **Dashboard** tab.</span></span>

1. <span data-ttu-id="67749-132">Turn on **Design Mode**.</span><span class="sxs-lookup"><span data-stu-id="67749-132">Turn on **Design Mode**.</span></span>

    ![Design Mode on](media/howto-use-device-sets/image3.png)

1. <span data-ttu-id="67749-134">For information about adding an image, see [Prepare and upload images to your Azure IoT Central application](howto-prepare-images.md).</span><span class="sxs-lookup"><span data-stu-id="67749-134">For information about adding an image, see [Prepare and upload images to your Azure IoT Central application](howto-prepare-images.md).</span></span>

1. <span data-ttu-id="67749-135">Add a link tile:</span><span class="sxs-lookup"><span data-stu-id="67749-135">Add a link tile:</span></span>
    1. <span data-ttu-id="67749-136">Choose **Link** on the right pane.</span><span class="sxs-lookup"><span data-stu-id="67749-136">Choose **Link** on the right pane.</span></span>

        ![Choose link](media/howto-use-device-sets/image6.png)

    1. <span data-ttu-id="67749-138">Give your link a **Title**.</span><span class="sxs-lookup"><span data-stu-id="67749-138">Give your link a **Title**.</span></span>
    1. <span data-ttu-id="67749-139">Choose a URL to be opened when the link is clicked.</span><span class="sxs-lookup"><span data-stu-id="67749-139">Choose a URL to be opened when the link is clicked.</span></span>
    1. <span data-ttu-id="67749-140">Give your link a description that shows below the **Title**.</span><span class="sxs-lookup"><span data-stu-id="67749-140">Give your link a description that shows below the **Title**.</span></span>
    1. <span data-ttu-id="67749-141">Choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="67749-141">Choose **Save**.</span></span>

        ![Save link](media/howto-use-device-sets/image7.png)

    1. <span data-ttu-id="67749-143">You can move and resize the link tile on the **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="67749-143">You can move and resize the link tile on the **Dashboard**.</span></span>

1. <span data-ttu-id="67749-144">Add a grid.</span><span class="sxs-lookup"><span data-stu-id="67749-144">Add a grid.</span></span> <span data-ttu-id="67749-145">A grid is a table of devices in the device set with the columns you choose.</span><span class="sxs-lookup"><span data-stu-id="67749-145">A grid is a table of devices in the device set with the columns you choose.</span></span>
    1. <span data-ttu-id="67749-146">Choose **Grid** on the right pane.</span><span class="sxs-lookup"><span data-stu-id="67749-146">Choose **Grid** on the right pane.</span></span>

        ![Choose grid](media/howto-use-device-sets/image8.png)

    1. <span data-ttu-id="67749-148">Give your grid a **Title**.</span><span class="sxs-lookup"><span data-stu-id="67749-148">Give your grid a **Title**.</span></span>
    1. <span data-ttu-id="67749-149">Select the columns to be shown by choosing the settings button.</span><span class="sxs-lookup"><span data-stu-id="67749-149">Select the columns to be shown by choosing the settings button.</span></span> <span data-ttu-id="67749-150">In the panel that pops up, choose the column you want shown and choose the right arrow to select it.</span><span class="sxs-lookup"><span data-stu-id="67749-150">In the panel that pops up, choose the column you want shown and choose the right arrow to select it.</span></span>
    1. <span data-ttu-id="67749-151">Choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="67749-151">Choose **OK**.</span></span>
    1. <span data-ttu-id="67749-152">Choose **Save**.</span><span class="sxs-lookup"><span data-stu-id="67749-152">Choose **Save**.</span></span>

        ![Save grid](media/howto-use-device-sets/image9.png)

    1. <span data-ttu-id="67749-154">Drag and drop the grid to place it on the **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="67749-154">Drag and drop the grid to place it on the **Dashboard**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="67749-155">You can add multiple images, links, and grids.</span><span class="sxs-lookup"><span data-stu-id="67749-155">You can add multiple images, links, and grids.</span></span>
  
    1. <span data-ttu-id="67749-156">Turn off **Design Mode**.</span><span class="sxs-lookup"><span data-stu-id="67749-156">Turn off **Design Mode**.</span></span>

    ![Design Mode off](media/howto-use-device-sets/image10.png)


### <a name="configuring-location-map-in-your-device-sets-dashboard"></a><span data-ttu-id="67749-158">Configuring Location Map in your device sets dashboard</span><span class="sxs-lookup"><span data-stu-id="67749-158">Configuring Location Map in your device sets dashboard</span></span> 
<span data-ttu-id="67749-159">You can add a location map to visualize location of your devices sets in a Map.</span><span class="sxs-lookup"><span data-stu-id="67749-159">You can add a location map to visualize location of your devices sets in a Map.</span></span> 

<span data-ttu-id="67749-160">In order to add a location map to you device sets dashboard you must have configured location property in your Device template, see [Create a Location Property powered by Azure Maps](howto-set-up-template.md).</span><span class="sxs-lookup"><span data-stu-id="67749-160">In order to add a location map to you device sets dashboard you must have configured location property in your Device template, see [Create a Location Property powered by Azure Maps](howto-set-up-template.md).</span></span>


1. <span data-ttu-id="67749-161">On Device Sets Dashboard, select Map from the library.</span><span class="sxs-lookup"><span data-stu-id="67749-161">On Device Sets Dashboard, select Map from the library.</span></span> 

    ![Device Sets Dashboard Maps](media/howto-use-device-sets/LocationMaps1.png)


2. <span data-ttu-id="67749-163">Give a title and choose the location property you have previously configured as part of your Device Property.</span><span class="sxs-lookup"><span data-stu-id="67749-163">Give a title and choose the location property you have previously configured as part of your Device Property.</span></span>

    ![Configure Dashboard Maps](media/howto-use-device-sets/LocationMaps2.png)

3. <span data-ttu-id="67749-165">Save and you will see the map tile displaying the location of your devices in the Device Set.</span><span class="sxs-lookup"><span data-stu-id="67749-165">Save and you will see the map tile displaying the location of your devices in the Device Set.</span></span>

    ![Save Dashboard Maps](media/howto-use-device-sets/LocationMaps3.png)


5. <span data-ttu-id="67749-167">Now when an operator views the device sets dashboard, she can see all the tiles you have configured including the location Map to visualize all the devices location at a glance!</span><span class="sxs-lookup"><span data-stu-id="67749-167">Now when an operator views the device sets dashboard, she can see all the tiles you have configured including the location Map to visualize all the devices location at a glance!</span></span> 

    ![Dashboard Maps Operator view](media/howto-use-device-sets/LocationMaps4.png)

    <span data-ttu-id="67749-169">You will be able to resize the map to your desired size.</span><span class="sxs-lookup"><span data-stu-id="67749-169">You will be able to resize the map to your desired size.</span></span>

    <span data-ttu-id="67749-170">Clicking on a pin in the map will display the device information, name and location.</span><span class="sxs-lookup"><span data-stu-id="67749-170">Clicking on a pin in the map will display the device information, name and location.</span></span> <span data-ttu-id="67749-171">You can click on the pop-up to go to the device property page.</span><span class="sxs-lookup"><span data-stu-id="67749-171">You can click on the pop-up to go to the device property page.</span></span>  


## <a name="configure-the-list-for-your-device-set"></a><span data-ttu-id="67749-172">Configure the List for your device set</span><span class="sxs-lookup"><span data-stu-id="67749-172">Configure the List for your device set</span></span>

<span data-ttu-id="67749-173">After you create your device set, you can configure the **List**.</span><span class="sxs-lookup"><span data-stu-id="67749-173">After you create your device set, you can configure the **List**.</span></span> <span data-ttu-id="67749-174">The **List** shows all the devices in the device set in a table with the columns you choose.</span><span class="sxs-lookup"><span data-stu-id="67749-174">The **List** shows all the devices in the device set in a table with the columns you choose.</span></span>

1. <span data-ttu-id="67749-175">Choose **Device Sets** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="67749-175">Choose **Device Sets** on the left navigation menu.</span></span>

1. <span data-ttu-id="67749-176">Choose the **List** tab.</span><span class="sxs-lookup"><span data-stu-id="67749-176">Choose the **List** tab.</span></span>

1. <span data-ttu-id="67749-177">Choose **Column Options**.</span><span class="sxs-lookup"><span data-stu-id="67749-177">Choose **Column Options**.</span></span>

    ![Column options](media/howto-use-device-sets/image11.png)

1. <span data-ttu-id="67749-179">Choose the columns to be shown by selecting the column you want to show and choosing the right arrow to select it.</span><span class="sxs-lookup"><span data-stu-id="67749-179">Choose the columns to be shown by selecting the column you want to show and choosing the right arrow to select it.</span></span>

    ![Choose column](media/howto-use-device-sets/image12.png)

1. <span data-ttu-id="67749-181">Choose **OK**.</span><span class="sxs-lookup"><span data-stu-id="67749-181">Choose **OK**.</span></span>

## <a name="analytics"></a><span data-ttu-id="67749-182">Analytics</span><span class="sxs-lookup"><span data-stu-id="67749-182">Analytics</span></span>

<span data-ttu-id="67749-183">The analytics in device sets is the same as the main analytics tab in the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="67749-183">The analytics in device sets is the same as the main analytics tab in the left navigation menu.</span></span> <span data-ttu-id="67749-184">You can learn more about analytics in the article on [how to create analytics](howto-create-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="67749-184">You can learn more about analytics in the article on [how to create analytics](howto-create-analytics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="67749-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="67749-185">Next steps</span></span>

<span data-ttu-id="67749-186">Now that you have learned how to use device sets in your Azure IoT Central application, here is the suggested next step:</span><span class="sxs-lookup"><span data-stu-id="67749-186">Now that you have learned how to use device sets in your Azure IoT Central application, here is the suggested next step:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="67749-187">How to create telemetry rules</span><span class="sxs-lookup"><span data-stu-id="67749-187">How to create telemetry rules</span></span>](howto-create-telemetry-rules.md)
