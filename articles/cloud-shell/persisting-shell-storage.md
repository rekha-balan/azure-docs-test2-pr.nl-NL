---
title: Persist files for Bash in Azure Cloud Shell | Microsoft Docs
description: Walkthrough of how Bash in Azure Cloud Shell persists files.
services: azure
documentationcenter: ''
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: ''
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 09/04/2018
ms.author: juluk
ms.openlocfilehash: 606b36be4a2bbeff8dd226f41341d60e23f0d988
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866935"
---
[!INCLUDE [PersistingStorage-introblock](../../includes/cloud-shell-persisting-shell-storage-introblock.md)]

## <a name="how-cloud-shell-storage-works"></a><span data-ttu-id="69203-103">How Cloud Shell storage works</span><span class="sxs-lookup"><span data-stu-id="69203-103">How Cloud Shell storage works</span></span> 
<span data-ttu-id="69203-104">Cloud Shell persists files through both of the following methods:</span><span class="sxs-lookup"><span data-stu-id="69203-104">Cloud Shell persists files through both of the following methods:</span></span> 
* <span data-ttu-id="69203-105">Creating a disk image of your `$Home` directory to persist all contents within the directory.</span><span class="sxs-lookup"><span data-stu-id="69203-105">Creating a disk image of your `$Home` directory to persist all contents within the directory.</span></span> <span data-ttu-id="69203-106">The disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span><span class="sxs-lookup"><span data-stu-id="69203-106">The disk image is saved in your specified file share as `acc_<User>.img` at `fileshare.storage.windows.net/fileshare/.cloudconsole/acc_<User>.img`, and it automatically syncs changes.</span></span> 
* <span data-ttu-id="69203-107">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file-share interaction.</span><span class="sxs-lookup"><span data-stu-id="69203-107">Mounting your specified file share as `clouddrive` in your `$Home` directory for direct file-share interaction.</span></span> <span data-ttu-id="69203-108">`/Home/<User>/clouddrive` is mapped to `fileshare.storage.windows.net/fileshare`.</span><span class="sxs-lookup"><span data-stu-id="69203-108">`/Home/<User>/clouddrive` is mapped to `fileshare.storage.windows.net/fileshare`.</span></span>
 
> [!NOTE]
> <span data-ttu-id="69203-109">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span><span class="sxs-lookup"><span data-stu-id="69203-109">All files in your `$Home` directory, such as SSH keys, are persisted in your user disk image, which is stored in your mounted file share.</span></span> <span data-ttu-id="69203-110">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span><span class="sxs-lookup"><span data-stu-id="69203-110">Apply best practices when you persist information in your `$Home` directory and mounted file share.</span></span>

## <a name="bash-specific-commands"></a><span data-ttu-id="69203-111">Bash-specific commands</span><span class="sxs-lookup"><span data-stu-id="69203-111">Bash-specific commands</span></span>

### <a name="use-the-clouddrive-command"></a><span data-ttu-id="69203-112">Use the `clouddrive` command</span><span class="sxs-lookup"><span data-stu-id="69203-112">Use the `clouddrive` command</span></span>
<span data-ttu-id="69203-113">With Bash in Cloud Shell, you can run a command called `clouddrive`, which enables you to manually update the file share that is mounted to Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="69203-113">With Bash in Cloud Shell, you can run a command called `clouddrive`, which enables you to manually update the file share that is mounted to Cloud Shell.</span></span>
<span data-ttu-id="69203-114">![Running the "clouddrive" command](media/persisting-shell-storage/clouddrive-h.png)</span><span class="sxs-lookup"><span data-stu-id="69203-114">![Running the "clouddrive" command](media/persisting-shell-storage/clouddrive-h.png)</span></span>

### <a name="mount-a-new-clouddrive"></a><span data-ttu-id="69203-115">Mount a new clouddrive</span><span class="sxs-lookup"><span data-stu-id="69203-115">Mount a new clouddrive</span></span>

#### <a name="prerequisites-for-manual-mounting"></a><span data-ttu-id="69203-116">Prerequisites for manual mounting</span><span class="sxs-lookup"><span data-stu-id="69203-116">Prerequisites for manual mounting</span></span>
<span data-ttu-id="69203-117">You can update the file share that's associated with Cloud Shell by using the `clouddrive mount` command.</span><span class="sxs-lookup"><span data-stu-id="69203-117">You can update the file share that's associated with Cloud Shell by using the `clouddrive mount` command.</span></span>

<span data-ttu-id="69203-118">If you mount an existing file share, the storage accounts must be located in your select Cloud Shell region.</span><span class="sxs-lookup"><span data-stu-id="69203-118">If you mount an existing file share, the storage accounts must be located in your select Cloud Shell region.</span></span> <span data-ttu-id="69203-119">Retrieve the location by running `env` from Bash and checking the `ACC_LOCATION`.</span><span class="sxs-lookup"><span data-stu-id="69203-119">Retrieve the location by running `env` from Bash and checking the `ACC_LOCATION`.</span></span>

