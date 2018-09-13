---
title: Replace a hardware component on an Azure Stack scale unit node | Microsoft Docs
description: Learn how to replace a hardware component on an Azure Stack integrated system.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2018
ms.author: mabrigg
ms.openlocfilehash: df9470813f3f9c3bff58882879c06e7b7b0fc15b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864982"
---
# <a name="replace-a-hardware-component-on-an-azure-stack-scale-unit-node"></a><span data-ttu-id="2f505-103">Replace a hardware component on an Azure Stack scale unit node</span><span class="sxs-lookup"><span data-stu-id="2f505-103">Replace a hardware component on an Azure Stack scale unit node</span></span>

<span data-ttu-id="2f505-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="2f505-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="2f505-105">This article describes the general process to replace hardware components that are non hot-swappable.</span><span class="sxs-lookup"><span data-stu-id="2f505-105">This article describes the general process to replace hardware components that are non hot-swappable.</span></span> <span data-ttu-id="2f505-106">Actual replacement steps vary based on your original equipment manufacturer (OEM) hardware vendor.</span><span class="sxs-lookup"><span data-stu-id="2f505-106">Actual replacement steps vary based on your original equipment manufacturer (OEM) hardware vendor.</span></span> <span data-ttu-id="2f505-107">See your vendor’s field replaceable unit (FRU) documentation for detailed steps that are specific to your Azure Stack integrated system.</span><span class="sxs-lookup"><span data-stu-id="2f505-107">See your vendor’s field replaceable unit (FRU) documentation for detailed steps that are specific to your Azure Stack integrated system.</span></span>

<span data-ttu-id="2f505-108">Non hot-swappable components include the following:</span><span class="sxs-lookup"><span data-stu-id="2f505-108">Non hot-swappable components include the following:</span></span>

- <span data-ttu-id="2f505-109">CPU\*</span><span class="sxs-lookup"><span data-stu-id="2f505-109">CPU\*</span></span>
- <span data-ttu-id="2f505-110">Memory\*</span><span class="sxs-lookup"><span data-stu-id="2f505-110">Memory\*</span></span>
- <span data-ttu-id="2f505-111">Motherboard/baseboard management controller (BMC)/video card</span><span class="sxs-lookup"><span data-stu-id="2f505-111">Motherboard/baseboard management controller (BMC)/video card</span></span>
- <span data-ttu-id="2f505-112">Disk controller/host bus adapter (HBA)/backplane</span><span class="sxs-lookup"><span data-stu-id="2f505-112">Disk controller/host bus adapter (HBA)/backplane</span></span>
- <span data-ttu-id="2f505-113">Network adapter (NIC)</span><span class="sxs-lookup"><span data-stu-id="2f505-113">Network adapter (NIC)</span></span>
- <span data-ttu-id="2f505-114">Operating system disk\*</span><span class="sxs-lookup"><span data-stu-id="2f505-114">Operating system disk\*</span></span>
- <span data-ttu-id="2f505-115">Data drives (drives that don't support hot swap, for example PCI-e add-in cards)\*</span><span class="sxs-lookup"><span data-stu-id="2f505-115">Data drives (drives that don't support hot swap, for example PCI-e add-in cards)\*</span></span>

<span data-ttu-id="2f505-116">\*These components may support hot swap, but can vary based on vendor implementation.</span><span class="sxs-lookup"><span data-stu-id="2f505-116">\*These components may support hot swap, but can vary based on vendor implementation.</span></span> <span data-ttu-id="2f505-117">See your OEM vendor’s FRU documentation for detailed steps.</span><span class="sxs-lookup"><span data-stu-id="2f505-117">See your OEM vendor’s FRU documentation for detailed steps.</span></span>

<span data-ttu-id="2f505-118">The following flow diagram shows the general FRU process to replace a non hot-swappable hardware component.</span><span class="sxs-lookup"><span data-stu-id="2f505-118">The following flow diagram shows the general FRU process to replace a non hot-swappable hardware component.</span></span>

![Flow diagram showing component replacement flow](media/azure-stack-replace-component/replacecomponentflow.PNG)

<span data-ttu-id="2f505-120">\*This action may not be required based on the physical condition of the hardware.</span><span class="sxs-lookup"><span data-stu-id="2f505-120">\*This action may not be required based on the physical condition of the hardware.</span></span>

<span data-ttu-id="2f505-121">\*\*Whether your OEM hardware vendor performs the component replacement and updates the firmware could vary based on your support contract.</span><span class="sxs-lookup"><span data-stu-id="2f505-121">\*\*Whether your OEM hardware vendor performs the component replacement and updates the firmware could vary based on your support contract.</span></span>

## <a name="review-alert-information"></a><span data-ttu-id="2f505-122">Review alert information</span><span class="sxs-lookup"><span data-stu-id="2f505-122">Review alert information</span></span>

<span data-ttu-id="2f505-123">The Azure Stack health and monitoring system track the health of network adapters and data drives controlled by Storage Spaces Direct.</span><span class="sxs-lookup"><span data-stu-id="2f505-123">The Azure Stack health and monitoring system track the health of network adapters and data drives controlled by Storage Spaces Direct.</span></span> <span data-ttu-id="2f505-124">It does not track other hardware components.</span><span class="sxs-lookup"><span data-stu-id="2f505-124">It does not track other hardware components.</span></span> <span data-ttu-id="2f505-125">For all other hardware components, alerts are raised in the vendor-specific hardware monitoring solution that runs on the hardware lifecycle host.</span><span class="sxs-lookup"><span data-stu-id="2f505-125">For all other hardware components, alerts are raised in the vendor-specific hardware monitoring solution that runs on the hardware lifecycle host.</span></span>  

