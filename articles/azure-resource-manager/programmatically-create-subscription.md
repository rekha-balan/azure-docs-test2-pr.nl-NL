---
title: Programmatically create Azure Enterprise subscriptions| Microsoft Docs
description: Learn how to create additional Azure Enterprise or Enterprise Dev/Test subscriptions programmatically.
services: azure-resource-manager
author: adpick
manager: adpick
editor: ''
ms.assetid: ''
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/05/2018
ms.author: adpick
ms.openlocfilehash: 2bfa9944d85fde65ad8dbd73ddda11fa405df2f8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867454"
---
# <a name="programmatically-create-azure-enterprise-subscriptions-preview"></a><span data-ttu-id="d5ca2-103">Programmatically create Azure Enterprise subscriptions (preview)</span><span class="sxs-lookup"><span data-stu-id="d5ca2-103">Programmatically create Azure Enterprise subscriptions (preview)</span></span>

<span data-ttu-id="d5ca2-104">As an Azure customer on [Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/), you can create EA (MS-AZR-0017P) and EA Dev/Test (MS-AZR-0148P) subscriptions programmatically.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-104">As an Azure customer on [Enterprise Agreement (EA)](https://azure.microsoft.com/pricing/enterprise-agreement/), you can create EA (MS-AZR-0017P) and EA Dev/Test (MS-AZR-0148P) subscriptions programmatically.</span></span> <span data-ttu-id="d5ca2-105">In this article, you learn how to create subscriptions programmatically using Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-105">In this article, you learn how to create subscriptions programmatically using Azure Resource Manager.</span></span>

