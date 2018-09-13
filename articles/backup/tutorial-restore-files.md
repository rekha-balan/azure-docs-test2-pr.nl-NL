---
title: Restore files to a VM with Azure Backup
description: Learn how to perform file-level restores on an Azure VM with Backup and Recovery Services.
services: backup
author: markgalioto
manager: carmonm
tags: azure-resource-manager, virtual-machine-backup
ms.service: backup
ms.topic: tutorial
ms.date: 2/14/2018
ms.author: markgal
ms.custom: mvc
ms.openlocfilehash: 2fd993960d8ae5d1f26939d333e546da760d8f43
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865361"
---
# <a name="restore-files-to-a-virtual-machine-in-azure"></a><span data-ttu-id="c539a-103">Restore files to a virtual machine in Azure</span><span class="sxs-lookup"><span data-stu-id="c539a-103">Restore files to a virtual machine in Azure</span></span>
<span data-ttu-id="c539a-104">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span><span class="sxs-lookup"><span data-stu-id="c539a-104">Azure Backup creates recovery points that are stored in geo-redundant recovery vaults.</span></span> <span data-ttu-id="c539a-105">When you restore from a recovery point, you can restore the whole VM or individual files.</span><span class="sxs-lookup"><span data-stu-id="c539a-105">When you restore from a recovery point, you can restore the whole VM or individual files.</span></span> <span data-ttu-id="c539a-106">This article details how to restore individual files.</span><span class="sxs-lookup"><span data-stu-id="c539a-106">This article details how to restore individual files.</span></span> <span data-ttu-id="c539a-107">In this tutorial you learn how to:</span><span class="sxs-lookup"><span data-stu-id="c539a-107">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c539a-108">List and select recovery points</span><span class="sxs-lookup"><span data-stu-id="c539a-108">List and select recovery points</span></span>
> * <span data-ttu-id="c539a-109">Connect a recovery point to a VM</span><span class="sxs-lookup"><span data-stu-id="c539a-109">Connect a recovery point to a VM</span></span>
> * <span data-ttu-id="c539a-110">Restore files from a recovery point</span><span class="sxs-lookup"><span data-stu-id="c539a-110">Restore files from a recovery point</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c539a-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.18 or later.</span><span class="sxs-lookup"><span data-stu-id="c539a-111">If you choose to install and use the CLI locally, this tutorial requires that you are running the Azure CLI version 2.0.18 or later.</span></span> <span data-ttu-id="c539a-112">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="c539a-112">Run `az --version` to find the version.</span></span> <span data-ttu-id="c539a-113">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c539a-113">If you need to install or upgrade, see [Install Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span> 


