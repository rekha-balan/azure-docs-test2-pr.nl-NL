---
title: How to troubleshoot common issues during VHD creation | Microsoft Docs
description: Answers to common troubleshooting questions and issues during VHD creation.
services: Azure Marketplace
documentationcenter: ''
author: HannibalSII
manager: ''
editor: ''
ms.assetid: e39563d8-8646-4cb7-b078-8b10ac35b494
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 09/26/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: c4e88a9fbb15dd90d619b159ae1065dfacc1907f
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551515"
---
# <a name="how-to-troubleshoot-common-issues-encountered-during-vhd-creation"></a><span data-ttu-id="977aa-103">How to troubleshoot common issues encountered during VHD creation</span><span class="sxs-lookup"><span data-stu-id="977aa-103">How to troubleshoot common issues encountered during VHD creation</span></span>
<span data-ttu-id="977aa-104">This article is provided to help an Azure Marketplace publisher and/or co-administrator that may experience an issue or have common questions while publishing or managing their virtual machine solution(s).</span><span class="sxs-lookup"><span data-stu-id="977aa-104">This article is provided to help an Azure Marketplace publisher and/or co-administrator that may experience an issue or have common questions while publishing or managing their virtual machine solution(s).</span></span>

1. <span data-ttu-id="977aa-105">How do I change the name of the host?</span><span class="sxs-lookup"><span data-stu-id="977aa-105">How do I change the name of the host?</span></span>
   
    <span data-ttu-id="977aa-106">Once VM is created, users can’t update the name of the host.</span><span class="sxs-lookup"><span data-stu-id="977aa-106">Once VM is created, users can’t update the name of the host.</span></span>
2. <span data-ttu-id="977aa-107">How to reset the Remote Desktop service or its login password?</span><span class="sxs-lookup"><span data-stu-id="977aa-107">How to reset the Remote Desktop service or its login password?</span></span>
   
   * [<span data-ttu-id="977aa-108">Reference for Windows VM</span><span class="sxs-lookup"><span data-stu-id="977aa-108">Reference for Windows VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-reset-rdp/)
   * [<span data-ttu-id="977aa-109">Reference for Linux VM</span><span class="sxs-lookup"><span data-stu-id="977aa-109">Reference for Linux VM</span></span>](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)
3. <span data-ttu-id="977aa-110">How to generate new ssh certificates?</span><span class="sxs-lookup"><span data-stu-id="977aa-110">How to generate new ssh certificates?</span></span>
   
   <span data-ttu-id="977aa-111">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span><span class="sxs-lookup"><span data-stu-id="977aa-111">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/](https://azure.microsoft.com/documentation/articles/virtual-machines-linux-classic-reset-access/)</span></span>
4. <span data-ttu-id="977aa-112">How to configure an open VPN certificate?</span><span class="sxs-lookup"><span data-stu-id="977aa-112">How to configure an open VPN certificate?</span></span>
   
   <span data-ttu-id="977aa-113">Please refer to the link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span><span class="sxs-lookup"><span data-stu-id="977aa-113">Please refer to the link: [https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/](https://azure.microsoft.com/documentation/articles/vpn-gateway-point-to-site-create/)</span></span>
5. <span data-ttu-id="977aa-114">What is the support policy for running Microsoft server software in the Microsoft Azure virtual machine environment (infrastructure-as-a-service)?</span><span class="sxs-lookup"><span data-stu-id="977aa-114">What is the support policy for running Microsoft server software in the Microsoft Azure virtual machine environment (infrastructure-as-a-service)?</span></span>
   
   <span data-ttu-id="977aa-115">Please refer to the link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="977aa-115">Please refer to the link: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
6. <span data-ttu-id="977aa-116">Do Virtual Machines have any unique identifier?</span><span class="sxs-lookup"><span data-stu-id="977aa-116">Do Virtual Machines have any unique identifier?</span></span>
   
   <span data-ttu-id="977aa-117">Azure encodes Azure VM Unique ID in every VM.</span><span class="sxs-lookup"><span data-stu-id="977aa-117">Azure encodes Azure VM Unique ID in every VM.</span></span> <span data-ttu-id="977aa-118">See details in this blog and documentation.</span><span class="sxs-lookup"><span data-stu-id="977aa-118">See details in this blog and documentation.</span></span>
7. <span data-ttu-id="977aa-119">In a VM how can I manage the custom script extension in the startup task?</span><span class="sxs-lookup"><span data-stu-id="977aa-119">In a VM how can I manage the custom script extension in the startup task?</span></span>
   
   <span data-ttu-id="977aa-120">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span><span class="sxs-lookup"><span data-stu-id="977aa-120">Please refer to the link: [https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/)</span></span>
8. <span data-ttu-id="977aa-121">How to create a VM from the Azure portal using the VHD that is uploaded to premium storage?</span><span class="sxs-lookup"><span data-stu-id="977aa-121">How to create a VM from the Azure portal using the VHD that is uploaded to premium storage?</span></span>
   
   <span data-ttu-id="977aa-122">We do not support this feature yet.</span><span class="sxs-lookup"><span data-stu-id="977aa-122">We do not support this feature yet.</span></span>
9. <span data-ttu-id="977aa-123">Is a 32-bit app supported in the Azure Marketplace?</span><span class="sxs-lookup"><span data-stu-id="977aa-123">Is a 32-bit app supported in the Azure Marketplace?</span></span>
   
   <span data-ttu-id="977aa-124">Please refer to the link for details on the support policy: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span><span class="sxs-lookup"><span data-stu-id="977aa-124">Please refer to the link for details on the support policy: [https://support.microsoft.com/kb/2721672](https://support.microsoft.com/kb/2721672)</span></span>
10. <span data-ttu-id="977aa-125">Every time I am trying to create an image from my VHDs, I get the error “.VHD is already registered with image repository as the resource” in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="977aa-125">Every time I am trying to create an image from my VHDs, I get the error “.VHD is already registered with image repository as the resource” in PowerShell.</span></span> <span data-ttu-id="977aa-126">I did not create any image before nor did I find any image with this name in Azure.</span><span class="sxs-lookup"><span data-stu-id="977aa-126">I did not create any image before nor did I find any image with this name in Azure.</span></span> <span data-ttu-id="977aa-127">How do I resolve this?</span><span class="sxs-lookup"><span data-stu-id="977aa-127">How do I resolve this?</span></span>
    
    <span data-ttu-id="977aa-128">This usually happen if the user provisioned a VM from this VHD and there is a lock on that VHD.</span><span class="sxs-lookup"><span data-stu-id="977aa-128">This usually happen if the user provisioned a VM from this VHD and there is a lock on that VHD.</span></span> <span data-ttu-id="977aa-129">Please check that there is no VM allocated from this VHD.</span><span class="sxs-lookup"><span data-stu-id="977aa-129">Please check that there is no VM allocated from this VHD.</span></span> <span data-ttu-id="977aa-130">If the error still persist , then please raise a support ticket using this link or from the Publishing portal regarding this (details are given in the answer of question 11).</span><span class="sxs-lookup"><span data-stu-id="977aa-130">If the error still persist , then please raise a support ticket using this link or from the Publishing portal regarding this (details are given in the answer of question 11).</span></span>