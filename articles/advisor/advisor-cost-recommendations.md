---
title: Azure Advisor Cost recommendations | Microsoft Docs
description: Use Azure Advisor to optimize the cost of your Azure deployments.
services: advisor
documentationcenter: NA
author: manbeenkohli
manager: ''
ms.assetid: ''
ms.service: advisor
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 11/16/2016
ms.author: makohli
ms.openlocfilehash: 71c380a1caae730b6b01615ce3047c2e22bd6dfb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44788767"
---
# <a name="advisor-cost-recommendations"></a><span data-ttu-id="def41-103">Advisor Cost recommendations</span><span class="sxs-lookup"><span data-stu-id="def41-103">Advisor Cost recommendations</span></span>

<span data-ttu-id="def41-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span><span class="sxs-lookup"><span data-stu-id="def41-104">Advisor helps you optimize and reduce your overall Azure spend by identifying idle and underutilized resources.</span></span> <span data-ttu-id="def41-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span><span class="sxs-lookup"><span data-stu-id="def41-105">You can get cost recommendations from the **Cost** tab on the Advisor dashboard.</span></span>

## <a name="optimize-virtual-machine-spend-by-resizing-or-shutting-down-underutilized-instances"></a><span data-ttu-id="def41-106">Optimize virtual machine spend by resizing or shutting down underutilized instances</span><span class="sxs-lookup"><span data-stu-id="def41-106">Optimize virtual machine spend by resizing or shutting down underutilized instances</span></span> 
<span data-ttu-id="def41-107">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="def41-107">Although certain application scenarios can result in low utilization by design, you can often save money by managing the size and number of your virtual machines.</span></span> <span data-ttu-id="def41-108">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span><span class="sxs-lookup"><span data-stu-id="def41-108">Advisor monitors your virtual machine usage for 14 days and then identifies low-utilization virtual machines.</span></span> <span data-ttu-id="def41-109">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span><span class="sxs-lookup"><span data-stu-id="def41-109">Virtual machines whose CPU utilization is 5 percent or less and network usage is 7 MB or less for four or more days are considered low-utilization virtual machines.</span></span>

<span data-ttu-id="def41-110">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span><span class="sxs-lookup"><span data-stu-id="def41-110">Advisor shows you the estimated cost of continuing to run your virtual machine, so that you can choose to shut it down or resize it.</span></span>

<span data-ttu-id="def41-111">If you want to be more aggressive at identifying underutilized virtual machines, you can adjust the average CPU utilization rule on a per subscription basis.</span><span class="sxs-lookup"><span data-stu-id="def41-111">If you want to be more aggressive at identifying underutilized virtual machines, you can adjust the average CPU utilization rule on a per subscription basis.</span></span>

## <a name="reduce-costs-by-eliminating-unprovisioned-expressroute-circuits"></a><span data-ttu-id="def41-112">Reduce costs by eliminating unprovisioned ExpressRoute circuits</span><span class="sxs-lookup"><span data-stu-id="def41-112">Reduce costs by eliminating unprovisioned ExpressRoute circuits</span></span>
<span data-ttu-id="def41-113">Advisor identifies ExpressRoute circuits that have been in the provider status of *Not Provisioned* for more than one month, and recommends deleting the circuit if you aren't planning to provision the circuit with your connectivity provider.</span><span class="sxs-lookup"><span data-stu-id="def41-113">Advisor identifies ExpressRoute circuits that have been in the provider status of *Not Provisioned* for more than one month, and recommends deleting the circuit if you aren't planning to provision the circuit with your connectivity provider.</span></span>

## <a name="reduce-costs-by-deleting-or-reconfiguring-idle-virtual-network-gateways"></a><span data-ttu-id="def41-114">Reduce costs by deleting or reconfiguring idle virtual network gateways</span><span class="sxs-lookup"><span data-stu-id="def41-114">Reduce costs by deleting or reconfiguring idle virtual network gateways</span></span>
<span data-ttu-id="def41-115">Advisor identifies virtual network gates that have been idle for over 90 days.</span><span class="sxs-lookup"><span data-stu-id="def41-115">Advisor identifies virtual network gates that have been idle for over 90 days.</span></span> <span data-ttu-id="def41-116">Since these gateways are billed hourly, you should consider reconfiguring or deleting them if you don't intend to use them anymore.</span><span class="sxs-lookup"><span data-stu-id="def41-116">Since these gateways are billed hourly, you should consider reconfiguring or deleting them if you don't intend to use them anymore.</span></span> 

