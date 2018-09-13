---
title: Replace a scale unit node on an Azure Stack integrated system | Microsoft Docs
description: Learn how to replace a physical scale unit node on an Azure Stack integrated system.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.assetid: f9434689-ee66-493c-a237-5c81e528e5de
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/10/2018
ms.author: mabrigg
ms.openlocfilehash: 1b37b150dad4951a4ade81f226b515ce9cae9053
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856314"
---
# <a name="replace-a-scale-unit-node-on-an-azure-stack-integrated-system"></a><span data-ttu-id="7d0bb-103">Replace a scale unit node on an Azure Stack integrated system</span><span class="sxs-lookup"><span data-stu-id="7d0bb-103">Replace a scale unit node on an Azure Stack integrated system</span></span>

<span data-ttu-id="7d0bb-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="7d0bb-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="7d0bb-105">This article describes the general process to replace a physical computer (also referred to as a *scale unit node*) on an Azure Stack integrated system.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-105">This article describes the general process to replace a physical computer (also referred to as a *scale unit node*) on an Azure Stack integrated system.</span></span> <span data-ttu-id="7d0bb-106">Actual scale unit node replacement steps will vary based on your original equipment manufacturer (OEM) hardware vendor.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-106">Actual scale unit node replacement steps will vary based on your original equipment manufacturer (OEM) hardware vendor.</span></span> <span data-ttu-id="7d0bb-107">See your vendor’s field replaceable unit (FRU) documentation for detailed steps that are specific to your system.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-107">See your vendor’s field replaceable unit (FRU) documentation for detailed steps that are specific to your system.</span></span>

<span data-ttu-id="7d0bb-108">The following flow diagram shows the general FRU process to replace an entire scale unit node.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-108">The following flow diagram shows the general FRU process to replace an entire scale unit node.</span></span>

![Flow chart for replace node process](media/azure-stack-replace-node/replacenodeflow.png)

<span data-ttu-id="7d0bb-110">\*This action may not be required based on the physical condition of the hardware.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-110">\*This action may not be required based on the physical condition of the hardware.</span></span>

## <a name="review-alert-information"></a><span data-ttu-id="7d0bb-111">Review alert information</span><span class="sxs-lookup"><span data-stu-id="7d0bb-111">Review alert information</span></span>

<span data-ttu-id="7d0bb-112">If a scale unit node is down, you’ll receive the following critical alerts:</span><span class="sxs-lookup"><span data-stu-id="7d0bb-112">If a scale unit node is down, you’ll receive the following critical alerts:</span></span>

- <span data-ttu-id="7d0bb-113">Node not connected to network controller</span><span class="sxs-lookup"><span data-stu-id="7d0bb-113">Node not connected to network controller</span></span>
- <span data-ttu-id="7d0bb-114">Node inaccessible for virtual machine placement</span><span class="sxs-lookup"><span data-stu-id="7d0bb-114">Node inaccessible for virtual machine placement</span></span>
- <span data-ttu-id="7d0bb-115">Scale unit node is offline</span><span class="sxs-lookup"><span data-stu-id="7d0bb-115">Scale unit node is offline</span></span>

![List of alerts for scale unit down](media/azure-stack-replace-node/nodedownalerts.png)

<span data-ttu-id="7d0bb-117">If you open the **Scale unit node is offline** alert, the alert description contains the scale unit node that's inaccessible.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-117">If you open the **Scale unit node is offline** alert, the alert description contains the scale unit node that's inaccessible.</span></span> <span data-ttu-id="7d0bb-118">You may also receive additional alerts in the OEM-specific monitoring solution that's running on the hardware lifecycle host.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-118">You may also receive additional alerts in the OEM-specific monitoring solution that's running on the hardware lifecycle host.</span></span>

![Details of node offline alert](media/azure-stack-replace-node/nodeoffline.png)

## <a name="scale-unit-node-replacement-process"></a><span data-ttu-id="7d0bb-120">Scale unit node replacement process</span><span class="sxs-lookup"><span data-stu-id="7d0bb-120">Scale unit node replacement process</span></span>

