---
title: Reset access with the VMAccess Extension and Azure CLI 2.0 | Microsoft Docs
description: How to manage users and reset access on Linux VMs using the VMAccess Extension and the Azure CLI 2.0
services: virtual-machines-linux
documentationcenter: ''
author: vlivech
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: 261a9646-1f93-407e-951e-0be7226b3064
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: azurecli
ms.topic: article
ms.date: 02/16/2017
ms.author: v-livech
ms.openlocfilehash: 5966319bf486d2323738c3db88b2d31330ff9834
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551177"
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-linux-vms-using-the-vmaccess-extension-with-the-azure-cli-20"></a><span data-ttu-id="5e808-103">Manage users, SSH, and check or repair disks on Linux VMs using the VMAccess Extension with the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="5e808-103">Manage users, SSH, and check or repair disks on Linux VMs using the VMAccess Extension with the Azure CLI 2.0</span></span>
<span data-ttu-id="5e808-104">The disk on your Linux VM is showing errors.</span><span class="sxs-lookup"><span data-stu-id="5e808-104">The disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="5e808-105">You somehow reset the root password for your Linux VM or accidentally deleted your SSH private key.</span><span class="sxs-lookup"><span data-stu-id="5e808-105">You somehow reset the root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="5e808-106">If that happened back in the days of the datacenter, you would need to drive there and then open the KVM to get at the server console.</span><span class="sxs-lookup"><span data-stu-id="5e808-106">If that happened back in the days of the datacenter, you would need to drive there and then open the KVM to get at the server console.</span></span> <span data-ttu-id="5e808-107">Think of the Azure VMAccess extension as that KVM switch that allows you to access the console to reset access to Linux or perform disk level maintenance.</span><span class="sxs-lookup"><span data-stu-id="5e808-107">Think of the Azure VMAccess extension as that KVM switch that allows you to access the console to reset access to Linux or perform disk level maintenance.</span></span>

