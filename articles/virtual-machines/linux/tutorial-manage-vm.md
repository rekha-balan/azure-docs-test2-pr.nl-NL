---
title: Manage Linux virtual machines with the Azure CLI | Microsoft Docs
description: Tutorial - Manage Linux virtual machines with the Azure CLI
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/28/2017
ms.author: nepeters
ms.openlocfilehash: 3fb5b3560b0c584b2d69f9257b2087b75017255a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553307"
---
# <a name="manage-linux-virtual-machines-with-the-azure-cli"></a><span data-ttu-id="e855c-103">Manage Linux virtual machines with the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e855c-103">Manage Linux virtual machines with the Azure CLI</span></span>

<span data-ttu-id="e855c-104">In this tutorial, you will create a virtual machine and perform common management tasks such as adding a disk, automating software installation, and creating a virtual machine snapshot.</span><span class="sxs-lookup"><span data-stu-id="e855c-104">In this tutorial, you will create a virtual machine and perform common management tasks such as adding a disk, automating software installation, and creating a virtual machine snapshot.</span></span> 

<span data-ttu-id="e855c-105">To complete this tutorial, make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="e855c-105">To complete this tutorial, make sure that you have installed the latest [Azure CLI 2.0](/cli/azure/install-azure-cli).</span></span>

## <a name="step-1--log-in-to-azure"></a><span data-ttu-id="e855c-106">Step 1 – Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="e855c-106">Step 1 – Log in to Azure</span></span>

