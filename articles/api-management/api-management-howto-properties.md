---
title: How to use Named Values in Azure API Management policies
description: Learn how to use Named Values in Azure API Management policies.
services: api-management
documentationcenter: ''
author: vladvino
manager: erikre
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/25/2018
ms.author: apimpm
ms.openlocfilehash: 829d6bc6cb3f8e78d065d7aaca4937634e7349c8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826111"
---
# <a name="how-to-use-named-values-in-azure-api-management-policies"></a><span data-ttu-id="b1bec-103">How to use Named Values in Azure API Management policies</span><span class="sxs-lookup"><span data-stu-id="b1bec-103">How to use Named Values in Azure API Management policies</span></span>
<span data-ttu-id="b1bec-104">API Management policies are a powerful capability of the system that allow the Azure portal to change the behavior of the API through configuration.</span><span class="sxs-lookup"><span data-stu-id="b1bec-104">API Management policies are a powerful capability of the system that allow the Azure portal to change the behavior of the API through configuration.</span></span> <span data-ttu-id="b1bec-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span><span class="sxs-lookup"><span data-stu-id="b1bec-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="b1bec-106">Policy statements can be constructed using literal text values, policy expressions, and named values.</span><span class="sxs-lookup"><span data-stu-id="b1bec-106">Policy statements can be constructed using literal text values, policy expressions, and named values.</span></span> 

<span data-ttu-id="b1bec-107">Each API Management service instance has a properties collection of key/value pairs, which is called Named Values, that are global to the service instance.</span><span class="sxs-lookup"><span data-stu-id="b1bec-107">Each API Management service instance has a properties collection of key/value pairs, which is called Named Values, that are global to the service instance.</span></span> <span data-ttu-id="b1bec-108">These Named Values can be used to manage constant string values across all API configuration and policies.</span><span class="sxs-lookup"><span data-stu-id="b1bec-108">These Named Values can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="b1bec-109">Each property can have the following attributes:</span><span class="sxs-lookup"><span data-stu-id="b1bec-109">Each property can have the following attributes:</span></span>

| <span data-ttu-id="b1bec-110">Attribute</span><span class="sxs-lookup"><span data-stu-id="b1bec-110">Attribute</span></span> | <span data-ttu-id="b1bec-111">Type</span><span class="sxs-lookup"><span data-stu-id="b1bec-111">Type</span></span> | <span data-ttu-id="b1bec-112">Description</span><span class="sxs-lookup"><span data-stu-id="b1bec-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="b1bec-113">Display name</span><span class="sxs-lookup"><span data-stu-id="b1bec-113">Display name</span></span> |<span data-ttu-id="b1bec-114">string</span><span class="sxs-lookup"><span data-stu-id="b1bec-114">string</span></span> |<span data-ttu-id="b1bec-115">Alphanumeric string used for referencing the property in the policies.</span><span class="sxs-lookup"><span data-stu-id="b1bec-115">Alphanumeric string used for referencing the property in the policies.</span></span> |
| <span data-ttu-id="b1bec-116">Value</span><span class="sxs-lookup"><span data-stu-id="b1bec-116">Value</span></span> |<span data-ttu-id="b1bec-117">string</span><span class="sxs-lookup"><span data-stu-id="b1bec-117">string</span></span> |<span data-ttu-id="b1bec-118">The value of the property.</span><span class="sxs-lookup"><span data-stu-id="b1bec-118">The value of the property.</span></span> <span data-ttu-id="b1bec-119">It may not be empty or consist only of whitespace.</span><span class="sxs-lookup"><span data-stu-id="b1bec-119">It may not be empty or consist only of whitespace.</span></span> |
|<span data-ttu-id="b1bec-120">Secret</span><span class="sxs-lookup"><span data-stu-id="b1bec-120">Secret</span></span>|<span data-ttu-id="b1bec-121">boolean</span><span class="sxs-lookup"><span data-stu-id="b1bec-121">boolean</span></span>|<span data-ttu-id="b1bec-122">Determines whether the value is a secret and should be encrypted or not.</span><span class="sxs-lookup"><span data-stu-id="b1bec-122">Determines whether the value is a secret and should be encrypted or not.</span></span>|
| <span data-ttu-id="b1bec-123">Tags</span><span class="sxs-lookup"><span data-stu-id="b1bec-123">Tags</span></span> |<span data-ttu-id="b1bec-124">array of string</span><span class="sxs-lookup"><span data-stu-id="b1bec-124">array of string</span></span> |<span data-ttu-id="b1bec-125">Optional tags that when provided can be used to filter the property list.</span><span class="sxs-lookup"><span data-stu-id="b1bec-125">Optional tags that when provided can be used to filter the property list.</span></span> |

