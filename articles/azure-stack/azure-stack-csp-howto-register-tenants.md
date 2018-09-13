---
title: Add tenants for usage and billing to Azure Stack | Microsoft Docs
description: The steps required add an end user to Azure Stack managed by a Cloud Service Provider (CSP).
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2018
ms.author: brenduns
ms.reviewer: alfredo
ms.openlocfilehash: d3fc3ef6c5fdcf5a87c691c73169ef2bec95805e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871053"
---
# <a name="add-tenant-for-usage-and-billing-to-azure-stack"></a><span data-ttu-id="05744-103">Add tenant for usage and billing to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="05744-103">Add tenant for usage and billing to Azure Stack</span></span>

<span data-ttu-id="05744-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="05744-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="05744-105">This article describes the steps required add an end user to Azure Stack managed by a Cloud Service Provider (CSP).</span><span class="sxs-lookup"><span data-stu-id="05744-105">This article describes the steps required add an end user to Azure Stack managed by a Cloud Service Provider (CSP).</span></span> <span data-ttu-id="05744-106">When the new tenant uses resources, Azure Stack will report usage to their CSP subscription.</span><span class="sxs-lookup"><span data-stu-id="05744-106">When the new tenant uses resources, Azure Stack will report usage to their CSP subscription.</span></span>

<span data-ttu-id="05744-107">CSPs often offer services to multiple end customers (tenants) on their Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="05744-107">CSPs often offer services to multiple end customers (tenants) on their Azure Stack deployment.</span></span> <span data-ttu-id="05744-108">Adding tenants to the Azure Stack registration ensures that each tenant’s usage will be reported and billed to the corresponding CSP subscription.</span><span class="sxs-lookup"><span data-stu-id="05744-108">Adding tenants to the Azure Stack registration ensures that each tenant’s usage will be reported and billed to the corresponding CSP subscription.</span></span> <span data-ttu-id="05744-109">If you do not complete the steps in this article, tenant usage is charged to the subscription used in the initial registration of Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="05744-109">If you do not complete the steps in this article, tenant usage is charged to the subscription used in the initial registration of Azure Stack.</span></span> <span data-ttu-id="05744-110">Before you can add an end customer to Azure Stack for usage tracking and to manage their tenant, you will need to configure Azure Stack as a CSP.</span><span class="sxs-lookup"><span data-stu-id="05744-110">Before you can add an end customer to Azure Stack for usage tracking and to manage their tenant, you will need to configure Azure Stack as a CSP.</span></span> <span data-ttu-id="05744-111">For steps and resources, see [Manage usage and billing for Azure Stack as a Cloud Service Provider](azure-stack-add-manage-billing-as-a-csp.md).</span><span class="sxs-lookup"><span data-stu-id="05744-111">For steps and resources, see [Manage usage and billing for Azure Stack as a Cloud Service Provider](azure-stack-add-manage-billing-as-a-csp.md).</span></span>

<span data-ttu-id="05744-112">The following diagram shows the steps that a CSP will need to follow to enable a new customer to use Azure Stack, and to set up usage tracking for the customer.</span><span class="sxs-lookup"><span data-stu-id="05744-112">The following diagram shows the steps that a CSP will need to follow to enable a new customer to use Azure Stack, and to set up usage tracking for the customer.</span></span> <span data-ttu-id="05744-113">By adding the end customer, you will also be to manage resources in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="05744-113">By adding the end customer, you will also be to manage resources in Azure Stack.</span></span> <span data-ttu-id="05744-114">You have two options for managing their resources:</span><span class="sxs-lookup"><span data-stu-id="05744-114">You have two options for managing their resources:</span></span>

1. <span data-ttu-id="05744-115">You can maintain the end customer and provide credentials to the local Azure Stack subscription to the end customer.</span><span class="sxs-lookup"><span data-stu-id="05744-115">You can maintain the end customer and provide credentials to the local Azure Stack subscription to the end customer.</span></span>  
2. <span data-ttu-id="05744-116">Or the end customer can work with their subscription locally and add the CSP as a guest with owner permissions.</span><span class="sxs-lookup"><span data-stu-id="05744-116">Or the end customer can work with their subscription locally and add the CSP as a guest with owner permissions.</span></span>  

