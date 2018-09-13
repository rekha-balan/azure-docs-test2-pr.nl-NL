---
title: Prepare a Windows VHD to upload to Azure | Microsoft Docs
description: How to prepare a Windows VHD or VHDX before uploading to Azure
services: virtual-machines-windows
documentationcenter: ''
author: genlin
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 7802489d-33ec-4302-82a4-91463d03887a
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 1/11/2017
ms.author: glimoli;genli
ms.openlocfilehash: c5c0d0c677a458c454c1fbcbd86ffc03ab53cf0d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554815"
---
# <a name="prepare-a-windows-vhd-or-vhdx-to-upload-to-azure"></a><span data-ttu-id="26a7a-103">Prepare a Windows VHD or VHDX to upload to Azure</span><span class="sxs-lookup"><span data-stu-id="26a7a-103">Prepare a Windows VHD or VHDX to upload to Azure</span></span>
<span data-ttu-id="26a7a-104">To upload a Windows VM from on-premises to Azure, you must prepare the virtual hard disk (VHD or VHDX).</span><span class="sxs-lookup"><span data-stu-id="26a7a-104">To upload a Windows VM from on-premises to Azure, you must prepare the virtual hard disk (VHD or VHDX).</span></span> <span data-ttu-id="26a7a-105">Azure only supports generation 1 virtual machines that are in the VHD file format and have a fixed sized disk.</span><span class="sxs-lookup"><span data-stu-id="26a7a-105">Azure only supports generation 1 virtual machines that are in the VHD file format and have a fixed sized disk.</span></span> <span data-ttu-id="26a7a-106">The maximum size allowed for the VHD is 1,023 GB.</span><span class="sxs-lookup"><span data-stu-id="26a7a-106">The maximum size allowed for the VHD is 1,023 GB.</span></span> <span data-ttu-id="26a7a-107">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed sized disk.</span><span class="sxs-lookup"><span data-stu-id="26a7a-107">You can convert a generation 1 virtual machine from VHDX to the VHD file format and from dynamically expanding to a fixed sized disk.</span></span> <span data-ttu-id="26a7a-108">But you can't change a virtual machine's generation.</span><span class="sxs-lookup"><span data-stu-id="26a7a-108">But you can't change a virtual machine's generation.</span></span> <span data-ttu-id="26a7a-109">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)</span><span class="sxs-lookup"><span data-stu-id="26a7a-109">For more information, see [Should I create a generation 1 or 2 virtual machine in Hyper-V?](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)</span></span>

## <a name="convert-the-virtual-disk-to-vhd-and-fixed-size-disk"></a><span data-ttu-id="26a7a-110">Convert the virtual disk to VHD and fixed size disk</span><span class="sxs-lookup"><span data-stu-id="26a7a-110">Convert the virtual disk to VHD and fixed size disk</span></span> 
<span data-ttu-id="26a7a-111">If you need to convert your virtual disk to the required format for Azure, use one of the methods in this section.</span><span class="sxs-lookup"><span data-stu-id="26a7a-111">If you need to convert your virtual disk to the required format for Azure, use one of the methods in this section.</span></span> <span data-ttu-id="26a7a-112">Back up the VM before you run the virtual disk conversion process and make sure that the Windows VHD works correctly on the local server.</span><span class="sxs-lookup"><span data-stu-id="26a7a-112">Back up the VM before you run the virtual disk conversion process and make sure that the Windows VHD works correctly on the local server.</span></span> <span data-ttu-id="26a7a-113">Resolve any errors within the VM itself before you try to convert or upload it to Azure.</span><span class="sxs-lookup"><span data-stu-id="26a7a-113">Resolve any errors within the VM itself before you try to convert or upload it to Azure.</span></span>

<span data-ttu-id="26a7a-114">After you convert the disk, create a VM that uses the converted disk.</span><span class="sxs-lookup"><span data-stu-id="26a7a-114">After you convert the disk, create a VM that uses the converted disk.</span></span> <span data-ttu-id="26a7a-115">Start and sign in to the VM to finish preparing the VM for upload.</span><span class="sxs-lookup"><span data-stu-id="26a7a-115">Start and sign in to the VM to finish preparing the VM for upload.</span></span>

