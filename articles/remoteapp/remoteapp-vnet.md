---
title: Validate the Azure VNET to use with Azure RemoteApp | Microsoft Docs
description: Learn how to make sure your Azure VNET is ready to use with Azure RemoteApp
services: remoteapp
documentationcenter: ''
author: msmbaldwin
manager: mbaldwin
ms.assetid: b573ba02-4587-4be5-9821-27bd891a73b2
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: mbaldwin
ms.openlocfilehash: 05c8a0ff04293947cec391b6467cc4adddb6a7b0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553393"
---
# <a name="validate-the-azure-vnet-to-use-with-azure-remoteapp"></a><span data-ttu-id="883ce-103">Validate the Azure VNET to use with Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="883ce-103">Validate the Azure VNET to use with Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="883ce-104">Azure RemoteApp is being discontinued on August 31, 2017.</span><span class="sxs-lookup"><span data-stu-id="883ce-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="883ce-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span><span class="sxs-lookup"><span data-stu-id="883ce-105">Read the [announcement](https://go.microsoft.com/fwlink/?linkid=821148) for details.</span></span>
> 
> 

<span data-ttu-id="883ce-106">Before you use an Azure VNET with Azure RemoteApp, you might want to validate the VNET.</span><span class="sxs-lookup"><span data-stu-id="883ce-106">Before you use an Azure VNET with Azure RemoteApp, you might want to validate the VNET.</span></span> <span data-ttu-id="883ce-107">This helps prevent issues with connectivity.</span><span class="sxs-lookup"><span data-stu-id="883ce-107">This helps prevent issues with connectivity.</span></span>

<span data-ttu-id="883ce-108">To validate your Azure VNET, do the following:</span><span class="sxs-lookup"><span data-stu-id="883ce-108">To validate your Azure VNET, do the following:</span></span>

1. <span data-ttu-id="883ce-109">Create an Azure virtual machine inside the subnet of the Azure VNET you want to use with Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="883ce-109">Create an Azure virtual machine inside the subnet of the Azure VNET you want to use with Azure RemoteApp.</span></span>
2. <span data-ttu-id="883ce-110">Connect to that VM by using the **Connect** option in the management portal.</span><span class="sxs-lookup"><span data-stu-id="883ce-110">Connect to that VM by using the **Connect** option in the management portal.</span></span>
3. <span data-ttu-id="883ce-111">Join the virtual machine to the same domain that you want to use with Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="883ce-111">Join the virtual machine to the same domain that you want to use with Azure RemoteApp.</span></span> <span data-ttu-id="883ce-112">If you are creating a hybrid collection that connects to your on-premises network, join the virtual machine to your local domain.</span><span class="sxs-lookup"><span data-stu-id="883ce-112">If you are creating a hybrid collection that connects to your on-premises network, join the virtual machine to your local domain.</span></span>

<span data-ttu-id="883ce-113">If this is successful, the Azure VNET is ready to use with RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="883ce-113">If this is successful, the Azure VNET is ready to use with RemoteApp.</span></span>

<span data-ttu-id="883ce-114">For more information about the end-to-end hybrid collection workflow, see the following articles:</span><span class="sxs-lookup"><span data-stu-id="883ce-114">For more information about the end-to-end hybrid collection workflow, see the following articles:</span></span>

* [<span data-ttu-id="883ce-115">How to plan your virtual network for Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="883ce-115">How to plan your virtual network for Azure RemoteApp</span></span>](remoteapp-planvnet.md)
* [<span data-ttu-id="883ce-116">Create a hybrid collection</span><span class="sxs-lookup"><span data-stu-id="883ce-116">Create a hybrid collection</span></span>](remoteapp-create-hybrid-deployment.md)
* [<span data-ttu-id="883ce-117">Deploy Azure RemoteApp collection to your Azure Virtual Network (with support for ExpressRoute)</span><span class="sxs-lookup"><span data-stu-id="883ce-117">Deploy Azure RemoteApp collection to your Azure Virtual Network (with support for ExpressRoute)</span></span>](http://blogs.msdn.com/b/rds/archive/2015/04/23/deploy-azure-remoteapp-collection-to-your-azure-virtual-network-with-support-for-expressroute.aspx)

