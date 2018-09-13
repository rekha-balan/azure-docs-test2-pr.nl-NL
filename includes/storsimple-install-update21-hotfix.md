<!--author=alkohli last changed: 05/19/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="11d66-101">To download hotfixes</span><span class="sxs-lookup"><span data-stu-id="11d66-101">To download hotfixes</span></span>
<span data-ttu-id="11d66-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="11d66-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="11d66-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="11d66-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="11d66-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span><span class="sxs-lookup"><span data-stu-id="11d66-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="11d66-105">![Install catalog](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="11d66-105">![Install catalog](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="11d66-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3179904**, and then click **Search**.</span><span class="sxs-lookup"><span data-stu-id="11d66-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3179904**, and then click **Search**.</span></span>
   
    <span data-ttu-id="11d66-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.2 for StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="11d66-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.2 for StorSimple 8000 Series**.</span></span>
   
    ![Search catalog](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="11d66-109">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="11d66-109">Click **Add**.</span></span> <span data-ttu-id="11d66-110">The update is added to the basket.</span><span class="sxs-lookup"><span data-stu-id="11d66-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="11d66-111">Search for any additional hotfixes listed in the table above (**3103616**, **3146621**), and add each to the basket.</span><span class="sxs-lookup"><span data-stu-id="11d66-111">Search for any additional hotfixes listed in the table above (**3103616**, **3146621**), and add each to the basket.</span></span>
6. <span data-ttu-id="11d66-112">Click **View Basket**.</span><span class="sxs-lookup"><span data-stu-id="11d66-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="11d66-113">Click **Download**.</span><span class="sxs-lookup"><span data-stu-id="11d66-113">Click **Download**.</span></span> <span data-ttu-id="11d66-114">Specify or **Browse** to a local location where you want the downloads to appear.</span><span class="sxs-lookup"><span data-stu-id="11d66-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="11d66-115">The updates are downloaded to the specified location and placed in a sub-folder with the same name as the update.</span><span class="sxs-lookup"><span data-stu-id="11d66-115">The updates are downloaded to the specified location and placed in a sub-folder with the same name as the update.</span></span> <span data-ttu-id="11d66-116">The folder can also be copied to a network share that is reachable from the device.</span><span class="sxs-lookup"><span data-stu-id="11d66-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="11d66-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span><span class="sxs-lookup"><span data-stu-id="11d66-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="11d66-118">To install and verify regular mode hotfixes</span><span class="sxs-lookup"><span data-stu-id="11d66-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="11d66-119">Perform the following steps to install and verify regular-mode hotfixes.</span><span class="sxs-lookup"><span data-stu-id="11d66-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="11d66-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="11d66-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="11d66-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span><span class="sxs-lookup"><span data-stu-id="11d66-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="11d66-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="11d66-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="11d66-123">At the command prompt, press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="11d66-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="11d66-124">Select **Option 1** to log on to the device with full access.</span><span class="sxs-lookup"><span data-stu-id="11d66-124">Select **Option 1** to log on to the device with full access.</span></span> <span data-ttu-id="11d66-125">We recommend that you install the hotfix on the passive controller first.</span><span class="sxs-lookup"><span data-stu-id="11d66-125">We recommend that you install the hotfix on the passive controller first.</span></span>
3. <span data-ttu-id="11d66-126">To install the hotfix, at the command prompt, type:</span><span class="sxs-lookup"><span data-stu-id="11d66-126">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="11d66-127">Use IP rather than DNS in share path in the above command.</span><span class="sxs-lookup"><span data-stu-id="11d66-127">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="11d66-128">The credential parameter is used only if you are accessing an authenticated share.</span><span class="sxs-lookup"><span data-stu-id="11d66-128">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="11d66-129">We recommend that you use the credential parameter to access shares.</span><span class="sxs-lookup"><span data-stu-id="11d66-129">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="11d66-130">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span><span class="sxs-lookup"><span data-stu-id="11d66-130">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="11d66-131">Supply the password when prompted.</span><span class="sxs-lookup"><span data-stu-id="11d66-131">Supply the password when prompted.</span></span>
   
    <span data-ttu-id="11d66-132">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="11d66-132">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```

4. <span data-ttu-id="11d66-133">Type **Y** when prompted to confirm the hotfix installation.</span><span class="sxs-lookup"><span data-stu-id="11d66-133">Type **Y** when prompted to confirm the hotfix installation.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="11d66-134">If installing Update 2.2, only install the binary file prefaced with 'all-hcsmdssoftwareudpate'.</span><span class="sxs-lookup"><span data-stu-id="11d66-134">If installing Update 2.2, only install the binary file prefaced with 'all-hcsmdssoftwareudpate'.</span></span> <span data-ttu-id="11d66-135">Do not install the Cis and the MDS agent update prefaced with all-cismdsagentupdatebundle.</span><span class="sxs-lookup"><span data-stu-id="11d66-135">Do not install the Cis and the MDS agent update prefaced with all-cismdsagentupdatebundle.</span></span> <span data-ttu-id="11d66-136">Failure to do so will result in an error.</span><span class="sxs-lookup"><span data-stu-id="11d66-136">Failure to do so will result in an error.</span></span> 

5. <span data-ttu-id="11d66-137">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="11d66-137">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span> <span data-ttu-id="11d66-138">The update will first complete on the passive controller.</span><span class="sxs-lookup"><span data-stu-id="11d66-138">The update will first complete on the passive controller.</span></span> <span data-ttu-id="11d66-139">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span><span class="sxs-lookup"><span data-stu-id="11d66-139">Once the passive controller is updated, there will be a failover and the update will then get applied on the other controller.</span></span> <span data-ttu-id="11d66-140">The update is complete when both the controllers are updated.</span><span class="sxs-lookup"><span data-stu-id="11d66-140">The update is complete when both the controllers are updated.</span></span>
   
    <span data-ttu-id="11d66-141">The following sample output shows the update in progress.</span><span class="sxs-lookup"><span data-stu-id="11d66-141">The following sample output shows the update in progress.</span></span> <span data-ttu-id="11d66-142">The `RunInprogress` will be `True` when the update is in progress.</span><span class="sxs-lookup"><span data-stu-id="11d66-142">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp :
    LastUpdateTimestamp : 5/5/2016 2:04:02 AM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="11d66-143">The following sample output indicates that the update is finished.</span><span class="sxs-lookup"><span data-stu-id="11d66-143">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="11d66-144">The `RunInProgress` will be `False` when the update has completed.</span><span class="sxs-lookup"><span data-stu-id="11d66-144">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : False
    LastHotfixTimestamp : 5/17/2016 9:15:55 AM
    LastUpdateTimestamp : 5/17/2016 9:06:07 AM
    Controller0Events   :
    Controller1Events   :
    ```

    > [!NOTE]
    > <span data-ttu-id="11d66-145">Occasionally, the cmdlet reports `False` when the update is still in progress.</span><span class="sxs-lookup"><span data-stu-id="11d66-145">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="11d66-146">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span><span class="sxs-lookup"><span data-stu-id="11d66-146">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="11d66-147">If it is, then the hotfix has completed.</span><span class="sxs-lookup"><span data-stu-id="11d66-147">If it is, then the hotfix has completed.</span></span>

1. <span data-ttu-id="11d66-148">After the software update is complete, verify the system software versions.</span><span class="sxs-lookup"><span data-stu-id="11d66-148">After the software update is complete, verify the system software versions.</span></span> <span data-ttu-id="11d66-149">Type:</span><span class="sxs-lookup"><span data-stu-id="11d66-149">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="11d66-150">You should see the following versions:</span><span class="sxs-lookup"><span data-stu-id="11d66-150">You should see the following versions:</span></span>
   
   * `HcsSoftwareVersion: 6.3.9600.17708`
   * `CisAgentVersion: 1.0.9299.0`
   * `MdsAgentVersion: 30.0.4698.16` 
     
     <span data-ttu-id="11d66-151">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span><span class="sxs-lookup"><span data-stu-id="11d66-151">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="11d66-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span><span class="sxs-lookup"><span data-stu-id="11d66-152">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
     
     > [!IMPORTANT]
     > <span data-ttu-id="11d66-153">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span><span class="sxs-lookup"><span data-stu-id="11d66-153">You must restart the active controller via the `Restart-HcsController` cmdlet before applying the remaining updates.</span></span> 
     > 
     > 
2. <span data-ttu-id="11d66-154">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span><span class="sxs-lookup"><span data-stu-id="11d66-154">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="11d66-155">The iSCSI update KB3146621</span><span class="sxs-lookup"><span data-stu-id="11d66-155">The iSCSI update KB3146621</span></span>
   * <span data-ttu-id="11d66-156">The WMI update KB3103616</span><span class="sxs-lookup"><span data-stu-id="11d66-156">The WMI update KB3103616</span></span>
3. <span data-ttu-id="11d66-157">Skip this step if you are updating from Update 2.</span><span class="sxs-lookup"><span data-stu-id="11d66-157">Skip this step if you are updating from Update 2.</span></span> <span data-ttu-id="11d66-158">If you are updating from a version prior to Update 2, you will also need to download:</span><span class="sxs-lookup"><span data-stu-id="11d66-158">If you are updating from a version prior to Update 2, you will also need to download:</span></span>

    - <span data-ttu-id="11d66-159">The LSI driver KB3121900</span><span class="sxs-lookup"><span data-stu-id="11d66-159">The LSI driver KB3121900</span></span>

    - <span data-ttu-id="11d66-160">The Spaceport update KB3090322</span><span class="sxs-lookup"><span data-stu-id="11d66-160">The Spaceport update KB3090322</span></span>

    - <span data-ttu-id="11d66-161">The Storport update KB3080728</span><span class="sxs-lookup"><span data-stu-id="11d66-161">The Storport update KB3080728</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="11d66-162">To install and verify maintenance mode hotfixes</span><span class="sxs-lookup"><span data-stu-id="11d66-162">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="11d66-163">Use KB3121899 to install disk firmware updates.</span><span class="sxs-lookup"><span data-stu-id="11d66-163">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="11d66-164">These are disruptive updates and take around 30 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="11d66-164">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="11d66-165">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span><span class="sxs-lookup"><span data-stu-id="11d66-165">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="11d66-166">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span><span class="sxs-lookup"><span data-stu-id="11d66-166">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="11d66-167">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span><span class="sxs-lookup"><span data-stu-id="11d66-167">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="11d66-168">To install the disk firmware updates, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="11d66-168">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="11d66-169">Place the device in the Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="11d66-169">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="11d66-170">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="11d66-170">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="11d66-171">Instead run this cmdlet on the device controller when connected through the device serial console.</span><span class="sxs-lookup"><span data-stu-id="11d66-171">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="11d66-172">Type:</span><span class="sxs-lookup"><span data-stu-id="11d66-172">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="11d66-173">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="11d66-173">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76673
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="11d66-174">Both the controllers then restart into Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="11d66-174">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="11d66-175">To install the disk firmware update, type:</span><span class="sxs-lookup"><span data-stu-id="11d66-175">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="11d66-176">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="11d66-176">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="11d66-177">Monitor the install progress using `Get-HcsUpdateStatus` command.</span><span class="sxs-lookup"><span data-stu-id="11d66-177">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="11d66-178">The update is complete when the `RunInProgress` changes to `False`.</span><span class="sxs-lookup"><span data-stu-id="11d66-178">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="11d66-179">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span><span class="sxs-lookup"><span data-stu-id="11d66-179">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="11d66-180">Log in as option 1 with full access and verify the disk firmware version.</span><span class="sxs-lookup"><span data-stu-id="11d66-180">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="11d66-181">Type:</span><span class="sxs-lookup"><span data-stu-id="11d66-181">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="11d66-182">The expected disk firmware versions are:</span><span class="sxs-lookup"><span data-stu-id="11d66-182">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="11d66-183">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="11d66-183">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17705
       Copyright (C) 2014 Microsoft Corporation. All rights reserved.
       You are connected to Controller1
       ---------------------------------------------------------------
   
       Controller1>Get-HcsFirmwareVersion
   
       Controller0 : TalladegaFirmware
         ActiveBIOS:0.45.0006
         BackupBIOS:0.45.0008
         MainCPLD:17.0.0005
         ActiveBMCRoot:2.0.000E
         BackupBMCRoot:2.0.000E
         BMCBoot:2.0.0001
         LsiFirmware:19.00.00.00
         LsiBios:07.37.00.00
         Battery1Firmware:06.29
         Battery2Firmware:06.29
         DomFirmware:X231600
         CanisterFirmware:3.5.0.32
         CanisterBootloader:5.03
         CanisterConfigCRC:0xD1B030A4
         CanisterVPDStructure:0x06
         CanisterGEMCPLD:0x17
         CanisterVPDCRC:0xEE3504B4
         MidplaneVPDStructure:0x0C
         MidplaneVPDCRC:0xA6BD4F64
         MidplaneCPLD:0x10
         PCM1Firmware:1.00|1.05
         PCM1VPDStructure:0x05
         PCM1VPDCRC:0x41BEF99C
         PCM2Firmware:1.00|1.05
         PCM2VPDStructure:0x05
         PCM2VPDCRC:0x41BEF99C
   
         DisksFirmware
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST400FM0073:XGEG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
         SEAGATE:ST4000NM0023:XMGG
   
    <span data-ttu-id="11d66-184">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span><span class="sxs-lookup"><span data-stu-id="11d66-184">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="11d66-185">You can then exit the maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="11d66-185">You can then exit the maintenance mode.</span></span> <span data-ttu-id="11d66-186">To do so, type the following command for each device controller:</span><span class="sxs-lookup"><span data-stu-id="11d66-186">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="11d66-187">The controllers restart when you exit Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="11d66-187">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="11d66-188">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="11d66-188">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="11d66-189">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="11d66-189">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>


