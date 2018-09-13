---
title: Mount Azure File storage on Linux VMs using SMB | Microsoft Docs
description: How to mount Azure File storage on Linux VMs using SMB with the Azure CLI
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: cynthn
manager: jeconnoc
editor: ''
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 06/28/2018
ms.author: cynthn
ms.openlocfilehash: 7669775e4ff5c75fd4a2a472b972e1d280b646d9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44828087"
---
# <a name="mount-azure-file-storage-on-linux-vms-using-smb"></a><span data-ttu-id="33e53-103">Mount Azure File storage on Linux VMs using SMB</span><span class="sxs-lookup"><span data-stu-id="33e53-103">Mount Azure File storage on Linux VMs using SMB</span></span>


<span data-ttu-id="33e53-104">This article shows you how to use the Azure File storage service on a Linux VM using an SMB mount with the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="33e53-104">This article shows you how to use the Azure File storage service on a Linux VM using an SMB mount with the Azure CLI.</span></span> <span data-ttu-id="33e53-105">Azure File storage offers file shares in the cloud using the standard SMB protocol.</span><span class="sxs-lookup"><span data-stu-id="33e53-105">Azure File storage offers file shares in the cloud using the standard SMB protocol.</span></span> 

<span data-ttu-id="33e53-106">File storage offers file shares in the cloud that use the standard SMB protocol.</span><span class="sxs-lookup"><span data-stu-id="33e53-106">File storage offers file shares in the cloud that use the standard SMB protocol.</span></span> <span data-ttu-id="33e53-107">You can mount a file share from any OS that supports SMB 3.0.</span><span class="sxs-lookup"><span data-stu-id="33e53-107">You can mount a file share from any OS that supports SMB 3.0.</span></span> <span data-ttu-id="33e53-108">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span><span class="sxs-lookup"><span data-stu-id="33e53-108">When you use an SMB mount on Linux, you get easy backups to a robust, permanent archiving storage location that is supported by an SLA.</span></span>

<span data-ttu-id="33e53-109">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span><span class="sxs-lookup"><span data-stu-id="33e53-109">Moving files from a VM to an SMB mount that's hosted on File storage is a great way to debug logs.</span></span> <span data-ttu-id="33e53-110">The same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span><span class="sxs-lookup"><span data-stu-id="33e53-110">The same SMB share can be mounted locally to your Mac, Linux, or Windows workstation.</span></span> <span data-ttu-id="33e53-111">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span><span class="sxs-lookup"><span data-stu-id="33e53-111">SMB isn't the best solution for streaming Linux or application logs in real time, because the SMB protocol is not built to handle such heavy logging duties.</span></span> <span data-ttu-id="33e53-112">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span><span class="sxs-lookup"><span data-stu-id="33e53-112">A dedicated, unified logging layer tool such as Fluentd would be a better choice than SMB for collecting Linux and application logging output.</span></span>

<span data-ttu-id="33e53-113">This guide requires that you're running the Azure CLI version 2.0.4 or later.</span><span class="sxs-lookup"><span data-stu-id="33e53-113">This guide requires that you're running the Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="33e53-114">Run **az --version** to find the version.</span><span class="sxs-lookup"><span data-stu-id="33e53-114">Run **az --version** to find the version.</span></span> <span data-ttu-id="33e53-115">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="33e53-115">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-resource-group"></a><span data-ttu-id="33e53-116">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="33e53-116">Create a resource group</span></span>

<span data-ttu-id="33e53-117">Create a resource group named *myResourceGroup* in the *East US* location.</span><span class="sxs-lookup"><span data-stu-id="33e53-117">Create a resource group named *myResourceGroup* in the *East US* location.</span></span>

```bash
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-storage-account"></a><span data-ttu-id="33e53-118">Create a storage account</span><span class="sxs-lookup"><span data-stu-id="33e53-118">Create a storage account</span></span>

<span data-ttu-id="33e53-119">Create a new storage account, within the resource group that you created, using [az storage account create](/cli/azure/storage/account#create).</span><span class="sxs-lookup"><span data-stu-id="33e53-119">Create a new storage account, within the resource group that you created, using [az storage account create](/cli/azure/storage/account#create).</span></span> <span data-ttu-id="33e53-120">This example creates a storage account named *mySTORAGEACCT<random number>* and puts the name of that storage account in the variable **STORAGEACCT**.</span><span class="sxs-lookup"><span data-stu-id="33e53-120">This example creates a storage account named *mySTORAGEACCT<random number>* and puts the name of that storage account in the variable **STORAGEACCT**.</span></span> <span data-ttu-id="33e53-121">Storage account names must be unique, using `$RANDOM` appends a number to the end to make it unique.</span><span class="sxs-lookup"><span data-stu-id="33e53-121">Storage account names must be unique, using `$RANDOM` appends a number to the end to make it unique.</span></span>

```bash
STORAGEACCT=$(az storage account create \
    --resource-group "myResourceGroup" \
    --name "mystorageacct$RANDOM" \
    --location eastus \
    --sku Standard_LRS \
    --query "name" | tr -d '"')
