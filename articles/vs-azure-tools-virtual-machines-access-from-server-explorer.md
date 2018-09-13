---
title: Accessing Azure Virtual Machines from Server Explorer | Microsoft Docs
description: Get an overview of how to view create and manage Azure virtual machines (VMs) in Server Explorer in Visual Studio.
services: visual-studio-online
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: tarcher
ms.openlocfilehash: 3a35bba4b5b694f9dd555d15fce934ff29d0ab70
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550425"
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a><span data-ttu-id="cda2e-103">Accessing Azure Virtual Machines from Server Explorer</span><span class="sxs-lookup"><span data-stu-id="cda2e-103">Accessing Azure Virtual Machines from Server Explorer</span></span>
<span data-ttu-id="cda2e-104">By using Server Explorer in Visual Studio, you can display information about your virtual machines hosted by Azure.</span><span class="sxs-lookup"><span data-stu-id="cda2e-104">By using Server Explorer in Visual Studio, you can display information about your virtual machines hosted by Azure.</span></span>

## <a name="accessing-virtual-machines-in-server-explorer"></a><span data-ttu-id="cda2e-105">Accessing virtual machines in Server Explorer</span><span class="sxs-lookup"><span data-stu-id="cda2e-105">Accessing virtual machines in Server Explorer</span></span>
<span data-ttu-id="cda2e-106">If you have virtual machines hosted by Azure, you can access them in Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="cda2e-106">If you have virtual machines hosted by Azure, you can access them in Server Explorer.</span></span> <span data-ttu-id="cda2e-107">You must first sign in to your Azure subscription to view your mobile services.</span><span class="sxs-lookup"><span data-stu-id="cda2e-107">You must first sign in to your Azure subscription to view your mobile services.</span></span> <span data-ttu-id="cda2e-108">To sign in, open the shortcut menu for the Azure node in Server Explorer, and choose **Connect to Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="cda2e-108">To sign in, open the shortcut menu for the Azure node in Server Explorer, and choose **Connect to Microsoft Azure**.</span></span>

### <a name="to-get-information-about-your-virtual-machines"></a><span data-ttu-id="cda2e-109">To get information about your virtual machines</span><span class="sxs-lookup"><span data-stu-id="cda2e-109">To get information about your virtual machines</span></span>
1. <span data-ttu-id="cda2e-110">In Server Explorer, choose a virtual machine, and then choose the F4 key to show its properties window.</span><span class="sxs-lookup"><span data-stu-id="cda2e-110">In Server Explorer, choose a virtual machine, and then choose the F4 key to show its properties window.</span></span>
   
    <span data-ttu-id="cda2e-111">The following table shows what properties are available, but they are all read-only.</span><span class="sxs-lookup"><span data-stu-id="cda2e-111">The following table shows what properties are available, but they are all read-only.</span></span> <span data-ttu-id="cda2e-112">To change them, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="cda2e-112">To change them, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
   
   | <span data-ttu-id="cda2e-113">Property</span><span class="sxs-lookup"><span data-stu-id="cda2e-113">Property</span></span> | <span data-ttu-id="cda2e-114">Description</span><span class="sxs-lookup"><span data-stu-id="cda2e-114">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="cda2e-115">DNS Name</span><span class="sxs-lookup"><span data-stu-id="cda2e-115">DNS Name</span></span> |<span data-ttu-id="cda2e-116">The URL with the Internet address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cda2e-116">The URL with the Internet address of the virtual machine.</span></span> |
   | <span data-ttu-id="cda2e-117">Environment</span><span class="sxs-lookup"><span data-stu-id="cda2e-117">Environment</span></span> |<span data-ttu-id="cda2e-118">For a virtual machine, the value of this property is always Production.</span><span class="sxs-lookup"><span data-stu-id="cda2e-118">For a virtual machine, the value of this property is always Production.</span></span> |
   | <span data-ttu-id="cda2e-119">Name</span><span class="sxs-lookup"><span data-stu-id="cda2e-119">Name</span></span> |<span data-ttu-id="cda2e-120">The name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="cda2e-120">The name of the virtual machine.</span></span> |
   | <span data-ttu-id="cda2e-121">Size</span><span class="sxs-lookup"><span data-stu-id="cda2e-121">Size</span></span> |<span data-ttu-id="cda2e-122">The size of the virtual machine, which reflects the amount of memory and disk space that’s available.</span><span class="sxs-lookup"><span data-stu-id="cda2e-122">The size of the virtual machine, which reflects the amount of memory and disk space that’s available.</span></span> <span data-ttu-id="cda2e-123">For more information, see How To: Configure Virtual Machine Sizes.</span><span class="sxs-lookup"><span data-stu-id="cda2e-123">For more information, see How To: Configure Virtual Machine Sizes.</span></span> |
   | <span data-ttu-id="cda2e-124">Status</span><span class="sxs-lookup"><span data-stu-id="cda2e-124">Status</span></span> |<span data-ttu-id="cda2e-125">Values include Starting, Started, Stopping, Stopped, and Retrieving Status.</span><span class="sxs-lookup"><span data-stu-id="cda2e-125">Values include Starting, Started, Stopping, Stopped, and Retrieving Status.</span></span> <span data-ttu-id="cda2e-126">If Retrieving Status appears, the current status is unknown.</span><span class="sxs-lookup"><span data-stu-id="cda2e-126">If Retrieving Status appears, the current status is unknown.</span></span> <span data-ttu-id="cda2e-127">The values for this property differ from the values that are used on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="cda2e-127">The values for this property differ from the values that are used on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> |
   | <span data-ttu-id="cda2e-128">SubscriptionID</span><span class="sxs-lookup"><span data-stu-id="cda2e-128">SubscriptionID</span></span> |<span data-ttu-id="cda2e-129">The subscription ID for your Azure account.</span><span class="sxs-lookup"><span data-stu-id="cda2e-129">The subscription ID for your Azure account.</span></span> <span data-ttu-id="cda2e-130">You can show this information on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) by viewing the properties for a subscription.</span><span class="sxs-lookup"><span data-stu-id="cda2e-130">You can show this information on the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) by viewing the properties for a subscription.</span></span> |
