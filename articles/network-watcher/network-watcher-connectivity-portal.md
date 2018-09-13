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
# <a name="troubleshoot-connections-with-azure-network-watcher-using-the-azure-portal"></a>Troubleshoot connections with Azure Network Watcher using the Azure portal

> [!div class="op_single_selector"]
> - [Portal](network-watcher-connectivity-portal.md)
> - [PowerShell](network-watcher-connectivity-powershell.md)
> - [CLI 2.0](network-watcher-connectivity-cli.md)
> - [Azure REST API](network-watcher-connectivity-rest.md)

Learn how to use connection troubleshoot to verify whether a direct TCP connection from a virtual machine to a given endpoint can be established.

## <a name="before-you-begin"></a>Before you begin

This article assumes you have the following resources:

* An instance of Network Watcher in the region you want to troubleshoot a connection.
* Virtual machines to troubleshoot connections with.

> [!IMPORTANT]
> Connection troubleshoot requires that the VM you troubleshoot from has the `AzureNetworkWatcherExtension` VM extension installed. For installing the extension on a Windows VM visit [Azure Network Watcher Agent virtual machine extension for Windows](../virtual-machines/windows/extensions-nwa.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json) and for Linux VM visit [Azure Network Watcher Agent virtual machine extension for Linux](../virtual-machines/linux/extensions-nwa.md?toc=%2fazure%2fnetwork-watcher%2ftoc.json). The extension is not required on the destination endpoint.

## <a name="check-connectivity-to-a-virtual-machine"></a>Check connectivity to a virtual machine

This example checks connectivity to a destination virtual machine over port 80.

Navigate to your Network Watcher and click **Connection troubleshoot**. Select the virtual machine to check connectivity from. In the **Destination** section choose **Select a virtual machine** and choose the correct virtual machine and port to test.

Once you click **Check**, connectivity between the virtual machines on the port specified is checked. In the example, the destination VM is unreachable, a listing of hops are shown.

![Check connectivity results for a virtual machine][1]

## <a name="check-remote-endpoint-connectivity"></a>Check remote endpoint connectivity

To check the connectivity and latency to a remote endpoint, choose the **Specify manually** radio button in the **Destination** section, input the url and the port and click **Check**.  This is used for remote endpoints like websites and storage endpoints.

![Check connectivity results for a web site][2]

## <a name="next-steps"></a>Next steps

Learn how to automate packet captures with Virtual machine alerts by viewing [Create an alert triggered packet capture](network-watcher-alert-triggered-packet-capture.md)

Find if certain traffic is allowed in or out of your VM by visiting [Check IP flow verify](diagnose-vm-network-traffic-filtering-problem.md)

[1]: ./media/network-watcher-connectivity-portal/figure1.png
[2]: ./media/network-watcher-connectivity-portal/figure2.png