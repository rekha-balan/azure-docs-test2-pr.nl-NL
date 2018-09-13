---
title: Azure Applications Solution Template Offer Publishing Guide
description: This article describes the requirements to publish a solution template in the Marketplace
services: Azure, Marketplace, Compute, Storage, Networking, Blockchain, Security
documentationcenter: ''
author: ellacroi
manager: nunoc
editor: ''
ms.assetid: ''
ms.service: marketplace
ms.workload: ''
ms.tgt_pltfrm: ''
ms.devlang: ''
ms.topic: article
ms.date: 07/09/2018
ms.author: ellacroi
ms.openlocfilehash: 44d081a0666aa37ec0bf8eeac540b7a7f4f4f904
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857338"
---
# <a name="azure-applications-solution-template-offer-publishing-guide"></a><span data-ttu-id="70c9d-103">Azure Applications: Solution Template Offer Publishing Guide</span><span class="sxs-lookup"><span data-stu-id="70c9d-103">Azure Applications: Solution Template Offer Publishing Guide</span></span>

<span data-ttu-id="70c9d-104">Solution Templates are one of the main ways to publish a solution in the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="70c9d-104">Solution Templates are one of the main ways to publish a solution in the Marketplace.</span></span> <span data-ttu-id="70c9d-105">Use this guide to understand the requirements for this offer.</span><span class="sxs-lookup"><span data-stu-id="70c9d-105">Use this guide to understand the requirements for this offer.</span></span> 

<span data-ttu-id="70c9d-106">These are transaction offers which are deployed and billed through the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="70c9d-106">These are transaction offers which are deployed and billed through the Marketplace.</span></span> <span data-ttu-id="70c9d-107">The call to action that a user sees is "Get It Now."</span><span class="sxs-lookup"><span data-stu-id="70c9d-107">The call to action that a user sees is "Get It Now."</span></span>

<span data-ttu-id="70c9d-108">Use the Azure app: solution template offer type when your solution requires additional deployment and configuration automation beyond a simple VM.</span><span class="sxs-lookup"><span data-stu-id="70c9d-108">Use the Azure app: solution template offer type when your solution requires additional deployment and configuration automation beyond a simple VM.</span></span> <span data-ttu-id="70c9d-109">You may automate the provisioning of one or more VMs using Azure apps: solution templates.</span><span class="sxs-lookup"><span data-stu-id="70c9d-109">You may automate the provisioning of one or more VMs using Azure apps: solution templates.</span></span> <span data-ttu-id="70c9d-110">You may also provision networking and storage resources.</span><span class="sxs-lookup"><span data-stu-id="70c9d-110">You may also provision networking and storage resources.</span></span> <span data-ttu-id="70c9d-111">Azure apps: solution templates offer type provides automation benefits for single VMs and entire IaaS-based solutions.</span><span class="sxs-lookup"><span data-stu-id="70c9d-111">Azure apps: solution templates offer type provides automation benefits for single VMs and entire IaaS-based solutions.</span></span>

## <a name="requirements-for-solution-templates"></a><span data-ttu-id="70c9d-112">Requirements for Solution Templates</span><span class="sxs-lookup"><span data-stu-id="70c9d-112">Requirements for Solution Templates</span></span>

|<span data-ttu-id="70c9d-113">Requirements</span><span class="sxs-lookup"><span data-stu-id="70c9d-113">Requirements</span></span> |<span data-ttu-id="70c9d-114">Details</span><span class="sxs-lookup"><span data-stu-id="70c9d-114">Details</span></span>  |
|---------|---------|
|<span data-ttu-id="70c9d-115">Billing and metering</span><span class="sxs-lookup"><span data-stu-id="70c9d-115">Billing and metering</span></span>    |  <span data-ttu-id="70c9d-116">The resources will be provisioned in the customer’s Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="70c9d-116">The resources will be provisioned in the customer’s Azure subscription.</span></span> <span data-ttu-id="70c9d-117">Pay-as-you-go (PAYGO) virtual machines will be transacted with the customer via Microsoft, billed via the customer’s Azure subscription (PAYGO)</span><span class="sxs-lookup"><span data-stu-id="70c9d-117">Pay-as-you-go (PAYGO) virtual machines will be transacted with the customer via Microsoft, billed via the customer’s Azure subscription (PAYGO)</span></span> 
<span data-ttu-id="70c9d-118">In the case of bring-your-own-license, while Microsoft will bill infrastructure costs incurred in the customer subscription, you will transact your software licensing fees to the customer directly</span><span class="sxs-lookup"><span data-stu-id="70c9d-118">In the case of bring-your-own-license, while Microsoft will bill infrastructure costs incurred in the customer subscription, you will transact your software licensing fees to the customer directly</span></span>        |
|<span data-ttu-id="70c9d-119">Azure-compatible virtual hard disk (VHD)</span><span class="sxs-lookup"><span data-stu-id="70c9d-119">Azure-compatible virtual hard disk (VHD)</span></span>    |   <span data-ttu-id="70c9d-120">VMs must be built on Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="70c9d-120">VMs must be built on Windows or Linux.</span></span><ul> <li><span data-ttu-id="70c9d-121">For more information about creating a Linux VHD, visit the Create an Azure-compatible VHD (Linux-based) section located at [docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#2-create-an-azure-compatible-vhd-linux-based](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#2-create-an-azure-compatible-vhd-linux-based).</span><span class="sxs-lookup"><span data-stu-id="70c9d-121">For more information about creating a Linux VHD, visit the Create an Azure-compatible VHD (Linux-based) section located at [docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#2-create-an-azure-compatible-vhd-linux-based](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#2-create-an-azure-compatible-vhd-linux-based).</span></span></li> <li><span data-ttu-id="70c9d-122">For more information about creating a Windows VHD, visit the Create an Azure-compatible VHD (Windows-based) section located at [docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#3-create-an-azure-compatible-vhd-windows-based](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#3-create-an-azure-compatible-vhd-windows-based).</span><span class="sxs-lookup"><span data-stu-id="70c9d-122">For more information about creating a Windows VHD, visit the Create an Azure-compatible VHD (Windows-based) section located at [docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#3-create-an-azure-compatible-vhd-windows-based](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#3-create-an-azure-compatible-vhd-windows-based).</span></span></li> </ul>      |



## <a name="next-steps"></a><span data-ttu-id="70c9d-123">Next Steps</span><span class="sxs-lookup"><span data-stu-id="70c9d-123">Next Steps</span></span>
<span data-ttu-id="70c9d-124">If you haven't already done so,</span><span class="sxs-lookup"><span data-stu-id="70c9d-124">If you haven't already done so,</span></span> 

- <span data-ttu-id="70c9d-125">[Register](https://azuremarketplace.microsoft.com/sell) in the marketplace</span><span class="sxs-lookup"><span data-stu-id="70c9d-125">[Register](https://azuremarketplace.microsoft.com/sell) in the marketplace</span></span>

<span data-ttu-id="70c9d-126">If you're registered and are creating a new offer or working on an existing one,</span><span class="sxs-lookup"><span data-stu-id="70c9d-126">If you're registered and are creating a new offer or working on an existing one,</span></span>

- <span data-ttu-id="70c9d-127">[Log in to Cloud Partner Portal](https://cloudpartner.azure.com) to create or complete your offer</span><span class="sxs-lookup"><span data-stu-id="70c9d-127">[Log in to Cloud Partner Portal](https://cloudpartner.azure.com) to create or complete your offer</span></span>
