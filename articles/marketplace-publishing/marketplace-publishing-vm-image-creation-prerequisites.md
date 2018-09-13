---
title: Technical prerequisites for creating a virtual machine image for the Azure Marketplace | Microsoft Docs
description: Understand the requirements for creating and deploying a virtual machine image to the Azure Marketplace for others to purchase.
services: marketplace-publishing
documentationcenter: ''
author: HannibalSII
manager: hascipio
editor: ''
ms.assetid: 63c16966-0304-4b17-a715-368a0a5ccb2c
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: Azure
ms.workload: na
ms.date: 04/29/2016
ms.author: hascipio; v-divte
ms.openlocfilehash: af3e2ad623d8d7bfafe676411f9ae3fbee78aab8
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670599"
---
# <a name="technical-prerequisites-for-creating-a-virtual-machine-image-for-the-azure-marketplace"></a><span data-ttu-id="ca170-103">Technical prerequisites for creating a virtual machine image for the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="ca170-103">Technical prerequisites for creating a virtual machine image for the Azure Marketplace</span></span>
<span data-ttu-id="ca170-104">Read the process thoroughly before beginning and understand where and why each step is performed.</span><span class="sxs-lookup"><span data-stu-id="ca170-104">Read the process thoroughly before beginning and understand where and why each step is performed.</span></span> <span data-ttu-id="ca170-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning the offer creation process.</span><span class="sxs-lookup"><span data-stu-id="ca170-105">As much as possible, you should prepare your company information and other data, download necessary tools, and/or create technical components before beginning the offer creation process.</span></span> <span data-ttu-id="ca170-106">These items should be clear from reviewing this article.</span><span class="sxs-lookup"><span data-stu-id="ca170-106">These items should be clear from reviewing this article.</span></span>  

## <a name="download-needed-tools--applications"></a><span data-ttu-id="ca170-107">Download needed tools & applications</span><span class="sxs-lookup"><span data-stu-id="ca170-107">Download needed tools & applications</span></span>
<span data-ttu-id="ca170-108">You should have the following items ready before beginning the process:</span><span class="sxs-lookup"><span data-stu-id="ca170-108">You should have the following items ready before beginning the process:</span></span>

