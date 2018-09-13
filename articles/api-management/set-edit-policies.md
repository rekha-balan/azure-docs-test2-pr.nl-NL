---
title: How to set or edit Azure API Management policies | Microsoft Docs
description: This topic shows how to set or edit Azure API Management policies.
services: api-management
documentationcenter: ''
author: vladvino
manager: cflower
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/27/2017
ms.author: apimpm
ms.openlocfilehash: aaf86a440328e27c8c47b809536951eeaf2104b9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968676"
---
# <a name="how-to-set-or-edit-azure-api-management-policies"></a><span data-ttu-id="0c78b-103">How to set or edit Azure API Management policies</span><span class="sxs-lookup"><span data-stu-id="0c78b-103">How to set or edit Azure API Management policies</span></span>

<span data-ttu-id="0c78b-104">The policy definition is an XML document that describes a sequence of inbound and outbound statements.</span><span class="sxs-lookup"><span data-stu-id="0c78b-104">The policy definition is an XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="0c78b-105">The XML can be edited directly in the definition window.</span><span class="sxs-lookup"><span data-stu-id="0c78b-105">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="0c78b-106">You can also select a predefined policy from the list that is provided to the right of the policy window.</span><span class="sxs-lookup"><span data-stu-id="0c78b-106">You can also select a predefined policy from the list that is provided to the right of the policy window.</span></span> <span data-ttu-id="0c78b-107">The statements applicable to the current scope are enabled and highlighted.</span><span class="sxs-lookup"><span data-stu-id="0c78b-107">The statements applicable to the current scope are enabled and highlighted.</span></span> <span data-ttu-id="0c78b-108">Clicking an enabled statement adds the appropriate XML at the location of the cursor in the definition view.</span><span class="sxs-lookup"><span data-stu-id="0c78b-108">Clicking an enabled statement adds the appropriate XML at the location of the cursor in the definition view.</span></span> 

