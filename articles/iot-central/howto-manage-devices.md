---
title: Manage the devices in your Azure IoT Central application | Microsoft Docs
description: As an operator, learn how to manage devices in your Azure IoT Central application.
author: ellenfosborne
ms.author: elfarber
ms.date: 01/21/2018
ms.topic: conceptual
ms.service: iot-central
services: iot-central
manager: peterpr
ms.openlocfilehash: cf803c03d266f2a400e47fc551dea62936456177
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857699"
---
# <a name="manage-devices-in-your-azure-iot-central-application"></a><span data-ttu-id="e3d4a-103">Manage devices in your Azure IoT Central application</span><span class="sxs-lookup"><span data-stu-id="e3d4a-103">Manage devices in your Azure IoT Central application</span></span>

<span data-ttu-id="e3d4a-104">This article describes how, as an operator, to manage devices in your Microsoft Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-104">This article describes how, as an operator, to manage devices in your Microsoft Azure IoT Central application.</span></span> <span data-ttu-id="e3d4a-105">As an operator, you can:</span><span class="sxs-lookup"><span data-stu-id="e3d4a-105">As an operator, you can:</span></span>

- <span data-ttu-id="e3d4a-106">Use the **Explorer** page to view, add, and delete devices connected to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-106">Use the **Explorer** page to view, add, and delete devices connected to your Azure IoT Central application.</span></span>
- <span data-ttu-id="e3d4a-107">Maintain an up-to-date inventory of your devices.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-107">Maintain an up-to-date inventory of your devices.</span></span>
- <span data-ttu-id="e3d4a-108">Keep your device metadata up-to-date by changing the values stored in the device properties.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-108">Keep your device metadata up-to-date by changing the values stored in the device properties.</span></span>
- <span data-ttu-id="e3d4a-109">Control the behavior of your devices by updating a setting on a specific device from the **Settings** page.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-109">Control the behavior of your devices by updating a setting on a specific device from the **Settings** page.</span></span>

## <a name="view-your-devices"></a><span data-ttu-id="e3d4a-110">View your devices</span><span class="sxs-lookup"><span data-stu-id="e3d4a-110">View your devices</span></span>

<span data-ttu-id="e3d4a-111">To view an individual device:</span><span class="sxs-lookup"><span data-stu-id="e3d4a-111">To view an individual device:</span></span>

1. <span data-ttu-id="e3d4a-112">Choose **Explorer** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-112">Choose **Explorer** on the left navigation menu.</span></span> <span data-ttu-id="e3d4a-113">Here you see a list of your [device templates](howto-set-up-template.md).</span><span class="sxs-lookup"><span data-stu-id="e3d4a-113">Here you see a list of your [device templates](howto-set-up-template.md).</span></span>

1. <span data-ttu-id="e3d4a-114">Choose a **Device Template** in the left-hand pane.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-114">Choose a **Device Template** in the left-hand pane.</span></span>