### <a name="convert-disk-using-hyper-v-manager"></a><span data-ttu-id="26a7a-116">Convert disk using Hyper-V Manager</span><span class="sxs-lookup"><span data-stu-id="26a7a-116">Convert disk using Hyper-V Manager</span></span>
1. <span data-ttu-id="26a7a-117">Open Hyper-V Manager and select your local computer on the left.</span><span class="sxs-lookup"><span data-stu-id="26a7a-117">Open Hyper-V Manager and select your local computer on the left.</span></span> <span data-ttu-id="26a7a-118">In the menu above it, click **Action** > **Edit Disk**.</span><span class="sxs-lookup"><span data-stu-id="26a7a-118">In the menu above it, click **Action** > **Edit Disk**.</span></span>
2. <span data-ttu-id="26a7a-119">On the **Locate Virtual Hard Disk** screen, browse to, and select your virtual disk.</span><span class="sxs-lookup"><span data-stu-id="26a7a-119">On the **Locate Virtual Hard Disk** screen, browse to, and select your virtual disk.</span></span>
3. <span data-ttu-id="26a7a-120">On the **Choose Action** screen, select **Convert** and **Next**.</span><span class="sxs-lookup"><span data-stu-id="26a7a-120">On the **Choose Action** screen, select **Convert** and **Next**.</span></span>
4. <span data-ttu-id="26a7a-121">If you need to convert from VHDX, select **VHD** and click **Next**</span><span class="sxs-lookup"><span data-stu-id="26a7a-121">If you need to convert from VHDX, select **VHD** and click **Next**</span></span>
5. <span data-ttu-id="26a7a-122">If you need to convert from dynamically expanding disk, select **Fixed size** and click **Next**</span><span class="sxs-lookup"><span data-stu-id="26a7a-122">If you need to convert from dynamically expanding disk, select **Fixed size** and click **Next**</span></span>
6. <span data-ttu-id="26a7a-123">Browse to and select a path to save the new VHD file.</span><span class="sxs-lookup"><span data-stu-id="26a7a-123">Browse to and select a path to save the new VHD file.</span></span>
7. <span data-ttu-id="26a7a-124">Click **Finish** to close.</span><span class="sxs-lookup"><span data-stu-id="26a7a-124">Click **Finish** to close.</span></span>