```

## <a name="get-the-storage-key"></a><span data-ttu-id="33e53-122">Get the storage key</span><span class="sxs-lookup"><span data-stu-id="33e53-122">Get the storage key</span></span>

<span data-ttu-id="33e53-123">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span><span class="sxs-lookup"><span data-stu-id="33e53-123">When you create a storage account, the account keys are created in pairs so that they can be rotated without any service interruption.</span></span> <span data-ttu-id="33e53-124">When you switch to the second key in the pair, you create a new key pair.</span><span class="sxs-lookup"><span data-stu-id="33e53-124">When you switch to the second key in the pair, you create a new key pair.</span></span> <span data-ttu-id="33e53-125">New storage account keys are always created in pairs, so you always have at least one unused storage account key ready to switch to.</span><span class="sxs-lookup"><span data-stu-id="33e53-125">New storage account keys are always created in pairs, so you always have at least one unused storage account key ready to switch to.</span></span>

<span data-ttu-id="33e53-126">View the storage account keys using [az storage account keys list](/cli/azure/storage/account/keys#list).</span><span class="sxs-lookup"><span data-stu-id="33e53-126">View the storage account keys using [az storage account keys list](/cli/azure/storage/account/keys#list).</span></span> <span data-ttu-id="33e53-127">This example stores the value of key 1 in the **STORAGEKEY** variable.</span><span class="sxs-lookup"><span data-stu-id="33e53-127">This example stores the value of key 1 in the **STORAGEKEY** variable.</span></span>

```bash
STORAGEKEY=$(az storage account keys list \
    --resource-group "myResourceGroup" \
    --account-name $STORAGEACCT \
    --query "[0].value" | tr -d '"')
```

## <a name="create-a-file-share"></a><span data-ttu-id="33e53-128">Create a file share</span><span class="sxs-lookup"><span data-stu-id="33e53-128">Create a file share</span></span>

<span data-ttu-id="33e53-129">Create the File storage share using [az storage share create](/cli/azure/storage/share#create).</span><span class="sxs-lookup"><span data-stu-id="33e53-129">Create the File storage share using [az storage share create](/cli/azure/storage/share#create).</span></span> 

<span data-ttu-id="33e53-130">Share names need to be all lower case letters, numbers, and single hyphens but can't start with a hyphen.</span><span class="sxs-lookup"><span data-stu-id="33e53-130">Share names need to be all lower case letters, numbers, and single hyphens but can't start with a hyphen.</span></span> <span data-ttu-id="33e53-131">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://docs.microsoft.com/rest/api/storageservices/Naming-and-Referencing-Shares--Directories--Files--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="33e53-131">For complete details about naming file shares and files, see [Naming and Referencing Shares, Directories, Files, and Metadata](https://docs.microsoft.com/rest/api/storageservices/Naming-and-Referencing-Shares--Directories--Files--and-Metadata).</span></span>

<span data-ttu-id="33e53-132">This example creates a share named *myshare* with a 10-GiB quota.</span><span class="sxs-lookup"><span data-stu-id="33e53-132">This example creates a share named *myshare* with a 10-GiB quota.</span></span> 

```bash
az storage share create --name myshare \
    --quota 10 \
    --account-name $STORAGEACCT \
    --account-key $STORAGEKEY
