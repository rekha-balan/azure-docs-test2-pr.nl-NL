---
title: Reset Linux VM password and SSH key from the CLI | Microsoft Docs
description: How to use the VMAccess extension from the Azure Command-Line Interface (CLI) to reset a Linux VM password or SSH key, fix the SSH configuration, and check disk consistency
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
editor: ''
tags: azure-service-management
ms.assetid: d975eb70-5ff1-40d1-a634-8dd2646dcd17
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 11/16/2016
ms.author: cynthn
ms.openlocfilehash: 54f3243247f8e84a519172c539c9b16720372061
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660723"
---
# <a name="how-to-reset-a-linux-vm-password-or-ssh-key-fix-the-ssh-configuration-and-check-disk-consistency-using-the-vmaccess-extension"></a><span data-ttu-id="feab1-103">How to reset a Linux VM password or SSH key, fix the SSH configuration, and check disk consistency using the VMAccess extension</span><span class="sxs-lookup"><span data-stu-id="feab1-103">How to reset a Linux VM password or SSH key, fix the SSH configuration, and check disk consistency using the VMAccess extension</span></span>
<span data-ttu-id="feab1-104">If you can't connect to a Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with the SSH configuration, use the VMAccessForLinux extension with the Azure CLI to reset the password or SSH key, fix the SSH configuration, and check disk consistency.</span><span class="sxs-lookup"><span data-stu-id="feab1-104">If you can't connect to a Linux virtual machine on Azure because of a forgotten password, an incorrect Secure Shell (SSH) key, or a problem with the SSH configuration, use the VMAccessForLinux extension with the Azure CLI to reset the password or SSH key, fix the SSH configuration, and check disk consistency.</span></span> 

> [!IMPORTANT] 
> <span data-ttu-id="feab1-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="feab1-105">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="feab1-106">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="feab1-106">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="feab1-107">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="feab1-107">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="feab1-108">Learn how to [perform these steps using the Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="feab1-108">Learn how to [perform these steps using the Resource Manager model](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span>

<span data-ttu-id="feab1-109">With the Azure CLI, you use the **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) to access commands.</span><span class="sxs-lookup"><span data-stu-id="feab1-109">With the Azure CLI, you use the **azure vm extension set** command from your command-line interface (Bash, Terminal, Command prompt) to access commands.</span></span> <span data-ttu-id="feab1-110">Run **azure help vm extension set** for detailed extension usage.</span><span class="sxs-lookup"><span data-stu-id="feab1-110">Run **azure help vm extension set** for detailed extension usage.</span></span>

<span data-ttu-id="feab1-111">With the Azure CLI, you can do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="feab1-111">With the Azure CLI, you can do the following tasks:</span></span>

