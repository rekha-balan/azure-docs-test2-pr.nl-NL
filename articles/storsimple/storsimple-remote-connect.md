---
title: Connect remotely to your StorSimple device | Microsoft Docs
description: Explains how to configure your device for remote management and how to connect to Windows PowerShell for StorSimple via HTTP or HTTPS.
services: storsimple
documentationcenter: ''
author: alkohli
manager: timlt
editor: ''
ms.assetid: 923377aa-f451-4656-87de-5e95a34a6a2a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/27/2017
ms.author: alkohli
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 674d006f17a95dbeb24949b7767b21c820c87090
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669850"
---
# <a name="connect-remotely-to-your-storsimple-8000-series-device"></a><span data-ttu-id="a3964-103">Connect remotely to your StorSimple 8000 series device</span><span class="sxs-lookup"><span data-stu-id="a3964-103">Connect remotely to your StorSimple 8000 series device</span></span>

## <a name="overview"></a><span data-ttu-id="a3964-104">Overview</span><span class="sxs-lookup"><span data-stu-id="a3964-104">Overview</span></span>
<span data-ttu-id="a3964-105">You can use Windows PowerShell remoting to connect to your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="a3964-105">You can use Windows PowerShell remoting to connect to your StorSimple device.</span></span> <span data-ttu-id="a3964-106">When you connect this way, you will not see a menu.</span><span class="sxs-lookup"><span data-stu-id="a3964-106">When you connect this way, you will not see a menu.</span></span> <span data-ttu-id="a3964-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span><span class="sxs-lookup"><span data-stu-id="a3964-107">(You see a menu only if you use the serial console on the device to connect.) With Windows PowerShell remoting, you connect to a specific runspace.</span></span> <span data-ttu-id="a3964-108">You can also specify the display language.</span><span class="sxs-lookup"><span data-stu-id="a3964-108">You can also specify the display language.</span></span> 

