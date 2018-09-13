---
title: Reset a local Windows password without Azure agent | Microsoft Docs
description: How to reset the password of a local Windows user account when the Azure guest agent is not installed or functioning on a VM
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: 0905dcc54def70e207f9d22b2cde9f1785c64e26
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540757"
---
# <a name="how-to-reset-local-windows-password-for-azure-vm"></a><span data-ttu-id="d1e10-103">How to reset local Windows password for Azure VM</span><span class="sxs-lookup"><span data-stu-id="d1e10-103">How to reset local Windows password for Azure VM</span></span>
<span data-ttu-id="d1e10-104">You can reset the local Windows password of a VM in Azure using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided the Azure guest agent is installed.</span><span class="sxs-lookup"><span data-stu-id="d1e10-104">You can reset the local Windows password of a VM in Azure using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) provided the Azure guest agent is installed.</span></span> <span data-ttu-id="d1e10-105">This method is the primary way to reset a password for an Azure VM.</span><span class="sxs-lookup"><span data-stu-id="d1e10-105">This method is the primary way to reset a password for an Azure VM.</span></span> <span data-ttu-id="d1e10-106">If you encounter issues with the Azure guest agent not responding, or failing to install after uploading a custom image, you can manually reset a Windows password.</span><span class="sxs-lookup"><span data-stu-id="d1e10-106">If you encounter issues with the Azure guest agent not responding, or failing to install after uploading a custom image, you can manually reset a Windows password.</span></span> <span data-ttu-id="d1e10-107">This article details how to reset a local account password by attaching the source OS virtual disk to another VM.</span><span class="sxs-lookup"><span data-stu-id="d1e10-107">This article details how to reset a local account password by attaching the source OS virtual disk to another VM.</span></span> 

> [!WARNING]
> <span data-ttu-id="d1e10-108">Only use this process as a last resort.</span><span class="sxs-lookup"><span data-stu-id="d1e10-108">Only use this process as a last resort.</span></span> <span data-ttu-id="d1e10-109">Always try to reset a password using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span><span class="sxs-lookup"><span data-stu-id="d1e10-109">Always try to reset a password using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) first.</span></span>
> 
> 

## <a name="overview-of-the-process"></a><span data-ttu-id="d1e10-110">Overview of the process</span><span class="sxs-lookup"><span data-stu-id="d1e10-110">Overview of the process</span></span>
<span data-ttu-id="d1e10-111">The core steps for performing a local password reset for a Windows VM in Azure when there is no access to the Azure guest agent is as follows:</span><span class="sxs-lookup"><span data-stu-id="d1e10-111">The core steps for performing a local password reset for a Windows VM in Azure when there is no access to the Azure guest agent is as follows:</span></span>

* <span data-ttu-id="d1e10-112">Delete the source VM.</span><span class="sxs-lookup"><span data-stu-id="d1e10-112">Delete the source VM.</span></span> <span data-ttu-id="d1e10-113">The virtual disks are retained.</span><span class="sxs-lookup"><span data-stu-id="d1e10-113">The virtual disks are retained.</span></span>
* <span data-ttu-id="d1e10-114">Attach the source VM's OS disk to another VM on the same location within your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d1e10-114">Attach the source VM's OS disk to another VM on the same location within your Azure subscription.</span></span> <span data-ttu-id="d1e10-115">This VM is referred to as the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="d1e10-115">This VM is referred to as the troubleshooting VM.</span></span>
* <span data-ttu-id="d1e10-116">Using the troubleshooting VM, create some config files on the source VM's OS disk.</span><span class="sxs-lookup"><span data-stu-id="d1e10-116">Using the troubleshooting VM, create some config files on the source VM's OS disk.</span></span>
* <span data-ttu-id="d1e10-117">Detach the VM's OS disk from the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="d1e10-117">Detach the VM's OS disk from the troubleshooting VM.</span></span>
* <span data-ttu-id="d1e10-118">Use a Resource Manager template to create a VM, using the original virtual disk.</span><span class="sxs-lookup"><span data-stu-id="d1e10-118">Use a Resource Manager template to create a VM, using the original virtual disk.</span></span>
* <span data-ttu-id="d1e10-119">When the new VM boots, the config files you create update the password of the required user.</span><span class="sxs-lookup"><span data-stu-id="d1e10-119">When the new VM boots, the config files you create update the password of the required user.</span></span>

## <a name="detailed-steps"></a><span data-ttu-id="d1e10-120">Detailed steps</span><span class="sxs-lookup"><span data-stu-id="d1e10-120">Detailed steps</span></span>
<span data-ttu-id="d1e10-121">Always try to reset a password using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying the following steps.</span><span class="sxs-lookup"><span data-stu-id="d1e10-121">Always try to reset a password using the [Azure portal or Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) before trying the following steps.</span></span> <span data-ttu-id="d1e10-122">Make sure you have a backup of your VM before you start.</span><span class="sxs-lookup"><span data-stu-id="d1e10-122">Make sure you have a backup of your VM before you start.</span></span> 

