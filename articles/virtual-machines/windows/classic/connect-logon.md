---
title: Log on to a classic Azure VM | Microsoft Docs
description: Use the Azure classic portal to log on to a Windows virtual machine created with the classic deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 3c1239ed-07dc-48b8-8b3d-dc8c5f0ab20e
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: cynthn
ms.openlocfilehash: 3806cabc409926050b1458c0cd434624a2604918
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554169"
---
# <a name="log-on-to-a-windows-virtual-machine-using-the-azure-portal"></a>Log on to a Windows virtual machine using the Azure portal
In the Azure portal, you use the **Connect** button to start a Remote Desktop session and log on to a Windows VM.

Do you want to connect to a Linux VM? See [How to log on to a virtual machine running Linux](../../linux/mac-create-ssh-keys.md).

<!--
Deleting, but not 100% sure
Learn how to [perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md). This article covers using the Classic deployment model. Microsoft recommends that most new deployments use the Resource Manager model. For information about how to log on to a VM using the Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

## <a name="connect-to-the-virtual-machine"></a>Connect to the virtual machine
1. Sign in to the Azure portal.
2. Click on the virtual machine that you want to access. The name is listed in the **All resources** pane.

    ![Virtual-machine-locations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/connect-logon/azureportaldashboard.png)

3. Click **Connect** on the command bar atop the virtual machine dashboard.

    ![Connect icon for the virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If the **Connect** button isn't available, see the troubleshooting tips at the end of this article.
>
>
-->

## <a name="log-on-to-the-virtual-machine"></a>Log on to the virtual machine
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a>Next steps
* If the **Connect** button is inactive or you are having other problems with the Remote Desktop connection, try resetting the configuration. click **Reset remote access** from the virtual machine dashboard.

    ![Reset-remote-access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* For problems with your password, try resetting it. Click **Reset password** along the left edge of virtual machine dashboard, under **Support + Troubleshooting**.

    ![Reset-password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/connect-logon/virtualmachine_dashboard_reset_password.png)

If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). This article walks you through diagnosing and resolving common problems.




