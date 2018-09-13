---
title: Azure Active Directory PoC Playbook Introduction| Microsoft Docs
description: Explore and quickly implement Identity and Access Management scenarios
services: active-directory
keywords: azure active directory, playbook, Proof of Concept, PoC
documentationcenter: ''
author: dstefanMSFT
manager: mtillman
ms.assetid: ''
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/12/2017
ms.author: dstefan
ms.openlocfilehash: 80b7ba9507b85621e7b0623362774edc0c8cc729
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818173"
---
# <a name="azure-active-directory-proof-of-concept-playbook-introduction"></a><span data-ttu-id="d3d2a-104">Azure Active Directory Proof of Concept Playbook: Introduction</span><span class="sxs-lookup"><span data-stu-id="d3d2a-104">Azure Active Directory Proof of Concept Playbook: Introduction</span></span>

<span data-ttu-id="d3d2a-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span><span class="sxs-lookup"><span data-stu-id="d3d2a-105">This article provides guidelines to explore different Azure AD capabilities in a Proof of Concept (PoC).</span></span> <span data-ttu-id="d3d2a-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span><span class="sxs-lookup"><span data-stu-id="d3d2a-106">The intended audience of this document is Identity Architects, IT Professionals, and System Integrators</span></span>

## <a name="how-to-use-this-playbook"></a><span data-ttu-id="d3d2a-107">How to use this Playbook</span><span class="sxs-lookup"><span data-stu-id="d3d2a-107">How to use this Playbook</span></span>

1. <span data-ttu-id="d3d2a-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-108">Use the [Theme](active-directory-playbook-ingredients.md#theme) section and pick the area(s) of interest based on your needs.</span></span>  
2. <span data-ttu-id="d3d2a-109">Scope the PoC by choosing the scenarios that align with your business goals.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-109">Scope the PoC by choosing the scenarios that align with your business goals.</span></span> <span data-ttu-id="d3d2a-110">The shorter the better.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-110">The shorter the better.</span></span> <span data-ttu-id="d3d2a-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-111">We recommend doing it as short and concise as possible to convey the value to the stakeholders while minimizing the complexity to realize it.</span></span>  
3. <span data-ttu-id="d3d2a-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-112">Use the [Implementation](active-directory-playbook-implementation.md) section to understand the scenarios, and what would they mean for your environment.</span></span> <span data-ttu-id="d3d2a-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-113">In each scenario, we describe how to set it up (what we call [Building Blocks](active-directory-playbook-building-blocks.md)), and how to navigate the scenarios.</span></span> 
4. <span data-ttu-id="d3d2a-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-114">Each building block explains the pre-requisites needed, as well as an approximate time to complete.</span></span> <span data-ttu-id="d3d2a-115">This can help you during the planning process.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-115">This can help you during the planning process.</span></span> 
5. <span data-ttu-id="d3d2a-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-116">Based on 1-3 Above, define the [Environment](active-directory-playbook-ingredients.md#environment) in which to execute.</span></span> <span data-ttu-id="d3d2a-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-117">We encourage to strive for a production environment to get a good feel of the experience for your users.</span></span> 
6. <span data-ttu-id="d3d2a-118">When having conflicting requirements, use this helpful tradeoff matrix</span><span class="sxs-lookup"><span data-stu-id="d3d2a-118">When having conflicting requirements, use this helpful tradeoff matrix</span></span> 
   * <span data-ttu-id="d3d2a-119">Theme-centric showing of value</span><span class="sxs-lookup"><span data-stu-id="d3d2a-119">Theme-centric showing of value</span></span>  
   * <span data-ttu-id="d3d2a-120">Smoothness to prepare, to set up, and to execute the scenarios</span><span class="sxs-lookup"><span data-stu-id="d3d2a-120">Smoothness to prepare, to set up, and to execute the scenarios</span></span> 
   * <span data-ttu-id="d3d2a-121">Minimal time to execute the target scenarios</span><span class="sxs-lookup"><span data-stu-id="d3d2a-121">Minimal time to execute the target scenarios</span></span> 
   * <span data-ttu-id="d3d2a-122">As close to production as feasible within your constraints</span><span class="sxs-lookup"><span data-stu-id="d3d2a-122">As close to production as feasible within your constraints</span></span> 

>[!NOTE]
> <span data-ttu-id="d3d2a-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-123">Throughout this article, you will see some specific third party applications and products mentioned as examples for convenience.</span></span> <span data-ttu-id="d3d2a-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span><span class="sxs-lookup"><span data-stu-id="d3d2a-124">Azure AD supports thousands of applications in our [application gallery](https://azuremarketplace.microsoft.com/marketplace/apps/category/azure-active-directory-apps) that you can use based on your needs and environment.</span></span> 



[!INCLUDE [active-directory-playbook-toc](../../includes/active-directory-playbook-steps.md)]