<span data-ttu-id="0c78b-109">For detailed information about policies, see [Policies in Azure API Management](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="0c78b-109">For detailed information about policies, see [Policies in Azure API Management](api-management-howto-policies.md).</span></span>

## <a name="set-or-edit-a-policy"></a><span data-ttu-id="0c78b-110">Set or edit a policy</span><span class="sxs-lookup"><span data-stu-id="0c78b-110">Set or edit a policy</span></span>

<span data-ttu-id="0c78b-111">To set or edit a policy, follow the following steps:</span><span class="sxs-lookup"><span data-stu-id="0c78b-111">To set or edit a policy, follow the following steps:</span></span>

1. <span data-ttu-id="0c78b-112">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0c78b-112">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>
2. <span data-ttu-id="0c78b-113">Browse to your APIM instance.</span><span class="sxs-lookup"><span data-stu-id="0c78b-113">Browse to your APIM instance.</span></span>
3. <span data-ttu-id="0c78b-114">Click the **APIs** tab.</span><span class="sxs-lookup"><span data-stu-id="0c78b-114">Click the **APIs** tab.</span></span>
4. <span data-ttu-id="0c78b-115">Select one of the APIs that you previously imported.</span><span class="sxs-lookup"><span data-stu-id="0c78b-115">Select one of the APIs that you previously imported.</span></span>
5. <span data-ttu-id="0c78b-116">Select the **Design** tab.</span><span class="sxs-lookup"><span data-stu-id="0c78b-116">Select the **Design** tab.</span></span>
6. <span data-ttu-id="0c78b-117">Select an operation to which you want to apply the policy.</span><span class="sxs-lookup"><span data-stu-id="0c78b-117">Select an operation to which you want to apply the policy.</span></span> <span data-ttu-id="0c78b-118">If you want to apply the policy to all operations, select **All operations**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-118">If you want to apply the policy to all operations, select **All operations**.</span></span>
7. <span data-ttu-id="0c78b-119">Click the triangle next to the **inbound** or **outbound** pencils.</span><span class="sxs-lookup"><span data-stu-id="0c78b-119">Click the triangle next to the **inbound** or **outbound** pencils.</span></span>
8. <span data-ttu-id="0c78b-120">Select the **Code editor** item.</span><span class="sxs-lookup"><span data-stu-id="0c78b-120">Select the **Code editor** item.</span></span>

    ![Edit policy](./media/set-edit-policies/set-edit-policies01.png)

9. <span data-ttu-id="0c78b-122">Paste the desired policy code into one of the appropriate blocks.</span><span class="sxs-lookup"><span data-stu-id="0c78b-122">Paste the desired policy code into one of the appropriate blocks.</span></span>
         
        <policies>
             <inbound>
                 <base />
             </inbound>
             <backend>
                 <base />
             </backend>
             <outbound>
                 <base />
             </outbound>
             <on-error>
                 <base />
             </on-error>
         </policies>
 
## <a name="configure-scope"></a><span data-ttu-id="0c78b-123">Configure scope</span><span class="sxs-lookup"><span data-stu-id="0c78b-123">Configure scope</span></span>

<span data-ttu-id="0c78b-124">Policies can be configured globally or at the scope of a Product, API, or Operation.</span><span class="sxs-lookup"><span data-stu-id="0c78b-124">Policies can be configured globally or at the scope of a Product, API, or Operation.</span></span> <span data-ttu-id="0c78b-125">To begin configuring a policy, you must first select the scope at which the policy should apply.</span><span class="sxs-lookup"><span data-stu-id="0c78b-125">To begin configuring a policy, you must first select the scope at which the policy should apply.</span></span>

<span data-ttu-id="0c78b-126">Policy scopes are evaluated in the following order:</span><span class="sxs-lookup"><span data-stu-id="0c78b-126">Policy scopes are evaluated in the following order:</span></span>

1. <span data-ttu-id="0c78b-127">Global scope</span><span class="sxs-lookup"><span data-stu-id="0c78b-127">Global scope</span></span>
2. <span data-ttu-id="0c78b-128">Product scope</span><span class="sxs-lookup"><span data-stu-id="0c78b-128">Product scope</span></span>
3. <span data-ttu-id="0c78b-129">API scope</span><span class="sxs-lookup"><span data-stu-id="0c78b-129">API scope</span></span>
4. <span data-ttu-id="0c78b-130">Operation scope</span><span class="sxs-lookup"><span data-stu-id="0c78b-130">Operation scope</span></span>

<span data-ttu-id="0c78b-131">The statements within policies are evaluated according to the placement of the `base` element, if it is present.</span><span class="sxs-lookup"><span data-stu-id="0c78b-131">The statements within policies are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="0c78b-132">Global policy has no parent policy and using the `<base>` element in it has no effect.</span><span class="sxs-lookup"><span data-stu-id="0c78b-132">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="0c78b-133">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-133">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

### <a name="global-scope"></a><span data-ttu-id="0c78b-134">Global scope</span><span class="sxs-lookup"><span data-stu-id="0c78b-134">Global scope</span></span>

<span data-ttu-id="0c78b-135">Global scope is configured for **All APIs** in your APIM instance.</span><span class="sxs-lookup"><span data-stu-id="0c78b-135">Global scope is configured for **All APIs** in your APIM instance.</span></span>

1. <span data-ttu-id="0c78b-136">Sign in to the [Azure portal](https://portal.azure.com/) and navigate to your APIM instance.</span><span class="sxs-lookup"><span data-stu-id="0c78b-136">Sign in to the [Azure portal](https://portal.azure.com/) and navigate to your APIM instance.</span></span>
2. <span data-ttu-id="0c78b-137">Click **All APIs**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-137">Click **All APIs**.</span></span>

    ![Global scope](./media/api-management-howto-policies/global-scope.png)

3. <span data-ttu-id="0c78b-139">Click the triangle icon.</span><span class="sxs-lookup"><span data-stu-id="0c78b-139">Click the triangle icon.</span></span>
4. <span data-ttu-id="0c78b-140">Select **Code editor**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-140">Select **Code editor**.</span></span>
5. <span data-ttu-id="0c78b-141">Add or edit policies.</span><span class="sxs-lookup"><span data-stu-id="0c78b-141">Add or edit policies.</span></span>
6. <span data-ttu-id="0c78b-142">Press **Save**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-142">Press **Save**.</span></span> 

    <span data-ttu-id="0c78b-143">The changes are propagated to the API Management gateway immediately.</span><span class="sxs-lookup"><span data-stu-id="0c78b-143">The changes are propagated to the API Management gateway immediately.</span></span>

### <a name="product-scope"></a><span data-ttu-id="0c78b-144">Product scope</span><span class="sxs-lookup"><span data-stu-id="0c78b-144">Product scope</span></span>

<span data-ttu-id="0c78b-145">Product scope is configured for the selected product.</span><span class="sxs-lookup"><span data-stu-id="0c78b-145">Product scope is configured for the selected product.</span></span>

1. <span data-ttu-id="0c78b-146">Click **Products**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-146">Click **Products**.</span></span>

    ![Product scope](./media/api-management-howto-policies/product-scope.png)

2. <span data-ttu-id="0c78b-148">Select the product to which you want to apply policies.</span><span class="sxs-lookup"><span data-stu-id="0c78b-148">Select the product to which you want to apply policies.</span></span>
3. <span data-ttu-id="0c78b-149">Click **Policies**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-149">Click **Policies**.</span></span>
4. <span data-ttu-id="0c78b-150">Add or edit policies.</span><span class="sxs-lookup"><span data-stu-id="0c78b-150">Add or edit policies.</span></span>
5. <span data-ttu-id="0c78b-151">Press **Save**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-151">Press **Save**.</span></span> 

### <a name="api-scope"></a><span data-ttu-id="0c78b-152">API scope</span><span class="sxs-lookup"><span data-stu-id="0c78b-152">API scope</span></span>

<span data-ttu-id="0c78b-153">API scope is configured for **All Operations** of the selected API.</span><span class="sxs-lookup"><span data-stu-id="0c78b-153">API scope is configured for **All Operations** of the selected API.</span></span>

1. <span data-ttu-id="0c78b-154">Select the **API** you want to apply policies to.</span><span class="sxs-lookup"><span data-stu-id="0c78b-154">Select the **API** you want to apply policies to.</span></span>

    ![API scope](./media/api-management-howto-policies/api-scope.png)

2. <span data-ttu-id="0c78b-156">Select **All operations**</span><span class="sxs-lookup"><span data-stu-id="0c78b-156">Select **All operations**</span></span>
3. <span data-ttu-id="0c78b-157">Click the triangle icon.</span><span class="sxs-lookup"><span data-stu-id="0c78b-157">Click the triangle icon.</span></span>
4. <span data-ttu-id="0c78b-158">Select **Code editor**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-158">Select **Code editor**.</span></span>
5. <span data-ttu-id="0c78b-159">Add or edit policies.</span><span class="sxs-lookup"><span data-stu-id="0c78b-159">Add or edit policies.</span></span>
6. <span data-ttu-id="0c78b-160">Press **Save**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-160">Press **Save**.</span></span> 

### <a name="operation-scope"></a><span data-ttu-id="0c78b-161">Operation scope</span><span class="sxs-lookup"><span data-stu-id="0c78b-161">Operation scope</span></span> 

<span data-ttu-id="0c78b-162">Operation scope is configured for the selected operation.</span><span class="sxs-lookup"><span data-stu-id="0c78b-162">Operation scope is configured for the selected operation.</span></span>

1. <span data-ttu-id="0c78b-163">Select an **API**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-163">Select an **API**.</span></span>
2. <span data-ttu-id="0c78b-164">Select the operation you want to apply policies to.</span><span class="sxs-lookup"><span data-stu-id="0c78b-164">Select the operation you want to apply policies to.</span></span>

    ![Operation scope](./media/api-management-howto-policies/operation-scope.png)

3. <span data-ttu-id="0c78b-166">Click the triangle icon.</span><span class="sxs-lookup"><span data-stu-id="0c78b-166">Click the triangle icon.</span></span>
4. <span data-ttu-id="0c78b-167">Select **Code editor**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-167">Select **Code editor**.</span></span>
5. <span data-ttu-id="0c78b-168">Add or edit policies.</span><span class="sxs-lookup"><span data-stu-id="0c78b-168">Add or edit policies.</span></span>
6. <span data-ttu-id="0c78b-169">Press **Save**.</span><span class="sxs-lookup"><span data-stu-id="0c78b-169">Press **Save**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="0c78b-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="0c78b-170">Next steps</span></span>

<span data-ttu-id="0c78b-171">See the following related topics:</span><span class="sxs-lookup"><span data-stu-id="0c78b-171">See the following related topics:</span></span>

+ [<span data-ttu-id="0c78b-172">Transform APIs</span><span class="sxs-lookup"><span data-stu-id="0c78b-172">Transform APIs</span></span>](transform-api.md)
+ <span data-ttu-id="0c78b-173">[Policy Reference](api-management-policy-reference.md) for a full list of policy statements and their settings</span><span class="sxs-lookup"><span data-stu-id="0c78b-173">[Policy Reference](api-management-policy-reference.md) for a full list of policy statements and their settings</span></span>
+ [<span data-ttu-id="0c78b-174">Policy samples</span><span class="sxs-lookup"><span data-stu-id="0c78b-174">Policy samples</span></span>](policy-samples.md)