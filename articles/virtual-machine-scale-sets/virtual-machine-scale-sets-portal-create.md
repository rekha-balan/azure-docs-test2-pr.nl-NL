---
title: Create a Virtual Machine Scale Set using the Azure portal | Microsoft Docs
description: Deploy scale sets using Azure portal.
keywords: virtual machine scale sets
services: virtual-machine-scale-sets
documentationcenter: ''
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 09/15/2016
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8597378ca4a25beabc3d2d95a9150e9ef6e99e9c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671045"
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-the-azure-portal"></a><span data-ttu-id="4be57-104">How to create a Virtual Machine Scale Set with the Azure portal</span><span class="sxs-lookup"><span data-stu-id="4be57-104">How to create a Virtual Machine Scale Set with the Azure portal</span></span>
<span data-ttu-id="4be57-105">This tutorial shows you how easy it is to create a Virtual Machine Scale Set in just a few minutes, by using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="4be57-105">This tutorial shows you how easy it is to create a Virtual Machine Scale Set in just a few minutes, by using the Azure portal.</span></span> <span data-ttu-id="4be57-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="4be57-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="choose-the-vm-image-from-the-marketplace"></a><span data-ttu-id="4be57-107">Choose the VM image from the marketplace</span><span class="sxs-lookup"><span data-stu-id="4be57-107">Choose the VM image from the marketplace</span></span>
<span data-ttu-id="4be57-108">From the portal, you can easily deploy a scale set with CentOS, CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server, or Windows Server images.</span><span class="sxs-lookup"><span data-stu-id="4be57-108">From the portal, you can easily deploy a scale set with CentOS, CoreOS, Debian, Open Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server, Ubuntu Server, or Windows Server images.</span></span>

