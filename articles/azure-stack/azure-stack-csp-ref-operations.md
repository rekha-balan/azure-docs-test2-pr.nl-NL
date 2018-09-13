---
title: Register tenants for usage tracking in Azure Stack | Microsoft Docs
description: Details about operations used to manage  tenant registrations and how tenant usage is tracked in Azure Stack.
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
ms.date: 06/08/2018
ms.author: brenduns
ms.reviewer: alfredo
ms.openlocfilehash: ce226bb34c5ff8a7ea7dc44d8428da2bb09e25e5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857259"
---
# <a name="manage-tenant-registration-in-azure-stack"></a><span data-ttu-id="fd199-103">Manage tenant registration in Azure Stack</span><span class="sxs-lookup"><span data-stu-id="fd199-103">Manage tenant registration in Azure Stack</span></span>

<span data-ttu-id="fd199-104">*Applies to: Azure Stack integrated systems*</span><span class="sxs-lookup"><span data-stu-id="fd199-104">*Applies to: Azure Stack integrated systems*</span></span>

<span data-ttu-id="fd199-105">This article contains details about operations you can use to manage your tenant registrations, and how tenant usage is tracked.</span><span class="sxs-lookup"><span data-stu-id="fd199-105">This article contains details about operations you can use to manage your tenant registrations, and how tenant usage is tracked.</span></span> <span data-ttu-id="fd199-106">You can find details about how to add, list, or remove tenant mappings.</span><span class="sxs-lookup"><span data-stu-id="fd199-106">You can find details about how to add, list, or remove tenant mappings.</span></span> <span data-ttu-id="fd199-107">You can use PowerShell or the Billing API endpoints to manage your use tracking.</span><span class="sxs-lookup"><span data-stu-id="fd199-107">You can use PowerShell or the Billing API endpoints to manage your use tracking.</span></span>

## <a name="add-tenant-to-registration"></a><span data-ttu-id="fd199-108">Add tenant to registration</span><span class="sxs-lookup"><span data-stu-id="fd199-108">Add tenant to registration</span></span>

<span data-ttu-id="fd199-109">You use this operation when you want to add a new tenant to your registration, so that their usage is reported under an Azure subscription connected with their Azure Active Directory (Azure AD) tenant.</span><span class="sxs-lookup"><span data-stu-id="fd199-109">You use this operation when you want to add a new tenant to your registration, so that their usage is reported under an Azure subscription connected with their Azure Active Directory (Azure AD) tenant.</span></span>

<span data-ttu-id="fd199-110">You can also use this operation if you want to change the subscription associated with a tenant, you can call PUT/New-AzureRMResource again.</span><span class="sxs-lookup"><span data-stu-id="fd199-110">You can also use this operation if you want to change the subscription associated with a tenant, you can call PUT/New-AzureRMResource again.</span></span> <span data-ttu-id="fd199-111">The old mapping is overwritten.</span><span class="sxs-lookup"><span data-stu-id="fd199-111">The old mapping is overwritten.</span></span>

<span data-ttu-id="fd199-112">Note that only one Azure subscription can be associated with a tenant.</span><span class="sxs-lookup"><span data-stu-id="fd199-112">Note that only one Azure subscription can be associated with a tenant.</span></span> <span data-ttu-id="fd199-113">If you try to add a second subscription to an existing tenant, the first subscription is over-written.</span><span class="sxs-lookup"><span data-stu-id="fd199-113">If you try to add a second subscription to an existing tenant, the first subscription is over-written.</span></span> 

### <a name="use-api-profiles"></a><span data-ttu-id="fd199-114">Use API profiles</span><span class="sxs-lookup"><span data-stu-id="fd199-114">Use API profiles</span></span>

<span data-ttu-id="fd199-115">The cmdlets in this article require that you specify an API profile when running PowerShell.</span><span class="sxs-lookup"><span data-stu-id="fd199-115">The cmdlets in this article require that you specify an API profile when running PowerShell.</span></span> <span data-ttu-id="fd199-116">API profiles represent a set of Azure resource providers and their API versions.</span><span class="sxs-lookup"><span data-stu-id="fd199-116">API profiles represent a set of Azure resource providers and their API versions.</span></span> <span data-ttu-id="fd199-117">They help you use the right version of the API when interacting with multiple Azure clouds, for instance when working with global Azure and Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fd199-117">They help you use the right version of the API when interacting with multiple Azure clouds, for instance when working with global Azure and Azure Stack.</span></span> <span data-ttu-id="fd199-118">Profiles are specified by a name that matches their release date.</span><span class="sxs-lookup"><span data-stu-id="fd199-118">Profiles are specified by a name that matches their release date.</span></span> <span data-ttu-id="fd199-119">With this article, you will need to use the **2017-09-03** profile.</span><span class="sxs-lookup"><span data-stu-id="fd199-119">With this article, you will need to use the **2017-09-03** profile.</span></span>