<span data-ttu-id="7d0bb-121">The following steps are provided as a high-level overview of the scale unit node replacement process.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-121">The following steps are provided as a high-level overview of the scale unit node replacement process.</span></span> <span data-ttu-id="7d0bb-122">See your OEM hardware vendor’s FRU documentation for detailed steps that are specific to your system.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-122">See your OEM hardware vendor’s FRU documentation for detailed steps that are specific to your system.</span></span> <span data-ttu-id="7d0bb-123">Do not follow these steps without referring to your OEM-provided documentation.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-123">Do not follow these steps without referring to your OEM-provided documentation.</span></span>

1. <span data-ttu-id="7d0bb-124">Use the [Drain](azure-stack-node-actions.md#scale-unit-node-actions) action to put the scale unit node into maintenance mode.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-124">Use the [Drain](azure-stack-node-actions.md#scale-unit-node-actions) action to put the scale unit node into maintenance mode.</span></span> <span data-ttu-id="7d0bb-125">This action may not be required based on the physical condition of the hardware.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-125">This action may not be required based on the physical condition of the hardware.</span></span>

   > [!NOTE]
   > <span data-ttu-id="7d0bb-126">In any case, only one node can be drained and powered off at the same time without breaking the S2D (Storage Spaces Direct).</span><span class="sxs-lookup"><span data-stu-id="7d0bb-126">In any case, only one node can be drained and powered off at the same time without breaking the S2D (Storage Spaces Direct).</span></span>

2. <span data-ttu-id="7d0bb-127">If the node is still powered on, use the [Power off](azure-stack-node-actions.md#scale-unit-node-actions) action.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-127">If the node is still powered on, use the [Power off](azure-stack-node-actions.md#scale-unit-node-actions) action.</span></span> <span data-ttu-id="7d0bb-128">This action may not be required based on the physical condition of the hardware.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-128">This action may not be required based on the physical condition of the hardware.</span></span>
 
   > [!NOTE]
   > <span data-ttu-id="7d0bb-129">In the unlikely case that the Power off action doesn't work, use the baseboard management controller (BMC) web interface instead.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-129">In the unlikely case that the Power off action doesn't work, use the baseboard management controller (BMC) web interface instead.</span></span>

1. <span data-ttu-id="7d0bb-130">Replace the physical computer.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-130">Replace the physical computer.</span></span> <span data-ttu-id="7d0bb-131">Typically, this is done by your OEM hardware vendor.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-131">Typically, this is done by your OEM hardware vendor.</span></span>
2. <span data-ttu-id="7d0bb-132">Use the [Repair](azure-stack-node-actions.md#scale-unit-node-actions) action to add the new physical computer to the scale unit.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-132">Use the [Repair](azure-stack-node-actions.md#scale-unit-node-actions) action to add the new physical computer to the scale unit.</span></span>
3. <span data-ttu-id="7d0bb-133">Use the privileged endpoint to [check the status of virtual disk repair](azure-stack-replace-disk.md#check-the-status-of-virtual-disk-repair).</span><span class="sxs-lookup"><span data-stu-id="7d0bb-133">Use the privileged endpoint to [check the status of virtual disk repair](azure-stack-replace-disk.md#check-the-status-of-virtual-disk-repair).</span></span> <span data-ttu-id="7d0bb-134">With new data drives, a full storage repair job can take multiple hours depending on system load and consumed space.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-134">With new data drives, a full storage repair job can take multiple hours depending on system load and consumed space.</span></span>
4. <span data-ttu-id="7d0bb-135">After the repair action has finished, validate that all active alerts have been automatically closed.</span><span class="sxs-lookup"><span data-stu-id="7d0bb-135">After the repair action has finished, validate that all active alerts have been automatically closed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d0bb-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="7d0bb-136">Next steps</span></span>

- <span data-ttu-id="7d0bb-137">For information about replacing a hot-swappable physical disk, see [Replace a disk](azure-stack-replace-disk.md).</span><span class="sxs-lookup"><span data-stu-id="7d0bb-137">For information about replacing a hot-swappable physical disk, see [Replace a disk](azure-stack-replace-disk.md).</span></span> 
- <span data-ttu-id="7d0bb-138">For information about replacing a non hot-swappable hardware component, see [Replace a hardware component](azure-stack-replace-component.md).</span><span class="sxs-lookup"><span data-stu-id="7d0bb-138">For information about replacing a non hot-swappable hardware component, see [Replace a hardware component](azure-stack-replace-component.md).</span></span>
