---
title: Understand shared IP addresses in Azure DevTest Labs | Microsoft Docs
description: Learn how Azure DevTest Labs uses shared IP addresses to minimize the public IP addresses required to access your lab VMs.
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: ''
ms.assetid: ''
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: f20f1d9370480b13ba1331d95c16345317eba27c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552573"
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a><span data-ttu-id="8a7a7-103">Understand shared IP addresses in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8a7a7-103">Understand shared IP addresses in Azure DevTest Labs</span></span>

<span data-ttu-id="8a7a7-104">Azure DevTest Labs uses shared IP addresses to minimize the number of public IP addresses required to access your individual lab VMs.</span><span class="sxs-lookup"><span data-stu-id="8a7a7-104">Azure DevTest Labs uses shared IP addresses to minimize the number of public IP addresses required to access your individual lab VMs.</span></span>  <span data-ttu-id="8a7a7-105">This article describes how shared IPs work and their related configuration options.</span><span class="sxs-lookup"><span data-stu-id="8a7a7-105">This article describes how shared IPs work and their related configuration options.</span></span>

## <a name="shared-ip-setting"></a><span data-ttu-id="8a7a7-106">Shared IP setting</span><span class="sxs-lookup"><span data-stu-id="8a7a7-106">Shared IP setting</span></span>

<span data-ttu-id="8a7a7-107">When you create a lab, it resides in a subnet of a virtual network.</span><span class="sxs-lookup"><span data-stu-id="8a7a7-107">When you create a lab, it resides in a subnet of a virtual network.</span></span>  <span data-ttu-id="8a7a7-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span><span class="sxs-lookup"><span data-stu-id="8a7a7-108">By default, this subnet is created with **Enable shared public IP** set to *Yes*.</span></span>  <span data-ttu-id="8a7a7-109">This configuration creates one public IP address for the entire subnet.</span><span class="sxs-lookup"><span data-stu-id="8a7a7-109">This configuration creates one public IP address for the entire subnet.</span></span>  <span data-ttu-id="8a7a7-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span><span class="sxs-lookup"><span data-stu-id="8a7a7-110">For more information about configuring virtual networks and subnets, see [Configure a virtual network in Azure DevTest Labs](devtest-lab-configure-vnet.md).</span></span>

![New lab subnet](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-shared-ip/lab-subnet.png)

<span data-ttu-id="8a7a7-112">Any VMs created in this lab default to using a shared IP.</span><span class="sxs-lookup"><span data-stu-id="8a7a7-112">Any VMs created in this lab default to using a shared IP.</span></span>  <span data-ttu-id="8a7a7-113">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span><span class="sxs-lookup"><span data-stu-id="8a7a7-113">When creating the VM, this setting can be observed in the **Advanced settings** blade under **IP address configuration**.</span></span>

![New VM](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-shared-ip/new-vm.png)

<span data-ttu-id="8a7a7-115">Whenever a VM with shared IP enabled is added to the subnet, a TCP port is assigned on the public IP address forwarding to the RDP port on the VM.</span><span class="sxs-lookup"><span data-stu-id="8a7a7-115">Whenever a VM with shared IP enabled is added to the subnet, a TCP port is assigned on the public IP address forwarding to the RDP port on the VM.</span></span>  

## <a name="using-the-shared-ip"></a><span data-ttu-id="8a7a7-116">Using the shared IP</span><span class="sxs-lookup"><span data-stu-id="8a7a7-116">Using the shared IP</span></span>

<span data-ttu-id="8a7a7-117">You connect to Remote Desktop on the VM in an RDP client using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span><span class="sxs-lookup"><span data-stu-id="8a7a7-117">You connect to Remote Desktop on the VM in an RDP client using the IP address or fully qualified domain name, followed by a colon, followed by the port.</span></span>  <span data-ttu-id="8a7a7-118">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span><span class="sxs-lookup"><span data-stu-id="8a7a7-118">For example, in the image below, the RDP address to connect to the VM is `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.</span></span>  <span data-ttu-id="8a7a7-119">Alternatively, from the Azure portal, select the **Connect** button to download a pre-configured RDP file.</span><span class="sxs-lookup"><span data-stu-id="8a7a7-119">Alternatively, from the Azure portal, select the **Connect** button to download a pre-configured RDP file.</span></span>

![VM example](https://docstestmedia1.blob.core.windows.net/azure-media/articles/devtest-lab/media/devtest-lab-shared-ip/vm-info.png)

## <a name="next-steps"></a><span data-ttu-id="8a7a7-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="8a7a7-121">Next steps</span></span>

* [<span data-ttu-id="8a7a7-122">Define lab policies in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8a7a7-122">Define lab policies in Azure DevTest Labs</span></span>](devtest-lab-set-lab-policy.md)
* [<span data-ttu-id="8a7a7-123">Configure a virtual network in Azure DevTest Labs</span><span class="sxs-lookup"><span data-stu-id="8a7a7-123">Configure a virtual network in Azure DevTest Labs</span></span>](devtest-lab-configure-vnet.md)








