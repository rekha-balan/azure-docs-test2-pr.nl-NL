---
title: Reset access on Azure Linux VMs using the VMAccess Extension  | Microsoft Docs
description: Reset access on Azure Linux VMs using the VMAccess Extension.
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
ms.devlang: na
ms.topic: article
ms.date: 10/25/2016
ms.author: v-livech
ms.openlocfilehash: 81756346f74cfe8ff0c4b3c96c0a93680ba0bc15
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553908"
---
# <a name="manage-users-ssh-and-check-or-repair-disks-on-azure-linux-vms-using-the-vmaccess-extension-with-the-azure-cli-10"></a><span data-ttu-id="b5230-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension with the Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b5230-103">Manage users, SSH, and check or repair disks on Azure Linux VMs using the VMAccess Extension with the Azure CLI 1.0</span></span>
<span data-ttu-id="b5230-104">This article shows you how to use the Azure VMAcesss Extension to check or repair a disk, reset user access, manage user accounts, or reset the SSHD configuration on Linux.</span><span class="sxs-lookup"><span data-stu-id="b5230-104">This article shows you how to use the Azure VMAcesss Extension to check or repair a disk, reset user access, manage user accounts, or reset the SSHD configuration on Linux.</span></span> <span data-ttu-id="b5230-105">The article requires:</span><span class="sxs-lookup"><span data-stu-id="b5230-105">The article requires:</span></span>

* <span data-ttu-id="b5230-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span><span class="sxs-lookup"><span data-stu-id="b5230-106">an Azure account ([get a free trial](https://azure.microsoft.com/pricing/free-trial/)).</span></span>
* <span data-ttu-id="b5230-107">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span><span class="sxs-lookup"><span data-stu-id="b5230-107">the [Azure CLI](../../cli-install-nodejs.md) logged in with `azure login`.</span></span>
* <span data-ttu-id="b5230-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span><span class="sxs-lookup"><span data-stu-id="b5230-108">the Azure CLI *must be in* Azure Resource Manager mode `azure config mode arm`.</span></span>


## <a name="cli-versions-to-complete-the-task"></a><span data-ttu-id="b5230-109">CLI versions to complete the task</span><span class="sxs-lookup"><span data-stu-id="b5230-109">CLI versions to complete the task</span></span>
<span data-ttu-id="b5230-110">You can complete the task using one of the following CLI versions:</span><span class="sxs-lookup"><span data-stu-id="b5230-110">You can complete the task using one of the following CLI versions:</span></span>

