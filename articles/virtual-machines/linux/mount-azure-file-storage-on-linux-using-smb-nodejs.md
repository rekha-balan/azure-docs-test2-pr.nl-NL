---
title: Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0 | Microsoft Docs
description: How to mount Azure File storage on Linux VMs by using SMB
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: vlivech
manager: timlt
editor: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/07/2016
ms.author: v-livech
ms.openlocfilehash: ab575bb3982e72654d75a6f8dff9cd456e1eb119
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553034"
---
# <a name="mount-azure-file-storage-on-linux-vms-by-using-smb-with-azure-cli-10"></a><span data-ttu-id="c2262-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="c2262-103">Mount Azure File storage on Linux VMs by using SMB with Azure CLI 1.0</span></span>

<span data-ttu-id="c2262-104">This article shows how to mount Azure File storage on a Linux VM by using the Server Message Block (SMB) protocol.</span><span class="sxs-lookup"><span data-stu-id="c2262-104">This article shows how to mount Azure File storage on a Linux VM by using the Server Message Block (SMB) protocol.</span></span> <span data-ttu-id="c2262-105">File storage offers file shares in the cloud via the standard SMB protocol.</span><span class="sxs-lookup"><span data-stu-id="c2262-105">File storage offers file shares in the cloud via the standard SMB protocol.</span></span> <span data-ttu-id="c2262-106">The requirements are:</span><span class="sxs-lookup"><span data-stu-id="c2262-106">The requirements are:</span></span>

