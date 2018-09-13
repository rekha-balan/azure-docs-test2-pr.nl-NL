<!--author=alkohli last changed: 03/17/16-->

#### <a name="to-download-hotfixes"></a><span data-ttu-id="99795-101">To download hotfixes</span><span class="sxs-lookup"><span data-stu-id="99795-101">To download hotfixes</span></span>
<span data-ttu-id="99795-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span><span class="sxs-lookup"><span data-stu-id="99795-102">Perform the following steps to download the software update from the Microsoft Update Catalog.</span></span>

1. <span data-ttu-id="99795-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="99795-103">Start Internet Explorer and navigate to [http://catalog.update.microsoft.com](http://catalog.update.microsoft.com).</span></span>
2. <span data-ttu-id="99795-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span><span class="sxs-lookup"><span data-stu-id="99795-104">If this is your first time using the Microsoft Update Catalog on this computer, click **Install** when prompted to install the Microsoft Update Catalog add-on.</span></span>
    <span data-ttu-id="99795-105">![Install catalog](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span><span class="sxs-lookup"><span data-stu-id="99795-105">![Install catalog](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-update2-hotfix/HCS_InstallCatalog-include.png)</span></span>
3. <span data-ttu-id="99795-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3121901**, and then click **Search**.</span><span class="sxs-lookup"><span data-stu-id="99795-106">In the search box of the Microsoft Update Catalog, enter the Knowledge Base (KB) number of the hotfix you want to download, for example **3121901**, and then click **Search**.</span></span>
   
    <span data-ttu-id="99795-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span><span class="sxs-lookup"><span data-stu-id="99795-107">The hotfix listing appears, for example, **Cumulative Software Bundle Update 2.0 for StorSimple 8000 Series**.</span></span>
   
    ![Search catalog](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-install-update2-hotfix/HCS_SearchCatalog1-include.png)
4. <span data-ttu-id="99795-109">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="99795-109">Click **Add**.</span></span> <span data-ttu-id="99795-110">The update is added to the basket.</span><span class="sxs-lookup"><span data-stu-id="99795-110">The update is added to the basket.</span></span>
5. <span data-ttu-id="99795-111">Search for any additional hotfixes listed in the table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each the basket.</span><span class="sxs-lookup"><span data-stu-id="99795-111">Search for any additional hotfixes listed in the table above (**3121900**, **3080728**, **3090322**, and **3121899**), and add each the basket.</span></span>
6. <span data-ttu-id="99795-112">Click **View Basket**.</span><span class="sxs-lookup"><span data-stu-id="99795-112">Click **View Basket**.</span></span>
7. <span data-ttu-id="99795-113">Click **Download**.</span><span class="sxs-lookup"><span data-stu-id="99795-113">Click **Download**.</span></span> <span data-ttu-id="99795-114">Specify or **Browse** to a local location where you want the downloads to appear.</span><span class="sxs-lookup"><span data-stu-id="99795-114">Specify or **Browse** to a local location where you want the downloads to appear.</span></span> <span data-ttu-id="99795-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span><span class="sxs-lookup"><span data-stu-id="99795-115">The updates are downloaded to the specified location and placed in a subfolder with the same name as the update.</span></span> <span data-ttu-id="99795-116">The folder can also be copied to a network share that is reachable from the device.</span><span class="sxs-lookup"><span data-stu-id="99795-116">The folder can also be copied to a network share that is reachable from the device.</span></span>

> [!NOTE]
> <span data-ttu-id="99795-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span><span class="sxs-lookup"><span data-stu-id="99795-117">The hotfixes must be accessible from both controllers to detect any potential error messages from the peer controller.</span></span>
> 
> 

#### <a name="to-install-and-verify-regular-mode-hotfixes"></a><span data-ttu-id="99795-118">To install and verify regular mode hotfixes</span><span class="sxs-lookup"><span data-stu-id="99795-118">To install and verify regular mode hotfixes</span></span>
<span data-ttu-id="99795-119">Perform the following steps to install and verify regular-mode hotfixes.</span><span class="sxs-lookup"><span data-stu-id="99795-119">Perform the following steps to install and verify regular-mode hotfixes.</span></span> <span data-ttu-id="99795-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span><span class="sxs-lookup"><span data-stu-id="99795-120">If you already installed them using the Azure Portal, skip ahead to [install and verify maintenance mode hotfixes](#to-install-and-verify-maintenance-mode-hotfixes).</span></span>

1. <span data-ttu-id="99795-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span><span class="sxs-lookup"><span data-stu-id="99795-121">To install the hotfixes, access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="99795-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="99795-122">Follow the detailed instructions in [Use PuTTy to connect to the serial console](../articles/storsimple/storsimple-deployment-walkthrough.md#use-putty-to-connect-to-the-device-serial-console).</span></span> <span data-ttu-id="99795-123">At the command prompt, press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="99795-123">At the command prompt, press **Enter**.</span></span>
2. <span data-ttu-id="99795-124">Select **Option 1** to log on to the device with full access.</span><span class="sxs-lookup"><span data-stu-id="99795-124">Select **Option 1** to log on to the device with full access.</span></span>
3. <span data-ttu-id="99795-125">To install the hotfix, at the command prompt, type:</span><span class="sxs-lookup"><span data-stu-id="99795-125">To install the hotfix, at the command prompt, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="99795-126">Use IP rather than DNS in share path in the above command.</span><span class="sxs-lookup"><span data-stu-id="99795-126">Use IP rather than DNS in share path in the above command.</span></span> <span data-ttu-id="99795-127">The credential parameter is used only if you are accessing an authenticated share.</span><span class="sxs-lookup"><span data-stu-id="99795-127">The credential parameter is used only if you are accessing an authenticated share.</span></span>
   
    <span data-ttu-id="99795-128">We recommend that you use the credential parameter to access shares.</span><span class="sxs-lookup"><span data-stu-id="99795-128">We recommend that you use the credential parameter to access shares.</span></span> <span data-ttu-id="99795-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span><span class="sxs-lookup"><span data-stu-id="99795-129">Even shares that are open to “everyone” are typically not open to unauthenticated users.</span></span>
   
    <span data-ttu-id="99795-130">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="99795-130">A sample output is shown below.</span></span>
   
    ```
    Controller0>Start-HcsHotfix -Path \\10.100.100.100\share
    \hcsmdssoftwareupdate.exe -Credential contoso\John

    Confirm

    This operation starts the hotfix installation and could reboot one or
    both of the controllers. If the device is serving I/Os, these will not
    be disrupted. Are you sure you want to continue?
    [Y] Yes [N] No [?] Help (default is "Y"): Y
    ```
4. <span data-ttu-id="99795-131">Type **Y** when prompted to confirm the hotfix installation.</span><span class="sxs-lookup"><span data-stu-id="99795-131">Type **Y** when prompted to confirm the hotfix installation.</span></span>
5. <span data-ttu-id="99795-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="99795-132">Monitor the update by using the `Get-HcsUpdateStatus` cmdlet.</span></span>
   
    <span data-ttu-id="99795-133">The following sample output shows the update in progress.</span><span class="sxs-lookup"><span data-stu-id="99795-133">The following sample output shows the update in progress.</span></span> <span data-ttu-id="99795-134">The `RunInprogress` will be `True` when the update is in progress.</span><span class="sxs-lookup"><span data-stu-id="99795-134">The `RunInprogress` will be `True` when the update is in progress.</span></span>
   
    ```
    Controller0>Get-HcsUpdateStatus
    RunInprogress       : True
    LastHotfixTimestamp : 12/21/2015 10:36:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
     <span data-ttu-id="99795-135">The following sample output indicates that the update is finished.</span><span class="sxs-lookup"><span data-stu-id="99795-135">The following sample output indicates that the update is finished.</span></span> <span data-ttu-id="99795-136">The `RunInProgress` will be `False` when the update has completed.</span><span class="sxs-lookup"><span data-stu-id="99795-136">The `RunInProgress` will be `False` when the update has completed.</span></span>
   
    ```
    Controller1>Get-HcsUpdateStatus

    RunInprogress       : False
    LastHotfixTimestamp : 12/21/2015 10:59:13 PM
    LastUpdateTimestamp : 12/21/2015 10:35:25 PM
    Controller0Events   :
    Controller1Events   :
    ```
   
   > [!NOTE]
   > <span data-ttu-id="99795-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span><span class="sxs-lookup"><span data-stu-id="99795-137">Occasionally, the cmdlet reports `False` when the update is still in progress.</span></span> <span data-ttu-id="99795-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span><span class="sxs-lookup"><span data-stu-id="99795-138">To ensure that the hotfix is complete, wait for a few minutes, rerun this command and verify that the `RunInProgress` is `False`.</span></span> <span data-ttu-id="99795-139">If it is, then the hotfix has completed.</span><span class="sxs-lookup"><span data-stu-id="99795-139">If it is, then the hotfix has completed.</span></span>

6. <span data-ttu-id="99795-140">After the software update is complete, repeat steps 3-5 to install and monitor the SaaS agent and MDS agent .</span><span class="sxs-lookup"><span data-stu-id="99795-140">After the software update is complete, repeat steps 3-5 to install and monitor the SaaS agent and MDS agent .</span></span> <span data-ttu-id="99795-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span><span class="sxs-lookup"><span data-stu-id="99795-141">Ensure that `all-hcsmdssoftwareupdate_0b438ddf0d5b686aada2378b754fac8c7f2160e9.exe` is installed before `all-cismdsagentupdatebundle_f98e62f4d56c79e2a6644d027af7a2393a93827a.exe`.</span></span>
7. <span data-ttu-id="99795-142">Verify the system software versions.</span><span class="sxs-lookup"><span data-stu-id="99795-142">Verify the system software versions.</span></span> <span data-ttu-id="99795-143">Type:</span><span class="sxs-lookup"><span data-stu-id="99795-143">Type:</span></span>
   
    `Get-HcsSystem`
   
    <span data-ttu-id="99795-144">You should see the following versions:</span><span class="sxs-lookup"><span data-stu-id="99795-144">You should see the following versions:</span></span>
   
   * <span data-ttu-id="99795-145">HcsSoftwareVersion: 6.3.9600.17673</span><span class="sxs-lookup"><span data-stu-id="99795-145">HcsSoftwareVersion: 6.3.9600.17673</span></span>
   * <span data-ttu-id="99795-146">CisAgentVersion: 1.0.9150.0</span><span class="sxs-lookup"><span data-stu-id="99795-146">CisAgentVersion: 1.0.9150.0</span></span>
   * <span data-ttu-id="99795-147">MdsAgentVersion: 30.0.4698.13</span><span class="sxs-lookup"><span data-stu-id="99795-147">MdsAgentVersion: 30.0.4698.13</span></span>
     
     <span data-ttu-id="99795-148">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span><span class="sxs-lookup"><span data-stu-id="99795-148">If the version numbers do not change after applying the update, it indicates that the hotfix has failed to apply.</span></span> <span data-ttu-id="99795-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span><span class="sxs-lookup"><span data-stu-id="99795-149">Should you see this, please contact [Microsoft Support](../articles/storsimple/storsimple-contact-microsoft-support.md) for further assistance.</span></span>
8. <span data-ttu-id="99795-150">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span><span class="sxs-lookup"><span data-stu-id="99795-150">Repeat steps 3-5 to install the remaining regular-mode hotfixes.</span></span>
   
   * <span data-ttu-id="99795-151">The LSI driver - KB3121900</span><span class="sxs-lookup"><span data-stu-id="99795-151">The LSI driver - KB3121900</span></span>
   * <span data-ttu-id="99795-152">The Storport update - KB3080728</span><span class="sxs-lookup"><span data-stu-id="99795-152">The Storport update - KB3080728</span></span>
   * <span data-ttu-id="99795-153">The Spaceport update - KB3090322</span><span class="sxs-lookup"><span data-stu-id="99795-153">The Spaceport update - KB3090322</span></span>

#### <a name="to-install-and-verify-maintenance-mode-hotfixes"></a><span data-ttu-id="99795-154">To install and verify maintenance mode hotfixes</span><span class="sxs-lookup"><span data-stu-id="99795-154">To install and verify maintenance mode hotfixes</span></span>
<span data-ttu-id="99795-155">Use KB3121899 to install disk firmware updates.</span><span class="sxs-lookup"><span data-stu-id="99795-155">Use KB3121899 to install disk firmware updates.</span></span> <span data-ttu-id="99795-156">These are disruptive updates and take around 30 minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="99795-156">These are disruptive updates and take around 30 minutes to complete.</span></span> <span data-ttu-id="99795-157">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span><span class="sxs-lookup"><span data-stu-id="99795-157">You can choose to install these in a planned maintenance window by connecting to the device serial console.</span></span>

<span data-ttu-id="99795-158">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span><span class="sxs-lookup"><span data-stu-id="99795-158">Note that if your disk firmware is already up-to-date, you won't need to install these updates.</span></span> <span data-ttu-id="99795-159">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span><span class="sxs-lookup"><span data-stu-id="99795-159">Run the `Get-HcsUpdateAvailability` cmdlet from the device serial console to check if updates are available and whether the updates are disruptive (maintenance mode) or non-disruptive (regular mode) updates.</span></span>

<span data-ttu-id="99795-160">To install the disk firmware updates, follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="99795-160">To install the disk firmware updates, follow the instructions below.</span></span>

1. <span data-ttu-id="99795-161">Place the device in the Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="99795-161">Place the device in the Maintenance mode.</span></span> <span data-ttu-id="99795-162">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="99795-162">Note that you should not use Windows PowerShell remoting when connecting to a device in Maintenance mode.</span></span> <span data-ttu-id="99795-163">Instead run this cmdlet on the device controller when connected through the device serial console.</span><span class="sxs-lookup"><span data-stu-id="99795-163">Instead run this cmdlet on the device controller when connected through the device serial console.</span></span> <span data-ttu-id="99795-164">Type:</span><span class="sxs-lookup"><span data-stu-id="99795-164">Type:</span></span>
   
    `Enter-HcsMaintenanceMode`
   
    <span data-ttu-id="99795-165">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="99795-165">A sample output is shown below.</span></span>
   
        Controller0>Enter-HcsMaintenanceMode
        Checking device state...
   
        In maintenance mode, your device will not service IOs and will be disconnected from the Microsoft Azure StorSimple Manager service. Entering maintenance mode will end the current session and reboot both controllers, which takes a few minutes to complete. Are you sure you want to enter maintenance mode?
        [Y] Yes [N] No (Default is "Y"): Y
   
        -----------------------MAINTENANCE MODE------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: Update2-8100-SHG0997879L76YD
        Software Version: 6.3.9600.17664
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Passive
        ---------------------------------------------------------------
   
        Serial Console Menu
        [1] Log in with full access
        [2] Log into peer controller with full access
        [3] Connect with limited access
        [4] Change language
        Please enter your choice>
   
    <span data-ttu-id="99795-166">Both the controllers then restart into Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="99795-166">Both the controllers then restart into Maintenance mode.</span></span>
2. <span data-ttu-id="99795-167">To install the disk firmware update, type:</span><span class="sxs-lookup"><span data-stu-id="99795-167">To install the disk firmware update, type:</span></span>
   
    `Start-HcsHotfix -Path <path to update file> -Credential <credentials in domain\username format>`
   
    <span data-ttu-id="99795-168">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="99795-168">A sample output is shown below.</span></span>
   
        Controller1>Start-HcsHotfix -Path \\10.100.100.100\share\DiskFirmwarePackage.exe -Credential contoso\john
        Enter Password:
        WARNING: In maintenance mode, hotfixes should be installed on each controller sequentially. After the hotfix is installed on this controller, install it on the peer controller.
        Confirm
        This operation starts a hotfix installation and could reboot one or both of the controllers. By installing new updates you agree to, and accept any additional terms associated with, the new functionality listed in the release notes (https://go.microsoft.com/fwLink/?LinkID=613790). Are you sure you want to continue?
        [Y] Yes [N] No (Default is "Y"): Y
        WARNING: Installation is currently in progress. This operation can take several minutes to complete.
3. <span data-ttu-id="99795-169">Monitor the install progress using `Get-HcsUpdateStatus` command.</span><span class="sxs-lookup"><span data-stu-id="99795-169">Monitor the install progress using `Get-HcsUpdateStatus` command.</span></span> <span data-ttu-id="99795-170">The update is complete when the `RunInProgress` changes to `False`.</span><span class="sxs-lookup"><span data-stu-id="99795-170">The update is complete when the `RunInProgress` changes to `False`.</span></span>
4. <span data-ttu-id="99795-171">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span><span class="sxs-lookup"><span data-stu-id="99795-171">After the installation is complete, the controller on which the maintenance mode hotfix was installed restarts.</span></span> <span data-ttu-id="99795-172">Log in as option 1 with full access and verify the disk firmware version.</span><span class="sxs-lookup"><span data-stu-id="99795-172">Log in as option 1 with full access and verify the disk firmware version.</span></span> <span data-ttu-id="99795-173">Type:</span><span class="sxs-lookup"><span data-stu-id="99795-173">Type:</span></span>
   
   `Get-HcsFirmwareVersion`
   
   <span data-ttu-id="99795-174">The expected disk firmware versions are:</span><span class="sxs-lookup"><span data-stu-id="99795-174">The expected disk firmware versions are:</span></span>
   
   `XMGG, XGEG, KZ50, F6C2, VR08`
   
   <span data-ttu-id="99795-175">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="99795-175">A sample output is shown below.</span></span>
   
       -----------------------MAINTENANCE MODE------------------------
       Microsoft Azure StorSimple Appliance Model 8100
       Name: Update2-8100-SHG0997879L76YD
       Software Version: 6.3.9600.17664
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
   
    <span data-ttu-id="99795-176">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span><span class="sxs-lookup"><span data-stu-id="99795-176">Run the `Get-HcsFirmwareVersion` command on the second controller to verify that the software version has been updated.</span></span> <span data-ttu-id="99795-177">You can then exit the maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="99795-177">You can then exit the maintenance mode.</span></span> <span data-ttu-id="99795-178">To do so, type the following command for each device controller:</span><span class="sxs-lookup"><span data-stu-id="99795-178">To do so, type the following command for each device controller:</span></span>
   
   `Exit-HcsMaintenanceMode`
5. <span data-ttu-id="99795-179">The controllers restart when you exit Maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="99795-179">The controllers restart when you exit Maintenance mode.</span></span> <span data-ttu-id="99795-180">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span><span class="sxs-lookup"><span data-stu-id="99795-180">After the disk firmware updates are successfully applied and the device has exited maintenance mode, return to the Azure classic portal.</span></span> <span data-ttu-id="99795-181">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="99795-181">Note that the portal might not show that you installed the Maintenance mode updates for 24 hours.</span></span>