```

## <a name="create-a-mount-point"></a><span data-ttu-id="33e53-133">Create a mount point</span><span class="sxs-lookup"><span data-stu-id="33e53-133">Create a mount point</span></span>

<span data-ttu-id="33e53-134">To mount the Azure file share on your Linux computer, you need to make sure you have the **cifs-utils** package installed.</span><span class="sxs-lookup"><span data-stu-id="33e53-134">To mount the Azure file share on your Linux computer, you need to make sure you have the **cifs-utils** package installed.</span></span> <span data-ttu-id="33e53-135">For installation instructions, see [Install the cifs-utils package for your Linux distribution](../../storage/files/storage-how-to-use-files-linux.md#install-cifs-utils).</span><span class="sxs-lookup"><span data-stu-id="33e53-135">For installation instructions, see [Install the cifs-utils package for your Linux distribution](../../storage/files/storage-how-to-use-files-linux.md#install-cifs-utils).</span></span>

<span data-ttu-id="33e53-136">Azure Files uses SMB protocol, which communicates over TCP port 445.</span><span class="sxs-lookup"><span data-stu-id="33e53-136">Azure Files uses SMB protocol, which communicates over TCP port 445.</span></span>  <span data-ttu-id="33e53-137">If you're having trouble mounting your Azure file share, make sure your firewall is not blocking TCP port 445.</span><span class="sxs-lookup"><span data-stu-id="33e53-137">If you're having trouble mounting your Azure file share, make sure your firewall is not blocking TCP port 445.</span></span>


```bash
mkdir -p /mnt/MyAzureFileShare
```

## <a name="mount-the-share"></a><span data-ttu-id="33e53-138">Mount the share</span><span class="sxs-lookup"><span data-stu-id="33e53-138">Mount the share</span></span>

<span data-ttu-id="33e53-139">Mount the Azure file share to the local directory.</span><span class="sxs-lookup"><span data-stu-id="33e53-139">Mount the Azure file share to the local directory.</span></span> 

```bash
sudo mount -t cifs //$STORAGEACCT.file.core.windows.net/myshare /mnt/MyAzureFileShare -o vers=3.0,username=$STORAGEACCT,password=$STORAGEKEY,dir_mode=0777,file_mode=0777,serverino
```



## <a name="persist-the-mount"></a><span data-ttu-id="33e53-140">Persist the mount</span><span class="sxs-lookup"><span data-stu-id="33e53-140">Persist the mount</span></span>

<span data-ttu-id="33e53-141">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span><span class="sxs-lookup"><span data-stu-id="33e53-141">When you reboot the Linux VM, the mounted SMB share is unmounted during shutdown.</span></span> <span data-ttu-id="33e53-142">To remount the SMB share on boot, add a line to the Linux /etc/fstab.</span><span class="sxs-lookup"><span data-stu-id="33e53-142">To remount the SMB share on boot, add a line to the Linux /etc/fstab.</span></span> <span data-ttu-id="33e53-143">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span><span class="sxs-lookup"><span data-stu-id="33e53-143">Linux uses the fstab file to list the file systems that it needs to mount during the boot process.</span></span> <span data-ttu-id="33e53-144">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span><span class="sxs-lookup"><span data-stu-id="33e53-144">Adding the SMB share ensures that the File storage share is a permanently mounted file system for the Linux VM.</span></span> <span data-ttu-id="33e53-145">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span><span class="sxs-lookup"><span data-stu-id="33e53-145">Adding the File storage SMB share to a new VM is possible when you use cloud-init.</span></span>

```bash
//myaccountname.file.core.windows.net/mystorageshare /mnt/mymountpoint cifs vers=3.0,username=mystorageaccount,password=myStorageAccountKeyEndingIn==,dir_mode=0777,file_mode=0777
```
<span data-ttu-id="33e53-146">For increased security in production environments, you should store your credentials outside of fstab.</span><span class="sxs-lookup"><span data-stu-id="33e53-146">For increased security in production environments, you should store your credentials outside of fstab.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33e53-147">Next steps</span><span class="sxs-lookup"><span data-stu-id="33e53-147">Next steps</span></span>

- [<span data-ttu-id="33e53-148">Using cloud-init to customize a Linux VM during creation</span><span class="sxs-lookup"><span data-stu-id="33e53-148">Using cloud-init to customize a Linux VM during creation</span></span>](using-cloud-init.md)
- [<span data-ttu-id="33e53-149">Add a disk to a Linux VM</span><span class="sxs-lookup"><span data-stu-id="33e53-149">Add a disk to a Linux VM</span></span>](add-disk.md)
- [<span data-ttu-id="33e53-150">Encrypt disks on a Linux VM by using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="33e53-150">Encrypt disks on a Linux VM by using the Azure CLI</span></span>](encrypt-disks.md)

