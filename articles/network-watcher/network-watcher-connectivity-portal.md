---
title: Troubleshoot connections with Azure Network Watcher - Azure portal | Microsoft Docs
description: Learn how to use the connection troubleshoot capability of Azure Network Watcher using the Azure portal.
services: network-watcher
documentationcenter: na
author: jimdial
manager: jeconnoc
editor: ''
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/03/2017
ms.author: jdial
ms.openlocfilehash: cf7b71a49b63a95ed535210125120c6b76d9de8f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867876"
---
# <a name="troubleshoot-connections-with-azure-network-watcher-using-the-azure-portal"></a><span data-ttu-id="1f071-103">Troubleshoot connections with Azure Network Watcher using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="1f071-103">Troubleshoot connections with Azure Network Watcher using the Azure portal</span></span>

> [!div class="op_single_selector"]
> - [Portal](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST API](network-watcher-connectivity-rest.md)

<span data-ttu-id="1f071-108">Learn how to use connection troubleshoot to verify whether a direct TCP connection from a virtual machine to a given endpoint can be established.</span><span class="sxs-lookup"><span data-stu-id="1f071-108">Learn how to use connection troubleshoot to verify whether a direct TCP connection from a virtual machine to a given endpoint can be established.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="1f071-109">Before you begin</span><span class="sxs-lookup"><span data-stu-id="1f071-109">Before you begin</span></span>

<span data-ttu-id="1f071-110">This article assumes you have the following resources:</span><span class="sxs-lookup"><span data-stu-id="1f071-110">This article assumes you have the following resources:</span></span>

* <span data-ttu-id="1f071-111">An instance of Network Watcher in the region you want to troubleshoot a connection.</span><span class="sxs-lookup"><span data-stu-id="1f071-111">An instance of Network Watcher in the region you want to troubleshoot a connection.</span></span>
* <span data-ttu-id="1f071-112">Virtual machines to troubleshoot connections with.</span><span class="sxs-lookup"><span data-stu-id="1f071-112">Virtual machines to troubleshoot connections with.</span></span>

> [!IMPORTANT]
> Connection troubleshoot requires that the VM you troubleshoot from has the `AzureNetworkWatcherExtension` VM extension installed. For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json). The extension is not required on the destination endpoint.

## <a name="check-connectivity-to-a-virtual-machine"></a><span data-ttu-id="1f071-116">Check connectivity to a virtual machine</span><span class="sxs-lookup"><span data-stu-id="1f071-116">Check connectivity to a virtual machine</span></span>

<span data-ttu-id="1f071-117">This example checks connectivity to a destination virtual machine over port 80.</span><span class="sxs-lookup"><span data-stu-id="1f071-117">This example checks connectivity to a destination virtual machine over port 80.</span></span>

<span data-ttu-id="1f071-118">Navigate to your Network Watcher and click **Connection troubleshoot**.</span><span class="sxs-lookup"><span data-stu-id="1f071-118">Navigate to your Network Watcher and click **Connection troubleshoot**.</span></span> <span data-ttu-id="1f071-119">Select the virtual machine to check connectivity from.</span><span class="sxs-lookup"><span data-stu-id="1f071-119">Select the virtual machine to check connectivity from.</span></span> <span data-ttu-id="1f071-120">In the **Destination** section choose **Select a virtual machine** and choose the correct virtual machine and port to test.</span><span class="sxs-lookup"><span data-stu-id="1f071-120">In the **Destination** section choose **Select a virtual machine** and choose the correct virtual machine and port to test.</span></span>

<span data-ttu-id="1f071-121">Once you click **Check**, connectivity between the virtual machines on the port specified is checked.</span><span class="sxs-lookup"><span data-stu-id="1f071-121">Once you click **Check**, connectivity between the virtual machines on the port specified is checked.</span></span> <span data-ttu-id="1f071-122">In the example, the destination VM is unreachable, a listing of hops are shown.</span><span class="sxs-lookup"><span data-stu-id="1f071-122">In the example, the destination VM is unreachable, a listing of hops are shown.</span></span>

![Check connectivity results for a virtual machine][1]

## <a name="check-remote-endpoint-connectivity"></a><span data-ttu-id="1f071-124">Check remote endpoint connectivity</span><span class="sxs-lookup"><span data-stu-id="1f071-124">Check remote endpoint connectivity</span></span>

<span data-ttu-id="1f071-125">To check the connectivity and latency to a remote endpoint, choose the **Specify manually** radio button in the **Destination** section, input the url and the port and click **Check**.</span><span class="sxs-lookup"><span data-stu-id="1f071-125">To check the connectivity and latency to a remote endpoint, choose the **Specify manually** radio button in the **Destination** section, input the url and the port and click **Check**.</span></span>  <span data-ttu-id="1f071-126">This is used for remote endpoints like websites and storage endpoints.</span><span class="sxs-lookup"><span data-stu-id="1f071-126">This is used for remote endpoints like websites and storage endpoints.</span></span>

![Check connectivity results for a web site][2]

## <a name="next-steps"></a><span data-ttu-id="1f071-128">Next steps</span><span class="sxs-lookup"><span data-stu-id="1f071-128">Next steps</span></span>

<span data-ttu-id="1f071-129">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span><span class="sxs-lookup"><span data-stu-id="1f071-129">Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)</span></span>

<span data-ttu-id="1f071-130">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](diagnose-vm-network-traffic-filtering-problem.md)</span><span class="sxs-lookup"><span data-stu-id="1f071-130">Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](diagnose-vm-network-traffic-filtering-problem.md)</span></span>

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png