<span data-ttu-id="a3964-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a3964-109">For more information about using Windows PowerShell remoting to manage your device, go to [Use Windows PowerShell for StorSimple to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>

<span data-ttu-id="a3964-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a3964-110">This tutorial explains how to configure your device for remote management and then how to connect to Windows PowerShell for StorSimple.</span></span> <span data-ttu-id="a3964-111">You can use HTTP or HTTPS to connect via Windows PowerShell remoting.</span><span class="sxs-lookup"><span data-stu-id="a3964-111">You can use HTTP or HTTPS to connect via Windows PowerShell remoting.</span></span> <span data-ttu-id="a3964-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following:</span><span class="sxs-lookup"><span data-stu-id="a3964-112">However, when you are deciding how to connect to Windows PowerShell for StorSimple, consider the following:</span></span> 

* <span data-ttu-id="a3964-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span><span class="sxs-lookup"><span data-stu-id="a3964-113">Connecting directly to the device serial console is secure, but connecting to the serial console over network switches is not.</span></span> <span data-ttu-id="a3964-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span><span class="sxs-lookup"><span data-stu-id="a3964-114">Be cautious of the security risk when connecting to the device serial console over network switches.</span></span> 
* <span data-ttu-id="a3964-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span><span class="sxs-lookup"><span data-stu-id="a3964-115">Connecting through an HTTP session might offer more security than connecting through the serial console over the network.</span></span> <span data-ttu-id="a3964-116">Although this is not the most secure method, it is acceptable on trusted networks.</span><span class="sxs-lookup"><span data-stu-id="a3964-116">Although this is not the most secure method, it is acceptable on trusted networks.</span></span> 
* <span data-ttu-id="a3964-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span><span class="sxs-lookup"><span data-stu-id="a3964-117">Connecting through an HTTPS session with a self-signed certificate is the most secure and the recommended option.</span></span>

<span data-ttu-id="a3964-118">You can connect remotely to the Windows PowerShell interface.</span><span class="sxs-lookup"><span data-stu-id="a3964-118">You can connect remotely to the Windows PowerShell interface.</span></span> <span data-ttu-id="a3964-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span><span class="sxs-lookup"><span data-stu-id="a3964-119">However, remote access to your StorSimple device via the Windows PowerShell interface is not enabled by default.</span></span> <span data-ttu-id="a3964-120">You need to enable remote management on the device first, and then on the client that is used to access your device.</span><span class="sxs-lookup"><span data-stu-id="a3964-120">You need to enable remote management on the device first, and then on the client that is used to access your device.</span></span>

<span data-ttu-id="a3964-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="a3964-121">The steps described in this article were performed on a host system running Windows Server 2012 R2.</span></span>

## <a name="connect-through-http"></a><span data-ttu-id="a3964-122">Connect through HTTP</span><span class="sxs-lookup"><span data-stu-id="a3964-122">Connect through HTTP</span></span>
<span data-ttu-id="a3964-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="a3964-123">Connecting to Windows PowerShell for StorSimple through an HTTP session offers more security than connecting through the serial console of your StorSimple device.</span></span> <span data-ttu-id="a3964-124">Although this is not the most secure method, it is acceptable on trusted networks.</span><span class="sxs-lookup"><span data-stu-id="a3964-124">Although this is not the most secure method, it is acceptable on trusted networks.</span></span>

<span data-ttu-id="a3964-125">You can use either the Azure classic portal or the serial console to configure remote management.</span><span class="sxs-lookup"><span data-stu-id="a3964-125">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="a3964-126">Select from the following procedures:</span><span class="sxs-lookup"><span data-stu-id="a3964-126">Select from the following procedures:</span></span>

* [<span data-ttu-id="a3964-127">Use the Azure classic portal to enable remote management over HTTP</span><span class="sxs-lookup"><span data-stu-id="a3964-127">Use the Azure classic portal to enable remote management over HTTP</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-http)
* [<span data-ttu-id="a3964-128">Use the serial console to enable remote management over HTTP</span><span class="sxs-lookup"><span data-stu-id="a3964-128">Use the serial console to enable remote management over HTTP</span></span>](#use-the-serial-console-to-enable-remote-management-over-http)

<span data-ttu-id="a3964-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span><span class="sxs-lookup"><span data-stu-id="a3964-129">After you enable remote management, use the following procedure to prepare the client for a remote connection.</span></span>

* [<span data-ttu-id="a3964-130">Prepare the client for remote connection</span><span class="sxs-lookup"><span data-stu-id="a3964-130">Prepare the client for remote connection</span></span>](#prepare-the-client-for-remote-connection)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-http"></a><span data-ttu-id="a3964-131">Use the Azure classic portal to enable remote management over HTTP</span><span class="sxs-lookup"><span data-stu-id="a3964-131">Use the Azure classic portal to enable remote management over HTTP</span></span>
<span data-ttu-id="a3964-132">Perform the following steps in the Azure classic portal to enable remote management over HTTP.</span><span class="sxs-lookup"><span data-stu-id="a3964-132">Perform the following steps in the Azure classic portal to enable remote management over HTTP.</span></span>

#### <a name="to-enable-remote-management-through-the-azure-classic-portal"></a><span data-ttu-id="a3964-133">To enable remote management through the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="a3964-133">To enable remote management through the Azure classic portal</span></span>
1. <span data-ttu-id="a3964-134">Access **Devices** > **Configure** for your device.</span><span class="sxs-lookup"><span data-stu-id="a3964-134">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="a3964-135">Scroll down to the **Remote Management** section.</span><span class="sxs-lookup"><span data-stu-id="a3964-135">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="a3964-136">Set **Enable Remote Management** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="a3964-136">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="a3964-137">You can now choose to connect using HTTP.</span><span class="sxs-lookup"><span data-stu-id="a3964-137">You can now choose to connect using HTTP.</span></span> <span data-ttu-id="a3964-138">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span><span class="sxs-lookup"><span data-stu-id="a3964-138">(The default is to connect over HTTPS.) Make sure that HTTP is selected.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a3964-139">Connecting over HTTP is acceptable only on trusted networks.</span><span class="sxs-lookup"><span data-stu-id="a3964-139">Connecting over HTTP is acceptable only on trusted networks.</span></span>
   > 
   > 
5. <span data-ttu-id="a3964-140">Click **Save** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a3964-140">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-http"></a><span data-ttu-id="a3964-141">Use the serial console to enable remote management over HTTP</span><span class="sxs-lookup"><span data-stu-id="a3964-141">Use the serial console to enable remote management over HTTP</span></span>
<span data-ttu-id="a3964-142">Perform the following steps on the device serial console to enable remote management.</span><span class="sxs-lookup"><span data-stu-id="a3964-142">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="a3964-143">To enable remote management through the device serial console</span><span class="sxs-lookup"><span data-stu-id="a3964-143">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="a3964-144">On the serial console menu, select option 1.</span><span class="sxs-lookup"><span data-stu-id="a3964-144">On the serial console menu, select option 1.</span></span> <span data-ttu-id="a3964-145">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="a3964-145">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="a3964-146">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span><span class="sxs-lookup"><span data-stu-id="a3964-146">At the prompt, type: `Enable-HcsRemoteManagement –AllowHttp`</span></span>
3. <span data-ttu-id="a3964-147">You will be notified about the security vulnerabilities of using HTTP to connect to the device.</span><span class="sxs-lookup"><span data-stu-id="a3964-147">You will be notified about the security vulnerabilities of using HTTP to connect to the device.</span></span> <span data-ttu-id="a3964-148">When prompted, confirm by typing **Y**.</span><span class="sxs-lookup"><span data-stu-id="a3964-148">When prompted, confirm by typing **Y**.</span></span>
4. <span data-ttu-id="a3964-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span><span class="sxs-lookup"><span data-stu-id="a3964-149">Verify that HTTP is enabled by typing: `Get-HcsSystem`</span></span>
5. <span data-ttu-id="a3964-150">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span><span class="sxs-lookup"><span data-stu-id="a3964-150">Verify that the **RemoteManagementMode** field shows **HttpsAndHttpEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Serial HTTPS and HTTP enabled](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-remote-connect/HCS_SerialHttpsAndHttpEnabled.png)

### <a name="prepare-the-client-for-remote-connection"></a><span data-ttu-id="a3964-152">Prepare the client for remote connection</span><span class="sxs-lookup"><span data-stu-id="a3964-152">Prepare the client for remote connection</span></span>
<span data-ttu-id="a3964-153">Perform the following steps on the client to enable remote management.</span><span class="sxs-lookup"><span data-stu-id="a3964-153">Perform the following steps on the client to enable remote management.</span></span>

#### <a name="to-prepare-the-client-for-remote-connection"></a><span data-ttu-id="a3964-154">To prepare the client for remote connection</span><span class="sxs-lookup"><span data-stu-id="a3964-154">To prepare the client for remote connection</span></span>
1. <span data-ttu-id="a3964-155">Start a Windows PowerShell session as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a3964-155">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="a3964-156">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span><span class="sxs-lookup"><span data-stu-id="a3964-156">Type the following command to add the IP address of the StorSimple device to the client’s trusted hosts list:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
     <span data-ttu-id="a3964-157">Replace <*device_ip*> with the IP address of your device; for example:</span><span class="sxs-lookup"><span data-stu-id="a3964-157">Replace <*device_ip*> with the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="a3964-158">Type the following command to save the device credentials in a variable:</span><span class="sxs-lookup"><span data-stu-id="a3964-158">Type the following command to save the device credentials in a variable:</span></span> 
   
    ```
    $cred = Get-Credential
    ```
    
4. <span data-ttu-id="a3964-159">In the dialog box that appears:</span><span class="sxs-lookup"><span data-stu-id="a3964-159">In the dialog box that appears:</span></span>
   
   1. <span data-ttu-id="a3964-160">Type the user name in this format: *device_ip\SSAdmin*.</span><span class="sxs-lookup"><span data-stu-id="a3964-160">Type the user name in this format: *device_ip\SSAdmin*.</span></span>
   2. <span data-ttu-id="a3964-161">Type the device administrator password that was set when the device was configured with the setup wizard.</span><span class="sxs-lookup"><span data-stu-id="a3964-161">Type the device administrator password that was set when the device was configured with the setup wizard.</span></span> <span data-ttu-id="a3964-162">The default password is *Password1*.</span><span class="sxs-lookup"><span data-stu-id="a3964-162">The default password is *Password1*.</span></span>
5. <span data-ttu-id="a3964-163">Start a Windows PowerShell session on the device by typing this command:</span><span class="sxs-lookup"><span data-stu-id="a3964-163">Start a Windows PowerShell session on the device by typing this command:</span></span>
   
     `Enter-PSSession -Credential $cred -ConfigurationName SSAdminConsole -ComputerName <device_ip>`
   
   > [!NOTE]
   > <span data-ttu-id="a3964-164">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span><span class="sxs-lookup"><span data-stu-id="a3964-164">To create a Windows PowerShell session for use with the StorSimple virtual device, append the `–Port` parameter and specify the public port that you configured in Remoting for StorSimple Virtual Appliance.</span></span>
   > 
   > 
   
     <span data-ttu-id="a3964-165">At this point, you should have an active remote Windows PowerShell session to the device.</span><span class="sxs-lookup"><span data-stu-id="a3964-165">At this point, you should have an active remote Windows PowerShell session to the device.</span></span>
   
    ![PowerShell remoting using HTTP](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-remote-connect/HCS_PSRemotingUsingHTTP.png)

## <a name="connect-through-https"></a><span data-ttu-id="a3964-167">Connect through HTTPS</span><span class="sxs-lookup"><span data-stu-id="a3964-167">Connect through HTTPS</span></span>
<span data-ttu-id="a3964-168">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span><span class="sxs-lookup"><span data-stu-id="a3964-168">Connecting to Windows PowerShell for StorSimple through an HTTPS session is the most secure and recommended method of remotely connecting to your Microsoft Azure StorSimple device.</span></span> <span data-ttu-id="a3964-169">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span><span class="sxs-lookup"><span data-stu-id="a3964-169">The following procedures explain how to set up the serial console and client computers so that you can use HTTPS to connect to Windows PowerShell for StorSimple.</span></span>

<span data-ttu-id="a3964-170">You can use either the Azure classic portal or the serial console to configure remote management.</span><span class="sxs-lookup"><span data-stu-id="a3964-170">You can use either the Azure classic portal or the serial console to configure remote management.</span></span> <span data-ttu-id="a3964-171">Select from the following procedures:</span><span class="sxs-lookup"><span data-stu-id="a3964-171">Select from the following procedures:</span></span>

* [<span data-ttu-id="a3964-172">Use the Azure classic portal to enable remote management over HTTPS</span><span class="sxs-lookup"><span data-stu-id="a3964-172">Use the Azure classic portal to enable remote management over HTTPS</span></span>](#use-the-azure-classic-portal-to-enable-remote-management-over-https)
* [<span data-ttu-id="a3964-173">Use the serial console to enable remote management over HTTPS</span><span class="sxs-lookup"><span data-stu-id="a3964-173">Use the serial console to enable remote management over HTTPS</span></span>](#use-the-serial-console-to-enable-remote-management-over-https)

<span data-ttu-id="a3964-174">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span><span class="sxs-lookup"><span data-stu-id="a3964-174">After you enable remote management, use the following procedures to prepare the host for a remote management and connect to the device from the remote host.</span></span>

* [<span data-ttu-id="a3964-175">Prepare the host for remote management</span><span class="sxs-lookup"><span data-stu-id="a3964-175">Prepare the host for remote management</span></span>](#prepare-the-host-for-remote-management)
* [<span data-ttu-id="a3964-176">Connect to the device from the remote host</span><span class="sxs-lookup"><span data-stu-id="a3964-176">Connect to the device from the remote host</span></span>](#connect-to-the-device-from-the-remote-host)

### <a name="use-the-azure-classic-portal-to-enable-remote-management-over-https"></a><span data-ttu-id="a3964-177">Use the Azure classic portal to enable remote management over HTTPS</span><span class="sxs-lookup"><span data-stu-id="a3964-177">Use the Azure classic portal to enable remote management over HTTPS</span></span>
<span data-ttu-id="a3964-178">Perform the following steps in the Azure classic portal to enable remote management over HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a3964-178">Perform the following steps in the Azure classic portal to enable remote management over HTTPS.</span></span>

#### <a name="to-enable-remote-management-over-https-from-the-azure-classic-portal"></a><span data-ttu-id="a3964-179">To enable remote management over HTTPS from the Azure classic portal</span><span class="sxs-lookup"><span data-stu-id="a3964-179">To enable remote management over HTTPS from the Azure classic portal</span></span>
1. <span data-ttu-id="a3964-180">Access **Devices** > **Configure** for your device.</span><span class="sxs-lookup"><span data-stu-id="a3964-180">Access **Devices** > **Configure** for your device.</span></span>
2. <span data-ttu-id="a3964-181">Scroll down to the **Remote Management** section.</span><span class="sxs-lookup"><span data-stu-id="a3964-181">Scroll down to the **Remote Management** section.</span></span>
3. <span data-ttu-id="a3964-182">Set **Enable Remote Management** to **Yes**.</span><span class="sxs-lookup"><span data-stu-id="a3964-182">Set **Enable Remote Management** to **Yes**.</span></span>
4. <span data-ttu-id="a3964-183">You can now choose to connect using HTTPS.</span><span class="sxs-lookup"><span data-stu-id="a3964-183">You can now choose to connect using HTTPS.</span></span> <span data-ttu-id="a3964-184">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span><span class="sxs-lookup"><span data-stu-id="a3964-184">(The default is to connect over HTTPS.) Make sure that HTTPS is selected.</span></span> 
5. <span data-ttu-id="a3964-185">Click **Download Remote Management Certificate**.</span><span class="sxs-lookup"><span data-stu-id="a3964-185">Click **Download Remote Management Certificate**.</span></span> <span data-ttu-id="a3964-186">Specify a location to save this file.</span><span class="sxs-lookup"><span data-stu-id="a3964-186">Specify a location to save this file.</span></span> <span data-ttu-id="a3964-187">You will need to install this certificate on the client or host computer that you will use to connect to the device.</span><span class="sxs-lookup"><span data-stu-id="a3964-187">You will need to install this certificate on the client or host computer that you will use to connect to the device.</span></span>
6. <span data-ttu-id="a3964-188">Click **Save** at the bottom of the page.</span><span class="sxs-lookup"><span data-stu-id="a3964-188">Click **Save** at the bottom of the page.</span></span>

### <a name="use-the-serial-console-to-enable-remote-management-over-https"></a><span data-ttu-id="a3964-189">Use the serial console to enable remote management over HTTPS</span><span class="sxs-lookup"><span data-stu-id="a3964-189">Use the serial console to enable remote management over HTTPS</span></span>
<span data-ttu-id="a3964-190">Perform the following steps on the device serial console to enable remote management.</span><span class="sxs-lookup"><span data-stu-id="a3964-190">Perform the following steps on the device serial console to enable remote management.</span></span>

#### <a name="to-enable-remote-management-through-the-device-serial-console"></a><span data-ttu-id="a3964-191">To enable remote management through the device serial console</span><span class="sxs-lookup"><span data-stu-id="a3964-191">To enable remote management through the device serial console</span></span>
1. <span data-ttu-id="a3964-192">On the serial console menu, select option 1.</span><span class="sxs-lookup"><span data-stu-id="a3964-192">On the serial console menu, select option 1.</span></span> <span data-ttu-id="a3964-193">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span><span class="sxs-lookup"><span data-stu-id="a3964-193">For more information about using the serial console on the device, go to [Connect to Windows PowerShell for StorSimple via device serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console).</span></span>
2. <span data-ttu-id="a3964-194">At the prompt, type:</span><span class="sxs-lookup"><span data-stu-id="a3964-194">At the prompt, type:</span></span> 
   
     `Enable-HcsRemoteManagement`
   
    <span data-ttu-id="a3964-195">This should enable HTTPS on your device.</span><span class="sxs-lookup"><span data-stu-id="a3964-195">This should enable HTTPS on your device.</span></span>
3. <span data-ttu-id="a3964-196">Verify that HTTPS has been enabled by typing:</span><span class="sxs-lookup"><span data-stu-id="a3964-196">Verify that HTTPS has been enabled by typing:</span></span> 
   
     `Get-HcsSystem`
   
    <span data-ttu-id="a3964-197">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span><span class="sxs-lookup"><span data-stu-id="a3964-197">Make sure that the **RemoteManagementMode** field shows **HttpsEnabled**.The following illustration shows these settings in PuTTY.</span></span>
   
     ![Serial HTTPS enabled](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-remote-connect/HCS_SerialHttpsEnabled.png)
4. <span data-ttu-id="a3964-199">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span><span class="sxs-lookup"><span data-stu-id="a3964-199">From the output of `Get-HcsSystem`, copy the serial number of the device and save it for later use.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a3964-200">The serial number maps to the CN name in the certificate.</span><span class="sxs-lookup"><span data-stu-id="a3964-200">The serial number maps to the CN name in the certificate.</span></span>
   > 
   > 
5. <span data-ttu-id="a3964-201">Obtain a remote management certificate by typing:</span><span class="sxs-lookup"><span data-stu-id="a3964-201">Obtain a remote management certificate by typing:</span></span> 
   
     `Get-HcsRemoteManagementCert`
   
    <span data-ttu-id="a3964-202">A certificate similar to the following will appear.</span><span class="sxs-lookup"><span data-stu-id="a3964-202">A certificate similar to the following will appear.</span></span>
   
    ![Get remote management certificate](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-remote-connect/HCS_GetRemoteManagementCertificate.png)
6. <span data-ttu-id="a3964-204">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span><span class="sxs-lookup"><span data-stu-id="a3964-204">Copy the information in the certificate from **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** into a text editor such as Notepad, and save it as a .cer file.</span></span> <span data-ttu-id="a3964-205">(You will copy this file to your remote host when you prepare the host.)</span><span class="sxs-lookup"><span data-stu-id="a3964-205">(You will copy this file to your remote host when you prepare the host.)</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a3964-206">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span><span class="sxs-lookup"><span data-stu-id="a3964-206">To generate a new certificate, use the `Set-HcsRemoteManagementCert` cmdlet.</span></span>
   > 
   > 

### <a name="prepare-the-host-for-remote-management"></a><span data-ttu-id="a3964-207">Prepare the host for remote management</span><span class="sxs-lookup"><span data-stu-id="a3964-207">Prepare the host for remote management</span></span>
<span data-ttu-id="a3964-208">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span><span class="sxs-lookup"><span data-stu-id="a3964-208">To prepare the host computer for a remote connection that uses an HTTPS session, perform the following procedures:</span></span>

* <span data-ttu-id="a3964-209">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="a3964-209">[Import the .cer file into the root store of the client or remote host](#to-import-the-certificate-on-the-remote-host).</span></span>
* <span data-ttu-id="a3964-210">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span><span class="sxs-lookup"><span data-stu-id="a3964-210">[Add the device serial numbers to the hosts file on your remote host](#to-add-device-serial-numbers-to-the-remote-host).</span></span>

<span data-ttu-id="a3964-211">Each of these procedures is described below.</span><span class="sxs-lookup"><span data-stu-id="a3964-211">Each of these procedures is described below.</span></span>

#### <a name="to-import-the-certificate-on-the-remote-host"></a><span data-ttu-id="a3964-212">To import the certificate on the remote host</span><span class="sxs-lookup"><span data-stu-id="a3964-212">To import the certificate on the remote host</span></span>
1. <span data-ttu-id="a3964-213">Right-click the .cer file and select **Install certificate**.</span><span class="sxs-lookup"><span data-stu-id="a3964-213">Right-click the .cer file and select **Install certificate**.</span></span> <span data-ttu-id="a3964-214">This will start the Certificate Import Wizard.</span><span class="sxs-lookup"><span data-stu-id="a3964-214">This will start the Certificate Import Wizard.</span></span>
   
    ![Certificate Import Wizard 1](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-remote-connect/HCS_CertificateImportWizard1.png)
2. <span data-ttu-id="a3964-216">For **Store location**, select **Local Machine**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3964-216">For **Store location**, select **Local Machine**, and then click **Next**.</span></span>
3. <span data-ttu-id="a3964-217">Select **Place all certificates in the following store**, and then click **Browse**.</span><span class="sxs-lookup"><span data-stu-id="a3964-217">Select **Place all certificates in the following store**, and then click **Browse**.</span></span> <span data-ttu-id="a3964-218">Navigate to the root store of your remote host, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="a3964-218">Navigate to the root store of your remote host, and then click **Next**.</span></span>
   
    ![Certificate Import Wizard 2](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-remote-connect/HCS_CertificateImportWizard2.png)
4. <span data-ttu-id="a3964-220">Click **Finish**.</span><span class="sxs-lookup"><span data-stu-id="a3964-220">Click **Finish**.</span></span> <span data-ttu-id="a3964-221">A message that tells you that the import was successful appears.</span><span class="sxs-lookup"><span data-stu-id="a3964-221">A message that tells you that the import was successful appears.</span></span>
   
    ![Certificate Import Wizard 3](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-remote-connect/HCS_CertificateImportWizard3.png)

#### <a name="to-add-device-serial-numbers-to-the-remote-host"></a><span data-ttu-id="a3964-223">To add device serial numbers to the remote host</span><span class="sxs-lookup"><span data-stu-id="a3964-223">To add device serial numbers to the remote host</span></span>
1. <span data-ttu-id="a3964-224">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span><span class="sxs-lookup"><span data-stu-id="a3964-224">Start Notepad as an administrator, and then open the hosts file located at \Windows\System32\Drivers\etc.</span></span>
2. <span data-ttu-id="a3964-225">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span><span class="sxs-lookup"><span data-stu-id="a3964-225">Add the following three entries to your hosts file: **DATA 0 IP address**, **Controller 0 Fixed IP address**, and **Controller 1 Fixed IP address**.</span></span>
3. <span data-ttu-id="a3964-226">Enter the device serial number that you saved earlier.</span><span class="sxs-lookup"><span data-stu-id="a3964-226">Enter the device serial number that you saved earlier.</span></span> <span data-ttu-id="a3964-227">Map this to the IP address as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="a3964-227">Map this to the IP address as shown in the following image.</span></span> <span data-ttu-id="a3964-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span><span class="sxs-lookup"><span data-stu-id="a3964-228">For Controller 0 and Controller 1, append **Controller0** and **Controller1** at the end of the serial number (CN name).</span></span>
   
    ![Adding CN Name to hosts file](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-remote-connect/HCS_AddingCNNameToHostsFile.png)
4. <span data-ttu-id="a3964-230">Save the hosts file.</span><span class="sxs-lookup"><span data-stu-id="a3964-230">Save the hosts file.</span></span>

### <a name="connect-to-the-device-from-the-remote-host"></a><span data-ttu-id="a3964-231">Connect to the device from the remote host</span><span class="sxs-lookup"><span data-stu-id="a3964-231">Connect to the device from the remote host</span></span>
<span data-ttu-id="a3964-232">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span><span class="sxs-lookup"><span data-stu-id="a3964-232">Use Windows PowerShell and SSL to enter an SSAdmin session on your device from a remote host or client.</span></span> <span data-ttu-id="a3964-233">The SSAdmin session maps to option 1 in the [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span><span class="sxs-lookup"><span data-stu-id="a3964-233">The SSAdmin session maps to option 1 in the [serial console](storsimple-windows-powershell-administration.md#connect-to-windows-powershell-for-storsimple-via-the-device-serial-console) menu of your device.</span></span>

<span data-ttu-id="a3964-234">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span><span class="sxs-lookup"><span data-stu-id="a3964-234">Perform the following procedure on the computer from which you want to make the remote Windows PowerShell connection.</span></span>

#### <a name="to-enter-an-ssadmin-session-on-the-device-by-using-windows-powershell-and-ssl"></a><span data-ttu-id="a3964-235">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span><span class="sxs-lookup"><span data-stu-id="a3964-235">To enter an SSAdmin session on the device by using Windows PowerShell and SSL</span></span>
1. <span data-ttu-id="a3964-236">Start a Windows PowerShell session as an administrator.</span><span class="sxs-lookup"><span data-stu-id="a3964-236">Start a Windows PowerShell session as an administrator.</span></span>
2. <span data-ttu-id="a3964-237">Add the device IP address to the client’s trusted hosts by typing:</span><span class="sxs-lookup"><span data-stu-id="a3964-237">Add the device IP address to the client’s trusted hosts by typing:</span></span>
   
     `Set-Item wsman:\localhost\Client\TrustedHosts <device_ip> -Concatenate -Force`
   
    <span data-ttu-id="a3964-238">Where <*device_ip*> is the IP address of your device; for example:</span><span class="sxs-lookup"><span data-stu-id="a3964-238">Where <*device_ip*> is the IP address of your device; for example:</span></span> 
   
     `Set-Item wsman:\localhost\Client\TrustedHosts 10.126.173.90 -Concatenate -Force`
3. <span data-ttu-id="a3964-239">Create a new credential by typing:</span><span class="sxs-lookup"><span data-stu-id="a3964-239">Create a new credential by typing:</span></span> 
   
     `$cred = New-Object pscredential @("<IP of target device>\SSAdmin", (ConvertTo-SecureString -Force -AsPlainText "<Device Administrator Password>"))`
   
    <span data-ttu-id="a3964-240">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span><span class="sxs-lookup"><span data-stu-id="a3964-240">Where <*IP of target device*> is the IP address of DATA 0 for your device; for example, **10.126.173.90** as shown in the preceding image of the hosts file.</span></span> <span data-ttu-id="a3964-241">Also, supply the administrator password for your device.</span><span class="sxs-lookup"><span data-stu-id="a3964-241">Also, supply the administrator password for your device.</span></span>
4. <span data-ttu-id="a3964-242">Create a session by typing:</span><span class="sxs-lookup"><span data-stu-id="a3964-242">Create a session by typing:</span></span>
   
     `$session = New-PSSession -UseSSL -ComputerName <Serial number of target device> -Credential $cred -ConfigurationName "SSAdminConsole"`
   
    <span data-ttu-id="a3964-243">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span><span class="sxs-lookup"><span data-stu-id="a3964-243">For the -ComputerName parameter in the cmdlet, provide the <*serial number of target device*>.</span></span> <span data-ttu-id="a3964-244">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span><span class="sxs-lookup"><span data-stu-id="a3964-244">This serial number was mapped to the IP address of DATA 0 in the hosts file on your remote host; for example, **SHX0991003G44MT** as shown in the following image.</span></span>
5. <span data-ttu-id="a3964-245">Type:</span><span class="sxs-lookup"><span data-stu-id="a3964-245">Type:</span></span> 
   
     `Enter-PSSession $session`
6. <span data-ttu-id="a3964-246">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span><span class="sxs-lookup"><span data-stu-id="a3964-246">You will need to wait a few minutes, and then you will be connected to your device via HTTPS over SSL.</span></span> <span data-ttu-id="a3964-247">You will see a message that indicates you are connected to your device.</span><span class="sxs-lookup"><span data-stu-id="a3964-247">You will see a message that indicates you are connected to your device.</span></span>
   
    ![PowerShell remoting using HTTPS and SSL](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storsimple/media/storsimple-remote-connect/HCS_PSRemotingUsingHTTPSAndSSL.png)

## <a name="next-steps"></a><span data-ttu-id="a3964-249">Next steps</span><span class="sxs-lookup"><span data-stu-id="a3964-249">Next steps</span></span>
* <span data-ttu-id="a3964-250">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a3964-250">Learn more about [using Windows PowerShell to administer your StorSimple device](storsimple-windows-powershell-administration.md).</span></span>
* <span data-ttu-id="a3964-251">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="a3964-251">Learn more about [using the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>










