---
title: Deploy Linux VMs into existing networks - Azure portal | Microsoft Docs
description: Deploy a Linux VM into an existing Azure Virtual Network using the portal.
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
ms.date: 11/21/2016
ms.author: v-livech
ms.openlocfilehash: 5f7c1b074b16121a13472965d2c978e4aaf37a7a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553366"
---
# <a name="deploy-a-linux-vm-into-an-existing-vnet--nsg-using-the-portal"></a>Deploy a Linux VM into an existing VNet & NSG using the portal

This article shows how to deploy a VM into an existing virtual network (VNet).  It is recommended that Azure assets like the VNets and NSGs (Network Security Groups) should be static and long lived resources that are rarely deployed.  Once a VNet has been deployed, it can be reused by constant redeployments without any adverse affects to the infrastructure.  Thinking about a VNet as being a traditional hardware network switch, you would not need to configure a brand new hardware switch with each deployment.  

With a correctly configured VNet, we can continue to deploy new servers into that VNet over and over with few, if any, changes required over the life of the VNet.

## <a name="create-the-resource-group"></a>Create the Resource group

First we deploy a Resource Group to organize everything we create in this walkthrough.  For more information on Azure Resource Groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

![createResourceGroup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deploy-linux-vm-into-existing-vnet-using-portal/createresourcegroup.png)


## <a name="create-the-vnet"></a>Create the VNet

The first step is to build a VNet to launch the VMs into.  The VNet contains one subnet and we associate the NSG with this subnet in a later step.

![createVNet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deploy-linux-vm-into-existing-vnet-using-portal/createvnet.png)

## <a name="add-a-vnic-to-the-subnet"></a>Add a VNic to the subnet

Virtual network cards (VNics) are important as you can connect them to different VMs, which keeps the VNic as a static resource while the VMs can be temporary. Create a VNic and associate it with the Subnet created in the previous step.

![createVNic](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deploy-linux-vm-into-existing-vnet-using-portal/createvnic.png)

## <a name="create-the-nsg"></a>Create the NSG

Azure NSGs are equivalent to a firewall at the network layer. For more information on Azure NSGs, see [What is a Network Security Group](../../virtual-network/virtual-networks-nsg.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

![createNSG](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deploy-linux-vm-into-existing-vnet-using-portal/creatensg.png)

## <a name="add-an-inbound-ssh-allow-rule"></a>Add an inbound SSH allow rule

The Linux VM needs access from the internet so a rule allowing inbound port 22 traffic to be passed through the network to port 22 on the Linux VM is created.

![createInboundSSH](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deploy-linux-vm-into-existing-vnet-using-portal/createinboundssh.png)

## <a name="associate-the-nsg-with-the-subnet"></a>Associate the NSG with the subnet

With the VNet, and the subnet created, we associate the NSG with the subnet.  NSGs can be associated with either an entire subnet or an individual VNic.  With the firewall filtering traffic at the subnet level, all VNics and the VMs within the subnet are protected by the NSG versus the NSG being associated with just a single VNic and protecting just one VM.

![associateNSG](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deploy-linux-vm-into-existing-vnet-using-portal/associatensg.png)


## <a name="deploy-the-vm-into-the-vnet-and-nsg"></a>Deploy the VM into the VNet and NSG

Using the Azure portal, the Linux VM is deployed to the existing Azure Resource Group, VNet, Subnet, and VNic.

![createVM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/linux/media/deploy-linux-vm-into-existing-vnet-using-portal/createvm.png)

By using the portal to choose existing resources, we instruct Azure to deploy the VM inside the existing network.  To reiterate, once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.  

## <a name="next-steps"></a>Next steps

* [Use an Azure Resource Manager template to create a specific deployment](../windows/cli-deploy-templates.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Create your own custom environment for a Linux VM using Azure CLI commands directly](create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Create a Linux VM on Azure using templates](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)