* [<span data-ttu-id="feab1-112">Reset the password</span><span class="sxs-lookup"><span data-stu-id="feab1-112">Reset the password</span></span>](#pwresetcli)
* [<span data-ttu-id="feab1-113">Reset the SSH key</span><span class="sxs-lookup"><span data-stu-id="feab1-113">Reset the SSH key</span></span>](#sshkeyresetcli)
* [<span data-ttu-id="feab1-114">Reset the password and the SSH key</span><span class="sxs-lookup"><span data-stu-id="feab1-114">Reset the password and the SSH key</span></span>](#resetbothcli)
* [<span data-ttu-id="feab1-115">Create a new sudo user account</span><span class="sxs-lookup"><span data-stu-id="feab1-115">Create a new sudo user account</span></span>](#createnewsudocli)
* [<span data-ttu-id="feab1-116">Reset the SSH configuration</span><span class="sxs-lookup"><span data-stu-id="feab1-116">Reset the SSH configuration</span></span>](#sshconfigresetcli)
* [<span data-ttu-id="feab1-117">Delete a user</span><span class="sxs-lookup"><span data-stu-id="feab1-117">Delete a user</span></span>](#deletecli)
* [<span data-ttu-id="feab1-118">Display the status of the VMAccess extension</span><span class="sxs-lookup"><span data-stu-id="feab1-118">Display the status of the VMAccess extension</span></span>](#statuscli)
* [<span data-ttu-id="feab1-119">Check consistency of added disks</span><span class="sxs-lookup"><span data-stu-id="feab1-119">Check consistency of added disks</span></span>](#checkdisk)
* [<span data-ttu-id="feab1-120">Repair added disks on your Linux VM</span><span class="sxs-lookup"><span data-stu-id="feab1-120">Repair added disks on your Linux VM</span></span>](#repairdisk)

## <a name="prerequisites"></a><span data-ttu-id="feab1-121">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="feab1-121">Prerequisites</span></span>
<span data-ttu-id="feab1-122">You will need to do the following:</span><span class="sxs-lookup"><span data-stu-id="feab1-122">You will need to do the following:</span></span>

* <span data-ttu-id="feab1-123">You will need to [install the Azure CLI](../../../cli-install-nodejs.md) and [connect to your subscription](../../../xplat-cli-connect.md) to use Azure resources associated with your account.</span><span class="sxs-lookup"><span data-stu-id="feab1-123">You will need to [install the Azure CLI](../../../cli-install-nodejs.md) and [connect to your subscription](../../../xplat-cli-connect.md) to use Azure resources associated with your account.</span></span>
* <span data-ttu-id="feab1-124">Set the correct mode for the classic deployment model by typing the following at the command prompt:</span><span class="sxs-lookup"><span data-stu-id="feab1-124">Set the correct mode for the classic deployment model by typing the following at the command prompt:</span></span>
    ``` 
        azure config mode asm
    ```
* <span data-ttu-id="feab1-125">Have a new password or set of SSH keys, if you want to reset either one.</span><span class="sxs-lookup"><span data-stu-id="feab1-125">Have a new password or set of SSH keys, if you want to reset either one.</span></span> <span data-ttu-id="feab1-126">You don't need these if you want to reset the SSH configuration.</span><span class="sxs-lookup"><span data-stu-id="feab1-126">You don't need these if you want to reset the SSH configuration.</span></span>

## <a name="pwresetcli"></a><span data-ttu-id="feab1-127">Reset the password</span><span class="sxs-lookup"><span data-stu-id="feab1-127">Reset the password</span></span>
1. <span data-ttu-id="feab1-128">Create a file on your local computer named PrivateConf.json with these lines.</span><span class="sxs-lookup"><span data-stu-id="feab1-128">Create a file on your local computer named PrivateConf.json with these lines.</span></span> <span data-ttu-id="feab1-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span><span class="sxs-lookup"><span data-stu-id="feab1-129">Replace **myUserName** and **myP@ssW0rd** with your own user name and password and set your own date for expiration.</span></span>

    ```   
        {
        "username":"myUserName",
        "password":"myP@ssW0rd",
        "expiration":"2020-01-01"
        }
    ```
        
2. <span data-ttu-id="feab1-130">Run this command, substituting the name of your virtual machine for **myVM**.</span><span class="sxs-lookup"><span data-stu-id="feab1-130">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* –-private-config-path PrivateConf.json
    ```

## <a name="sshkeyresetcli"></a><span data-ttu-id="feab1-131">Reset the SSH key</span><span class="sxs-lookup"><span data-stu-id="feab1-131">Reset the SSH key</span></span>
1. <span data-ttu-id="feab1-132">Create a file named PrivateConf.json with these contents.</span><span class="sxs-lookup"><span data-stu-id="feab1-132">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="feab1-133">Replace the **myUserName** and **mySSHKey** values with your own information.</span><span class="sxs-lookup"><span data-stu-id="feab1-133">Replace the **myUserName** and **mySSHKey** values with your own information.</span></span>

    ```   
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey"
        }
    ```
2. <span data-ttu-id="feab1-134">Run this command, substituting the name of your virtual machine for **myVM**.</span><span class="sxs-lookup"><span data-stu-id="feab1-134">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>
   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json

## <a name="resetbothcli"></a><span data-ttu-id="feab1-135">Reset both the password and the SSH key</span><span class="sxs-lookup"><span data-stu-id="feab1-135">Reset both the password and the SSH key</span></span>
1. <span data-ttu-id="feab1-136">Create a file named PrivateConf.json with these contents.</span><span class="sxs-lookup"><span data-stu-id="feab1-136">Create a file named PrivateConf.json with these contents.</span></span> <span data-ttu-id="feab1-137">Replace the **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span><span class="sxs-lookup"><span data-stu-id="feab1-137">Replace the **myUserName**, **mySSHKey** and **myP@ssW0rd** values with your own information.</span></span>

    ``` 
        {
        "username":"myUserName",
        "ssh_key":"mySSHKey",
        "password":"myP@ssW0rd"
        }
    ```

2. <span data-ttu-id="feab1-138">Run this command, substituting the name of your virtual machine for **myVM**.</span><span class="sxs-lookup"><span data-stu-id="feab1-138">Run this command, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set MyVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="createnewsudocli"></a><span data-ttu-id="feab1-139">Create a new sudo user account</span><span class="sxs-lookup"><span data-stu-id="feab1-139">Create a new sudo user account</span></span>

<span data-ttu-id="feab1-140">If you forget your user name, you can use VMAccess to create a new one with the sudo authority.</span><span class="sxs-lookup"><span data-stu-id="feab1-140">If you forget your user name, you can use VMAccess to create a new one with the sudo authority.</span></span> <span data-ttu-id="feab1-141">In this case, the existing user name and password will not be modified.</span><span class="sxs-lookup"><span data-stu-id="feab1-141">In this case, the existing user name and password will not be modified.</span></span>

<span data-ttu-id="feab1-142">To create a new sudo user with password access, use the script in [Reset the password](#pwresetcli) and specify the new user name.</span><span class="sxs-lookup"><span data-stu-id="feab1-142">To create a new sudo user with password access, use the script in [Reset the password](#pwresetcli) and specify the new user name.</span></span>

<span data-ttu-id="feab1-143">To create a new sudo user with SSH key access, use the script in [Reset the SSH key](#sshkeyresetcli) and specify the new user name.</span><span class="sxs-lookup"><span data-stu-id="feab1-143">To create a new sudo user with SSH key access, use the script in [Reset the SSH key](#sshkeyresetcli) and specify the new user name.</span></span>

<span data-ttu-id="feab1-144">You can also use [Reset the password and the SSH key](#resetbothcli) to create a new user with both password and SSH key access.</span><span class="sxs-lookup"><span data-stu-id="feab1-144">You can also use [Reset the password and the SSH key](#resetbothcli) to create a new user with both password and SSH key access.</span></span>

## <a name="sshconfigresetcli"></a><span data-ttu-id="feab1-145">Reset the SSH configuration</span><span class="sxs-lookup"><span data-stu-id="feab1-145">Reset the SSH configuration</span></span>
<span data-ttu-id="feab1-146">If the SSH configuration is in an undesired state, you might also lose access to the VM.</span><span class="sxs-lookup"><span data-stu-id="feab1-146">If the SSH configuration is in an undesired state, you might also lose access to the VM.</span></span> <span data-ttu-id="feab1-147">You can use the VMAccess extension to reset the configuration to its default state.</span><span class="sxs-lookup"><span data-stu-id="feab1-147">You can use the VMAccess extension to reset the configuration to its default state.</span></span> <span data-ttu-id="feab1-148">To do so, you just need to set the “reset_ssh” key to “True”.</span><span class="sxs-lookup"><span data-stu-id="feab1-148">To do so, you just need to set the “reset_ssh” key to “True”.</span></span> <span data-ttu-id="feab1-149">The extension will restart the SSH server, open the SSH port on your VM, and reset the SSH configuration to default values.</span><span class="sxs-lookup"><span data-stu-id="feab1-149">The extension will restart the SSH server, open the SSH port on your VM, and reset the SSH configuration to default values.</span></span> <span data-ttu-id="feab1-150">The user account (name, password or SSH keys) will not be changed.</span><span class="sxs-lookup"><span data-stu-id="feab1-150">The user account (name, password or SSH keys) will not be changed.</span></span>

> [!NOTE]
> <span data-ttu-id="feab1-151">The SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span><span class="sxs-lookup"><span data-stu-id="feab1-151">The SSH configuration file that gets reset is located at /etc/ssh/sshd_config.</span></span>
> 
> 

1. <span data-ttu-id="feab1-152">Create a file named PrivateConf.json with this content.</span><span class="sxs-lookup"><span data-stu-id="feab1-152">Create a file named PrivateConf.json with this content.</span></span>

    ```   
        {
        "reset_ssh":"True"
        }
    ```

2. <span data-ttu-id="feab1-153">Run this command, substituting the name of your virtual machine for **myVM**.</span><span class="sxs-lookup"><span data-stu-id="feab1-153">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="deletecli"></a><span data-ttu-id="feab1-154">Delete a user</span><span class="sxs-lookup"><span data-stu-id="feab1-154">Delete a user</span></span>
<span data-ttu-id="feab1-155">If you want to delete a user account without logging into to the VM directly, you can use this script.</span><span class="sxs-lookup"><span data-stu-id="feab1-155">If you want to delete a user account without logging into to the VM directly, you can use this script.</span></span>

1. <span data-ttu-id="feab1-156">Create a file named PrivateConf.json with this content, substituting the user name to remove for **removeUserName**.</span><span class="sxs-lookup"><span data-stu-id="feab1-156">Create a file named PrivateConf.json with this content, substituting the user name to remove for **removeUserName**.</span></span> 

    ```   
        {
        "remove_user":"removeUserName"
        }
    ```

2. <span data-ttu-id="feab1-157">Run this command, substituting the name of your virtual machine for **myVM**.</span><span class="sxs-lookup"><span data-stu-id="feab1-157">Run this command, substituting the name of your virtual machine for **myVM**.</span></span> 

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --private-config-path PrivateConf.json
    ```

## <a name="statuscli"></a><span data-ttu-id="feab1-158">Display the status of the VMAccess extension</span><span class="sxs-lookup"><span data-stu-id="feab1-158">Display the status of the VMAccess extension</span></span>
<span data-ttu-id="feab1-159">To display the status of the VMAccess extension, run this command.</span><span class="sxs-lookup"><span data-stu-id="feab1-159">To display the status of the VMAccess extension, run this command.</span></span>

```
        azure vm extension get
```

## <a name='checkdisk'></a><span data-ttu-id="feab1-160">Check consistency of added disks</span><span class="sxs-lookup"><span data-stu-id="feab1-160">Check consistency of added disks</span></span>
<span data-ttu-id="feab1-161">To run fsck on all disks in your Linux virtual machine, you will need to do the following:</span><span class="sxs-lookup"><span data-stu-id="feab1-161">To run fsck on all disks in your Linux virtual machine, you will need to do the following:</span></span>

1. <span data-ttu-id="feab1-162">Create a file named PublicConf.json with this content.</span><span class="sxs-lookup"><span data-stu-id="feab1-162">Create a file named PublicConf.json with this content.</span></span> <span data-ttu-id="feab1-163">Check Disk takes a boolean for whether to check disks attached to your virtual machine or not.</span><span class="sxs-lookup"><span data-stu-id="feab1-163">Check Disk takes a boolean for whether to check disks attached to your virtual machine or not.</span></span> 

    ```   
        {   
        "check_disk": "true"
        }
    ```

2. <span data-ttu-id="feab1-164">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span><span class="sxs-lookup"><span data-stu-id="feab1-164">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json 
    ```

## <a name='repairdisk'></a><span data-ttu-id="feab1-165">Repair disks</span><span class="sxs-lookup"><span data-stu-id="feab1-165">Repair disks</span></span>
<span data-ttu-id="feab1-166">To repair disks that are not mounting or have mount configuration errors, use the VMAccess extension to reset the mount configuration on your Linux virtual machine.</span><span class="sxs-lookup"><span data-stu-id="feab1-166">To repair disks that are not mounting or have mount configuration errors, use the VMAccess extension to reset the mount configuration on your Linux virtual machine.</span></span> <span data-ttu-id="feab1-167">Substituting the name of your disk for **myDisk**.</span><span class="sxs-lookup"><span data-stu-id="feab1-167">Substituting the name of your disk for **myDisk**.</span></span>

1. <span data-ttu-id="feab1-168">Create a file named PublicConf.json with this content.</span><span class="sxs-lookup"><span data-stu-id="feab1-168">Create a file named PublicConf.json with this content.</span></span> 

    ```   
        {
        "repair_disk":"true",
        "disk_name":"myDisk"
        }
    ```

2. <span data-ttu-id="feab1-169">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span><span class="sxs-lookup"><span data-stu-id="feab1-169">Run this command to execute, substituting the name of your virtual machine for **myVM**.</span></span>

    ```   
        azure vm extension set myVM VMAccessForLinux Microsoft.OSTCExtensions 1.* --public-config-path PublicConf.json
    ```

## <a name="next-steps"></a><span data-ttu-id="feab1-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="feab1-170">Next steps</span></span>
* <span data-ttu-id="feab1-171">If you want to use Azure PowerShell cmdlets or Azure Resource Manager templates to reset the password or SSH key, fix the SSH configuration, and check disk consistency, see the [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span><span class="sxs-lookup"><span data-stu-id="feab1-171">If you want to use Azure PowerShell cmdlets or Azure Resource Manager templates to reset the password or SSH key, fix the SSH configuration, and check disk consistency, see the [VMAccess extension documentation on GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/VMAccess).</span></span> 
* <span data-ttu-id="feab1-172">You can also use the [Azure portal](https://portal.azure.com) to reset the password or SSH key of a Linux VM deployed in the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="feab1-172">You can also use the [Azure portal](https://portal.azure.com) to reset the password or SSH key of a Linux VM deployed in the classic deployment model.</span></span> <span data-ttu-id="feab1-173">You can't currently use the portal do to this for a Linux VM deployed in the Resource Manager deployment model.</span><span class="sxs-lookup"><span data-stu-id="feab1-173">You can't currently use the portal do to this for a Linux VM deployed in the Resource Manager deployment model.</span></span>
* <span data-ttu-id="feab1-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span><span class="sxs-lookup"><span data-stu-id="feab1-174">See [About virtual machine extensions and features](../extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) for more about using VM extensions for Azure virtual machines.</span></span>

