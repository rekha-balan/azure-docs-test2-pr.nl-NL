---
title: Manage usage and billing for Azure Stack as a Cloud Service Provider | Microsoft Docs
description: A walk through registering Azure Stack as a Cloud Provider (CSP) and adding customers for billing.
services: azure-stack
documentationcenter: ''
author: brenduns
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/30/2018
ms.author: brenduns
ms.reviewer: alfredo
ms.openlocfilehash: 9bb4a4ea81f2dc0fb11e2f7cae1b9d02b0edfdde
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869744"
---
# <a name="manage-usage-and-billing-for-azure-stack-as-a-cloud-service-provider"></a><span data-ttu-id="8498e-103">Manage usage and billing for Azure Stack as a Cloud Service Provider</span><span class="sxs-lookup"><span data-stu-id="8498e-103">Manage usage and billing for Azure Stack as a Cloud Service Provider</span></span> 

<span data-ttu-id="8498e-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="8498e-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="8498e-105">This article walks you through registering Azure Stack as a Cloud Provider (CSP) and adding customers.</span><span class="sxs-lookup"><span data-stu-id="8498e-105">This article walks you through registering Azure Stack as a Cloud Provider (CSP) and adding customers.</span></span>

<span data-ttu-id="8498e-106">As a CSP you work with diverse customers using your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8498e-106">As a CSP you work with diverse customers using your Azure Stack.</span></span> <span data-ttu-id="8498e-107">Each customer has a CSP subscription in Azure.</span><span class="sxs-lookup"><span data-stu-id="8498e-107">Each customer has a CSP subscription in Azure.</span></span> <span data-ttu-id="8498e-108">You'll need to direct usage from your Azure Stack to each user subscription.</span><span class="sxs-lookup"><span data-stu-id="8498e-108">You'll need to direct usage from your Azure Stack to each user subscription.</span></span>

<span data-ttu-id="8498e-109">The following diagram shows the steps that you will need to choose your shared services account and register the Azure account with the Azure Stack account.</span><span class="sxs-lookup"><span data-stu-id="8498e-109">The following diagram shows the steps that you will need to choose your shared services account and register the Azure account with the Azure Stack account.</span></span> <span data-ttu-id="8498e-110">Registered, you can onboard your end customers.</span><span class="sxs-lookup"><span data-stu-id="8498e-110">Registered, you can onboard your end customers.</span></span>

<span data-ttu-id="8498e-111">**Steps to add usage tracking as a CSP**</span><span class="sxs-lookup"><span data-stu-id="8498e-111">**Steps to add usage tracking as a CSP**</span></span>

![Process for enabling usage and management as a Cloud Service Provider.](media\azure-stack-add-manage-billing-as-a-csp\process-add-useage-as-a-csp.png)

## <a name="create-a-csp-or-cspss-subscription"></a><span data-ttu-id="8498e-113">Create a CSP or CSPSS subscription</span><span class="sxs-lookup"><span data-stu-id="8498e-113">Create a CSP or CSPSS subscription</span></span>

### <a name="cloud-service-provider-subscription-types"></a><span data-ttu-id="8498e-114">Cloud Service Provider subscription types</span><span class="sxs-lookup"><span data-stu-id="8498e-114">Cloud Service Provider subscription types</span></span>

<span data-ttu-id="8498e-115">You will need to choose the type of shared services account that you use for Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8498e-115">You will need to choose the type of shared services account that you use for Azure Stack.</span></span> <span data-ttu-id="8498e-116">The types of subscriptions that can be used for registration of a multitenant Azure Stack are:</span><span class="sxs-lookup"><span data-stu-id="8498e-116">The types of subscriptions that can be used for registration of a multitenant Azure Stack are:</span></span>

 - <span data-ttu-id="8498e-117">Cloud Service Provider</span><span class="sxs-lookup"><span data-stu-id="8498e-117">Cloud Service Provider</span></span> 
 - <span data-ttu-id="8498e-118">Partner Shared Services subscription</span><span class="sxs-lookup"><span data-stu-id="8498e-118">Partner Shared Services subscription</span></span> 

#### <a name="csp-shared-services"></a><span data-ttu-id="8498e-119">CSP Shared Services</span><span class="sxs-lookup"><span data-stu-id="8498e-119">CSP Shared Services</span></span>

<span data-ttu-id="8498e-120">Cloud Service Provider Shared Services (CSPSS) subscriptions are the preferred choice for registration when a Direct CSP or a CSP Distributor operates Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8498e-120">Cloud Service Provider Shared Services (CSPSS) subscriptions are the preferred choice for registration when a Direct CSP or a CSP Distributor operates Azure Stack.</span></span>