<span data-ttu-id="d5ca2-106">When you create an Azure subscription from this API, that subscription is governed by the agreement under which you obtained Microsoft Azure services from Microsoft or an authorized reseller.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-106">When you create an Azure subscription from this API, that subscription is governed by the agreement under which you obtained Microsoft Azure services from Microsoft or an authorized reseller.</span></span> <span data-ttu-id="d5ca2-107">To learn more, see [Microsoft Azure Legal Information](https://azure.microsoft.com/support/legal/).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-107">To learn more, see [Microsoft Azure Legal Information](https://azure.microsoft.com/support/legal/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d5ca2-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d5ca2-108">Prerequisites</span></span>

<span data-ttu-id="d5ca2-109">You must have an Owner or Contributor role on the Enrollment Account you wish to create subscriptions under.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-109">You must have an Owner or Contributor role on the Enrollment Account you wish to create subscriptions under.</span></span> <span data-ttu-id="d5ca2-110">There are two ways to get these roles:</span><span class="sxs-lookup"><span data-stu-id="d5ca2-110">There are two ways to get these roles:</span></span>

* <span data-ttu-id="d5ca2-111">Your Enrollment Administrator can [make you an Account Owner](https://ea.azure.com/helpdocs/addNewAccount) (log-in required) which makes you an Owner of the Enrollment Account.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-111">Your Enrollment Administrator can [make you an Account Owner](https://ea.azure.com/helpdocs/addNewAccount) (log-in required) which makes you an Owner of the Enrollment Account.</span></span> <span data-ttu-id="d5ca2-112">Follow the instructions in the invitation email you receive to manually create an initial subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-112">Follow the instructions in the invitation email you receive to manually create an initial subscription.</span></span> <span data-ttu-id="d5ca2-113">Confirm account ownership and manually create an initial EA subscription before proceeding to the next step.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-113">Confirm account ownership and manually create an initial EA subscription before proceeding to the next step.</span></span> <span data-ttu-id="d5ca2-114">Just adding the account to the enrollment isn't enough.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-114">Just adding the account to the enrollment isn't enough.</span></span>

* <span data-ttu-id="d5ca2-115">An existing Owner of the Enrollment Account can [grant you access](grant-access-to-create-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-115">An existing Owner of the Enrollment Account can [grant you access](grant-access-to-create-subscription.md).</span></span> <span data-ttu-id="d5ca2-116">Similarly, if you want to use a service principal to create the EA subscription, you must [grant that service principal the ability to create subscriptions](grant-access-to-create-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-116">Similarly, if you want to use a service principal to create the EA subscription, you must [grant that service principal the ability to create subscriptions](grant-access-to-create-subscription.md).</span></span>

## <a name="find-accounts-you-have-access-to"></a><span data-ttu-id="d5ca2-117">Find accounts you have access to</span><span class="sxs-lookup"><span data-stu-id="d5ca2-117">Find accounts you have access to</span></span>

<span data-ttu-id="d5ca2-118">After you're added to an Azure EA enrollment as an Account Owner, Azure uses the account-to-enrollment relationship to determine where to bill the subscription charges.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-118">After you're added to an Azure EA enrollment as an Account Owner, Azure uses the account-to-enrollment relationship to determine where to bill the subscription charges.</span></span> <span data-ttu-id="d5ca2-119">All subscriptions created under the account are billed towards the EA enrollment that the account is in.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-119">All subscriptions created under the account are billed towards the EA enrollment that the account is in.</span></span> <span data-ttu-id="d5ca2-120">To create subscriptions, you must pass in values about the enrollment account and the user principals to own the subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-120">To create subscriptions, you must pass in values about the enrollment account and the user principals to own the subscription.</span></span> 

<span data-ttu-id="d5ca2-121">To run the following commands, you must be logged in to the Account Owner's *home directory*, which is the directory that subscriptions are created in by default.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-121">To run the following commands, you must be logged in to the Account Owner's *home directory*, which is the directory that subscriptions are created in by default.</span></span>

# <a name="resttabrest"></a>[<span data-ttu-id="d5ca2-122">REST</span><span class="sxs-lookup"><span data-stu-id="d5ca2-122">REST</span></span>](#tab/rest)

<span data-ttu-id="d5ca2-123">Request to list all enrollment accounts:</span><span class="sxs-lookup"><span data-stu-id="d5ca2-123">Request to list all enrollment accounts:</span></span>

```json
GET https://management.azure.com/providers/Microsoft.Billing/enrollmentAccounts?api-version=2018-03-01-preview
```

<span data-ttu-id="d5ca2-124">Azure responds with a list of all enrollment accounts you have access to:</span><span class="sxs-lookup"><span data-stu-id="d5ca2-124">Azure responds with a list of all enrollment accounts you have access to:</span></span>

```json
{
  "value": [
    {
      "id": "/providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "name": "747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "type": "Microsoft.Billing/enrollmentAccounts",
      "properties": {
        "principalName": "SignUpEngineering@contoso.com"
      }
    },
    {
      "id": "/providers/Microsoft.Billing/enrollmentAccounts/4cd2fcf6-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "name": "4cd2fcf6-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "type": "Microsoft.Billing/enrollmentAccounts",
      "properties": {
        "principalName": "BillingPlatformTeam@contoso.com"
      }
    }
  ]
}
```

# <a name="powershelltabazure-powershell"></a>[<span data-ttu-id="d5ca2-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5ca2-125">PowerShell</span></span>](#tab/azure-powershell)

<span data-ttu-id="d5ca2-126">Use the [Get-AzureRmEnrollmentAccount command](/powershell/module/azurerm.billing/get-azurermenrollmentaccount) to list all enrollment accounts you have access to.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-126">Use the [Get-AzureRmEnrollmentAccount command](/powershell/module/azurerm.billing/get-azurermenrollmentaccount) to list all enrollment accounts you have access to.</span></span>

```azurepowershell-interactive
Get-AzureRmEnrollmentAccount
```

<span data-ttu-id="d5ca2-127">Azure responds with a list of the Object IDs and email addresses of accounts.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-127">Azure responds with a list of the Object IDs and email addresses of accounts.</span></span>

```azurepowershell
ObjectId                               | PrincipalName
747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx   | SignUpEngineering@contoso.com
4cd2fcf6-xxxx-xxxx-xxxx-xxxxxxxxxxxx   | BillingPlatformTeam@contoso.com
```

# <a name="azure-clitabazure-cli"></a>[<span data-ttu-id="d5ca2-128">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d5ca2-128">Azure CLI</span></span>](#tab/azure-cli)

<span data-ttu-id="d5ca2-129">Use the [az billing enrollment-account list](https://aka.ms/EASubCreationPublicPreviewCLI) command to list all enrollment accounts you have access to.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-129">Use the [az billing enrollment-account list](https://aka.ms/EASubCreationPublicPreviewCLI) command to list all enrollment accounts you have access to.</span></span>

```azurecli-interactive 
az billing enrollment-account list
```

<span data-ttu-id="d5ca2-130">Azure responds with a list of the Object IDs and email addresses of accounts.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-130">Azure responds with a list of the Object IDs and email addresses of accounts.</span></span>

```json
{
  "value": [
    {
      "id": "/providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "name": "747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "type": "Microsoft.Billing/enrollmentAccounts",
      "properties": {
        "principalName": "SignUpEngineering@contoso.com"
      }
    },
    {
      "id": "/providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "name": "4cd2fcf6-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
      "type": "Microsoft.Billing/enrollmentAccounts",
      "properties": {
        "principalName": "BillingPlatformTeam@contoso.com"
      }
    }
  ]
}
```

---

<span data-ttu-id="d5ca2-131">Use the `principalName` property to identify the account that you want subscriptions to be billed to.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-131">Use the `principalName` property to identify the account that you want subscriptions to be billed to.</span></span> <span data-ttu-id="d5ca2-132">Use the `id` as the `enrollmentAccount` value that you use to create the subscription in the next step.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-132">Use the `id` as the `enrollmentAccount` value that you use to create the subscription in the next step.</span></span>

## <a name="create-subscriptions-under-a-specific-enrollment-account"></a><span data-ttu-id="d5ca2-133">Create subscriptions under a specific enrollment account</span><span class="sxs-lookup"><span data-stu-id="d5ca2-133">Create subscriptions under a specific enrollment account</span></span> 

<span data-ttu-id="d5ca2-134">The following example creates a request to create subscription named *Dev Team Subscription* and subscription offer is *MS-AZR-0017P* (regular EA).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-134">The following example creates a request to create subscription named *Dev Team Subscription* and subscription offer is *MS-AZR-0017P* (regular EA).</span></span> <span data-ttu-id="d5ca2-135">The enrollment account is `747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx` (placeholder value, this value is a GUID), which is the enrollment account for SignUpEngineering@contoso.com.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-135">The enrollment account is `747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx` (placeholder value, this value is a GUID), which is the enrollment account for SignUpEngineering@contoso.com.</span></span> <span data-ttu-id="d5ca2-136">It also optionally adds two users as RBAC Owners for the subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-136">It also optionally adds two users as RBAC Owners for the subscription.</span></span>

# <a name="resttabrest"></a>[<span data-ttu-id="d5ca2-137">REST</span><span class="sxs-lookup"><span data-stu-id="d5ca2-137">REST</span></span>](#tab/rest)

<span data-ttu-id="d5ca2-138">Use the `id` of the `enrollmentAccount` in the path of the request to create subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-138">Use the `id` of the `enrollmentAccount` in the path of the request to create subscription.</span></span>

```json
POST https://management.azure.com/providers/Microsoft.Billing/enrollmentAccounts/747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx/providers/Microsoft.Subscription/createSubscription?api-version=2018-03-01-preview

{
  "displayName": "Dev Team Subscription",
  "offerType": "MS-AZR-0017P",
  "owners": [
    {
      "objectId": "<userObjectId>"
    },
    {
      "objectId": "<servicePrincipalObjectId>"
    }
  ]
}
```

| <span data-ttu-id="d5ca2-139">Element Name</span><span class="sxs-lookup"><span data-stu-id="d5ca2-139">Element Name</span></span>  | <span data-ttu-id="d5ca2-140">Required</span><span class="sxs-lookup"><span data-stu-id="d5ca2-140">Required</span></span> | <span data-ttu-id="d5ca2-141">Type</span><span class="sxs-lookup"><span data-stu-id="d5ca2-141">Type</span></span>   | <span data-ttu-id="d5ca2-142">Description</span><span class="sxs-lookup"><span data-stu-id="d5ca2-142">Description</span></span>                                                                                               |
|---------------|----------|--------|-----------------------------------------------------------------------------------------------------------|
| `displayName` | <span data-ttu-id="d5ca2-143">No</span><span class="sxs-lookup"><span data-stu-id="d5ca2-143">No</span></span>      | <span data-ttu-id="d5ca2-144">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-144">String</span></span> | <span data-ttu-id="d5ca2-145">The display name of the subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-145">The display name of the subscription.</span></span> <span data-ttu-id="d5ca2-146">If not specified, it's set to the name of the offer, like "Microsoft Azure Enterprise."</span><span class="sxs-lookup"><span data-stu-id="d5ca2-146">If not specified, it's set to the name of the offer, like "Microsoft Azure Enterprise."</span></span>                                 |
| `offerType`   | <span data-ttu-id="d5ca2-147">Yes</span><span class="sxs-lookup"><span data-stu-id="d5ca2-147">Yes</span></span>      | <span data-ttu-id="d5ca2-148">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-148">String</span></span> | <span data-ttu-id="d5ca2-149">The offer of the subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-149">The offer of the subscription.</span></span> <span data-ttu-id="d5ca2-150">The two options for EA are [MS-AZR-0017P](https://azure.microsoft.com/pricing/enterprise-agreement/) (production use) and [MS-AZR-0148P](https://azure.microsoft.com/offers/ms-azr-0148p/) (dev/test, needs to be [turned on using the EA portal](https://ea.azure.com/helpdocs/DevOrTestOffer)).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-150">The two options for EA are [MS-AZR-0017P](https://azure.microsoft.com/pricing/enterprise-agreement/) (production use) and [MS-AZR-0148P](https://azure.microsoft.com/offers/ms-azr-0148p/) (dev/test, needs to be [turned on using the EA portal](https://ea.azure.com/helpdocs/DevOrTestOffer)).</span></span>                |
| `owners`      | <span data-ttu-id="d5ca2-151">No</span><span class="sxs-lookup"><span data-stu-id="d5ca2-151">No</span></span>       | <span data-ttu-id="d5ca2-152">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-152">String</span></span> | <span data-ttu-id="d5ca2-153">The Object ID of any user that you'd like to add as an RBAC Owner on the subscription when it's created.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-153">The Object ID of any user that you'd like to add as an RBAC Owner on the subscription when it's created.</span></span>  |

<span data-ttu-id="d5ca2-154">In the response, you get back a `subscriptionOperation` object for monitoring.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-154">In the response, you get back a `subscriptionOperation` object for monitoring.</span></span> <span data-ttu-id="d5ca2-155">When the subscription creation is finished, the `subscriptionOperation` object would return a `subscriptionLink` object, which has the subscription ID.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-155">When the subscription creation is finished, the `subscriptionOperation` object would return a `subscriptionLink` object, which has the subscription ID.</span></span>

# <a name="powershelltabazure-powershell"></a>[<span data-ttu-id="d5ca2-156">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d5ca2-156">PowerShell</span></span>](#tab/azure-powershell)

<span data-ttu-id="d5ca2-157">To use this preview module, install it by running `Install-Module AzureRM.Subscription -AllowPrerelease` first.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-157">To use this preview module, install it by running `Install-Module AzureRM.Subscription -AllowPrerelease` first.</span></span> <span data-ttu-id="d5ca2-158">To make sure `-AllowPrerelease` works, install a recent version of PowerShellGet from [Get PowerShellGet Module](/powershell/gallery/installing-psget).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-158">To make sure `-AllowPrerelease` works, install a recent version of PowerShellGet from [Get PowerShellGet Module](/powershell/gallery/installing-psget).</span></span>

<span data-ttu-id="d5ca2-159">Use the [New-AzureRmSubscription](/powershell/module/azurerm.subscription) along with `enrollmentAccount` object ID as the `EnrollmentAccountObjectId` parameter to create a new subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-159">Use the [New-AzureRmSubscription](/powershell/module/azurerm.subscription) along with `enrollmentAccount` object ID as the `EnrollmentAccountObjectId` parameter to create a new subscription.</span></span> 

```azurepowershell-interactive
New-AzureRmSubscription -OfferType MS-AZR-0017P -Name "Dev Team Subscription" -EnrollmentAccountObjectId 747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx -OwnerObjectId <userObjectId>,<servicePrincipalObjectId>
```

| <span data-ttu-id="d5ca2-160">Element Name</span><span class="sxs-lookup"><span data-stu-id="d5ca2-160">Element Name</span></span>  | <span data-ttu-id="d5ca2-161">Required</span><span class="sxs-lookup"><span data-stu-id="d5ca2-161">Required</span></span> | <span data-ttu-id="d5ca2-162">Type</span><span class="sxs-lookup"><span data-stu-id="d5ca2-162">Type</span></span>   | <span data-ttu-id="d5ca2-163">Description</span><span class="sxs-lookup"><span data-stu-id="d5ca2-163">Description</span></span>                                                                                               |
|---------------|----------|--------|-----------------------------------------------------------------------------------------------------------|
| `Name` | <span data-ttu-id="d5ca2-164">No</span><span class="sxs-lookup"><span data-stu-id="d5ca2-164">No</span></span>      | <span data-ttu-id="d5ca2-165">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-165">String</span></span> | <span data-ttu-id="d5ca2-166">The display name of the subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-166">The display name of the subscription.</span></span> <span data-ttu-id="d5ca2-167">If not specified, it's set to the name of the offer, like "Microsoft Azure Enterprise."</span><span class="sxs-lookup"><span data-stu-id="d5ca2-167">If not specified, it's set to the name of the offer, like "Microsoft Azure Enterprise."</span></span>                                 |
| `OfferType`   | <span data-ttu-id="d5ca2-168">Yes</span><span class="sxs-lookup"><span data-stu-id="d5ca2-168">Yes</span></span>      | <span data-ttu-id="d5ca2-169">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-169">String</span></span> | <span data-ttu-id="d5ca2-170">The offer of the subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-170">The offer of the subscription.</span></span> <span data-ttu-id="d5ca2-171">The two options for EA are [MS-AZR-0017P](https://azure.microsoft.com/pricing/enterprise-agreement/) (production use) and [MS-AZR-0148P](https://azure.microsoft.com/offers/ms-azr-0148p/) (dev/test, needs to be [turned on using the EA portal](https://ea.azure.com/helpdocs/DevOrTestOffer)).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-171">The two options for EA are [MS-AZR-0017P](https://azure.microsoft.com/pricing/enterprise-agreement/) (production use) and [MS-AZR-0148P](https://azure.microsoft.com/offers/ms-azr-0148p/) (dev/test, needs to be [turned on using the EA portal](https://ea.azure.com/helpdocs/DevOrTestOffer)).</span></span>                |
| `EnrollmentAccountObjectId`      | <span data-ttu-id="d5ca2-172">Yes</span><span class="sxs-lookup"><span data-stu-id="d5ca2-172">Yes</span></span>       | <span data-ttu-id="d5ca2-173">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-173">String</span></span> | <span data-ttu-id="d5ca2-174">The Object ID of the enrollment account that the subscription is created under and billed to.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-174">The Object ID of the enrollment account that the subscription is created under and billed to.</span></span> <span data-ttu-id="d5ca2-175">This value is a GUID that you get from `Get-AzureRmEnrollmentAccount`.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-175">This value is a GUID that you get from `Get-AzureRmEnrollmentAccount`.</span></span> |
| `OwnerObjectId`      | <span data-ttu-id="d5ca2-176">No</span><span class="sxs-lookup"><span data-stu-id="d5ca2-176">No</span></span>       | <span data-ttu-id="d5ca2-177">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-177">String</span></span> | <span data-ttu-id="d5ca2-178">The Object ID of any user that you'd like to add as an RBAC Owner on the subscription when it's created.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-178">The Object ID of any user that you'd like to add as an RBAC Owner on the subscription when it's created.</span></span>  |
| `OwnerSignInName`    | <span data-ttu-id="d5ca2-179">No</span><span class="sxs-lookup"><span data-stu-id="d5ca2-179">No</span></span>       | <span data-ttu-id="d5ca2-180">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-180">String</span></span> | <span data-ttu-id="d5ca2-181">The email address of any user that you'd like to add as an RBAC Owner on the subscription when it's created.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-181">The email address of any user that you'd like to add as an RBAC Owner on the subscription when it's created.</span></span> <span data-ttu-id="d5ca2-182">You can use this parameter instead of `OwnerObjectId`.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-182">You can use this parameter instead of `OwnerObjectId`.</span></span>|
| `OwnerApplicationId` | <span data-ttu-id="d5ca2-183">No</span><span class="sxs-lookup"><span data-stu-id="d5ca2-183">No</span></span>       | <span data-ttu-id="d5ca2-184">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-184">String</span></span> | <span data-ttu-id="d5ca2-185">The application ID of any service principal that you'd like to add as an RBAC Owner on the subscription when it's created.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-185">The application ID of any service principal that you'd like to add as an RBAC Owner on the subscription when it's created.</span></span> <span data-ttu-id="d5ca2-186">You can use this parameter instead of `OwnerObjectId`.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-186">You can use this parameter instead of `OwnerObjectId`.</span></span>| 

<span data-ttu-id="d5ca2-187">To see a full list of all parameters, see [New-AzureRmSubscription](/powershell/module/azurerm.subscription.preview).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-187">To see a full list of all parameters, see [New-AzureRmSubscription](/powershell/module/azurerm.subscription.preview).</span></span>

# <a name="azure-clitabazure-cli"></a>[<span data-ttu-id="d5ca2-188">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d5ca2-188">Azure CLI</span></span>](#tab/azure-cli)

<span data-ttu-id="d5ca2-189">To use this preview extension, install it by running `az extension add --name subscription` first.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-189">To use this preview extension, install it by running `az extension add --name subscription` first.</span></span>

<span data-ttu-id="d5ca2-190">Use the [az account create](/cli/azure/ext/subscription/account?view=azure-cli-latest#-ext-subscription-az-account-create) along with `enrollmentAccount` object ID as the `enrollment-account-object-id` parameter to create a new subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-190">Use the [az account create](/cli/azure/ext/subscription/account?view=azure-cli-latest#-ext-subscription-az-account-create) along with `enrollmentAccount` object ID as the `enrollment-account-object-id` parameter to create a new subscription.</span></span>

```azurecli-interactive 
az account create --offer-type "MS-AZR-0017P" --display-name "Dev Team Subscription" --enrollment-account-object-id "747ddfe5-xxxx-xxxx-xxxx-xxxxxxxxxxxx" --owner-object-id "<userObjectId>","<servicePrincipalObjectId>"
```

| <span data-ttu-id="d5ca2-191">Element Name</span><span class="sxs-lookup"><span data-stu-id="d5ca2-191">Element Name</span></span>  | <span data-ttu-id="d5ca2-192">Required</span><span class="sxs-lookup"><span data-stu-id="d5ca2-192">Required</span></span> | <span data-ttu-id="d5ca2-193">Type</span><span class="sxs-lookup"><span data-stu-id="d5ca2-193">Type</span></span>   | <span data-ttu-id="d5ca2-194">Description</span><span class="sxs-lookup"><span data-stu-id="d5ca2-194">Description</span></span>                                                                                               |
|---------------|----------|--------|-----------------------------------------------------------------------------------------------------------|
| `display-name` | <span data-ttu-id="d5ca2-195">No</span><span class="sxs-lookup"><span data-stu-id="d5ca2-195">No</span></span>      | <span data-ttu-id="d5ca2-196">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-196">String</span></span> | <span data-ttu-id="d5ca2-197">The display name of the subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-197">The display name of the subscription.</span></span> <span data-ttu-id="d5ca2-198">If not specified, it's set to the name of the offer, like "Microsoft Azure Enterprise."</span><span class="sxs-lookup"><span data-stu-id="d5ca2-198">If not specified, it's set to the name of the offer, like "Microsoft Azure Enterprise."</span></span>                                 |
| `offer-type`   | <span data-ttu-id="d5ca2-199">Yes</span><span class="sxs-lookup"><span data-stu-id="d5ca2-199">Yes</span></span>      | <span data-ttu-id="d5ca2-200">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-200">String</span></span> | <span data-ttu-id="d5ca2-201">The offer of the subscription.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-201">The offer of the subscription.</span></span> <span data-ttu-id="d5ca2-202">The two options for EA are [MS-AZR-0017P](https://azure.microsoft.com/pricing/enterprise-agreement/) (production use) and [MS-AZR-0148P](https://azure.microsoft.com/offers/ms-azr-0148p/) (dev/test, needs to be [turned on using the EA portal](https://ea.azure.com/helpdocs/DevOrTestOffer)).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-202">The two options for EA are [MS-AZR-0017P](https://azure.microsoft.com/pricing/enterprise-agreement/) (production use) and [MS-AZR-0148P](https://azure.microsoft.com/offers/ms-azr-0148p/) (dev/test, needs to be [turned on using the EA portal](https://ea.azure.com/helpdocs/DevOrTestOffer)).</span></span>                |
| `enrollment-account-object-id`      | <span data-ttu-id="d5ca2-203">Yes</span><span class="sxs-lookup"><span data-stu-id="d5ca2-203">Yes</span></span>       | <span data-ttu-id="d5ca2-204">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-204">String</span></span> | <span data-ttu-id="d5ca2-205">The Object ID of the enrollment account that the subscription is created under and billed to.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-205">The Object ID of the enrollment account that the subscription is created under and billed to.</span></span> <span data-ttu-id="d5ca2-206">This value is a GUID that you get from `az billing enrollment-account list`.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-206">This value is a GUID that you get from `az billing enrollment-account list`.</span></span> |
| `owner-object-id`      | <span data-ttu-id="d5ca2-207">No</span><span class="sxs-lookup"><span data-stu-id="d5ca2-207">No</span></span>       | <span data-ttu-id="d5ca2-208">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-208">String</span></span> | <span data-ttu-id="d5ca2-209">The Object ID of any user that you'd like to add as an RBAC Owner on the subscription when it's created.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-209">The Object ID of any user that you'd like to add as an RBAC Owner on the subscription when it's created.</span></span>  |
| `owner-upn`    | <span data-ttu-id="d5ca2-210">No</span><span class="sxs-lookup"><span data-stu-id="d5ca2-210">No</span></span>       | <span data-ttu-id="d5ca2-211">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-211">String</span></span> | <span data-ttu-id="d5ca2-212">The email address of any user that you'd like to add as an RBAC Owner on the subscription when it's created.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-212">The email address of any user that you'd like to add as an RBAC Owner on the subscription when it's created.</span></span> <span data-ttu-id="d5ca2-213">You can use this parameter instead of `owner-object-id`.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-213">You can use this parameter instead of `owner-object-id`.</span></span>|
| `owner-spn` | <span data-ttu-id="d5ca2-214">No</span><span class="sxs-lookup"><span data-stu-id="d5ca2-214">No</span></span>       | <span data-ttu-id="d5ca2-215">String</span><span class="sxs-lookup"><span data-stu-id="d5ca2-215">String</span></span> | <span data-ttu-id="d5ca2-216">The application ID of any service principal that you'd like to add as an RBAC Owner on the subscription when it's created.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-216">The application ID of any service principal that you'd like to add as an RBAC Owner on the subscription when it's created.</span></span> <span data-ttu-id="d5ca2-217">You can use this parameter instead of `owner-object-id`.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-217">You can use this parameter instead of `owner-object-id`.</span></span>| 

<span data-ttu-id="d5ca2-218">To see a full list of all parameters, see [az account create](/cli/azure/ext/subscription/account?view=azure-cli-latest#-ext-subscription-az-account-create).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-218">To see a full list of all parameters, see [az account create](/cli/azure/ext/subscription/account?view=azure-cli-latest#-ext-subscription-az-account-create).</span></span>

----

## <a name="limitations-of-azure-enterprise-subscription-creation-api"></a><span data-ttu-id="d5ca2-219">Limitations of Azure Enterprise subscription creation API</span><span class="sxs-lookup"><span data-stu-id="d5ca2-219">Limitations of Azure Enterprise subscription creation API</span></span>

- <span data-ttu-id="d5ca2-220">Only Azure Enterprise subscriptions can be created using this API.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-220">Only Azure Enterprise subscriptions can be created using this API.</span></span>
- <span data-ttu-id="d5ca2-221">There's a limit of 50 subscriptions per account.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-221">There's a limit of 50 subscriptions per account.</span></span> <span data-ttu-id="d5ca2-222">After that, subscriptions can only be created by using Account Center.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-222">After that, subscriptions can only be created by using Account Center.</span></span>
- <span data-ttu-id="d5ca2-223">There needs to be at least one EA or EA Dev/Test subscriptions under the account, which means the Account Owner has gone through manual sign-up at least once.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-223">There needs to be at least one EA or EA Dev/Test subscriptions under the account, which means the Account Owner has gone through manual sign-up at least once.</span></span>
- <span data-ttu-id="d5ca2-224">Users who aren't Account Owners, but were added to an enrollment account via RBAC, can't create subscriptions using Account Center.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-224">Users who aren't Account Owners, but were added to an enrollment account via RBAC, can't create subscriptions using Account Center.</span></span>
- <span data-ttu-id="d5ca2-225">You can't select the tenant for the subscription to be created in.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-225">You can't select the tenant for the subscription to be created in.</span></span> <span data-ttu-id="d5ca2-226">The subscription is always created in the home tenant of the Account Owner.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-226">The subscription is always created in the home tenant of the Account Owner.</span></span> <span data-ttu-id="d5ca2-227">To move the subscription to a different tenant, see [change subscription tenant](../active-directory/fundamentals/active-directory-how-subscriptions-associated-directory.md).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-227">To move the subscription to a different tenant, see [change subscription tenant](../active-directory/fundamentals/active-directory-how-subscriptions-associated-directory.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d5ca2-228">Next steps</span><span class="sxs-lookup"><span data-stu-id="d5ca2-228">Next steps</span></span>

* <span data-ttu-id="d5ca2-229">For an example on creating subscriptions using .NET, see [sample code on GitHub](https://github.com/Azure-Samples/create-azure-subscription-dotnet-core).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-229">For an example on creating subscriptions using .NET, see [sample code on GitHub](https://github.com/Azure-Samples/create-azure-subscription-dotnet-core).</span></span>
* <span data-ttu-id="d5ca2-230">Now that you've created a subscription, you can grant that ability to other users and service principals.</span><span class="sxs-lookup"><span data-stu-id="d5ca2-230">Now that you've created a subscription, you can grant that ability to other users and service principals.</span></span> <span data-ttu-id="d5ca2-231">For more information, see [Grant access to create Azure Enterprise subscriptions (preview)](grant-access-to-create-subscription.md).</span><span class="sxs-lookup"><span data-stu-id="d5ca2-231">For more information, see [Grant access to create Azure Enterprise subscriptions (preview)](grant-access-to-create-subscription.md).</span></span>
* <span data-ttu-id="d5ca2-232">To learn more about managing large numbers of subscriptions using management groups, see [Organize your resources with Azure management groups](management-groups-overview.md)</span><span class="sxs-lookup"><span data-stu-id="d5ca2-232">To learn more about managing large numbers of subscriptions using management groups, see [Organize your resources with Azure management groups](management-groups-overview.md)</span></span>
