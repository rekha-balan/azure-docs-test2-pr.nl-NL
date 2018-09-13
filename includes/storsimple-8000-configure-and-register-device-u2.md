<!--author=alkohli last changed: 01/18/2017-->


#### <a name="to-configure-and-register-the-device"></a><span data-ttu-id="cdbae-101">To configure and register the device</span><span class="sxs-lookup"><span data-stu-id="cdbae-101">To configure and register the device</span></span>

1. <span data-ttu-id="cdbae-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span><span class="sxs-lookup"><span data-stu-id="cdbae-102">Access the Windows PowerShell interface on your StorSimple device serial console.</span></span> <span data-ttu-id="cdbae-103">See [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span><span class="sxs-lookup"><span data-stu-id="cdbae-103">See [Use PuTTY to connect to the device serial console](#use-putty-to-connect-to-the-device-serial-console) for instructions.</span></span> <span data-ttu-id="cdbae-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span><span class="sxs-lookup"><span data-stu-id="cdbae-104">**Be sure to follow the procedure exactly or you will not be able to access the console.**</span></span>

2. <span data-ttu-id="cdbae-105">In the session that opens up, press **Enter** one time to get a command prompt.</span><span class="sxs-lookup"><span data-stu-id="cdbae-105">In the session that opens up, press **Enter** one time to get a command prompt.</span></span>

3. <span data-ttu-id="cdbae-106">You will be prompted to choose the language that you would like to set for your device.</span><span class="sxs-lookup"><span data-stu-id="cdbae-106">You will be prompted to choose the language that you would like to set for your device.</span></span> <span data-ttu-id="cdbae-107">Specify the language, and then press **Enter**.</span><span class="sxs-lookup"><span data-stu-id="cdbae-107">Specify the language, and then press **Enter**.</span></span>

4. <span data-ttu-id="cdbae-108">In the serial console menu that is presented, choose option 1, **Log in with full access**.</span><span class="sxs-lookup"><span data-stu-id="cdbae-108">In the serial console menu that is presented, choose option 1, **Log in with full access**.</span></span>
     <span data-ttu-id="cdbae-109">Complete steps 5-12 to configure the minimum required network settings for your device.</span><span class="sxs-lookup"><span data-stu-id="cdbae-109">Complete steps 5-12 to configure the minimum required network settings for your device.</span></span> <span data-ttu-id="cdbae-110">**These configuration steps need to be performed on the active controller of the device.**</span><span class="sxs-lookup"><span data-stu-id="cdbae-110">**These configuration steps need to be performed on the active controller of the device.**</span></span> <span data-ttu-id="cdbae-111">The serial console menu indicates the controller state in the banner message.</span><span class="sxs-lookup"><span data-stu-id="cdbae-111">The serial console menu indicates the controller state in the banner message.</span></span> <span data-ttu-id="cdbae-112">If you are not connected to the active controller, disconnect and then connect to the active controller.</span><span class="sxs-lookup"><span data-stu-id="cdbae-112">If you are not connected to the active controller, disconnect and then connect to the active controller.</span></span>

5. <span data-ttu-id="cdbae-113">At the command prompt, type your password.</span><span class="sxs-lookup"><span data-stu-id="cdbae-113">At the command prompt, type your password.</span></span> <span data-ttu-id="cdbae-114">The default device password is **Password1**.</span><span class="sxs-lookup"><span data-stu-id="cdbae-114">The default device password is **Password1**.</span></span>

6. <span data-ttu-id="cdbae-115">Type the following command: `Invoke-HcsSetupWizard`.</span><span class="sxs-lookup"><span data-stu-id="cdbae-115">Type the following command: `Invoke-HcsSetupWizard`.</span></span>

