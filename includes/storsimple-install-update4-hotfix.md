<!--author=alkohli last changed: 02/10/17-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="f4b58-101">To download hotfixes</span><span class="sxs-lookup"><span data-stu-id="f4b58-101">To download hotfixes</span></span>

<span data-ttu-id="f4b58-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="f4b58-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="f4b58-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="f4b58-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="f4b58-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span><span class="sxs-lookup"><span data-stu-id="f4b58-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>

    ![Install catalog](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)

3. <span data-ttu-id="f4b58-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4011839**, and then click **Search**.</span><span class="sxs-lookup"><span data-stu-id="f4b58-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **4011839**, and then click **Search**.</span></span>
   
    <span data-ttu-id="f4b58-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="f4b58-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 4.0 for StorSimple 8000 Series**.</span></span>
   
    ![Search catalog](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="f4b58-109">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4b58-109">Click **Add**.</span></span> <span data-ttu-id="f4b58-110">The update is added to the basket.</span><span class="sxs-lookup"><span data-stu-id="f4b58-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="f4b58-111">Search for any additional hotfixes listed in the table above (**4011841**), and add each to the basket.</span><span class="sxs-lookup"><span data-stu-id="f4b58-111">Search for any additional hotfixes listed in the table above (**4011841**), and add each to the basket.</span></span>
6. <span data-ttu-id="f4b58-112">Click **View Basket**.</span><span class="sxs-lookup"><span data-stu-id="f4b58-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="f4b58-113">Click **Download**.</span><span class="sxs-lookup"><span data-stu-id="f4b58-113">Click **Download**.</span></span> <span data-ttu-id="f4b58-114">Specify or **Browse** to a local location where you want the downloads to appear.</span><span class="sxs-lookup"><span data-stu-id="f4b58-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="f4b58-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span><span class="sxs-lookup"><span data-stu-id="f4b58-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="f4b58-116">The folder can also be copied to a network share that is reachable from the device.</span><span class="sxs-lookup"><span data-stu-id="f4b58-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="f4b58-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer > controller.</span><span class="sxs-lookup"><span data-stu-id="f4b58-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer > controller.</span></span>
>
> <span data-ttu-id="f4b58-118">The hotfixes must be copied in 3 separate folders.</span><span class="sxs-lookup"><span data-stu-id="f4b58-118">The hotfixes must be copied in 3 separate folders.</span></span> <span data-ttu-id="f4b58-119">For example, the device software update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span><span class="sxs-lookup"><span data-stu-id="f4b58-119">For example, the device software update can be copied in _FirstOrderUpdate_ folder, all the other non-disruptive updates could be copied in the _SecondOrderUpdate_ folder, and maintenance mode updates copied in _ThirdOrderUpdate_ folder.</span></span>

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="f4b58-120">To install and verify regular mode hotfixes</span><span class="sxs-lookup"><span data-stu-id="f4b58-120">To install and verify regular mode hotfixes</span></span>

<span data-ttu-id="f4b58-121">Perform the following steps to install and verify regular-mode hotfixes.</span><span class="sxs-lookup"><span data-stu-id="f4b58-121">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="f4b58-122">If you already installed them using the Azure classic portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="f4b58-122">If you already installed them using the Azure classic portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="f4b58-123">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span><span class="sxs-lookup"><span data-stu-id="f4b58-123">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="f4b58-124">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="f4b58-124">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="f4b58-125">At the command prompt, press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="f4b58-125">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="f4b58-126">Select **Option 1** to log on to the device with full access.</span><span class="sxs-lookup"><span data-stu-id="f4b58-126">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="f4b58-127">We recommend that you install the hotfix on the passive controller first.</span><span class="sxs-lookup"><span data-stu-id="f4b58-127">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="f4b58-128">To install the hotfix, at the command prompt, type:</span><span class="sxs-lookup"><span data-stu-id="f4b58-128">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="f4b58-129">Use IP rather than DNS in share path in the above command.</span><span class="sxs-lookup"><span data-stu-id="f4b58-129">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="f4b58-130">The credential parameter is used only if you are accessing an authenticated share.</span><span class="sxs-lookup"><span data-stu-id="f4b58-130">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="f4b58-131">We recommend that you use the credential parameter to access shares.</span><span class="sxs-lookup"><span data-stu-id="f4b58-131">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="f4b58-132">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span><span class="sxs-lookup"><span data-stu-id="f4b58-132">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="f4b58-133">Supply the password when prompted.</span><span class="sxs-lookup"><span data-stu-id="f4b58-133">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="f4b58-134">A sample output for installing the first order updates is shown below.</span><span class="sxs-lookup"><span data-stu-id="f4b58-134">A sample output for installing the first order updates is shown below.</span></span> <span data-ttu-id="f4b58-135">For the first order update, you need to point to the specific file.</span><span class="sxs-lookup"><span data-stu-id="f4b58-135">For the first order update, you need to point to the specific file.</span></span>
   
        ````
        Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
        \FirstOrderUpdate\HcsSoftwareUpdate.exe -Credential contoso\John
   
        Confirm
   
        This operation starts the hotfix installation and could reboot one or
        both of the controllers. If the device is serving I/Os, these will not
        be disrupted. Are you sure you want to continue?
        [Y] Yes [N] No [?] Help (default is "Y"): Y
   
        ````
4. <span data-ttu-id="f4b58-136">Type **Y** when prompted to confirm the hotfix installation.</span><span class="sxs-lookup"><span data-stu-id="f4b58-136">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="f4b58-137">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f4b58-137">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="f4b58-138">The update will first complete on the passive controller.</span><span class="sxs-lookup"><span data-stu-id="f4b58-138">The update will first complete on the passive controller.</span></span> <span data-ttu-id="f4b58-139">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span><span class="sxs-lookup"><span data-stu-id="f4b58-139">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="f4b58-140">The update is complete when both the controllers are updated.</span><span class="sxs-lookup"><span data-stu-id="f4b58-140">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="f4b58-141">The following sample output shows the update in progress.</span><span class="sxs-lookup"><span data-stu-id="f4b58-141">The following sample output shows the update in progress.</span></span> <span data-ttu-id="f4b58-142">The `RunInprogress` will be `True` when the update is in progress.</span><span class="sxs-lookup"><span data-stu-id="f4b58-142">The `RunInprogress` will be `True` when the update is in progress.</span></span>

    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 02/03/2017 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="f4b58-143">The following sample output indicates that the update is finished.</span><span class="sxs-lookup"><span data-stu-id="f4b58-143">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="f4b58-144">The `RunInProgress` will be `False` when the update has completed.</span><span class="sxs-lookup"><span data-stu-id="f4b58-144">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 02/03/2017 9:15:55 AM
    LastUpdateTimestamp : 02/03/2017 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE] 
    > <span data-ttu-id="f4b58-145">Occasionally, the cmdlet reports `False` when the update is still in progress.</span><span class="sxs-lookup"><span data-stu-id="f4b58-145">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="f4b58-146">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span><span class="sxs-lookup"><span data-stu-id="f4b58-146">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="f4b58-147">If it is, then the hotfix has completed.</span><span class="sxs-lookup"><span data-stu-id="f4b58-147">If it is, then the hotfix has completed.</span></span>

