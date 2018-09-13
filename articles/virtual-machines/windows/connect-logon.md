---
title: Connect to a Windows Server VM | Microsoft Docs
description: Learn how to connect and log on to a Windows VM using the Azure portal and the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 04/11/2018
ms.author: cynthn
ms.openlocfilehash: f47b18b4d0b8065d23803870304d0e5a8991d992
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44800805"
---
# <a name="how-to-connect-and-log-on-to-an-azure-virtual-machine-running-windows"></a><span data-ttu-id="ad6e7-103">How to connect and log on to an Azure virtual machine running Windows</span><span class="sxs-lookup"><span data-stu-id="ad6e7-103">How to connect and log on to an Azure virtual machine running Windows</span></span>
<span data-ttu-id="ad6e7-104">You'll use the **Connect** button in the Azure portal to start a Remote Desktop (RDP) session from a Windows desktop.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-104">You'll use the **Connect** button in the Azure portal to start a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="ad6e7-105">First you connect to the virtual machine, then you log on.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-105">First you connect to the virtual machine, then you log on.</span></span>

<span data-ttu-id="ad6e7-106">If you are trying to connect to a Windows VM from a Mac, you need to install an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="ad6e7-106">If you are trying to connect to a Windows VM from a Mac, you need to install an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="ad6e7-107">Connect to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="ad6e7-107">Connect to the virtual machine</span></span>
1. <span data-ttu-id="ad6e7-108">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="ad6e7-108">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="ad6e7-109">In the left menu, click **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-109">In the left menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="ad6e7-110">Select the virtual machine from the list.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-110">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="ad6e7-111">On the top of the page for the virtual machine, click the</span><span class="sxs-lookup"><span data-stu-id="ad6e7-111">On the top of the page for the virtual machine, click the</span></span> ![Image of the connect button.](./media/connect-logon/connect.png) <span data-ttu-id="ad6e7-113">button.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-113">button.</span></span>
2. <span data-ttu-id="ad6e7-114">In the **Connect to virtual machine** page, select the appropriate options and click **Download RDP file**.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-114">In the **Connect to virtual machine** page, select the appropriate options and click **Download RDP file**.</span></span>
2. <span data-ttu-id="ad6e7-115">Open the downloaded RDP file and click **Connect** when prompted.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-115">Open the downloaded RDP file and click **Connect** when prompted.</span></span> 
2. <span data-ttu-id="ad6e7-116">You get a warning that the `.rdp` file is from an unknown publisher.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-116">You get a warning that the `.rdp` file is from an unknown publisher.</span></span> <span data-ttu-id="ad6e7-117">This is normal.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-117">This is normal.</span></span> <span data-ttu-id="ad6e7-118">In the Remote Desktop window, click **Connect** to continue.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-118">In the Remote Desktop window, click **Connect** to continue.</span></span>
   
    ![Screenshot of a warning about an unknown publisher.](./media/connect-logon/rdp-warn.png)
3. <span data-ttu-id="ad6e7-120">In the **Windows Security** window, select **More choices** and then **Use a different account**.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-120">In the **Windows Security** window, select **More choices** and then **Use a different account**.</span></span> <span data-ttu-id="ad6e7-121">Type the credentials for an account on the virtual machine and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-121">Type the credentials for an account on the virtual machine and then click **OK**.</span></span>
   
     <span data-ttu-id="ad6e7-122">**Local account** - this is usually the local account user name and password that you specified when you created the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-122">**Local account** - this is usually the local account user name and password that you specified when you created the virtual machine.</span></span> <span data-ttu-id="ad6e7-123">In this case, the domain is the name of the virtual machine and it is entered as *vmname*&#92;*username*.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-123">In this case, the domain is the name of the virtual machine and it is entered as *vmname*&#92;*username*.</span></span>  
   
    <span data-ttu-id="ad6e7-124">**Domain joined VM** - if the VM belongs to a domain, enter the user name in the format *Domain*&#92;*Username*.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-124">**Domain joined VM** - if the VM belongs to a domain, enter the user name in the format *Domain*&#92;*Username*.</span></span> <span data-ttu-id="ad6e7-125">The account also needs to either be in the Administrators group or have been granted remote access privileges to the VM.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-125">The account also needs to either be in the Administrators group or have been granted remote access privileges to the VM.</span></span>
   
    <span data-ttu-id="ad6e7-126">**Domain controller** - if the VM is a domain controller, type the user name and password of a domain administrator account for that domain.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-126">**Domain controller** - if the VM is a domain controller, type the user name and password of a domain administrator account for that domain.</span></span>
4. <span data-ttu-id="ad6e7-127">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-127">Click **Yes** to verify the identity of the virtual machine and finish logging on.</span></span>
   
   ![Screenshot showing a message abut verifying the identity of the VM.](./media/connect-logon/cert-warning.png)


   > [!TIP]
   > <span data-ttu-id="ad6e7-129">If the **Connect** button in the portal is greyed out and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-129">If the **Connect** button in the portal is greyed out and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="ad6e7-130">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ad6e7-130">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 


## <a name="next-steps"></a><span data-ttu-id="ad6e7-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="ad6e7-131">Next steps</span></span>
<span data-ttu-id="ad6e7-132">If you run into trouble when you try to connect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ad6e7-132">If you run into trouble when you try to connect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="ad6e7-133">This article walks you through diagnosing and resolving common problems.</span><span class="sxs-lookup"><span data-stu-id="ad6e7-133">This article walks you through diagnosing and resolving common problems.</span></span>