<span data-ttu-id="4be57-109">First, navigate to the [Azure portal](https://portal.azure.com) in a web browser.</span><span class="sxs-lookup"><span data-stu-id="4be57-109">First, navigate to the [Azure portal](https://portal.azure.com) in a web browser.</span></span> <span data-ttu-id="4be57-110">Click `New`, search for `scale set`, and then select the `Virtual machine scale set` entry:</span><span class="sxs-lookup"><span data-stu-id="4be57-110">Click `New`, search for `scale set`, and then select the `Virtual machine scale set` entry:</span></span>

![ScaleSetPortalOverview](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-the-scale-set"></a><span data-ttu-id="4be57-112">Create the scale set</span><span class="sxs-lookup"><span data-stu-id="4be57-112">Create the scale set</span></span>
<span data-ttu-id="4be57-113">Now you can use the default settings and quickly create the scale set.</span><span class="sxs-lookup"><span data-stu-id="4be57-113">Now you can use the default settings and quickly create the scale set.</span></span>

* <span data-ttu-id="4be57-114">On the `Basics` blade, enter a name for the scale set.</span><span class="sxs-lookup"><span data-stu-id="4be57-114">On the `Basics` blade, enter a name for the scale set.</span></span> <span data-ttu-id="4be57-115">This name becomes the base of the FQDN of the load balancer in front of the scale set, so make sure the name is unique across all Azure.</span><span class="sxs-lookup"><span data-stu-id="4be57-115">This name becomes the base of the FQDN of the load balancer in front of the scale set, so make sure the name is unique across all Azure.</span></span>
* <span data-ttu-id="4be57-116">Select your desired OS type, enter your desired username, and select which authentication type you prefer.</span><span class="sxs-lookup"><span data-stu-id="4be57-116">Select your desired OS type, enter your desired username, and select which authentication type you prefer.</span></span> <span data-ttu-id="4be57-117">If you choose a password, it must be at least 12 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span><span class="sxs-lookup"><span data-stu-id="4be57-117">If you choose a password, it must be at least 12 characters long and meet three out of the four following complexity requirements: one lower case character, one upper case character, one number, and one special character.</span></span> <span data-ttu-id="4be57-118">See more about [username and password requirements](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span><span class="sxs-lookup"><span data-stu-id="4be57-118">See more about [username and password requirements](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm).</span></span> <span data-ttu-id="4be57-119">If you choose `SSH public key`, be sure to only paste in your public key, NOT your private key:</span><span class="sxs-lookup"><span data-stu-id="4be57-119">If you choose `SSH public key`, be sure to only paste in your public key, NOT your private key:</span></span>

![ScaleSetPortalBasics](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* <span data-ttu-id="4be57-121">Choose whether you would like to limit the scale set to a single placement group or whether it should span multiple placement groups.</span><span class="sxs-lookup"><span data-stu-id="4be57-121">Choose whether you would like to limit the scale set to a single placement group or whether it should span multiple placement groups.</span></span> <span data-ttu-id="4be57-122">Allowing the scale set to span placement groups allows for scale sets over 100 VMs in capacity (up to 1,000) with certain limitations.</span><span class="sxs-lookup"><span data-stu-id="4be57-122">Allowing the scale set to span placement groups allows for scale sets over 100 VMs in capacity (up to 1,000) with certain limitations.</span></span> <span data-ttu-id="4be57-123">For more information, see [this documentation](./virtual-machine-scale-sets-placement-groups.md).</span><span class="sxs-lookup"><span data-stu-id="4be57-123">For more information, see [this documentation](./virtual-machine-scale-sets-placement-groups.md).</span></span>
* <span data-ttu-id="4be57-124">Enter your desired resource group name and location, and then click `OK`.</span><span class="sxs-lookup"><span data-stu-id="4be57-124">Enter your desired resource group name and location, and then click `OK`.</span></span>
* <span data-ttu-id="4be57-125">On the `Virtual machine scale set service settings` blade: enter your desired domain name label (the base of the FQDN for the load balancer in front of the scale set).</span><span class="sxs-lookup"><span data-stu-id="4be57-125">On the `Virtual machine scale set service settings` blade: enter your desired domain name label (the base of the FQDN for the load balancer in front of the scale set).</span></span> <span data-ttu-id="4be57-126">This label must be unique across all Azure.</span><span class="sxs-lookup"><span data-stu-id="4be57-126">This label must be unique across all Azure.</span></span>
* <span data-ttu-id="4be57-127">Choose your desired operating system disk image, instance count, and machine size.</span><span class="sxs-lookup"><span data-stu-id="4be57-127">Choose your desired operating system disk image, instance count, and machine size.</span></span>
* <span data-ttu-id="4be57-128">Choose your desired disk type: managed or unmanaged.</span><span class="sxs-lookup"><span data-stu-id="4be57-128">Choose your desired disk type: managed or unmanaged.</span></span> <span data-ttu-id="4be57-129">For more information, see [this documentation](./virtual-machine-scale-sets-managed-disks.md).</span><span class="sxs-lookup"><span data-stu-id="4be57-129">For more information, see [this documentation](./virtual-machine-scale-sets-managed-disks.md).</span></span> <span data-ttu-id="4be57-130">If you chose to have the scale set span multiple placement groups, this option will not be available because managed disk is required for scale sets to span placement groups.</span><span class="sxs-lookup"><span data-stu-id="4be57-130">If you chose to have the scale set span multiple placement groups, this option will not be available because managed disk is required for scale sets to span placement groups.</span></span>
* <span data-ttu-id="4be57-131">Enable or disable autoscale and configure if enabled:</span><span class="sxs-lookup"><span data-stu-id="4be57-131">Enable or disable autoscale and configure if enabled:</span></span>

![ScaleSetPortalService](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* <span data-ttu-id="4be57-133">On the `Summary` blade, when validation is done, click `OK` to start the scale set deployment.</span><span class="sxs-lookup"><span data-stu-id="4be57-133">On the `Summary` blade, when validation is done, click `OK` to start the scale set deployment.</span></span>


## <a name="connect-to-a-vm-in-the-scale-set"></a><span data-ttu-id="4be57-134">Connect to a VM in the scale set</span><span class="sxs-lookup"><span data-stu-id="4be57-134">Connect to a VM in the scale set</span></span>
<span data-ttu-id="4be57-135">If you chose to limit your scale set to a single placement group, then the scale set is deployed with NAT rules configured to let you connect to the scale set easily (if not, to connect to the virtual machines in the scale set, you likely need to create a jumpbox in the same virtual network as the scale set).</span><span class="sxs-lookup"><span data-stu-id="4be57-135">If you chose to limit your scale set to a single placement group, then the scale set is deployed with NAT rules configured to let you connect to the scale set easily (if not, to connect to the virtual machines in the scale set, you likely need to create a jumpbox in the same virtual network as the scale set).</span></span> <span data-ttu-id="4be57-136">To see them, navigate to the `Inbound NAT Rules` tab of the load balancer for the scale set:</span><span class="sxs-lookup"><span data-stu-id="4be57-136">To see them, navigate to the `Inbound NAT Rules` tab of the load balancer for the scale set:</span></span>

![ScaleSetPortalNatRules](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machine-scale-sets/media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

<span data-ttu-id="4be57-138">You can connect to each VM in the scale set using these NAT rules.</span><span class="sxs-lookup"><span data-stu-id="4be57-138">You can connect to each VM in the scale set using these NAT rules.</span></span> <span data-ttu-id="4be57-139">For instance, for a Windows scale set, if there is a NAT rule on incoming port 50000, you could connect to that machine via RDP on `<load-balancer-ip-address>:50000`.</span><span class="sxs-lookup"><span data-stu-id="4be57-139">For instance, for a Windows scale set, if there is a NAT rule on incoming port 50000, you could connect to that machine via RDP on `<load-balancer-ip-address>:50000`.</span></span> <span data-ttu-id="4be57-140">For a Linux scale set, you would connect using the command `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span><span class="sxs-lookup"><span data-stu-id="4be57-140">For a Linux scale set, you would connect using the command `ssh -p 50000 <username>@<load-balancer-ip-address>`.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4be57-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="4be57-141">Next steps</span></span>
<span data-ttu-id="4be57-142">For documentation on how to deploy scale sets from the CLI, see [this documentation](virtual-machine-scale-sets-cli-quick-create.md).</span><span class="sxs-lookup"><span data-stu-id="4be57-142">For documentation on how to deploy scale sets from the CLI, see [this documentation](virtual-machine-scale-sets-cli-quick-create.md).</span></span>

<span data-ttu-id="4be57-143">For documentation on how to deploy scale sets from PowerShell, see [this documentation](virtual-machine-scale-sets-windows-create.md).</span><span class="sxs-lookup"><span data-stu-id="4be57-143">For documentation on how to deploy scale sets from PowerShell, see [this documentation](virtual-machine-scale-sets-windows-create.md).</span></span>

<span data-ttu-id="4be57-144">For documentation on how to deploy scale sets from Visual Studio, see [this documentation](virtual-machine-scale-sets-vs-create.md).</span><span class="sxs-lookup"><span data-stu-id="4be57-144">For documentation on how to deploy scale sets from Visual Studio, see [this documentation](virtual-machine-scale-sets-vs-create.md).</span></span>

<span data-ttu-id="4be57-145">For general documentation, check out the [documentation overview page for scale sets](virtual-machine-scale-sets-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4be57-145">For general documentation, check out the [documentation overview page for scale sets](virtual-machine-scale-sets-overview.md).</span></span>

<span data-ttu-id="4be57-146">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span><span class="sxs-lookup"><span data-stu-id="4be57-146">For general information, check out the [main landing page for scale sets](https://azure.microsoft.com/services/virtual-machine-scale-sets/).</span></span>