1. <span data-ttu-id="f4b58-148">After the software update is complete, verify the system software versions.</span><span class="sxs-lookup"><span data-stu-id="f4b58-148">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="f4b58-149">Type:</span><span class="sxs-lookup"><span data-stu-id="f4b58-149">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="f4b58-150">You should see the following versions:</span><span class="sxs-lookup"><span data-stu-id="f4b58-150">You should see the following versions:</span></span>
   
   * `FriendlySoftwareVersion: StorSimple 8000 Series Update 4.0`
   *  `HcsSoftwareVersion: 6.3.9600.17820`
   
    <span data-ttu-id="f4b58-151">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span><span class="sxs-lookup"><span data-stu-id="f4b58-151">If the version number does not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="f4b58-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span><span class="sxs-lookup"><span data-stu-id="f4b58-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
    > [!IMPORTANT]
    > <span data-ttu-id="f4b58-153">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span><span class="sxs-lookup"><span data-stu-id="f4b58-153">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span></span>
     
7. <span data-ttu-id="f4b58-154">Repeat steps 3-5 to install the second order updates.</span><span class="sxs-lookup"><span data-stu-id="f4b58-154">Repeat steps 3-5 to install the second order updates.</span></span> <span data-ttu-id="f4b58-155">**For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located. The cmdlet will execute all the updates available in the folder.**</span><span class="sxs-lookup"><span data-stu-id="f4b58-155">**For second order updates, multiple updates can be installed by just running the `Start-HcsHotfix cmdlet` and pointing to the folder where second order updates are located. The cmdlet will execute all the updates available in the folder.**</span></span> <span data-ttu-id="f4b58-156">If an update is already installed, the update logic will detect that and not apply that update.</span><span class="sxs-lookup"><span data-stu-id="f4b58-156">If an update is already installed, the update logic will detect that and not apply that update.</span></span> <span data-ttu-id="f4b58-157">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="f4b58-157">After all the hotfixes are installed, use the `Get-HcsSystem` cmdlet.</span></span> <span data-ttu-id="f4b58-158">The versions should be:</span><span class="sxs-lookup"><span data-stu-id="f4b58-158">The versions should be:</span></span>

   * `CisAgentVersion:  1.0.9441.0`
   * `MdsAgentVersion: 35.2.2.0`
   * `Lsisas2Version: 2.0.78.00`