#### <a name="the-clouddrive-mount-command"></a><span data-ttu-id="69203-120">The `clouddrive mount` command</span><span class="sxs-lookup"><span data-stu-id="69203-120">The `clouddrive mount` command</span></span>

> [!NOTE]
> <span data-ttu-id="69203-121">If you're mounting a new file share, a new user image is created for your `$Home` directory.</span><span class="sxs-lookup"><span data-stu-id="69203-121">If you're mounting a new file share, a new user image is created for your `$Home` directory.</span></span> <span data-ttu-id="69203-122">Your previous `$Home` image is kept in your previous file share.</span><span class="sxs-lookup"><span data-stu-id="69203-122">Your previous `$Home` image is kept in your previous file share.</span></span>

<span data-ttu-id="69203-123">Run the `clouddrive mount` command with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="69203-123">Run the `clouddrive mount` command with the following parameters:</span></span>

```
clouddrive mount -s mySubscription -g myRG -n storageAccountName -f fileShareName
```

<span data-ttu-id="69203-124">To view more details, run `clouddrive mount -h`, as shown here:</span><span class="sxs-lookup"><span data-stu-id="69203-124">To view more details, run `clouddrive mount -h`, as shown here:</span></span>

![Running the `clouddrive mount`command](media/persisting-shell-storage/mount-h.png)

### <a name="unmount-clouddrive"></a><span data-ttu-id="69203-126">Unmount clouddrive</span><span class="sxs-lookup"><span data-stu-id="69203-126">Unmount clouddrive</span></span>
<span data-ttu-id="69203-127">You can unmount a file share that's mounted to Cloud Shell at any time.</span><span class="sxs-lookup"><span data-stu-id="69203-127">You can unmount a file share that's mounted to Cloud Shell at any time.</span></span> <span data-ttu-id="69203-128">Since Cloud Shell requires a mounted file share to be used, you will be prompted to create and mount another file share on the next session.</span><span class="sxs-lookup"><span data-stu-id="69203-128">Since Cloud Shell requires a mounted file share to be used, you will be prompted to create and mount another file share on the next session.</span></span>

1. <span data-ttu-id="69203-129">Run `clouddrive unmount`.</span><span class="sxs-lookup"><span data-stu-id="69203-129">Run `clouddrive unmount`.</span></span>
2. <span data-ttu-id="69203-130">Acknowledge and confirm prompts.</span><span class="sxs-lookup"><span data-stu-id="69203-130">Acknowledge and confirm prompts.</span></span>

<span data-ttu-id="69203-131">Your file share will continue to exist unless you delete it manually.</span><span class="sxs-lookup"><span data-stu-id="69203-131">Your file share will continue to exist unless you delete it manually.</span></span> <span data-ttu-id="69203-132">Cloud Shell will no longer search for this file share on subsequent sessions.</span><span class="sxs-lookup"><span data-stu-id="69203-132">Cloud Shell will no longer search for this file share on subsequent sessions.</span></span> <span data-ttu-id="69203-133">To view more details, run `clouddrive unmount -h`, as shown here:</span><span class="sxs-lookup"><span data-stu-id="69203-133">To view more details, run `clouddrive unmount -h`, as shown here:</span></span>

![Running the `clouddrive unmount`command](media/persisting-shell-storage/unmount-h.png)

> [!WARNING]
> <span data-ttu-id="69203-135">Although running this command will not delete any resources, manually deleting a resource group, storage account, or file share that's mapped to Cloud Shell erases your `$Home` directory disk image and any files in your file share.</span><span class="sxs-lookup"><span data-stu-id="69203-135">Although running this command will not delete any resources, manually deleting a resource group, storage account, or file share that's mapped to Cloud Shell erases your `$Home` directory disk image and any files in your file share.</span></span> <span data-ttu-id="69203-136">This action cannot be undone.</span><span class="sxs-lookup"><span data-stu-id="69203-136">This action cannot be undone.</span></span>

### <a name="list-clouddrive"></a><span data-ttu-id="69203-137">List `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="69203-137">List `clouddrive`</span></span>
<span data-ttu-id="69203-138">To discover which file share is mounted as `clouddrive`, run the `df` command.</span><span class="sxs-lookup"><span data-stu-id="69203-138">To discover which file share is mounted as `clouddrive`, run the `df` command.</span></span> 

<span data-ttu-id="69203-139">The file path to clouddrive shows your storage account name and file share in the URL.</span><span class="sxs-lookup"><span data-stu-id="69203-139">The file path to clouddrive shows your storage account name and file share in the URL.</span></span> <span data-ttu-id="69203-140">For example, `//storageaccountname.file.core.windows.net/filesharename`</span><span class="sxs-lookup"><span data-stu-id="69203-140">For example, `//storageaccountname.file.core.windows.net/filesharename`</span></span>

