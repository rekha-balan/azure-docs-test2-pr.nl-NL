---
title: Azure Virtual Machines Guidelines | Microsoft Docs
description: Learn about the key design and implementation guidelines for deploying Windows virtual machines into Azure
documentationcenter: ''
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: f932e65a-437b-48b0-8d70-f61ded8ce1c6
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/17/2017
ms.author: iainfou
ms.openlocfilehash: 4bb9fa9f9beb2055768fbee0a3bb63d59e37f34f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562723"
---
# <a name="azure-virtual-machines-guidelines-for-windows"></a>Azure virtual machines guidelines for Windows
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

This article focuses on understanding the required planning steps for creating and managing virtual machines (VMs) within your Azure environment.

## <a name="implementation-guidelines-for-vms"></a>Implementation guidelines for VMs
Decisions:

* How many VMs do you require for your various application tiers and components of your infrastructure?
* What CPU and memory resources does each VM need, and what are the storage requirements?

Tasks:

* Define the workloads for your application and the resources the VMs require.
* Align the resource demands for each VM with the appropriate VM size and storage type.
* Define your resource groups for the different tiers and components of your infrastructure.
* Define your VM naming convention.
* Create your VMs using the Azure PowerShell, web portal, or with Resource Manager templates.

## <a name="virtual-machines"></a>Virtual machines
One of the main resources within your Azure environment is likely VMs. This resource is where you run your applications, databases, authentication services, etc.

It is important to understand the [different VM sizes](sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to correctly size your environment from a performance and cost perspective. If your VMs do not have enough CPU cores or memory, performance of your application suffers regardless of how well it is designed and developed. Review the suggested workloads for each VM series as a starting point as you decide which size VM to use for each component in your infrastructure. You can [change the size of a VM](https://azure.microsoft.com/blog/resize-virtual-machines/) after deployment.

Storage plays a key role in VM performance. You can use Standard storage, that uses regular spinning disks, or Premium storage for high I/O workloads and peak performance, that uses SSD disks. As with the VM size, there are cost considerations to selecting the storage medium. You can read the [storage infrastructure guidelines article](infrastructure-storage-solutions-guidelines.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to understand how to design appropriate storage for optimum performance of your VMs.

## <a name="resource-groups"></a>Resource groups
Components such as VMs are logically grouped for ease of management and maintenance using [Azure Resource Groups](../../azure-resource-manager/resource-group-overview.md). By using resource groups, you can create, manage, and monitor all the resources that make up a given application. You can also implement [role-based access controls](../../active-directory/role-based-access-control-what-is.md) to grant access to others within your team to only the resources they require. Take time to plan out your resource groups and role assignments. There are different approaches to actually design and implement resource groups, so be sure to read the [resource groups guidelines article](infrastructure-resource-groups-guidelines.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) to understand how best to build out your VMs.

## <a name="templates"></a>Templates
You can build templates, defined by declarative JSON files, to create your VMs. Templates typically also build the required storage, networking, network interfaces, IP addressing, etc. along with the VMs themselves. You use templates to create consistent, reproducible environments for development and testing purposes to easily replicate production environments and vice versa. You can read more about [building and using templates](../../azure-resource-manager/resource-group-overview.md#template-deployment) to understand how you can use them for creating and deploying your VMs.

## <a name="next-steps"></a>Next steps
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

