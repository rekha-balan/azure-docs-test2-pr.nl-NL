---
title: Using the administrator and user portals in Azure Stack | Microsoft Docs
description: Learn the differences between the administrator and user portals in Azure Stack.
services: azure-stack
documentationcenter: ''
author: twooley
manager: byronr
editor: ''
ms.assetid: 02c7ff03-874e-4951-b591-28166b7a7a79
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: twooley
ms.openlocfilehash: 681dce70ecce6717159089de70c2e2132fda8b10
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552581"
---
# <a name="using-the-administrator-and-user-portals-in-azure-stack"></a><span data-ttu-id="3b8c9-103">Using the administrator and user portals in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3b8c9-103">Using the administrator and user portals in Azure Stack</span></span>

<span data-ttu-id="3b8c9-104">Starting with the Technical Preview 3 (TP3) release of Azure Stack, there are two portals; the administrator portal and the user portal (also referred to as the *tenant* portal).</span><span class="sxs-lookup"><span data-stu-id="3b8c9-104">Starting with the Technical Preview 3 (TP3) release of Azure Stack, there are two portals; the administrator portal and the user portal (also referred to as the *tenant* portal).</span></span> <span data-ttu-id="3b8c9-105">The portals are backed by separate instances of Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-105">The portals are backed by separate instances of Azure Resource Manager.</span></span>

<span data-ttu-id="3b8c9-106">The following table shows how to connect to the portals and to Resource Manager endpoints in an Azure Stack Proof of Concept (POC) environment.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-106">The following table shows how to connect to the portals and to Resource Manager endpoints in an Azure Stack Proof of Concept (POC) environment.</span></span>

|  <span data-ttu-id="3b8c9-107">Portal</span><span class="sxs-lookup"><span data-stu-id="3b8c9-107">Portal</span></span> | <span data-ttu-id="3b8c9-108">Portal URL</span><span class="sxs-lookup"><span data-stu-id="3b8c9-108">Portal URL</span></span> | <span data-ttu-id="3b8c9-109">Resource Manager endpoint URL</span><span class="sxs-lookup"><span data-stu-id="3b8c9-109">Resource Manager endpoint URL</span></span> |   
| -------- | ------------- | ------- |  
| <span data-ttu-id="3b8c9-110">Administrator</span><span class="sxs-lookup"><span data-stu-id="3b8c9-110">Administrator</span></span> | https://adminportal.local.azurestack.external  | https://adminmanagement.local.azurestack.external  |  
| <span data-ttu-id="3b8c9-111">User</span><span class="sxs-lookup"><span data-stu-id="3b8c9-111">User</span></span> | https://portal.local.azurestack.external | https://management.local.azurestack.external  |
| | |

>[!NOTE]
 <span data-ttu-id="3b8c9-112">These URLs were updated in the latest release of TP3.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-112">These URLs were updated in the latest release of TP3.</span></span> <span data-ttu-id="3b8c9-113">Previously, they were https://portal.local.azurestack.external and https://api.local.azurestack.external for administrator, and https://publicportal.local.azurestack.external and https://publicapi.local.azurestack.external for user.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-113">Previously, they were https://portal.local.azurestack.external and https://api.local.azurestack.external for administrator, and https://publicportal.local.azurestack.external and https://publicapi.local.azurestack.external for user.</span></span>


## <a name="the-administrator-portal"></a><span data-ttu-id="3b8c9-114">The administrator portal</span><span class="sxs-lookup"><span data-stu-id="3b8c9-114">The administrator portal</span></span>

<span data-ttu-id="3b8c9-115">The administrator portal enables a cloud administrator to perform administrative tasks.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-115">The administrator portal enables a cloud administrator to perform administrative tasks.</span></span> <span data-ttu-id="3b8c9-116">An administrator can do things such as:</span><span class="sxs-lookup"><span data-stu-id="3b8c9-116">An administrator can do things such as:</span></span>
* <span data-ttu-id="3b8c9-117">monitor health and alerts</span><span class="sxs-lookup"><span data-stu-id="3b8c9-117">monitor health and alerts</span></span>
* <span data-ttu-id="3b8c9-118">manage capacity</span><span class="sxs-lookup"><span data-stu-id="3b8c9-118">manage capacity</span></span>
* <span data-ttu-id="3b8c9-119">populate the marketplace</span><span class="sxs-lookup"><span data-stu-id="3b8c9-119">populate the marketplace</span></span>
* <span data-ttu-id="3b8c9-120">create plans and offers</span><span class="sxs-lookup"><span data-stu-id="3b8c9-120">create plans and offers</span></span>
* <span data-ttu-id="3b8c9-121">create subscriptions for tenant users</span><span class="sxs-lookup"><span data-stu-id="3b8c9-121">create subscriptions for tenant users</span></span>

