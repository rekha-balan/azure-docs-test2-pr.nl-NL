---
title: Offering services in Azure Stack | Microsoft Docs
description: As a cloud operator, you can offer services to your users.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2018
ms.author: brenduns
ms.reviewer: ''
ms.openlocfilehash: 042e65cfe350cb61124ed8920ae3616502e6553d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856237"
---
# <a name="overview-of-offering-services-in-azure-stack"></a><span data-ttu-id="a18c2-103">Overview of offering services in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a18c2-103">Overview of offering services in Azure Stack</span></span>

<span data-ttu-id="a18c2-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span><span class="sxs-lookup"><span data-stu-id="a18c2-104">*Applies to: Azure Stack integrated systems and Azure Stack Development Kit*</span></span>

<span data-ttu-id="a18c2-105">[Microsoft Azure Stack](azure-stack-poc.md) is a hybrid cloud platform that lets you deliver services from your datacenter.</span><span class="sxs-lookup"><span data-stu-id="a18c2-105">[Microsoft Azure Stack](azure-stack-poc.md) is a hybrid cloud platform that lets you deliver services from your datacenter.</span></span> <span data-ttu-id="a18c2-106">As a service provider, you can offer services to your tenants.</span><span class="sxs-lookup"><span data-stu-id="a18c2-106">As a service provider, you can offer services to your tenants.</span></span> <span data-ttu-id="a18c2-107">Within a business or government agency, you can offer on-premises services to your employees.</span><span class="sxs-lookup"><span data-stu-id="a18c2-107">Within a business or government agency, you can offer on-premises services to your employees.</span></span> <span data-ttu-id="a18c2-108">The services that you can deliver include, but aren't limited to:</span><span class="sxs-lookup"><span data-stu-id="a18c2-108">The services that you can deliver include, but aren't limited to:</span></span>

- <span data-ttu-id="a18c2-109">Platform as a Service (PaaS) services like App Services, API Apps, API Functions, SQL, and MySQL.</span><span class="sxs-lookup"><span data-stu-id="a18c2-109">Platform as a Service (PaaS) services like App Services, API Apps, API Functions, SQL, and MySQL.</span></span>

<span data-ttu-id="a18c2-110">You can even combine services to integrate and build complex solutions for different users.</span><span class="sxs-lookup"><span data-stu-id="a18c2-110">You can even combine services to integrate and build complex solutions for different users.</span></span>

<span data-ttu-id="a18c2-111">To deliver these services to your users, you must create [plans, offers, and quotas](azure-stack-plan-offer-quota-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a18c2-111">To deliver these services to your users, you must create [plans, offers, and quotas](azure-stack-plan-offer-quota-overview.md).</span></span> <span data-ttu-id="a18c2-112">Your users can then subscribe to your offers to use the services.</span><span class="sxs-lookup"><span data-stu-id="a18c2-112">Your users can then subscribe to your offers to use the services.</span></span>

## <a name="plan-your-service-offers"></a><span data-ttu-id="a18c2-113">Plan your service offers</span><span class="sxs-lookup"><span data-stu-id="a18c2-113">Plan your service offers</span></span>

<span data-ttu-id="a18c2-114">When you’re planning your offers, keep the following points in mind:</span><span class="sxs-lookup"><span data-stu-id="a18c2-114">When you’re planning your offers, keep the following points in mind:</span></span>

<span data-ttu-id="a18c2-115">**Trial offers**: You can use trial offers to attract new users, who can then upgrade to additional services.</span><span class="sxs-lookup"><span data-stu-id="a18c2-115">**Trial offers**: You can use trial offers to attract new users, who can then upgrade to additional services.</span></span> <span data-ttu-id="a18c2-116">To create a trial offer, create a small [base plan](azure-stack-plan-offer-quota-overview.md#base-plan) with an optional larger add-on plan.</span><span class="sxs-lookup"><span data-stu-id="a18c2-116">To create a trial offer, create a small [base plan](azure-stack-plan-offer-quota-overview.md#base-plan) with an optional larger add-on plan.</span></span>

<span data-ttu-id="a18c2-117">**Capacity planning**: You might be concerned about users that grab large amounts of resources and clogging the system for all users.</span><span class="sxs-lookup"><span data-stu-id="a18c2-117">**Capacity planning**: You might be concerned about users that grab large amounts of resources and clogging the system for all users.</span></span> <span data-ttu-id="a18c2-118">To help performance, you can [configure your plans with quotas](azure-stack-plan-offer-quota-overview.md#plans) to cap usage.</span><span class="sxs-lookup"><span data-stu-id="a18c2-118">To help performance, you can [configure your plans with quotas](azure-stack-plan-offer-quota-overview.md#plans) to cap usage.</span></span>

<span data-ttu-id="a18c2-119">**Delegated providers**: You can grant others the ability to create offers in your environment.</span><span class="sxs-lookup"><span data-stu-id="a18c2-119">**Delegated providers**: You can grant others the ability to create offers in your environment.</span></span> <span data-ttu-id="a18c2-120">For example, if you’re a service provider, you can [delegate](azure-stack-delegated-provider.md) this ability to your resellers.</span><span class="sxs-lookup"><span data-stu-id="a18c2-120">For example, if you’re a service provider, you can [delegate](azure-stack-delegated-provider.md) this ability to your resellers.</span></span> <span data-ttu-id="a18c2-121">Or, if you’re an organization, you can delegate to other divisions/subsidiaries.</span><span class="sxs-lookup"><span data-stu-id="a18c2-121">Or, if you’re an organization, you can delegate to other divisions/subsidiaries.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a18c2-122">Next steps</span><span class="sxs-lookup"><span data-stu-id="a18c2-122">Next steps</span></span>

[<span data-ttu-id="a18c2-123">Create an offer in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="a18c2-123">Create an offer in Azure Stack</span></span>](azure-stack-create-offer.md)
