---
title: Azure Quick Start - Back up a VM with Azure CLI
description: Learn how to back up your virtual machines with the Azure CLI
services: backup
author: markgalioto
manager: carmonm
tags: azure-resource-manager, virtual-machine-backup
ms.service: backup
ms.devlang: azurecli
ms.topic: quickstart
ms.date: 8/3/2018
ms.author: markgal
ms.custom: mvc
ms.openlocfilehash: 9693c619b9723ed6dfd9da02bfdf41e93518f6f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855672"
---
# <a name="back-up-a-virtual-machine-in-azure-with-the-cli"></a><span data-ttu-id="7f4a9-103">Back up a virtual machine in Azure with the CLI</span><span class="sxs-lookup"><span data-stu-id="7f4a9-103">Back up a virtual machine in Azure with the CLI</span></span>
<span data-ttu-id="7f4a9-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-104">The Azure CLI is used to create and manage Azure resources from the command line or in scripts.</span></span> <span data-ttu-id="7f4a9-105">You can protect your data by taking backups at regular intervals.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-105">You can protect your data by taking backups at regular intervals.</span></span> <span data-ttu-id="7f4a9-106">Azure Backup creates recovery points that can be stored in geo-redundant recovery vaults.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-106">Azure Backup creates recovery points that can be stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="7f4a9-107">This article details how to back up a virtual machine (VM) in Azure with the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-107">This article details how to back up a virtual machine (VM) in Azure with the Azure CLI.</span></span> <span data-ttu-id="7f4a9-108">You can also perform these steps with [Azure PowerShell](quick-backup-vm-powershell.md) or in the [Azure portal](quick-backup-vm-portal.md).</span><span class="sxs-lookup"><span data-stu-id="7f4a9-108">You can also perform these steps with [Azure PowerShell](quick-backup-vm-powershell.md) or in the [Azure portal](quick-backup-vm-portal.md).</span></span>

<span data-ttu-id="7f4a9-109">This quick start enables backup on an existing Azure VM.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-109">This quick start enables backup on an existing Azure VM.</span></span> <span data-ttu-id="7f4a9-110">If you need to create a VM, you can [create a VM with the Azure CLI](../virtual-machines/linux/quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="7f4a9-110">If you need to create a VM, you can [create a VM with the Azure CLI](../virtual-machines/linux/quick-create-cli.md).</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="7f4a9-111">To install and use the CLI locally, you must run Azure CLI version 2.0.18 or later.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-111">To install and use the CLI locally, you must run Azure CLI version 2.0.18 or later.</span></span> <span data-ttu-id="7f4a9-112">To find the CLI version, run `az --version`.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-112">To find the CLI version, run `az --version`.</span></span> <span data-ttu-id="7f4a9-113">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7f4a9-113">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 


## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="7f4a9-114">Create a recovery services vault</span><span class="sxs-lookup"><span data-stu-id="7f4a9-114">Create a recovery services vault</span></span>
<span data-ttu-id="7f4a9-115">A Recovery Services vault is a logical container that stores the backup data for each protected resource, such as Azure VMs.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-115">A Recovery Services vault is a logical container that stores the backup data for each protected resource, such as Azure VMs.</span></span> <span data-ttu-id="7f4a9-116">When the backup job for a protected resource runs, it creates a recovery point inside the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-116">When the backup job for a protected resource runs, it creates a recovery point inside the Recovery Services vault.</span></span> <span data-ttu-id="7f4a9-117">You can then use one of these recovery points to restore data to a given point in time.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-117">You can then use one of these recovery points to restore data to a given point in time.</span></span>

