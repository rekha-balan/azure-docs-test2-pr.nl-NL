---
title: Mount Azure File Storage on Linux VMs using SMB | Microsoft Docs
description: How to mount Azure File Storage on Linux VMs using SMB with the Azure CLI 2.0
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
ms.date: 02/13/2017
ms.author: v-livech
ms.openlocfilehash: 3acfa09810d894244bb05436b87da73b0acf14fc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555590"
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="5823b-103">Mount Azure File Storage on Linux VMs using SMB</span><span class="sxs-lookup"><span data-stu-id="5823b-103">Mount Azure File Storage on Linux VMs using SMB</span></span>

<span data-ttu-id="5823b-104">This article shows you how to utilize the Azure File Storage service on a Linux VM using an SMB mount with the Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="5823b-104">This article shows you how to utilize the Azure File Storage service on a Linux VM using an SMB mount with the Azure CLI 2.0.</span></span> <span data-ttu-id="5823b-105">Azure File storage offers file shares in the cloud using the standard SMB protocol.</span><span class="sxs-lookup"><span data-stu-id="5823b-105">Azure File storage offers file shares in the cloud using the standard SMB protocol.</span></span> <span data-ttu-id="5823b-106">You can also perform these steps with the [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5823b-106">You can also perform these steps with the [Azure CLI 1.0](mount-azure-file-storage-on-linux-using-smb-nodejs.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span> <span data-ttu-id="5823b-107">The requirements are:</span><span class="sxs-lookup"><span data-stu-id="5823b-107">The requirements are:</span></span>

- [<span data-ttu-id="5823b-108">an Azure account</span><span class="sxs-lookup"><span data-stu-id="5823b-108">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="5823b-109">SSH public and private key files</span><span class="sxs-lookup"><span data-stu-id="5823b-109">SSH public and private key files</span></span>](mac-create-ssh-keys.md)

## <a name="quick-commands"></a><span data-ttu-id="5823b-110">Quick Commands</span><span class="sxs-lookup"><span data-stu-id="5823b-110">Quick Commands</span></span>

* <span data-ttu-id="5823b-111">A resource group</span><span class="sxs-lookup"><span data-stu-id="5823b-111">A resource group</span></span>
* <span data-ttu-id="5823b-112">An Azure virtual network</span><span class="sxs-lookup"><span data-stu-id="5823b-112">An Azure virtual network</span></span>
* <span data-ttu-id="5823b-113">A network security group with an SSH inbound</span><span class="sxs-lookup"><span data-stu-id="5823b-113">A network security group with an SSH inbound</span></span>
* <span data-ttu-id="5823b-114">A subnet</span><span class="sxs-lookup"><span data-stu-id="5823b-114">A subnet</span></span>
* <span data-ttu-id="5823b-115">An Azure storage account</span><span class="sxs-lookup"><span data-stu-id="5823b-115">An Azure storage account</span></span>
* <span data-ttu-id="5823b-116">Azure storage account keys</span><span class="sxs-lookup"><span data-stu-id="5823b-116">Azure storage account keys</span></span>
* <span data-ttu-id="5823b-117">An Azure File storage share</span><span class="sxs-lookup"><span data-stu-id="5823b-117">An Azure File storage share</span></span>
* <span data-ttu-id="5823b-118">A Linux VM</span><span class="sxs-lookup"><span data-stu-id="5823b-118">A Linux VM</span></span>

<span data-ttu-id="5823b-119">Replace any examples with your own settings.</span><span class="sxs-lookup"><span data-stu-id="5823b-119">Replace any examples with your own settings.</span></span>

### <a name="create-a-directory-for-the-local-mount"></a><span data-ttu-id="5823b-120">Create a directory for the local mount</span><span class="sxs-lookup"><span data-stu-id="5823b-120">Create a directory for the local mount</span></span>

```bash
mkdir -p /mnt/mymountpoint
```

### <a name="mount-the-file-storage-smb-share-to-the-mount-point"></a><span data-ttu-id="5823b-121">Mount the File storage SMB share to the mount point</span><span class="sxs-lookup"><span data-stu-id="5823b-121">Mount the File storage SMB share to the mount point</span></span>

```bash
sudo mount -t cifs //myaccountname.file.core.windows.net/mysharename /mymountpoint -o vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

### <a name="persist-the-mount-after-a-reboot"></a><span data-ttu-id="5823b-122">Persist the mount after a reboot</span><span class="sxs-lookup"><span data-stu-id="5823b-122">Persist the mount after a reboot</span></span>
<span data-ttu-id="5823b-123">To do so, add the following line to the `/etc/fstab`:</span><span class="sxs-lookup"><span data-stu-id="5823b-123">To do so, add the following line to the `/etc/fstab`:</span></span>

```bash
//myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="5823b-124">Detailed walkthrough</span><span class="sxs-lookup"><span data-stu-id="5823b-124">Detailed walkthrough</span></span>

<span data-ttu-id="5823b-125">File storage offers file shares in the cloud that use the standard SMB protocol.</span><span class="sxs-lookup"><span data-stu-id="5823b-125">File storage offers file shares in the cloud that use the standard SMB protocol.</span></span> <span data-ttu-id="5823b-126">With the latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="5823b-126">With the latest release of File storage, you can also mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="5823b-127">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span><span class="sxs-lookup"><span data-stu-id="5823b-127">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="5823b-128">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span><span class="sxs-lookup"><span data-stu-id="5823b-128">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span></span> <span data-ttu-id="5823b-129">That's because the same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span><span class="sxs-lookup"><span data-stu-id="5823b-129">That's because the same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="5823b-130">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span><span class="sxs-lookup"><span data-stu-id="5823b-130">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span></span> <span data-ttu-id="5823b-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span><span class="sxs-lookup"><span data-stu-id="5823b-131">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="5823b-132">For this detailed walkthrough, we create the prerequisites needed to first create the File storage share, and then mount it via SMB on a Linux VM.</span><span class="sxs-lookup"><span data-stu-id="5823b-132">For this detailed walkthrough, we create the prerequisites needed to first create the File storage share, and then mount it via SMB on a Linux VM.</span></span>

1. <span data-ttu-id="5823b-133">Create a resource group with [az group create](/cli/azure/group#create) to hold the file share.</span><span class="sxs-lookup"><span data-stu-id="5823b-133">Create a resource group with [az group create](/cli/azure/group#create) to hold the file share.</span></span>

    <span data-ttu-id="5823b-134">To create a resource group named `myResourceGroup` in the "West US" location, use the following example:</span><span class="sxs-lookup"><span data-stu-id="5823b-134">To create a resource group named `myResourceGroup` in the "West US" location, use the following example:</span></span>

    ```azurecli
    az group create --name myResourceGroup --location westus
    ```

2. <span data-ttu-id="5823b-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) to store the actual files.</span><span class="sxs-lookup"><span data-stu-id="5823b-135">Create an Azure storage account with [az storage account create](/cli/azure/storage/account#create) to store the actual files.</span></span>

    <span data-ttu-id="5823b-136">To create a storage account named mystorageaccount by using the Standard_LRS storage SKU, use the following example:</span><span class="sxs-lookup"><span data-stu-id="5823b-136">To create a storage account named mystorageaccount by using the Standard_LRS storage SKU, use the following example:</span></span>

    ```azurecli
    az storage account create --resource-group myResourceGroup \
        --name mystorageaccount \
        --location westus \
        --sku Standard_LRS
    ```

3. <span data-ttu-id="5823b-137">Show the storage account keys.</span><span class="sxs-lookup"><span data-stu-id="5823b-137">Show the storage account keys.</span></span>

    <span data-ttu-id="5823b-138">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span><span class="sxs-lookup"><span data-stu-id="5823b-138">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="5823b-139">When you switch to the second key in the pair, you create a new key pair.</span><span class="sxs-lookup"><span data-stu-id="5823b-139">When you switch to the second key in the pair, you create a new key pair.</span></span> <span data-ttu-id="5823b-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready to switch to.</span><span class="sxs-lookup"><span data-stu-id="5823b-140">New storage account keys are always created in pairs, ensuring that you always have at least one unused storage account key ready to switch to.</span></span>

    <span data-ttu-id="5823b-141">View the storage account keys with the [az storage account keys list](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="5823b-141">View the storage account keys with the [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="5823b-142">The storage account keys for the named `mystorageaccount` are listed in the following example:</span><span class="sxs-lookup"><span data-stu-id="5823b-142">The storage account keys for the named `mystorageaccount` are listed in the following example:</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount
    ```

    <span data-ttu-id="5823b-143">To extract a single key, use the `--query` flag.</span><span class="sxs-lookup"><span data-stu-id="5823b-143">To extract a single key, use the `--query` flag.</span></span> <span data-ttu-id="5823b-144">The following example extracts the first key (`[0]`):</span><span class="sxs-lookup"><span data-stu-id="5823b-144">The following example extracts the first key (`[0]`):</span></span>

    ```azurecli
    az storage account keys list --resource-group myResourceGroup \
        --account-name mystorageaccount \
        --query '[0].{Key:value}' --output tsv
    ```

4. <span data-ttu-id="5823b-145">Create the File storage share.</span><span class="sxs-lookup"><span data-stu-id="5823b-145">Create the File storage share.</span></span>

    <span data-ttu-id="5823b-146">The File storage share contains the SMB share with [az storage share create](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="5823b-146">The File storage share contains the SMB share with [az storage share create](/cli/azure/storage/share#create).</span></span> <span data-ttu-id="5823b-147">The quota is always expressed in gigabytes (GB).</span><span class="sxs-lookup"><span data-stu-id="5823b-147">The quota is always expressed in gigabytes (GB).</span></span> <span data-ttu-id="5823b-148">Pass in one of the keys from the preceding `az storage account keys list` command.</span><span class="sxs-lookup"><span data-stu-id="5823b-148">Pass in one of the keys from the preceding `az storage account keys list` command.</span></span> <span data-ttu-id="5823b-149">Create a share named mystorageshare with a 10-GB quota by using the following example:</span><span class="sxs-lookup"><span data-stu-id="5823b-149">Create a share named mystorageshare with a 10-GB quota by using the following example:</span></span>

    ```azurecli
    az storage share create --name mystorageshare \
        --quota 10 \
        --account-name mystorageaccount \
        --account-key nPOgPR<--snip-->4Q==
    ```

5. <span data-ttu-id="5823b-150">Create a mount-point directory.</span><span class="sxs-lookup"><span data-stu-id="5823b-150">Create a mount-point directory.</span></span>

    <span data-ttu-id="5823b-151">Create a local directory in the Linux file system to mount the SMB share to.</span><span class="sxs-lookup"><span data-stu-id="5823b-151">Create a local directory in the Linux file system to mount the SMB share to.</span></span> <span data-ttu-id="5823b-152">Anything written or read from the local mount directory is forwarded to the SMB share that's hosted on File storage.</span><span class="sxs-lookup"><span data-stu-id="5823b-152">Anything written or read from the local mount directory is forwarded to the SMB share that's hosted on File storage.</span></span> <span data-ttu-id="5823b-153">To create a local directory at /mnt/mymountdirectory, use the following example:</span><span class="sxs-lookup"><span data-stu-id="5823b-153">To create a local directory at /mnt/mymountdirectory, use the following example:</span></span>

    ```bash
    sudo mkdir -p /mnt/mymountdirectory
    ```

6. <span data-ttu-id="5823b-154">Mount the SMB share to the local directory.</span><span class="sxs-lookup"><span data-stu-id="5823b-154">Mount the SMB share to the local directory.</span></span>

    <span data-ttu-id="5823b-155">Provide your own storage account username and storage account key for the mount credentials as follows:</span><span class="sxs-lookup"><span data-stu-id="5823b-155">Provide your own storage account username and storage account key for the mount credentials as follows:</span></span>

    ```azurecli
    sudo mount -t cifs //myStorageAccount.file.core.windows.net/mystorageshare /mnt/mymountdirectory -o vers=3.0,username=mystorageaccount,password=mystorageaccountkey,dir_mode=0777,file_mode=0777
    ```

7. <span data-ttu-id="5823b-156">Persist the SMB mount through reboots.</span><span class="sxs-lookup"><span data-stu-id="5823b-156">Persist the SMB mount through reboots.</span></span>

    <span data-ttu-id="5823b-157">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span><span class="sxs-lookup"><span data-stu-id="5823b-157">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="5823b-158">To remount the SMB share on boot, add a line to the Linux /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="5823b-158">To remount the SMB share on boot, add a line to the Linux /etc/fstab.</span></span> <span data-ttu-id="5823b-159">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span><span class="sxs-lookup"><span data-stu-id="5823b-159">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span></span> <span data-ttu-id="5823b-160">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span><span class="sxs-lookup"><span data-stu-id="5823b-160">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span></span> <span data-ttu-id="5823b-161">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span><span class="sxs-lookup"><span data-stu-id="5823b-161">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span></span>

    ```bash
    //myaccountname.file.core.windows.net/mysharename /mymountpoint cifs vers=3.0,username=myaccountname,password=StorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
    ```

## <a name="next-steps"></a><span data-ttu-id="5823b-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="5823b-162">Next steps</span></span>

- [<span data-ttu-id="5823b-163">Using cloud-init to customize a Linux VM during creation</span><span class="sxs-lookup"><span data-stu-id="5823b-163">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="5823b-164">Add a disk to a Linux VM</span><span class="sxs-lookup"><span data-stu-id="5823b-164">Add a disk to a Linux VM</span></span>](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
- [<span data-ttu-id="5823b-165">Encrypt disks on a Linux VM by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="5823b-165">Encrypt disks on a Linux VM by using the Azure CLI</span></span>](encrypt-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