## <a name="prerequisites"></a><span data-ttu-id="c539a-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c539a-114">Prerequisites</span></span>
<span data-ttu-id="c539a-115">This tutorial requires a Linux VM that has been protected with Azure Backup.</span><span class="sxs-lookup"><span data-stu-id="c539a-115">This tutorial requires a Linux VM that has been protected with Azure Backup.</span></span> <span data-ttu-id="c539a-116">To simulate an accidental file deletion and recovery process, you delete a page from a web server.</span><span class="sxs-lookup"><span data-stu-id="c539a-116">To simulate an accidental file deletion and recovery process, you delete a page from a web server.</span></span> <span data-ttu-id="c539a-117">If you need a Linux VM that runs a webserver and has been protected with Azure Backup, see [Back up a virtual machine in Azure with the CLI](quick-backup-vm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="c539a-117">If you need a Linux VM that runs a webserver and has been protected with Azure Backup, see [Back up a virtual machine in Azure with the CLI](quick-backup-vm-cli.md).</span></span>


## <a name="backup-overview"></a><span data-ttu-id="c539a-118">Backup overview</span><span class="sxs-lookup"><span data-stu-id="c539a-118">Backup overview</span></span>
<span data-ttu-id="c539a-119">When Azure initiates a backup, the backup extension on the VM takes a point-in-time snapshot.</span><span class="sxs-lookup"><span data-stu-id="c539a-119">When Azure initiates a backup, the backup extension on the VM takes a point-in-time snapshot.</span></span> <span data-ttu-id="c539a-120">The backup extension is installed on the VM when the first backup is requested.</span><span class="sxs-lookup"><span data-stu-id="c539a-120">The backup extension is installed on the VM when the first backup is requested.</span></span> <span data-ttu-id="c539a-121">Azure Backup can also take a snapshot of the underlying storage if the VM is not running when the backup takes place.</span><span class="sxs-lookup"><span data-stu-id="c539a-121">Azure Backup can also take a snapshot of the underlying storage if the VM is not running when the backup takes place.</span></span>

<span data-ttu-id="c539a-122">By default, Azure Backup takes a file system consistent backup.</span><span class="sxs-lookup"><span data-stu-id="c539a-122">By default, Azure Backup takes a file system consistent backup.</span></span> <span data-ttu-id="c539a-123">Once Azure Backup takes the snapshot, the data is transferred to the Recovery Services vault.</span><span class="sxs-lookup"><span data-stu-id="c539a-123">Once Azure Backup takes the snapshot, the data is transferred to the Recovery Services vault.</span></span> <span data-ttu-id="c539a-124">To maximize efficiency, Azure Backup identifies and transfers only the blocks of data that have changed since the previous backup.</span><span class="sxs-lookup"><span data-stu-id="c539a-124">To maximize efficiency, Azure Backup identifies and transfers only the blocks of data that have changed since the previous backup.</span></span>

<span data-ttu-id="c539a-125">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span><span class="sxs-lookup"><span data-stu-id="c539a-125">When the data transfer is complete, the snapshot is removed and a recovery point is created.</span></span>


## <a name="delete-a-file-from-a-vm"></a><span data-ttu-id="c539a-126">Delete a file from a VM</span><span class="sxs-lookup"><span data-stu-id="c539a-126">Delete a file from a VM</span></span>
<span data-ttu-id="c539a-127">If you accidentally delete or make changes to a file, you can restore individual files from a recovery point.</span><span class="sxs-lookup"><span data-stu-id="c539a-127">If you accidentally delete or make changes to a file, you can restore individual files from a recovery point.</span></span> <span data-ttu-id="c539a-128">This process allows you to browse the files backed up in a recovery point and restore only the files you need.</span><span class="sxs-lookup"><span data-stu-id="c539a-128">This process allows you to browse the files backed up in a recovery point and restore only the files you need.</span></span> <span data-ttu-id="c539a-129">In this example, we delete a file from a web server to demonstrate the file-level recovery process.</span><span class="sxs-lookup"><span data-stu-id="c539a-129">In this example, we delete a file from a web server to demonstrate the file-level recovery process.</span></span>

1. <span data-ttu-id="c539a-130">To connect to your VM, obtain the IP address of your VM with [az vm show](/cli/azure/vm?view=azure-cli-latest#az-vm-show):</span><span class="sxs-lookup"><span data-stu-id="c539a-130">To connect to your VM, obtain the IP address of your VM with [az vm show](/cli/azure/vm?view=azure-cli-latest#az-vm-show):</span></span>

     ```azurecli-interactive
     az vm show --resource-group myResourceGroup --name myVM -d --query [publicIps] --o tsv
     ```

2. <span data-ttu-id="c539a-131">To confirm that your web site currently works, open a web browser to the public IP address of your VM.</span><span class="sxs-lookup"><span data-stu-id="c539a-131">To confirm that your web site currently works, open a web browser to the public IP address of your VM.</span></span> <span data-ttu-id="c539a-132">Leave the web browser window open.</span><span class="sxs-lookup"><span data-stu-id="c539a-132">Leave the web browser window open.</span></span>

    ![Default NGINX web page](./media/tutorial-restore-files/nginx-working.png)

3. <span data-ttu-id="c539a-134">Connect to your VM with SSH.</span><span class="sxs-lookup"><span data-stu-id="c539a-134">Connect to your VM with SSH.</span></span> <span data-ttu-id="c539a-135">Replace *publicIpAddress* with the public IP address that you obtained in a previous command:</span><span class="sxs-lookup"><span data-stu-id="c539a-135">Replace *publicIpAddress* with the public IP address that you obtained in a previous command:</span></span>

    ```bash
    ssh publicIpAddress
    ```

4. <span data-ttu-id="c539a-136">Delete the default page from the web server at */var/www/html/index.nginx-debian.html* as follows:</span><span class="sxs-lookup"><span data-stu-id="c539a-136">Delete the default page from the web server at */var/www/html/index.nginx-debian.html* as follows:</span></span>

    ```bash
    sudo rm /var/www/html/index.nginx-debian.html
    ```

5. <span data-ttu-id="c539a-137">In your web browser, refresh the web page.</span><span class="sxs-lookup"><span data-stu-id="c539a-137">In your web browser, refresh the web page.</span></span> <span data-ttu-id="c539a-138">The web site no longer loads the page, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="c539a-138">The web site no longer loads the page, as shown in the following example:</span></span>

    ![NGINX web site no longer loads default page](./media/tutorial-restore-files/nginx-broken.png)

6. <span data-ttu-id="c539a-140">Close the SSH session to your VM as follows:</span><span class="sxs-lookup"><span data-stu-id="c539a-140">Close the SSH session to your VM as follows:</span></span>

    ```bash
    exit
    ```


## <a name="generate-file-recovery-script"></a><span data-ttu-id="c539a-141">Generate file recovery script</span><span class="sxs-lookup"><span data-stu-id="c539a-141">Generate file recovery script</span></span>
<span data-ttu-id="c539a-142">To restore your files, Azure Backup provides a script to run on your VM that connects your recovery point as a local drive.</span><span class="sxs-lookup"><span data-stu-id="c539a-142">To restore your files, Azure Backup provides a script to run on your VM that connects your recovery point as a local drive.</span></span> <span data-ttu-id="c539a-143">You can browse this local drive, restore files to the VM itself, then disconnect the recovery point.</span><span class="sxs-lookup"><span data-stu-id="c539a-143">You can browse this local drive, restore files to the VM itself, then disconnect the recovery point.</span></span> <span data-ttu-id="c539a-144">Azure Backup continues to back up your data based on the assigned policy for schedule and retention.</span><span class="sxs-lookup"><span data-stu-id="c539a-144">Azure Backup continues to back up your data based on the assigned policy for schedule and retention.</span></span>

1. <span data-ttu-id="c539a-145">To list recovery points for your VM, use [az backup recoverypoint list](https://docs.microsoft.com/cli/azure/backup/recoverypoint?view=azure-cli-latest#az-backup-recoverypoint-list).</span><span class="sxs-lookup"><span data-stu-id="c539a-145">To list recovery points for your VM, use [az backup recoverypoint list](https://docs.microsoft.com/cli/azure/backup/recoverypoint?view=azure-cli-latest#az-backup-recoverypoint-list).</span></span> <span data-ttu-id="c539a-146">In this example, we select the most recent recovery point for the VM named *myVM* that is protected in *myRecoveryServicesVault*:</span><span class="sxs-lookup"><span data-stu-id="c539a-146">In this example, we select the most recent recovery point for the VM named *myVM* that is protected in *myRecoveryServicesVault*:</span></span>

    ```azurecli-interactive
    az backup recoverypoint list \
        --resource-group myResourceGroup \
        --vault-name myRecoveryServicesVault \
        --container-name myVM \
        --item-name myVM \
        --query [0].name \
        --output tsv
    ```

2. <span data-ttu-id="c539a-147">To obtain the script that connects, or mounts, the recovery point to your VM, use [az backup restore files mount-rp](https://docs.microsoft.com/cli/azure/backup/restore/files?view=azure-cli-latest#az-backup-restore-files-mount-rp).</span><span class="sxs-lookup"><span data-stu-id="c539a-147">To obtain the script that connects, or mounts, the recovery point to your VM, use [az backup restore files mount-rp](https://docs.microsoft.com/cli/azure/backup/restore/files?view=azure-cli-latest#az-backup-restore-files-mount-rp).</span></span> <span data-ttu-id="c539a-148">The following example obtains the script for the VM named *myVM* that is protected in *myRecoveryServicesVault*.</span><span class="sxs-lookup"><span data-stu-id="c539a-148">The following example obtains the script for the VM named *myVM* that is protected in *myRecoveryServicesVault*.</span></span>

    <span data-ttu-id="c539a-149">Replace *myRecoveryPointName* with the name of the recovery point that you obtained in the preceding command:</span><span class="sxs-lookup"><span data-stu-id="c539a-149">Replace *myRecoveryPointName* with the name of the recovery point that you obtained in the preceding command:</span></span>

    ```azurecli-interactive
    az backup restore files mount-rp \
        --resource-group myResourceGroup \
        --vault-name myRecoveryServicesVault \
        --container-name myVM \
        --item-name myVM \
        --rp-name myRecoveryPointName
    ```

    <span data-ttu-id="c539a-150">The script is downloaded and a password is displayed, as in the following example:</span><span class="sxs-lookup"><span data-stu-id="c539a-150">The script is downloaded and a password is displayed, as in the following example:</span></span>

    ```
    File downloaded: myVM_we_1571974050985163527.sh. Use password c068a041ce12465
    ```

3. <span data-ttu-id="c539a-151">To transfer the script to your VM, use Secure Copy (SCP).</span><span class="sxs-lookup"><span data-stu-id="c539a-151">To transfer the script to your VM, use Secure Copy (SCP).</span></span> <span data-ttu-id="c539a-152">Provide the name of your downloaded script, and replace *publicIpAddress* with the public IP address of your VM.</span><span class="sxs-lookup"><span data-stu-id="c539a-152">Provide the name of your downloaded script, and replace *publicIpAddress* with the public IP address of your VM.</span></span> <span data-ttu-id="c539a-153">Make sure you include the trailing `:` at the end of the SCP command as follows:</span><span class="sxs-lookup"><span data-stu-id="c539a-153">Make sure you include the trailing `:` at the end of the SCP command as follows:</span></span>

    ```bash
    scp myVM_we_1571974050985163527.sh 52.174.241.110:
    ```


## <a name="restore-file-to-your-vm"></a><span data-ttu-id="c539a-154">Restore file to your VM</span><span class="sxs-lookup"><span data-stu-id="c539a-154">Restore file to your VM</span></span>
<span data-ttu-id="c539a-155">With the recovery script copied to your VM, you can now connect the recovery point and restore files.</span><span class="sxs-lookup"><span data-stu-id="c539a-155">With the recovery script copied to your VM, you can now connect the recovery point and restore files.</span></span>

1. <span data-ttu-id="c539a-156">Connect to your VM with SSH.</span><span class="sxs-lookup"><span data-stu-id="c539a-156">Connect to your VM with SSH.</span></span> <span data-ttu-id="c539a-157">Replace *publicIpAddress* with the public IP address of your VM as follows:</span><span class="sxs-lookup"><span data-stu-id="c539a-157">Replace *publicIpAddress* with the public IP address of your VM as follows:</span></span>

    ```bash
    ssh publicIpAddress
    ```

2. <span data-ttu-id="c539a-158">To allow your script to run correctly, add execute permissions with **chmod**.</span><span class="sxs-lookup"><span data-stu-id="c539a-158">To allow your script to run correctly, add execute permissions with **chmod**.</span></span> <span data-ttu-id="c539a-159">Enter the name of your own script:</span><span class="sxs-lookup"><span data-stu-id="c539a-159">Enter the name of your own script:</span></span>

    ```bash
    chmod +x myVM_we_1571974050985163527.sh
    ```

3. <span data-ttu-id="c539a-160">To mount the recovery point, run the script.</span><span class="sxs-lookup"><span data-stu-id="c539a-160">To mount the recovery point, run the script.</span></span> <span data-ttu-id="c539a-161">Enter the name of your own script:</span><span class="sxs-lookup"><span data-stu-id="c539a-161">Enter the name of your own script:</span></span>

    ```bash
    ./myVM_we_1571974050985163527.sh
    ```

    <span data-ttu-id="c539a-162">As the script runs, you are prompted to enter a password to access the recovery point.</span><span class="sxs-lookup"><span data-stu-id="c539a-162">As the script runs, you are prompted to enter a password to access the recovery point.</span></span> <span data-ttu-id="c539a-163">Enter the password shown in the output from the previous [az backup restore files mount-rp](https://docs.microsoft.com/cli/azure/backup/restore/files?view=azure-cli-latest#az-backup-restore-files-mount-rp) command that generated the recovery script.</span><span class="sxs-lookup"><span data-stu-id="c539a-163">Enter the password shown in the output from the previous [az backup restore files mount-rp](https://docs.microsoft.com/cli/azure/backup/restore/files?view=azure-cli-latest#az-backup-restore-files-mount-rp) command that generated the recovery script.</span></span>

    <span data-ttu-id="c539a-164">The output from the script gives you the path for the recovery point.</span><span class="sxs-lookup"><span data-stu-id="c539a-164">The output from the script gives you the path for the recovery point.</span></span> <span data-ttu-id="c539a-165">The following example output shows that the recovery point is mounted at */home/azureuser/myVM-20170919213536/Volume1*:</span><span class="sxs-lookup"><span data-stu-id="c539a-165">The following example output shows that the recovery point is mounted at */home/azureuser/myVM-20170919213536/Volume1*:</span></span>

    ```
    Microsoft Azure VM Backup - File Recovery
    ______________________________________________
    Please enter the password as shown on the portal to securely connect to the recovery point. : c068a041ce12465
    
    Connecting to recovery point using ISCSI service...
    
    Connection succeeded!
    
    Please wait while we attach volumes of the recovery point to this machine...
    
    ************ Volumes of the recovery point and their mount paths on this machine ************
    
    Sr.No.  |  Disk  |  Volume  |  MountPath
    
    1)  | /dev/sdc  |  /dev/sdc1  |  /home/azureuser/myVM-20170919213536/Volume1
    
    ************ Open File Explorer to browse for files. ************
    ```

4. <span data-ttu-id="c539a-166">Use **cp** to copy the NGINX default web page from the mounted recovery point back to the original file location.</span><span class="sxs-lookup"><span data-stu-id="c539a-166">Use **cp** to copy the NGINX default web page from the mounted recovery point back to the original file location.</span></span> <span data-ttu-id="c539a-167">Replace the */home/azureuser/myVM-20170919213536/Volume1* mount point with your own location:</span><span class="sxs-lookup"><span data-stu-id="c539a-167">Replace the */home/azureuser/myVM-20170919213536/Volume1* mount point with your own location:</span></span>

    ```bash
    sudo cp /home/azureuser/myVM-20170919213536/Volume1/var/www/html/index.nginx-debian.html /var/www/html/
    ```

6. <span data-ttu-id="c539a-168">In your web browser, refresh the web page.</span><span class="sxs-lookup"><span data-stu-id="c539a-168">In your web browser, refresh the web page.</span></span> <span data-ttu-id="c539a-169">The web site now loads correctly again, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="c539a-169">The web site now loads correctly again, as shown in the following example:</span></span>

    ![NGINX web site now loads correctly](./media/tutorial-restore-files/nginx-restored.png)

7. <span data-ttu-id="c539a-171">Close the SSH session to your VM as follows:</span><span class="sxs-lookup"><span data-stu-id="c539a-171">Close the SSH session to your VM as follows:</span></span>

    ```bash
    exit
    ```

8. <span data-ttu-id="c539a-172">Unmount the recovery point from your VM with [az backup restore files unmount-rp](https://docs.microsoft.com/cli/azure/backup/restore/files?view=azure-cli-latest#az-backup-restore-files-unmount-rp).</span><span class="sxs-lookup"><span data-stu-id="c539a-172">Unmount the recovery point from your VM with [az backup restore files unmount-rp](https://docs.microsoft.com/cli/azure/backup/restore/files?view=azure-cli-latest#az-backup-restore-files-unmount-rp).</span></span> <span data-ttu-id="c539a-173">The following example unmounts the recovery point from the VM named *myVM* in *myRecoveryServicesVault*.</span><span class="sxs-lookup"><span data-stu-id="c539a-173">The following example unmounts the recovery point from the VM named *myVM* in *myRecoveryServicesVault*.</span></span>

    <span data-ttu-id="c539a-174">Replace *myRecoveryPointName* with the name of your recovery point that you obtained in the previous commands:</span><span class="sxs-lookup"><span data-stu-id="c539a-174">Replace *myRecoveryPointName* with the name of your recovery point that you obtained in the previous commands:</span></span>
    
    ```azurecli-interactive
    az backup restore files unmount-rp \
        --resource-group myResourceGroup \
        --vault-name myRecoveryServicesVault \
        --container-name myVM \
        --item-name myVM \
        --rp-name myRecoveryPointName
    ```

## <a name="next-steps"></a><span data-ttu-id="c539a-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="c539a-175">Next steps</span></span>
<span data-ttu-id="c539a-176">In this tutorial, you connected a recovery point to a VM and restored files for a web server.</span><span class="sxs-lookup"><span data-stu-id="c539a-176">In this tutorial, you connected a recovery point to a VM and restored files for a web server.</span></span> <span data-ttu-id="c539a-177">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="c539a-177">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c539a-178">List and select recovery points</span><span class="sxs-lookup"><span data-stu-id="c539a-178">List and select recovery points</span></span>
> * <span data-ttu-id="c539a-179">Connect a recovery point to a VM</span><span class="sxs-lookup"><span data-stu-id="c539a-179">Connect a recovery point to a VM</span></span>
> * <span data-ttu-id="c539a-180">Restore files from a recovery point</span><span class="sxs-lookup"><span data-stu-id="c539a-180">Restore files from a recovery point</span></span>

<span data-ttu-id="c539a-181">Advance to the next tutorial to learn about how to back up Windows Server to Azure.</span><span class="sxs-lookup"><span data-stu-id="c539a-181">Advance to the next tutorial to learn about how to back up Windows Server to Azure.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c539a-182">Back up Windows Server to Azure</span><span class="sxs-lookup"><span data-stu-id="c539a-182">Back up Windows Server to Azure</span></span>](tutorial-backup-windows-server-to-azure.md)

