---
title: Azure Applications Managed Application Offer Publishing Guide
description: This article describes the requirements to publish a managed application in the Marketplace
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
ms.openlocfilehash: c8ead3dc34faefce0f113dee2074960fddfa11a1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858008"
---
# <a name="azure-applications-managed-application-offer-publishing-guide"></a><span data-ttu-id="648cb-103">Azure Applications: Managed Application Offer Publishing Guide</span><span class="sxs-lookup"><span data-stu-id="648cb-103">Azure Applications: Managed Application Offer Publishing Guide</span></span>

<span data-ttu-id="648cb-104">A managed application is one of the main ways to publish a solution in the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="648cb-104">A managed application is one of the main ways to publish a solution in the Marketplace.</span></span> <span data-ttu-id="648cb-105">Use this guide to understand the requirements for this offer.</span><span class="sxs-lookup"><span data-stu-id="648cb-105">Use this guide to understand the requirements for this offer.</span></span> 

<span data-ttu-id="648cb-106">These are transaction offers which are deployed and billed through the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="648cb-106">These are transaction offers which are deployed and billed through the Marketplace.</span></span> <span data-ttu-id="648cb-107">The call to action that a user sees is "Get It Now."</span><span class="sxs-lookup"><span data-stu-id="648cb-107">The call to action that a user sees is "Get It Now."</span></span>

<span data-ttu-id="648cb-108">Use the Azure app: managed app offer type when the following conditions are required:</span><span class="sxs-lookup"><span data-stu-id="648cb-108">Use the Azure app: managed app offer type when the following conditions are required:</span></span>
- <span data-ttu-id="648cb-109">You deploy either a subscription-based solution for your customer using either a VM or an entire IaaS-based solution.</span><span class="sxs-lookup"><span data-stu-id="648cb-109">You deploy either a subscription-based solution for your customer using either a VM or an entire IaaS-based solution.</span></span>
- <span data-ttu-id="648cb-110">You or your customer require that the solution is managed by a partner.</span><span class="sxs-lookup"><span data-stu-id="648cb-110">You or your customer require that the solution is managed by a partner.</span></span>

>[!NOTE]
><span data-ttu-id="648cb-111">For example, a partner may be an SI or managed service provider (MSP).</span><span class="sxs-lookup"><span data-stu-id="648cb-111">For example, a partner may be an SI or managed service provider (MSP).</span></span>  

## <a name="managed-application-offer"></a><span data-ttu-id="648cb-112">Managed Application Offer</span><span class="sxs-lookup"><span data-stu-id="648cb-112">Managed Application Offer</span></span>