1. <span data-ttu-id="d1e10-123">Delete the affected VM in Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d1e10-123">Delete the affected VM in Azure portal.</span></span> <span data-ttu-id="d1e10-124">Deleting the VM only deletes the metadata, the reference of the VM within Azure.</span><span class="sxs-lookup"><span data-stu-id="d1e10-124">Deleting the VM only deletes the metadata, the reference of the VM within Azure.</span></span> <span data-ttu-id="d1e10-125">The virtual disks are retained when the VM is deleted:</span><span class="sxs-lookup"><span data-stu-id="d1e10-125">The virtual disks are retained when the VM is deleted:</span></span>
   
   * <span data-ttu-id="d1e10-126">Select the VM in the Azure portal, click *Delete*:</span><span class="sxs-lookup"><span data-stu-id="d1e10-126">Select the VM in the Azure portal, click *Delete*:</span></span>
     
     ![Delete existing VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/delete_vm.png)
2. <span data-ttu-id="d1e10-128">Attach the source VM’s OS disk to the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="d1e10-128">Attach the source VM’s OS disk to the troubleshooting VM.</span></span> <span data-ttu-id="d1e10-129">The troubleshooting VM must be in the same region as the source VM's OS disk (such as `West US`):</span><span class="sxs-lookup"><span data-stu-id="d1e10-129">The troubleshooting VM must be in the same region as the source VM's OS disk (such as `West US`):</span></span>
   
   * <span data-ttu-id="d1e10-130">Select the troubleshooting VM in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="d1e10-130">Select the troubleshooting VM in the Azure portal.</span></span> <span data-ttu-id="d1e10-131">Click *Disks* | *Attach existing*:</span><span class="sxs-lookup"><span data-stu-id="d1e10-131">Click *Disks* | *Attach existing*:</span></span>
     
     ![Attach existing disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/disks_attach_existing.png)
     
     <span data-ttu-id="d1e10-133">Select *VHD File* and then select the storage account that contains your source VM:</span><span class="sxs-lookup"><span data-stu-id="d1e10-133">Select *VHD File* and then select the storage account that contains your source VM:</span></span>
     
     ![Select storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/disks_select_storageaccount.png)
     
     <span data-ttu-id="d1e10-135">Select the source container.</span><span class="sxs-lookup"><span data-stu-id="d1e10-135">Select the source container.</span></span> <span data-ttu-id="d1e10-136">The source container is typically *vhds*:</span><span class="sxs-lookup"><span data-stu-id="d1e10-136">The source container is typically *vhds*:</span></span>
     
     ![Select storage container](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/disks_select_container.png)
     
     <span data-ttu-id="d1e10-138">Select the OS vhd to attach.</span><span class="sxs-lookup"><span data-stu-id="d1e10-138">Select the OS vhd to attach.</span></span> <span data-ttu-id="d1e10-139">Click *Select* to complete the process:</span><span class="sxs-lookup"><span data-stu-id="d1e10-139">Click *Select* to complete the process:</span></span>
     
     ![Select source virtual disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. <span data-ttu-id="d1e10-141">Connect to the troubleshooting VM using Remote Desktop and ensure the source VM's OS disk is visible:</span><span class="sxs-lookup"><span data-stu-id="d1e10-141">Connect to the troubleshooting VM using Remote Desktop and ensure the source VM's OS disk is visible:</span></span>
   
   * <span data-ttu-id="d1e10-142">Select the troubleshooting VM in the Azure portal and click *Connect*.</span><span class="sxs-lookup"><span data-stu-id="d1e10-142">Select the troubleshooting VM in the Azure portal and click *Connect*.</span></span>
   * <span data-ttu-id="d1e10-143">Open the RDP file that downloads.</span><span class="sxs-lookup"><span data-stu-id="d1e10-143">Open the RDP file that downloads.</span></span> <span data-ttu-id="d1e10-144">Enter the username and password of the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="d1e10-144">Enter the username and password of the troubleshooting VM.</span></span>
   * <span data-ttu-id="d1e10-145">In File Explorer, look for the data disk you attached.</span><span class="sxs-lookup"><span data-stu-id="d1e10-145">In File Explorer, look for the data disk you attached.</span></span> <span data-ttu-id="d1e10-146">If the source VM’s VHD is the only data disk attached to the troubleshooting VM, it should be the F: drive:</span><span class="sxs-lookup"><span data-stu-id="d1e10-146">If the source VM’s VHD is the only data disk attached to the troubleshooting VM, it should be the F: drive:</span></span>
     
     ![View attached data disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. <span data-ttu-id="d1e10-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on the source VM’s drive (if gpt.ini exists, rename to gpt.ini.bak):</span><span class="sxs-lookup"><span data-stu-id="d1e10-148">Create `gpt.ini` in `\Windows\System32\GroupPolicy` on the source VM’s drive (if gpt.ini exists, rename to gpt.ini.bak):</span></span>
   
   > [!WARNING]
   > <span data-ttu-id="d1e10-149">Make sure that you do not accidentally create the following files in C:\Windows, the OS drive for the troubleshooting VM.</span><span class="sxs-lookup"><span data-stu-id="d1e10-149">Make sure that you do not accidentally create the following files in C:\Windows, the OS drive for the troubleshooting VM.</span></span> <span data-ttu-id="d1e10-150">Create the following files in the OS drive for your source VM that is attached as a data disk.</span><span class="sxs-lookup"><span data-stu-id="d1e10-150">Create the following files in the OS drive for your source VM that is attached as a data disk.</span></span>
   > 
   > 
   
   * <span data-ttu-id="d1e10-151">Add the following lines into the `gpt.ini` file you created:</span><span class="sxs-lookup"><span data-stu-id="d1e10-151">Add the following lines into the `gpt.ini` file you created:</span></span>
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Create gpt.ini](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/create_gpt_ini.png)
5. <span data-ttu-id="d1e10-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span><span class="sxs-lookup"><span data-stu-id="d1e10-153">Create `scripts.ini` in `\Windows\System32\GroupPolicy\Machine\Scripts`.</span></span> <span data-ttu-id="d1e10-154">Make sure hidden folders are shown.</span><span class="sxs-lookup"><span data-stu-id="d1e10-154">Make sure hidden folders are shown.</span></span> <span data-ttu-id="d1e10-155">If needed, create the `Machine` or `Scripts` folders.</span><span class="sxs-lookup"><span data-stu-id="d1e10-155">If needed, create the `Machine` or `Scripts` folders.</span></span>
   
   * <span data-ttu-id="d1e10-156">Add the following lines the `scripts.ini` file you created:</span><span class="sxs-lookup"><span data-stu-id="d1e10-156">Add the following lines the `scripts.ini` file you created:</span></span>
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Create scripts.ini](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/create_scripts_ini.png)
6. <span data-ttu-id="d1e10-158">Create `FixAzureVM.cmd` in `\Windows\System32` with the following contents, replacing `<username>` and `<newpassword>` with your own values:</span><span class="sxs-lookup"><span data-stu-id="d1e10-158">Create `FixAzureVM.cmd` in `\Windows\System32` with the following contents, replacing `<username>` and `<newpassword>` with your own values:</span></span>
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Create FixAzureVM.cmd](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    <span data-ttu-id="d1e10-160">You must meet the configured password complexity requirements for your VM when defining the new password.</span><span class="sxs-lookup"><span data-stu-id="d1e10-160">You must meet the configured password complexity requirements for your VM when defining the new password.</span></span>
7. <span data-ttu-id="d1e10-161">In Azure portal, detach the disk from the troubleshooting VM:</span><span class="sxs-lookup"><span data-stu-id="d1e10-161">In Azure portal, detach the disk from the troubleshooting VM:</span></span>
   
   * <span data-ttu-id="d1e10-162">Select the troubleshooting VM in the Azure portal, click *Disks*.</span><span class="sxs-lookup"><span data-stu-id="d1e10-162">Select the troubleshooting VM in the Azure portal, click *Disks*.</span></span>
   * <span data-ttu-id="d1e10-163">Select the data disk attached in step 2, click *Detach*:</span><span class="sxs-lookup"><span data-stu-id="d1e10-163">Select the data disk attached in step 2, click *Detach*:</span></span>
     
     ![Detach disk](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/detach_disk.png)
8. <span data-ttu-id="d1e10-165">Before you create a VM, obtain the URI to your source OS disk:</span><span class="sxs-lookup"><span data-stu-id="d1e10-165">Before you create a VM, obtain the URI to your source OS disk:</span></span>
   
   * <span data-ttu-id="d1e10-166">Select the storage account in the Azure portal, click *Blobs*.</span><span class="sxs-lookup"><span data-stu-id="d1e10-166">Select the storage account in the Azure portal, click *Blobs*.</span></span>
   * <span data-ttu-id="d1e10-167">Select the container.</span><span class="sxs-lookup"><span data-stu-id="d1e10-167">Select the container.</span></span> <span data-ttu-id="d1e10-168">The source container is typically *vhds*:</span><span class="sxs-lookup"><span data-stu-id="d1e10-168">The source container is typically *vhds*:</span></span>
     
     ![Select storage account blob](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/select_storage_details.png)
     
     <span data-ttu-id="d1e10-170">Select your source VM OS VHD and click the *Copy* button next to the *URL* name:</span><span class="sxs-lookup"><span data-stu-id="d1e10-170">Select your source VM OS VHD and click the *Copy* button next to the *URL* name:</span></span>
     
     ![Copy disk URI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. <span data-ttu-id="d1e10-172">Create a VM from the source VM’s OS disk:</span><span class="sxs-lookup"><span data-stu-id="d1e10-172">Create a VM from the source VM’s OS disk:</span></span>
   
   * <span data-ttu-id="d1e10-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) to create a VM from a specialized VHD.</span><span class="sxs-lookup"><span data-stu-id="d1e10-173">Use [this Azure Resource Manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) to create a VM from a specialized VHD.</span></span> <span data-ttu-id="d1e10-174">Click the `Deploy to Azure` button to open the Azure portal with the templated details populated for you.</span><span class="sxs-lookup"><span data-stu-id="d1e10-174">Click the `Deploy to Azure` button to open the Azure portal with the templated details populated for you.</span></span>
   * <span data-ttu-id="d1e10-175">If you want to retain all the previous settings for the VM, select *Edit template* to provide your existing VNet, subnet, network adapter, or public IP.</span><span class="sxs-lookup"><span data-stu-id="d1e10-175">If you want to retain all the previous settings for the VM, select *Edit template* to provide your existing VNet, subnet, network adapter, or public IP.</span></span>
   * <span data-ttu-id="d1e10-176">In the `OSDISKVHDURI` parameter text box, paste the URI of your source VHD obtain in the preceding step:</span><span class="sxs-lookup"><span data-stu-id="d1e10-176">In the `OSDISKVHDURI` parameter text box, paste the URI of your source VHD obtain in the preceding step:</span></span>
     
     ![Create a VM from template](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. <span data-ttu-id="d1e10-178">After the new VM is running, connect to the VM using Remote Desktop with the new password you specified in the `FixAzureVM.cmd` script.</span><span class="sxs-lookup"><span data-stu-id="d1e10-178">After the new VM is running, connect to the VM using Remote Desktop with the new password you specified in the `FixAzureVM.cmd` script.</span></span>
11. <span data-ttu-id="d1e10-179">From your remote session to the new VM, remove the following files to clean up the environment:</span><span class="sxs-lookup"><span data-stu-id="d1e10-179">From your remote session to the new VM, remove the following files to clean up the environment:</span></span>
    
    * <span data-ttu-id="d1e10-180">From %windir%\System32</span><span class="sxs-lookup"><span data-stu-id="d1e10-180">From %windir%\System32</span></span>
      * <span data-ttu-id="d1e10-181">remove FixAzureVM.cmd</span><span class="sxs-lookup"><span data-stu-id="d1e10-181">remove FixAzureVM.cmd</span></span>
    * <span data-ttu-id="d1e10-182">From %windir%\System32\GroupPolicy\Machine\\</span><span class="sxs-lookup"><span data-stu-id="d1e10-182">From %windir%\System32\GroupPolicy\Machine\\</span></span>
      * <span data-ttu-id="d1e10-183">remove scripts.ini</span><span class="sxs-lookup"><span data-stu-id="d1e10-183">remove scripts.ini</span></span>
    * <span data-ttu-id="d1e10-184">From %windir%\System32\GroupPolicy</span><span class="sxs-lookup"><span data-stu-id="d1e10-184">From %windir%\System32\GroupPolicy</span></span>
      * <span data-ttu-id="d1e10-185">remove gpt.ini (if gpt.ini existed before, and you renamed it to gpt.ini.bak, rename the .bak file back to gpt.ini)</span><span class="sxs-lookup"><span data-stu-id="d1e10-185">remove gpt.ini (if gpt.ini existed before, and you renamed it to gpt.ini.bak, rename the .bak file back to gpt.ini)</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1e10-186">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1e10-186">Next steps</span></span>
<span data-ttu-id="d1e10-187">If you still cannot connect using Remote Desktop, see the [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1e10-187">If you still cannot connect using Remote Desktop, see the [RDP troubleshooting guide](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="d1e10-188">The [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span><span class="sxs-lookup"><span data-stu-id="d1e10-188">The [detailed RDP troubleshooting guide](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) looks at troubleshooting methods rather than specific steps.</span></span> <span data-ttu-id="d1e10-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span><span class="sxs-lookup"><span data-stu-id="d1e10-189">You can also [open an Azure support request](https://azure.microsoft.com/support/options/) for hands-on assistance.</span></span>














