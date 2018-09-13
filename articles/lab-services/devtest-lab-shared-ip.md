---
title: Understand shared IP addresses in Azure DevTest Labs | Microsoft Docs
description: Learn how Azure DevTest Labs uses shared IP addresses to minimize the public IP addresses required to access your lab VMs.
services: devtest-lab,virtual-machines,lab-services
documentationcenter: na
author: spelluru
manager: femila
ms.assetid: ''
ms.service: lab-services
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/17/2018
ms.author: spelluru
ms.openlocfilehash: c62f8808565022371484b936f5a2bdaba1f8900e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868600"
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="7acfc-103">Understand shared IP addresses in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="7acfc-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="7acfc-104">Azure DevTest Labs lets lab VMs share the same public IP address to minimize the number of public IP addresses required to access your individual lab VMs.</span><span class="sxs-lookup"><span data-stu-id="7acfc-104">Azure DevTest Labs lets lab VMs share the same public IP address to minimize the number of public IP addresses required to access your individual lab VMs.</span></span>  <span data-ttu-id="7acfc-105">This article describes how shared IPs work and their related configuration options.</span><span class="sxs-lookup"><span data-stu-id="7acfc-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="7acfc-106">Shared IP setting</span><span class="sxs-lookup"><span data-stu-id="7acfc-106">Shared IP setting</span></span>

<span data-ttu-id="7acfc-107">When you create a lab, it resides in a subnet of a virtual network.</span><span class="sxs-lookup"><span data-stu-id="7acfc-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="7acfc-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span><span class="sxs-lookup"><span data-stu-id="7acfc-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span></span>  <span data-ttu-id="7acfc-109">This configuration creates one public IP address for the entire subnet.</span><span class="sxs-lookup"><span data-stu-id="7acfc-109">This configuration creates one public IP address for the entire subnet.</span></span>  <span data-ttu-id="7acfc-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="7acfc-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![New lab subnet](media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="7acfc-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span><span class="sxs-lookup"><span data-stu-id="7acfc-112">For existing labs, you can enable this option by selecting **Configuration and policies > Virtual Networks**.</span></span> <span data-ttu-id="7acfc-113">Then, select a virtual network from the list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span><span class="sxs-lookup"><span data-stu-id="7acfc-113">Then, select a virtual network from the list and choose **ENABLE SHARED PUBLIC IP** for a selected subnet.</span></span> <span data-ttu-id="7acfc-114">You can also disable this option in any lab if you don't want to share a public IP address across lab VMs.</span><span class="sxs-lookup"><span data-stu-id="7acfc-114">You can also disable this option in any lab if you don't want to share a public IP address across lab VMs.</span></span>

<span data-ttu-id="7acfc-115">Any VMs created in this lab default to using a shared IP.</span><span class="sxs-lookup"><span data-stu-id="7acfc-115">Any VMs created in this lab default to using a shared IP.</span></span>  <span data-ttu-id="7acfc-116">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span><span class="sxs-lookup"><span data-stu-id="7acfc-116">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span></span>

![New VM](media/devtest-lab-shared-ip/new-vm.png)

- <span data-ttu-id="7acfc-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span><span class="sxs-lookup"><span data-stu-id="7acfc-118">**Shared:** All VMs created as **Shared** are placed into one resource group (RG).</span></span> <span data-ttu-id="7acfc-119">A single IP address is assigned for that RG and all VMs in the RG will use that IP address.</span><span class="sxs-lookup"><span data-stu-id="7acfc-119">A single IP address is assigned for that RG and all VMs in the RG will use that IP address.</span></span>
- <span data-ttu-id="7acfc-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span><span class="sxs-lookup"><span data-stu-id="7acfc-120">**Public:** Every VM you create has its own IP address and is created in its own resource group.</span></span>
- <span data-ttu-id="7acfc-121">**Private:** Every VM you create uses a private IP address.</span><span class="sxs-lookup"><span data-stu-id="7acfc-121">**Private:** Every VM you create uses a private IP address.</span></span> <span data-ttu-id="7acfc-122">You will not be able to connect to this VM directly from the internet with Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="7acfc-122">You will not be able to connect to this VM directly from the internet with Remote Desktop.</span></span>

<span data-ttu-id="7acfc-123">Whenever a VM with shared IP enabled is added to the subnet, DevTest Labs automatically adds the VM to a load balancer and assigns a TCP port number on the public IP address, forwarding to the RDP port on the VM.</span><span class="sxs-lookup"><span data-stu-id="7acfc-123">Whenever a VM with shared IP enabled is added to the subnet, DevTest Labs automatically adds the VM to a load balancer and assigns a TCP port number on the public IP address, forwarding to the RDP port on the VM.</span></span>  

## <a name="using-the-shared-ip"></a><span data-ttu-id="7acfc-124">Using the shared IP</span><span class="sxs-lookup"><span data-stu-id="7acfc-124">Using the shared IP</span></span>

- <span data-ttu-id="7acfc-125">**Linux users:** SSH to the VM by using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span><span class="sxs-lookup"><span data-stu-id="7acfc-125">**Linux users:** SSH to the VM by using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span></span> <span data-ttu-id="7acfc-126">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="7acfc-126">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>

  ![VM example](media/devtest-lab-shared-ip/vm-info.png)

- <span data-ttu-id="7acfc-128">**Windows users:** Select the **Connect** button on the Azure portal to download a pre-configured RDP file and access the VM.</span><span class="sxs-lookup"><span data-stu-id="7acfc-128">**Windows users:** Select the **Connect** button on the Azure portal to download a pre-configured RDP file and access the VM.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7acfc-129">Next steps</span><span class="sxs-lookup"><span data-stu-id="7acfc-129">Next steps</span></span>

* [<span data-ttu-id="7acfc-130">Define lab policies in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="7acfc-130">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="7acfc-131">Configure a virtual network in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="7acfc-131">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)