2. <span data-ttu-id="cda2e-131">Choose an endpoint node, and then view the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="cda2e-131">Choose an endpoint node, and then view the **Properties** window.</span></span>
3. <span data-ttu-id="cda2e-132">The following table describes the available properties of endpoints, but they are read-only.</span><span class="sxs-lookup"><span data-stu-id="cda2e-132">The following table describes the available properties of endpoints, but they are read-only.</span></span> <span data-ttu-id="cda2e-133">To add or edit the endpoints for a virtual machine, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span><span class="sxs-lookup"><span data-stu-id="cda2e-133">To add or edit the endpoints for a virtual machine, use the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> 
   
   | <span data-ttu-id="cda2e-134">Property</span><span class="sxs-lookup"><span data-stu-id="cda2e-134">Property</span></span> | <span data-ttu-id="cda2e-135">Description</span><span class="sxs-lookup"><span data-stu-id="cda2e-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="cda2e-136">Name</span><span class="sxs-lookup"><span data-stu-id="cda2e-136">Name</span></span> |<span data-ttu-id="cda2e-137">An identifier for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="cda2e-137">An identifier for the endpoint.</span></span> |
   | <span data-ttu-id="cda2e-138">Private Port</span><span class="sxs-lookup"><span data-stu-id="cda2e-138">Private Port</span></span> |<span data-ttu-id="cda2e-139">The port for network access internal to your application.</span><span class="sxs-lookup"><span data-stu-id="cda2e-139">The port for network access internal to your application.</span></span> |
   | <span data-ttu-id="cda2e-140">Protocol</span><span class="sxs-lookup"><span data-stu-id="cda2e-140">Protocol</span></span> |<span data-ttu-id="cda2e-141">The protocol that the transport layer for this endpoint uses, either TCP or UDP.</span><span class="sxs-lookup"><span data-stu-id="cda2e-141">The protocol that the transport layer for this endpoint uses, either TCP or UDP.</span></span> |
   | <span data-ttu-id="cda2e-142">Public Port</span><span class="sxs-lookup"><span data-stu-id="cda2e-142">Public Port</span></span> |<span data-ttu-id="cda2e-143">The port that’s used for public access to your application.</span><span class="sxs-lookup"><span data-stu-id="cda2e-143">The port that’s used for public access to your application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="cda2e-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="cda2e-144">Next steps</span></span>
<span data-ttu-id="cda2e-145">To learn more about using Azure roles in Visual Studio, see [Using Remote Desktop with Azure Roles](vs-azure-tools-remote-desktop-roles.md).</span><span class="sxs-lookup"><span data-stu-id="cda2e-145">To learn more about using Azure roles in Visual Studio, see [Using Remote Desktop with Azure Roles](vs-azure-tools-remote-desktop-roles.md).</span></span>