7. <span data-ttu-id="cdbae-116">A setup wizard will appear to help you configure the network settings for the device.</span><span class="sxs-lookup"><span data-stu-id="cdbae-116">A setup wizard will appear to help you configure the network settings for the device.</span></span> <span data-ttu-id="cdbae-117">Supply the following information:</span><span class="sxs-lookup"><span data-stu-id="cdbae-117">Supply the following information:</span></span>
   
   * <span data-ttu-id="cdbae-118">IP address for the DATA 0 network interface</span><span class="sxs-lookup"><span data-stu-id="cdbae-118">IP address for the DATA 0 network interface</span></span>
   * <span data-ttu-id="cdbae-119">Subnet mask</span><span class="sxs-lookup"><span data-stu-id="cdbae-119">Subnet mask</span></span>
   * <span data-ttu-id="cdbae-120">Gateway</span><span class="sxs-lookup"><span data-stu-id="cdbae-120">Gateway</span></span>
   * <span data-ttu-id="cdbae-121">IP address for Primary DNS server</span><span class="sxs-lookup"><span data-stu-id="cdbae-121">IP address for Primary DNS server</span></span>

   <span data-ttu-id="cdbae-122">A sample output is presented below.</span><span class="sxs-lookup"><span data-stu-id="cdbae-122">A sample output is presented below.</span></span>

    ```
        ---------------------------------------------------------------
        Microsoft Azure StorSimple Appliance Model 8100
        Name: 8100-SHX0991003G44MT
        Software Version: 6.3.9600.17759
        Copyright (C) 2014 Microsoft Corporation. All rights reserved.
        You are connected to Controller0 - Active
        ---------------------------------------------------------------

        Your device needs to be registered with the Microsoft Azure StorSimple Manager service. Please run 'Invoke-HcsSetupWizard' to set up your device.

        Controller0>Invoke-HcsSetupWizard

        Which IP address family would you like to configure on interface Data0?
        [4] IPv4 [6] IPv6 [B] Both (Default is "4"): 4

        Data0 IPv4 address:10.111.111.00
        Data0 IPv4 subnet: 255.255.252.0
        Data0 IPv4 gateway: 10.111.111.11

        IPv4 primary DNS server [10.222.118.154]:10.222.222.111
    ```

    <br>
    <span data-ttu-id="cdbae-123">In the preceding sample output, you can see that the system is validating network settings after each step in the process.</span><span class="sxs-lookup"><span data-stu-id="cdbae-123">In the preceding sample output, you can see that the system is validating network settings after each step in the process.</span></span>

     > [!NOTE]
     > <span data-ttu-id="cdbae-124">You may have to wait for a few minutes for the subnet mask and the DNS settings to be applied.</span><span class="sxs-lookup"><span data-stu-id="cdbae-124">You may have to wait for a few minutes for the subnet mask and the DNS settings to be applied.</span></span> <span data-ttu-id="cdbae-125">If you get a "Check the network connectivity to Data 0" error message, check the physical network connection on the DATA 0 network interface of your active controller.</span><span class="sxs-lookup"><span data-stu-id="cdbae-125">If you get a "Check the network connectivity to Data 0" error message, check the physical network connection on the DATA 0 network interface of your active controller.</span></span>

8. <span data-ttu-id="cdbae-126">(Optional) configure your web proxy server.</span><span class="sxs-lookup"><span data-stu-id="cdbae-126">(Optional) configure your web proxy server.</span></span> <span data-ttu-id="cdbae-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span><span class="sxs-lookup"><span data-stu-id="cdbae-127">Although web proxy configuration is optional, **be aware that if you use a web proxy, you can only configure it here**.</span></span> <span data-ttu-id="cdbae-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span><span class="sxs-lookup"><span data-stu-id="cdbae-128">For more information, go to [Configure web proxy for your device](../articles/storsimple/storsimple-8000-configure-web-proxy.md).</span></span>
9. <span data-ttu-id="cdbae-129">Configure a Primary NTP server for your device.</span><span class="sxs-lookup"><span data-stu-id="cdbae-129">Configure a Primary NTP server for your device.</span></span> <span data-ttu-id="cdbae-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span><span class="sxs-lookup"><span data-stu-id="cdbae-130">NTP servers are required, as your device must synchronize time so that it can authenticate with your cloud service providers.</span></span> <span data-ttu-id="cdbae-131">Ensure that your network allows NTP traffic to pass from your datacenter to the Internet.</span><span class="sxs-lookup"><span data-stu-id="cdbae-131">Ensure that your network allows NTP traffic to pass from your datacenter to the Internet.</span></span> <span data-ttu-id="cdbae-132">If this is not possible, specify an internal NTP server.</span><span class="sxs-lookup"><span data-stu-id="cdbae-132">If this is not possible, specify an internal NTP server.</span></span>

    <span data-ttu-id="cdbae-133">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="cdbae-133">A sample output is shown below.</span></span>

    ```
        Would you like to configure a web proxy?
        [Y] Yes [N] No (Default is "N"):N

        Primary NTP server [time.windows.com]:time.windows.com

    ```

