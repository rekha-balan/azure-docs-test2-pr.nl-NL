<!--author=SharS last changed: 02/22/2016-->

### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="ccd81-101">To configure and register the device</span><span class="sxs-lookup"><span data-stu-id="ccd81-101">To configure and register the device</span></span>
1. <span data-ttu-id="ccd81-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span><span class="sxs-lookup"><span data-stu-id="ccd81-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="ccd81-103">See [Use PuTTY to connect to the device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span><span class="sxs-lookup"><span data-stu-id="ccd81-103">See [Use PuTTY to connect to the device serial console](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="ccd81-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span><span class="sxs-lookup"><span data-stu-id="ccd81-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>
2. <span data-ttu-id="ccd81-105">In the session that opens up, press Enter one time to get a command prompt.</span><span class="sxs-lookup"><span data-stu-id="ccd81-105">In the session that opens up, press Enter one time to get a command prompt.</span></span>
3. <span data-ttu-id="ccd81-106">You will be prompted to choose the language that you would like to set for your device.</span><span class="sxs-lookup"><span data-stu-id="ccd81-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="ccd81-107">Specify the language, and then press Enter.</span><span class="sxs-lookup"><span data-stu-id="ccd81-107">Specify the language, and then press Enter.</span></span>
   
    ![StorSimple configure and register device 1](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice1-gov-include.png)
4. <span data-ttu-id="ccd81-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span><span class="sxs-lookup"><span data-stu-id="ccd81-109">In the serial console menu that is presented, choose option 1 to log on with full access.</span></span>
   
    ![StorSimple register device 2](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice2-gov-include.png)
5. <span data-ttu-id="ccd81-111">Perform the following steps to configure the minimum required network settings for your device.</span><span class="sxs-lookup"><span data-stu-id="ccd81-111">Perform the following steps to configure the minimum required network settings for your device.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="ccd81-112">These configuration steps need to be performed on the active controller of the device.</span><span class="sxs-lookup"><span data-stu-id="ccd81-112">These configuration steps need to be performed on the active controller of the device.</span></span> <span data-ttu-id="ccd81-113">The serial console menu indicates the controller state in the banner message.</span><span class="sxs-lookup"><span data-stu-id="ccd81-113">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="ccd81-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span><span class="sxs-lookup"><span data-stu-id="ccd81-114">If you are not connect to the active controller, disconnect and then connect to the active controller.</span></span>
   > 
   > 
   
   1. <span data-ttu-id="ccd81-115">At the command prompt, type your password.</span><span class="sxs-lookup"><span data-stu-id="ccd81-115">At the command prompt, type your password.</span></span> <span data-ttu-id="ccd81-116">The default device password is **Password1**.</span><span class="sxs-lookup"><span data-stu-id="ccd81-116">The default device password is **Password1**.</span></span>
   2. <span data-ttu-id="ccd81-117">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="ccd81-117">Type the following command:</span></span>
      
        `Invoke-HcsSetupWizard`
   3. <span data-ttu-id="ccd81-118">A setup wizard will appear to help you configure the network settings for the device.</span><span class="sxs-lookup"><span data-stu-id="ccd81-118">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="ccd81-119">Supply the following information:</span><span class="sxs-lookup"><span data-stu-id="ccd81-119">Supply the following information:</span></span>
      
      * <span data-ttu-id="ccd81-120">IP address for DATA 0 network interface</span><span class="sxs-lookup"><span data-stu-id="ccd81-120">IP address for DATA 0 network interface</span></span>
      * <span data-ttu-id="ccd81-121">Subnet mask</span><span class="sxs-lookup"><span data-stu-id="ccd81-121">Subnet mask</span></span>
      * <span data-ttu-id="ccd81-122">Gateway</span><span class="sxs-lookup"><span data-stu-id="ccd81-122">Gateway</span></span>
      * <span data-ttu-id="ccd81-123">IP address for Primary DNS server</span><span class="sxs-lookup"><span data-stu-id="ccd81-123">IP address for Primary DNS server</span></span>
      * <span data-ttu-id="ccd81-124">IP address for Primary NTP server</span><span class="sxs-lookup"><span data-stu-id="ccd81-124">IP address for Primary NTP server</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="ccd81-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span><span class="sxs-lookup"><span data-stu-id="ccd81-125">You may have to wait for a few minutes for the subnet mask and DNS settings to be applied.</span></span>
      > 
      > 
   4. <span data-ttu-id="ccd81-126">Optionally, configure your web proxy server.</span><span class="sxs-lookup"><span data-stu-id="ccd81-126">Optionally, configure your web proxy server.</span></span>
      
      > [!IMPORTANT]
      > <span data-ttu-id="ccd81-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span><span class="sxs-lookup"><span data-stu-id="ccd81-127">Although web proxy configuration is optional, be aware that if you use a web proxy, you can only configure it here.</span></span> <span data-ttu-id="ccd81-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="ccd81-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-configure-web-proxy.md).</span></span>
      > 
      > 
6. <span data-ttu-id="ccd81-129">Press Ctrl + C to exit the setup wizard.</span><span class="sxs-lookup"><span data-stu-id="ccd81-129">Press Ctrl + C to exit the setup wizard.</span></span>
7. <span data-ttu-id="ccd81-130">Install the updates as follows:</span><span class="sxs-lookup"><span data-stu-id="ccd81-130">Install the updates as follows:</span></span>
   
   1. <span data-ttu-id="ccd81-131">Use the following cmdlet to set IPs on both the controllers:</span><span class="sxs-lookup"><span data-stu-id="ccd81-131">Use the following cmdlet to set IPs on both the controllers:</span></span>
      
      `Set-HcsNetInterface -InterfaceAlias Data0 -Controller0IPv4Address <Controller0 IP> -Controller1IPv4Address <Controller1 IP>`
   2. <span data-ttu-id="ccd81-132">At the command prompt, run `Get-HcsUpdateAvailability`.</span><span class="sxs-lookup"><span data-stu-id="ccd81-132">At the command prompt, run `Get-HcsUpdateAvailability`.</span></span> <span data-ttu-id="ccd81-133">You should be notified that updates are available.</span><span class="sxs-lookup"><span data-stu-id="ccd81-133">You should be notified that updates are available.</span></span>
   3. <span data-ttu-id="ccd81-134">Run `Start-HcsUpdate`.</span><span class="sxs-lookup"><span data-stu-id="ccd81-134">Run `Start-HcsUpdate`.</span></span> <span data-ttu-id="ccd81-135">You can run this command on any node.</span><span class="sxs-lookup"><span data-stu-id="ccd81-135">You can run this command on any node.</span></span> <span data-ttu-id="ccd81-136">Updates will be applied on the first controller, the controller will fail over, and then the updates will be applied on the other controller.</span><span class="sxs-lookup"><span data-stu-id="ccd81-136">Updates will be applied on the first controller, the controller will fail over, and then the updates will be applied on the other controller.</span></span>
      
      <span data-ttu-id="ccd81-137">You can monitor the progress of the update by running `Get-HcsUpdateStatus`.</span><span class="sxs-lookup"><span data-stu-id="ccd81-137">You can monitor the progress of the update by running `Get-HcsUpdateStatus`.</span></span>    
      
      <span data-ttu-id="ccd81-138">The following sample output shows the update in progress.</span><span class="sxs-lookup"><span data-stu-id="ccd81-138">The following sample output shows the update in progress.</span></span>
      
      ````
      Controller0>Get-HcsUpdateStatus
      RunInprogress       : True
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ````
      
      <span data-ttu-id="ccd81-139">The following sample output indicates that the update is finished.</span><span class="sxs-lookup"><span data-stu-id="ccd81-139">The following sample output indicates that the update is finished.</span></span>
      
      ```
      Controller1>Get-HcsUpdateStatus
      
      RunInprogress       : False
      LastHotfixTimestamp : 4/13/2015 10:56:13 PM
      LastUpdateTimestamp : 4/13/2015 10:35:25 PM
      Controller0Events   :
      Controller1Events   :
      ```
      
      <span data-ttu-id="ccd81-140">It may take up to 11 hours to apply all the updates, including the Windows Updates.</span><span class="sxs-lookup"><span data-stu-id="ccd81-140">It may take up to 11 hours to apply all the updates, including the Windows Updates.</span></span>
8. <span data-ttu-id="ccd81-141">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span><span class="sxs-lookup"><span data-stu-id="ccd81-141">Run the following cmdlet to point the device to the Microsoft Azure Government portal (because it points to the public Azure classic portal by default).</span></span> <span data-ttu-id="ccd81-142">This will restart both controllers.</span><span class="sxs-lookup"><span data-stu-id="ccd81-142">This will restart both controllers.</span></span> <span data-ttu-id="ccd81-143">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span><span class="sxs-lookup"><span data-stu-id="ccd81-143">We recommend that you use two PuTTY sessions to simultaneously connect to both controllers so that you can see when each controller is restarted.</span></span>
   
    `Set-CloudPlatform -AzureGovt_US`
   
   <span data-ttu-id="ccd81-144">You will see a confirmation message.</span><span class="sxs-lookup"><span data-stu-id="ccd81-144">You will see a confirmation message.</span></span> <span data-ttu-id="ccd81-145">Accept the default (**Y**).</span><span class="sxs-lookup"><span data-stu-id="ccd81-145">Accept the default (**Y**).</span></span>
9. <span data-ttu-id="ccd81-146">Run the following cmdlet to resume setup:</span><span class="sxs-lookup"><span data-stu-id="ccd81-146">Run the following cmdlet to resume setup:</span></span>
   
    `Invoke-HcsSetupWizard`
   
    ![Resume setup wizard](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov-u2/HCS_ResumeSetup-gov-include.png)
   
   <span data-ttu-id="ccd81-148">When you resume setup, the wizard will be the Update 2 version.</span><span class="sxs-lookup"><span data-stu-id="ccd81-148">When you resume setup, the wizard will be the Update 2 version.</span></span>
10. <span data-ttu-id="ccd81-149">Accept the network settings.</span><span class="sxs-lookup"><span data-stu-id="ccd81-149">Accept the network settings.</span></span> <span data-ttu-id="ccd81-150">You will see a validation message after you accept each setting.</span><span class="sxs-lookup"><span data-stu-id="ccd81-150">You will see a validation message after you accept each setting.</span></span>
11. <span data-ttu-id="ccd81-151">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span><span class="sxs-lookup"><span data-stu-id="ccd81-151">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="ccd81-152">When prompted, provide a device administrator password.</span><span class="sxs-lookup"><span data-stu-id="ccd81-152">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="ccd81-153">A valid device administrator password must be between 8 and 15 characters.</span><span class="sxs-lookup"><span data-stu-id="ccd81-153">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="ccd81-154">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span><span class="sxs-lookup"><span data-stu-id="ccd81-154">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>
    
    <br/>![StorSimple register device 5](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice5_gov-include.png)
12. <span data-ttu-id="ccd81-156">The final step in the setup wizard registers your device with the StorSimple Manager service.</span><span class="sxs-lookup"><span data-stu-id="ccd81-156">The final step in the setup wizard registers your device with the StorSimple Manager service.</span></span> <span data-ttu-id="ccd81-157">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span><span class="sxs-lookup"><span data-stu-id="ccd81-157">For this, you will need the service registration key that you obtained in [Step 2: Get the service registration key](../articles/storsimple/storsimple-deployment-walkthrough-gov-u2.md#step-2-get-the-service-registration-key).</span></span> <span data-ttu-id="ccd81-158">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span><span class="sxs-lookup"><span data-stu-id="ccd81-158">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="ccd81-159">You can press Ctrl + C at any time to exit the setup wizard.</span><span class="sxs-lookup"><span data-stu-id="ccd81-159">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="ccd81-160">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span><span class="sxs-lookup"><span data-stu-id="ccd81-160">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    > 
    > 
    
    ![StorSimple registration progress](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov-u2/HCS_RegistrationProgress-gov-include.png)
13. <span data-ttu-id="ccd81-162">After the device is registered, a Service Data Encryption key will appear.</span><span class="sxs-lookup"><span data-stu-id="ccd81-162">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="ccd81-163">Copy this key and save it in a safe location.</span><span class="sxs-lookup"><span data-stu-id="ccd81-163">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="ccd81-164">**This key will be required with the service registration key to register additional devices with the StorSimple Manager service.**</span><span class="sxs-lookup"><span data-stu-id="ccd81-164">**This key will be required with the service registration key to register additional devices with the StorSimple Manager service.**</span></span> <span data-ttu-id="ccd81-165">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span><span class="sxs-lookup"><span data-stu-id="ccd81-165">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple register device 7](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov-u2/HCS_RegisterYourDevice7_gov-include.png)    
    
    > [!IMPORTANT]
    > <span data-ttu-id="ccd81-167">To copy the text from the serial console window, simply select the text.</span><span class="sxs-lookup"><span data-stu-id="ccd81-167">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="ccd81-168">You should then be able to paste it in the clipboard or any text editor.</span><span class="sxs-lookup"><span data-stu-id="ccd81-168">You should then be able to paste it in the clipboard or any text editor.</span></span>
    > 
    > <span data-ttu-id="ccd81-169">DO NOT use Ctrl + C to copy the service data encryption key.</span><span class="sxs-lookup"><span data-stu-id="ccd81-169">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="ccd81-170">Using Ctrl + C will cause you to exit the setup wizard.</span><span class="sxs-lookup"><span data-stu-id="ccd81-170">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="ccd81-171">As a result, the device administrator password will not be changed and the device will revert to the default password.</span><span class="sxs-lookup"><span data-stu-id="ccd81-171">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    > 
    > 
14. <span data-ttu-id="ccd81-172">Exit the serial console.</span><span class="sxs-lookup"><span data-stu-id="ccd81-172">Exit the serial console.</span></span>
15. <span data-ttu-id="ccd81-173">Return to the Azure Government Portal, and complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="ccd81-173">Return to the Azure Government Portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="ccd81-174">Double-click your StorSimple Manager service to access the **Quick Start** page.</span><span class="sxs-lookup"><span data-stu-id="ccd81-174">Double-click your StorSimple Manager service to access the **Quick Start** page.</span></span>
    2. <span data-ttu-id="ccd81-175">Click **View connected devices**.</span><span class="sxs-lookup"><span data-stu-id="ccd81-175">Click **View connected devices**.</span></span>
    3. <span data-ttu-id="ccd81-176">On the **Devices** page, verify that the device has successfully connected to the service by looking up the status.</span><span class="sxs-lookup"><span data-stu-id="ccd81-176">On the **Devices** page, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="ccd81-177">The device status should be **Online**.</span><span class="sxs-lookup"><span data-stu-id="ccd81-177">The device status should be **Online**.</span></span>
       
        ![StorSimple Devices page](https://docstestmedia1.blob.core.windows.net/azure-media/includes/media/storsimple-configure-and-register-device-gov-u2/HCS_DeviceOnline-gov-include.png)
       
        <span data-ttu-id="ccd81-179">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span><span class="sxs-lookup"><span data-stu-id="ccd81-179">If the device status is **Offline**, wait for a couple of minutes for the device to come online.</span></span>
       
        <span data-ttu-id="ccd81-180">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="ccd81-180">If the device is still offline after a few minutes, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-system-requirements.md).</span></span>
       
        <span data-ttu-id="ccd81-181">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Manager Service-to-device communication.</span><span class="sxs-lookup"><span data-stu-id="ccd81-181">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Manager Service-to-device communication.</span></span>