<span data-ttu-id="8498e-121">CSPSS subscriptions are associated with a shared-services tenant.</span><span class="sxs-lookup"><span data-stu-id="8498e-121">CSPSS subscriptions are associated with a shared-services tenant.</span></span> <span data-ttu-id="8498e-122">When you register Azure Stack, you need to provide credentials for an account that is an owner of the subscription.</span><span class="sxs-lookup"><span data-stu-id="8498e-122">When you register Azure Stack, you need to provide credentials for an account that is an owner of the subscription.</span></span> <span data-ttu-id="8498e-123">The account you use to register Azure Stack can be different from the administrator account that you use for deployment.</span><span class="sxs-lookup"><span data-stu-id="8498e-123">The account you use to register Azure Stack can be different from the administrator account that you use for deployment.</span></span> <span data-ttu-id="8498e-124">Furthermore, the two accounts do *not* need to belong to the same domain.</span><span class="sxs-lookup"><span data-stu-id="8498e-124">Furthermore, the two accounts do *not* need to belong to the same domain.</span></span> <span data-ttu-id="8498e-125">In other words, you may deploy using the tenant that you already use.</span><span class="sxs-lookup"><span data-stu-id="8498e-125">In other words, you may deploy using the tenant that you already use.</span></span> <span data-ttu-id="8498e-126">For example you may use ContosoCSP.onmicrosoft.com, then register using a different tenant, for example IURContosoCSP.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="8498e-126">For example you may use ContosoCSP.onmicrosoft.com, then register using a different tenant, for example IURContosoCSP.onmicrosoft.com.</span></span> <span data-ttu-id="8498e-127">You will need to remember that you sign in using ContosoCSP.onmicrosoft.com when you do day-to-do Azure Stack administration.</span><span class="sxs-lookup"><span data-stu-id="8498e-127">You will need to remember that you sign in using ContosoCSP.onmicrosoft.com when you do day-to-do Azure Stack administration.</span></span> <span data-ttu-id="8498e-128">When you sign in to Azure using IURContosoCSP.onmicrosoft.com when you need to do registration operations.</span><span class="sxs-lookup"><span data-stu-id="8498e-128">When you sign in to Azure using IURContosoCSP.onmicrosoft.com when you need to do registration operations.</span></span>