* <span data-ttu-id="c2262-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="c2262-107">An [Azure account](https://azure.microsoft.com/pricing/free-trial/)</span></span>
* [<span data-ttu-id="c2262-108">Secure Shell (SSH) public and private key files</span><span class="sxs-lookup"><span data-stu-id="c2262-108">Secure Shell (SSH) public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="cli-versions-to-use"></a><span data-ttu-id="c2262-109">CLI versions to use</span><span class="sxs-lookup"><span data-stu-id="c2262-109">CLI versions to use</span></span>
<span data-ttu-id="c2262-110">You can complete the task by using one of the following command-line interface (CLI) versions:</span><span class="sxs-lookup"><span data-stu-id="c2262-110">You can complete the task by using one of the following command-line interface (CLI) versions:</span></span>

- <span data-ttu-id="c2262-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span><span class="sxs-lookup"><span data-stu-id="c2262-111">[Azure CLI 1.0](#quick-commands) – our CLI for the classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="c2262-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for the resource management deployment model</span><span class="sxs-lookup"><span data-stu-id="c2262-112">[Azure CLI 2.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)- our next generation CLI for the resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="c2262-113">Quick commands</span><span class="sxs-lookup"><span data-stu-id="c2262-113">Quick commands</span></span>
<span data-ttu-id="c2262-114">To accomplish the task quickly, follow the steps in this section.</span><span class="sxs-lookup"><span data-stu-id="c2262-114">To accomplish the task quickly, follow the steps in this section.</span></span> <span data-ttu-id="c2262-115">For more detailed information and context, begin at the ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span><span class="sxs-lookup"><span data-stu-id="c2262-115">For more detailed information and context, begin at the ["Detailed walkthrough"](mount-azure-file-storage-on-linux-using-smb.md#detailed-walkthrough) section.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="c2262-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c2262-116">Prerequisites</span></span>
* <span data-ttu-id="c2262-117">A resource group</span><span class="sxs-lookup"><span data-stu-id="c2262-117">A resource group</span></span>
* <span data-ttu-id="c2262-118">An Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="c2262-118">An Azure virtual network</span></span>
* <span data-ttu-id="c2262-119">A network security group with an SSH inbound</span><span class="sxs-lookup"><span data-stu-id="c2262-119">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="c2262-120">A subnet</span><span class="sxs-lookup"><span data-stu-id="c2262-120">A subnet</span></span>
* <span data-ttu-id="c2262-121">An Azure storage account</span><span class="sxs-lookup"><span data-stu-id="c2262-121">An Azure storage account</span></span>
* <span data-ttu-id="c2262-122">Azure storage account keys</span><span class="sxs-lookup"><span data-stu-id="c2262-122">Azure storage account keys</span></span>
* <span data-ttu-id="c2262-123">An Azure File storage share</span><span class="sxs-lookup"><span data-stu-id="c2262-123">An Azure File storage share</span></span>
* <span data-ttu-id="c2262-124">A Linux VM</span><span class="sxs-lookup"><span data-stu-id="c2262-124">A Linux VM</span></span>

<span data-ttu-id="c2262-125">Replace any examples with your own settings.</span><span class="sxs-lookup"><span data-stu-id="c2262-125">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-the-local-mount"></a><span data-ttu-id="c2262-126">Create a directory for the local mount</span><span class="sxs-lookup"><span data-stu-id="c2262-126">Create a directory for the local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-the-file-storage-smb-share-to-the-mount-point"></a><span data-ttu-id="c2262-127">Mount the File storage SMB share to the mount point</span><span class="sxs-lookup"><span data-stu-id="c2262-127">Mount the File storage SMB share to the mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-the-mount-after-a-reboot"></a><span data-ttu-id="c2262-128">Persist the mount after a reboot</span><span class="sxs-lookup"><span data-stu-id="c2262-128">Persist the mount after a reboot</span></span>
<span data-ttu-id="c2262-129">Add the following line to `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="c2262-129">Add the following line to `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="c2262-130">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="c2262-130">Detailed walkthrough</span></span>

<span data-ttu-id="c2262-131">File storage offers file shares in the cloud that use the standard SMB protocol.</span><span class="sxs-lookup"><span data-stu-id="c2262-131">File storage offers file shares in the cloud that use the standard SMB protocol.</span></span> <span data-ttu-id="c2262-132">With the latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="c2262-132">With the latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="c2262-133">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span><span class="sxs-lookup"><span data-stu-id="c2262-133">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="c2262-134">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span><span class="sxs-lookup"><span data-stu-id="c2262-134">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span></span> <span data-ttu-id="c2262-135">That's because the same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span><span class="sxs-lookup"><span data-stu-id="c2262-135">That's because the same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="c2262-136">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span><span class="sxs-lookup"><span data-stu-id="c2262-136">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span></span> <span data-ttu-id="c2262-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span><span class="sxs-lookup"><span data-stu-id="c2262-137">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="c2262-138">For this detailed walkthrough, we create the prerequisites needed to first create the File storage share, and then mount it via SMB on a Linux VM.</span><span class="sxs-lookup"><span data-stu-id="c2262-138">For this detailed walkthrough, we create the prerequisites needed to first create the File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="c2262-139">Create an Azure storage account by using the following code:</span><span class="sxs-lookup"><span data-stu-id="c2262-139">Create an Azure storage account by using the following code:</span></span>

    ```azurecli
    azure storage account create myStorageAccount \
    --sku-name lrs \
    --kind storage \
    -l westus \
    -g myResourceGroup
    ```

2. <span data-ttu-id="c2262-140">Show the storage account keys.</span><span class="sxs-lookup"><span data-stu-id="c2262-140">Show the storage account keys.</span></span>

    <span data-ttu-id="c2262-141">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span><span class="sxs-lookup"><span data-stu-id="c2262-141">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="c2262-142">When you switch to the second key in the pair, you create a new key pair.</span><span class="sxs-lookup"><span data-stu-id="c2262-142">When you switch to the second key in the pair, you create a new key pair.</span></span> <span data-ttu-id="c2262-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready to switch to.</span><span class="sxs-lookup"><span data-stu-id="c2262-143">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage key ready to switch to.</span></span> <span data-ttu-id="c2262-144">To show the storage account keys, use the following code:</span><span class="sxs-lookup"><span data-stu-id="c2262-144">To show the storage account keys, use the following code:</span></span>

    ```azurecli
    azure storage account keys list myStorageAccount \
    --resource-group myResourceGroup
    ```
3. <span data-ttu-id="c2262-145">Create the File storage share.</span><span class="sxs-lookup"><span data-stu-id="c2262-145">Create the File storage share.</span></span>

    <span data-ttu-id="c2262-146">The File storage share contains the SMB share.</span><span class="sxs-lookup"><span data-stu-id="c2262-146">The File storage share contains the SMB share.</span></span> <span data-ttu-id="c2262-147">The quota is always expressed in gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="c2262-147">The quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="c2262-148">To create the File storage share, use the following code:</span><span class="sxs-lookup"><span data-stu-id="c2262-148">To create the File storage share, use the following code:</span></span>

    ```azurecli
    azure storage share create mystorageshare \
    --quota 10 \
    --account-name myStorageAccount \
    --account-key nPOgPR<--snip-->4Q==
    ```

4. <span data-ttu-id="c2262-149">Create the mount-point directory.</span><span class="sxs-lookup"><span data-stu-id="c2262-149">Create the mount-point directory.</span></span>

    <span data-ttu-id="c2262-150">You must create a local directory in the Linux file system to mount the SMB share to.</span><span class="sxs-lookup"><span data-stu-id="c2262-150">You must create a local directory in the Linux file system to mount the SMB share to.</span></span> <span data-ttu-id="c2262-151">Anything written or read from the local mount directory is forwarded to the SMB share that's hosted on File storage.</span><span class="sxs-lookup"><span data-stu-id="c2262-151">Anything written or read from the local mount directory is forwarded to the SMB share that's hosted on File storage.</span></span> <span data-ttu-id="c2262-152">To create the directory, use the following code:</span><span class="sxs-lookup"><span data-stu-id="c2262-152">To create the directory, use the following code:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

5. <span data-ttu-id="c2262-153">Mount the SMB share by using the following code:</span><span class="sxs-lookup"><span data-stu-id="c2262-153">Mount the SMB share by using the following code:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=myStorageAccount,password=myStorageAccountkey,dir_mode=0777,file_mode=0777
    ```

6. <span data-ttu-id="c2262-154">Persist the SMB mount through reboots.</span><span class="sxs-lookup"><span data-stu-id="c2262-154">Persist the SMB mount through reboots.</span></span>

    <span data-ttu-id="c2262-155">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span><span class="sxs-lookup"><span data-stu-id="c2262-155">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="c2262-156">To remount the SMB share on boot, you must add a line to the Linux /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="c2262-156">To remount the SMB share on boot, you must add a line to the Linux /etc/fstab.</span></span> <span data-ttu-id="c2262-157">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span><span class="sxs-lookup"><span data-stu-id="c2262-157">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span></span> <span data-ttu-id="c2262-158">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span><span class="sxs-lookup"><span data-stu-id="c2262-158">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span></span> <span data-ttu-id="c2262-159">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span><span class="sxs-lookup"><span data-stu-id="c2262-159">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="c2262-160">Next steps</span><span class="sxs-lookup"><span data-stu-id="c2262-160">Next steps</span></span>

- [<span data-ttu-id="c2262-161">Using cloud-init to customize a Linux VM during creation</span><span class="sxs-lookup"><span data-stu-id="c2262-161">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="c2262-162">Add a disk to a Linux VM</span><span class="sxs-lookup"><span data-stu-id="c2262-162">Add a disk to a Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="c2262-163">Encrypt disks on a Linux VM by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="c2262-163">Encrypt disks on a Linux VM by using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