|<span data-ttu-id="648cb-113">Requirements</span><span class="sxs-lookup"><span data-stu-id="648cb-113">Requirements</span></span> |<span data-ttu-id="648cb-114">Details</span><span class="sxs-lookup"><span data-stu-id="648cb-114">Details</span></span>  |
|---------|---------|
|<span data-ttu-id="648cb-115">Deployed to a customer’s Azure subscription</span><span class="sxs-lookup"><span data-stu-id="648cb-115">Deployed to a customer’s Azure subscription</span></span> | <span data-ttu-id="648cb-116">Managed Apps must be deployed in the customer’s subscription and can be managed by a 3rd party</span><span class="sxs-lookup"><span data-stu-id="648cb-116">Managed Apps must be deployed in the customer’s subscription and can be managed by a 3rd party</span></span> | 
|<span data-ttu-id="648cb-117">Billing and metering</span><span class="sxs-lookup"><span data-stu-id="648cb-117">Billing and metering</span></span>    |  <span data-ttu-id="648cb-118">The resources will be provisioned in the customer’s Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="648cb-118">The resources will be provisioned in the customer’s Azure subscription.</span></span> <span data-ttu-id="648cb-119">Pay-as-you-go (PAYGO) virtual machines will be transacted with the customer via Microsoft, billed via the customer’s Azure subscription (PAYGO)</span><span class="sxs-lookup"><span data-stu-id="648cb-119">Pay-as-you-go (PAYGO) virtual machines will be transacted with the customer via Microsoft, billed via the customer’s Azure subscription (PAYGO)</span></span> 
<span data-ttu-id="648cb-120">In the case of bring-your-own-license, while Microsoft will bill infrastructure costs incurred in the customer subscription, you will transact your software licensing fees to the customer directly</span><span class="sxs-lookup"><span data-stu-id="648cb-120">In the case of bring-your-own-license, while Microsoft will bill infrastructure costs incurred in the customer subscription, you will transact your software licensing fees to the customer directly</span></span>        |
|<span data-ttu-id="648cb-121">Azure-compatible virtual hard disk (VHD)</span><span class="sxs-lookup"><span data-stu-id="648cb-121">Azure-compatible virtual hard disk (VHD)</span></span>    |   <span data-ttu-id="648cb-122">VMs must be built on Windows or Linux.</span><span class="sxs-lookup"><span data-stu-id="648cb-122">VMs must be built on Windows or Linux.</span></span><ul> <li><span data-ttu-id="648cb-123">For more information about creating a Linux VHD, visit the Create an Azure-compatible VHD (Linux-based) section located at [docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#2-create-an-azure-compatible-vhd-linux-based](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#2-create-an-azure-compatible-vhd-linux-based).</span><span class="sxs-lookup"><span data-stu-id="648cb-123">For more information about creating a Linux VHD, visit the Create an Azure-compatible VHD (Linux-based) section located at [docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#2-create-an-azure-compatible-vhd-linux-based](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#2-create-an-azure-compatible-vhd-linux-based).</span></span></li> <li><span data-ttu-id="648cb-124">For more information about creating a Windows VHD, visit the Create an Azure-compatible VHD (Windows-based) section located at [docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#3-create-an-azure-compatible-vhd-windows-based](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#3-create-an-azure-compatible-vhd-windows-based).</span><span class="sxs-lookup"><span data-stu-id="648cb-124">For more information about creating a Windows VHD, visit the Create an Azure-compatible VHD (Windows-based) section located at [docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#3-create-an-azure-compatible-vhd-windows-based](https://docs.microsoft.com/azure/marketplace-publishing/marketplace-publishing-vm-image-creation#3-create-an-azure-compatible-vhd-windows-based).</span></span></li> </ul>      |

>[!NOTE]
> <span data-ttu-id="648cb-125">Managed apps must be deployable through the Marketplace.</span><span class="sxs-lookup"><span data-stu-id="648cb-125">Managed apps must be deployable through the Marketplace.</span></span> <span data-ttu-id="648cb-126">If customer communication is a concern, then you should reach out to interested customers after you have enabled lead sharing.</span><span class="sxs-lookup"><span data-stu-id="648cb-126">If customer communication is a concern, then you should reach out to interested customers after you have enabled lead sharing.</span></span>  


## <a name="next-steps"></a><span data-ttu-id="648cb-127">Next Steps</span><span class="sxs-lookup"><span data-stu-id="648cb-127">Next Steps</span></span>
<span data-ttu-id="648cb-128">If you haven't already done so,</span><span class="sxs-lookup"><span data-stu-id="648cb-128">If you haven't already done so,</span></span> 

- <span data-ttu-id="648cb-129">[Register](https://azuremarketplace.microsoft.com/sell) in the marketplace</span><span class="sxs-lookup"><span data-stu-id="648cb-129">[Register](https://azuremarketplace.microsoft.com/sell) in the marketplace</span></span>

<span data-ttu-id="648cb-130">If you're registered and are creating a new offer or working on an existing one,</span><span class="sxs-lookup"><span data-stu-id="648cb-130">If you're registered and are creating a new offer or working on an existing one,</span></span>

- <span data-ttu-id="648cb-131">[Log in to Cloud Partner Portal](https://cloudpartner.azure.com) to create or complete your offer</span><span class="sxs-lookup"><span data-stu-id="648cb-131">[Log in to Cloud Partner Portal](https://cloudpartner.azure.com) to create or complete your offer</span></span>