<span data-ttu-id="8498e-129">Refer to the following for a description of CSPSS subscriptions, and instructions on how to create subscription [Add Azure Partner Shared Services](https://msdn.microsoft.com/partner-center/shared-services).</span><span class="sxs-lookup"><span data-stu-id="8498e-129">Refer to the following for a description of CSPSS subscriptions, and instructions on how to create subscription [Add Azure Partner Shared Services](https://msdn.microsoft.com/partner-center/shared-services).</span></span>

#### <a name="csp-subscriptions"></a><span data-ttu-id="8498e-130">CSP subscriptions</span><span class="sxs-lookup"><span data-stu-id="8498e-130">CSP subscriptions</span></span>

<span data-ttu-id="8498e-131">Cloud Service Provider (CSP) subscriptions are the preferred choice for registration when a CSP reseller or an end customer operates  Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8498e-131">Cloud Service Provider (CSP) subscriptions are the preferred choice for registration when a CSP reseller or an end customer operates  Azure Stack.</span></span>

## <a name="register-azure-stack"></a><span data-ttu-id="8498e-132">Register Azure Stack</span><span class="sxs-lookup"><span data-stu-id="8498e-132">Register Azure Stack</span></span>

<span data-ttu-id="8498e-133">Use the CSPSS subscription created following the information in the preceding section to register Azure Stack with Azure.</span><span class="sxs-lookup"><span data-stu-id="8498e-133">Use the CSPSS subscription created following the information in the preceding section to register Azure Stack with Azure.</span></span> <span data-ttu-id="8498e-134">For more information, see [Register Azure Stack with your Azure Subscription](azure-stack-registration.md).</span><span class="sxs-lookup"><span data-stu-id="8498e-134">For more information, see [Register Azure Stack with your Azure Subscription](azure-stack-registration.md).</span></span>

## <a name="add-end-customer"></a><span data-ttu-id="8498e-135">Add end customer</span><span class="sxs-lookup"><span data-stu-id="8498e-135">Add end customer</span></span>

<span data-ttu-id="8498e-136">To configure Azure Stack so that when a new tenant uses resources their usage will be reported to their Cloud Service Provider (CSP) subscription, see [Add tenant for usage and billing to Azure Stack](azure-stack-csp-howto-register-tenants.md).</span><span class="sxs-lookup"><span data-stu-id="8498e-136">To configure Azure Stack so that when a new tenant uses resources their usage will be reported to their Cloud Service Provider (CSP) subscription, see [Add tenant for usage and billing to Azure Stack](azure-stack-csp-howto-register-tenants.md).</span></span>

## <a name="charge-the-right-subscriptions"></a><span data-ttu-id="8498e-137">Charge the right subscriptions</span><span class="sxs-lookup"><span data-stu-id="8498e-137">Charge the right subscriptions</span></span>

<span data-ttu-id="8498e-138">Azure Stack uses a feature called registration.</span><span class="sxs-lookup"><span data-stu-id="8498e-138">Azure Stack uses a feature called registration.</span></span> <span data-ttu-id="8498e-139">A registration is an object stored in Azure.</span><span class="sxs-lookup"><span data-stu-id="8498e-139">A registration is an object stored in Azure.</span></span> <span data-ttu-id="8498e-140">The registration object documents which Azure subscription(s) to use to charge for a given Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8498e-140">The registration object documents which Azure subscription(s) to use to charge for a given Azure Stack.</span></span> <span data-ttu-id="8498e-141">This section addresses the importance of registration.</span><span class="sxs-lookup"><span data-stu-id="8498e-141">This section addresses the importance of registration.</span></span>

<span data-ttu-id="8498e-142">Using registration Azure Stack can:</span><span class="sxs-lookup"><span data-stu-id="8498e-142">Using registration Azure Stack can:</span></span>
 - <span data-ttu-id="8498e-143">Forward Azure Stack usage data to Azure Commerce and bill an Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8498e-143">Forward Azure Stack usage data to Azure Commerce and bill an Azure subscription.</span></span>
 - <span data-ttu-id="8498e-144">Report each customer’s usage on a different subscription with a multitenant Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="8498e-144">Report each customer’s usage on a different subscription with a multitenant Azure Stack deployment.</span></span> <span data-ttu-id="8498e-145">Multitenancy enables Azure Stack to support different organizations on the same Azure Stack instance.</span><span class="sxs-lookup"><span data-stu-id="8498e-145">Multitenancy enables Azure Stack to support different organizations on the same Azure Stack instance.</span></span>

<span data-ttu-id="8498e-146">For each Azure Stack, there is one default subscription and many tenant subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8498e-146">For each Azure Stack, there is one default subscription and many tenant subscriptions.</span></span> <span data-ttu-id="8498e-147">The default subscription is an Azure subscription that is charged if there isn't a tenant-specific subscription.</span><span class="sxs-lookup"><span data-stu-id="8498e-147">The default subscription is an Azure subscription that is charged if there isn't a tenant-specific subscription.</span></span> <span data-ttu-id="8498e-148">It must be the first to subscription registered.</span><span class="sxs-lookup"><span data-stu-id="8498e-148">It must be the first to subscription registered.</span></span> <span data-ttu-id="8498e-149">For multi-tenant usage reporting to work, the subscription must be a CSP or CSPSS subscription.</span><span class="sxs-lookup"><span data-stu-id="8498e-149">For multi-tenant usage reporting to work, the subscription must be a CSP or CSPSS subscription.</span></span>

<span data-ttu-id="8498e-150">Then, the registration is updated with an Azure subscription for each tenant that is going to use Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="8498e-150">Then, the registration is updated with an Azure subscription for each tenant that is going to use Azure Stack.</span></span> <span data-ttu-id="8498e-151">Tenant subscriptions must be of the CSP type and must roll up to the partner who owns the default subscription.</span><span class="sxs-lookup"><span data-stu-id="8498e-151">Tenant subscriptions must be of the CSP type and must roll up to the partner who owns the default subscription.</span></span> <span data-ttu-id="8498e-152">In other words, you cannot register someone else’s customers.</span><span class="sxs-lookup"><span data-stu-id="8498e-152">In other words, you cannot register someone else’s customers.</span></span>

<span data-ttu-id="8498e-153">When Azure Stack forwards usage information to global Azure, a service in Azure consults the registration and maps each tenant’s usage to the appropriate tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="8498e-153">When Azure Stack forwards usage information to global Azure, a service in Azure consults the registration and maps each tenant’s usage to the appropriate tenant subscription.</span></span> <span data-ttu-id="8498e-154">If a tenant has not been registered, that usage goes to the default subscription for the Azure Stack instance from which it originated.</span><span class="sxs-lookup"><span data-stu-id="8498e-154">If a tenant has not been registered, that usage goes to the default subscription for the Azure Stack instance from which it originated.</span></span>

<span data-ttu-id="8498e-155">Since tenant subscriptions are CSP subscriptions, their bill is sent to the CSP partner, and usage information is not visible to the end customer.</span><span class="sxs-lookup"><span data-stu-id="8498e-155">Since tenant subscriptions are CSP subscriptions, their bill is sent to the CSP partner, and usage information is not visible to the end customer.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8498e-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="8498e-156">Next steps</span></span>

 - <span data-ttu-id="8498e-157">To learn more about the CSP program, see [Cloud Solution Provider program](https://partner.microsoft.com/solutions/microsoft-cloud-solutions).</span><span class="sxs-lookup"><span data-stu-id="8498e-157">To learn more about the CSP program, see [Cloud Solution Provider program](https://partner.microsoft.com/solutions/microsoft-cloud-solutions).</span></span>
 - <span data-ttu-id="8498e-158">To learn more about how to retrieve resource usage information from Azure Stack, see [Usage and billing in Azure Stack](azure-stack-billing-and-chargeback.md).</span><span class="sxs-lookup"><span data-stu-id="8498e-158">To learn more about how to retrieve resource usage information from Azure Stack, see [Usage and billing in Azure Stack](azure-stack-billing-and-chargeback.md).</span></span>