<span data-ttu-id="3b8c9-122">An administrator can also create resources such as virtual machines, virtual networks, and storage accounts.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-122">An administrator can also create resources such as virtual machines, virtual networks, and storage accounts.</span></span>

 ![The administrator portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-portals/image1.PNG)

 ## <a name="the-user-portal"></a><span data-ttu-id="3b8c9-124">The user portal</span><span class="sxs-lookup"><span data-stu-id="3b8c9-124">The user portal</span></span>

 <span data-ttu-id="3b8c9-125">The user portal does not provide access to any of the administrative capabilities of the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-125">The user portal does not provide access to any of the administrative capabilities of the administrator portal.</span></span> <span data-ttu-id="3b8c9-126">In the user portal, a user can subscribe to public offers, and use the services that are made available through those offers.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-126">In the user portal, a user can subscribe to public offers, and use the services that are made available through those offers.</span></span>

  ![The user portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-manage-portals/image2.PNG)
 
 ## <a name="subscription-behavior"></a><span data-ttu-id="3b8c9-128">Subscription behavior</span><span class="sxs-lookup"><span data-stu-id="3b8c9-128">Subscription behavior</span></span>
 
 <span data-ttu-id="3b8c9-129">Make sure that you understand the following differences between subscription behavior in the two portals.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-129">Make sure that you understand the following differences between subscription behavior in the two portals.</span></span>

 <span data-ttu-id="3b8c9-130">Administrator portal:</span><span class="sxs-lookup"><span data-stu-id="3b8c9-130">Administrator portal:</span></span>
* <span data-ttu-id="3b8c9-131">There is only one subscription that is available in the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-131">There is only one subscription that is available in the administrator portal.</span></span> <span data-ttu-id="3b8c9-132">This subscription is the *Default Provider Subscription*.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-132">This subscription is the *Default Provider Subscription*.</span></span> <span data-ttu-id="3b8c9-133">You can't add any other subscriptions for use in the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-133">You can't add any other subscriptions for use in the administrator portal.</span></span>
* <span data-ttu-id="3b8c9-134">As a cloud administrator, you can add subscriptions for your users (including yourself) from the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-134">As a cloud administrator, you can add subscriptions for your users (including yourself) from the administrator portal.</span></span> <span data-ttu-id="3b8c9-135">Users (including yourself) can access and use these subscriptions from the user portal.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-135">Users (including yourself) can access and use these subscriptions from the user portal.</span></span>

  >[!NOTE]
  <span data-ttu-id="3b8c9-136">Because of the Azure Resource Manager separation, subscriptions do not cross portals.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-136">Because of the Azure Resource Manager separation, subscriptions do not cross portals.</span></span> <span data-ttu-id="3b8c9-137">For example, if you as a cloud administrator signs in to the user portal, you can't access the Default Provider Subscription.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-137">For example, if you as a cloud administrator signs in to the user portal, you can't access the Default Provider Subscription.</span></span> <span data-ttu-id="3b8c9-138">Therefore, you don't have access to any administrative functions.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-138">Therefore, you don't have access to any administrative functions.</span></span> <span data-ttu-id="3b8c9-139">You can create subscriptions for yourself from public offers, but you are considered a tenant user.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-139">You can create subscriptions for yourself from public offers, but you are considered a tenant user.</span></span>

<span data-ttu-id="3b8c9-140">User portal:</span><span class="sxs-lookup"><span data-stu-id="3b8c9-140">User portal:</span></span>
* <span data-ttu-id="3b8c9-141">In the user portal, an account can have multiple subscriptions.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-141">In the user portal, an account can have multiple subscriptions.</span></span>

  >[!NOTE]
  <span data-ttu-id="3b8c9-142">In the POC environment, if a tenant user belongs to the same directory as the cloud administrator, they are not blocked from signing in to the administrator portal.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-142">In the POC environment, if a tenant user belongs to the same directory as the cloud administrator, they are not blocked from signing in to the administrator portal.</span></span> <span data-ttu-id="3b8c9-143">However, they can't access any of the administrative functions.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-143">However, they can't access any of the administrative functions.</span></span> <span data-ttu-id="3b8c9-144">Also, they can't add subscriptions or access offers that are made available to them in the user portal.</span><span class="sxs-lookup"><span data-stu-id="3b8c9-144">Also, they can't add subscriptions or access offers that are made available to them in the user portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3b8c9-145">Next steps</span><span class="sxs-lookup"><span data-stu-id="3b8c9-145">Next steps</span></span>

[<span data-ttu-id="3b8c9-146">Connect to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3b8c9-146">Connect to Azure Stack</span></span>](azure-stack-connect-azure-stack.md)

[<span data-ttu-id="3b8c9-147">Region management in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="3b8c9-147">Region management in Azure Stack</span></span>](azure-stack-region-management.md)