- <span data-ttu-id="b5230-111">[Azure CLI 1.0](#quick-commands)– our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="b5230-111">[Azure CLI 1.0](#quick-commands)– our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="b5230-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="b5230-112">[Azure CLI 2.0](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="b5230-113">Quick commands</span><span class="sxs-lookup"><span data-stu-id="b5230-113">Quick commands</span></span>
<span data-ttu-id="b5230-114">There are two ways to use VMAccess on your Linux VMs:</span><span class="sxs-lookup"><span data-stu-id="b5230-114">There are two ways to use VMAccess on your Linux VMs:</span></span>

* <span data-ttu-id="b5230-115">Using the Azure CLI 1.0 and the required parameters.</span><span class="sxs-lookup"><span data-stu-id="b5230-115">Using the Azure CLI 1.0 and the required parameters.</span></span>
* <span data-ttu-id="b5230-116">Using raw JSON files that VMAccess processes and then act on.</span><span class="sxs-lookup"><span data-stu-id="b5230-116">Using raw JSON files that VMAccess processes and then act on.</span></span>

<span data-ttu-id="b5230-117">For the quick command section, we are going to use the Azure CLI 1.0 `azure vm reset-access` method.</span><span class="sxs-lookup"><span data-stu-id="b5230-117">For the quick command section, we are going to use the Azure CLI 1.0 `azure vm reset-access` method.</span></span> <span data-ttu-id="b5230-118">In the following command examples, replace the values that contain "example" with the values from your own environment.</span><span class="sxs-lookup"><span data-stu-id="b5230-118">In the following command examples, replace the values that contain "example" with the values from your own environment.</span></span>

## <a name="create-a-resource-group-and-linux-vm"></a><span data-ttu-id="b5230-119">Create a Resource Group and Linux VM</span><span class="sxs-lookup"><span data-stu-id="b5230-119">Create a Resource Group and Linux VM</span></span>
```bash
azure group create myResourceGroup westus
```

## <a name="create-a-debian-vm"></a><span data-ttu-id="b5230-120">Create a Debian VM</span><span class="sxs-lookup"><span data-stu-id="b5230-120">Create a Debian VM</span></span>
```azurecli
azure vm quick-create \
  -M ~/.ssh/id_rsa.pub \
  -u myAdminUser \
  -g myResourceGroup \
  -l westus \
  -y Linux \
  -n myVM \
  -Q Debian
```

## <a name="reset-root-password"></a><span data-ttu-id="b5230-121">Reset root password</span><span class="sxs-lookup"><span data-stu-id="b5230-121">Reset root password</span></span>
<span data-ttu-id="b5230-122">To reset the root password:</span><span class="sxs-lookup"><span data-stu-id="b5230-122">To reset the root password:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u root \
  -p myNewPassword
```

## <a name="ssh-key-reset"></a><span data-ttu-id="b5230-123">SSH key reset</span><span class="sxs-lookup"><span data-stu-id="b5230-123">SSH key reset</span></span>
<span data-ttu-id="b5230-124">To reset the SSH key of a non-root user:</span><span class="sxs-lookup"><span data-stu-id="b5230-124">To reset the SSH key of a non-root user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -M ~/.ssh/id_rsa.pub
```

## <a name="create-a-user"></a><span data-ttu-id="b5230-125">Create a user</span><span class="sxs-lookup"><span data-stu-id="b5230-125">Create a user</span></span>
<span data-ttu-id="b5230-126">To create a user:</span><span class="sxs-lookup"><span data-stu-id="b5230-126">To create a user:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -u myAdminUser \
  -p myAdminUserPassword
```

## <a name="remove-a-user"></a><span data-ttu-id="b5230-127">Remove a user</span><span class="sxs-lookup"><span data-stu-id="b5230-127">Remove a user</span></span>
```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM \
  -R myRemovedUser
```

## <a name="reset-sshd"></a><span data-ttu-id="b5230-128">Reset SSHD</span><span class="sxs-lookup"><span data-stu-id="b5230-128">Reset SSHD</span></span>
<span data-ttu-id="b5230-129">To reset the SSHD configuration:</span><span class="sxs-lookup"><span data-stu-id="b5230-129">To reset the SSHD configuration:</span></span>

```azurecli
azure vm reset-access \
  -g myResourceGroup \
  -n myVM
  -r
```


## <a name="detailed-walkthrough"></a><span data-ttu-id="b5230-130">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="b5230-130">Detailed walkthrough</span></span>
### <a name="vmaccess-defined"></a><span data-ttu-id="b5230-131">VMAccess defined:</span><span class="sxs-lookup"><span data-stu-id="b5230-131">VMAccess defined:</span></span>
<span data-ttu-id="b5230-132">The disk on your Linux VM is showing errors.</span><span class="sxs-lookup"><span data-stu-id="b5230-132">The disk on your Linux VM is showing errors.</span></span> <span data-ttu-id="b5230-133">You somehow reset the root password for your Linux VM or accidentally deleted your SSH private key.</span><span class="sxs-lookup"><span data-stu-id="b5230-133">You somehow reset the root password for your Linux VM or accidentally deleted your SSH private key.</span></span> <span data-ttu-id="b5230-134">If that happened back in the days of the datacenter, you would need to drive there and then open the KVM to get at the server console.</span><span class="sxs-lookup"><span data-stu-id="b5230-134">If that happened back in the days of the datacenter, you would need to drive there and then open the KVM to get at the server console.</span></span> <span data-ttu-id="b5230-135">Think of the Azure VMAccess extension as that KVM switch that allows you to access the console to reset access to Linux or perform disk level maintenance.</span><span class="sxs-lookup"><span data-stu-id="b5230-135">Think of the Azure VMAccess extension as that KVM switch that allows you to access the console to reset access to Linux or perform disk level maintenance.</span></span>

<span data-ttu-id="b5230-136">For the detailed walkthrough, we are going to use the long form of VMAccess, which uses raw JSON files.</span><span class="sxs-lookup"><span data-stu-id="b5230-136">For the detailed walkthrough, we are going to use the long form of VMAccess, which uses raw JSON files.</span></span>  <span data-ttu-id="b5230-137">These VMAccess JSON files can also be called from Azure templates.</span><span class="sxs-lookup"><span data-stu-id="b5230-137">These VMAccess JSON files can also be called from Azure templates.</span></span>

### <a name="using-vmaccess-to-check-or-repair-the-disk-of-a-linux-vm"></a><span data-ttu-id="b5230-138">Using VMAccess to check or repair the disk of a Linux VM</span><span class="sxs-lookup"><span data-stu-id="b5230-138">Using VMAccess to check or repair the disk of a Linux VM</span></span>
<span data-ttu-id="b5230-139">Using VMAccess you can do a fsck run on the disk under your Linux VM.</span><span class="sxs-lookup"><span data-stu-id="b5230-139">Using VMAccess you can do a fsck run on the disk under your Linux VM.</span></span>  <span data-ttu-id="b5230-140">You can also do a disk check and a disk repair using a VMAccess.</span><span class="sxs-lookup"><span data-stu-id="b5230-140">You can also do a disk check and a disk repair using a VMAccess.</span></span>

<span data-ttu-id="b5230-141">To check, and then repair the disk use this VMAccess script:</span><span class="sxs-lookup"><span data-stu-id="b5230-141">To check, and then repair the disk use this VMAccess script:</span></span>

`disk_check_repair.json`

```json
{
  "check_disk": "true",
  "repair_disk": "true, user-disk-name"
}
```

<span data-ttu-id="b5230-142">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="b5230-142">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path disk_check_repair.json
```

### <a name="using-vmaccess-to-reset-user-access-to-linux"></a><span data-ttu-id="b5230-143">Using VMAccess to reset user access to Linux</span><span class="sxs-lookup"><span data-stu-id="b5230-143">Using VMAccess to reset user access to Linux</span></span>
<span data-ttu-id="b5230-144">If you have lost access to root on your Linux VM, you can launch a VMAccess script to reset the root password.</span><span class="sxs-lookup"><span data-stu-id="b5230-144">If you have lost access to root on your Linux VM, you can launch a VMAccess script to reset the root password.</span></span>

<span data-ttu-id="b5230-145">To reset the root password, use this VMAccess script:</span><span class="sxs-lookup"><span data-stu-id="b5230-145">To reset the root password, use this VMAccess script:</span></span>

`reset_root_password.json`

```json
{
  "username":"root",
  "password":"myNewPassword"
}
```

<span data-ttu-id="b5230-146">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="b5230-146">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_root_password.json
```

<span data-ttu-id="b5230-147">To reset the SSH key of a non-root user, use this VMAccess script:</span><span class="sxs-lookup"><span data-stu-id="b5230-147">To reset the SSH key of a non-root user, use this VMAccess script:</span></span>

`reset_ssh_key.json`

```json
{
  "username":"myAdminUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myAdminUser@myVM" 
}
```

<span data-ttu-id="b5230-148">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="b5230-148">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_ssh_key.json
```

### <a name="using-vmaccess-to-manage-user-accounts-on-linux"></a><span data-ttu-id="b5230-149">Using VMAccess to manage user accounts on Linux</span><span class="sxs-lookup"><span data-stu-id="b5230-149">Using VMAccess to manage user accounts on Linux</span></span>
<span data-ttu-id="b5230-150">VMAccess is a Python script that can be used to manage users on your Linux VM without logging in and using sudo or the root account.</span><span class="sxs-lookup"><span data-stu-id="b5230-150">VMAccess is a Python script that can be used to manage users on your Linux VM without logging in and using sudo or the root account.</span></span>

<span data-ttu-id="b5230-151">To create a user, use this VMAccess script:</span><span class="sxs-lookup"><span data-stu-id="b5230-151">To create a user, use this VMAccess script:</span></span>

`create_new_user.json`

```json
{
  "username":"myNewUser",
  "ssh_key":"ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAACAQCZ3S7gGp3rcbKmG2Y4vGZFMuMZCwoUzZNG1vHY7P2XV2x9FfAhy8iGD+lF8UdjFX3t5ebMm6BnnMh8fHwkTRdOt3LDQq8o8ElTBrZaKPxZN2thMZnODs5Hlemb2UX0oRIGRcvWqsd4oJmxsXa/Si98Wa6RHWbc9QZhw80KAcOVhmndZAZAGR+Wq6yslNo5TMOr1/ZyQAook5C4FtcSGn3Y+WczaoGWIxG4ZaWk128g79VIeJcIQqOjPodHvQAhll7qDlItVvBfMOben3GyhYTm7k4YwlEdkONm4yV/UIW0la1rmyztSBQIm9sZmSq44XXgjVmDHNF8UfCZ1ToE4r2SdwTmZv00T2i5faeYnHzxiLPA3Enub7iUo5IdwFArnqad7MO1SY1kLemhX9eFjLWN4mJe56Fu4NiWJkR9APSZQrYeKaqru4KUC68QpVasNJHbuxPSf/PcjF3cjO1+X+4x6L1H5HTPuqUkyZGgDO4ynUHbko4dhlanALcriF7tIfQR9i2r2xOyv5gxJEW/zztGqWma/d4rBoPjnf6tO7rLFHXMt/DVTkAfn5woYtLDwkn5FMyvThRmex3BDf0gujoI1y6cOWLe9Y5geNX0oj+MXg/W0cXAtzSFocstV1PoVqy883hNoeQZ3mIGB3Q0rIUm5d9MA2bMMt31m1g3Sin6EQ== myNewUser@myVM",
  "password":"myNewUserPassword"
}
```

<span data-ttu-id="b5230-152">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="b5230-152">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path create_new_user.json
```

<span data-ttu-id="b5230-153">To delete a user, use this VMAccess script:</span><span class="sxs-lookup"><span data-stu-id="b5230-153">To delete a user, use this VMAccess script:</span></span>

`remove_user.json`

```json
{
  "remove_user":"myDeletedUser"
}
```

<span data-ttu-id="b5230-154">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="b5230-154">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path remove_user.json
```

### <a name="using-vmaccess-to-reset-the-sshd-configuration"></a><span data-ttu-id="b5230-155">Using VMAccess to reset the SSHD configuration</span><span class="sxs-lookup"><span data-stu-id="b5230-155">Using VMAccess to reset the SSHD configuration</span></span>
<span data-ttu-id="b5230-156">If you make changes to the Linux VMs SSHD configuration and close the SSH connection before verifying the changes, you may be prevented from SSH'ing back in.</span><span class="sxs-lookup"><span data-stu-id="b5230-156">If you make changes to the Linux VMs SSHD configuration and close the SSH connection before verifying the changes, you may be prevented from SSH'ing back in.</span></span>  <span data-ttu-id="b5230-157">VMAccess can be used to reset the SSHD configuration back to a known good configuration without being logged in over SSH.</span><span class="sxs-lookup"><span data-stu-id="b5230-157">VMAccess can be used to reset the SSHD configuration back to a known good configuration without being logged in over SSH.</span></span>

<span data-ttu-id="b5230-158">To reset the SSHD configuration use this VMAccess script:</span><span class="sxs-lookup"><span data-stu-id="b5230-158">To reset the SSHD configuration use this VMAccess script:</span></span>

`reset_sshd.json`

```json
{
  "reset_ssh": true
}
```

<span data-ttu-id="b5230-159">Execute the VMAccess script with:</span><span class="sxs-lookup"><span data-stu-id="b5230-159">Execute the VMAccess script with:</span></span>

```azurecli
azure vm extension set \
  myResourceGroup \
  myVM \
  VMAccessForLinux \
  Microsoft.OSTCExtensions * \
  --private-config-path reset_sshd.json
```

## <a name="next-steps"></a><span data-ttu-id="b5230-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5230-160">Next steps</span></span>
<span data-ttu-id="b5230-161">Updating Linux using Azure VMAccess Extensions is one method to make changes on a running Linux VM.</span><span class="sxs-lookup"><span data-stu-id="b5230-161">Updating Linux using Azure VMAccess Extensions is one method to make changes on a running Linux VM.</span></span>  <span data-ttu-id="b5230-162">You can also use tools like cloud-init and Azure Templates to modify your Linux VM on boot.</span><span class="sxs-lookup"><span data-stu-id="b5230-162">You can also use tools like cloud-init and Azure Templates to modify your Linux VM on boot.</span></span>

[<span data-ttu-id="b5230-163">About virtual machine extensions and features</span><span class="sxs-lookup"><span data-stu-id="b5230-163">About virtual machine extensions and features</span></span>](../windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="b5230-164">Authoring Azure Resource Manager templates with Linux VM extensions</span><span class="sxs-lookup"><span data-stu-id="b5230-164">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>](../windows/extensions-authoring-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

[<span data-ttu-id="b5230-165">Using cloud-init to customize a Linux VM during creation</span><span class="sxs-lookup"><span data-stu-id="b5230-165">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