1. <span data-ttu-id="e3d4a-115">In the right-hand pane, you see a list of devices created from that device template.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-115">In the right-hand pane, you see a list of devices created from that device template.</span></span> <span data-ttu-id="e3d4a-116">Choose an individual device to see the **Device Details** page for that device:</span><span class="sxs-lookup"><span data-stu-id="e3d4a-116">Choose an individual device to see the **Device Details** page for that device:</span></span>

    <span data-ttu-id="e3d4a-117">[![Device Details Page](./media/howto-manage-devices/image1.png)](./media/howto-manage-devices/image1.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="e3d4a-117">[![Device Details Page](./media/howto-manage-devices/image1.png)](./media/howto-manage-devices/image1.png#lightbox)</span></span>

## <a name="add-a-device"></a><span data-ttu-id="e3d4a-118">Add a device</span><span class="sxs-lookup"><span data-stu-id="e3d4a-118">Add a device</span></span>

<span data-ttu-id="e3d4a-119">To add a device to your Azure IoT Central application:</span><span class="sxs-lookup"><span data-stu-id="e3d4a-119">To add a device to your Azure IoT Central application:</span></span>

1. <span data-ttu-id="e3d4a-120">Choose **Explorer** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-120">Choose **Explorer** on the left navigation menu.</span></span>

1. <span data-ttu-id="e3d4a-121">Choose the device template from which you want to create a device.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-121">Choose the device template from which you want to create a device.</span></span>

1. <span data-ttu-id="e3d4a-122">Choose + **New**.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-122">Choose + **New**.</span></span>

1. <span data-ttu-id="e3d4a-123">Choose **Real** or **Simulated**.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-123">Choose **Real** or **Simulated**.</span></span> <span data-ttu-id="e3d4a-124">A real device is for a physical device that you connect to your Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-124">A real device is for a physical device that you connect to your Azure IoT Central application.</span></span> <span data-ttu-id="e3d4a-125">A simulated device has sample data generated for you by Azure IoT Central.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-125">A simulated device has sample data generated for you by Azure IoT Central.</span></span> <span data-ttu-id="e3d4a-126">This example uses a real device.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-126">This example uses a real device.</span></span> <span data-ttu-id="e3d4a-127">Choose **Real** to navigate to the **Device Details** page for your new device.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-127">Choose **Real** to navigate to the **Device Details** page for your new device.</span></span>


## <a name="import-devices"></a><span data-ttu-id="e3d4a-128">Import devices</span><span class="sxs-lookup"><span data-stu-id="e3d4a-128">Import devices</span></span>

<span data-ttu-id="e3d4a-129">To connect large number of devices to your application, Azure IoT Central offers bulk importing devices via a CSV file.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-129">To connect large number of devices to your application, Azure IoT Central offers bulk importing devices via a CSV file.</span></span> 

<span data-ttu-id="e3d4a-130">CSV file requirements:</span><span class="sxs-lookup"><span data-stu-id="e3d4a-130">CSV file requirements:</span></span>
1. <span data-ttu-id="e3d4a-131">The CSV file should have only one column that contains the Device IDs.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-131">The CSV file should have only one column that contains the Device IDs.</span></span>

1. <span data-ttu-id="e3d4a-132">File should not have any header.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-132">File should not have any header.</span></span>


<span data-ttu-id="e3d4a-133">To bulk-register devices in your application:</span><span class="sxs-lookup"><span data-stu-id="e3d4a-133">To bulk-register devices in your application:</span></span>

1. <span data-ttu-id="e3d4a-134">Choose **Explorer** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-134">Choose **Explorer** on the left navigation menu.</span></span>

1. <span data-ttu-id="e3d4a-135">On the left panel, choose the device template for which you want to bulk create the devices.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-135">On the left panel, choose the device template for which you want to bulk create the devices.</span></span>

 >   [!NOTE] 
    <span data-ttu-id="e3d4a-136">If you don’t have a device template yet then you can import devices under **Unassociated devices** and register them without any template.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-136">If you don’t have a device template yet then you can import devices under **Unassociated devices** and register them without any template.</span></span> <span data-ttu-id="e3d4a-137">Once devices have been imported, you can then associate them with a template as a subsequent step.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-137">Once devices have been imported, you can then associate them with a template as a subsequent step.</span></span>

1. <span data-ttu-id="e3d4a-138">Click **Import**.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-138">Click **Import**.</span></span>

    <span data-ttu-id="e3d4a-139">[![Import Action](./media/howto-manage-devices/BulkImport1.png)](./media/howto-manage-devices/BulkImport1.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="e3d4a-139">[![Import Action](./media/howto-manage-devices/BulkImport1.png)](./media/howto-manage-devices/BulkImport1.png#lightbox)</span></span>

1. <span data-ttu-id="e3d4a-140">Select the CSV file that has the list of Device IDs to be imported.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-140">Select the CSV file that has the list of Device IDs to be imported.</span></span>

1. <span data-ttu-id="e3d4a-141">Device import starts once the file has been uploaded.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-141">Device import starts once the file has been uploaded.</span></span> <span data-ttu-id="e3d4a-142">You can track the import status at the top of the device grid.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-142">You can track the import status at the top of the device grid.</span></span>

1. <span data-ttu-id="e3d4a-143">Once the import completes, a success message is shown on the device grid.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-143">Once the import completes, a success message is shown on the device grid.</span></span>

    <span data-ttu-id="e3d4a-144">[![Import Success](./media/howto-manage-devices/BulkImport3.png)](./media/howto-manage-devices/BulkImport3.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="e3d4a-144">[![Import Success](./media/howto-manage-devices/BulkImport3.png)](./media/howto-manage-devices/BulkImport3.png#lightbox)</span></span>

<span data-ttu-id="e3d4a-145">If the device import operation fails, you will see an error message on the Device grid.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-145">If the device import operation fails, you will see an error message on the Device grid.</span></span> <span data-ttu-id="e3d4a-146">A log file capturing all the errors is generated and can be downloaded by clicking the error message.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-146">A log file capturing all the errors is generated and can be downloaded by clicking the error message.</span></span>


<span data-ttu-id="e3d4a-147">**Associating devices with a template**</span><span class="sxs-lookup"><span data-stu-id="e3d4a-147">**Associating devices with a template**</span></span>

<span data-ttu-id="e3d4a-148">If you register devices by starting the import under **Unassociated devices**, then the devices are created without any device template association.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-148">If you register devices by starting the import under **Unassociated devices**, then the devices are created without any device template association.</span></span> <span data-ttu-id="e3d4a-149">Device must be associated with a template to explore the data and other details about the device.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-149">Device must be associated with a template to explore the data and other details about the device.</span></span> <span data-ttu-id="e3d4a-150">Follow these steps to associate devices with a template:</span><span class="sxs-lookup"><span data-stu-id="e3d4a-150">Follow these steps to associate devices with a template:</span></span>
1. <span data-ttu-id="e3d4a-151">Choose **Explorer** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-151">Choose **Explorer** on the left navigation menu.</span></span>
1. <span data-ttu-id="e3d4a-152">On the left panel, choose **Unassociated devices**.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-152">On the left panel, choose **Unassociated devices**.</span></span>
    <span data-ttu-id="e3d4a-153">[![Unassociated Devices](./media/howto-manage-devices/UnassociatedDevices1.png)](./media/howto-manage-devices/UnassociatedDevices1.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="e3d4a-153">[![Unassociated Devices](./media/howto-manage-devices/UnassociatedDevices1.png)](./media/howto-manage-devices/UnassociatedDevices1.png#lightbox)</span></span>
1. <span data-ttu-id="e3d4a-154">Select the devices you want to associate with a template.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-154">Select the devices you want to associate with a template.</span></span>
1. <span data-ttu-id="e3d4a-155">Click **Associate** option.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-155">Click **Associate** option.</span></span>
    <span data-ttu-id="e3d4a-156">[![Associate Devices](./media/howto-manage-devices/UnassociatedDevices2.png)](./media/howto-manage-devices/UnassociatedDevices2.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="e3d4a-156">[![Associate Devices](./media/howto-manage-devices/UnassociatedDevices2.png)](./media/howto-manage-devices/UnassociatedDevices2.png#lightbox)</span></span>
1. <span data-ttu-id="e3d4a-157">Choose the template from the list of available templates and click **Associate** button.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-157">Choose the template from the list of available templates and click **Associate** button.</span></span>
1. <span data-ttu-id="e3d4a-158">The selected devices will be moved under the respective device template.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-158">The selected devices will be moved under the respective device template.</span></span>

 >   [!NOTE] 
    <span data-ttu-id="e3d4a-159">Once a device has been associated with a template it cannot be unassociated or associated with a different template.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-159">Once a device has been associated with a template it cannot be unassociated or associated with a different template.</span></span>

## <a name="export-devices"></a><span data-ttu-id="e3d4a-160">Export devices</span><span class="sxs-lookup"><span data-stu-id="e3d4a-160">Export devices</span></span>

<span data-ttu-id="e3d4a-161">To provision devices to connect to IoT Central, you will need the connection string of the device that is generated by IoT Central.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-161">To provision devices to connect to IoT Central, you will need the connection string of the device that is generated by IoT Central.</span></span> <span data-ttu-id="e3d4a-162">You can use the Export feature to get the connection strings and other properties of the devices in bulk from your application.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-162">You can use the Export feature to get the connection strings and other properties of the devices in bulk from your application.</span></span> <span data-ttu-id="e3d4a-163">Export creates a CSV file with the Device Identity, Device Name, and Primary Connection String for all the selected devices.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-163">Export creates a CSV file with the Device Identity, Device Name, and Primary Connection String for all the selected devices.</span></span>

<span data-ttu-id="e3d4a-164">To bulk export devices from your application:</span><span class="sxs-lookup"><span data-stu-id="e3d4a-164">To bulk export devices from your application:</span></span>
1. <span data-ttu-id="e3d4a-165">Choose **Explorer** on the left navigation menu.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-165">Choose **Explorer** on the left navigation menu.</span></span>

1. <span data-ttu-id="e3d4a-166">On the left panel, choose the device template for which you want to export the devices.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-166">On the left panel, choose the device template for which you want to export the devices.</span></span>

1. <span data-ttu-id="e3d4a-167">Select the devices that you want to export and then click the **Export** action.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-167">Select the devices that you want to export and then click the **Export** action.</span></span>

    <span data-ttu-id="e3d4a-168">[![Export](./media/howto-manage-devices/Export1.png)](./media/howto-manage-devices/Export1.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="e3d4a-168">[![Export](./media/howto-manage-devices/Export1.png)](./media/howto-manage-devices/Export1.png#lightbox)</span></span>

1. <span data-ttu-id="e3d4a-169">Export process will start and you can track the status at the top of the grid.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-169">Export process will start and you can track the status at the top of the grid.</span></span> 

1. <span data-ttu-id="e3d4a-170">Once the export completes, a success message is shown along with a link to download the generated file.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-170">Once the export completes, a success message is shown along with a link to download the generated file.</span></span>

1. <span data-ttu-id="e3d4a-171">Click on the **success message** to download the file to a local folder on the disk.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-171">Click on the **success message** to download the file to a local folder on the disk.</span></span>

    <span data-ttu-id="e3d4a-172">[![Export Success](./media/howto-manage-devices/Export2.png)](./media/howto-manage-devices/Export2.png#lightbox)</span><span class="sxs-lookup"><span data-stu-id="e3d4a-172">[![Export Success](./media/howto-manage-devices/Export2.png)](./media/howto-manage-devices/Export2.png#lightbox)</span></span>

1. <span data-ttu-id="e3d4a-173">The exported CSV file will have the following information:</span><span class="sxs-lookup"><span data-stu-id="e3d4a-173">The exported CSV file will have the following information:</span></span>
    1. <span data-ttu-id="e3d4a-174">Name</span><span class="sxs-lookup"><span data-stu-id="e3d4a-174">Name</span></span>
    1. <span data-ttu-id="e3d4a-175">Device ID</span><span class="sxs-lookup"><span data-stu-id="e3d4a-175">Device ID</span></span>
    1. <span data-ttu-id="e3d4a-176">Primary connection string</span><span class="sxs-lookup"><span data-stu-id="e3d4a-176">Primary connection string</span></span>


## <a name="delete-a-device"></a><span data-ttu-id="e3d4a-177">Delete a device</span><span class="sxs-lookup"><span data-stu-id="e3d4a-177">Delete a device</span></span>

<span data-ttu-id="e3d4a-178">To delete either a real or simulated device from your Azure IoT Central application:</span><span class="sxs-lookup"><span data-stu-id="e3d4a-178">To delete either a real or simulated device from your Azure IoT Central application:</span></span>

1. <span data-ttu-id="e3d4a-179">Choose **Explorer** on the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-179">Choose **Explorer** on the navigation menu.</span></span>

1. <span data-ttu-id="e3d4a-180">Choose the device template of the device you want to delete.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-180">Choose the device template of the device you want to delete.</span></span>

1. <span data-ttu-id="e3d4a-181">Check the box next to the device to delete.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-181">Check the box next to the device to delete.</span></span>

1. <span data-ttu-id="e3d4a-182">Choose **Delete**.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-182">Choose **Delete**.</span></span>

## <a name="change-a-device-setting"></a><span data-ttu-id="e3d4a-183">Change a device setting</span><span class="sxs-lookup"><span data-stu-id="e3d4a-183">Change a device setting</span></span>

<span data-ttu-id="e3d4a-184">Settings control the behavior of a device.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-184">Settings control the behavior of a device.</span></span> <span data-ttu-id="e3d4a-185">In other words, they enable you to provide inputs to your device.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-185">In other words, they enable you to provide inputs to your device.</span></span> <span data-ttu-id="e3d4a-186">You can view and update device settings on the **Device Details** page.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-186">You can view and update device settings on the **Device Details** page.</span></span>

1. <span data-ttu-id="e3d4a-187">Choose **Explorer** on the navigation menu.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-187">Choose **Explorer** on the navigation menu.</span></span>

1. <span data-ttu-id="e3d4a-188">Choose the device template of the device whose settings you want to change.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-188">Choose the device template of the device whose settings you want to change.</span></span>

1. <span data-ttu-id="e3d4a-189">Choose the **Settings** tab. Here you see all the settings your device has and their current values.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-189">Choose the **Settings** tab. Here you see all the settings your device has and their current values.</span></span> <span data-ttu-id="e3d4a-190">For each setting, you can see if the device is still syncing.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-190">For each setting, you can see if the device is still syncing.</span></span>

1. <span data-ttu-id="e3d4a-191">Modify the settings to your desired values.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-191">Modify the settings to your desired values.</span></span> <span data-ttu-id="e3d4a-192">You can modify multiple settings at once and update them all at the same time.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-192">You can modify multiple settings at once and update them all at the same time.</span></span>

1. <span data-ttu-id="e3d4a-193">Choose **Update**.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-193">Choose **Update**.</span></span> <span data-ttu-id="e3d4a-194">The values are sent to your device.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-194">The values are sent to your device.</span></span> <span data-ttu-id="e3d4a-195">When the device acknowledges the setting change, the status of the setting goes back to **synced**.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-195">When the device acknowledges the setting change, the status of the setting goes back to **synced**.</span></span>

## <a name="change-a-property"></a><span data-ttu-id="e3d4a-196">Change a property</span><span class="sxs-lookup"><span data-stu-id="e3d4a-196">Change a property</span></span>

<span data-ttu-id="e3d4a-197">Properties are the device metadata associated with the device, such as city and serial number.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-197">Properties are the device metadata associated with the device, such as city and serial number.</span></span> <span data-ttu-id="e3d4a-198">You can view and update properties on the **Device Details** page.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-198">You can view and update properties on the **Device Details** page.</span></span>

1. <span data-ttu-id="e3d4a-199">Choose **Explorer** on navigation menu.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-199">Choose **Explorer** on navigation menu.</span></span>

1. <span data-ttu-id="e3d4a-200">Choose the device template of the device whose properties you want to change.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-200">Choose the device template of the device whose properties you want to change.</span></span>

1. <span data-ttu-id="e3d4a-201">Choose the **Properties** tab, where you see all the properties.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-201">Choose the **Properties** tab, where you see all the properties.</span></span>

1. <span data-ttu-id="e3d4a-202">Modify the properties to your desired values.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-202">Modify the properties to your desired values.</span></span> <span data-ttu-id="e3d4a-203">You can modify multiple properties at once and update them all at the same time.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-203">You can modify multiple properties at once and update them all at the same time.</span></span>

1. <span data-ttu-id="e3d4a-204">Choose **Update**.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-204">Choose **Update**.</span></span>

> [!NOTE]
> <span data-ttu-id="e3d4a-205">You cannot change the value of _device properties_.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-205">You cannot change the value of _device properties_.</span></span> <span data-ttu-id="e3d4a-206">Device properties are set by the device and are read-only within the Azure IoT Central application.</span><span class="sxs-lookup"><span data-stu-id="e3d4a-206">Device properties are set by the device and are read-only within the Azure IoT Central application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e3d4a-207">Next steps</span><span class="sxs-lookup"><span data-stu-id="e3d4a-207">Next steps</span></span>

<span data-ttu-id="e3d4a-208">Now that you have learned how to manage devices in your Azure IoT Central application, here is the suggested next step:</span><span class="sxs-lookup"><span data-stu-id="e3d4a-208">Now that you have learned how to manage devices in your Azure IoT Central application, here is the suggested next step:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e3d4a-209">How to use device sets</span><span class="sxs-lookup"><span data-stu-id="e3d4a-209">How to use device sets</span></span>](howto-use-device-sets.md)

<!-- Next how-tos in the sequence -->
