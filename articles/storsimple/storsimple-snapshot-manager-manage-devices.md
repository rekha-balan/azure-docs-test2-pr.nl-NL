---
title: Manage devices with StorSimple Snapshot Manager | Microsoft Docs
description: Describes how to use the StorSimple Snapshot Manager MMC snap-in to connect and manage StorSimple devices.
services: storsimple
documentationcenter: ''
author: SharS
manager: carmonm
editor: ''
ms.assetid: 966ecbe3-a7fa-4752-825f-6694dd949946
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 04/18/2016
ms.author: v-sharos
ms.openlocfilehash: 501aaf887ea36588711845e22b748cab5e23201d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551958"
---
# <a name="use-storsimple-snapshot-manager-to-connect-and-manage-storsimple-devices"></a><span data-ttu-id="27435-103">Use StorSimple Snapshot Manager to connect and manage StorSimple devices</span><span class="sxs-lookup"><span data-stu-id="27435-103">Use StorSimple Snapshot Manager to connect and manage StorSimple devices</span></span>
## <a name="overview"></a><span data-ttu-id="27435-104">Overview</span><span class="sxs-lookup"><span data-stu-id="27435-104">Overview</span></span>
<span data-ttu-id="27435-105">You can use nodes in the StorSimple Snapshot Manager **Scope** pane to verify imported StorSimple device data and refresh connected storage devices.</span><span class="sxs-lookup"><span data-stu-id="27435-105">You can use nodes in the StorSimple Snapshot Manager **Scope** pane to verify imported StorSimple device data and refresh connected storage devices.</span></span> <span data-ttu-id="27435-106">Additionally, when you click the **Devices** node, you can see a list of connected devices and corresponding status information in the **Results** pane.</span><span class="sxs-lookup"><span data-stu-id="27435-106">Additionally, when you click the **Devices** node, you can see a list of connected devices and corresponding status information in the **Results** pane.</span></span>

![Connected devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-devices/HCS_SSM_connect_devices.png)

<span data-ttu-id="27435-108">**Figure 1: StorSimple Snapshot Manager connected device**</span><span class="sxs-lookup"><span data-stu-id="27435-108">**Figure 1: StorSimple Snapshot Manager connected device**</span></span> 

