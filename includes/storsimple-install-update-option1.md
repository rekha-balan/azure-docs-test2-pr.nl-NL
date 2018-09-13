<!--author=SharS last changed: 03/17/2016-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="08449-101">To download hotfixes</span><span class="sxs-lookup"><span data-stu-id="08449-101">To download hotfixes</span></span>
<span data-ttu-id="08449-102">Perform the following steps to download the software update.</span><span class="sxs-lookup"><span data-stu-id="08449-102">Perform the following steps to download the software update.</span></span>

1. <span data-ttu-id="08449-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="08449-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="08449-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span><span class="sxs-lookup"><span data-stu-id="08449-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="08449-105">![Install catalog](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="08449-105">![Install catalog](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-update-option-1/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="08449-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3063418**, and then click **Search**.</span><span class="sxs-lookup"><span data-stu-id="08449-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3063418**, and then click **Search**.</span></span>
4. <span data-ttu-id="08449-107">You will see the **StorSimple Update 1.2 Appliance Update** bundle.</span><span class="sxs-lookup"><span data-stu-id="08449-107">You will see the **StorSimple Update 1.2 Appliance Update** bundle.</span></span> <span data-ttu-id="08449-108">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="08449-108">Click **Add**.</span></span> <span data-ttu-id="08449-109">The update will be added to the basket.</span><span class="sxs-lookup"><span data-stu-id="08449-109">The update will be added to the basket.</span></span>
5. <span data-ttu-id="08449-110">Search for any additional hotfixes listed in the table above (**3043005** and **3063416**), and add each the basket.</span><span class="sxs-lookup"><span data-stu-id="08449-110">Search for any additional hotfixes listed in the table above (**3043005** and **3063416**), and add each the basket.</span></span>
6. <span data-ttu-id="08449-111">Click **View Basket**.</span><span class="sxs-lookup"><span data-stu-id="08449-111">Click **View Basket**.</span></span>
   
    ![View basket](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-update-option-1/HCS_InstallBasket-include.png)
7. <span data-ttu-id="08449-113">Click **Download**.</span><span class="sxs-lookup"><span data-stu-id="08449-113">Click **Download**.</span></span> <span data-ttu-id="08449-114">Specify or **Browse** to a local location where you want the downloads to appear.</span><span class="sxs-lookup"><span data-stu-id="08449-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="08449-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span><span class="sxs-lookup"><span data-stu-id="08449-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="08449-116">The folder can also be copied to a network share that is reachable from the device.</span><span class="sxs-lookup"><span data-stu-id="08449-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="08449-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span><span class="sxs-lookup"><span data-stu-id="08449-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="08449-118">To install and verify regular mode hotfixes</span><span class="sxs-lookup"><span data-stu-id="08449-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="08449-119">Perform the following steps to install and verify the regular-mode hotfixes.</span><span class="sxs-lookup"><span data-stu-id="08449-119">Perform the following steps to install and verify the regular-mode hotfixes.</span></span> <span data-ttu-id="08449-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="08449-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="08449-121">To install the software update, access the Windows PowerShell interface on your StorSimple device serial console.</span><span class="sxs-lookup"><span data-stu-id="08449-121">To install the software update, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="08449-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="08449-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="08449-123">At the command prompt, press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="08449-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="08449-124">Select **Option 1** to log on to the device with full access.</span><span class="sxs-lookup"><span data-stu-id="08449-124">Select **Option 1** to log on to the device with full access.</span></span>
3. <span data-ttu-id="08449-125">To install the update package, at the command prompt, type:</span><span class="sxs-lookup"><span data-stu-id="08449-125">To install the update package, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="08449-126">Use IP rather than DNS in share path in the above command.</span><span class="sxs-lookup"><span data-stu-id="08449-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="08449-127">The credential parameter is used only if you are accessing an authenticated share.</span><span class="sxs-lookup"><span data-stu-id="08449-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="08449-128">We recommend that you use the credential parameter to access shares.</span><span class="sxs-lookup"><span data-stu-id="08449-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="08449-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span><span class="sxs-lookup"><span data-stu-id="08449-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="08449-130">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="08449-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="08449-131">Type **Y** when prompted to confirm the hotfix installation.</span><span class="sxs-lookup"><span data-stu-id="08449-131">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="08449-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="08449-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="08449-133">The following sample output shows the update in progress.</span><span class="sxs-lookup"><span data-stu-id="08449-133">The following sample output shows the update in progress.</span></span> <span data-ttu-id="08449-134">The `RunInprogress` will be `True` when the update is in progress.</span><span class="sxs-lookup"><span data-stu-id="08449-134">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 9/02/2015 10:36:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="08449-135">The following sample output indicates that the update is finished.</span><span class="sxs-lookup"><span data-stu-id="08449-135">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="08449-136">The `RunInProgress` will be `False` when the update has completed.</span><span class="sxs-lookup"><span data-stu-id="08449-136">The `RunInProgress` will be `False` when the update has completed.</span></span>

    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 9/02/2015 10:56:13 PM
    LastUpdateTimestamp : 9/02/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="08449-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span><span class="sxs-lookup"><span data-stu-id="08449-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="08449-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span><span class="sxs-lookup"><span data-stu-id="08449-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="08449-139">If it is, then the hotfix has completed.</span><span class="sxs-lookup"><span data-stu-id="08449-139">If it is, then the hotfix has completed.</span></span>
   > 
   > 
6. <span data-ttu-id="08449-140">After the software update is complete, verify the system software versions.</span><span class="sxs-lookup"><span data-stu-id="08449-140">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="08449-141">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="08449-141">Type the following command:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="08449-142">You should see the following versions:</span><span class="sxs-lookup"><span data-stu-id="08449-142">You should see the following versions:</span></span>
   
   * <span data-ttu-id="08449-143">HcsSoftwareVersion: 6.3.9600.17584</span><span class="sxs-lookup"><span data-stu-id="08449-143">HcsSoftwareVersion: 6.3.9600.17584</span></span>
   * <span data-ttu-id="08449-144">CisAgentVersion: 1.0.9049.0</span><span class="sxs-lookup"><span data-stu-id="08449-144">CisAgentVersion: 1.0.9049.0</span></span>
   * <span data-ttu-id="08449-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="08449-145">MdsAgentVersion: 26.0.4696.1433</span></span>
     
     <span data-ttu-id="08449-146">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span><span class="sxs-lookup"><span data-stu-id="08449-146">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="08449-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span><span class="sxs-lookup"><span data-stu-id="08449-147">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
7. <span data-ttu-id="08449-148">Repeat steps 3-5 to install the remaining regular-mode hotfix (KB3043005).</span><span class="sxs-lookup"><span data-stu-id="08449-148">Repeat steps 3-5 to install the remaining regular-mode hotfix (KB3043005).</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="08449-149">To install and verify maintenance mode hotfixes</span><span class="sxs-lookup"><span data-stu-id="08449-149">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="08449-150">Use KB3063416 to install disk firmware updates.</span><span class="sxs-lookup"><span data-stu-id="08449-150">Use KB3063416 to install disk firmware updates.</span></span> <span data-ttu-id="08449-151">These are disruptive updates and take around 30-45 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="08449-151">These are disruptive updates and take around 30-45 minutes to complete.</span></span> <span data-ttu-id="08449-152">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span><span class="sxs-lookup"><span data-stu-id="08449-152">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="08449-153">To install the disk firmware updates, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="08449-153">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="08449-154">Place the device in Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="08449-154">Place the device in Maintenance mode.</span></span> <span data-ttu-id="08449-155">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="08449-155">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="08449-156">You will need to run this cmdlet on the device controller when connected through the device serial console.</span><span class="sxs-lookup"><span data-stu-id="08449-156">You will need to run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="08449-157">Type:</span><span class="sxs-lookup"><span data-stu-id="08449-157">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="08449-158">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="08449-158">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update1-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17584
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="08449-159">Both the controllers then restart into Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="08449-159">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="08449-160">To install the disk firmware update, type:</span><span class="sxs-lookup"><span data-stu-id="08449-160">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="08449-161">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="08449-161">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="08449-162">Monitor the install progress using `Get-HcsUpdateStatus` command.</span><span class="sxs-lookup"><span data-stu-id="08449-162">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="08449-163">The update is complete when the `RunInProgress` changes to `False`.</span><span class="sxs-lookup"><span data-stu-id="08449-163">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="08449-164">After the installation is complete, the controller on which the maintenance mode hotfix was installed will be rebooted.</span><span class="sxs-lookup"><span data-stu-id="08449-164">After the installation is complete, the controller on which the maintenance mode hotfix was installed will be rebooted.</span></span> <span data-ttu-id="08449-165">Log in as option 1 with full access and verify the disk firmware version.</span><span class="sxs-lookup"><span data-stu-id="08449-165">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="08449-166">Type:</span><span class="sxs-lookup"><span data-stu-id="08449-166">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="08449-167">The expected disk firmware versions are:</span><span class="sxs-lookup"><span data-stu-id="08449-167">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEE, KZ50, F6C2, VR08`
   
   <span data-ttu-id="08449-168">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span><span class="sxs-lookup"><span data-stu-id="08449-168">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="08449-169">You can then exit the maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="08449-169">You can then exit the maintenance mode.</span></span> <span data-ttu-id="08449-170">Type the following command for each device controller:</span><span class="sxs-lookup"><span data-stu-id="08449-170">Type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="08449-171">The controllers restart when you exit Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="08449-171">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="08449-172">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="08449-172">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="08449-173">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="08449-173">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>



