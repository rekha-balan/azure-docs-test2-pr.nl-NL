---
title: Install MongoDB on a Windows VM in Azure | Microsoft Docs
description: Learn how to install MongoDB on an Azure VM created with the classic deployment model running Windows Server.
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: 7cf2c0a9e5e7785397a7229e3b44e9dbcc26f429
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662070"
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>Install MongoDB on a Windows VM in Azure
> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources: [Resource Manager and classic](../../../resource-manager-deployment-model.md).  This article covers using the classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. To install and configure MongoDB using the Resource Manager deployment model, see [this article](../../virtual-machines-windows-install-mongodb.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

[MongoDB][MongoDB] is a popular open-source, high-performance NoSQL database. This article guides you through creating a Windows Server virtual machine (VM) using the [Azure portal][AzurePortal]. You then create and attach a data disk to the VM before installing and configuring MongoDB. If you have an existing VM in Azure that you would like to use, you can jump straight to [installing and configuring MongoDB](#install-and-run-mongodb-on-the-virtual-machine).

## <a name="create-a-virtual-machine-running-windows-server"></a>Create a virtual machine running Windows Server
Follow these instructions to create a virtual machine.

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> You can add an endpoint for MongoDB while creating the virtual machine, and configure it as follows: name it as **Mongo**, use **TCP** as the protocol, and set both the public and private ports to **27017**.
>
>

## <a name="attach-a-data-disk"></a>Attach a data disk
To provide storage for the virtual machine, attach a data disk and then initialize it so that Windows can use it. If you already have a data disk, you can attach that existing disk, or you can attach an empty disk.

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

For instructions on initializing the disk, see "How to: Initialize a new data disk in Windows Server" in [How to attach a data disk to a Windows virtual machine](attach-disk.md).

## <a name="install-and-run-mongodb-on-the-virtual-machine"></a>Install and run MongoDB on the virtual machine
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>Summary
In this tutorial, you learned how to create a virtual machine running Windows Server, remotely connect to it, and attach a data disk.  You also learned how to install and configure MongoDB on the Windows-based virtual machine. You can now access MongoDB on the Windows-based virtual machine, by following the advanced topics in the [MongoDB documentation][MongoDocs].

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

<!-- Classic portal. Removed 03/07/2017 -->
<!-- [AzurePortal]: http://manage.windowsazure.com  -->
