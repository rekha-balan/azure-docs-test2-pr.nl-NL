---
title: Specifying DNS Settings in a service configuration file | Microsoft Docs
description: specifying custom DNS settings using service configuration file for virtual network
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 467a4b99-8691-40b3-b640-e25e49675c71
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/24/2016
ms.author: jdial
ms.openlocfilehash: 0fba2ea06827aff29a7a092933edb8120d668b29
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564032"
---
# <a name="specifying-dns-settings-in-a-service-configuration-file"></a><span data-ttu-id="df958-103">Specifying DNS Settings in a Service Configuration File</span><span class="sxs-lookup"><span data-stu-id="df958-103">Specifying DNS Settings in a Service Configuration File</span></span>
## <a name="dns-elements"></a><span data-ttu-id="df958-104">DNS elements</span><span class="sxs-lookup"><span data-stu-id="df958-104">DNS elements</span></span>
<span data-ttu-id="df958-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for the Domain Name System (DNS) servers that the service will use.</span><span class="sxs-lookup"><span data-stu-id="df958-105">A service configuration file may contain a DnsServers element with a list of IPv4 addresses for the Domain Name System (DNS) servers that the service will use.</span></span> <span data-ttu-id="df958-106">Settings in the service configuration file take precedence over settings in the network configuration file.</span><span class="sxs-lookup"><span data-stu-id="df958-106">Settings in the service configuration file take precedence over settings in the network configuration file.</span></span> <span data-ttu-id="df958-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span><span class="sxs-lookup"><span data-stu-id="df958-107">For more information, see [Azure Service Configuration Schema (.cscfg File)](https://msdn.microsoft.com/library/azure/ee758710.aspx).</span></span>

<span data-ttu-id="df958-108">**NetworkConfiguration element**</span><span class="sxs-lookup"><span data-stu-id="df958-108">**NetworkConfiguration element**</span></span>

      <DnsServers>
        <DnsServer name="ID1" IPAddress="IPAddress1" />
        <DnsServer name="ID2" IPAddress="IPAddress2" />
        <DnsServer name="ID3" IPAddress="IPAddress3" />
      </DnsServers>

> [!WARNING]
> <span data-ttu-id="df958-109">The **name** attribute in the **DnsServer** element is used only as a reference name.</span><span class="sxs-lookup"><span data-stu-id="df958-109">The **name** attribute in the **DnsServer** element is used only as a reference name.</span></span> <span data-ttu-id="df958-110">It does not represent the host name for the DNS server.</span><span class="sxs-lookup"><span data-stu-id="df958-110">It does not represent the host name for the DNS server.</span></span> <span data-ttu-id="df958-111">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="df958-111">Each **DnsServer** attribute value must be unique across the entire Microsoft Azure subscription.</span></span>
> 
> 

## <a name="see-also"></a><span data-ttu-id="df958-112">See Also</span><span class="sxs-lookup"><span data-stu-id="df958-112">See Also</span></span>
[<span data-ttu-id="df958-113">Azure Service Configuration Schema (.cscfg)</span><span class="sxs-lookup"><span data-stu-id="df958-113">Azure Service Configuration Schema (.cscfg)</span></span>](https://msdn.microsoft.com/library/windowsazure/ee758710)

[<span data-ttu-id="df958-114">Azure Virtual Network Configuration Schema</span><span class="sxs-lookup"><span data-stu-id="df958-114">Azure Virtual Network Configuration Schema</span></span>](http://go.microsoft.com/fwlink/?LinkId=248093)

[<span data-ttu-id="df958-115">Configure a Virtual Network Using Network Configuration Files</span><span class="sxs-lookup"><span data-stu-id="df958-115">Configure a Virtual Network Using Network Configuration Files</span></span>](http://go.microsoft.com/fwlink/?LinkId=248094)

[<span data-ttu-id="df958-116">About Virtual Network settings in the Management Portal</span><span class="sxs-lookup"><span data-stu-id="df958-116">About Virtual Network settings in the Management Portal</span></span>](http://go.microsoft.com/fwlink/?LinkId=248092)

