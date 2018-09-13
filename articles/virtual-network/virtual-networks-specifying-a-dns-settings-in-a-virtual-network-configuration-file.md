---
title: Specifying DNS Settings in a virtual network configuration file | Microsoft Docs
description: How to change DNS server settings in a virtual network using a virtual network configuration file in the classic deployment model
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
tags: azure-service-management
ms.assetid: a8905927-92ac-42b5-8c33-8e42c000692c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2016
ms.author: jdial
ms.openlocfilehash: ec33268915a1888509834ce6a5b2bc782a12ce4a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552990"
---
# <a name="specifying-dns-settings-in-a-virtual-network-configuration-file"></a><span data-ttu-id="bc9e9-103">Specifying DNS settings in a virtual network configuration file</span><span class="sxs-lookup"><span data-stu-id="bc9e9-103">Specifying DNS settings in a virtual network configuration file</span></span>
<span data-ttu-id="bc9e9-104">A network configuration file has two elements that you can use to specify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span><span class="sxs-lookup"><span data-stu-id="bc9e9-104">A network configuration file has two elements that you can use to specify Domain Name System (DNS) settings: **DnsServers** and **DnsServerRef**.</span></span> <span data-ttu-id="bc9e9-105">You can add a list of DNS servers by specifying their IP addresses and reference names to the **DnsServers** element.</span><span class="sxs-lookup"><span data-stu-id="bc9e9-105">You can add a list of DNS servers by specifying their IP addresses and reference names to the **DnsServers** element.</span></span> <span data-ttu-id="bc9e9-106">You can then use a **DnsServerRef** element to specify which DNS server entries from the DnsServers element are used for different network sites within your virtual network.</span><span class="sxs-lookup"><span data-stu-id="bc9e9-106">You can then use a **DnsServerRef** element to specify which DNS server entries from the DnsServers element are used for different network sites within your virtual network.</span></span>

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

<span data-ttu-id="bc9e9-107">This article covers the classic deployment model.</span><span class="sxs-lookup"><span data-stu-id="bc9e9-107">This article covers the classic deployment model.</span></span>

<span data-ttu-id="bc9e9-108">The network configuration file may contain the following elements.</span><span class="sxs-lookup"><span data-stu-id="bc9e9-108">The network configuration file may contain the following elements.</span></span> <span data-ttu-id="bc9e9-109">The title of each element is linked to a page that provides additional information about the element value settings.</span><span class="sxs-lookup"><span data-stu-id="bc9e9-109">The title of each element is linked to a page that provides additional information about the element value settings.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="bc9e9-110">For information about how to configure the network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="bc9e9-110">For information about how to configure the network configuration file, see [Configure a Virtual Network Using a Network Configuration File](virtual-networks-using-network-configuration-file.md).</span></span> <span data-ttu-id="bc9e9-111">For information about each element contained in the network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span><span class="sxs-lookup"><span data-stu-id="bc9e9-111">For information about each element contained in the network configuration file, see [Azure Virtual Network Configuration Schema](https://msdn.microsoft.com/library/azure/jj157100.aspx).</span></span>
> 
> 

[<span data-ttu-id="bc9e9-112">Dns Element</span><span class="sxs-lookup"><span data-stu-id="bc9e9-112">Dns Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <Dns>
      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>
    </Dns>

> [!WARNING]
> <span data-ttu-id="bc9e9-113">The **name** attribute in the **DnsServer** element is used only as a reference for the **DnsServerRef** element.</span><span class="sxs-lookup"><span data-stu-id="bc9e9-113">The **name** attribute in the **DnsServer** element is used only as a reference for the **DnsServerRef** element.</span></span> <span data-ttu-id="bc9e9-114">It does not represent the host name for the DNS server.</span><span class="sxs-lookup"><span data-stu-id="bc9e9-114">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="bc9e9-115">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription</span><span class="sxs-lookup"><span data-stu-id="bc9e9-115">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription</span></span>
> 
> 

[<span data-ttu-id="bc9e9-116">Virtual Network Sites Element</span><span class="sxs-lookup"><span data-stu-id="bc9e9-116">Virtual Network Sites Element</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

    <DnsServersRef>
      <DnsServerRef name="ID1" />
      <DnsServerRef name="ID2" />
      <DnsServerRef name="ID3" />
    </DnsServersRef>

> [!NOTE]
> <span data-ttu-id="bc9e9-117">In order to specify this setting for the Virtual Network Sites element, it must be previously defined in the DNS element.</span><span class="sxs-lookup"><span data-stu-id="bc9e9-117">In order to specify this setting for the Virtual Network Sites element, it must be previously defined in the DNS element.</span></span> <span data-ttu-id="bc9e9-118">The DnsServerRef *name* in the Virtual Network Sites element must refer to a name value specified in the DNS element for DnsServer *name*.</span><span class="sxs-lookup"><span data-stu-id="bc9e9-118">The DnsServerRef *name* in the Virtual Network Sites element must refer to a name value specified in the DNS element for DnsServer *name*.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="bc9e9-119">Next steps</span><span class="sxs-lookup"><span data-stu-id="bc9e9-119">Next steps</span></span>
* <span data-ttu-id="bc9e9-120">Understand the [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span><span class="sxs-lookup"><span data-stu-id="bc9e9-120">Understand the [Azure Virtual Network Configuration Schema](http://go.microsoft.com/fwlink/?LinkId=248093).</span></span>
* <span data-ttu-id="bc9e9-121">Understand the [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span><span class="sxs-lookup"><span data-stu-id="bc9e9-121">Understand the [Azure Service Configuration Schema](https://msdn.microsoft.com/library/windowsazure/ee758710).</span></span>
* <span data-ttu-id="bc9e9-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span><span class="sxs-lookup"><span data-stu-id="bc9e9-122">[Configure a virtual network using Network configuration files](virtual-networks-using-network-configuration-file.md).</span></span>

