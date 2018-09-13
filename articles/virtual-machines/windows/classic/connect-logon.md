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
# <a name="log-on-to-a-windows-virtual-machine-using-the-azure-portal"></a><span data-ttu-id="04269-103">Log on to a Windows virtual machine using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="04269-103">Log on to a Windows virtual machine using the Azure portal</span></span>
<span data-ttu-id="04269-104">In the Azure portal, you use the **Connect** button to start a Remote Desktop session and log on to a Windows VM.</span><span class="sxs-lookup"><span data-stu-id="04269-104">In the Azure portal, you use the **Connect** button to start a Remote Desktop session and log on to a Windows VM.</span></span>

<span data-ttu-id="04269-105">Do you want to connect to a Linux VM?</span><span class="sxs-lookup"><span data-stu-id="04269-105">Do you want to connect to a Linux VM?</span></span> <span data-ttu-id="04269-106">See [How to log on to a virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span><span class="sxs-lookup"><span data-stu-id="04269-106">See [How to log on to a virtual machine running Linux](../../linux/mac-create-ssh-keys.md).</span></span>

<!--
Deleting, but not 100% sure
Learn how to [perform these steps using new Azure portal](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
-->

> [!IMPORTANT]
> <span data-ttu-id="04269-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="04269-107">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="04269-108">This article covers using the Classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="04269-108">This article covers using the Classic deployment model.</span></span> <span data-ttu-id="04269-109">Microsoft recommends that most new deployments use the Resource Manager model.</span><span class="sxs-lookup"><span data-stu-id="04269-109">Microsoft recommends that most new deployments use the Resource Manager model.</span></span> <span data-ttu-id="04269-110">For information about how to log on to a VM using the Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04269-110">For information about how to log on to a VM using the Resource Manager model, see [here](../connect-logon.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="04269-111">Connect to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="04269-111">Connect to the virtual machine</span></span>
1. <span data-ttu-id="04269-112">Sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="04269-112">Sign in to the Azure portal.</span></span>
2. <span data-ttu-id="04269-113">Click on the virtual machine that you want to access.</span><span class="sxs-lookup"><span data-stu-id="04269-113">Click on the virtual machine that you want to access.</span></span> <span data-ttu-id="04269-114">The name is listed in the **All resources** pane.</span><span class="sxs-lookup"><span data-stu-id="04269-114">The name is listed in the **All resources** pane.</span></span>

    ![Virtual-machine-locations](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/connect-logon/azureportaldashboard.png)

3. <span data-ttu-id="04269-116">Click **Connect** on the command bar atop the virtual machine dashboard.</span><span class="sxs-lookup"><span data-stu-id="04269-116">Click **Connect** on the command bar atop the virtual machine dashboard.</span></span>

    ![Connect icon for the virtual machine](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/connect-logon/virtualmachine_dashboard_connect.png)

<!-- Don't know if this still applies
     I think we can zap this.
> [!TIP]
> If the **Connect** button isn't available, see the troubleshooting tips at the end of this article.
>
>
-->

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="04269-118">Log on to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="04269-118">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="04269-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="04269-119">Next steps</span></span>
* <span data-ttu-id="04269-120">If the **Connect** button is inactive or you are having other problems with the Remote Desktop connection, try resetting the configuration.</span><span class="sxs-lookup"><span data-stu-id="04269-120">If the **Connect** button is inactive or you are having other problems with the Remote Desktop connection, try resetting the configuration.</span></span> <span data-ttu-id="04269-121">click **Reset remote access** from the virtual machine dashboard.</span><span class="sxs-lookup"><span data-stu-id="04269-121">click **Reset remote access** from the virtual machine dashboard.</span></span>

    ![Reset-remote-access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/connect-logon/virtualmachine_dashboard_reset_remote_access.png)

* <span data-ttu-id="04269-123">For problems with your password, try resetting it.</span><span class="sxs-lookup"><span data-stu-id="04269-123">For problems with your password, try resetting it.</span></span> <span data-ttu-id="04269-124">Click **Reset password** along the left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span><span class="sxs-lookup"><span data-stu-id="04269-124">Click **Reset password** along the left edge of virtual machine dashboard, under **Support + Troubleshooting**.</span></span>

    ![Reset-password](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/classic/media/connect-logon/virtualmachine_dashboard_reset_password.png)

<span data-ttu-id="04269-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="04269-126">If those tips don't work or aren't what you need, see [Troubleshoot Remote Desktop connections to a Windows-based Azure Virtual Machine](../troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="04269-127">This article walks you through diagnosing and resolving common problems.</span><span class="sxs-lookup"><span data-stu-id="04269-127">This article walks you through diagnosing and resolving common problems.</span></span>




