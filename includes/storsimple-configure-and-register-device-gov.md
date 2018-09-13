<!--author=SharS last changed: 02/22/16-->

### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="8e19d-101">To configure and register the device</span><span class="sxs-lookup"><span data-stu-id="8e19d-101">To configure and register the device</span></span>
1. <span data-ttu-id="8e19d-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span><span class="sxs-lookup"><span data-stu-id="8e19d-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="8e19d-103">See [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span><span class="sxs-lookup"><span data-stu-id="8e19d-103">See [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="8e19d-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span><span class="sxs-lookup"><span data-stu-id="8e19d-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>
2. <span data-ttu-id="8e19d-105">In the session that opens up, press Enter one time to get a command prompt.</span><span class="sxs-lookup"><span data-stu-id="8e19d-105">In the session that opens up, press Enter one time to get a command prompt.</span></span> 
3. <span data-ttu-id="8e19d-106">You will be prompted to choose the language that you would like to set for your device.</span><span class="sxs-lookup"><span data-stu-id="8e19d-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="8e19d-107">Specify the language, and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="8e19d-107">Specify the language, and then press Enter.</span></span> 
   
    ![StorSimple configure and register device 1](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="8e19d-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span><span class="sxs-lookup"><span data-stu-id="8e19d-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span></span> 
   
    ![StorSimple register device 2](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="8e19d-111">Perform the following steps to configure the minimum required network settings for your device.</span><span class="sxs-lookup"><span data-stu-id="8e19d-111">Perform the following steps to configure the minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="8e19d-112">These configuration steps need to be performed on the active controller of the device.</span><span class="sxs-lookup"><span data-stu-id="8e19d-112">These configuration steps need to be performed on the active controller of the device.</span></span> <span data-ttu-id="8e19d-113">The serial console menu indicates the controller state in the banner message.</span><span class="sxs-lookup"><span data-stu-id="8e19d-113">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="8e19d-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span><span class="sxs-lookup"><span data-stu-id="8e19d-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="8e19d-115">At the command prompt, type your password.</span><span class="sxs-lookup"><span data-stu-id="8e19d-115">At the command prompt, type your password.</span></span> <span data-ttu-id="8e19d-116">The default device password is **Password1**.</span><span class="sxs-lookup"><span data-stu-id="8e19d-116">The default device password is **Password1**.</span></span>
   2. <span data-ttu-id="8e19d-117">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="8e19d-117">Type the following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="8e19d-118">A setup wizard will appear to help you configure the network settings for the device.</span><span class="sxs-lookup"><span data-stu-id="8e19d-118">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="8e19d-119">Supply the following information:</span><span class="sxs-lookup"><span data-stu-id="8e19d-119">Supply the following information:</span></span> 
      
      * <span data-ttu-id="8e19d-120">IP address for DATA 0 network interface</span><span class="sxs-lookup"><span data-stu-id="8e19d-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="8e19d-121">Subnet mask</span><span class="sxs-lookup"><span data-stu-id="8e19d-121">Subnet mask</span></span>
      * <span data-ttu-id="8e19d-122">Gateway</span><span class="sxs-lookup"><span data-stu-id="8e19d-122">Gateway</span></span>
      * <span data-ttu-id="8e19d-123">IP address for Primary DNS server</span><span class="sxs-lookup"><span data-stu-id="8e19d-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="8e19d-124">IP address for Primary NTP server</span><span class="sxs-lookup"><span data-stu-id="8e19d-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="8e19d-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span><span class="sxs-lookup"><span data-stu-id="8e19d-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span></span> 
      > 
      > 
   4. <span data-ttu-id="8e19d-126">Optionally, configure your web proxy server.</span><span class="sxs-lookup"><span data-stu-id="8e19d-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="8e19d-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span><span class="sxs-lookup"><span data-stu-id="8e19d-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="8e19d-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="8e19d-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span> 
      > 
      > 
6. <span data-ttu-id="8e19d-129">Press Ctrl + C to exit the setup wizard.</span><span class="sxs-lookup"><span data-stu-id="8e19d-129">Press Ctrl + C to exit the setup wizard.</span></span>
7. <span data-ttu-id="8e19d-130">Install the updates as follows:</span><span class="sxs-lookup"><span data-stu-id="8e19d-130">Install the updates as follows:</span></span>
   
   1. <span data-ttu-id="8e19d-131">Use the following cmdlet to set IPs on both the controllers:</span><span class="sxs-lookup"><span data-stu-id="8e19d-131">Use the following cmdlet to set IPs on both the controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="8e19d-132">At the command prompt, run `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="8e19d-132">At the command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="8e19d-133">You should be notified that updates are available.</span><span class="sxs-lookup"><span data-stu-id="8e19d-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="8e19d-134">Run `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="8e19d-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="8e19d-135">You can run this command on any node.</span><span class="sxs-lookup"><span data-stu-id="8e19d-135">You can run this command on any node.</span></span> <span data-ttu-id="8e19d-136">Updates will be applied on the first controller, the controller will fail over, and then the updates will be applied on the other controller.</span><span class="sxs-lookup"><span data-stu-id="8e19d-136">Updates will be applied on the first controller, the controller will fail over, and then the updates will be applied on the other controller.</span></span>
      
      <span data-ttu-id="8e19d-137">You can monitor the progress of the update by running `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="8e19d-137">You can monitor the progress of the update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="8e19d-138">The following sample output shows the update in progress.</span><span class="sxs-lookup"><span data-stu-id="8e19d-138">The following sample output shows the update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   : 
      ````
      
      <span data-ttu-id="8e19d-139">The following sample output indicates that the update is finished.</span><span class="sxs-lookup"><span data-stu-id="8e19d-139">The following sample output indicates that the update is finished.</span></span>
      
      ````
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      
      ````
      
      <span data-ttu-id="8e19d-140">It may take up to 11 hours to apply all the updates, including the Windows Updates.</span><span class="sxs-lookup"><span data-stu-id="8e19d-140">It may take up to 11 hours to apply all the updates, including the Windows Updates.</span></span>

8. <span data-ttu-id="8e19d-141">After all the updates are successfully installed, run the following cmdlet to confirm that the software updates were applied correctly:</span><span class="sxs-lookup"><span data-stu-id="8e19d-141">After all the updates are successfully installed, run the following cmdlet to confirm that the software updates were applied correctly:</span></span>
   
     `Get-HcsSystem`
   
    <span data-ttu-id="8e19d-142">You should see the following versions:</span><span class="sxs-lookup"><span data-stu-id="8e19d-142">You should see the following versions:</span></span>
   
   * <span data-ttu-id="8e19d-143">HcsSoftwareVersion: 6.3.9600.17491</span><span class="sxs-lookup"><span data-stu-id="8e19d-143">HcsSoftwareVersion: 6.3.9600.17491</span></span>
   * <span data-ttu-id="8e19d-144">CisAgentVersion: 1.0.9037.0</span><span class="sxs-lookup"><span data-stu-id="8e19d-144">CisAgentVersion: 1.0.9037.0</span></span>
   * <span data-ttu-id="8e19d-145">MdsAgentVersion: 26.0.4696.1433</span><span class="sxs-lookup"><span data-stu-id="8e19d-145">MdsAgentVersion: 26.0.4696.1433</span></span>
9. <span data-ttu-id="8e19d-146">Run the following cmdlet to confirm that the firmware update was applied correctly:</span><span class="sxs-lookup"><span data-stu-id="8e19d-146">Run the following cmdlet to confirm that the firmware update was applied correctly:</span></span>
   
    <span data-ttu-id="8e19d-147">`Start-HcsFirmwareCheck`.</span><span class="sxs-lookup"><span data-stu-id="8e19d-147">`Start-HcsFirmwareCheck`.</span></span>
   
     <span data-ttu-id="8e19d-148">The firmware status should be **UpToDate**.</span><span class="sxs-lookup"><span data-stu-id="8e19d-148">The firmware status should be **UpToDate**.</span></span>
10. <span data-ttu-id="8e19d-149">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span><span class="sxs-lookup"><span data-stu-id="8e19d-149">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span></span> <span data-ttu-id="8e19d-150">This will restart both controllers.</span><span class="sxs-lookup"><span data-stu-id="8e19d-150">This will restart both controllers.</span></span> <span data-ttu-id="8e19d-151">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span><span class="sxs-lookup"><span data-stu-id="8e19d-151">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span></span>
    
     `Set-CloudPlatform -AzureGovt_US`
    
    <span data-ttu-id="8e19d-152">You will see a confirmation message.</span><span class="sxs-lookup"><span data-stu-id="8e19d-152">You will see a confirmation message.</span></span> <span data-ttu-id="8e19d-153">Accept the default (**Y**).</span><span class="sxs-lookup"><span data-stu-id="8e19d-153">Accept the default (**Y**).</span></span>
11. <span data-ttu-id="8e19d-154">Run the following cmdlet to resume setup:</span><span class="sxs-lookup"><span data-stu-id="8e19d-154">Run the following cmdlet to resume setup:</span></span>
    
     `Invoke-HcsSetupWizard`
    
     ![Resume setup wizard](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov/HCS_ResumeSetup-gov-include.png)
    
    <span data-ttu-id="8e19d-156">When you resume setup, the wizard will be the Update 1 version (which corresponds to version 17469).</span><span class="sxs-lookup"><span data-stu-id="8e19d-156">When you resume setup, the wizard will be the Update 1 version (which corresponds to version 17469).</span></span> 
12. <span data-ttu-id="8e19d-157">Accept the network settings.</span><span class="sxs-lookup"><span data-stu-id="8e19d-157">Accept the network settings.</span></span> <span data-ttu-id="8e19d-158">You will see a validation message after you accept each setting.</span><span class="sxs-lookup"><span data-stu-id="8e19d-158">You will see a validation message after you accept each setting.</span></span>
13. <span data-ttu-id="8e19d-159">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span><span class="sxs-lookup"><span data-stu-id="8e19d-159">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="8e19d-160">When prompted, provide a device administrator password.</span><span class="sxs-lookup"><span data-stu-id="8e19d-160">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="8e19d-161">A valid device administrator password must be between 8 and 15 characters.</span><span class="sxs-lookup"><span data-stu-id="8e19d-161">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="8e19d-162">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span><span class="sxs-lookup"><span data-stu-id="8e19d-162">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![StorSimple register device 5](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice5_gov-include.png)
14. <span data-ttu-id="8e19d-164">The final step in the setup wizard registers your device with the StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="8e19d-164">The final step in the setup wizard registers your device with the StorSimple Manager service.</span></span> <span data-ttu-id="8e19d-165">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="8e19d-165">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="8e19d-166">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span><span class="sxs-lookup"><span data-stu-id="8e19d-166">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="8e19d-167">You can press Ctrl + C at any time to exit the setup wizard.</span><span class="sxs-lookup"><span data-stu-id="8e19d-167">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="8e19d-168">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span><span class="sxs-lookup"><span data-stu-id="8e19d-168">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![StorSimple registration progress](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov/HCS_RegistrationProgress-gov-include.png)
15. <span data-ttu-id="8e19d-170">After the device is registered, a Service Data Encryption key will appear.</span><span class="sxs-lookup"><span data-stu-id="8e19d-170">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="8e19d-171">Copy this key and save it in a safe location.</span><span class="sxs-lookup"><span data-stu-id="8e19d-171">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="8e19d-172">**This key will be required with the service registration key to register additional devices with the StorSimple Manager service.**</span><span class="sxs-lookup"><span data-stu-id="8e19d-172">**This key will be required with the service registration key to register additional devices with the StorSimple Manager service.**</span></span> <span data-ttu-id="8e19d-173">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span><span class="sxs-lookup"><span data-stu-id="8e19d-173">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple register device 7](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="8e19d-175">To copy the text from the serial console window, simply select the text.</span><span class="sxs-lookup"><span data-stu-id="8e19d-175">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="8e19d-176">You should then be able to paste it in the clipboard or any text editor.</span><span class="sxs-lookup"><span data-stu-id="8e19d-176">You should then be able to paste it in the clipboard or any text editor.</span></span> 
    > 
    > <span data-ttu-id="8e19d-177">DO NOT use Ctrl + C to copy the service data encryption key.</span><span class="sxs-lookup"><span data-stu-id="8e19d-177">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="8e19d-178">Using Ctrl + C will cause you to exit the setup wizard.</span><span class="sxs-lookup"><span data-stu-id="8e19d-178">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="8e19d-179">As a result, the device administrator password will not be changed and the device will revert to the default password.</span><span class="sxs-lookup"><span data-stu-id="8e19d-179">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    > 
    > 
16. <span data-ttu-id="8e19d-180">Exit the serial console.</span><span class="sxs-lookup"><span data-stu-id="8e19d-180">Exit the serial console.</span></span>
17. <span data-ttu-id="8e19d-181">Return to the Azure Government Portal, and complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="8e19d-181">Return to the Azure Government Portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="8e19d-182">Double-click your StorSimple Manager service to access the **Quick Start** page.</span><span class="sxs-lookup"><span data-stu-id="8e19d-182">Double-click your StorSimple Manager service to access the **Quick Start** page.</span></span>
    2. <span data-ttu-id="8e19d-183">Click **View connected devices**.</span><span class="sxs-lookup"><span data-stu-id="8e19d-183">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="8e19d-184">On the **Devices** page, verify that the device has successfully connected to the service by looking up the status.</span><span class="sxs-lookup"><span data-stu-id="8e19d-184">On the **Devices** page, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="8e19d-185">The device status should be **Online**.</span><span class="sxs-lookup"><span data-stu-id="8e19d-185">The device status should be **Online**.</span></span>
       
        ![StorSimple Devices page](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov/HCS_DeviceOnline-gov-include.png) 
       
        <span data-ttu-id="8e19d-187">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span><span class="sxs-lookup"><span data-stu-id="8e19d-187">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span></span> 
       
        <span data-ttu-id="8e19d-188">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="8e19d-188">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span> 
       
        <span data-ttu-id="8e19d-189">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Manager service-to-device communication.</span><span class="sxs-lookup"><span data-stu-id="8e19d-189">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Manager service-to-device communication.</span></span>








