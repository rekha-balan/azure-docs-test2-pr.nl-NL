---
title: Restore a VM disk with Azure Backup
description: Learn how to restore a disk and create a recover a VM in Azure with Backup and Recovery Services.
services: backup
author: markgalioto
manager: carmonm
tags: azure-resource-manager, virtual-machine-backup
ms.service: backup
ms.topic: tutorial
ms.date: 4/17/2018
ms.author: markgal
ms.custom: mvc
ms.openlocfilehash: 4a122aebd149131e97be5c593a51871b1a943577
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858055"
---
# <a name="restore-a-disk-and-create-a-recovered-vm-in-azure"></a><span data-ttu-id="a88ac-103">Restore a disk and create a recovered VM in Azure</span><span class="sxs-lookup"><span data-stu-id="a88ac-103">Restore a disk and create a recovered VM in Azure</span></span>
<span data-ttu-id="a88ac-104">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span><span class="sxs-lookup"><span data-stu-id="a88ac-104">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="a88ac-105">When you restore from a recovery point, you can restore the whole VM or individual files.</span><span class="sxs-lookup"><span data-stu-id="a88ac-105">When you restore from a recovery point, you can restore the whole VM or individual files.</span></span> <span data-ttu-id="a88ac-106">This article explains how to restore a complete VM using CLI.</span><span class="sxs-lookup"><span data-stu-id="a88ac-106">This article explains how to restore a complete VM using CLI.</span></span> <span data-ttu-id="a88ac-107">In this tutorial you learn how to:</span><span class="sxs-lookup"><span data-stu-id="a88ac-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a88ac-108">List and select recovery points</span><span class="sxs-lookup"><span data-stu-id="a88ac-108">List and select recovery points</span></span>
> * <span data-ttu-id="a88ac-109">Restore a disk from a recovery point</span><span class="sxs-lookup"><span data-stu-id="a88ac-109">Restore a disk from a recovery point</span></span>
> * <span data-ttu-id="a88ac-110">Create a VM from the restored disk</span><span class="sxs-lookup"><span data-stu-id="a88ac-110">Create a VM from the restored disk</span></span>