## <a name="buy-reserved-virtual-machine-instances-to-save-money-over-pay-as-you-go-costs"></a><span data-ttu-id="def41-117">Buy reserved virtual machine instances to save money over pay-as-you-go costs</span><span class="sxs-lookup"><span data-stu-id="def41-117">Buy reserved virtual machine instances to save money over pay-as-you-go costs</span></span>
<span data-ttu-id="def41-118">Advisor will review your virtual machine usage over the last 30 days and determine if you could save money by purchasing an Azure reservation.</span><span class="sxs-lookup"><span data-stu-id="def41-118">Advisor will review your virtual machine usage over the last 30 days and determine if you could save money by purchasing an Azure reservation.</span></span> <span data-ttu-id="def41-119">Advisor will show you the regions and sizes where you potentially have the most savings and will show you the estimated savings from purchasing reservations.</span><span class="sxs-lookup"><span data-stu-id="def41-119">Advisor will show you the regions and sizes where you potentially have the most savings and will show you the estimated savings from purchasing reservations.</span></span> 

<span data-ttu-id="def41-120">With Azure reservations, you can pre-purchase the base costs for your virtual machines.</span><span class="sxs-lookup"><span data-stu-id="def41-120">With Azure reservations, you can pre-purchase the base costs for your virtual machines.</span></span> <span data-ttu-id="def41-121">Discounts will automatically apply to new or existing VMs that have the same size and region as your reservations.</span><span class="sxs-lookup"><span data-stu-id="def41-121">Discounts will automatically apply to new or existing VMs that have the same size and region as your reservations.</span></span> [<span data-ttu-id="def41-122">Learn more about Azure Reserved VM Instances.</span><span class="sxs-lookup"><span data-stu-id="def41-122">Learn more about Azure Reserved VM Instances.</span></span>](https://azure.microsoft.com/pricing/reserved-vm-instances/)

## <a name="how-to-access-cost-recommendations-in-azure-advisor"></a><span data-ttu-id="def41-123">How to access Cost recommendations in Azure Advisor</span><span class="sxs-lookup"><span data-stu-id="def41-123">How to access Cost recommendations in Azure Advisor</span></span>

1. <span data-ttu-id="def41-124">Sign in to the [Azure portal](https://portal.azure.com), and then open [Advisor](https://aka.ms/azureadvisordashboard).</span><span class="sxs-lookup"><span data-stu-id="def41-124">Sign in to the [Azure portal](https://portal.azure.com), and then open [Advisor](https://aka.ms/azureadvisordashboard).</span></span>

2.  <span data-ttu-id="def41-125">On the Advisor dashboard, click the **Cost** tab.</span><span class="sxs-lookup"><span data-stu-id="def41-125">On the Advisor dashboard, click the **Cost** tab.</span></span>

## <a name="next-steps"></a><span data-ttu-id="def41-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="def41-126">Next steps</span></span>

<span data-ttu-id="def41-127">To learn more about Advisor recommendations, see:</span><span class="sxs-lookup"><span data-stu-id="def41-127">To learn more about Advisor recommendations, see:</span></span>
* [<span data-ttu-id="def41-128">Introduction to Advisor</span><span class="sxs-lookup"><span data-stu-id="def41-128">Introduction to Advisor</span></span>](advisor-overview.md)
* [<span data-ttu-id="def41-129">Get Started</span><span class="sxs-lookup"><span data-stu-id="def41-129">Get Started</span></span>](advisor-get-started.md)
* [<span data-ttu-id="def41-130">Advisor Performance recommendations</span><span class="sxs-lookup"><span data-stu-id="def41-130">Advisor Performance recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="def41-131">Advisor High Availability recommendations</span><span class="sxs-lookup"><span data-stu-id="def41-131">Advisor High Availability recommendations</span></span>](advisor-cost-recommendations.md)
* [<span data-ttu-id="def41-132">Advisor Security recommendations</span><span class="sxs-lookup"><span data-stu-id="def41-132">Advisor Security recommendations</span></span>](advisor-cost-recommendations.md)