#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="f4b58-159">To install and verify maintenance mode hotfixes</span><span class="sxs-lookup"><span data-stu-id="f4b58-159">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="f4b58-160">Use KB4011837 to install disk firmware updates.</span><span class="sxs-lookup"><span data-stu-id="f4b58-160">Use KB4011837 to install disk firmware updates.</span></span> <span data-ttu-id="f4b58-161">These are disruptive updates and take around 30 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="f4b58-161">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="f4b58-162">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span><span class="sxs-lookup"><span data-stu-id="f4b58-162">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="f4b58-163">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span><span class="sxs-lookup"><span data-stu-id="f4b58-163">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="f4b58-164">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span><span class="sxs-lookup"><span data-stu-id="f4b58-164">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="f4b58-165">To install the disk firmware updates, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="f4b58-165">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="f4b58-166">Place the device in the maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="f4b58-166">Place the device in the maintenance mode.</span></span> <span data-ttu-id="f4b58-167">**Note that you should not use Windows PowerShell remoting when connecting to a device in maintenance mode. Instead run this cmdlet on the device controller when connected through the device serial console.**</span><span class="sxs-lookup"><span data-stu-id="f4b58-167">**Note that you should not use Windows PowerShell remoting when connecting to a device in maintenance mode. Instead run this cmdlet on the device controller when connected through the device serial console.**</span></span> <span data-ttu-id="f4b58-168">Type:</span><span class="sxs-lookup"><span data-stu-id="f4b58-168">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="f4b58-169">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="f4b58-169">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8600
        Name: Update4-8600-mystorsimple
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="f4b58-170">Both the controllers then restart into maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="f4b58-170">Both the controllers then restart into maintenance mode.</span></span>
2. <span data-ttu-id="f4b58-171">To install the disk firmware update, type:</span><span class="sxs-lookup"><span data-stu-id="f4b58-171">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="f4b58-172">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="f4b58-172">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\ThirdOrderUpdates\ -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="f4b58-173">Monitor the install progress using `Get-HcsUpdateStatus` command.</span><span class="sxs-lookup"><span data-stu-id="f4b58-173">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="f4b58-174">The update is complete when the `RunInProgress` changes to `False`.</span><span class="sxs-lookup"><span data-stu-id="f4b58-174">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="f4b58-175">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span><span class="sxs-lookup"><span data-stu-id="f4b58-175">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="f4b58-176">Log in as option 1 with full access and verify the disk firmware version.</span><span class="sxs-lookup"><span data-stu-id="f4b58-176">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="f4b58-177">Type:</span><span class="sxs-lookup"><span data-stu-id="f4b58-177">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="f4b58-178">The expected disk firmware versions are:</span><span class="sxs-lookup"><span data-stu-id="f4b58-178">The expected disk firmware versions are:</span></span>
   
   `XMGJ, XGEG, KZ50, F6C2, VR08, N002, 0106`
   
   <span data-ttu-id="f4b58-179">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="f4b58-179">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8600
       Name: Update4-8600-mystorsimple
       Software Version: 6.3.9600.17820
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
           ActiveBIOS:0.45.0010
              BackupBIOS:0.45.0006
              MainCPLD:17.0.000b
              ActiveBMCRoot:2.0.001F
              BackupBMCRoot:2.0.001F
              BMCBoot:2.0.0002
              LsiFirmware:20.00.04.00
              LsiBios:07.37.00.00
              Battery1Firmware:06.2C
              Battery2Firmware:06.2C
              DomFirmware:X231600
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0x9134777A
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x19
              CanisterVPDCRC:0x142F7DC2
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:1.00|1.05
              PCM1VPDStructure:0x05
              PCM1VPDCRC:0x41BEF99C
              PCM2Firmware:1.00|1.05
              PCM2VPDStructure:0x05
              PCM2VPDCRC:0x41BEF99C

           EbodFirmware
              CanisterFirmware:3.5.0.56
              CanisterBootloader:5.03
              CanisterConfigCRC:0xB23150F8
              CanisterVPDStructure:0x06
              CanisterGEMCPLD:0x14
              CanisterVPDCRC:0xBAA55828
              MidplaneVPDStructure:0x0C
              MidplaneVPDCRC:0xA6BD4F64
              MidplaneCPLD:0x10
              PCM1Firmware:3.11
              PCM1VPDStructure:0x03
              PCM1VPDCRC:0x6B58AD13
              PCM2Firmware:3.11
              PCM2VPDStructure:0x03
              PCM2VPDCRC:0x6B58AD13

           DisksFirmware
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              SmrtStor:TXA2D20800GA6XYR:KZ50
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
              WD:WD4001FYYG-01SL3:VR08
   
    <span data-ttu-id="f4b58-180">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span><span class="sxs-lookup"><span data-stu-id="f4b58-180">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="f4b58-181">You can then exit the maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="f4b58-181">You can then exit the maintenance mode.</span></span> <span data-ttu-id="f4b58-182">To do so, type the following command for each device controller:</span><span class="sxs-lookup"><span data-stu-id="f4b58-182">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`

5. <span data-ttu-id="f4b58-183">The controllers restart when you exit maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="f4b58-183">The controllers restart when you exit maintenance mode.</span></span> <span data-ttu-id="f4b58-184">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="f4b58-184">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="f4b58-185">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="f4b58-185">Note that the portal might not show that you installed the maintenance mode updates for 24 hours.</span></span>



