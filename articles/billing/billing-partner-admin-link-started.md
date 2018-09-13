---
title: Link Azure account to partner ID | Microsoft Docs
description: Track engagements with Azure customers by linking partner ID to the user account that you use to manage the customer's resources.
services: billing
author: dhirajgandhi
ms.author: dhgandhi
ms.date: 03/12/2018
ms.service: billing
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: na
ms.openlocfilehash: a48298668e2297cb95f2a2f16eac6387ff509781
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871282"
---
# <a name="link-partner-id-to-your-azure-accounts"></a><span data-ttu-id="f21af-103">Link partner ID to your Azure accounts</span><span class="sxs-lookup"><span data-stu-id="f21af-103">Link partner ID to your Azure accounts</span></span>

<span data-ttu-id="f21af-104">As a partner, you can track your impact across your customer engagements by linking your partner ID to the accounts used for managing customer's resources.</span><span class="sxs-lookup"><span data-stu-id="f21af-104">As a partner, you can track your impact across your customer engagements by linking your partner ID to the accounts used for managing customer's resources.</span></span>

<span data-ttu-id="f21af-105">This feature is available in a public preview.</span><span class="sxs-lookup"><span data-stu-id="f21af-105">This feature is available in a public preview.</span></span>

## <a name="get-access-from-your-customer"></a><span data-ttu-id="f21af-106">Get access from your customer</span><span class="sxs-lookup"><span data-stu-id="f21af-106">Get access from your customer</span></span>

<span data-ttu-id="f21af-107">Before you link your partner ID, your customer must give you access to their Azure resources by using one of the following options:</span><span class="sxs-lookup"><span data-stu-id="f21af-107">Before you link your partner ID, your customer must give you access to their Azure resources by using one of the following options:</span></span>