10. <span data-ttu-id="cdbae-134">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span><span class="sxs-lookup"><span data-stu-id="cdbae-134">For security reasons, the device administrator password expires after the first session, and you will need to change it now.</span></span> <span data-ttu-id="cdbae-135">When prompted, provide a device administrator password.</span><span class="sxs-lookup"><span data-stu-id="cdbae-135">When prompted, provide a device administrator password.</span></span> <span data-ttu-id="cdbae-136">A valid device administrator password must be between 8 and 15 characters.</span><span class="sxs-lookup"><span data-stu-id="cdbae-136">A valid device administrator password must be between 8 and 15 characters.</span></span> <span data-ttu-id="cdbae-137">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span><span class="sxs-lookup"><span data-stu-id="cdbae-137">The password must contain three of the following: lowercase, uppercase, numeric, and special characters.</span></span>

    ```
        The device administrator password must be between 8 and 15 characters. The password must contain a combination of uppercase letters, lowercase letters, numbers and special characters.
        Administrator Password:********
        Confirm Administrator Password:********
    ```
11. <span data-ttu-id="cdbae-138">The final step in the setup wizard registers your device with the StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="cdbae-138">The final step in the setup wizard registers your device with the StorSimple Device Manager service.</span></span> <span data-ttu-id="cdbae-139">For this, you will need the service registration key that you obtained in step 2.</span><span class="sxs-lookup"><span data-stu-id="cdbae-139">For this, you will need the service registration key that you obtained in step 2.</span></span> <span data-ttu-id="cdbae-140">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span><span class="sxs-lookup"><span data-stu-id="cdbae-140">After you supply the registration key, you may need to wait for 2-3 minutes before the device is registered.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="cdbae-141">You can press Ctrl + C at any time to exit the setup wizard.</span><span class="sxs-lookup"><span data-stu-id="cdbae-141">You can press Ctrl + C at any time to exit the setup wizard.</span></span> <span data-ttu-id="cdbae-142">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span><span class="sxs-lookup"><span data-stu-id="cdbae-142">If you have entered all the network settings (IP address for Data 0, Subnet mask, and Gateway), your entries will be retained.</span></span>
    
    <span data-ttu-id="cdbae-143">A sample output is shown below.</span><span class="sxs-lookup"><span data-stu-id="cdbae-143">A sample output is shown below.</span></span>

    ```
        The service registration key is available in the StorSimple Manager service.
        Enter service registration key:**************************************
        Device registration is in progress. Please wait.

    ```