```
justin@Azure:~$ df
Filesystem                                          1K-blocks   Used  Available Use% Mounted on
overlay                                             29711408 5577940   24117084  19% /
tmpfs                                                 986716       0     986716   0% /dev
tmpfs                                                 986716       0     986716   0% /sys/fs/cgroup
/dev/sda1                                           29711408 5577940   24117084  19% /etc/hosts
shm                                                    65536       0      65536   0% /dev/shm
//mystoragename.file.core.windows.net/fileshareName 5368709120    64 5368709056   1% /home/justin/clouddrive
justin@Azure:~$
```
## <a name="powershell-specific-commands"></a><span data-ttu-id="69203-141">PowerShell-specific commands</span><span class="sxs-lookup"><span data-stu-id="69203-141">PowerShell-specific commands</span></span>

### <a name="list-clouddrive-azure-file-shares"></a><span data-ttu-id="69203-142">List `clouddrive` Azure file shares</span><span class="sxs-lookup"><span data-stu-id="69203-142">List `clouddrive` Azure file shares</span></span>
<span data-ttu-id="69203-143">The `Get-CloudDrive` cmdlet retrieves the Azure file share information currently mounted by the `clouddrive` in the Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="69203-143">The `Get-CloudDrive` cmdlet retrieves the Azure file share information currently mounted by the `clouddrive` in the Cloud Shell.</span></span> <br>
<span data-ttu-id="69203-144">![Running Get-CloudDrive](media/persisting-shell-storage-powershell/Get-Clouddrive.png)</span><span class="sxs-lookup"><span data-stu-id="69203-144">![Running Get-CloudDrive](media/persisting-shell-storage-powershell/Get-Clouddrive.png)</span></span>

### <a name="unmount-clouddrive"></a><span data-ttu-id="69203-145">Unmount `clouddrive`</span><span class="sxs-lookup"><span data-stu-id="69203-145">Unmount `clouddrive`</span></span>
<span data-ttu-id="69203-146">You can unmount an Azure file share that's mounted to Cloud Shell at any time.</span><span class="sxs-lookup"><span data-stu-id="69203-146">You can unmount an Azure file share that's mounted to Cloud Shell at any time.</span></span> <span data-ttu-id="69203-147">If the Azure file share has been removed, you will be prompted to create and mount a new Azure file share at the next session.</span><span class="sxs-lookup"><span data-stu-id="69203-147">If the Azure file share has been removed, you will be prompted to create and mount a new Azure file share at the next session.</span></span>

<span data-ttu-id="69203-148">The `Dismount-CloudDrive` cmdlet unmounts an Azure file share from the current storage account.</span><span class="sxs-lookup"><span data-stu-id="69203-148">The `Dismount-CloudDrive` cmdlet unmounts an Azure file share from the current storage account.</span></span> <span data-ttu-id="69203-149">Dismounting the `clouddrive` terminates the current session.</span><span class="sxs-lookup"><span data-stu-id="69203-149">Dismounting the `clouddrive` terminates the current session.</span></span> <span data-ttu-id="69203-150">The user will be prompted to create and mount a new Azure file share during the next session.</span><span class="sxs-lookup"><span data-stu-id="69203-150">The user will be prompted to create and mount a new Azure file share during the next session.</span></span>
<span data-ttu-id="69203-151">![Running Dismount-CloudDrive](media/persisting-shell-storage-powershell/Dismount-Clouddrive.png)</span><span class="sxs-lookup"><span data-stu-id="69203-151">![Running Dismount-CloudDrive](media/persisting-shell-storage-powershell/Dismount-Clouddrive.png)</span></span>

[!INCLUDE [PersistingStorage-endblock](../../includes/cloud-shell-persisting-shell-storage-endblock.md)]

## <a name="next-steps"></a><span data-ttu-id="69203-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="69203-152">Next steps</span></span>
[<span data-ttu-id="69203-153">Bash in Cloud Shell Quickstart</span><span class="sxs-lookup"><span data-stu-id="69203-153">Bash in Cloud Shell Quickstart</span></span>](quickstart.md) <br>
[<span data-ttu-id="69203-154">PowerShell in Cloud Shell Quickstart</span><span class="sxs-lookup"><span data-stu-id="69203-154">PowerShell in Cloud Shell Quickstart</span></span>](quickstart-powershell.md) <br>
[<span data-ttu-id="69203-155">Learn about Microsoft Azure Files storage</span><span class="sxs-lookup"><span data-stu-id="69203-155">Learn about Microsoft Azure Files storage</span></span>](https://docs.microsoft.com/azure/storage/storage-introduction#file-storage) <br>
[<span data-ttu-id="69203-156">Learn about storage tags</span><span class="sxs-lookup"><span data-stu-id="69203-156">Learn about storage tags</span></span>](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-using-tags) <br>