## <a name="component-replacement-process"></a><span data-ttu-id="2f505-126">Component replacement process</span><span class="sxs-lookup"><span data-stu-id="2f505-126">Component replacement process</span></span>

<span data-ttu-id="2f505-127">The following steps provide a high-level overview of the component replacement process.</span><span class="sxs-lookup"><span data-stu-id="2f505-127">The following steps provide a high-level overview of the component replacement process.</span></span> <span data-ttu-id="2f505-128">Do not follow these steps without referring to your OEM-provided FRU documentation.</span><span class="sxs-lookup"><span data-stu-id="2f505-128">Do not follow these steps without referring to your OEM-provided FRU documentation.</span></span>

1. <span data-ttu-id="2f505-129">Use the [Drain](azure-stack-node-actions.md#scale-unit-node-actions) action to put the scale unit node into maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="2f505-129">Use the [Drain](azure-stack-node-actions.md#scale-unit-node-actions) action to put the scale unit node into maintenance mode.</span></span> <span data-ttu-id="2f505-130">This action may not be required based on the physical condition of the hardware.</span><span class="sxs-lookup"><span data-stu-id="2f505-130">This action may not be required based on the physical condition of the hardware.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2f505-131">In any case, only one node can be drained and powered off at the same time without breaking the S2D (Storage Spaces Direct).</span><span class="sxs-lookup"><span data-stu-id="2f505-131">In any case, only one node can be drained and powered off at the same time without breaking the S2D (Storage Spaces Direct).</span></span>

2. <span data-ttu-id="2f505-132">After the scale unit node is in maintenance mode, use the [Power off](azure-stack-node-actions.md#scale-unit-node-actions) action.</span><span class="sxs-lookup"><span data-stu-id="2f505-132">After the scale unit node is in maintenance mode, use the [Power off](azure-stack-node-actions.md#scale-unit-node-actions) action.</span></span> <span data-ttu-id="2f505-133">This action may not be required based on the physical condition of the hardware.</span><span class="sxs-lookup"><span data-stu-id="2f505-133">This action may not be required based on the physical condition of the hardware.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2f505-134">In the unlikely case that the power off action doesn't work, use the baseboard management controller (BMC) web interface instead.</span><span class="sxs-lookup"><span data-stu-id="2f505-134">In the unlikely case that the power off action doesn't work, use the baseboard management controller (BMC) web interface instead.</span></span>

3. <span data-ttu-id="2f505-135">Replace the damaged hardware component.</span><span class="sxs-lookup"><span data-stu-id="2f505-135">Replace the damaged hardware component.</span></span> <span data-ttu-id="2f505-136">Whether your OEM hardware vendor performs the component replacement could vary based on your support contract.</span><span class="sxs-lookup"><span data-stu-id="2f505-136">Whether your OEM hardware vendor performs the component replacement could vary based on your support contract.</span></span>  
4. <span data-ttu-id="2f505-137">Update the firmware.</span><span class="sxs-lookup"><span data-stu-id="2f505-137">Update the firmware.</span></span> <span data-ttu-id="2f505-138">Follow your vendor-specific firmware update process using the hardware lifecycle host to make sure the replaced hardware component has the approved firmware level applied.</span><span class="sxs-lookup"><span data-stu-id="2f505-138">Follow your vendor-specific firmware update process using the hardware lifecycle host to make sure the replaced hardware component has the approved firmware level applied.</span></span> <span data-ttu-id="2f505-139">Whether your OEM hardware vendor performs this step could vary based on your support contract.</span><span class="sxs-lookup"><span data-stu-id="2f505-139">Whether your OEM hardware vendor performs this step could vary based on your support contract.</span></span>  
5. <span data-ttu-id="2f505-140">Use the [Repair](azure-stack-node-actions.md#scale-unit-node-actions) action to bring the scale unit node back into the scale unit.</span><span class="sxs-lookup"><span data-stu-id="2f505-140">Use the [Repair](azure-stack-node-actions.md#scale-unit-node-actions) action to bring the scale unit node back into the scale unit.</span></span>
6. <span data-ttu-id="2f505-141">Use the privileged endpoint to [check the status of virtual disk repair](azure-stack-replace-disk.md#check-the-status-of-virtual-disk-repair).</span><span class="sxs-lookup"><span data-stu-id="2f505-141">Use the privileged endpoint to [check the status of virtual disk repair](azure-stack-replace-disk.md#check-the-status-of-virtual-disk-repair).</span></span> <span data-ttu-id="2f505-142">With new data drives, a full storage repair job can take multiple hours depending on system load and consumed space.</span><span class="sxs-lookup"><span data-stu-id="2f505-142">With new data drives, a full storage repair job can take multiple hours depending on system load and consumed space.</span></span>
7. <span data-ttu-id="2f505-143">After the repair action has finished, validate that all active alerts have been automatically closed.</span><span class="sxs-lookup"><span data-stu-id="2f505-143">After the repair action has finished, validate that all active alerts have been automatically closed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f505-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f505-144">Next steps</span></span>

- <span data-ttu-id="2f505-145">For information about replacing a hot-swappable physical disk, see [Replace a disk](azure-stack-replace-disk.md).</span><span class="sxs-lookup"><span data-stu-id="2f505-145">For information about replacing a hot-swappable physical disk, see [Replace a disk](azure-stack-replace-disk.md).</span></span>
- <span data-ttu-id="2f505-146">For information about replacing a physical node, see [Replace a scale unit node](azure-stack-replace-node.md).</span><span class="sxs-lookup"><span data-stu-id="2f505-146">For information about replacing a physical node, see [Replace a scale unit node](azure-stack-replace-node.md).</span></span>