<span data-ttu-id="e855c-107">First, open up a terminal and log in to your Azure subscription with the [az login](/cli/azure/#login) command.</span><span class="sxs-lookup"><span data-stu-id="e855c-107">First, open up a terminal and log in to your Azure subscription with the [az login](/cli/azure/#login) command.</span></span>

```azurecli
az login
```

## <a name="step-2--create-resource-group"></a><span data-ttu-id="e855c-108">Step 2 – Create resource group</span><span class="sxs-lookup"><span data-stu-id="e855c-108">Step 2 – Create resource group</span></span>

<span data-ttu-id="e855c-109">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span><span class="sxs-lookup"><span data-stu-id="e855c-109">Create a resource group with the [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> 

<span data-ttu-id="e855c-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span><span class="sxs-lookup"><span data-stu-id="e855c-110">An Azure resource group is a logical container into which Azure resources are deployed and managed.</span></span> <span data-ttu-id="e855c-111">A resource group must be created before a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-111">A resource group must be created before a virtual machine.</span></span> <span data-ttu-id="e855c-112">In this example, a resource group named `myResourceGroup` is created in the `westeurope` region.</span><span class="sxs-lookup"><span data-stu-id="e855c-112">In this example, a resource group named `myResourceGroup` is created in the `westeurope` region.</span></span> 

```azurecli
az group create --name myResourceGroup --location westeurope
```

## <a name="step-3---prepare-configuration"></a><span data-ttu-id="e855c-113">Step 3 - Prepare configuration</span><span class="sxs-lookup"><span data-stu-id="e855c-113">Step 3 - Prepare configuration</span></span>

<span data-ttu-id="e855c-114">When deploying a virtual machine, **cloud-init** can be used to automate configurations such as installing packages, creating files, and running scripts.</span><span class="sxs-lookup"><span data-stu-id="e855c-114">When deploying a virtual machine, **cloud-init** can be used to automate configurations such as installing packages, creating files, and running scripts.</span></span> <span data-ttu-id="e855c-115">In this tutorial, the configurations of two items are automated:</span><span class="sxs-lookup"><span data-stu-id="e855c-115">In this tutorial, the configurations of two items are automated:</span></span>

- <span data-ttu-id="e855c-116">Installing an NGINX webserver</span><span class="sxs-lookup"><span data-stu-id="e855c-116">Installing an NGINX webserver</span></span>
- <span data-ttu-id="e855c-117">Provisioning a second disk on the VM</span><span class="sxs-lookup"><span data-stu-id="e855c-117">Provisioning a second disk on the VM</span></span>

<span data-ttu-id="e855c-118">Because the **cloud-init** configuration happens at VM deployment time, a **cloud-init** configuration needs to be defined before creating the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-118">Because the **cloud-init** configuration happens at VM deployment time, a **cloud-init** configuration needs to be defined before creating the virtual machine.</span></span>

<span data-ttu-id="e855c-119">Create a file name `cloud-init.txt` and copy in the following content.</span><span class="sxs-lookup"><span data-stu-id="e855c-119">Create a file name `cloud-init.txt` and copy in the following content.</span></span> <span data-ttu-id="e855c-120">This configuration installs the NGINX package and runs commands to formant and mount the second disk.</span><span class="sxs-lookup"><span data-stu-id="e855c-120">This configuration installs the NGINX package and runs commands to formant and mount the second disk.</span></span>

```yaml
#cloud-config
package_upgrade: true
packages:
  - nginx
runcmd:
  - (echo n; echo p; echo 1; echo ; echo ; echo w) | sudo fdisk /dev/sdc
  - sudo mkfs -t ext4 /dev/sdc1
  - sudo mkdir /datadrive
  - sudo mount /dev/sdc1 /datadrive
```

## <a name="step-4---create-virtual-machine"></a><span data-ttu-id="e855c-121">Step 4 - Create virtual machine</span><span class="sxs-lookup"><span data-stu-id="e855c-121">Step 4 - Create virtual machine</span></span>

<span data-ttu-id="e855c-122">Create a virtual machine with the [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span><span class="sxs-lookup"><span data-stu-id="e855c-122">Create a virtual machine with the [az vm create](https://docs.microsoft.com/cli/azure/vm#create) command.</span></span> 

<span data-ttu-id="e855c-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span><span class="sxs-lookup"><span data-stu-id="e855c-123">When creating a virtual machine, several options are available such as operating system image, disk sizing, and administrative credentials.</span></span> <span data-ttu-id="e855c-124">In this example, a virtual machine is created with a name of `myVM` running Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e855c-124">In this example, a virtual machine is created with a name of `myVM` running Ubuntu.</span></span> <span data-ttu-id="e855c-125">A 50-GB disk is created and attached to the VM using the `--data-disk-sizes-gb` argument.</span><span class="sxs-lookup"><span data-stu-id="e855c-125">A 50-GB disk is created and attached to the VM using the `--data-disk-sizes-gb` argument.</span></span> <span data-ttu-id="e855c-126">The `--custom-data` argument takes in the cloud-init configuration and stages it on the VM.</span><span class="sxs-lookup"><span data-stu-id="e855c-126">The `--custom-data` argument takes in the cloud-init configuration and stages it on the VM.</span></span> <span data-ttu-id="e855c-127">Finally, SSH keys are also created if they do not exist.</span><span class="sxs-lookup"><span data-stu-id="e855c-127">Finally, SSH keys are also created if they do not exist.</span></span>

```azurecli
az vm create \
  --resource-group myResourceGroup \
  --name myVM \
  --image Canonical:UbuntuServer:14.04.4-LTS:latest \
  --generate-ssh-keys \
  --data-disk-sizes-gb 50 \
  --custom-data cloud-init.txt
```

<span data-ttu-id="e855c-128">Once the VM has been created, the Azure CLI outputs the following information.</span><span class="sxs-lookup"><span data-stu-id="e855c-128">Once the VM has been created, the Azure CLI outputs the following information.</span></span> <span data-ttu-id="e855c-129">Take note of the public IP address, this address is used when accessing the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-129">Take note of the public IP address, this address is used when accessing the virtual machine.</span></span> 

```azurecli
{
  "fqdns": "",
  "id": "/subscriptions/d5b9d4b7-6fc1-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myVM",
  "location": "westeurope",
  "macAddress": "00-0D-3A-23-9A-49",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "52.174.34.95",
  "resourceGroup": "myResourceGroup"
}
```

<span data-ttu-id="e855c-130">While the VM has been deployed, the **cloud-init** configuration may take a few minutes to complete.</span><span class="sxs-lookup"><span data-stu-id="e855c-130">While the VM has been deployed, the **cloud-init** configuration may take a few minutes to complete.</span></span> 

## <a name="step-5--configure-firewall"></a><span data-ttu-id="e855c-131">Step 5 – Configure firewall</span><span class="sxs-lookup"><span data-stu-id="e855c-131">Step 5 – Configure firewall</span></span>

<span data-ttu-id="e855c-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span><span class="sxs-lookup"><span data-stu-id="e855c-132">An Azure [network security group](../../virtual-network/virtual-networks-nsg.md) (NSG) controls inbound and outbound traffic for one or many virtual machines.</span></span> <span data-ttu-id="e855c-133">Network security group rules allow or deny network traffic on a specific port or port range.</span><span class="sxs-lookup"><span data-stu-id="e855c-133">Network security group rules allow or deny network traffic on a specific port or port range.</span></span> <span data-ttu-id="e855c-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-134">These rules can also include a source address prefix so that only traffic originating at a predefined source can communicate with a virtual machine.</span></span>

<span data-ttu-id="e855c-135">In the previous section, the NGINX webserver was installed.</span><span class="sxs-lookup"><span data-stu-id="e855c-135">In the previous section, the NGINX webserver was installed.</span></span> <span data-ttu-id="e855c-136">Without a network security group rule to allow inbound traffic on port 80, the webserver cannot be accessed on the internet.</span><span class="sxs-lookup"><span data-stu-id="e855c-136">Without a network security group rule to allow inbound traffic on port 80, the webserver cannot be accessed on the internet.</span></span> <span data-ttu-id="e855c-137">This step walks you through creating the NSG rule to allow inbound connections on port 80.</span><span class="sxs-lookup"><span data-stu-id="e855c-137">This step walks you through creating the NSG rule to allow inbound connections on port 80.</span></span>

### <a name="create-nsg-rule"></a><span data-ttu-id="e855c-138">Create NSG rule</span><span class="sxs-lookup"><span data-stu-id="e855c-138">Create NSG rule</span></span>

<span data-ttu-id="e855c-139">To create an inbound NSG rule, use the [az vm open-port](https://docs.microsoft.com/cli/azure/vm#open-port) command.</span><span class="sxs-lookup"><span data-stu-id="e855c-139">To create an inbound NSG rule, use the [az vm open-port](https://docs.microsoft.com/cli/azure/vm#open-port) command.</span></span> <span data-ttu-id="e855c-140">The following example opens port `80` for the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-140">The following example opens port `80` for the virtual machine.</span></span>

```azurecli
az vm open-port --port 80 --resource-group myResourceGroup --name myVM 
```

<span data-ttu-id="e855c-141">Now browse to the public IP address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-141">Now browse to the public IP address of the virtual machine.</span></span> <span data-ttu-id="e855c-142">With the NSG rule in place, the default NGINX website is displayed.</span><span class="sxs-lookup"><span data-stu-id="e855c-142">With the NSG rule in place, the default NGINX website is displayed.</span></span>

![NGINX default site](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/tutorial-manage-vm/nginx.png)  

## <a name="step-6--snapshot-virtual-machine"></a><span data-ttu-id="e855c-144">Step 6 – Snapshot virtual machine</span><span class="sxs-lookup"><span data-stu-id="e855c-144">Step 6 – Snapshot virtual machine</span></span>

<span data-ttu-id="e855c-145">Taking a disk snapshot creates a read only, point-in-time copy of the disk.</span><span class="sxs-lookup"><span data-stu-id="e855c-145">Taking a disk snapshot creates a read only, point-in-time copy of the disk.</span></span> <span data-ttu-id="e855c-146">In this step, a snapshot is taken of the VMs operating system disk.</span><span class="sxs-lookup"><span data-stu-id="e855c-146">In this step, a snapshot is taken of the VMs operating system disk.</span></span> <span data-ttu-id="e855c-147">With an OS disk snapshot, the virtual machine can be quickly restored to a specific state, or the snapshot can be used to create a new virtual machine with an identical state.</span><span class="sxs-lookup"><span data-stu-id="e855c-147">With an OS disk snapshot, the virtual machine can be quickly restored to a specific state, or the snapshot can be used to create a new virtual machine with an identical state.</span></span>

### <a name="create-snapshot"></a><span data-ttu-id="e855c-148">Create snapshot</span><span class="sxs-lookup"><span data-stu-id="e855c-148">Create snapshot</span></span>

<span data-ttu-id="e855c-149">Before creating a snapshot, the Id or name of the disk is needed.</span><span class="sxs-lookup"><span data-stu-id="e855c-149">Before creating a snapshot, the Id or name of the disk is needed.</span></span> <span data-ttu-id="e855c-150">Use the [az vm show](https://docs.microsoft.com/cli/azure/vm#show) command to get the disk id. In this example, the disk id is stored in a variable and is used in a later step.</span><span class="sxs-lookup"><span data-stu-id="e855c-150">Use the [az vm show](https://docs.microsoft.com/cli/azure/vm#show) command to get the disk id. In this example, the disk id is stored in a variable and is used in a later step.</span></span>

```azurecli
osdiskid=$(az vm show -g myResourceGroup -n myVM --query "storageProfile.osDisk.managedDisk.id" -o tsv)
```

<span data-ttu-id="e855c-151">Now that you have the id of the disk, the following command creates the snapshot.</span><span class="sxs-lookup"><span data-stu-id="e855c-151">Now that you have the id of the disk, the following command creates the snapshot.</span></span>

```azurcli
az snapshot create -g myResourceGroup --source "$osdiskid" --name osDisk-backup
```

### <a name="create-disk-from-snapshot"></a><span data-ttu-id="e855c-152">Create disk from snapshot</span><span class="sxs-lookup"><span data-stu-id="e855c-152">Create disk from snapshot</span></span>

<span data-ttu-id="e855c-153">This snapshot can then be converted into a disk, which can be used to recreate the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-153">This snapshot can then be converted into a disk, which can be used to recreate the virtual machine.</span></span>

```azurecli
az disk create --resource-group myResourceGroup --name mySnapshotDisk --source osDisk-backup
```

### <a name="restore-virtual-machine-from-snapshot"></a><span data-ttu-id="e855c-154">Restore virtual machine from snapshot</span><span class="sxs-lookup"><span data-stu-id="e855c-154">Restore virtual machine from snapshot</span></span>

<span data-ttu-id="e855c-155">To demonstrate virtual machine recovery, delete the existing virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-155">To demonstrate virtual machine recovery, delete the existing virtual machine.</span></span> 

```azurecli
az vm delete --resource-group myResourceGroup --name myVM
```

<span data-ttu-id="e855c-156">When re-creating the virtual machine, the existing network interface will be re-used.</span><span class="sxs-lookup"><span data-stu-id="e855c-156">When re-creating the virtual machine, the existing network interface will be re-used.</span></span> <span data-ttu-id="e855c-157">This ensures that network security configurations are retained.</span><span class="sxs-lookup"><span data-stu-id="e855c-157">This ensures that network security configurations are retained.</span></span>

<span data-ttu-id="e855c-158">Get the network interface name using the [az network nic list](https://docs.microsoft.com/cli/azure/network/nic#list) command.</span><span class="sxs-lookup"><span data-stu-id="e855c-158">Get the network interface name using the [az network nic list](https://docs.microsoft.com/cli/azure/network/nic#list) command.</span></span> <span data-ttu-id="e855c-159">This example places the name in a variable named `nic`, which is used in the next step.</span><span class="sxs-lookup"><span data-stu-id="e855c-159">This example places the name in a variable named `nic`, which is used in the next step.</span></span>

```azurecli
nic=$(az network nic list --resource-group myResourceGroup --query "[].[name]" -o tsv)
```

<span data-ttu-id="e855c-160">Create a new virtual machine from the snapshot disk.</span><span class="sxs-lookup"><span data-stu-id="e855c-160">Create a new virtual machine from the snapshot disk.</span></span>

```azurecli
az vm create --resource-group myResourceGroup --name myVM --attach-os-disk mySnapshotDisk --os-type linux --nics $nic
```

<span data-ttu-id="e855c-161">Take note of the new public ip address, and browser to this address with an internet browser.</span><span class="sxs-lookup"><span data-stu-id="e855c-161">Take note of the new public ip address, and browser to this address with an internet browser.</span></span> <span data-ttu-id="e855c-162">You will see that NGINX is running in the restored virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-162">You will see that NGINX is running in the restored virtual machine.</span></span> 

### <a name="reconfigure-data-disk"></a><span data-ttu-id="e855c-163">Reconfigure data disk</span><span class="sxs-lookup"><span data-stu-id="e855c-163">Reconfigure data disk</span></span>

<span data-ttu-id="e855c-164">The data disk can now be reattached to the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-164">The data disk can now be reattached to the virtual machine.</span></span> 

<span data-ttu-id="e855c-165">First find the data disks name using the [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span><span class="sxs-lookup"><span data-stu-id="e855c-165">First find the data disks name using the [az disk list](https://docs.microsoft.com/cli/azure/disk#list) command.</span></span> <span data-ttu-id="e855c-166">This example places the name of the disk in a variable named `datadisk`, which is used in the next step.</span><span class="sxs-lookup"><span data-stu-id="e855c-166">This example places the name of the disk in a variable named `datadisk`, which is used in the next step.</span></span>

```azurecli
datadisk=$(az disk list -g myResourceGroup --query "[?contains(name,'myVM')].[name]" -o tsv)
```

<span data-ttu-id="e855c-167">Use the [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command to attach the disk.</span><span class="sxs-lookup"><span data-stu-id="e855c-167">Use the [az vm disk attach](https://docs.microsoft.com/cli/azure/vm/disk#attach) command to attach the disk.</span></span>

```azurecli
az vm disk attach –g myResourceGroup –-vm-name myVM –-disk $datadisk
```

<span data-ttu-id="e855c-168">The disk also needs to be mounted to the operating system.</span><span class="sxs-lookup"><span data-stu-id="e855c-168">The disk also needs to be mounted to the operating system.</span></span> <span data-ttu-id="e855c-169">To mount the disk, connect to the virtual machine and run `sudo mount /dev/sdc1 /datadrive`, or your preferred disk mounting operation.</span><span class="sxs-lookup"><span data-stu-id="e855c-169">To mount the disk, connect to the virtual machine and run `sudo mount /dev/sdc1 /datadrive`, or your preferred disk mounting operation.</span></span> 

## <a name="step-7--management-tasks"></a><span data-ttu-id="e855c-170">Step 7 – Management tasks</span><span class="sxs-lookup"><span data-stu-id="e855c-170">Step 7 – Management tasks</span></span>

<span data-ttu-id="e855c-171">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-171">During the lifecycle of a virtual machine, you may want to run management tasks such as starting, stopping, or deleting a virtual machine.</span></span> <span data-ttu-id="e855c-172">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span><span class="sxs-lookup"><span data-stu-id="e855c-172">Additionally, you may want to create scripts to automate repetitive or complex tasks.</span></span> <span data-ttu-id="e855c-173">Using the Azure CLI, many common management tasks can be run from the command line or in scripts.</span><span class="sxs-lookup"><span data-stu-id="e855c-173">Using the Azure CLI, many common management tasks can be run from the command line or in scripts.</span></span> 

### <a name="get-ip-address"></a><span data-ttu-id="e855c-174">Get IP address</span><span class="sxs-lookup"><span data-stu-id="e855c-174">Get IP address</span></span>

<span data-ttu-id="e855c-175">This command returns the private and public IP addresses of a virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e855c-175">This command returns the private and public IP addresses of a virtual machine.</span></span>  

```azurecli
az vm list-ip-addresses --resource-group myResourceGroup --name myVM
```

### <a name="resize-virtual-machine"></a><span data-ttu-id="e855c-176">Resize virtual machine</span><span class="sxs-lookup"><span data-stu-id="e855c-176">Resize virtual machine</span></span>

<span data-ttu-id="e855c-177">To resize an Azure virtual machine, you need to know the name of the sizes available in the chosen Azure region.</span><span class="sxs-lookup"><span data-stu-id="e855c-177">To resize an Azure virtual machine, you need to know the name of the sizes available in the chosen Azure region.</span></span> <span data-ttu-id="e855c-178">These sizes can be found with the [az vm list-sizes](https://docs.microsoft.com/cli/azure/vm#list-sizes) command.</span><span class="sxs-lookup"><span data-stu-id="e855c-178">These sizes can be found with the [az vm list-sizes](https://docs.microsoft.com/cli/azure/vm#list-sizes) command.</span></span>

```azurecli
az vm list-sizes --location westeurope --output table
```

<span data-ttu-id="e855c-179">The virtual machine can be resized using the [az vm resize](https://docs.microsoft.com/cli/azure/vm#resize) command.</span><span class="sxs-lookup"><span data-stu-id="e855c-179">The virtual machine can be resized using the [az vm resize](https://docs.microsoft.com/cli/azure/vm#resize) command.</span></span> 

```azurecli
az vm resize -g myResourceGroup -n myVM --size Standard_F4s
```

### <a name="stop-virtual-machine"></a><span data-ttu-id="e855c-180">Stop virtual machine</span><span class="sxs-lookup"><span data-stu-id="e855c-180">Stop virtual machine</span></span>

```azurecli
az vm stop --resource-group myResourceGroup --name myVM
```

### <a name="start-virtual-machine"></a><span data-ttu-id="e855c-181">Start virtual machine</span><span class="sxs-lookup"><span data-stu-id="e855c-181">Start virtual machine</span></span>

```azurecli
az vm start --resource-group myResourceGroup --name myVM
```

### <a name="delete-resource-group"></a><span data-ttu-id="e855c-182">Delete resource group</span><span class="sxs-lookup"><span data-stu-id="e855c-182">Delete resource group</span></span>

<span data-ttu-id="e855c-183">Deleting a resource group also deletes all resources contained within.</span><span class="sxs-lookup"><span data-stu-id="e855c-183">Deleting a resource group also deletes all resources contained within.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="next-steps"></a><span data-ttu-id="e855c-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="e855c-184">Next steps</span></span>
<span data-ttu-id="e855c-185">This tutorial creates a single virtual machine using the individual Azure resources.</span><span class="sxs-lookup"><span data-stu-id="e855c-185">This tutorial creates a single virtual machine using the individual Azure resources.</span></span> <span data-ttu-id="e855c-186">The next tutorial builds on these concepts to create a highly available application that is load balanced and resilient to maintenance events.</span><span class="sxs-lookup"><span data-stu-id="e855c-186">The next tutorial builds on these concepts to create a highly available application that is load balanced and resilient to maintenance events.</span></span> <span data-ttu-id="e855c-187">Continue on to the next tutorial - [Build a load balanced, highly available application on Linux virtual machines in Azure](tutorial-load-balance-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e855c-187">Continue on to the next tutorial - [Build a load balanced, highly available application on Linux virtual machines in Azure](tutorial-load-balance-nodejs.md).</span></span>

<span data-ttu-id="e855c-188">Samples – [Azure CLI sample scripts](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="e855c-188">Samples – [Azure CLI sample scripts](../windows/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)</span></span>