![Named values](./media/api-management-howto-properties/named-values.png)

<span data-ttu-id="b1bec-127">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1bec-127">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="b1bec-128">For example, the value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span><span class="sxs-lookup"><span data-stu-id="b1bec-128">For example, the value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="b1bec-129">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span><span class="sxs-lookup"><span data-stu-id="b1bec-129">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="b1bec-130">Name</span><span class="sxs-lookup"><span data-stu-id="b1bec-130">Name</span></span> | <span data-ttu-id="b1bec-131">Value</span><span class="sxs-lookup"><span data-stu-id="b1bec-131">Value</span></span> | <span data-ttu-id="b1bec-132">Secret</span><span class="sxs-lookup"><span data-stu-id="b1bec-132">Secret</span></span> | <span data-ttu-id="b1bec-133">Tags</span><span class="sxs-lookup"><span data-stu-id="b1bec-133">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b1bec-134">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="b1bec-134">ContosoHeader</span></span> |<span data-ttu-id="b1bec-135">TrackingId</span><span class="sxs-lookup"><span data-stu-id="b1bec-135">TrackingId</span></span> |<span data-ttu-id="b1bec-136">False</span><span class="sxs-lookup"><span data-stu-id="b1bec-136">False</span></span> |<span data-ttu-id="b1bec-137">Contoso</span><span class="sxs-lookup"><span data-stu-id="b1bec-137">Contoso</span></span> |
| <span data-ttu-id="b1bec-138">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="b1bec-138">ContosoHeaderValue</span></span> |<span data-ttu-id="b1bec-139">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="b1bec-139">••••••••••••••••••••••</span></span> |<span data-ttu-id="b1bec-140">True</span><span class="sxs-lookup"><span data-stu-id="b1bec-140">True</span></span> |<span data-ttu-id="b1bec-141">Contoso</span><span class="sxs-lookup"><span data-stu-id="b1bec-141">Contoso</span></span> |
| <span data-ttu-id="b1bec-142">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="b1bec-142">ExpressionProperty</span></span> |<span data-ttu-id="b1bec-143">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="b1bec-143">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="b1bec-144">False</span><span class="sxs-lookup"><span data-stu-id="b1bec-144">False</span></span> | |

## <a name="to-add-and-edit-a-property"></a><span data-ttu-id="b1bec-145">To add and edit a property</span><span class="sxs-lookup"><span data-stu-id="b1bec-145">To add and edit a property</span></span>

![Add a property](./media/api-management-howto-properties/add-property.png)

1. <span data-ttu-id="b1bec-147">Select **APIs** from under **API MANAGEMENT**.</span><span class="sxs-lookup"><span data-stu-id="b1bec-147">Select **APIs** from under **API MANAGEMENT**.</span></span>
2. <span data-ttu-id="b1bec-148">Select **Named values**.</span><span class="sxs-lookup"><span data-stu-id="b1bec-148">Select **Named values**.</span></span>
3. <span data-ttu-id="b1bec-149">Press **+Add**.</span><span class="sxs-lookup"><span data-stu-id="b1bec-149">Press **+Add**.</span></span>

  <span data-ttu-id="b1bec-150">Name and Value are required values.</span><span class="sxs-lookup"><span data-stu-id="b1bec-150">Name and Value are required values.</span></span> <span data-ttu-id="b1bec-151">If this property value is a secret, check the This is a secret checkbox.</span><span class="sxs-lookup"><span data-stu-id="b1bec-151">If this property value is a secret, check the This is a secret checkbox.</span></span> <span data-ttu-id="b1bec-152">Enter one or more optional tags to help with organizing your named values, and click Save.</span><span class="sxs-lookup"><span data-stu-id="b1bec-152">Enter one or more optional tags to help with organizing your named values, and click Save.</span></span>
4. <span data-ttu-id="b1bec-153">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="b1bec-153">Click **Create**.</span></span>

<span data-ttu-id="b1bec-154">Once the property is created, you can edit it by clicking on the property.</span><span class="sxs-lookup"><span data-stu-id="b1bec-154">Once the property is created, you can edit it by clicking on the property.</span></span> <span data-ttu-id="b1bec-155">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span><span class="sxs-lookup"><span data-stu-id="b1bec-155">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

<span data-ttu-id="b1bec-156">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="b1bec-156">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="b1bec-157">To delete a property</span><span class="sxs-lookup"><span data-stu-id="b1bec-157">To delete a property</span></span>