<span data-ttu-id="05744-117">**Steps to add an end customer**</span><span class="sxs-lookup"><span data-stu-id="05744-117">**Steps to add an end customer**</span></span>

![Set up Cloud Service Provider for usage tracking and to manage the end customer account](media\azure-stack-csp-enable-billing-usage-tracking\process-csp-enable-billing.png)

## <a name="create-a-new-customer-in-partner-center"></a><span data-ttu-id="05744-119">Create a new customer in Partner Center</span><span class="sxs-lookup"><span data-stu-id="05744-119">Create a new customer in Partner Center</span></span>

<span data-ttu-id="05744-120">In Partner Center, create a new Azure subscription for the customer.</span><span class="sxs-lookup"><span data-stu-id="05744-120">In Partner Center, create a new Azure subscription for the customer.</span></span> <span data-ttu-id="05744-121">For instructions, see [Add a new customer](https://msdn.microsoft.com/partner-center/add-a-new-customer).</span><span class="sxs-lookup"><span data-stu-id="05744-121">For instructions, see [Add a new customer](https://msdn.microsoft.com/partner-center/add-a-new-customer).</span></span>


##  <a name="create-an-azure-subscription-for-the-end-customer"></a><span data-ttu-id="05744-122">Create an Azure subscription for the end customer</span><span class="sxs-lookup"><span data-stu-id="05744-122">Create an Azure subscription for the end customer</span></span>

<span data-ttu-id="05744-123">After you've created a record of your customer in Partner Center, you can sell them subscriptions to products in the catalog.</span><span class="sxs-lookup"><span data-stu-id="05744-123">After you've created a record of your customer in Partner Center, you can sell them subscriptions to products in the catalog.</span></span> <span data-ttu-id="05744-124">For instructions, see [Create, suspend, or cancel customer subscriptions](https://msdn.microsoft.com/partner-center/create-a-new-subscription).</span><span class="sxs-lookup"><span data-stu-id="05744-124">For instructions, see [Create, suspend, or cancel customer subscriptions](https://msdn.microsoft.com/partner-center/create-a-new-subscription).</span></span>

## <a name="create-a-guest-user-in-the-end-customer-directory"></a><span data-ttu-id="05744-125">Create a guest user in the end customer directory</span><span class="sxs-lookup"><span data-stu-id="05744-125">Create a guest user in the end customer directory</span></span>

<span data-ttu-id="05744-126">If the end customer will manage their own account, create a guest user in their directory, and send them the information.</span><span class="sxs-lookup"><span data-stu-id="05744-126">If the end customer will manage their own account, create a guest user in their directory, and send them the information.</span></span> <span data-ttu-id="05744-127">The end user will then add the guest and elevate the guest permission to **Owner** to the Azure Stack CSP account.</span><span class="sxs-lookup"><span data-stu-id="05744-127">The end user will then add the guest and elevate the guest permission to **Owner** to the Azure Stack CSP account.</span></span>
 
## <a name="update-the-registration-with-the-end-customer-subscription"></a><span data-ttu-id="05744-128">Update the registration with the end customer subscription</span><span class="sxs-lookup"><span data-stu-id="05744-128">Update the registration with the end customer subscription</span></span>

<span data-ttu-id="05744-129">Update your registration with the new customer’s subscription.</span><span class="sxs-lookup"><span data-stu-id="05744-129">Update your registration with the new customer’s subscription.</span></span> <span data-ttu-id="05744-130">Azure reports the customer's usage using the customer identity from Partner Central.</span><span class="sxs-lookup"><span data-stu-id="05744-130">Azure reports the customer's usage using the customer identity from Partner Central.</span></span> <span data-ttu-id="05744-131">This step ensures that each customer’s usage is reported under that customer’s individual CSP subscription.</span><span class="sxs-lookup"><span data-stu-id="05744-131">This step ensures that each customer’s usage is reported under that customer’s individual CSP subscription.</span></span> <span data-ttu-id="05744-132">This makes tracking user usage and billing much easier.</span><span class="sxs-lookup"><span data-stu-id="05744-132">This makes tracking user usage and billing much easier.</span></span>

> [!Note]  
> <span data-ttu-id="05744-133">To carry out this step, you must have [registered Azure Stack](azure-stack-register.md).</span><span class="sxs-lookup"><span data-stu-id="05744-133">To carry out this step, you must have [registered Azure Stack](azure-stack-register.md).</span></span>

1. <span data-ttu-id="05744-134">Open Windows PowerShell with an elevated prompt, and run:</span><span class="sxs-lookup"><span data-stu-id="05744-134">Open Windows PowerShell with an elevated prompt, and run:</span></span>  
    `Add-AzureRmAccount`
2. <span data-ttu-id="05744-135">Type your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="05744-135">Type your Azure credentials.</span></span>
3. <span data-ttu-id="05744-136">In the PowerShell session, run:</span><span class="sxs-lookup"><span data-stu-id="05744-136">In the PowerShell session, run:</span></span>

```powershell
    New-AzureRmResource -ResourceId "subscriptions/{registrationSubscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionId}" -ApiVersion 2017-06-01 -Properties <PSObject>
```
### <a name="new-azurermresource-powershell-parameters"></a><span data-ttu-id="05744-137">New-AzureRmResource PowerShell parameters</span><span class="sxs-lookup"><span data-stu-id="05744-137">New-AzureRmResource PowerShell parameters</span></span>
| <span data-ttu-id="05744-138">Parameter</span><span class="sxs-lookup"><span data-stu-id="05744-138">Parameter</span></span> | <span data-ttu-id="05744-139">Description</span><span class="sxs-lookup"><span data-stu-id="05744-139">Description</span></span> |
| --- | --- | 
|<span data-ttu-id="05744-140">registrationSubscriptionID</span><span class="sxs-lookup"><span data-stu-id="05744-140">registrationSubscriptionID</span></span> | <span data-ttu-id="05744-141">The Azure subscription that was used for the initial registration of the Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="05744-141">The Azure subscription that was used for the initial registration of the Azure Stack.</span></span> |
| <span data-ttu-id="05744-142">customerSubscriptionID</span><span class="sxs-lookup"><span data-stu-id="05744-142">customerSubscriptionID</span></span> | <span data-ttu-id="05744-143">The Azure subscription (not Azure Stack) belonging to the customer to be registered.</span><span class="sxs-lookup"><span data-stu-id="05744-143">The Azure subscription (not Azure Stack) belonging to the customer to be registered.</span></span> <span data-ttu-id="05744-144">Must be created in the CSP offer; in practice, this means through Partner Center.</span><span class="sxs-lookup"><span data-stu-id="05744-144">Must be created in the CSP offer; in practice, this means through Partner Center.</span></span> <span data-ttu-id="05744-145">If a customer has more than one Azure Active Directory tenant, this subscription must be created in the tenant that will be used to log into Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="05744-145">If a customer has more than one Azure Active Directory tenant, this subscription must be created in the tenant that will be used to log into Azure Stack.</span></span>
| <span data-ttu-id="05744-146">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="05744-146">resourceGroup</span></span> | <span data-ttu-id="05744-147">The resource group in Azure in which your registration is stored.</span><span class="sxs-lookup"><span data-stu-id="05744-147">The resource group in Azure in which your registration is stored.</span></span> 
| <span data-ttu-id="05744-148">registrationName</span><span class="sxs-lookup"><span data-stu-id="05744-148">registrationName</span></span> | <span data-ttu-id="05744-149">The name of the registration of your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="05744-149">The name of the registration of your Azure Stack.</span></span> <span data-ttu-id="05744-150">It is an object stored in Azure.</span><span class="sxs-lookup"><span data-stu-id="05744-150">It is an object stored in Azure.</span></span> | 
| <span data-ttu-id="05744-151">Properties</span><span class="sxs-lookup"><span data-stu-id="05744-151">Properties</span></span> | <span data-ttu-id="05744-152">Specifies properties for the resource.</span><span class="sxs-lookup"><span data-stu-id="05744-152">Specifies properties for the resource.</span></span> <span data-ttu-id="05744-153">Use this parameter to specify the values of properties that are specific to the resource type.</span><span class="sxs-lookup"><span data-stu-id="05744-153">Use this parameter to specify the values of properties that are specific to the resource type.</span></span>


> [!Note]  
> <span data-ttu-id="05744-154">Tenants need to be registered with each Azure Stack they use.</span><span class="sxs-lookup"><span data-stu-id="05744-154">Tenants need to be registered with each Azure Stack they use.</span></span> <span data-ttu-id="05744-155">If you have two Azure Stack deployments, and a tenant is going to use both of them,  you need to update the initial registrations of each deployment with the tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="05744-155">If you have two Azure Stack deployments, and a tenant is going to use both of them,  you need to update the initial registrations of each deployment with the tenant subscription.</span></span>

## <a name="onboard-tenant-to-azure-stack"></a><span data-ttu-id="05744-156">Onboard tenant to Azure Stack</span><span class="sxs-lookup"><span data-stu-id="05744-156">Onboard tenant to Azure Stack</span></span>

<span data-ttu-id="05744-157">Configure Azure Stack to support users from multiple Azure AD tenants to use services in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="05744-157">Configure Azure Stack to support users from multiple Azure AD tenants to use services in Azure Stack.</span></span> <span data-ttu-id="05744-158">For instructions, see [Enable multi-tenancy in Azure Stack](azure-stack-enable-multitenancy.md).</span><span class="sxs-lookup"><span data-stu-id="05744-158">For instructions, see [Enable multi-tenancy in Azure Stack](azure-stack-enable-multitenancy.md).</span></span>


## <a name="create-a-local-resource-in-the-end-customer-tenant-in-azure-stack"></a><span data-ttu-id="05744-159">Create a local resource in the end customer tenant in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="05744-159">Create a local resource in the end customer tenant in Azure Stack</span></span>

<span data-ttu-id="05744-160">Once you have added the new customer to Azure Stack, or the end customer tenant has enabled your guest account with owner privileges, verify that you can create a resource in their tenant.</span><span class="sxs-lookup"><span data-stu-id="05744-160">Once you have added the new customer to Azure Stack, or the end customer tenant has enabled your guest account with owner privileges, verify that you can create a resource in their tenant.</span></span> <span data-ttu-id="05744-161">For example, they can [Create a Windows virtual machine with the Azure Stack portal](user\azure-stack-quick-windows-portal.md).</span><span class="sxs-lookup"><span data-stu-id="05744-161">For example, they can [Create a Windows virtual machine with the Azure Stack portal](user\azure-stack-quick-windows-portal.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="05744-162">Next steps</span><span class="sxs-lookup"><span data-stu-id="05744-162">Next steps</span></span>

 - <span data-ttu-id="05744-163">To review the error messages if they are triggered in your registration process, see [Tenant registration error messages](azure-stack-csp-ref-infrastructure.md#usage-and-billing-error-codes).</span><span class="sxs-lookup"><span data-stu-id="05744-163">To review the error messages if they are triggered in your registration process, see [Tenant registration error messages](azure-stack-csp-ref-infrastructure.md#usage-and-billing-error-codes).</span></span>
 - <span data-ttu-id="05744-164">To learn more about how to retrieve resource usage information from Azure Stack, see [Usage and billing in Azure Stack](azure-stack-billing-and-chargeback.md).</span><span class="sxs-lookup"><span data-stu-id="05744-164">To learn more about how to retrieve resource usage information from Azure Stack, see [Usage and billing in Azure Stack](azure-stack-billing-and-chargeback.md).</span></span>
 - <span data-ttu-id="05744-165">To review how an end customer may add you, as the CSP, as the manager for their Azure Stack, tenant, see [Enable a Cloud Service Provider to manage your Azure Stack subscription](user\azure-stack-csp-enable-billing-usage-tracking.md).</span><span class="sxs-lookup"><span data-stu-id="05744-165">To review how an end customer may add you, as the CSP, as the manager for their Azure Stack, tenant, see [Enable a Cloud Service Provider to manage your Azure Stack subscription](user\azure-stack-csp-enable-billing-usage-tracking.md).</span></span>