<span data-ttu-id="fd199-120">For more information about Azure Stack and API Profiles, see [Manage API version profiles in Azure Stack](user/azure-stack-version-profiles.md).</span><span class="sxs-lookup"><span data-stu-id="fd199-120">For more information about Azure Stack and API Profiles, see [Manage API version profiles in Azure Stack](user/azure-stack-version-profiles.md).</span></span> <span data-ttu-id="fd199-121">For instructions on getting up and running with API Profile with PowerShell, see [Use API version profiles for PowerShell in Azure Stack](user/azure-stack-version-profiles-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="fd199-121">For instructions on getting up and running with API Profile with PowerShell, see [Use API version profiles for PowerShell in Azure Stack](user/azure-stack-version-profiles-powershell.md).</span></span>

### <a name="parameters"></a><span data-ttu-id="fd199-122">Parameters</span><span class="sxs-lookup"><span data-stu-id="fd199-122">Parameters</span></span>

| <span data-ttu-id="fd199-123">Parameter</span><span class="sxs-lookup"><span data-stu-id="fd199-123">Parameter</span></span>                  | <span data-ttu-id="fd199-124">Description</span><span class="sxs-lookup"><span data-stu-id="fd199-124">Description</span></span> |
|---                         | --- |
| <span data-ttu-id="fd199-125">registrationSubscriptionID</span><span class="sxs-lookup"><span data-stu-id="fd199-125">registrationSubscriptionID</span></span> | <span data-ttu-id="fd199-126">The Azure subscription that was used for the initial registration.</span><span class="sxs-lookup"><span data-stu-id="fd199-126">The Azure subscription that was used for the initial registration.</span></span> |
| <span data-ttu-id="fd199-127">customerSubscriptionID</span><span class="sxs-lookup"><span data-stu-id="fd199-127">customerSubscriptionID</span></span>     | <span data-ttu-id="fd199-128">The  Azure subscription (not Azure Stack) belonging to the customer to be registered.</span><span class="sxs-lookup"><span data-stu-id="fd199-128">The  Azure subscription (not Azure Stack) belonging to the customer to be registered.</span></span> <span data-ttu-id="fd199-129">Must be created in the Cloud Service Provider (CSP) offer.</span><span class="sxs-lookup"><span data-stu-id="fd199-129">Must be created in the Cloud Service Provider (CSP) offer.</span></span> <span data-ttu-id="fd199-130">In practice, this means through Partner Center.</span><span class="sxs-lookup"><span data-stu-id="fd199-130">In practice, this means through Partner Center.</span></span> <span data-ttu-id="fd199-131">If a customer has more than one tenant, this subscription must be created in the tenant that will be used to log into Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fd199-131">If a customer has more than one tenant, this subscription must be created in the tenant that will be used to log into Azure Stack.</span></span> |
| <span data-ttu-id="fd199-132">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="fd199-132">resourceGroup</span></span>              | <span data-ttu-id="fd199-133">The resource group in Azure in which your registration is stored.</span><span class="sxs-lookup"><span data-stu-id="fd199-133">The resource group in Azure in which your registration is stored.</span></span> |
| <span data-ttu-id="fd199-134">registrationName</span><span class="sxs-lookup"><span data-stu-id="fd199-134">registrationName</span></span>           | <span data-ttu-id="fd199-135">The name of the registration of your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fd199-135">The name of the registration of your Azure Stack.</span></span> <span data-ttu-id="fd199-136">It is an object stored in Azure.</span><span class="sxs-lookup"><span data-stu-id="fd199-136">It is an object stored in Azure.</span></span> <span data-ttu-id="fd199-137">The name is usually in the form azurestack-CloudID, where CloudID is the Cloud ID of your Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="fd199-137">The name is usually in the form azurestack-CloudID, where CloudID is the Cloud ID of your Azure Stack deployment.</span></span> |

> [!Note]  
> <span data-ttu-id="fd199-138">Tenants need to be registered with each Azure Stack they use.</span><span class="sxs-lookup"><span data-stu-id="fd199-138">Tenants need to be registered with each Azure Stack they use.</span></span> <span data-ttu-id="fd199-139">If a tenant uses more than one Azure Stack, you need to update the initial registrations of each deployment with the tenant subscription.</span><span class="sxs-lookup"><span data-stu-id="fd199-139">If a tenant uses more than one Azure Stack, you need to update the initial registrations of each deployment with the tenant subscription.</span></span>

### <a name="powershell"></a><span data-ttu-id="fd199-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd199-140">PowerShell</span></span>

<span data-ttu-id="fd199-141">Use the New-AzureRmResource cmdlet to update the registration resource.</span><span class="sxs-lookup"><span data-stu-id="fd199-141">Use the New-AzureRmResource cmdlet to update the registration resource.</span></span> <span data-ttu-id="fd199-142">Sign in to Azure (`Add-AzureRmAccount`) using the account you used for the initial registration.</span><span class="sxs-lookup"><span data-stu-id="fd199-142">Sign in to Azure (`Add-AzureRmAccount`) using the account you used for the initial registration.</span></span> <span data-ttu-id="fd199-143">Here is an example of how to add a tenant:</span><span class="sxs-lookup"><span data-stu-id="fd199-143">Here is an example of how to add a tenant:</span></span>

```powershell
  New-AzureRmResource -ResourceId "subscriptions/{registrationSubscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionId}" -ApiVersion 2017-06-01 -Properties
```

### <a name="api-call"></a><span data-ttu-id="fd199-144">API call</span><span class="sxs-lookup"><span data-stu-id="fd199-144">API call</span></span>

<span data-ttu-id="fd199-145">**Operation**: PUT</span><span class="sxs-lookup"><span data-stu-id="fd199-145">**Operation**: PUT</span></span>  
<span data-ttu-id="fd199-146">**RequestURI**: `subscriptions/{registrationSubscriptionId}/resourceGroups/{resourceGroup}  /providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/  
{customerSubscriptionId}?api-version=2017-06-01 HTTP/1.1`</span><span class="sxs-lookup"><span data-stu-id="fd199-146">**RequestURI**: `subscriptions/{registrationSubscriptionId}/resourceGroups/{resourceGroup}  /providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/  
{customerSubscriptionId}?api-version=2017-06-01 HTTP/1.1`</span></span>  
<span data-ttu-id="fd199-147">**Response**: 201 Created</span><span class="sxs-lookup"><span data-stu-id="fd199-147">**Response**: 201 Created</span></span>  
<span data-ttu-id="fd199-148">**Response Body**: Empty</span><span class="sxs-lookup"><span data-stu-id="fd199-148">**Response Body**: Empty</span></span>  

## <a name="list-all-registered-tenants"></a><span data-ttu-id="fd199-149">List all registered tenants</span><span class="sxs-lookup"><span data-stu-id="fd199-149">List all registered tenants</span></span>

<span data-ttu-id="fd199-150">Get a list of all tenants that have been added to a registration.</span><span class="sxs-lookup"><span data-stu-id="fd199-150">Get a list of all tenants that have been added to a registration.</span></span>

 > [!Note]  
 > <span data-ttu-id="fd199-151">If no tenants have been registered, you won't receive a response.</span><span class="sxs-lookup"><span data-stu-id="fd199-151">If no tenants have been registered, you won't receive a response.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd199-152">Parameters</span><span class="sxs-lookup"><span data-stu-id="fd199-152">Parameters</span></span>

| <span data-ttu-id="fd199-153">Parameter</span><span class="sxs-lookup"><span data-stu-id="fd199-153">Parameter</span></span>                  | <span data-ttu-id="fd199-154">Description</span><span class="sxs-lookup"><span data-stu-id="fd199-154">Description</span></span>          |
|---                         | ---                  |
| <span data-ttu-id="fd199-155">registrationSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="fd199-155">registrationSubscriptionId</span></span> | <span data-ttu-id="fd199-156">The Azure subscription that was used for the initial registration.</span><span class="sxs-lookup"><span data-stu-id="fd199-156">The Azure subscription that was used for the initial registration.</span></span>   |
| <span data-ttu-id="fd199-157">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="fd199-157">resourceGroup</span></span>              | <span data-ttu-id="fd199-158">The resource group in Azure in which your registration is stored.</span><span class="sxs-lookup"><span data-stu-id="fd199-158">The resource group in Azure in which your registration is stored.</span></span>    |
| <span data-ttu-id="fd199-159">registrationName</span><span class="sxs-lookup"><span data-stu-id="fd199-159">registrationName</span></span>           | <span data-ttu-id="fd199-160">The name of the registration of your Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="fd199-160">The name of the registration of your Azure Stack.</span></span> <span data-ttu-id="fd199-161">It is an object stored in Azure.</span><span class="sxs-lookup"><span data-stu-id="fd199-161">It is an object stored in Azure.</span></span> <span data-ttu-id="fd199-162">The name is usually in the form of **azurestack**-***CloudID***, where ***CloudID*** is the Cloud ID of your Azure Stack deployment.</span><span class="sxs-lookup"><span data-stu-id="fd199-162">The name is usually in the form of **azurestack**-***CloudID***, where ***CloudID*** is the Cloud ID of your Azure Stack deployment.</span></span>   |

### <a name="powershell"></a><span data-ttu-id="fd199-163">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd199-163">PowerShell</span></span>

<span data-ttu-id="fd199-164">Use the Get-AzureRmResource cmdlet to list all registered tenants.</span><span class="sxs-lookup"><span data-stu-id="fd199-164">Use the Get-AzureRmResource cmdlet to list all registered tenants.</span></span> <span data-ttu-id="fd199-165">Sign in to Azure (`Add-AzureRmAccount`) using the account you used for the initial registration.</span><span class="sxs-lookup"><span data-stu-id="fd199-165">Sign in to Azure (`Add-AzureRmAccount`) using the account you used for the initial registration.</span></span> <span data-ttu-id="fd199-166">Here is an example of how to add a tenant:</span><span class="sxs-lookup"><span data-stu-id="fd199-166">Here is an example of how to add a tenant:</span></span>

```powershell
  Get-AzureRmResource -ResourceId "subscriptions/{registrationSubscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions" -ApiVersion 2017-06-01
```

### <a name="api-call"></a><span data-ttu-id="fd199-167">API Call</span><span class="sxs-lookup"><span data-stu-id="fd199-167">API Call</span></span>

<span data-ttu-id="fd199-168">You can get a list of all tenant mappings using the GET operation</span><span class="sxs-lookup"><span data-stu-id="fd199-168">You can get a list of all tenant mappings using the GET operation</span></span>

<span data-ttu-id="fd199-169">**Operation**: GET</span><span class="sxs-lookup"><span data-stu-id="fd199-169">**Operation**: GET</span></span>  
<span data-ttu-id="fd199-170">**RequestURI**: `subscriptions/{registrationSubscriptionId}/resourceGroups/{resourceGroup}  
/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions?  
api-version=2017-06-01 HTTP/1.1`</span><span class="sxs-lookup"><span data-stu-id="fd199-170">**RequestURI**: `subscriptions/{registrationSubscriptionId}/resourceGroups/{resourceGroup}  
/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions?  
api-version=2017-06-01 HTTP/1.1`</span></span>  
<span data-ttu-id="fd199-171">**Response**: 200</span><span class="sxs-lookup"><span data-stu-id="fd199-171">**Response**: 200</span></span>  
<span data-ttu-id="fd199-172">**Response Body**:</span><span class="sxs-lookup"><span data-stu-id="fd199-172">**Response Body**:</span></span> 

```JSON  
{
    "value": [{
            "id": " subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{ cspSubscriptionId 1}”,
            "name": " cspSubscriptionId 1",
            "type": “Microsoft.AzureStack\customerSubscriptions”,
            "properties": { "tenantId": "tId1" }
        },
        {
            "id": " subscriptions/{subscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{ cspSubscriptionId 2}”,
            "name": " cspSubscriptionId2 ",
            "type": “Microsoft.AzureStack\customerSubscriptions”,
            "properties": { "tenantId": "tId2" }
        }
    ],
    "nextLink": "{originalRequestUrl}?$skipToken={opaqueString}"
}
```

## <a name="remove-a-tenant-mapping"></a><span data-ttu-id="fd199-173">Remove a tenant mapping</span><span class="sxs-lookup"><span data-stu-id="fd199-173">Remove a tenant mapping</span></span>

<span data-ttu-id="fd199-174">You can remove a tenant that has been added to a registration.</span><span class="sxs-lookup"><span data-stu-id="fd199-174">You can remove a tenant that has been added to a registration.</span></span> <span data-ttu-id="fd199-175">If that tenant is still using resources on Azure Stack, their usage is charged to the subscription used in the initial Azure Stack registration.</span><span class="sxs-lookup"><span data-stu-id="fd199-175">If that tenant is still using resources on Azure Stack, their usage is charged to the subscription used in the initial Azure Stack registration.</span></span>

### <a name="parameters"></a><span data-ttu-id="fd199-176">Parameters</span><span class="sxs-lookup"><span data-stu-id="fd199-176">Parameters</span></span>

| <span data-ttu-id="fd199-177">Parameter</span><span class="sxs-lookup"><span data-stu-id="fd199-177">Parameter</span></span>                  | <span data-ttu-id="fd199-178">Description</span><span class="sxs-lookup"><span data-stu-id="fd199-178">Description</span></span>          |
|---                         | ---                  |
| <span data-ttu-id="fd199-179">registrationSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="fd199-179">registrationSubscriptionId</span></span> | <span data-ttu-id="fd199-180">Subscription ID for the registration.</span><span class="sxs-lookup"><span data-stu-id="fd199-180">Subscription ID for the registration.</span></span>   |
| <span data-ttu-id="fd199-181">resourceGroup</span><span class="sxs-lookup"><span data-stu-id="fd199-181">resourceGroup</span></span>              | <span data-ttu-id="fd199-182">The resource group for the registration.</span><span class="sxs-lookup"><span data-stu-id="fd199-182">The resource group for the registration.</span></span>   |
| <span data-ttu-id="fd199-183">registrationName</span><span class="sxs-lookup"><span data-stu-id="fd199-183">registrationName</span></span>           | <span data-ttu-id="fd199-184">The name of the registration.</span><span class="sxs-lookup"><span data-stu-id="fd199-184">The name of the registration.</span></span>  |
| <span data-ttu-id="fd199-185">customerSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="fd199-185">customerSubscriptionId</span></span>     | <span data-ttu-id="fd199-186">The customer subscription ID.</span><span class="sxs-lookup"><span data-stu-id="fd199-186">The customer subscription ID.</span></span>  |

### <a name="powershell"></a><span data-ttu-id="fd199-187">PowerShell</span><span class="sxs-lookup"><span data-stu-id="fd199-187">PowerShell</span></span>

```powershell
  Remove-AzureRmResource -ResourceId "subscriptions/{registrationSubscriptionId}/resourceGroups/{resourceGroup}/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/{customerSubscriptionId}" -ApiVersion 2017-06-01
```

### <a name="api-call"></a><span data-ttu-id="fd199-188">API Call</span><span class="sxs-lookup"><span data-stu-id="fd199-188">API Call</span></span>

<span data-ttu-id="fd199-189">You can remove tenant mappings using the DELETE operation.</span><span class="sxs-lookup"><span data-stu-id="fd199-189">You can remove tenant mappings using the DELETE operation.</span></span>

<span data-ttu-id="fd199-190">**Operation**: DELETE</span><span class="sxs-lookup"><span data-stu-id="fd199-190">**Operation**: DELETE</span></span>  
<span data-ttu-id="fd199-191">**RequestURI**: `subscriptions/{registrationSubscriptionId}/resourceGroups/{resourceGroup}  
/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/  
{customerSubscriptionId}?api-version=2017-06-01 HTTP/1.1`</span><span class="sxs-lookup"><span data-stu-id="fd199-191">**RequestURI**: `subscriptions/{registrationSubscriptionId}/resourceGroups/{resourceGroup}  
/providers/Microsoft.AzureStack/registrations/{registrationName}/customerSubscriptions/  
{customerSubscriptionId}?api-version=2017-06-01 HTTP/1.1`</span></span>  
<span data-ttu-id="fd199-192">**Response**: 204 No Content</span><span class="sxs-lookup"><span data-stu-id="fd199-192">**Response**: 204 No Content</span></span>  
<span data-ttu-id="fd199-193">**Response Body**: Empty</span><span class="sxs-lookup"><span data-stu-id="fd199-193">**Response Body**: Empty</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd199-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="fd199-194">Next steps</span></span>

 - <span data-ttu-id="fd199-195">To learn more about how to retrieve resource usage information from Azure Stack, see [Usage and billing in Azure Stack](azure-stack-billing-and-chargeback.md).</span><span class="sxs-lookup"><span data-stu-id="fd199-195">To learn more about how to retrieve resource usage information from Azure Stack, see [Usage and billing in Azure Stack](azure-stack-billing-and-chargeback.md).</span></span>
