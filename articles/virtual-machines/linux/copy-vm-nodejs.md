---
title: Create a copy of your Linux VM with the Azure CLI 1.0 | Microsoft Docs
description: Learn how to create a copy of your Azure Linux virtual machine with the Azure CLI 1.0 in the Resource Manager deployment model
services: virtual-machines-linux
documentationcenter: ''
author: cynthn
manager: timlt
tags: azure-resource-manager
ms.assetid: 770569d2-23c1-4a5b-801e-cddcd1375164
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 03/22/2017
ms.author: cynthn
ms.openlocfilehash: 4448c57cdd8a0d0bc94e013f7da74e1a332bfd42
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549762"
---
# <a name="create-a-copy-of-a-linux-virtual-machine-running-on-azure-with-the-azure-cli-10"></a>Create a copy of a Linux virtual machine running on Azure with the Azure CLI 1.0
This article shows you how to create a copy of your Azure virtual machine (VM) running Linux using the Resource Manager deployment model. First you copy over the operating system and data disks to a new container, then set up the network resources and create the new virtual machine.

You can also [upload and create a VM from custom disk image](upload-vhd.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

## <a name="cli-versions-to-complete-the-task"></a>CLI versions to complete the task
You can complete the task using one of the following CLI versions:

- Azure CLI 1.0 – our CLI for the classic and resource management deployment models (this article)
- [Azure CLI 2.0](copy-vm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) - our next generation CLI for the resource management deployment model

## <a name="before-you-begin"></a>Before you begin
Ensure that you meet the following prerequisites before you start the steps:

* You have the [Azure CLI](../../cli-install-nodejs.md) downloaded and installed on your machine. 
* You also need some information about your existing Azure Linux VM:

| Source VM information | Where to get it |
| --- | --- |
| VM name |`azure vm list` |
| Resource Group name |`azure vm list` |
| Location |`azure vm list` |
| Storage Account name |`azure storage account list -g <resourceGroup>` |
| Container name |`azure storage container list -a <sourcestorageaccountname>` |
| Source VM VHD file name |`azure storage blob list --container <containerName>` |

* You will need to make some choices about your new VM:    <br> -Container name    <br> -VM name    <br> -VM size    <br> -vNet name    <br> -SubNet name    <br> -IP Name    <br> -NIC name

## <a name="login-and-set-your-subscription"></a>Login and set your subscription
1. Login to the CLI.

    ```azurecli
    azure login
    ```
2. Make sure you are in Resource Manager mode.

    ```azurecli
    azure config mode arm
    ```
3. Set the correct subscription. You can use 'azure account list' to see all of your subscriptions.

    ```azurecli
    azure account set mySubscriptionID
    ```

## <a name="stop-the-vm"></a>Stop the VM
Stop and deallocate the source VM. You can use 'azure vm list' to get a list of all of the VMs in your subscription and their resource group names.

```azurecli
azure vm stop myResourceGroup myVM
azure vm deallocate myResourceGroup MyVM
```


## <a name="copy-the-vhd"></a>Copy the VHD
You can copy the VHD from the source storage to the destination using the `azure storage blob copy start`. In this example, we are going to copy the VHD to the same storage account, but a different container.

To copy the VHD to another container in the same storage account, type:

```azurecli
azure storage blob copy start \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd \
        myNewContainerName
```

## <a name="set-up-the-virtual-network-for-your-new-vm"></a>Set up the virtual network for your new VM
Set up a virtual network and NIC for your new VM. 

```azurecli
azure network vnet create myResourceGroup myVnet -l myLocation

azure network vnet subnet create -a <address.prefix.in.CIDR/format> myResourceGroup myVnet mySubnet

azure network public-ip create myResourceGroup myPublicIP -l myLocation

azure network nic create myResourceGroup myNic -k mySubnet -m myVnet -p myPublicIP -l myLocation
```


## <a name="create-the-new-vm"></a>Create the new VM
You can now create a VM from your uploaded virtual disk [using a resource manager template](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-from-specialized-vhd) or through the CLI by specifying the URI to your copied disk by typing:

```azurecli
azure vm create -n myVM -l myLocation -g myResourceGroup -f myNic \
        -z Standard_DS1_v2 -y Linux \
        https://mystorageaccountname.blob.core.windows.net:8080/mycontainername/myVHD.vhd 
```



## <a name="next-steps"></a>Next steps
To learn how to use Azure CLI to manage your new virtual machine, see [Azure CLI commands for the Azure Resource Manager](../azure-cli-arm-commands.md).