<span data-ttu-id="b1bec-158">To delete a property, click **Delete** beside the property to delete.</span><span class="sxs-lookup"><span data-stu-id="b1bec-158">To delete a property, click **Delete** beside the property to delete.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b1bec-159">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span><span class="sxs-lookup"><span data-stu-id="b1bec-159">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="b1bec-160">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="b1bec-160">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-named-values"></a><span data-ttu-id="b1bec-161">To search and filter Named Values</span><span class="sxs-lookup"><span data-stu-id="b1bec-161">To search and filter Named Values</span></span>

<span data-ttu-id="b1bec-162">The **Named values** tab includes searching and filtering capabilities to help you manage your named values.</span><span class="sxs-lookup"><span data-stu-id="b1bec-162">The **Named values** tab includes searching and filtering capabilities to help you manage your named values.</span></span> <span data-ttu-id="b1bec-163">To filter the property list by property name, enter a search term in the **Search property** textbox.</span><span class="sxs-lookup"><span data-stu-id="b1bec-163">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="b1bec-164">To display all named values, clear the **Search property** textbox and press enter.</span><span class="sxs-lookup"><span data-stu-id="b1bec-164">To display all named values, clear the **Search property** textbox and press enter.</span></span>

<span data-ttu-id="b1bec-165">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span><span class="sxs-lookup"><span data-stu-id="b1bec-165">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="b1bec-166">To display all named values, clear the **Filter by tags** textbox and press enter.</span><span class="sxs-lookup"><span data-stu-id="b1bec-166">To display all named values, clear the **Filter by tags** textbox and press enter.</span></span>

## <a name="to-use-a-property"></a><span data-ttu-id="b1bec-167">To use a property</span><span class="sxs-lookup"><span data-stu-id="b1bec-167">To use a property</span></span>

<span data-ttu-id="b1bec-168">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="b1bec-168">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example:</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="b1bec-169">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span><span class="sxs-lookup"><span data-stu-id="b1bec-169">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="b1bec-170">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span><span class="sxs-lookup"><span data-stu-id="b1bec-170">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="b1bec-171">Named values can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="b1bec-171">Named values can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="b1bec-172">Named values can also contain policy expressions.</span><span class="sxs-lookup"><span data-stu-id="b1bec-172">Named values can also contain policy expressions.</span></span> <span data-ttu-id="b1bec-173">In the following example, the `ExpressionProperty` is used.</span><span class="sxs-lookup"><span data-stu-id="b1bec-173">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="b1bec-174">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="b1bec-174">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="b1bec-175">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span><span class="sxs-lookup"><span data-stu-id="b1bec-175">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="b1bec-176">You can test this out in the developer portal by calling an operation that has a policy with named values in scope.</span><span class="sxs-lookup"><span data-stu-id="b1bec-176">You can test this out in the developer portal by calling an operation that has a policy with named values in scope.</span></span> <span data-ttu-id="b1bec-177">In the following example, an operation is called with the two previous example `set-header` policies with named values.</span><span class="sxs-lookup"><span data-stu-id="b1bec-177">In the following example, an operation is called with the two previous example `set-header` policies with named values.</span></span> <span data-ttu-id="b1bec-178">Note that the response contains two custom headers that were configured using policies with named values.</span><span class="sxs-lookup"><span data-stu-id="b1bec-178">Note that the response contains two custom headers that were configured using policies with named values.</span></span>

![Developer portal][api-management-send-results]

<span data-ttu-id="b1bec-180">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with named values, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span><span class="sxs-lookup"><span data-stu-id="b1bec-180">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with named values, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![API Inspector trace][api-management-api-inspector-trace]

<span data-ttu-id="b1bec-182">While property values can contain policy expressions, property values can't contain other named values.</span><span class="sxs-lookup"><span data-stu-id="b1bec-182">While property values can contain policy expressions, property values can't contain other named values.</span></span> <span data-ttu-id="b1bec-183">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span><span class="sxs-lookup"><span data-stu-id="b1bec-183">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b1bec-184">Next steps</span><span class="sxs-lookup"><span data-stu-id="b1bec-184">Next steps</span></span>
* <span data-ttu-id="b1bec-185">Learn more about working with policies</span><span class="sxs-lookup"><span data-stu-id="b1bec-185">Learn more about working with policies</span></span>
  * [<span data-ttu-id="b1bec-186">Policies in API Management</span><span class="sxs-lookup"><span data-stu-id="b1bec-186">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="b1bec-187">Policy reference</span><span class="sxs-lookup"><span data-stu-id="b1bec-187">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="b1bec-188">Policy expressions</span><span class="sxs-lookup"><span data-stu-id="b1bec-188">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

[api-management-send-results]: ./media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: ./media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: ./media/api-management-howto-properties/api-management-api-inspector-trace.png