<span data-ttu-id="a88ac-111">For information on using PowerShell to restore a disk and create a recovered VM, see [Back up and restore Azure VMs with PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span><span class="sxs-lookup"><span data-stu-id="a88ac-111">For information on using PowerShell to restore a disk and create a recovered VM, see [Back up and restore Azure VMs with PowerShell](backup-azure-vms-automation.md#restore-an-azure-vm).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="a88ac-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.18 or later.</span><span class="sxs-lookup"><span data-stu-id="a88ac-112">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.18 or later.</span></span> <span data-ttu-id="a88ac-113">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="a88ac-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="a88ac-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="a88ac-114">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="a88ac-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="a88ac-115">Prerequisites</span></span>
<span data-ttu-id="a88ac-116">This tutorial requires a Linux VM that has been protected with Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="a88ac-116">This tutorial requires a Linux VM that has been protected with Azure Backup.</span></span> <span data-ttu-id="a88ac-117">To simulate an accidental VM deletion and recovery process, you create a VM from a disk in a recovery point.</span><span class="sxs-lookup"><span data-stu-id="a88ac-117">To simulate an accidental VM deletion and recovery process, you create a VM from a disk in a recovery point.</span></span> <span data-ttu-id="a88ac-118">If you need a Linux VM that has been protected with Azure Backup, see [Back up a virtual machine in Azure with the CLI](quick-backup-vm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="a88ac-118">If you need a Linux VM that has been protected with Azure Backup, see [Back up a virtual machine in Azure with the CLI](quick-backup-vm-cli.md).</span></span>


## <a name="backup-overview"></a><span data-ttu-id="a88ac-119">Backup overview</span><span class="sxs-lookup"><span data-stu-id="a88ac-119">Backup overview</span></span>
<span data-ttu-id="a88ac-120">When Azure initiates a backup, the backup extension on the VM takes a point-in-time snapshot.</span><span class="sxs-lookup"><span data-stu-id="a88ac-120">When Azure initiates a backup, the backup extension on the VM takes a point-in-time snapshot.</span></span> <span data-ttu-id="a88ac-121">The backup extension is installed on the VM when the first backup is requested.</span><span class="sxs-lookup"><span data-stu-id="a88ac-121">The backup extension is installed on the VM when the first backup is requested.</span></span> <span data-ttu-id="a88ac-122">Azure Backup can also take a snapshot of the underlying storage if the VM is not running when the backup takes place.</span><span class="sxs-lookup"><span data-stu-id="a88ac-122">Azure Backup can also take a snapshot of the underlying storage if the VM is not running when the backup takes place.</span></span>

<span data-ttu-id="a88ac-123">By default, Azure Backup takes a file system consistent backup.</span><span class="sxs-lookup"><span data-stu-id="a88ac-123">By default, Azure Backup takes a file system consistent backup.</span></span> <span data-ttu-id="a88ac-124">Once Azure Backup takes the snapshot, the data is transferred to the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="a88ac-124">Once Azure Backup takes the snapshot, the data is transferred to the Recovery Services vault.</span></span> <span data-ttu-id="a88ac-125">To maximize efficiency, Azure Backup identifies and transfers only the blocks of data that have changed since the previous backup.</span><span class="sxs-lookup"><span data-stu-id="a88ac-125">To maximize efficiency, Azure Backup identifies and transfers only the blocks of data that have changed since the previous backup.</span></span>

<span data-ttu-id="a88ac-126">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span><span class="sxs-lookup"><span data-stu-id="a88ac-126">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span></span>


## <a name="list-available-recovery-points"></a><span data-ttu-id="a88ac-127">List available recovery points</span><span class="sxs-lookup"><span data-stu-id="a88ac-127">List available recovery points</span></span>
<span data-ttu-id="a88ac-128">To restore a disk, you select a recovery point as the source for the recovery data.</span><span class="sxs-lookup"><span data-stu-id="a88ac-128">To restore a disk, you select a recovery point as the source for the recovery data.</span></span> <span data-ttu-id="a88ac-129">As the default policy creates a recovery point each day and retains them for 30 days, you can keep a set of recovery points that allows you to select a particular point in time for recovery.</span><span class="sxs-lookup"><span data-stu-id="a88ac-129">As the default policy creates a recovery point each day and retains them for 30 days, you can keep a set of recovery points that allows you to select a particular point in time for recovery.</span></span> 

<span data-ttu-id="a88ac-130">To see a list of available recovery points, use [az backup recoverypoint list](https://docs.microsoft.com/cli/azure/backup/recoverypoint?view=azure-cli-latest#az-backup-recoverypoint-list).</span><span class="sxs-lookup"><span data-stu-id="a88ac-130">To see a list of available recovery points, use [az backup recoverypoint list](https://docs.microsoft.com/cli/azure/backup/recoverypoint?view=azure-cli-latest#az-backup-recoverypoint-list).</span></span> <span data-ttu-id="a88ac-131">The recovery point **name** is used to recover disks.</span><span class="sxs-lookup"><span data-stu-id="a88ac-131">The recovery point **name** is used to recover disks.</span></span> <span data-ttu-id="a88ac-132">In this tutorial, we want the most recent recovery point available.</span><span class="sxs-lookup"><span data-stu-id="a88ac-132">In this tutorial, we want the most recent recovery point available.</span></span> <span data-ttu-id="a88ac-133">The `--query [0].name` parameter selects the most recent recovery point name as follows:</span><span class="sxs-lookup"><span data-stu-id="a88ac-133">The `--query [0].name` parameter selects the most recent recovery point name as follows:</span></span>

```azurecli-interactive
az backup recoverypoint list \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --container-name myVM \
    --item-name myVM \
    --query [0].name \
    --output tsv
```


## <a name="restore-a-vm-disk"></a><span data-ttu-id="a88ac-134">Restore a VM disk</span><span class="sxs-lookup"><span data-stu-id="a88ac-134">Restore a VM disk</span></span>
<span data-ttu-id="a88ac-135">To restore your disk from the recovery point, you first create an Azure storage account.</span><span class="sxs-lookup"><span data-stu-id="a88ac-135">To restore your disk from the recovery point, you first create an Azure storage account.</span></span> <span data-ttu-id="a88ac-136">This storage account is used to store the restored disk.</span><span class="sxs-lookup"><span data-stu-id="a88ac-136">This storage account is used to store the restored disk.</span></span> <span data-ttu-id="a88ac-137">In additional steps, the restored disk is used to create a VM.</span><span class="sxs-lookup"><span data-stu-id="a88ac-137">In additional steps, the restored disk is used to create a VM.</span></span>

1. <span data-ttu-id="a88ac-138">To create a storage account, use [az storage account create](https://docs.microsoft.com/cli/azure/storage/account?view=azure-cli-latest#az-storage-account-create).</span><span class="sxs-lookup"><span data-stu-id="a88ac-138">To create a storage account, use [az storage account create](https://docs.microsoft.com/cli/azure/storage/account?view=azure-cli-latest#az-storage-account-create).</span></span> <span data-ttu-id="a88ac-139">The storage account name must be all lowercase, and be globally unique.</span><span class="sxs-lookup"><span data-stu-id="a88ac-139">The storage account name must be all lowercase, and be globally unique.</span></span> <span data-ttu-id="a88ac-140">Replace *mystorageaccount* with your own unique name:</span><span class="sxs-lookup"><span data-stu-id="a88ac-140">Replace *mystorageaccount* with your own unique name:</span></span>

    ```azurecli-interactive
    az storage account create \
        --resource-group myResourceGroup \
        --name mystorageaccount \
        --sku Standard_LRS
    ```

2. <span data-ttu-id="a88ac-141">Restore the disk from your recovery point with [az backup restore restore-disks](https://docs.microsoft.com/cli/azure/backup/restore?view=azure-cli-latest#az-backup-restore-restore-disks).</span><span class="sxs-lookup"><span data-stu-id="a88ac-141">Restore the disk from your recovery point with [az backup restore restore-disks](https://docs.microsoft.com/cli/azure/backup/restore?view=azure-cli-latest#az-backup-restore-restore-disks).</span></span> <span data-ttu-id="a88ac-142">Replace *mystorageaccount* with the name of the storage account you created in the preceding command.</span><span class="sxs-lookup"><span data-stu-id="a88ac-142">Replace *mystorageaccount* with the name of the storage account you created in the preceding command.</span></span> <span data-ttu-id="a88ac-143">Replace *myRecoveryPointName* with the recovery point name you obtained in the output from the previous [az backup recoverypoint list](https://docs.microsoft.com/cli/azure/backup/recoverypoint?view=azure-cli-latest#az-backup-recoverypoint-list) command:</span><span class="sxs-lookup"><span data-stu-id="a88ac-143">Replace *myRecoveryPointName* with the recovery point name you obtained in the output from the previous [az backup recoverypoint list](https://docs.microsoft.com/cli/azure/backup/recoverypoint?view=azure-cli-latest#az-backup-recoverypoint-list) command:</span></span>

    ```azurecli-interactive
    az backup restore restore-disks \
        --resource-group myResourceGroup \
        --vault-name myRecoveryServicesVault \
        --container-name myVM \
        --item-name myVM \
        --storage-account mystorageaccount \
        --rp-name myRecoveryPointName
    ```


## <a name="monitor-the-restore-job"></a><span data-ttu-id="a88ac-144">Monitor the restore job</span><span class="sxs-lookup"><span data-stu-id="a88ac-144">Monitor the restore job</span></span>
<span data-ttu-id="a88ac-145">To monitor the status of restore job, use [az backup job list](https://docs.microsoft.com/cli/azure/backup/job?view=azure-cli-latest#az-backup-job-list):</span><span class="sxs-lookup"><span data-stu-id="a88ac-145">To monitor the status of restore job, use [az backup job list](https://docs.microsoft.com/cli/azure/backup/job?view=azure-cli-latest#az-backup-job-list):</span></span>

```azurecli-interactive 
az backup job list \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --output table
```

<span data-ttu-id="a88ac-146">The output is similar to the following example, which shows the restore job is *InProgress*:</span><span class="sxs-lookup"><span data-stu-id="a88ac-146">The output is similar to the following example, which shows the restore job is *InProgress*:</span></span>

```
Name      Operation        Status      Item Name    Start Time UTC       Duration
--------  ---------------  ----------  -----------  -------------------  --------------
7f2ad916  Restore          InProgress  myvm         2017-09-19T19:39:52  0:00:34.520850
a0a8e5e6  Backup           Completed   myvm         2017-09-19T03:09:21  0:15:26.155212
fe5d0414  ConfigureBackup  Completed   myvm         2017-09-19T03:03:57  0:00:31.191807
```

<span data-ttu-id="a88ac-147">When the *Status* of the restore job reports *Completed*, the disk has been restored to the storage account.</span><span class="sxs-lookup"><span data-stu-id="a88ac-147">When the *Status* of the restore job reports *Completed*, the disk has been restored to the storage account.</span></span>


## <a name="convert-the-restored-disk-to-a-managed-disk"></a><span data-ttu-id="a88ac-148">Convert the restored disk to a Managed Disk</span><span class="sxs-lookup"><span data-stu-id="a88ac-148">Convert the restored disk to a Managed Disk</span></span>
<span data-ttu-id="a88ac-149">The restore job creates an unmanaged disk.</span><span class="sxs-lookup"><span data-stu-id="a88ac-149">The restore job creates an unmanaged disk.</span></span> <span data-ttu-id="a88ac-150">In order to create a VM from the disk, it must first be converted to a managed disk.</span><span class="sxs-lookup"><span data-stu-id="a88ac-150">In order to create a VM from the disk, it must first be converted to a managed disk.</span></span>

1. <span data-ttu-id="a88ac-151">Obtain the connection information for your storage account with [az storage account show-connection-string](https://docs.microsoft.com/cli/azure/storage/account?view=azure-cli-latest#az-storage-account-show-connection-string).</span><span class="sxs-lookup"><span data-stu-id="a88ac-151">Obtain the connection information for your storage account with [az storage account show-connection-string](https://docs.microsoft.com/cli/azure/storage/account?view=azure-cli-latest#az-storage-account-show-connection-string).</span></span> <span data-ttu-id="a88ac-152">Replace *mystorageaccount* with the name of your storage account as follows:</span><span class="sxs-lookup"><span data-stu-id="a88ac-152">Replace *mystorageaccount* with the name of your storage account as follows:</span></span>
    
    ```azurecli-interactive
    export AZURE_STORAGE_CONNECTION_STRING=$( az storage account show-connection-string \
        --resource-group myResourceGroup \
        --output tsv \
        --name mystorageaccount )
    ```

2. <span data-ttu-id="a88ac-153">Your unmanaged disk is secured in the storage account.</span><span class="sxs-lookup"><span data-stu-id="a88ac-153">Your unmanaged disk is secured in the storage account.</span></span> <span data-ttu-id="a88ac-154">The following commands get information about your unmanaged disk and create a variable named *uri* that is used in the next step when you create the Managed Disk.</span><span class="sxs-lookup"><span data-stu-id="a88ac-154">The following commands get information about your unmanaged disk and create a variable named *uri* that is used in the next step when you create the Managed Disk.</span></span>

    ```azurecli-interactive
    container=$(az storage container list --query [0].name -o tsv)
    blob=$(az storage blob list --container-name $container --query [0].name -o tsv)
    uri=$(az storage blob url --container-name $container --name $blob -o tsv)
    ```

3. <span data-ttu-id="a88ac-155">Now you can create a Managed Disk from your recovered disk with [az disk create](https://docs.microsoft.com/cli/azure/disk?view=azure-cli-latest#az-disk-create).</span><span class="sxs-lookup"><span data-stu-id="a88ac-155">Now you can create a Managed Disk from your recovered disk with [az disk create](https://docs.microsoft.com/cli/azure/disk?view=azure-cli-latest#az-disk-create).</span></span> <span data-ttu-id="a88ac-156">The *uri* variable from the preceding step is used as the source for your Managed Disk.</span><span class="sxs-lookup"><span data-stu-id="a88ac-156">The *uri* variable from the preceding step is used as the source for your Managed Disk.</span></span>

    ```azurecli-interactive
    az disk create \
        --resource-group myResourceGroup \
        --name myRestoredDisk \
        --source $uri
    ```

4. <span data-ttu-id="a88ac-157">As you now have a Managed Disk from your restored disk, clean up the unmanaged disk and storage account with [az storage account delete](/cli/azure/storage/account?view=azure-cli-latest#az-storage-account-delete).</span><span class="sxs-lookup"><span data-stu-id="a88ac-157">As you now have a Managed Disk from your restored disk, clean up the unmanaged disk and storage account with [az storage account delete](/cli/azure/storage/account?view=azure-cli-latest#az-storage-account-delete).</span></span> <span data-ttu-id="a88ac-158">Replace *mystorageaccount* with the name of your storage account as follows:</span><span class="sxs-lookup"><span data-stu-id="a88ac-158">Replace *mystorageaccount* with the name of your storage account as follows:</span></span>

    ```azurecli-interactive
    az storage account delete \
        --resource-group myResourceGroup \
        --name mystorageaccount
    ```


## <a name="create-a-vm-from-the-restored-disk"></a><span data-ttu-id="a88ac-159">Create a VM from the restored disk</span><span class="sxs-lookup"><span data-stu-id="a88ac-159">Create a VM from the restored disk</span></span>
<span data-ttu-id="a88ac-160">The final step is to create a VM from the Managed Disk.</span><span class="sxs-lookup"><span data-stu-id="a88ac-160">The final step is to create a VM from the Managed Disk.</span></span>

1. <span data-ttu-id="a88ac-161">Create a VM from your Managed Disk with [az vm create](/cli/azure/vm?view=azure-cli-latest#az-vm-create) as follows:</span><span class="sxs-lookup"><span data-stu-id="a88ac-161">Create a VM from your Managed Disk with [az vm create](/cli/azure/vm?view=azure-cli-latest#az-vm-create) as follows:</span></span>

    ```azurecli-interactive
    az vm create \
        --resource-group myResourceGroup \
        --name myRestoredVM \
        --attach-os-disk myRestoredDisk \
        --os-type linux
    ```

2. <span data-ttu-id="a88ac-162">To confirm that your VM has been created from your recovered disk, list the VMs in your resource group with [az vm list](/cli/azure/vm?view=azure-cli-latest#az-vm-list) as follows:</span><span class="sxs-lookup"><span data-stu-id="a88ac-162">To confirm that your VM has been created from your recovered disk, list the VMs in your resource group with [az vm list](/cli/azure/vm?view=azure-cli-latest#az-vm-list) as follows:</span></span>

    ```azurecli-interactive
    az vm list --resource-group myResourceGroup --output table
    ```


## <a name="next-steps"></a><span data-ttu-id="a88ac-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="a88ac-163">Next steps</span></span>
<span data-ttu-id="a88ac-164">In this tutorial, you restored a disk from a recovery point and then created a VM from the disk.</span><span class="sxs-lookup"><span data-stu-id="a88ac-164">In this tutorial, you restored a disk from a recovery point and then created a VM from the disk.</span></span> <span data-ttu-id="a88ac-165">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="a88ac-165">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a88ac-166">List and select recovery points</span><span class="sxs-lookup"><span data-stu-id="a88ac-166">List and select recovery points</span></span>
> * <span data-ttu-id="a88ac-167">Restore a disk from a recovery point</span><span class="sxs-lookup"><span data-stu-id="a88ac-167">Restore a disk from a recovery point</span></span>
> * <span data-ttu-id="a88ac-168">Create a VM from the restored disk</span><span class="sxs-lookup"><span data-stu-id="a88ac-168">Create a VM from the restored disk</span></span>

<span data-ttu-id="a88ac-169">Advance to the next tutorial to learn about restoring individual files from a recovery point.</span><span class="sxs-lookup"><span data-stu-id="a88ac-169">Advance to the next tutorial to learn about restoring individual files from a recovery point.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a88ac-170">Restore files to a virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="a88ac-170">Restore files to a virtual machine in Azure</span></span>](tutorial-restore-files.md)