<span data-ttu-id="27435-109">Depending on your **View** selections, the **Results** pane shows the following information about each device.</span><span class="sxs-lookup"><span data-stu-id="27435-109">Depending on your **View** selections, the **Results** pane shows the following information about each device.</span></span> <span data-ttu-id="27435-110">(For more information about configuring a view, go to [View menu](storsimple-use-snapshot-manager.md#view-menu).</span><span class="sxs-lookup"><span data-stu-id="27435-110">(For more information about configuring a view, go to [View menu](storsimple-use-snapshot-manager.md#view-menu).</span></span>

| <span data-ttu-id="27435-111">Results column</span><span class="sxs-lookup"><span data-stu-id="27435-111">Results column</span></span> | <span data-ttu-id="27435-112">Description</span><span class="sxs-lookup"><span data-stu-id="27435-112">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="27435-113">Name</span><span class="sxs-lookup"><span data-stu-id="27435-113">Name</span></span> |<span data-ttu-id="27435-114">The name of the device as configured in the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="27435-114">The name of the device as configured in the Azure classic portal</span></span> |
| <span data-ttu-id="27435-115">Model</span><span class="sxs-lookup"><span data-stu-id="27435-115">Model</span></span> |<span data-ttu-id="27435-116">The model number of the device</span><span class="sxs-lookup"><span data-stu-id="27435-116">The model number of the device</span></span> |
| <span data-ttu-id="27435-117">Version</span><span class="sxs-lookup"><span data-stu-id="27435-117">Version</span></span> |<span data-ttu-id="27435-118">The version of the software installed on the device</span><span class="sxs-lookup"><span data-stu-id="27435-118">The version of the software installed on the device</span></span> |
| <span data-ttu-id="27435-119">Status</span><span class="sxs-lookup"><span data-stu-id="27435-119">Status</span></span> |<span data-ttu-id="27435-120">Whether the device is available</span><span class="sxs-lookup"><span data-stu-id="27435-120">Whether the device is available</span></span> |
| <span data-ttu-id="27435-121">Last Synced</span><span class="sxs-lookup"><span data-stu-id="27435-121">Last Synced</span></span> |<span data-ttu-id="27435-122">Date and time when the device was last synchronized</span><span class="sxs-lookup"><span data-stu-id="27435-122">Date and time when the device was last synchronized</span></span> |
| <span data-ttu-id="27435-123">Serial No.</span><span class="sxs-lookup"><span data-stu-id="27435-123">Serial No.</span></span> |<span data-ttu-id="27435-124">The serial number for the device</span><span class="sxs-lookup"><span data-stu-id="27435-124">The serial number for the device</span></span> |

<span data-ttu-id="27435-125">If you right-click the **Devices** node in the **Scope** pane, you can select from the following actions:</span><span class="sxs-lookup"><span data-stu-id="27435-125">If you right-click the **Devices** node in the **Scope** pane, you can select from the following actions:</span></span>

* <span data-ttu-id="27435-126">Add or replace a device</span><span class="sxs-lookup"><span data-stu-id="27435-126">Add or replace a device</span></span> 
* <span data-ttu-id="27435-127">Connect a device and verify imports</span><span class="sxs-lookup"><span data-stu-id="27435-127">Connect a device and verify imports</span></span> 
* <span data-ttu-id="27435-128">Refresh connected devices</span><span class="sxs-lookup"><span data-stu-id="27435-128">Refresh connected devices</span></span> 

<span data-ttu-id="27435-129">If you click the **Devices** node and then right-click a device name in the **Results** pane, you can select from the following actions:</span><span class="sxs-lookup"><span data-stu-id="27435-129">If you click the **Devices** node and then right-click a device name in the **Results** pane, you can select from the following actions:</span></span>

* <span data-ttu-id="27435-130">Authenticate a device</span><span class="sxs-lookup"><span data-stu-id="27435-130">Authenticate a device</span></span> 
* <span data-ttu-id="27435-131">View device details</span><span class="sxs-lookup"><span data-stu-id="27435-131">View device details</span></span> 
* <span data-ttu-id="27435-132">Refresh a device</span><span class="sxs-lookup"><span data-stu-id="27435-132">Refresh a device</span></span> 
* <span data-ttu-id="27435-133">Delete a device configuration</span><span class="sxs-lookup"><span data-stu-id="27435-133">Delete a device configuration</span></span> 
* <span data-ttu-id="27435-134">Change a device password</span><span class="sxs-lookup"><span data-stu-id="27435-134">Change a device password</span></span>

> [!NOTE]
> <span data-ttu-id="27435-135">All of these actions are also available in the **Actions** pane.</span><span class="sxs-lookup"><span data-stu-id="27435-135">All of these actions are also available in the **Actions** pane.</span></span>
> 
> 

<span data-ttu-id="27435-136">This tutorial explains how to use StorSimple Snapshot Manager to connect and manage devices and perform the following tasks:</span><span class="sxs-lookup"><span data-stu-id="27435-136">This tutorial explains how to use StorSimple Snapshot Manager to connect and manage devices and perform the following tasks:</span></span>

* <span data-ttu-id="27435-137">Add or replace a device</span><span class="sxs-lookup"><span data-stu-id="27435-137">Add or replace a device</span></span> 
* <span data-ttu-id="27435-138">Connect a device and verify imports</span><span class="sxs-lookup"><span data-stu-id="27435-138">Connect a device and verify imports</span></span> 
* <span data-ttu-id="27435-139">Refresh connected devices</span><span class="sxs-lookup"><span data-stu-id="27435-139">Refresh connected devices</span></span> 
* <span data-ttu-id="27435-140">Authenticate a device</span><span class="sxs-lookup"><span data-stu-id="27435-140">Authenticate a device</span></span> 
* <span data-ttu-id="27435-141">View device details</span><span class="sxs-lookup"><span data-stu-id="27435-141">View device details</span></span> 
* <span data-ttu-id="27435-142">Refresh an individual device</span><span class="sxs-lookup"><span data-stu-id="27435-142">Refresh an individual device</span></span> 
* <span data-ttu-id="27435-143">Delete a device configuration</span><span class="sxs-lookup"><span data-stu-id="27435-143">Delete a device configuration</span></span> 
* <span data-ttu-id="27435-144">Change an expired device password</span><span class="sxs-lookup"><span data-stu-id="27435-144">Change an expired device password</span></span>
* <span data-ttu-id="27435-145">Replace a failed device</span><span class="sxs-lookup"><span data-stu-id="27435-145">Replace a failed device</span></span>

> [!NOTE]
> <span data-ttu-id="27435-146">For general information about using the StorSimple Snapshot Manager interface, go to [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span><span class="sxs-lookup"><span data-stu-id="27435-146">For general information about using the StorSimple Snapshot Manager interface, go to [StorSimple Snapshot Manager user interface](storsimple-use-snapshot-manager.md).</span></span>
> 
> 

## <a name="add-or-replace-a-device"></a><span data-ttu-id="27435-147">Add or replace a device</span><span class="sxs-lookup"><span data-stu-id="27435-147">Add or replace a device</span></span>
<span data-ttu-id="27435-148">Use the following procedure to add or replace a StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="27435-148">Use the following procedure to add or replace a StorSimple device.</span></span>

#### <a name="to-add-or-replace-a-device"></a><span data-ttu-id="27435-149">To add or replace a device</span><span class="sxs-lookup"><span data-stu-id="27435-149">To add or replace a device</span></span>
1. <span data-ttu-id="27435-150">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-150">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="27435-151">In the **Scope** pane, right-click the **Devices** node, and then click **Configure a device**.</span><span class="sxs-lookup"><span data-stu-id="27435-151">In the **Scope** pane, right-click the **Devices** node, and then click **Configure a device**.</span></span> <span data-ttu-id="27435-152">The **Configure a Device** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="27435-152">The **Configure a Device** dialog box appears.</span></span>
   
    ![Configure a StorSimple device](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-devices/HCS_SSM_config_device.png) 
3. <span data-ttu-id="27435-154">In the **Device** drop-down box, select the IP address of the device or virtual device.</span><span class="sxs-lookup"><span data-stu-id="27435-154">In the **Device** drop-down box, select the IP address of the device or virtual device.</span></span> 
4. <span data-ttu-id="27435-155">In the **Password** text box, type the StorSimple Snapshot Manager password that you created for the device in the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="27435-155">In the **Password** text box, type the StorSimple Snapshot Manager password that you created for the device in the Azure classic portal.</span></span> <span data-ttu-id="27435-156">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="27435-156">Click **OK**.</span></span> <span data-ttu-id="27435-157">StorSimple Snapshot Manager searches for the device that you identified.</span><span class="sxs-lookup"><span data-stu-id="27435-157">StorSimple Snapshot Manager searches for the device that you identified.</span></span> 
   
   * <span data-ttu-id="27435-158">If the device is available, StorSimple Snapshot Manager adds a connection.</span><span class="sxs-lookup"><span data-stu-id="27435-158">If the device is available, StorSimple Snapshot Manager adds a connection.</span></span> 
   * <span data-ttu-id="27435-159">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span><span class="sxs-lookup"><span data-stu-id="27435-159">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> <span data-ttu-id="27435-160">Click **OK** to close the error message, and then click **Cancel** to close the **Configure a Device** dialog box.</span><span class="sxs-lookup"><span data-stu-id="27435-160">Click **OK** to close the error message, and then click **Cancel** to close the **Configure a Device** dialog box.</span></span>

## <a name="connect-a-device-and-verify-imports"></a><span data-ttu-id="27435-161">Connect a device and verify imports</span><span class="sxs-lookup"><span data-stu-id="27435-161">Connect a device and verify imports</span></span>
<span data-ttu-id="27435-162">Use the following procedure to connect a StorSimple device and verify that any existing volume groups that have associated backups are imported.</span><span class="sxs-lookup"><span data-stu-id="27435-162">Use the following procedure to connect a StorSimple device and verify that any existing volume groups that have associated backups are imported.</span></span>

#### <a name="to-connect-a-device-and-verify-imports"></a><span data-ttu-id="27435-163">To connect a device and verify imports</span><span class="sxs-lookup"><span data-stu-id="27435-163">To connect a device and verify imports</span></span>
1. <span data-ttu-id="27435-164">To connect a device to StorSimple Snapshot Manager, follow the instructions in Add or replace a device.</span><span class="sxs-lookup"><span data-stu-id="27435-164">To connect a device to StorSimple Snapshot Manager, follow the instructions in Add or replace a device.</span></span> <span data-ttu-id="27435-165">When it connects to a device, StorSimple Snapshot Manager responds as follows:</span><span class="sxs-lookup"><span data-stu-id="27435-165">When it connects to a device, StorSimple Snapshot Manager responds as follows:</span></span>
   
   * <span data-ttu-id="27435-166">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span><span class="sxs-lookup"><span data-stu-id="27435-166">If the device is unavailable for any reason, StorSimple Snapshot Manager returns an error message.</span></span> 
   
   * <span data-ttu-id="27435-167">If the device is available, StorSimple Snapshot Manager adds a connection.</span><span class="sxs-lookup"><span data-stu-id="27435-167">If the device is available, StorSimple Snapshot Manager adds a connection.</span></span> <span data-ttu-id="27435-168">When you select the device, it appears in the **Results** pane, and the status field indicates that the device is **Available**.</span><span class="sxs-lookup"><span data-stu-id="27435-168">When you select the device, it appears in the **Results** pane, and the status field indicates that the device is **Available**.</span></span> <span data-ttu-id="27435-169">StorSimple Snapshot Manager imports any volume groups configured for the device, provided that the volume groups have associated backups.</span><span class="sxs-lookup"><span data-stu-id="27435-169">StorSimple Snapshot Manager imports any volume groups configured for the device, provided that the volume groups have associated backups.</span></span> <span data-ttu-id="27435-170">Backup policies are not imported.</span><span class="sxs-lookup"><span data-stu-id="27435-170">Backup policies are not imported.</span></span> <span data-ttu-id="27435-171">Volume groups that do not have associated backups are not imported.</span><span class="sxs-lookup"><span data-stu-id="27435-171">Volume groups that do not have associated backups are not imported.</span></span>
2. <span data-ttu-id="27435-172">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-172">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
3. <span data-ttu-id="27435-173">Right-click the top node in the **Scope** pane, and then click **Toggle Imports Display**.</span><span class="sxs-lookup"><span data-stu-id="27435-173">Right-click the top node in the **Scope** pane, and then click **Toggle Imports Display**.</span></span>
   
    ![Select Toggle Imports Display](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Toggle_Imports_Display.png) 
4. <span data-ttu-id="27435-175">The **Toggle Imports Display** dialog box appears, showing the status of the imported volume groups and backups.</span><span class="sxs-lookup"><span data-stu-id="27435-175">The **Toggle Imports Display** dialog box appears, showing the status of the imported volume groups and backups.</span></span> <span data-ttu-id="27435-176">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="27435-176">Click **OK**.</span></span> 

<span data-ttu-id="27435-177">After the volume groups and backups are successfully imported, you can use StorSimple Snapshot Manager to manage them, just as you would manage volume groups and backups that you created and configured with StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-177">After the volume groups and backups are successfully imported, you can use StorSimple Snapshot Manager to manage them, just as you would manage volume groups and backups that you created and configured with StorSimple Snapshot Manager.</span></span> 

## <a name="refresh-connected-devices"></a><span data-ttu-id="27435-178">Refresh connected devices</span><span class="sxs-lookup"><span data-stu-id="27435-178">Refresh connected devices</span></span>
<span data-ttu-id="27435-179">Use the following procedure to synchronize the connected StorSimple devices with StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-179">Use the following procedure to synchronize the connected StorSimple devices with StorSimple Snapshot Manager.</span></span>

#### <a name="to-refresh-connected-devices"></a><span data-ttu-id="27435-180">To refresh connected devices</span><span class="sxs-lookup"><span data-stu-id="27435-180">To refresh connected devices</span></span>
1. <span data-ttu-id="27435-181">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-181">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="27435-182">In the **Scope** pane, right-click **Devices**, and then click **Refresh Devices**.</span><span class="sxs-lookup"><span data-stu-id="27435-182">In the **Scope** pane, right-click **Devices**, and then click **Refresh Devices**.</span></span> <span data-ttu-id="27435-183">This synchronizes the connected devices with StorSimple Snapshot Manager so that you can view the volume groups and backups, including any recent additions.</span><span class="sxs-lookup"><span data-stu-id="27435-183">This synchronizes the connected devices with StorSimple Snapshot Manager so that you can view the volume groups and backups, including any recent additions.</span></span> 
   
    ![Refresh the StorSimple devices](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Refresh_devices.png)

<span data-ttu-id="27435-185">The **Refresh Devices** action retrieves any new volume groups and any associated backups from connected devices.</span><span class="sxs-lookup"><span data-stu-id="27435-185">The **Refresh Devices** action retrieves any new volume groups and any associated backups from connected devices.</span></span> <span data-ttu-id="27435-186">Unlike the **Rescan volumes** action available for the **Volumes** node, **Refresh Devices** does not restore the backup registry.</span><span class="sxs-lookup"><span data-stu-id="27435-186">Unlike the **Rescan volumes** action available for the **Volumes** node, **Refresh Devices** does not restore the backup registry.</span></span>

## <a name="authenticate-a-device"></a><span data-ttu-id="27435-187">Authenticate a device</span><span class="sxs-lookup"><span data-stu-id="27435-187">Authenticate a device</span></span>
<span data-ttu-id="27435-188">Use the following procedure to authenticate a StorSimple device with StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-188">Use the following procedure to authenticate a StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-authenticate-a-device"></a><span data-ttu-id="27435-189">To authenticate a device</span><span class="sxs-lookup"><span data-stu-id="27435-189">To authenticate a device</span></span>
1. <span data-ttu-id="27435-190">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-190">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="27435-191">In the **Scope** pane, click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="27435-191">In the **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="27435-192">In the **Results** pane, right-click the name of the device, and then click **Authenticate**.</span><span class="sxs-lookup"><span data-stu-id="27435-192">In the **Results** pane, right-click the name of the device, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="27435-193">The **Authenticate** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="27435-193">The **Authenticate** dialog box appears.</span></span> <span data-ttu-id="27435-194">Type the device password, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="27435-194">Type the device password, and then click **OK**.</span></span>
   
    ![Authenticate dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Authenticate.png) 

## <a name="view-device-details"></a><span data-ttu-id="27435-196">View device details</span><span class="sxs-lookup"><span data-stu-id="27435-196">View device details</span></span>
<span data-ttu-id="27435-197">Use the following procedure to view the details of a StorSimple device and, if necessary, resynchronize the device with StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-197">Use the following procedure to view the details of a StorSimple device and, if necessary, resynchronize the device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-view-and-resynchronize-device-details"></a><span data-ttu-id="27435-198">To view and resynchronize device details</span><span class="sxs-lookup"><span data-stu-id="27435-198">To view and resynchronize device details</span></span>
1. <span data-ttu-id="27435-199">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-199">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="27435-200">In the **Scope** pane, click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="27435-200">In the **Scope** pane, click **Devices**.</span></span>
3. <span data-ttu-id="27435-201">In the **Results** pane, right-click the name of the device, and then click **Details**.</span><span class="sxs-lookup"><span data-stu-id="27435-201">In the **Results** pane, right-click the name of the device, and then click **Details**.</span></span> 

<span data-ttu-id="27435-202">4.The **Device Details** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="27435-202">4.The **Device Details** dialog box appears.</span></span> <span data-ttu-id="27435-203">This box shows the name, model, version, serial number, status, target iSCSI Qualified Name (IQN), and last synchronization date and time.</span><span class="sxs-lookup"><span data-stu-id="27435-203">This box shows the name, model, version, serial number, status, target iSCSI Qualified Name (IQN), and last synchronization date and time.</span></span> 

* <span data-ttu-id="27435-204">Click **Resync** to synchronize the device.</span><span class="sxs-lookup"><span data-stu-id="27435-204">Click **Resync** to synchronize the device.</span></span>
* <span data-ttu-id="27435-205">Click **OK** or **Cancel** to close the dialog box.</span><span class="sxs-lookup"><span data-stu-id="27435-205">Click **OK** or **Cancel** to close the dialog box.</span></span>
  
  ![Device details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-devices/HCS_SSM_Device_details.png) 

## <a name="refresh-an-individual-device"></a><span data-ttu-id="27435-207">Refresh an individual device</span><span class="sxs-lookup"><span data-stu-id="27435-207">Refresh an individual device</span></span>
<span data-ttu-id="27435-208">Use the following procedure to resynchronize an individual StorSimple device with StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-208">Use the following procedure to resynchronize an individual StorSimple device with StorSimple Snapshot Manager.</span></span>

#### <a name="to-refresh-a-device"></a><span data-ttu-id="27435-209">To refresh a device</span><span class="sxs-lookup"><span data-stu-id="27435-209">To refresh a device</span></span>
1. <span data-ttu-id="27435-210">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-210">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="27435-211">In the **Scope** pane, click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="27435-211">In the **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="27435-212">In the **Results** pane, right-click the name of the device, and then click **Refresh Device**.</span><span class="sxs-lookup"><span data-stu-id="27435-212">In the **Results** pane, right-click the name of the device, and then click **Refresh Device**.</span></span> <span data-ttu-id="27435-213">This synchronizes the device with StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-213">This synchronizes the device with StorSimple Snapshot Manager.</span></span> 

## <a name="delete-a-device-configuration"></a><span data-ttu-id="27435-214">Delete a device configuration</span><span class="sxs-lookup"><span data-stu-id="27435-214">Delete a device configuration</span></span>
<span data-ttu-id="27435-215">Use the following procedure to delete an individual StorSimple device configuration from StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-215">Use the following procedure to delete an individual StorSimple device configuration from StorSimple Snapshot Manager.</span></span>

#### <a name="to-delete-a-device-configuration"></a><span data-ttu-id="27435-216">To delete a device configuration</span><span class="sxs-lookup"><span data-stu-id="27435-216">To delete a device configuration</span></span>
1. <span data-ttu-id="27435-217">Click the desktop icon to start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-217">Click the desktop icon to start StorSimple Snapshot Manager.</span></span> 
2. <span data-ttu-id="27435-218">In the **Scope** pane, click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="27435-218">In the **Scope** pane, click **Devices**.</span></span> 
3. <span data-ttu-id="27435-219">In the **Results** pane, right-click the name of the device, and then click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="27435-219">In the **Results** pane, right-click the name of the device, and then click **Delete**.</span></span> 
4. <span data-ttu-id="27435-220">The following message appears.</span><span class="sxs-lookup"><span data-stu-id="27435-220">The following message appears.</span></span> <span data-ttu-id="27435-221">Click **Yes** to delete the configuration or click **No** to cancel the deletion.</span><span class="sxs-lookup"><span data-stu-id="27435-221">Click **Yes** to delete the configuration or click **No** to cancel the deletion.</span></span>
   
    ![Delete device configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-snapshot-manager-manage-devices/HCS_SSM_DeleteDevice.png)

## <a name="change-an-expired-device-password"></a><span data-ttu-id="27435-223">Change an expired device password</span><span class="sxs-lookup"><span data-stu-id="27435-223">Change an expired device password</span></span>
<span data-ttu-id="27435-224">You must enter a password to authenticate a StorSimple device with StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-224">You must enter a password to authenticate a StorSimple device with StorSimple Snapshot Manager.</span></span> <span data-ttu-id="27435-225">You configure this password when you use the Windows PowerShell interface to set up the device.</span><span class="sxs-lookup"><span data-stu-id="27435-225">You configure this password when you use the Windows PowerShell interface to set up the device.</span></span> <span data-ttu-id="27435-226">However, the password can expire.</span><span class="sxs-lookup"><span data-stu-id="27435-226">However, the password can expire.</span></span> <span data-ttu-id="27435-227">If this happens, you can use the Azure classic portal to change the password.</span><span class="sxs-lookup"><span data-stu-id="27435-227">If this happens, you can use the Azure classic portal to change the password.</span></span> <span data-ttu-id="27435-228">Then, because the device was configured in StorSimple Snapshot Manager before the password expired, you must re-authenticate the device in StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-228">Then, because the device was configured in StorSimple Snapshot Manager before the password expired, you must re-authenticate the device in StorSimple Snapshot Manager.</span></span> 

#### <a name="to-change-the-expired-password"></a><span data-ttu-id="27435-229">To change the expired password</span><span class="sxs-lookup"><span data-stu-id="27435-229">To change the expired password</span></span>
1. <span data-ttu-id="27435-230">In the Azure classic portal, start the StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="27435-230">In the Azure classic portal, start the StorSimple Manager service.</span></span>
2. <span data-ttu-id="27435-231">Click **Devices** > **Configure** for the device.</span><span class="sxs-lookup"><span data-stu-id="27435-231">Click **Devices** > **Configure** for the device.</span></span>
3. <span data-ttu-id="27435-232">Scroll down to the StorSimple Snapshot Manager section.</span><span class="sxs-lookup"><span data-stu-id="27435-232">Scroll down to the StorSimple Snapshot Manager section.</span></span> <span data-ttu-id="27435-233">Enter a password that is 14-15 characters.</span><span class="sxs-lookup"><span data-stu-id="27435-233">Enter a password that is 14-15 characters.</span></span> <span data-ttu-id="27435-234">Make sure that the password contains a mix of uppercase, lowercase, numeric, and special characters.</span><span class="sxs-lookup"><span data-stu-id="27435-234">Make sure that the password contains a mix of uppercase, lowercase, numeric, and special characters.</span></span>
4. <span data-ttu-id="27435-235">Re-enter the password to confirm it.</span><span class="sxs-lookup"><span data-stu-id="27435-235">Re-enter the password to confirm it.</span></span>
5. <span data-ttu-id="27435-236">Click **Save** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="27435-236">Click **Save** at the bottom of the page.</span></span>

#### <a name="to-re-authenticate-the-device"></a><span data-ttu-id="27435-237">To re-authenticate the device</span><span class="sxs-lookup"><span data-stu-id="27435-237">To re-authenticate the device</span></span>
1. <span data-ttu-id="27435-238">Start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-238">Start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="27435-239">In the **Scope** pane, click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="27435-239">In the **Scope** pane, click **Devices**.</span></span> <span data-ttu-id="27435-240">A list of configured devices appears in the **Results** pane.</span><span class="sxs-lookup"><span data-stu-id="27435-240">A list of configured devices appears in the **Results** pane.</span></span> 
3. <span data-ttu-id="27435-241">Select the device, right-click, and then click **Authenticate**.</span><span class="sxs-lookup"><span data-stu-id="27435-241">Select the device, right-click, and then click **Authenticate**.</span></span>
4. <span data-ttu-id="27435-242">In the **Authenticate** window, enter the new password.</span><span class="sxs-lookup"><span data-stu-id="27435-242">In the **Authenticate** window, enter the new password.</span></span> 
5. <span data-ttu-id="27435-243">Select the device, right-click, and select **Refresh device**.</span><span class="sxs-lookup"><span data-stu-id="27435-243">Select the device, right-click, and select **Refresh device**.</span></span> <span data-ttu-id="27435-244">This synchronizes the device with StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-244">This synchronizes the device with StorSimple Snapshot Manager.</span></span> 

## <a name="replace-a-failed-device"></a><span data-ttu-id="27435-245">Replace a failed device</span><span class="sxs-lookup"><span data-stu-id="27435-245">Replace a failed device</span></span>
<span data-ttu-id="27435-246">If a StorSimple device fails and is replaced by a standby (failover) device, use the following steps to connect to the new device and view the associated backups.</span><span class="sxs-lookup"><span data-stu-id="27435-246">If a StorSimple device fails and is replaced by a standby (failover) device, use the following steps to connect to the new device and view the associated backups.</span></span>

#### <a name="to-connect-to-a-new-device-after-failover"></a><span data-ttu-id="27435-247">To connect to a new device after failover</span><span class="sxs-lookup"><span data-stu-id="27435-247">To connect to a new device after failover</span></span>
1. <span data-ttu-id="27435-248">Reconfigure the iSCSI connection to the new device.</span><span class="sxs-lookup"><span data-stu-id="27435-248">Reconfigure the iSCSI connection to the new device.</span></span> <span data-ttu-id="27435-249">For instructions, go to "Step 7: Mount, initialize, and format a volume" in [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span><span class="sxs-lookup"><span data-stu-id="27435-249">For instructions, go to "Step 7: Mount, initialize, and format a volume" in [Deploy your on-premises StorSimple device](storsimple-deployment-walkthrough-u2.md).</span></span> 

> [!NOTE]
> <span data-ttu-id="27435-250">If the new StorSimple device has the same IP address as the old one, you might be able to connect the old configuration.</span><span class="sxs-lookup"><span data-stu-id="27435-250">If the new StorSimple device has the same IP address as the old one, you might be able to connect the old configuration.</span></span> 
> 
> 

1. <span data-ttu-id="27435-251">Stop the Microsoft StorSimple Management Service:</span><span class="sxs-lookup"><span data-stu-id="27435-251">Stop the Microsoft StorSimple Management Service:</span></span>
   
   1. <span data-ttu-id="27435-252">Start Server Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-252">Start Server Manager.</span></span>
   2. <span data-ttu-id="27435-253">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span><span class="sxs-lookup"><span data-stu-id="27435-253">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span> 
   3. <span data-ttu-id="27435-254">On the **Services** window, select the **Microsoft StorSimple Management Service**.</span><span class="sxs-lookup"><span data-stu-id="27435-254">On the **Services** window, select the **Microsoft StorSimple Management Service**.</span></span> 
   4. <span data-ttu-id="27435-255">In the right pane, under **Microsoft StorSimple Management Service**, click **Stop the service**.</span><span class="sxs-lookup"><span data-stu-id="27435-255">In the right pane, under **Microsoft StorSimple Management Service**, click **Stop the service**.</span></span> 
2. <span data-ttu-id="27435-256">Remove the configuration information related to the old device:</span><span class="sxs-lookup"><span data-stu-id="27435-256">Remove the configuration information related to the old device:</span></span> 
   
   1. <span data-ttu-id="27435-257">In File Explorer, browse to C:\ProgramData\Microsoft\StorSimple\BACatalog.</span><span class="sxs-lookup"><span data-stu-id="27435-257">In File Explorer, browse to C:\ProgramData\Microsoft\StorSimple\BACatalog.</span></span> 
   2. <span data-ttu-id="27435-258">Delete the files in the BACatalog folder.</span><span class="sxs-lookup"><span data-stu-id="27435-258">Delete the files in the BACatalog folder.</span></span> 
3. <span data-ttu-id="27435-259">Restart the Microsoft StorSimple Management Service:</span><span class="sxs-lookup"><span data-stu-id="27435-259">Restart the Microsoft StorSimple Management Service:</span></span> 
   
   1. <span data-ttu-id="27435-260">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span><span class="sxs-lookup"><span data-stu-id="27435-260">On the Server Manager Dashboard, on the **Tools** menu, select **Services**.</span></span> 
   2. <span data-ttu-id="27435-261">On the **Services** window, select the **Microsoft StorSimple Management Service**.</span><span class="sxs-lookup"><span data-stu-id="27435-261">On the **Services** window, select the **Microsoft StorSimple Management Service**.</span></span> 
   3. <span data-ttu-id="27435-262">In the right pane, under **Microsoft StorSimple Management Service**, click **Restart the service**.</span><span class="sxs-lookup"><span data-stu-id="27435-262">In the right pane, under **Microsoft StorSimple Management Service**, click **Restart the service**.</span></span> 
4. <span data-ttu-id="27435-263">Start StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-263">Start StorSimple Snapshot Manager.</span></span> 
5. <span data-ttu-id="27435-264">To configure the new StorSimple device, complete the steps in Step 2: Connect a StorSimple device in [Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span><span class="sxs-lookup"><span data-stu-id="27435-264">To configure the new StorSimple device, complete the steps in Step 2: Connect a StorSimple device in [Deploy StorSimple Snapshot Manager](storsimple-snapshot-manager-deployment.md).</span></span> 
6. <span data-ttu-id="27435-265">Right-click the top-level node in the **Scope** pane (StorSimple Snapshot Manager in the example), and then click **Toggle Imports Display**.</span><span class="sxs-lookup"><span data-stu-id="27435-265">Right-click the top-level node in the **Scope** pane (StorSimple Snapshot Manager in the example), and then click **Toggle Imports Display**.</span></span> 
7. <span data-ttu-id="27435-266">A message appears when the imported volume groups and backups are visible in StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="27435-266">A message appears when the imported volume groups and backups are visible in StorSimple Snapshot Manager.</span></span> <span data-ttu-id="27435-267">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="27435-267">Click **OK**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="27435-268">Next steps</span><span class="sxs-lookup"><span data-stu-id="27435-268">Next steps</span></span>
* <span data-ttu-id="27435-269">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="27435-269">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="27435-270">Learn how to [use StorSimple Snapshot Manager to view and manage volumes](storsimple-snapshot-manager-manage-volumes.md).</span><span class="sxs-lookup"><span data-stu-id="27435-270">Learn how to [use StorSimple Snapshot Manager to view and manage volumes](storsimple-snapshot-manager-manage-volumes.md).</span></span>








