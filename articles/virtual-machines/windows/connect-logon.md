---
title: Connect to a Windows Server VM | Microsoft Docs
description: Learn how to connect and log on to a Windows VM using the Azure portal and the Resource Manager deployment model.
services: virtual-machines-windows
documentationcenter: ''
author: cynthn
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ef62b02e-bf35-468d-b4c3-71b63fe7f409
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/01/2017
ms.author: cynthn
ms.openlocfilehash: 28b22ac67ec5d3c132ae9216aa8e18ba8866b3d2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551012"
---
# <a name="how-to-connect-and-log-on-to-an-azure-virtual-machine-running-windows"></a><span data-ttu-id="076e2-103">How to connect and log on to an Azure virtual machine running Windows</span><span class="sxs-lookup"><span data-stu-id="076e2-103">How to connect and log on to an Azure virtual machine running Windows</span></span>
<span data-ttu-id="076e2-104">You'll use the **Connect** button in the Azure portal to start a Remote Desktop (RDP) session from a Windows desktop.</span><span class="sxs-lookup"><span data-stu-id="076e2-104">You'll use the **Connect** button in the Azure portal to start a Remote Desktop (RDP) session from a Windows desktop.</span></span> <span data-ttu-id="076e2-105">First you connect to the virtual machine, then you log on.</span><span class="sxs-lookup"><span data-stu-id="076e2-105">First you connect to the virtual machine, then you log on.</span></span>

<span data-ttu-id="076e2-106">If you are trying to connect to a Windows VM from a Mac, you need to install an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span><span class="sxs-lookup"><span data-stu-id="076e2-106">If you are trying to connect to a Windows VM from a Mac, you need to install an RDP client for Mac like [Microsoft Remote Desktop](https://itunes.apple.com/app/microsoft-remote-desktop/id715768417).</span></span>

## <a name="connect-to-the-virtual-machine"></a><span data-ttu-id="076e2-107">Connect to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="076e2-107">Connect to the virtual machine</span></span>
1. <span data-ttu-id="076e2-108">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="076e2-108">If you haven't already done so, sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="076e2-109">On the Hub menu, click **Virtual Machines**.</span><span class="sxs-lookup"><span data-stu-id="076e2-109">On the Hub menu, click **Virtual Machines**.</span></span>
3. <span data-ttu-id="076e2-110">Select the virtual machine from the list.</span><span class="sxs-lookup"><span data-stu-id="076e2-110">Select the virtual machine from the list.</span></span>
4. <span data-ttu-id="076e2-111">On the blade for the virtual machine, click **Connect**.</span><span class="sxs-lookup"><span data-stu-id="076e2-111">On the blade for the virtual machine, click **Connect**.</span></span>
   
    ![Screenshot of the Azure portal showing how to connect to your VM.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/connect-logon/connect.png)
   
   > [!TIP]
   > <span data-ttu-id="076e2-113">If the **Connect** button in the portal is greyed out and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span><span class="sxs-lookup"><span data-stu-id="076e2-113">If the **Connect** button in the portal is greyed out and you are not connected to Azure via an [Express Route](../../expressroute/expressroute-introduction.md) or [Site-to-Site VPN](../../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md) connection, you need to create and assign your VM a public IP address before you can use RDP.</span></span> <span data-ttu-id="076e2-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span><span class="sxs-lookup"><span data-stu-id="076e2-114">You can read more about [public IP addresses in Azure](../../virtual-network/virtual-network-ip-addresses-overview-arm.md).</span></span>
   > 
   > 

## <a name="log-on-to-the-virtual-machine"></a><span data-ttu-id="076e2-115">Log on to the virtual machine</span><span class="sxs-lookup"><span data-stu-id="076e2-115">Log on to the virtual machine</span></span>
[!INCLUDE [virtual-machines-log-on-win-server](../../../includes/virtual-machines-log-on-win-server.md)]

## <a name="next-steps"></a><span data-ttu-id="076e2-116">Next steps</span><span class="sxs-lookup"><span data-stu-id="076e2-116">Next steps</span></span>
<span data-ttu-id="076e2-117">If you run into trouble when you try to connect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="076e2-117">If you run into trouble when you try to connect, see [Troubleshoot Remote Desktop connections](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="076e2-118">This article walks you through diagnosing and resolving common problems.</span><span class="sxs-lookup"><span data-stu-id="076e2-118">This article walks you through diagnosing and resolving common problems.</span></span>


