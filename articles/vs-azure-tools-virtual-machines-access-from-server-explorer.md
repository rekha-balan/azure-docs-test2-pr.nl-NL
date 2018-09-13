---
title: Accessing Azure Virtual Machines from Server Explorer | Microsoft Docs
description: Get an overview of how to view create and manage Azure virtual machines (VMs) in Server Explorer in Visual Studio.
services: visual-studio-online
author: ghogen
manager: douge
assetId: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.custom: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 8/31/2017
ms.author: ghogen
ms.openlocfilehash: 81a0e2923ddbb6960066f01d6365e8c9278defac
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44810237"
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a><span data-ttu-id="b1f2c-103">Accessing Azure Virtual Machines from Server Explorer</span><span class="sxs-lookup"><span data-stu-id="b1f2c-103">Accessing Azure Virtual Machines from Server Explorer</span></span>

<span data-ttu-id="b1f2c-104">If you have virtual machines hosted by Azure, you can access them in Server Explorer.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-104">If you have virtual machines hosted by Azure, you can access them in Server Explorer.</span></span> <span data-ttu-id="b1f2c-105">You must first sign in to your Azure subscription to view your mobile services.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-105">You must first sign in to your Azure subscription to view your mobile services.</span></span> <span data-ttu-id="b1f2c-106">To sign in, open the shortcut menu for the Azure node in Server Explorer, and choose **Connect to Microsoft Azure**.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-106">To sign in, open the shortcut menu for the Azure node in Server Explorer, and choose **Connect to Microsoft Azure**.</span></span>

1. <span data-ttu-id="b1f2c-107">In Cloud Explorer, choose a virtual machine, and then choose the F4 key to show its properties window.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-107">In Cloud Explorer, choose a virtual machine, and then choose the F4 key to show its properties window.</span></span>

    <span data-ttu-id="b1f2c-108">The following table shows what properties are available, but they are all read-only.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-108">The following table shows what properties are available, but they are all read-only.</span></span> <span data-ttu-id="b1f2c-109">To change them, use the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b1f2c-109">To change them, use the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span>

   | <span data-ttu-id="b1f2c-110">Property</span><span class="sxs-lookup"><span data-stu-id="b1f2c-110">Property</span></span> | <span data-ttu-id="b1f2c-111">Description</span><span class="sxs-lookup"><span data-stu-id="b1f2c-111">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="b1f2c-112">DNS Name</span><span class="sxs-lookup"><span data-stu-id="b1f2c-112">DNS Name</span></span> |<span data-ttu-id="b1f2c-113">The URL with the Internet address of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-113">The URL with the Internet address of the virtual machine.</span></span> |
   | <span data-ttu-id="b1f2c-114">Environment</span><span class="sxs-lookup"><span data-stu-id="b1f2c-114">Environment</span></span> |<span data-ttu-id="b1f2c-115">For a virtual machine, the value of this property is always Production.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-115">For a virtual machine, the value of this property is always Production.</span></span> |
   | <span data-ttu-id="b1f2c-116">Name</span><span class="sxs-lookup"><span data-stu-id="b1f2c-116">Name</span></span> |<span data-ttu-id="b1f2c-117">The name of the virtual machine.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-117">The name of the virtual machine.</span></span> |
   | <span data-ttu-id="b1f2c-118">Size</span><span class="sxs-lookup"><span data-stu-id="b1f2c-118">Size</span></span> |<span data-ttu-id="b1f2c-119">The size of the virtual machine, which reflects the amount of memory and disk space that’s available.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-119">The size of the virtual machine, which reflects the amount of memory and disk space that’s available.</span></span> <span data-ttu-id="b1f2c-120">For more information, see [Virtual Machine Sizes](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs).</span><span class="sxs-lookup"><span data-stu-id="b1f2c-120">For more information, see [Virtual Machine Sizes](https://docs.microsoft.com/azure/cloud-services/cloud-services-sizes-specs).</span></span> |
   | <span data-ttu-id="b1f2c-121">Status</span><span class="sxs-lookup"><span data-stu-id="b1f2c-121">Status</span></span> |<span data-ttu-id="b1f2c-122">Values include Starting, Started, Stopping, Stopped, and Retrieving Status.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-122">Values include Starting, Started, Stopping, Stopped, and Retrieving Status.</span></span> <span data-ttu-id="b1f2c-123">If Retrieving Status appears, the current status is unknown.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-123">If Retrieving Status appears, the current status is unknown.</span></span> <span data-ttu-id="b1f2c-124">The values for this property differ from the values that are used on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b1f2c-124">The values for this property differ from the values that are used on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> |
   | <span data-ttu-id="b1f2c-125">SubscriptionID</span><span class="sxs-lookup"><span data-stu-id="b1f2c-125">SubscriptionID</span></span> |<span data-ttu-id="b1f2c-126">The subscription ID for your Azure account.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-126">The subscription ID for your Azure account.</span></span> <span data-ttu-id="b1f2c-127">You can show this information on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) by viewing the properties for a subscription.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-127">You can show this information on the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) by viewing the properties for a subscription.</span></span> |
2. <span data-ttu-id="b1f2c-128">Choose an endpoint node, and then view the **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-128">Choose an endpoint node, and then view the **Properties** window.</span></span>
3. <span data-ttu-id="b1f2c-129">The following table describes the available properties of endpoints, but they are read-only.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-129">The following table describes the available properties of endpoints, but they are read-only.</span></span> <span data-ttu-id="b1f2c-130">To add or edit the endpoints for a virtual machine, use the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span><span class="sxs-lookup"><span data-stu-id="b1f2c-130">To add or edit the endpoints for a virtual machine, use the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040).</span></span> 

   | <span data-ttu-id="b1f2c-131">Property</span><span class="sxs-lookup"><span data-stu-id="b1f2c-131">Property</span></span> | <span data-ttu-id="b1f2c-132">Description</span><span class="sxs-lookup"><span data-stu-id="b1f2c-132">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="b1f2c-133">Name</span><span class="sxs-lookup"><span data-stu-id="b1f2c-133">Name</span></span> |<span data-ttu-id="b1f2c-134">An identifier for the endpoint.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-134">An identifier for the endpoint.</span></span> |
   | <span data-ttu-id="b1f2c-135">Private Port</span><span class="sxs-lookup"><span data-stu-id="b1f2c-135">Private Port</span></span> |<span data-ttu-id="b1f2c-136">The port for network access internal to your application.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-136">The port for network access internal to your application.</span></span> |
   | <span data-ttu-id="b1f2c-137">Protocol</span><span class="sxs-lookup"><span data-stu-id="b1f2c-137">Protocol</span></span> |<span data-ttu-id="b1f2c-138">The protocol that the transport layer for this endpoint uses, either TCP or UDP.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-138">The protocol that the transport layer for this endpoint uses, either TCP or UDP.</span></span> |
   | <span data-ttu-id="b1f2c-139">Public Port</span><span class="sxs-lookup"><span data-stu-id="b1f2c-139">Public Port</span></span> |<span data-ttu-id="b1f2c-140">The port that’s used for public access to your application.</span><span class="sxs-lookup"><span data-stu-id="b1f2c-140">The port that’s used for public access to your application.</span></span> |
