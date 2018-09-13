---
title: Sizing information for a VNET in Azure RemoteApp | Microsoft Docs
description: Learn about the IP address requirements for Azure RemoteApp running with a VNET
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: b6e1c4ba-0236-42b2-bced-69353bf211be
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 9375981db64ec4a1ae523e958423b5f5787cec33
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540830"
---
# <a name="sizing-information-for-a-vnet-in-azure-remoteapp"></a><span data-ttu-id="88d51-103">Sizing information for a VNET in Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="88d51-103">Sizing information for a VNET in Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="88d51-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="88d51-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="88d51-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="88d51-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="88d51-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within the subnet.</span><span class="sxs-lookup"><span data-stu-id="88d51-106">When you use Azure RemoteApp with a virtual network (VNET), RemoteApp uses IP addresses within the subnet.</span></span> <span data-ttu-id="88d51-107">Based on the scale of your RemoteApp service, you need to ensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span><span class="sxs-lookup"><span data-stu-id="88d51-107">Based on the scale of your RemoteApp service, you need to ensure that your subnet has enough IP addresses available for RemoteApp virtual machines.</span></span> <span data-ttu-id="88d51-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span><span class="sxs-lookup"><span data-stu-id="88d51-108">While this sizing guidance isn’t perfect given how RemoteApp dynamically spins up and spins down virtual machines within a collection, it will help you estimate your subnet range.</span></span> <span data-ttu-id="88d51-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase the subnet size without removing RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="88d51-109">This is especially important as, once a RemoteApp service is placed in a VNET, you cannot increase the subnet size without removing RemoteApp.</span></span>

<span data-ttu-id="88d51-110">For each RemoteApp collection that you want to run at maximum capacity, you should have 100 IP addresses available.</span><span class="sxs-lookup"><span data-stu-id="88d51-110">For each RemoteApp collection that you want to run at maximum capacity, you should have 100 IP addresses available.</span></span> <span data-ttu-id="88d51-111">For example, if you have one RemoteApp collection in the Standard plan and you want to have the maximum 500 users, you should have 100 IP addresses for that collection.</span><span class="sxs-lookup"><span data-stu-id="88d51-111">For example, if you have one RemoteApp collection in the Standard plan and you want to have the maximum 500 users, you should have 100 IP addresses for that collection.</span></span> <span data-ttu-id="88d51-112">Similarly, you need 100 IP addresses for a RemoteApp collection in the Basic plan that has 800 users.</span><span class="sxs-lookup"><span data-stu-id="88d51-112">Similarly, you need 100 IP addresses for a RemoteApp collection in the Basic plan that has 800 users.</span></span> <span data-ttu-id="88d51-113">If you plan to have fewer users (less than the maximum), you can reduce the IP addresses needed per collection.</span><span class="sxs-lookup"><span data-stu-id="88d51-113">If you plan to have fewer users (less than the maximum), you can reduce the IP addresses needed per collection.</span></span> <span data-ttu-id="88d51-114">The minimum subnet size requirement is 30 IP addresses (/27).</span><span class="sxs-lookup"><span data-stu-id="88d51-114">The minimum subnet size requirement is 30 IP addresses (/27).</span></span>

<span data-ttu-id="88d51-115">Check out the following information to make sure your VNET is configured and working propertly:</span><span class="sxs-lookup"><span data-stu-id="88d51-115">Check out the following information to make sure your VNET is configured and working propertly:</span></span>

* [<span data-ttu-id="88d51-116">Migrate from a personal VNET to an Azure VNET</span><span class="sxs-lookup"><span data-stu-id="88d51-116">Migrate from a personal VNET to an Azure VNET</span></span>](remoteapp-migratevnet.md)
* [<span data-ttu-id="88d51-117">Validate the Azure VNET to use with Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="88d51-117">Validate the Azure VNET to use with Azure RemoteApp</span></span>](remoteapp-vnet.md)