### <a name="convert-disk-using-powershell"></a><span data-ttu-id="26a7a-125">Convert disk using PowerShell</span><span class="sxs-lookup"><span data-stu-id="26a7a-125">Convert disk using PowerShell</span></span>
<span data-ttu-id="26a7a-126">You can convert a virtual disk by using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet in Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="26a7a-126">You can convert a virtual disk by using the [Convert-VHD](http://technet.microsoft.com/library/hh848454.aspx) cmdlet in Windows PowerShell.</span></span> <span data-ttu-id="26a7a-127">Select **Run as administrator** when you start PowerShell.</span><span class="sxs-lookup"><span data-stu-id="26a7a-127">Select **Run as administrator** when you start PowerShell.</span></span> <span data-ttu-id="26a7a-128">The following example shows you how to convert from a VHDX to VHD, and from a dynamically expanding disk to fixed size:</span><span class="sxs-lookup"><span data-stu-id="26a7a-128">The following example shows you how to convert from a VHDX to VHD, and from a dynamically expanding disk to fixed size:</span></span>

```powershell
Convert-VHD –Path c:\test\MY-VM.vhdx –DestinationPath c:\test\MY-NEW-VM.vhd -VHDType Fixed
```
<span data-ttu-id="26a7a-129">Replace the values for -Path with the path to the virtual hard disk that you want to convert and -DestinationPath with the new path and name for the converted disk.</span><span class="sxs-lookup"><span data-stu-id="26a7a-129">Replace the values for -Path with the path to the virtual hard disk that you want to convert and -DestinationPath with the new path and name for the converted disk.</span></span>

### <a name="convert-from-vmware-vmdk-disk-format"></a><span data-ttu-id="26a7a-130">Convert from VMware VMDK disk format</span><span class="sxs-lookup"><span data-stu-id="26a7a-130">Convert from VMware VMDK disk format</span></span>
<span data-ttu-id="26a7a-131">If you have a Windows VM image in the [VMDK file format](https://en.wikipedia.org/wiki/VMDK), convert it to a VHD by using the [Microsoft Virtual Machine Converter](https://www.microsoft.com/download/details.aspx?id=42497).</span><span class="sxs-lookup"><span data-stu-id="26a7a-131">If you have a Windows VM image in the [VMDK file format](https://en.wikipedia.org/wiki/VMDK), convert it to a VHD by using the [Microsoft Virtual Machine Converter](https://www.microsoft.com/download/details.aspx?id=42497).</span></span> <span data-ttu-id="26a7a-132">For more information, see the blog [How to Convert a VMware VMDK to Hyper-V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).</span><span class="sxs-lookup"><span data-stu-id="26a7a-132">For more information, see the blog [How to Convert a VMware VMDK to Hyper-V VHD](http://blogs.msdn.com/b/timomta/archive/2015/06/11/how-to-convert-a-vmware-vmdk-to-hyper-v-vhd.aspx).</span></span>

## <a name="set-windows-configurations-for-azure"></a><span data-ttu-id="26a7a-133">Set Windows configurations for Azure</span><span class="sxs-lookup"><span data-stu-id="26a7a-133">Set Windows configurations for Azure</span></span>

<span data-ttu-id="26a7a-134">On the virtual machine you plan to upload to Azure, run all the following commands from the command prompt window with [administrative privileges](https://technet.microsoft.com/library/cc947813.aspx).</span><span class="sxs-lookup"><span data-stu-id="26a7a-134">On the virtual machine you plan to upload to Azure, run all the following commands from the command prompt window with [administrative privileges](https://technet.microsoft.com/library/cc947813.aspx).</span></span>

1. <span data-ttu-id="26a7a-135">Remove any static persistent route on the routing table:</span><span class="sxs-lookup"><span data-stu-id="26a7a-135">Remove any static persistent route on the routing table:</span></span>
   
   * <span data-ttu-id="26a7a-136">To view the route table, run `route print` from the command prompt window.</span><span class="sxs-lookup"><span data-stu-id="26a7a-136">To view the route table, run `route print` from the command prompt window.</span></span>
   * <span data-ttu-id="26a7a-137">Check the **Persistence Routes** sections.</span><span class="sxs-lookup"><span data-stu-id="26a7a-137">Check the **Persistence Routes** sections.</span></span> <span data-ttu-id="26a7a-138">If there is a persistent route, use [route delete](https://technet.microsoft.com/library/cc739598.apx) to remove it.</span><span class="sxs-lookup"><span data-stu-id="26a7a-138">If there is a persistent route, use [route delete](https://technet.microsoft.com/library/cc739598.apx) to remove it.</span></span>
2. <span data-ttu-id="26a7a-139">Remove the WinHTTP proxy:</span><span class="sxs-lookup"><span data-stu-id="26a7a-139">Remove the WinHTTP proxy:</span></span>
   
    ```CMD
    netsh winhttp reset proxy
    ```
3. <span data-ttu-id="26a7a-140">Set the disk SAN policy to [Onlineall](https://technet.microsoft.com/library/gg252636.aspx).</span><span class="sxs-lookup"><span data-stu-id="26a7a-140">Set the disk SAN policy to [Onlineall](https://technet.microsoft.com/library/gg252636.aspx).</span></span> 
   
    ```CMD
    diskpart 
    san policy=onlineall
    exit
    ```
    

4. <span data-ttu-id="26a7a-141">Set Coordinated Universal Time (UTC) time for Windows and the startup type of the Windows Time (w32time) service to **Automatically**:</span><span class="sxs-lookup"><span data-stu-id="26a7a-141">Set Coordinated Universal Time (UTC) time for Windows and the startup type of the Windows Time (w32time) service to **Automatically**:</span></span>
   
    ```CMD
    REG ADD HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1
    ```
    ```CMD
    sc config w32time start= auto
    ```

## <a name="set-services-startup-to-windows-default-values"></a><span data-ttu-id="26a7a-142">Set services startup to Windows default values</span><span class="sxs-lookup"><span data-stu-id="26a7a-142">Set services startup to Windows default values</span></span>
<span data-ttu-id="26a7a-143">Make sure that each of the following Windows services is set to the **Windows default values**.</span><span class="sxs-lookup"><span data-stu-id="26a7a-143">Make sure that each of the following Windows services is set to the **Windows default values**.</span></span> <span data-ttu-id="26a7a-144">To reset the startup settings, run the following commands:</span><span class="sxs-lookup"><span data-stu-id="26a7a-144">To reset the startup settings, run the following commands:</span></span>
   
```CMD
sc config bfe start= auto
   
sc config dcomlaunch start= auto
   
sc config dhcp start= auto
   
sc config dnscache start= auto
   
sc config IKEEXT start= auto
   
sc config iphlpsvc start= auto
   
sc config PolicyAgent start= demand
   
sc config LSM start= auto
   
sc config netlogon start= demand
   
sc config netman start= demand
   
sc config NcaSvc start= demand
   
sc config netprofm start= demand
   
sc config NlaSvc start= auto
   
sc config nsi start= auto
   
sc config RpcSs start= auto
   
sc config RpcEptMapper start= auto
   
sc config termService start= demand
   
sc config MpsSvc start= auto
   
sc config WinHttpAutoProxySvc start= demand
   
sc config LanmanWorkstation start= auto
   
sc config RemoteRegistry start= auto
```

## <a name="update-remote-desktop-registry-settings"></a><span data-ttu-id="26a7a-145">Update Remote Desktop registry settings</span><span class="sxs-lookup"><span data-stu-id="26a7a-145">Update Remote Desktop registry settings</span></span>
1. <span data-ttu-id="26a7a-146">If there are any self-signed certificates tied to the Remote Desktop Protocol (RDP) listener, remove them:</span><span class="sxs-lookup"><span data-stu-id="26a7a-146">If there are any self-signed certificates tied to the Remote Desktop Protocol (RDP) listener, remove them:</span></span>
   
    ```CMD
    REG DELETE "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp\SSLCertificateSHA1Hash”
    ```
   
    <span data-ttu-id="26a7a-147">For more information about configuring certificates for RDP listener, see [Listener Certificate Configurations in Windows Server ](https://blogs.technet.microsoft.com/askperf/2014/05/28/listener-certificate-configurations-in-windows-server-2012-2012-r2/)</span><span class="sxs-lookup"><span data-stu-id="26a7a-147">For more information about configuring certificates for RDP listener, see [Listener Certificate Configurations in Windows Server ](https://blogs.technet.microsoft.com/askperf/2014/05/28/listener-certificate-configurations-in-windows-server-2012-2012-r2/)</span></span>
2. <span data-ttu-id="26a7a-148">Configure the [KeepAlive](https://technet.microsoft.com/library/cc957549.aspx) values for RDP service:</span><span class="sxs-lookup"><span data-stu-id="26a7a-148">Configure the [KeepAlive](https://technet.microsoft.com/library/cc957549.aspx) values for RDP service:</span></span>
   
    ```CMD
    REG ADD "HKLM\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services" /v KeepAliveEnable /t REG_DWORD  /d 1 /f
    ```
    ```CMD
    REG ADD "HKLM\SOFTWARE\Policies\Microsoft\Windows NT\Terminal Services" /v KeepAliveInterval /t REG_DWORD  /d 1 /f
    ```
    ```CMD
    REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\Winstations\RDP-Tcp" /v KeepAliveTimeout /t REG_DWORD /d 1 /f
    ```
3. <span data-ttu-id="26a7a-149">Configure the authentication mode for the RDP service:</span><span class="sxs-lookup"><span data-stu-id="26a7a-149">Configure the authentication mode for the RDP service:</span></span>
   
    ```CMD
    REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /v UserAuthentication /t REG_DWORD  /d 1 /f
   ```
    ```CMD
    REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /v SecurityLayer /t REG_DWORD  /d 1 /f
   ```
    ```CMD
    REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server\WinStations\RDP-Tcp" /v fAllowSecProtocolNegotiation /t REG_DWORD  /d 1 /f
    ```
4. <span data-ttu-id="26a7a-150">Enable RDP service by adding the following subkeys to the registry:</span><span class="sxs-lookup"><span data-stu-id="26a7a-150">Enable RDP service by adding the following subkeys to the registry:</span></span>
   
    ```CMD
    REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\Terminal Server" /v fDenyTSConnections /t REG_DWORD  /d 0 /f
    ```

## <a name="configure-windows-firewall-rules"></a><span data-ttu-id="26a7a-151">Configure Windows Firewall rules</span><span class="sxs-lookup"><span data-stu-id="26a7a-151">Configure Windows Firewall rules</span></span>
1. <span data-ttu-id="26a7a-152">Run the following command in PowerShell to allow WinRM through the three firewall profiles (Domain, Private, and Public) and enable PowerShell Remote service:</span><span class="sxs-lookup"><span data-stu-id="26a7a-152">Run the following command in PowerShell to allow WinRM through the three firewall profiles (Domain, Private, and Public) and enable PowerShell Remote service:</span></span>
   
   ```powershell
   Enable-PSRemoting -force
   ```
2. <span data-ttu-id="26a7a-153">Run the following commands in the command prompt window to make sure that the following guest operating system firewall rules are in place:</span><span class="sxs-lookup"><span data-stu-id="26a7a-153">Run the following commands in the command prompt window to make sure that the following guest operating system firewall rules are in place:</span></span>
   
   * <span data-ttu-id="26a7a-154">Inbound</span><span class="sxs-lookup"><span data-stu-id="26a7a-154">Inbound</span></span>
   
   ```CMD
   netsh advfirewall firewall set rule dir=in name="File and Printer Sharing (Echo Request - ICMPv4-In)" new enable=yes
   
   netsh advfirewall firewall set rule dir=in name="Network Discovery (LLMNR-UDP-In)" new enable=yes
   
   netsh advfirewall firewall set rule dir=in name="Network Discovery (NB-Datagram-In)" new enable=yes
   
   netsh advfirewall firewall set rule dir=in name="Network Discovery (NB-Name-In)" new enable=yes
   
   netsh advfirewall firewall set rule dir=in name="Network Discovery (Pub-WSD-In)" new enable=yes
   
   netsh advfirewall firewall set rule dir=in name="Network Discovery (SSDP-In)" new enable=yes
   
   netsh advfirewall firewall set rule dir=in name="Network Discovery (UPnP-In)" new enable=yes
   
   netsh advfirewall firewall set rule dir=in name="Network Discovery (WSD EventsSecure-In)" new enable=yes
   
   netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   
   netsh advfirewall firewall set rule dir=in name="Windows Remote Management (HTTP-In)" new enable=yes
   ```
   
   * <span data-ttu-id="26a7a-155">Inbound and outbound</span><span class="sxs-lookup"><span data-stu-id="26a7a-155">Inbound and outbound</span></span>
   
   ```CMD
   netsh advfirewall firewall set rule group="Remote Desktop" new enable=yes
   
   netsh advfirewall firewall set rule group="Core Networking" new enable=yes
   ```
   
   * <span data-ttu-id="26a7a-156">Outbound</span><span class="sxs-lookup"><span data-stu-id="26a7a-156">Outbound</span></span>
   
   ```CMD
   netsh advfirewall firewall set rule dir=out name="Network Discovery (LLMNR-UDP-Out)" new enable=yes
   
   netsh advfirewall firewall set rule dir=out name="Network Discovery (NB-Datagram-Out)" new enable=yes
   
   netsh advfirewall firewall set rule dir=out name="Network Discovery (NB-Name-Out)" new enable=yes
   
   netsh advfirewall firewall set rule dir=out name="Network Discovery (Pub-WSD-Out)" new enable=yes
   
   netsh advfirewall firewall set rule dir=out name="Network Discovery (SSDP-Out)" new enable=yes
   
   netsh advfirewall firewall set rule dir=out name="Network Discovery (UPnPHost-Out)" new enable=yes
   
   netsh advfirewall firewall set rule dir=out name="Network Discovery (UPnP-Out)" new enable=yes
   
   netsh advfirewall firewall set rule dir=out name="Network Discovery (WSD Events-Out)" new enable=yes
   
   netsh advfirewall firewall set rule dir=out name="Network Discovery (WSD EventsSecure-Out)" new enable=yes
   
   netsh advfirewall firewall set rule dir=out name="Network Discovery (WSD-Out)" new enable=yes
   ```

## <a name="verify-vm-is-healthy-secure-and-accessible-with-rdp"></a><span data-ttu-id="26a7a-157">Verify VM is healthy, secure, and accessible with RDP</span><span class="sxs-lookup"><span data-stu-id="26a7a-157">Verify VM is healthy, secure, and accessible with RDP</span></span> 
1. <span data-ttu-id="26a7a-158">In the command prompt window, run `winmgmt /verifyrepository` to confirm that the Windows Management Instrumentation (WMI) repository is consistent.</span><span class="sxs-lookup"><span data-stu-id="26a7a-158">In the command prompt window, run `winmgmt /verifyrepository` to confirm that the Windows Management Instrumentation (WMI) repository is consistent.</span></span> <span data-ttu-id="26a7a-159">If the repository is corrupted, see the blog post [WMI: Repository Corruption, or Not?](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not)</span><span class="sxs-lookup"><span data-stu-id="26a7a-159">If the repository is corrupted, see the blog post [WMI: Repository Corruption, or Not?](https://blogs.technet.microsoft.com/askperf/2014/08/08/wmi-repository-corruption-or-not)</span></span>
2. <span data-ttu-id="26a7a-160">Set the Boot Configuration Data (BCD) settings:</span><span class="sxs-lookup"><span data-stu-id="26a7a-160">Set the Boot Configuration Data (BCD) settings:</span></span>
   
   ```CMD
   bcdedit /set {bootmgr} integrityservices enable
   
   bcdedit /set {default} device partition=C:
   
   bcdedit /set {default} integrityservices enable
   
   bcdedit /set {default} recoveryenabled Off
   
   bcdedit /set {default} osdevice partition=C:
   
   bcdedit /set {default} bootstatuspolicy IgnoreAllFailures
   ```
3. <span data-ttu-id="26a7a-161">Remove any extra Transport Driver Interface filters, such as software that analyzes TCP packets.</span><span class="sxs-lookup"><span data-stu-id="26a7a-161">Remove any extra Transport Driver Interface filters, such as software that analyzes TCP packets.</span></span>
4. <span data-ttu-id="26a7a-162">To make sure the disk is healthy and consistent, run the `CHKDSK /f` command in the command prompt window.</span><span class="sxs-lookup"><span data-stu-id="26a7a-162">To make sure the disk is healthy and consistent, run the `CHKDSK /f` command in the command prompt window.</span></span> <span data-ttu-id="26a7a-163">Type "Y" to schedule the check and restart the VM.</span><span class="sxs-lookup"><span data-stu-id="26a7a-163">Type "Y" to schedule the check and restart the VM.</span></span>
5. <span data-ttu-id="26a7a-164">Uninstall any other third-party software and driver related to physical components or any other virtualization technology.</span><span class="sxs-lookup"><span data-stu-id="26a7a-164">Uninstall any other third-party software and driver related to physical components or any other virtualization technology.</span></span>
6. <span data-ttu-id="26a7a-165">Make sure that a third-party application is not using Port 3389.</span><span class="sxs-lookup"><span data-stu-id="26a7a-165">Make sure that a third-party application is not using Port 3389.</span></span> <span data-ttu-id="26a7a-166">This port is used for the RDP service in Azure.</span><span class="sxs-lookup"><span data-stu-id="26a7a-166">This port is used for the RDP service in Azure.</span></span> <span data-ttu-id="26a7a-167">You can run `netstat -anob` in the command prompt window to see the ports that are used by the applications.</span><span class="sxs-lookup"><span data-stu-id="26a7a-167">You can run `netstat -anob` in the command prompt window to see the ports that are used by the applications.</span></span>
7. <span data-ttu-id="26a7a-168">If the Windows VHD that you want to upload is a domain controller, follow [these extra steps](https://support.microsoft.com/kb/2904015) to prepare the disk.</span><span class="sxs-lookup"><span data-stu-id="26a7a-168">If the Windows VHD that you want to upload is a domain controller, follow [these extra steps](https://support.microsoft.com/kb/2904015) to prepare the disk.</span></span>
8. <span data-ttu-id="26a7a-169">Reboot the VM to make sure that Windows is still healthy can be reached by using the RDP connection.</span><span class="sxs-lookup"><span data-stu-id="26a7a-169">Reboot the VM to make sure that Windows is still healthy can be reached by using the RDP connection.</span></span>
9. <span data-ttu-id="26a7a-170">Reset the current local administrator password and make sure that you can use this account to sign in to Windows through the RDP connection.</span><span class="sxs-lookup"><span data-stu-id="26a7a-170">Reset the current local administrator password and make sure that you can use this account to sign in to Windows through the RDP connection.</span></span> <span data-ttu-id="26a7a-171">This access permission is controlled by the "Allow log on through Remote Desktop Services" Group Policy object.</span><span class="sxs-lookup"><span data-stu-id="26a7a-171">This access permission is controlled by the "Allow log on through Remote Desktop Services" Group Policy object.</span></span> <span data-ttu-id="26a7a-172">You can view this object in the Local Group Policy Editor under "Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment."</span><span class="sxs-lookup"><span data-stu-id="26a7a-172">You can view this object in the Local Group Policy Editor under "Computer Configuration\Windows Settings\Security Settings\Local Policies\User Rights Assignment."</span></span>

## <a name="install-windows-updates"></a><span data-ttu-id="26a7a-173">Install Windows Updates</span><span class="sxs-lookup"><span data-stu-id="26a7a-173">Install Windows Updates</span></span>
<span data-ttu-id="26a7a-174">Install the latest updates for Windows.</span><span class="sxs-lookup"><span data-stu-id="26a7a-174">Install the latest updates for Windows.</span></span> <span data-ttu-id="26a7a-175">If that's not possible, make sure that the following updates are installed:</span><span class="sxs-lookup"><span data-stu-id="26a7a-175">If that's not possible, make sure that the following updates are installed:</span></span>
   
   * <span data-ttu-id="26a7a-176">[KB3137061](https://support.microsoft.com/kb/3137061) Microsoft Azure VMs don't recover from a network outage and data corruption issues occur</span><span class="sxs-lookup"><span data-stu-id="26a7a-176">[KB3137061](https://support.microsoft.com/kb/3137061) Microsoft Azure VMs don't recover from a network outage and data corruption issues occur</span></span>
   * <span data-ttu-id="26a7a-177">[KB3115224](https://support.microsoft.com/kb/3115224) Reliability improvements for VMs that are running on a Windows Server 2012 R2 or Windows Server 2012 host</span><span class="sxs-lookup"><span data-stu-id="26a7a-177">[KB3115224](https://support.microsoft.com/kb/3115224) Reliability improvements for VMs that are running on a Windows Server 2012 R2 or Windows Server 2012 host</span></span>
   * <span data-ttu-id="26a7a-178">[KB3140410](https://support.microsoft.com/kb/3140410) MS16-031: Security update for Microsoft Windows to address elevation of privilege: March 8, 2016</span><span class="sxs-lookup"><span data-stu-id="26a7a-178">[KB3140410](https://support.microsoft.com/kb/3140410) MS16-031: Security update for Microsoft Windows to address elevation of privilege: March 8, 2016</span></span>
   * <span data-ttu-id="26a7a-179">[KB3063075](https://support.microsoft.com/kb/3063075) Many ID 129 events are logged when you run a Windows Server 2012 R2 virtual machine in Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="26a7a-179">[KB3063075](https://support.microsoft.com/kb/3063075) Many ID 129 events are logged when you run a Windows Server 2012 R2 virtual machine in Microsoft Azure</span></span>
   * <span data-ttu-id="26a7a-180">[KB3137061](https://support.microsoft.com/kb/3137061) Microsoft Azure VMs don't recover from a network outage and data corruption issues occur</span><span class="sxs-lookup"><span data-stu-id="26a7a-180">[KB3137061](https://support.microsoft.com/kb/3137061) Microsoft Azure VMs don't recover from a network outage and data corruption issues occur</span></span>
   * <span data-ttu-id="26a7a-181">[KB3114025](https://support.microsoft.com/kb/3114025) Slow performance when you access Azure files storage from Windows 8.1 or Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="26a7a-181">[KB3114025](https://support.microsoft.com/kb/3114025) Slow performance when you access Azure files storage from Windows 8.1 or Server 2012 R2</span></span>
   * <span data-ttu-id="26a7a-182">[KB3033930](https://support.microsoft.com/kb/3033930) Hotfix increases the 64K limit on RIO buffers per process for Azure service in Windows</span><span class="sxs-lookup"><span data-stu-id="26a7a-182">[KB3033930](https://support.microsoft.com/kb/3033930) Hotfix increases the 64K limit on RIO buffers per process for Azure service in Windows</span></span>
   * <span data-ttu-id="26a7a-183">[KB3004545](https://support.microsoft.com/kb/3004545) You cannot access virtual machines that are hosted on Azure hosting services through a VPN connection in Windows</span><span class="sxs-lookup"><span data-stu-id="26a7a-183">[KB3004545](https://support.microsoft.com/kb/3004545) You cannot access virtual machines that are hosted on Azure hosting services through a VPN connection in Windows</span></span>
   * <span data-ttu-id="26a7a-184">[KB3082343](https://support.microsoft.com/kb/3082343) Cross-Premises VPN connectivity is lost when Azure site-to-site VPN tunnels use Windows Server 2012 R2 RRAS</span><span class="sxs-lookup"><span data-stu-id="26a7a-184">[KB3082343](https://support.microsoft.com/kb/3082343) Cross-Premises VPN connectivity is lost when Azure site-to-site VPN tunnels use Windows Server 2012 R2 RRAS</span></span>
   * <span data-ttu-id="26a7a-185">[KB3140410](https://support.microsoft.com/kb/3140410) MS16-031: Security update for Microsoft Windows to address elevation of privilege: March 8, 2016</span><span class="sxs-lookup"><span data-stu-id="26a7a-185">[KB3140410](https://support.microsoft.com/kb/3140410) MS16-031: Security update for Microsoft Windows to address elevation of privilege: March 8, 2016</span></span>
   * <span data-ttu-id="26a7a-186">[KB3146723](https://support.microsoft.com/kb/3146723) MS16-048: Description of the security update for CSRSS: April 12, 2016</span><span class="sxs-lookup"><span data-stu-id="26a7a-186">[KB3146723](https://support.microsoft.com/kb/3146723) MS16-048: Description of the security update for CSRSS: April 12, 2016</span></span>
   * <span data-ttu-id="26a7a-187">[KB2904100](https://support.microsoft.com/kb/2904100) System freezes during disk I/O in Windows</span><span class="sxs-lookup"><span data-stu-id="26a7a-187">[KB2904100](https://support.microsoft.com/kb/2904100) System freezes during disk I/O in Windows</span></span>
     
## <span data-ttu-id="26a7a-188">Run Sysprep  <a id="step23"></a></span><span class="sxs-lookup"><span data-stu-id="26a7a-188">Run Sysprep  <a id="step23"></a></span></span>    
<span data-ttu-id="26a7a-189">If you want to create an image to deploy to multiple VMs, you need to [generalize the image by running Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before you upload the VHD to Azure.</span><span class="sxs-lookup"><span data-stu-id="26a7a-189">If you want to create an image to deploy to multiple VMs, you need to [generalize the image by running Sysprep](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before you upload the VHD to Azure.</span></span> <span data-ttu-id="26a7a-190">You don't need to run Sysprep to use a specialized VHD.</span><span class="sxs-lookup"><span data-stu-id="26a7a-190">You don't need to run Sysprep to use a specialized VHD.</span></span> <span data-ttu-id="26a7a-191">For more information, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="26a7a-191">For more information, see the following articles:</span></span>
   
   * [<span data-ttu-id="26a7a-192">Generalize a Windows virtual machine using Sysprep</span><span class="sxs-lookup"><span data-stu-id="26a7a-192">Generalize a Windows virtual machine using Sysprep</span></span>](generalize-vhd.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)
   * [<span data-ttu-id="26a7a-193">Sysprep Support for Server Roles</span><span class="sxs-lookup"><span data-stu-id="26a7a-193">Sysprep Support for Server Roles</span></span>](https://msdn.microsoft.com/windows/hardware/commercialize/manufacture/desktop/sysprep-support-for-server-roles)

## <a name="complete-recommended-configurations"></a><span data-ttu-id="26a7a-194">Complete recommended configurations</span><span class="sxs-lookup"><span data-stu-id="26a7a-194">Complete recommended configurations</span></span>
<span data-ttu-id="26a7a-195">The following settings do not affect VHD uploading.</span><span class="sxs-lookup"><span data-stu-id="26a7a-195">The following settings do not affect VHD uploading.</span></span> <span data-ttu-id="26a7a-196">However, we strongly recommend that you have them configured.</span><span class="sxs-lookup"><span data-stu-id="26a7a-196">However, we strongly recommend that you have them configured.</span></span>

* <span data-ttu-id="26a7a-197">Install the [Azure Virtual Machines Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="26a7a-197">Install the [Azure Virtual Machines Agent](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409).</span></span> <span data-ttu-id="26a7a-198">After you install the agent, you can enable VM extensions.</span><span class="sxs-lookup"><span data-stu-id="26a7a-198">After you install the agent, you can enable VM extensions.</span></span> <span data-ttu-id="26a7a-199">The VM extensions implement most of the critical functionality that you want to use with your VMs like resetting passwords, configuring RDP, and many others.</span><span class="sxs-lookup"><span data-stu-id="26a7a-199">The VM extensions implement most of the critical functionality that you want to use with your VMs like resetting passwords, configuring RDP, and many others.</span></span>
* <span data-ttu-id="26a7a-200">The Dump log can be helpful in troubleshooting Windows crash issues.</span><span class="sxs-lookup"><span data-stu-id="26a7a-200">The Dump log can be helpful in troubleshooting Windows crash issues.</span></span> <span data-ttu-id="26a7a-201">Enable the Dump log collection:</span><span class="sxs-lookup"><span data-stu-id="26a7a-201">Enable the Dump log collection:</span></span>
  
    ```CMD
    REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\CrashControl" /v CrashDumpEnabled /t REG_DWORD /d 2 /f`
  
    REG ADD "HKLM\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps" /v DumpFolder /t REG_EXPAND_SZ /d "c:\CrashDumps" /f
  
    REG ADD "HKLM\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps" /v DumpCount /t REG_DWORD /d 10 /f
  
    REG ADD "HKLM\SOFTWARE\Microsoft\Windows\Windows Error Reporting\LocalDumps" /v DumpType /t REG_DWORD /d 2 /f
  
    sc config wer start= auto
    ```
* <span data-ttu-id="26a7a-202">After the VM is created in Azure, configure the system defined size pagefile on drive D:</span><span class="sxs-lookup"><span data-stu-id="26a7a-202">After the VM is created in Azure, configure the system defined size pagefile on drive D:</span></span>
  
    ```CMD
    REG ADD "HKLM\SYSTEM\CurrentControlSet\Control\Session Manager\Memory Management" /t REG_MULTI_SZ /v PagingFiles /d "D:\pagefile.sys 0 0" /f
    ```

## <a name="next-steps"></a><span data-ttu-id="26a7a-203">Next steps</span><span class="sxs-lookup"><span data-stu-id="26a7a-203">Next steps</span></span>
* [<span data-ttu-id="26a7a-204">Upload a Windows VM image to Azure for Resource Manager deployments</span><span class="sxs-lookup"><span data-stu-id="26a7a-204">Upload a Windows VM image to Azure for Resource Manager deployments</span></span>](upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