- <span data-ttu-id="f21af-108">**Guest user:** Your customer can add you as a guest user and assign any RBAC roles.</span><span class="sxs-lookup"><span data-stu-id="f21af-108">**Guest user:** Your customer can add you as a guest user and assign any RBAC roles.</span></span> <span data-ttu-id="f21af-109">For more information, see [Add guest users from another directory](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b).</span><span class="sxs-lookup"><span data-stu-id="f21af-109">For more information, see [Add guest users from another directory](https://docs.microsoft.com/azure/active-directory/active-directory-b2b-what-is-azure-ad-b2b).</span></span>

- <span data-ttu-id="f21af-110">**Directory account:**  Your customer can create a new user from your organization in their directory and assign any RBAC role.</span><span class="sxs-lookup"><span data-stu-id="f21af-110">**Directory account:**  Your customer can create a new user from your organization in their directory and assign any RBAC role.</span></span>

- <span data-ttu-id="f21af-111">**Service principal:**  Your customer can add an app or script from your organization in their directory and assign any RBAC role.</span><span class="sxs-lookup"><span data-stu-id="f21af-111">**Service principal:**  Your customer can add an app or script from your organization in their directory and assign any RBAC role.</span></span> <span data-ttu-id="f21af-112">The identity of the app or script is known as service principal.</span><span class="sxs-lookup"><span data-stu-id="f21af-112">The identity of the app or script is known as service principal.</span></span>

## <a name="link-partner-id"></a><span data-ttu-id="f21af-113">Link partner ID</span><span class="sxs-lookup"><span data-stu-id="f21af-113">Link partner ID</span></span>

<span data-ttu-id="f21af-114">When you have access to the customer's resources, use Azure portal, PowerShell, or CLI to link your Microsoft Partner Network ID (MPN ID) to your user ID or service principal.</span><span class="sxs-lookup"><span data-stu-id="f21af-114">When you have access to the customer's resources, use Azure portal, PowerShell, or CLI to link your Microsoft Partner Network ID (MPN ID) to your user ID or service principal.</span></span> <span data-ttu-id="f21af-115">You have to link the partner ID in each customer tenant.</span><span class="sxs-lookup"><span data-stu-id="f21af-115">You have to link the partner ID in each customer tenant.</span></span>

### <a name="use-azure-portal-to-link-new-partner-id"></a><span data-ttu-id="f21af-116">Use Azure portal to link new partner ID</span><span class="sxs-lookup"><span data-stu-id="f21af-116">Use Azure portal to link new partner ID</span></span>

1. <span data-ttu-id="f21af-117">Go to [link to a partner ID](https://portal.azure.com/#blade/Microsoft_Azure_Billing/managementpartnerblade) in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f21af-117">Go to [link to a partner ID](https://portal.azure.com/#blade/Microsoft_Azure_Billing/managementpartnerblade) in the Azure portal.</span></span>

2. <span data-ttu-id="f21af-118">Sign in to the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f21af-118">Sign in to the Azure portal.</span></span>

3. <span data-ttu-id="f21af-119">Enter the Microsoft partner ID.The partner ID is the [Microsoft Partner Network(MPN)](https://partner.microsoft.com/) ID of your organization.</span><span class="sxs-lookup"><span data-stu-id="f21af-119">Enter the Microsoft partner ID.The partner ID is the [Microsoft Partner Network(MPN)](https://partner.microsoft.com/) ID of your organization.</span></span>

  ![Screenshot that shows link partner ID](./media/billing-link-partner-id/link-partner-ID.PNG)

4. <span data-ttu-id="f21af-121">To link partner ID for another customer, use the directory switcher.</span><span class="sxs-lookup"><span data-stu-id="f21af-121">To link partner ID for another customer, use the directory switcher.</span></span> <span data-ttu-id="f21af-122">Under Switch directory, choose your directory.</span><span class="sxs-lookup"><span data-stu-id="f21af-122">Under Switch directory, choose your directory.</span></span>

  ![Screenshot that shows link partner ID](./media/billing-link-partner-id/directory-switcher.png)

### <a name="use-powershell-to-link-new-partner-id"></a><span data-ttu-id="f21af-124">Use PowerShell to link new partner ID</span><span class="sxs-lookup"><span data-stu-id="f21af-124">Use PowerShell to link new partner ID</span></span>

1. <span data-ttu-id="f21af-125">Install the [AzureRM.ManagementPartner](https://www.powershellgallery.com/packages/AzureRM.ManagementPartner) PowerShell Module.</span><span class="sxs-lookup"><span data-stu-id="f21af-125">Install the [AzureRM.ManagementPartner](https://www.powershellgallery.com/packages/AzureRM.ManagementPartner) PowerShell Module.</span></span>

2. <span data-ttu-id="f21af-126">Sign in to the customer's tenant either with the user account or service principal, For more information, see [Login with Powershell](https://docs.microsoft.com/powershell/azure/authenticate-azureps?view=azurermps-5.2.0).</span><span class="sxs-lookup"><span data-stu-id="f21af-126">Sign in to the customer's tenant either with the user account or service principal, For more information, see [Login with Powershell](https://docs.microsoft.com/powershell/azure/authenticate-azureps?view=azurermps-5.2.0).</span></span>
 
   ```azurepowershell-interactive
    C:\> Connect-AzureRmAccount -TenantId XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX 
   ```


3. <span data-ttu-id="f21af-127">Link the new partner ID.</span><span class="sxs-lookup"><span data-stu-id="f21af-127">Link the new partner ID.</span></span> <span data-ttu-id="f21af-128">The partner ID is the [Microsoft Partner Network(MPN)](https://partner.microsoft.com/) ID of your organization.</span><span class="sxs-lookup"><span data-stu-id="f21af-128">The partner ID is the [Microsoft Partner Network(MPN)](https://partner.microsoft.com/) ID of your organization.</span></span>

    ```azurepowershell-interactive
    C:\> new-AzureRmManagementPartner -PartnerId 12345 
    ```

#### <a name="get-the-linked-partner-id"></a><span data-ttu-id="f21af-129">Get the linked partner ID</span><span class="sxs-lookup"><span data-stu-id="f21af-129">Get the linked partner ID</span></span>
```azurepowershell-interactive
C:\> get-AzureRmManagementPartner 
```

#### <a name="update-the-linked-partner-id"></a><span data-ttu-id="f21af-130">Update the linked partner ID</span><span class="sxs-lookup"><span data-stu-id="f21af-130">Update the linked partner ID</span></span>
```azurepowershell-interactive
C:\> Update-AzureRmManagementPartner -PartnerId 12345 
```
#### <a name="delete-the-linked-partner-id"></a><span data-ttu-id="f21af-131">Delete the linked partner ID</span><span class="sxs-lookup"><span data-stu-id="f21af-131">Delete the linked partner ID</span></span>
```azurepowershell-interactive
C:\> remove-AzureRmManagementPartner -PartnerId 12345 
```

### <a name="use-cli-to-link-new-partner-id"></a><span data-ttu-id="f21af-132">Use CLI to link new partner ID</span><span class="sxs-lookup"><span data-stu-id="f21af-132">Use CLI to link new partner ID</span></span>
1.  <span data-ttu-id="f21af-133">Install the CLI Extension.</span><span class="sxs-lookup"><span data-stu-id="f21af-133">Install the CLI Extension.</span></span>

    ```azurecli-interactive
    C:\ az extension add --name managementpartner
    ``` 

2.  <span data-ttu-id="f21af-134">Sign in to the customer's tenant with the user account or service principal.</span><span class="sxs-lookup"><span data-stu-id="f21af-134">Sign in to the customer's tenant with the user account or service principal.</span></span> <span data-ttu-id="f21af-135">For more information, see [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest).</span><span class="sxs-lookup"><span data-stu-id="f21af-135">For more information, see [Log in with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest).</span></span>

    ```azurecli-interactive
    C:\ az login --tenant <tenant>
    ``` 

3.  <span data-ttu-id="f21af-136">Link the new partner ID.</span><span class="sxs-lookup"><span data-stu-id="f21af-136">Link the new partner ID.</span></span> <span data-ttu-id="f21af-137">The partner ID is the [Microsoft Partner Network(MPN)](https://partner.microsoft.com/) ID of your organization.</span><span class="sxs-lookup"><span data-stu-id="f21af-137">The partner ID is the [Microsoft Partner Network(MPN)](https://partner.microsoft.com/) ID of your organization.</span></span>

     ```azurecli-interactive
     C:\ az managementpartner create --partner-id 12345
      ```  

#### <a name="get-the-linked-partner-id"></a><span data-ttu-id="f21af-138">Get the linked partner ID</span><span class="sxs-lookup"><span data-stu-id="f21af-138">Get the linked partner ID</span></span>
```azurecli-interactive
C:\ az managementpartner show
``` 

#### <a name="update-the-linked-partner-id"></a><span data-ttu-id="f21af-139">Update the linked partner ID</span><span class="sxs-lookup"><span data-stu-id="f21af-139">Update the linked partner ID</span></span>
```azurecli-interactive
C:\ az managementpartner update --partner-id 12345
``` 

#### <a name="delete-the-linked-partner-id"></a><span data-ttu-id="f21af-140">Delete the linked partner ID</span><span class="sxs-lookup"><span data-stu-id="f21af-140">Delete the linked partner ID</span></span>
```azurecli-interactive
C:\ az managementpartner delete --partner-id 12345
``` 

## <a name="next-steps"></a><span data-ttu-id="f21af-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="f21af-141">Next steps</span></span>

<span data-ttu-id="f21af-142">Join the discussion in the [Microsoft Partner Community](https://aka.ms/PALdiscussion) to receive updates or send feedback.</span><span class="sxs-lookup"><span data-stu-id="f21af-142">Join the discussion in the [Microsoft Partner Community](https://aka.ms/PALdiscussion) to receive updates or send feedback.</span></span>

## <a name="frequently-asked-questions"></a><span data-ttu-id="f21af-143">Frequently Asked Questions</span><span class="sxs-lookup"><span data-stu-id="f21af-143">Frequently Asked Questions</span></span>

<span data-ttu-id="f21af-144">**Who can link the partner ID?**</span><span class="sxs-lookup"><span data-stu-id="f21af-144">**Who can link the partner ID?**</span></span>

<span data-ttu-id="f21af-145">Any user from the partner organization who is managing customer's resource can link the partner ID to the account.</span><span class="sxs-lookup"><span data-stu-id="f21af-145">Any user from the partner organization who is managing customer's resource can link the partner ID to the account.</span></span>

<span data-ttu-id="f21af-146">**Once a partner ID is linked can it be changed?**</span><span class="sxs-lookup"><span data-stu-id="f21af-146">**Once a partner ID is linked can it be changed?**</span></span>

<span data-ttu-id="f21af-147">Yes, linked partner ID can be changed, added, or removed.</span><span class="sxs-lookup"><span data-stu-id="f21af-147">Yes, linked partner ID can be changed, added, or removed.</span></span>

<span data-ttu-id="f21af-148">**What if a user has an account in multiple customer tenants?**</span><span class="sxs-lookup"><span data-stu-id="f21af-148">**What if a user has an account in multiple customer tenants?**</span></span>

<span data-ttu-id="f21af-149">The link between the partner ID and the account is done for each customer tenant.</span><span class="sxs-lookup"><span data-stu-id="f21af-149">The link between the partner ID and the account is done for each customer tenant.</span></span>  <span data-ttu-id="f21af-150">You have to link the partner ID in each customer tenant.</span><span class="sxs-lookup"><span data-stu-id="f21af-150">You have to link the partner ID in each customer tenant.</span></span>

<span data-ttu-id="f21af-151">**Can other partner or customer edit or remove the link to the partner ID?**</span><span class="sxs-lookup"><span data-stu-id="f21af-151">**Can other partner or customer edit or remove the link to the partner ID?**</span></span>

<span data-ttu-id="f21af-152">The link is associated at the account level.</span><span class="sxs-lookup"><span data-stu-id="f21af-152">The link is associated at the account level.</span></span> <span data-ttu-id="f21af-153">Only you can edit or remove the link to the partner ID.</span><span class="sxs-lookup"><span data-stu-id="f21af-153">Only you can edit or remove the link to the partner ID.</span></span> <span data-ttu-id="f21af-154">The customer and other partner can't change the link to the partner ID.</span><span class="sxs-lookup"><span data-stu-id="f21af-154">The customer and other partner can't change the link to the partner ID.</span></span> 