12. <span data-ttu-id="cdbae-144">After the device is registered, a Service Data Encryption key will appear.</span><span class="sxs-lookup"><span data-stu-id="cdbae-144">After the device is registered, a Service Data Encryption key will appear.</span></span> <span data-ttu-id="cdbae-145">Copy this key and save it in a safe location.</span><span class="sxs-lookup"><span data-stu-id="cdbae-145">Copy this key and save it in a safe location.</span></span> <span data-ttu-id="cdbae-146">**This key will be required with the service registration key to register additional devices with the StorSimple Device Manager service.**</span><span class="sxs-lookup"><span data-stu-id="cdbae-146">**This key will be required with the service registration key to register additional devices with the StorSimple Device Manager service.**</span></span> <span data-ttu-id="cdbae-147">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span><span class="sxs-lookup"><span data-stu-id="cdbae-147">Refer to [StorSimple security](../articles/storsimple/storsimple-security.md) for more information about this key.</span></span>
    
    ![StorSimple register device 7](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup1.png)
    
    > [!NOTE]
    > <span data-ttu-id="cdbae-149">To copy the text from the serial console window, simply select the text.</span><span class="sxs-lookup"><span data-stu-id="cdbae-149">To copy the text from the serial console window, simply select the text.</span></span> <span data-ttu-id="cdbae-150">You should then be able to paste it in the clipboard or any text editor.</span><span class="sxs-lookup"><span data-stu-id="cdbae-150">You should then be able to paste it in the clipboard or any text editor.</span></span> <span data-ttu-id="cdbae-151">DO NOT use Ctrl + C to copy the service data encryption key.</span><span class="sxs-lookup"><span data-stu-id="cdbae-151">DO NOT use Ctrl + C to copy the service data encryption key.</span></span> <span data-ttu-id="cdbae-152">Using Ctrl + C will cause you to exit the setup wizard.</span><span class="sxs-lookup"><span data-stu-id="cdbae-152">Using Ctrl + C will cause you to exit the setup wizard.</span></span> <span data-ttu-id="cdbae-153">As a result, the device administrator password will not be changed and the device will revert to the default password.</span><span class="sxs-lookup"><span data-stu-id="cdbae-153">As a result, the device administrator password will not be changed and the device will revert to the default password.</span></span>
    
13. <span data-ttu-id="cdbae-154">Exit the serial console.</span><span class="sxs-lookup"><span data-stu-id="cdbae-154">Exit the serial console.</span></span>
14. <span data-ttu-id="cdbae-155">Return to the Azure portal, and complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="cdbae-155">Return to the Azure portal, and complete the following steps:</span></span>
    
    1. <span data-ttu-id="cdbae-156">Go to your StorSimple Device Manager service.</span><span class="sxs-lookup"><span data-stu-id="cdbae-156">Go to your StorSimple Device Manager service.</span></span>
    2. <span data-ttu-id="cdbae-157">Click **Devices**.</span><span class="sxs-lookup"><span data-stu-id="cdbae-157">Click **Devices**.</span></span>
    3. <span data-ttu-id="cdbae-158">In the tabular listing of devices, verify that the device has successfully connected to the service by looking up the status.</span><span class="sxs-lookup"><span data-stu-id="cdbae-158">In the tabular listing of devices, verify that the device has successfully connected to the service by looking up the status.</span></span> <span data-ttu-id="cdbae-159">The device status should be **Ready to set up**.</span><span class="sxs-lookup"><span data-stu-id="cdbae-159">The device status should be **Ready to set up**.</span></span>
       
        ![StorSimple Devices page](./media/storsimple-8000-configure-and-register-device-u2/step3pssetup2.png)
       
        <span data-ttu-id="cdbae-161">You may need to wait for a couple of minutes for the device status to change to **Ready to set up**.</span><span class="sxs-lookup"><span data-stu-id="cdbae-161">You may need to wait for a couple of minutes for the device status to change to **Ready to set up**.</span></span>
       
        <span data-ttu-id="cdbae-162">If the device does not show up in this list, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span><span class="sxs-lookup"><span data-stu-id="cdbae-162">If the device does not show up in this list, then you need to make sure that your firewall network was configured as described in [networking requirements for your StorSimple device](../articles/storsimple/storsimple-8000-system-requirements.md).</span></span> <span data-ttu-id="cdbae-163">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Device Manager service-to-device communication.</span><span class="sxs-lookup"><span data-stu-id="cdbae-163">Verify that port 9354 is open for outbound communication as this is used by the service bus for StorSimple Device Manager service-to-device communication.</span></span>

