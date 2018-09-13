---
title: Create a Classic Linux VM using the Azure CLI 1.0 | Microsoft Docs
description: Learn how to create a Linux virtual machine with the Azure CLI 1.0 using the Classic deployment model
services: virtual-machines-linux
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 6415e6238dc817ed0175933f989aafa0c6c42fc9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549233"
---
# <a name="how-to-create-a-classic-linux-vm-with-the-azure-cli-10"></a>How to Create a Classic Linux VM with the Azure CLI 1.0
> [!IMPORTANT] 
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. For the Resource Manager version, see [here](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

This topic describes how to create a Linux virtual machine (VM) with the Azure CLI 1.0 using the Classic deployment model. We use a Linux image from the available **IMAGES** on Azure. The Azure CLI 1.0 commands give the following configuration choices, among others:

* Connecting the VM to a virtual network
* Adding the VM to an existing cloud service
* Adding the VM to an existing storage account
* Adding the VM to an availability set or location

> [!IMPORTANT]
> If you want your VM to use a virtual network so you can connect to it directly by hostname or set up cross-premises connections, make sure you specify the virtual network when you create the VM. A VM can be configured to join a virtual network only when you create the VM. For details on virtual networks, see [Azure Virtual Network Overview](http://go.microsoft.com/fwlink/p/?LinkID=294063).
> 
> 

## <a name="how-to-create-a-linux-vm-using-the-classic-deployment-model"></a>How to create a Linux VM using the Classic deployment model
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

