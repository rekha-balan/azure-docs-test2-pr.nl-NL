---
title: List of Ports and URLs to whitelist for Azure RemoteApp Deployed in customer virtual network | Microsoft Docs
description: Learn which ports and URLs you'll need to configure for communication through Azure RemoteApp.
services: remoteapp
documentationcenter: ''
author: mghosh1616
manager: mbaldwin
ms.assetid: 5a001ff7-14c9-47fa-9b39-78fd5a5f0250
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/16/2016
ms.author: mbaldwin
ms.openlocfilehash: 9390af174262e0dd2bb5beb30ae08b3063c1a5e6
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564471"
---
# <a name="list-of-ports-and-urls-to-permit-access-for-azure-remoteapp-deployed-in-customer-virtual-network"></a><span data-ttu-id="61bfc-103">List of Ports and URLs to permit access for Azure RemoteApp Deployed in customer Virtual Network</span><span class="sxs-lookup"><span data-stu-id="61bfc-103">List of Ports and URLs to permit access for Azure RemoteApp Deployed in customer Virtual Network</span></span>
> [!IMPORTANT]
> <span data-ttu-id="61bfc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="61bfc-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="61bfc-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="61bfc-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="61bfc-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review the following port information.</span><span class="sxs-lookup"><span data-stu-id="61bfc-106">If you are deploying an Azure RemoteApp cloud or hybrid collection in a virtual network (VNET), review the following port information.</span></span> <span data-ttu-id="61bfc-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span><span class="sxs-lookup"><span data-stu-id="61bfc-107">For more information on virtual networks, read [Virtual Network Overview](../virtual-network/virtual-networks-overview.md).</span></span> <span data-ttu-id="61bfc-108">If you have created a network security group (NSG) restricting traffic to the virtual network resources in your collection, make sure the following ports are accessible and allowed through the security policies on the virtual network.</span><span class="sxs-lookup"><span data-stu-id="61bfc-108">If you have created a network security group (NSG) restricting traffic to the virtual network resources in your collection, make sure the following ports are accessible and allowed through the security policies on the virtual network.</span></span> <span data-ttu-id="61bfc-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span><span class="sxs-lookup"><span data-stu-id="61bfc-109">For more information on network security groups, read [What is a Network Security Group? (NSG)](../virtual-network/virtual-networks-nsg.md).</span></span>

## <a name="azure-remoteapp-subnet-needs-access-to-these-endpoints-and-urls"></a><span data-ttu-id="61bfc-110">Azure RemoteApp subnet needs access to these endpoints and URLs:</span><span class="sxs-lookup"><span data-stu-id="61bfc-110">Azure RemoteApp subnet needs access to these endpoints and URLs:</span></span>
* <span data-ttu-id="61bfc-111">\*.servicebus.windows.net</span><span class="sxs-lookup"><span data-stu-id="61bfc-111">\*.servicebus.windows.net</span></span>
* <span data-ttu-id="61bfc-112">\*.servicebus.net</span><span class="sxs-lookup"><span data-stu-id="61bfc-112">\*.servicebus.net</span></span>
* <span data-ttu-id="61bfc-113">https://\*.remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="61bfc-113">https://\*.remoteapp.windowsazure.com</span></span>  
* https://www.remoteapp.windowsazure.com 
* <span data-ttu-id="61bfc-114">https://\*remoteapp.windowsazure.com</span><span class="sxs-lookup"><span data-stu-id="61bfc-114">https://\*remoteapp.windowsazure.com</span></span>  
* <span data-ttu-id="61bfc-115">https://\*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="61bfc-115">https://\*.core.windows.net</span></span>  
* <span data-ttu-id="61bfc-116">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span><span class="sxs-lookup"><span data-stu-id="61bfc-116">Outbound: TCP: TCP: 443, 9351, 9352, 10101-10175</span></span> 
* <span data-ttu-id="61bfc-117">Optional – UDP: 10201-10275</span><span class="sxs-lookup"><span data-stu-id="61bfc-117">Optional – UDP: 10201-10275</span></span>  

## <a name="azure-remoteapp-clients-need-access-to-these-endpoints-and-urls"></a><span data-ttu-id="61bfc-118">Azure RemoteApp clients need access to these endpoints and URLs:</span><span class="sxs-lookup"><span data-stu-id="61bfc-118">Azure RemoteApp clients need access to these endpoints and URLs:</span></span>
<span data-ttu-id="61bfc-119">By clients I mean the desktops, devices etc. that people use to connect to the apps deployed in the Azure RemoteApp collection.</span><span class="sxs-lookup"><span data-stu-id="61bfc-119">By clients I mean the desktops, devices etc. that people use to connect to the apps deployed in the Azure RemoteApp collection.</span></span>

* https://telemetry.remoteapp.windowsazure.com  
* <span data-ttu-id="61bfc-120">https://\*.remoteapp.windowsazure.com (the optional UDP ports are for this address)</span><span class="sxs-lookup"><span data-stu-id="61bfc-120">https://\*.remoteapp.windowsazure.com (the optional UDP ports are for this address)</span></span> 
* https://login.windows.net  
* https://login.microsoftonline.com  
* https://www.remoteapp.windowsazure.com 
* <span data-ttu-id="61bfc-121">https://\*.core.windows.net</span><span class="sxs-lookup"><span data-stu-id="61bfc-121">https://\*.core.windows.net</span></span>  
* <span data-ttu-id="61bfc-122">Outbound: TCP: 443</span><span class="sxs-lookup"><span data-stu-id="61bfc-122">Outbound: TCP: 443</span></span>  
* <span data-ttu-id="61bfc-123">Optional - UDP: 3391</span><span class="sxs-lookup"><span data-stu-id="61bfc-123">Optional - UDP: 3391</span></span> 