<span data-ttu-id="5e808-108">This article shows you how to use the Azure VMAcesss Extension to check or repair a disk, reset user access, manage user accounts, or reset the SSHD configuration on Linux.</span><span class="sxs-lookup"><span data-stu-id="5e808-108">This article shows you how to use the Azure VMAcesss Extension to check or repair a disk, reset user access, manage user accounts, or reset the SSHD configuration on Linux.</span></span> <span data-ttu-id="5e808-109">You can also perform these steps with the [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5e808-109">You can also perform these steps with the [Azure CLI 1.0](using-vmaccess-extension-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>


## <a name="ways-to-use-the-vmaccess-extension"></a><span data-ttu-id="5e808-110">Ways to use the VMAccess Extension</span><span class="sxs-lookup"><span data-stu-id="5e808-110">Ways to use the VMAccess Extension</span></span>
<span data-ttu-id="5e808-111">There are two ways that you can use the VMAccess Extension on your Linux VMs:</span><span class="sxs-lookup"><span data-stu-id="5e808-111">There are two ways that you can use the VMAccess Extension on your Linux VMs:</span></span>

* <span data-ttu-id="5e808-112">Use the Azure CLI 2.0 and the required parameters.</span><span class="sxs-lookup"><span data-stu-id="5e808-112">Use the Azure CLI 2.0 and the required parameters.</span></span>
* <span data-ttu-id="5e808-113">[Use raw JSON files that the VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span><span class="sxs-lookup"><span data-stu-id="5e808-113">[Use raw JSON files that the VMAccess Extension process](#use-json-files-and-the-vmaccess-extension) and then act on.</span></span>

<span data-ttu-id="5e808-114">The following examples use [az vm access](/cli/azure/vm/access) along with the appropriate parameters.</span><span class="sxs-lookup"><span data-stu-id="5e808-114">The following examples use [az vm access](/cli/azure/vm/access) along with the appropriate parameters.</span></span> <span data-ttu-id="5e808-115">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span><span class="sxs-lookup"><span data-stu-id="5e808-115">To perform these steps, you need the latest [Azure CLI 2.0](/cli/azure/install-az-cli2) installed and logged in to an Azure account using [az login](/cli/azure/#login).</span></span>

## <a name="reset-ssh-key"></a><span data-ttu-id="5e808-116">Reset SSH key</span><span class="sxs-lookup"><span data-stu-id="5e808-116">Reset SSH key</span></span>
<span data-ttu-id="5e808-117">The following example resets the SSH key for the user `azureuser` on the VM named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5e808-117">The following example resets the SSH key for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm access set-linux-user \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="reset-password"></a><span data-ttu-id="5e808-118">Reset password</span><span class="sxs-lookup"><span data-stu-id="5e808-118">Reset password</span></span>
<span data-ttu-id="5e808-119">The following example resets the password for the user `azureuser` on the VM named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5e808-119">The following example resets the password for the user `azureuser` on the VM named `myVM`:</span></span>

```azurecli
az vm access set-linux-user \
  --resource-group myResourceGroup \
  --name myVM \
  --username azureuser \
  --password myNewPassword
```

## <a name="reset-sshd"></a><span data-ttu-id="5e808-120">Reset SSHD</span><span class="sxs-lookup"><span data-stu-id="5e808-120">Reset SSHD</span></span>
<span data-ttu-id="5e808-121">The following example resets the SSHD configuration on a VM named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5e808-121">The following example resets the SSHD configuration on a VM named `myVM`:</span></span>

```azurecli
az vm access reset-linux-ssh \
  --resource-group myResourceGroup \
  --name myVM
```

## <a name="create-a-user"></a><span data-ttu-id="5e808-122">Create a user</span><span class="sxs-lookup"><span data-stu-id="5e808-122">Create a user</span></span>
<span data-ttu-id="5e808-123">The following example creates a user named `myNewUser` using an SSH key for authentication on the VM named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5e808-123">The following example creates a user named `myNewUser` using an SSH key for authentication on the VM named `myVM`:</span></span>

```azurecli
az vm access set-linux-user \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser \
  --ssh-key-value ~/.ssh/id_rsa.pub
```

## <a name="deletes-a-user"></a><span data-ttu-id="5e808-124">Deletes a user</span><span class="sxs-lookup"><span data-stu-id="5e808-124">Deletes a user</span></span>
<span data-ttu-id="5e808-125">The following example deletes a user named `myNewUser` on the VM named `myVM`:</span><span class="sxs-lookup"><span data-stu-id="5e808-125">The following example deletes a user named `myNewUser` on the VM named `myVM`:</span></span>

```azurecli
az vm access delete-linux-user \
  --resource-group myResourceGroup \
  --name myVM \
  --username myNewUser
```


## <a name="use-json-files-and-the-vmaccess-extension"></a><span data-ttu-id="5e808-126">Use JSON files and the VMAccess Extension</span><span class="sxs-lookup"><span data-stu-id="5e808-126">Use JSON files and the VMAccess Extension</span></span>
<span data-ttu-id="5e808-127">The following examples use raw JSON files.</span><span class="sxs-lookup"><span data-stu-id="5e808-127">The following examples use raw JSON files.</span></span> <span data-ttu-id="5e808-128">Use [az vm extension set](/cli/azure/vm/extension#set) to then call your JSON files.</span><span class="sxs-lookup"><span data-stu-id="5e808-128">Use [az vm extension set](/cli/azure/vm/extension#set) to then call your JSON files.</span></span> <span data-ttu-id="5e808-129">These JSON files can also be called from Azure templates.</span><span class="sxs-lookup"><span data-stu-id="5e808-129">These JSON files can also be called from Azure templates.</span></span> 

### <a name="reset-user-access"></a><span data-ttu-id="5e808-130">Reset user access</span><span class="sxs-lookup"><span data-stu-id="5e808-130">Reset user access</span></span>
<span data-ttu-id="5e808-131">If you have lost access to root on your Linux VM, you can launch a VMAccess script to reset a user password.</span><span class="sxs-lookup"><span data-stu-id="5e808-131">If you have lost access to root on your Linux VM, you can launch a VMAccess script to reset a user password.</span></span>

<span data-ttu-id="5e808-132">To reset the SSH key of a user, create a file named `reset_ssh_key.json` and add the following content:</span><span class="sxs-lookup"><span data-stu-id="5e808-132">To reset the SSH key of a user, create a file named `reset_ssh_key.json` and add the following content:</span></span>

```json
{
  "username":"azureuser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== azureuser@myVM"
}
```

<span data-ttu-id="5e808-133">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="5e808-133">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_ssh_key.json
```

<span data-ttu-id="5e808-134">To reset a user password, create a file named `reset_user_password.json` and add the following content:</span><span class="sxs-lookup"><span data-stu-id="5e808-134">To reset a user password, create a file named `reset_user_password.json` and add the following content:</span></span>

```json
{
  "username":"azureuser",
  "password":"myNewPassword" 
}
```

<span data-ttu-id="5e808-135">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="5e808-135">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_user_password.json
```

### <a name="reset-ssh"></a><span data-ttu-id="5e808-136">Reset SSH</span><span class="sxs-lookup"><span data-stu-id="5e808-136">Reset SSH</span></span>
<span data-ttu-id="5e808-137">If you make changes to the Linux VMs SSHD configuration and close the SSH connection before verifying the changes, you may be prevented from SSH'ing back in.</span><span class="sxs-lookup"><span data-stu-id="5e808-137">If you make changes to the Linux VMs SSHD configuration and close the SSH connection before verifying the changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="5e808-138">VMAccess can be used to reset the SSHD configuration back to a known good configuration without being logged in over SSH.</span><span class="sxs-lookup"><span data-stu-id="5e808-138">VMAccess can be used to reset the SSHD configuration back to a known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="5e808-139">To reset the SSHD configuration, create a file named `reset_sshd.json` and add the following content:</span><span class="sxs-lookup"><span data-stu-id="5e808-139">To reset the SSHD configuration, create a file named `reset_sshd.json` and add the following content:</span></span>

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="5e808-140">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="5e808-140">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings reset_sshd.json
```

### <a name="manage-users"></a><span data-ttu-id="5e808-141">Manage users</span><span class="sxs-lookup"><span data-stu-id="5e808-141">Manage users</span></span>
<span data-ttu-id="5e808-142">VMAccess is a Python script that can be used to manage users on your Linux VM without logging in and using sudo or the root account.</span><span class="sxs-lookup"><span data-stu-id="5e808-142">VMAccess is a Python script that can be used to manage users on your Linux VM without logging in and using sudo or the root account.</span></span>

<span data-ttu-id="5e808-143">To create a user, create a file named `create_new_user.json` and add the following content:</span><span class="sxs-lookup"><span data-stu-id="5e808-143">To create a user, create a file named `create_new_user.json` and add the following content:</span></span>

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="5e808-144">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="5e808-144">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings create_new_user.json
```

<span data-ttu-id="5e808-145">To delete a user, create a file named `delete_user.json` and add the following content:</span><span class="sxs-lookup"><span data-stu-id="5e808-145">To delete a user, create a file named `delete_user.json` and add the following content:</span></span>

```json
{
  "remove_user":"myDeleteUser"
}
```

<span data-ttu-id="5e808-146">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="5e808-146">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings delete_user.json
```

### <a name="check-or-repair-the-disk"></a><span data-ttu-id="5e808-147">Check or repair the disk</span><span class="sxs-lookup"><span data-stu-id="5e808-147">Check or repair the disk</span></span>
<span data-ttu-id="5e808-148">Using VMAccess you can do a fsck run on the disk under your Linux VM.</span><span class="sxs-lookup"><span data-stu-id="5e808-148">Using VMAccess you can do a fsck run on the disk under your Linux VM.</span></span> <span data-ttu-id="5e808-149">You can also do a disk check and a disk repair using a VMAccess.</span><span class="sxs-lookup"><span data-stu-id="5e808-149">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="5e808-150">To check, and then repair the disk use this VMAccess script, create a file named `disk_check_repair.json` and add the following content:</span><span class="sxs-lookup"><span data-stu-id="5e808-150">To check, and then repair the disk use this VMAccess script, create a file named `disk_check_repair.json` and add the following content:</span></span>

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="5e808-151">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="5e808-151">Execute the VMAccess script with:</span></span>

```azurecli
az vm extension set \
  --resource-group myResourceGroup \
  --vm-name myVM \
  --name VMAccessForLinux \
  --publisher Microsoft.OSTCExtensions \
  --version 1.4 \
  --protected-settings disk_check_repair.json
```

## <a name="next-steps"></a><span data-ttu-id="5e808-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e808-152">Next steps</span></span>
<span data-ttu-id="5e808-153">Updating Linux using Azure VMAccess Extension is one method to make changes on a running Linux VM.</span><span class="sxs-lookup"><span data-stu-id="5e808-153">Updating Linux using Azure VMAccess Extension is one method to make changes on a running Linux VM.</span></span> <span data-ttu-id="5e808-154">You can also use tools like cloud-init and Azure Resource Manager templates to modify your Linux VM on boot.</span><span class="sxs-lookup"><span data-stu-id="5e808-154">You can also use tools like cloud-init and Azure Resource Manager templates to modify your Linux VM on boot.</span></span>

[<span data-ttu-id="5e808-155">About virtual machine extensions and features</span><span class="sxs-lookup"><span data-stu-id="5e808-155">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="5e808-156">Authoring Azure Resource Manager templates with Linux VM extensions</span><span class="sxs-lookup"><span data-stu-id="5e808-156">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="5e808-157">Using cloud-init to customize a Linux VM during creation</span><span class="sxs-lookup"><span data-stu-id="5e808-157">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