* <span data-ttu-id="ca170-109">Depending on which operating system you are targeting, install the [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from the [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span><span class="sxs-lookup"><span data-stu-id="ca170-109">Depending on which operating system you are targeting, install the [Azure PowerShell cmdlets](https://www.microsoft.com/web/handlers/webpi.ashx/getinstaller/WindowsAzurePowershellGet.3f.3f.3fnew.appids) or [Linux command-line interface tool](https://go.microsoft.com/fwlink/?LinkId=253472&clcid=0x409) from the [Azure Downloads](https://azure.microsoft.com/downloads/) page.</span></span>
* <span data-ttu-id="ca170-110">Install Azure Storage Explorer from CodePlex.</span><span class="sxs-lookup"><span data-stu-id="ca170-110">Install Azure Storage Explorer from CodePlex.</span></span>
* <span data-ttu-id="ca170-111">Download and install the Certification Test Tool for Azure Certified:</span><span class="sxs-lookup"><span data-stu-id="ca170-111">Download and install the Certification Test Tool for Azure Certified:</span></span>
  * <span data-ttu-id="ca170-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span><span class="sxs-lookup"><span data-stu-id="ca170-112">[http://go.microsoft.com/fwlink/?LinkID=526913](http://go.microsoft.com/fwlink/?LinkID=526913).</span></span> <span data-ttu-id="ca170-113">You need a Windows-based computer to run the certification tool.</span><span class="sxs-lookup"><span data-stu-id="ca170-113">You need a Windows-based computer to run the certification tool.</span></span> <span data-ttu-id="ca170-114">If you do not have a Windows-based computer available, you can run the tool using a Windows-based VM in Azure.</span><span class="sxs-lookup"><span data-stu-id="ca170-114">If you do not have a Windows-based computer available, you can run the tool using a Windows-based VM in Azure.</span></span>

## <a name="platforms-supported"></a><span data-ttu-id="ca170-115">Platforms supported</span><span class="sxs-lookup"><span data-stu-id="ca170-115">Platforms supported</span></span>
<span data-ttu-id="ca170-116">You can develop Azure-based VMs on Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="ca170-116">You can develop Azure-based VMs on Windows or Linux.</span></span> <span data-ttu-id="ca170-117">Some elements of the publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span><span class="sxs-lookup"><span data-stu-id="ca170-117">Some elements of the publishing process--such as creating an Azure-compatible virtual hard disk (VHD)--use different tools and steps depending on which operating system you are using:</span></span>  

* <span data-ttu-id="ca170-118">If you are using Linux, refer to the “Create an Azure-compatible VHD (Linux-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="ca170-118">If you are using Linux, refer to the “Create an Azure-compatible VHD (Linux-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>
* <span data-ttu-id="ca170-119">If you are using Windows, refer to the “Create an Azure-compatible VHD (Windows-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span><span class="sxs-lookup"><span data-stu-id="ca170-119">If you are using Windows, refer to the “Create an Azure-compatible VHD (Windows-based)” section of the [Virtual machine image publishing guide](marketplace-publishing-vm-image-creation.md).</span></span>

> [!NOTE]
> <span data-ttu-id="ca170-120">You need access to a Windows-based machine to:</span><span class="sxs-lookup"><span data-stu-id="ca170-120">You need access to a Windows-based machine to:</span></span>
> 
> * <span data-ttu-id="ca170-121">Run the certification validation tool.</span><span class="sxs-lookup"><span data-stu-id="ca170-121">Run the certification validation tool.</span></span>
> * <span data-ttu-id="ca170-122">Create the VHD shared access signature URL for the VHD certification submission.</span><span class="sxs-lookup"><span data-stu-id="ca170-122">Create the VHD shared access signature URL for the VHD certification submission.</span></span>
> 
> 

## <a name="develop-your-vhd"></a><span data-ttu-id="ca170-123">Develop your VHD</span><span class="sxs-lookup"><span data-stu-id="ca170-123">Develop your VHD</span></span>
<span data-ttu-id="ca170-124">You can develop Azure VHDs in the cloud or on-premises:</span><span class="sxs-lookup"><span data-stu-id="ca170-124">You can develop Azure VHDs in the cloud or on-premises:</span></span>

* <span data-ttu-id="ca170-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span><span class="sxs-lookup"><span data-stu-id="ca170-125">Cloud-based development means all development steps are performed remotely on a VHD resident on Azure.</span></span>
* <span data-ttu-id="ca170-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span><span class="sxs-lookup"><span data-stu-id="ca170-126">On-premises development requires downloading a VHD and developing it using on-premises infrastructure.</span></span> <span data-ttu-id="ca170-127">Although this is possible, we do not recommend it.</span><span class="sxs-lookup"><span data-stu-id="ca170-127">Although this is possible, we do not recommend it.</span></span> <span data-ttu-id="ca170-128">Note that developing for Windows or SQL on-premises requires you to have the relevant on-premises license keys.</span><span class="sxs-lookup"><span data-stu-id="ca170-128">Note that developing for Windows or SQL on-premises requires you to have the relevant on-premises license keys.</span></span> <span data-ttu-id="ca170-129">You cannot include or install SQL Server after creating a VM.</span><span class="sxs-lookup"><span data-stu-id="ca170-129">You cannot include or install SQL Server after creating a VM.</span></span> <span data-ttu-id="ca170-130">You must also base your offer on an approved SQL image from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="ca170-130">You must also base your offer on an approved SQL image from the Azure portal.</span></span> <span data-ttu-id="ca170-131">If you decide to develop on-premises, you must perform some steps differently than if you were developing in the cloud.</span><span class="sxs-lookup"><span data-stu-id="ca170-131">If you decide to develop on-premises, you must perform some steps differently than if you were developing in the cloud.</span></span> <span data-ttu-id="ca170-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span><span class="sxs-lookup"><span data-stu-id="ca170-132">You can find relevant information in [Create an on-premises VM image](marketplace-publishing-vm-image-creation-on-premise.md).</span></span>

[link-acct-creation]:marketplace-publishing-accounts-creation-registration.md