<span data-ttu-id="7f4a9-118">Create a Recovery Services vault with [az backup vault create](https://docs.microsoft.com/cli/azure/backup/vault#az-backup-vault-create).</span><span class="sxs-lookup"><span data-stu-id="7f4a9-118">Create a Recovery Services vault with [az backup vault create](https://docs.microsoft.com/cli/azure/backup/vault#az-backup-vault-create).</span></span> <span data-ttu-id="7f4a9-119">Specify the same resource group and location as the VM you wish to protect.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-119">Specify the same resource group and location as the VM you wish to protect.</span></span> <span data-ttu-id="7f4a9-120">If you used the [VM quickstart](../virtual-machines/linux/quick-create-cli.md), then you created:</span><span class="sxs-lookup"><span data-stu-id="7f4a9-120">If you used the [VM quickstart](../virtual-machines/linux/quick-create-cli.md), then you created:</span></span>

- <span data-ttu-id="7f4a9-121">a resource group named *myResourceGroup*,</span><span class="sxs-lookup"><span data-stu-id="7f4a9-121">a resource group named *myResourceGroup*,</span></span>
- <span data-ttu-id="7f4a9-122">a VM named *myVM*,</span><span class="sxs-lookup"><span data-stu-id="7f4a9-122">a VM named *myVM*,</span></span>
- <span data-ttu-id="7f4a9-123">resources in the *eastus* location.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-123">resources in the *eastus* location.</span></span>

```azurecli-interactive 
az backup vault create --resource-group myResourceGroup \
    --name myRecoveryServicesVault \
    --location eastus
```

<span data-ttu-id="7f4a9-124">By default, the Recovery Services vault is set for Geo-Redundant storage.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-124">By default, the Recovery Services vault is set for Geo-Redundant storage.</span></span> <span data-ttu-id="7f4a9-125">Geo-Redundant storage ensures your backup data is replicated to a secondary Azure region that is hundreds of miles away from the primary region.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-125">Geo-Redundant storage ensures your backup data is replicated to a secondary Azure region that is hundreds of miles away from the primary region.</span></span>


## <a name="enable-backup-for-an-azure-vm"></a><span data-ttu-id="7f4a9-126">Enable backup for an Azure VM</span><span class="sxs-lookup"><span data-stu-id="7f4a9-126">Enable backup for an Azure VM</span></span>
<span data-ttu-id="7f4a9-127">Create a protection policy to define: when a backup job runs, and how long the recovery points are stored.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-127">Create a protection policy to define: when a backup job runs, and how long the recovery points are stored.</span></span> <span data-ttu-id="7f4a9-128">The default protection policy runs a backup job each day and retains recovery points for 30 days.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-128">The default protection policy runs a backup job each day and retains recovery points for 30 days.</span></span> <span data-ttu-id="7f4a9-129">You can use these default policy values to quickly protect your VM.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-129">You can use these default policy values to quickly protect your VM.</span></span> <span data-ttu-id="7f4a9-130">To enable backup protection for a VM, use [az backup protection enable-for-vm](https://docs.microsoft.com/cli/azure/backup/protection#az-backup-protection-enable-for-vm).</span><span class="sxs-lookup"><span data-stu-id="7f4a9-130">To enable backup protection for a VM, use [az backup protection enable-for-vm](https://docs.microsoft.com/cli/azure/backup/protection#az-backup-protection-enable-for-vm).</span></span> <span data-ttu-id="7f4a9-131">Specify the resource group and VM to protect, then the policy to use:</span><span class="sxs-lookup"><span data-stu-id="7f4a9-131">Specify the resource group and VM to protect, then the policy to use:</span></span>

```azurecli-interactive 
az backup protection enable-for-vm \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --vm myVM \
    --policy-name DefaultPolicy
```

> [!NOTE]
<span data-ttu-id="7f4a9-132">If the VM is not in the same resource group as that of vault, then myResourceGroup refers to the resource group where vault was created.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-132">If the VM is not in the same resource group as that of vault, then myResourceGroup refers to the resource group where vault was created.</span></span> <span data-ttu-id="7f4a9-133">Instead of VM name, provide the VM ID as indicated below.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-133">Instead of VM name, provide the VM ID as indicated below.</span></span>

```azurecli-interactive 
az backup protection enable-for-vm \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --vm $(az vm show -g VMResourceGroup -n MyVm --query id) \
    --policy-name DefaultPolicy
```

## <a name="start-a-backup-job"></a><span data-ttu-id="7f4a9-134">Start a backup job</span><span class="sxs-lookup"><span data-stu-id="7f4a9-134">Start a backup job</span></span>
<span data-ttu-id="7f4a9-135">To start a backup now rather than wait for the default policy to run the job at the scheduled time, use [az backup protection backup-now](https://docs.microsoft.com/cli/azure/backup/protection#az-backup-protection-backup-now).</span><span class="sxs-lookup"><span data-stu-id="7f4a9-135">To start a backup now rather than wait for the default policy to run the job at the scheduled time, use [az backup protection backup-now](https://docs.microsoft.com/cli/azure/backup/protection#az-backup-protection-backup-now).</span></span> <span data-ttu-id="7f4a9-136">This first backup job creates a full recovery point.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-136">This first backup job creates a full recovery point.</span></span> <span data-ttu-id="7f4a9-137">Each backup job after this initial backup creates incremental recovery points.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-137">Each backup job after this initial backup creates incremental recovery points.</span></span> <span data-ttu-id="7f4a9-138">Incremental recovery points are storage and time-efficient, as they only transfer changes made since the last backup.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-138">Incremental recovery points are storage and time-efficient, as they only transfer changes made since the last backup.</span></span>

<span data-ttu-id="7f4a9-139">The following parameters are used to back up the VM:</span><span class="sxs-lookup"><span data-stu-id="7f4a9-139">The following parameters are used to back up the VM:</span></span>

- <span data-ttu-id="7f4a9-140">`--container-name` is the name of your VM</span><span class="sxs-lookup"><span data-stu-id="7f4a9-140">`--container-name` is the name of your VM</span></span>
- <span data-ttu-id="7f4a9-141">`--item-name` is the name of your VM</span><span class="sxs-lookup"><span data-stu-id="7f4a9-141">`--item-name` is the name of your VM</span></span>
- <span data-ttu-id="7f4a9-142">`--retain-until` value should be set to the last available date, in UTC time format (**dd-mm-yyyy**), that you wish the recovery point to be available</span><span class="sxs-lookup"><span data-stu-id="7f4a9-142">`--retain-until` value should be set to the last available date, in UTC time format (**dd-mm-yyyy**), that you wish the recovery point to be available</span></span>

<span data-ttu-id="7f4a9-143">The following example backs up the VM named *myVM* and sets the expiration of the recovery point to October 18, 2017:</span><span class="sxs-lookup"><span data-stu-id="7f4a9-143">The following example backs up the VM named *myVM* and sets the expiration of the recovery point to October 18, 2017:</span></span>

```azurecli-interactive 
az backup protection backup-now \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --container-name myVM \
    --item-name myVM \
    --retain-until 18-10-2017
```


## <a name="monitor-the-backup-job"></a><span data-ttu-id="7f4a9-144">Monitor the backup job</span><span class="sxs-lookup"><span data-stu-id="7f4a9-144">Monitor the backup job</span></span>
<span data-ttu-id="7f4a9-145">To monitor the status of backup jobs, use [az backup job list](https://docs.microsoft.com/cli/azure/backup/job#az-backup-job-list):</span><span class="sxs-lookup"><span data-stu-id="7f4a9-145">To monitor the status of backup jobs, use [az backup job list](https://docs.microsoft.com/cli/azure/backup/job#az-backup-job-list):</span></span>

```azurecli-interactive 
az backup job list \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --output table
```

<span data-ttu-id="7f4a9-146">The output is similar to the following example, which shows the backup job is *InProgress*:</span><span class="sxs-lookup"><span data-stu-id="7f4a9-146">The output is similar to the following example, which shows the backup job is *InProgress*:</span></span>

```
Name      Operation        Status      Item Name    Start Time UTC       Duration
--------  ---------------  ----------  -----------  -------------------  --------------
a0a8e5e6  Backup           InProgress  myvm         2017-09-19T03:09:21  0:00:48.718366
fe5d0414  ConfigureBackup  Completed   myvm         2017-09-19T03:03:57  0:00:31.191807
```

<span data-ttu-id="7f4a9-147">When the *Status* of the backup job reports *Completed*, your VM is protected with Recovery Services and has a full recovery point stored.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-147">When the *Status* of the backup job reports *Completed*, your VM is protected with Recovery Services and has a full recovery point stored.</span></span>


## <a name="clean-up-deployment"></a><span data-ttu-id="7f4a9-148">Clean up deployment</span><span class="sxs-lookup"><span data-stu-id="7f4a9-148">Clean up deployment</span></span>
<span data-ttu-id="7f4a9-149">When no longer needed, you can disable protection on the VM, remove the restore points and Recovery Services vault, then delete the resource group and associated VM resources.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-149">When no longer needed, you can disable protection on the VM, remove the restore points and Recovery Services vault, then delete the resource group and associated VM resources.</span></span> <span data-ttu-id="7f4a9-150">If you used an existing VM, you can skip the final [az group delete](/cli/azure/group?view=azure-cli-latest#az-group-delete) command to leave the resource group and VM in place.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-150">If you used an existing VM, you can skip the final [az group delete](/cli/azure/group?view=azure-cli-latest#az-group-delete) command to leave the resource group and VM in place.</span></span>

<span data-ttu-id="7f4a9-151">If you want to try a Backup tutorial that explains how to restore data for your VM, go to [Next steps](#next-steps).</span><span class="sxs-lookup"><span data-stu-id="7f4a9-151">If you want to try a Backup tutorial that explains how to restore data for your VM, go to [Next steps](#next-steps).</span></span> 

```azurecli-interactive 
az backup protection disable \
    --resource-group myResourceGroup \
    --vault-name myRecoveryServicesVault \
    --container-name myVM \
    --item-name myVM \
    --delete-backup-data true
az backup vault delete \
    --resource-group myResourceGroup \
    --name myRecoveryServicesVault \
az group delete --name myResourceGroup
```


## <a name="next-steps"></a><span data-ttu-id="7f4a9-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="7f4a9-152">Next steps</span></span>
<span data-ttu-id="7f4a9-153">In this quick start, you created a Recovery Services vault, enabled protection on a VM, and created the initial recovery point.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-153">In this quick start, you created a Recovery Services vault, enabled protection on a VM, and created the initial recovery point.</span></span> <span data-ttu-id="7f4a9-154">To learn more about Azure Backup and Recovery Services, continue to the tutorials.</span><span class="sxs-lookup"><span data-stu-id="7f4a9-154">To learn more about Azure Backup and Recovery Services, continue to the tutorials.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7f4a9-155">Back up multiple Azure VMs</span><span class="sxs-lookup"><span data-stu-id="7f4a9-155">Back up multiple Azure VMs</span></span>](./tutorial-backup-vm-at-scale.md)
