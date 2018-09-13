---
title: How to use properties in Azure API Management policies
description: Learn how to use properties in Azure API Management policies.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 6f39b00f-cf6e-4cef-9bf2-1f89202c0bc0
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 698ecc01f54b6fade3b2fb5125714be74f98b7c9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550163"
---
# <a name="how-to-use-properties-in-azure-api-management-policies"></a><span data-ttu-id="e36d8-103">How to use properties in Azure API Management policies</span><span class="sxs-lookup"><span data-stu-id="e36d8-103">How to use properties in Azure API Management policies</span></span>
<span data-ttu-id="e36d8-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span><span class="sxs-lookup"><span data-stu-id="e36d8-104">API Management policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="e36d8-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span><span class="sxs-lookup"><span data-stu-id="e36d8-105">Policies are a collection of statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="e36d8-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span><span class="sxs-lookup"><span data-stu-id="e36d8-106">Policy statements can be constructed using literal text values, policy expressions, and properties.</span></span> 

<span data-ttu-id="e36d8-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span><span class="sxs-lookup"><span data-stu-id="e36d8-107">Each API Management service instance has a properties collection of key/value pairs that are global to the service instance.</span></span> <span data-ttu-id="e36d8-108">These properties can be used to manage constant string values across all API configuration and policies.</span><span class="sxs-lookup"><span data-stu-id="e36d8-108">These properties can be used to manage constant string values across all API configuration and policies.</span></span> <span data-ttu-id="e36d8-109">Each property has the following attributes.</span><span class="sxs-lookup"><span data-stu-id="e36d8-109">Each property has the following attributes.</span></span>

| <span data-ttu-id="e36d8-110">Attribute</span><span class="sxs-lookup"><span data-stu-id="e36d8-110">Attribute</span></span> | <span data-ttu-id="e36d8-111">Type</span><span class="sxs-lookup"><span data-stu-id="e36d8-111">Type</span></span> | <span data-ttu-id="e36d8-112">Description</span><span class="sxs-lookup"><span data-stu-id="e36d8-112">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e36d8-113">Name</span><span class="sxs-lookup"><span data-stu-id="e36d8-113">Name</span></span> |<span data-ttu-id="e36d8-114">string</span><span class="sxs-lookup"><span data-stu-id="e36d8-114">string</span></span> |<span data-ttu-id="e36d8-115">The name of the property.</span><span class="sxs-lookup"><span data-stu-id="e36d8-115">The name of the property.</span></span> <span data-ttu-id="e36d8-116">It may contain only letters, digits, period, dash, and underscore characters.</span><span class="sxs-lookup"><span data-stu-id="e36d8-116">It may contain only letters, digits, period, dash, and underscore characters.</span></span> |
| <span data-ttu-id="e36d8-117">Value</span><span class="sxs-lookup"><span data-stu-id="e36d8-117">Value</span></span> |<span data-ttu-id="e36d8-118">string</span><span class="sxs-lookup"><span data-stu-id="e36d8-118">string</span></span> |<span data-ttu-id="e36d8-119">The value of the property.</span><span class="sxs-lookup"><span data-stu-id="e36d8-119">The value of the property.</span></span> <span data-ttu-id="e36d8-120">It may not be empty or consist only of whitespace.</span><span class="sxs-lookup"><span data-stu-id="e36d8-120">It may not be empty or consist only of whitespace.</span></span> |
| <span data-ttu-id="e36d8-121">Secret</span><span class="sxs-lookup"><span data-stu-id="e36d8-121">Secret</span></span> |<span data-ttu-id="e36d8-122">boolean</span><span class="sxs-lookup"><span data-stu-id="e36d8-122">boolean</span></span> |<span data-ttu-id="e36d8-123">Determines whether the value is a secret and should be encrypted or not.</span><span class="sxs-lookup"><span data-stu-id="e36d8-123">Determines whether the value is a secret and should be encrypted or not.</span></span> |
| <span data-ttu-id="e36d8-124">Tags</span><span class="sxs-lookup"><span data-stu-id="e36d8-124">Tags</span></span> |<span data-ttu-id="e36d8-125">array of string</span><span class="sxs-lookup"><span data-stu-id="e36d8-125">array of string</span></span> |<span data-ttu-id="e36d8-126">Optional tags that when provided can be used to filter the property list.</span><span class="sxs-lookup"><span data-stu-id="e36d8-126">Optional tags that when provided can be used to filter the property list.</span></span> |

<span data-ttu-id="e36d8-127">Properties are configured in the publisher portal on the **Properties** tab. In the following example, three properties are configured.</span><span class="sxs-lookup"><span data-stu-id="e36d8-127">Properties are configured in the publisher portal on the **Properties** tab. In the following example, three properties are configured.</span></span>

![Properties][api-management-properties]

<span data-ttu-id="e36d8-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span><span class="sxs-lookup"><span data-stu-id="e36d8-129">Property values can contain literal strings and [policy expressions](https://msdn.microsoft.com/library/azure/dn910913.aspx).</span></span> <span data-ttu-id="e36d8-130">The following table shows the previous three sample properties and their attributes.</span><span class="sxs-lookup"><span data-stu-id="e36d8-130">The following table shows the previous three sample properties and their attributes.</span></span> <span data-ttu-id="e36d8-131">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span><span class="sxs-lookup"><span data-stu-id="e36d8-131">The value of `ExpressionProperty` is a policy expression that returns a string containing the current date and time.</span></span> <span data-ttu-id="e36d8-132">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span><span class="sxs-lookup"><span data-stu-id="e36d8-132">The property `ContosoHeaderValue` is marked as a secret, so its value is not displayed.</span></span>

| <span data-ttu-id="e36d8-133">Name</span><span class="sxs-lookup"><span data-stu-id="e36d8-133">Name</span></span> | <span data-ttu-id="e36d8-134">Value</span><span class="sxs-lookup"><span data-stu-id="e36d8-134">Value</span></span> | <span data-ttu-id="e36d8-135">Secret</span><span class="sxs-lookup"><span data-stu-id="e36d8-135">Secret</span></span> | <span data-ttu-id="e36d8-136">Tags</span><span class="sxs-lookup"><span data-stu-id="e36d8-136">Tags</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="e36d8-137">ContosoHeader</span><span class="sxs-lookup"><span data-stu-id="e36d8-137">ContosoHeader</span></span> |<span data-ttu-id="e36d8-138">TrackingId</span><span class="sxs-lookup"><span data-stu-id="e36d8-138">TrackingId</span></span> |<span data-ttu-id="e36d8-139">False</span><span class="sxs-lookup"><span data-stu-id="e36d8-139">False</span></span> |<span data-ttu-id="e36d8-140">Contoso</span><span class="sxs-lookup"><span data-stu-id="e36d8-140">Contoso</span></span> |
| <span data-ttu-id="e36d8-141">ContosoHeaderValue</span><span class="sxs-lookup"><span data-stu-id="e36d8-141">ContosoHeaderValue</span></span> |<span data-ttu-id="e36d8-142">••••••••••••••••••••••</span><span class="sxs-lookup"><span data-stu-id="e36d8-142">••••••••••••••••••••••</span></span> |<span data-ttu-id="e36d8-143">True</span><span class="sxs-lookup"><span data-stu-id="e36d8-143">True</span></span> |<span data-ttu-id="e36d8-144">Contoso</span><span class="sxs-lookup"><span data-stu-id="e36d8-144">Contoso</span></span> |
| <span data-ttu-id="e36d8-145">ExpressionProperty</span><span class="sxs-lookup"><span data-stu-id="e36d8-145">ExpressionProperty</span></span> |<span data-ttu-id="e36d8-146">@(DateTime.Now.ToString())</span><span class="sxs-lookup"><span data-stu-id="e36d8-146">@(DateTime.Now.ToString())</span></span> |<span data-ttu-id="e36d8-147">False</span><span class="sxs-lookup"><span data-stu-id="e36d8-147">False</span></span> | |

## <a name="to-use-a-property"></a><span data-ttu-id="e36d8-148">To use a property</span><span class="sxs-lookup"><span data-stu-id="e36d8-148">To use a property</span></span>
<span data-ttu-id="e36d8-149">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="e36d8-149">To use a property in a policy, place the property name inside a double pair of braces like `{{ContosoHeader}}`, as shown in the following example.</span></span>

```xml
<set-header name="{{ContosoHeader}}" exists-action="override">
  <value>{{ContosoHeaderValue}}</value>
</set-header>
```

<span data-ttu-id="e36d8-150">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span><span class="sxs-lookup"><span data-stu-id="e36d8-150">In this example, `ContosoHeader` is used as the name of a header in a `set-header` policy, and `ContosoHeaderValue` is used as the value of that header.</span></span> <span data-ttu-id="e36d8-151">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span><span class="sxs-lookup"><span data-stu-id="e36d8-151">When this policy is evaluated during a request or response to the API Management gateway, `{{ContosoHeader}}` and `{{ContosoHeaderValue}}` are replaced with their respective property values.</span></span>

<span data-ttu-id="e36d8-152">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span><span class="sxs-lookup"><span data-stu-id="e36d8-152">Properties can be used as complete attribute or element values as shown in the previous example, but they can also be inserted into or combined with part of a literal text expression as shown in the following example: `<set-header name = "CustomHeader{{ContosoHeader}}" ...>`</span></span>

<span data-ttu-id="e36d8-153">Properties can also contain policy expressions.</span><span class="sxs-lookup"><span data-stu-id="e36d8-153">Properties can also contain policy expressions.</span></span> <span data-ttu-id="e36d8-154">In the following example, the `ExpressionProperty` is used.</span><span class="sxs-lookup"><span data-stu-id="e36d8-154">In the following example, the `ExpressionProperty` is used.</span></span>

```xml
<set-header name="CustomHeader" exists-action="override">
    <value>{{ExpressionProperty}}</value>
</set-header>
```

<span data-ttu-id="e36d8-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span><span class="sxs-lookup"><span data-stu-id="e36d8-155">When this policy is evaluated, `{{ExpressionProperty}}` is replaced with its value: `@(DateTime.Now.ToString())`.</span></span> <span data-ttu-id="e36d8-156">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span><span class="sxs-lookup"><span data-stu-id="e36d8-156">Since the value is a policy expression, the expression is evaluated and the policy proceeds with its execution.</span></span>

<span data-ttu-id="e36d8-157">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span><span class="sxs-lookup"><span data-stu-id="e36d8-157">You can test this out in the developer portal by calling an operation that has a policy with properties in scope.</span></span> <span data-ttu-id="e36d8-158">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span><span class="sxs-lookup"><span data-stu-id="e36d8-158">In the following example, an operation is called with the two previous example `set-header` policies with properties.</span></span> <span data-ttu-id="e36d8-159">Note that the response contains two custom headers that were configured using policies with properties.</span><span class="sxs-lookup"><span data-stu-id="e36d8-159">Note that the response contains two custom headers that were configured using policies with properties.</span></span>

![Developer portal][api-management-send-results]

<span data-ttu-id="e36d8-161">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span><span class="sxs-lookup"><span data-stu-id="e36d8-161">If you look at the [API Inspector trace](api-management-howto-api-inspector.md) for a call that includes the two previous sample policies with properties, you can see the two `set-header` policies with the property values inserted as well as the policy expression evaluation for the property that contained the policy expression.</span></span>

![API Inspector trace][api-management-api-inspector-trace]

<span data-ttu-id="e36d8-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span><span class="sxs-lookup"><span data-stu-id="e36d8-163">Note that while property values can contain policy expressions, property values can't contain other properties.</span></span> <span data-ttu-id="e36d8-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span><span class="sxs-lookup"><span data-stu-id="e36d8-164">If text containing a property reference is used for a property value, such as `Property value text {{MyProperty}}`, that property reference won't be replaced and will be included as part of the property value.</span></span>

## <a name="to-create-a-property"></a><span data-ttu-id="e36d8-165">To create a property</span><span class="sxs-lookup"><span data-stu-id="e36d8-165">To create a property</span></span>
<span data-ttu-id="e36d8-166">To create a property, click **Add property** on the **Properties** tab.</span><span class="sxs-lookup"><span data-stu-id="e36d8-166">To create a property, click **Add property** on the **Properties** tab.</span></span>

![Add property][api-management-properties-add-property-menu]

<span data-ttu-id="e36d8-168">**Name** and **Value** are required values.</span><span class="sxs-lookup"><span data-stu-id="e36d8-168">**Name** and **Value** are required values.</span></span> <span data-ttu-id="e36d8-169">If this property value is a secret, check the **This is a secret** checkbox.</span><span class="sxs-lookup"><span data-stu-id="e36d8-169">If this property value is a secret, check the **This is a secret** checkbox.</span></span> <span data-ttu-id="e36d8-170">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e36d8-170">Enter one or more optional tags to help with organizing your properties, and click **Save**.</span></span>

![Add property][api-management-properties-add-property]

<span data-ttu-id="e36d8-172">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span><span class="sxs-lookup"><span data-stu-id="e36d8-172">When a new property is saved, the **Search property** textbox is populated with the name of the new property and the new property is displayed.</span></span> <span data-ttu-id="e36d8-173">To display all properties, clear the **Search property** textbox and press enter.</span><span class="sxs-lookup"><span data-stu-id="e36d8-173">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Properties][api-management-properties-property-saved]

<span data-ttu-id="e36d8-175">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span><span class="sxs-lookup"><span data-stu-id="e36d8-175">For information on creating a property using the REST API, see [Create a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Put).</span></span>

## <a name="to-edit-a-property"></a><span data-ttu-id="e36d8-176">To edit a property</span><span class="sxs-lookup"><span data-stu-id="e36d8-176">To edit a property</span></span>
<span data-ttu-id="e36d8-177">To edit a property, click **Edit** beside the property to edit.</span><span class="sxs-lookup"><span data-stu-id="e36d8-177">To edit a property, click **Edit** beside the property to edit.</span></span>

![Edit property][api-management-properties-edit]

<span data-ttu-id="e36d8-179">Make any desired changes, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e36d8-179">Make any desired changes, and click **Save**.</span></span> <span data-ttu-id="e36d8-180">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span><span class="sxs-lookup"><span data-stu-id="e36d8-180">If you change the property name, any policies that reference that property are automatically updated to use the new name.</span></span>

![Edit property][api-management-properties-edit-property]

<span data-ttu-id="e36d8-182">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span><span class="sxs-lookup"><span data-stu-id="e36d8-182">For information on editing a property using the REST API, see [Edit a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Patch).</span></span>

## <a name="to-delete-a-property"></a><span data-ttu-id="e36d8-183">To delete a property</span><span class="sxs-lookup"><span data-stu-id="e36d8-183">To delete a property</span></span>
<span data-ttu-id="e36d8-184">To delete a property, click **Delete** beside the property to delete.</span><span class="sxs-lookup"><span data-stu-id="e36d8-184">To delete a property, click **Delete** beside the property to delete.</span></span>

![Delete property][api-management-properties-delete]

<span data-ttu-id="e36d8-186">Click **Yes, delete it** to confirm.</span><span class="sxs-lookup"><span data-stu-id="e36d8-186">Click **Yes, delete it** to confirm.</span></span>

![Confirm delete][api-management-delete-confirm]

> [!IMPORTANT]
> <span data-ttu-id="e36d8-188">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span><span class="sxs-lookup"><span data-stu-id="e36d8-188">If the property is referenced by any policies, you will be unable to successfully delete it until you remove the property from all policies that use it.</span></span>
> 
> 

<span data-ttu-id="e36d8-189">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span><span class="sxs-lookup"><span data-stu-id="e36d8-189">For information on deleting a property using the REST API, see [Delete a property using the REST API](https://msdn.microsoft.com/library/azure/mt651775.aspx#Delete).</span></span>

## <a name="to-search-and-filter-properties"></a><span data-ttu-id="e36d8-190">To search and filter properties</span><span class="sxs-lookup"><span data-stu-id="e36d8-190">To search and filter properties</span></span>
<span data-ttu-id="e36d8-191">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span><span class="sxs-lookup"><span data-stu-id="e36d8-191">The **Properties** tab includes searching and filtering capabilities to help you manage your properties.</span></span> <span data-ttu-id="e36d8-192">To filter the property list by property name, enter a search term in the **Search property** textbox.</span><span class="sxs-lookup"><span data-stu-id="e36d8-192">To filter the property list by property name, enter a search term in the **Search property** textbox.</span></span> <span data-ttu-id="e36d8-193">To display all properties, clear the **Search property** textbox and press enter.</span><span class="sxs-lookup"><span data-stu-id="e36d8-193">To display all properties, clear the **Search property** textbox and press enter.</span></span>

![Search][api-management-properties-search]

<span data-ttu-id="e36d8-195">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span><span class="sxs-lookup"><span data-stu-id="e36d8-195">To filter the property list by tag values, enter one or more tags into the **Filter by tags** textbox.</span></span> <span data-ttu-id="e36d8-196">To display all properties, clear the **Filter by tags** textbox and press enter.</span><span class="sxs-lookup"><span data-stu-id="e36d8-196">To display all properties, clear the **Filter by tags** textbox and press enter.</span></span>

![Filter][api-management-properties-filter]

## <a name="next-steps"></a><span data-ttu-id="e36d8-198">Next steps</span><span class="sxs-lookup"><span data-stu-id="e36d8-198">Next steps</span></span>
* <span data-ttu-id="e36d8-199">Learn more about working with policies</span><span class="sxs-lookup"><span data-stu-id="e36d8-199">Learn more about working with policies</span></span>
  * [<span data-ttu-id="e36d8-200">Policies in API Management</span><span class="sxs-lookup"><span data-stu-id="e36d8-200">Policies in API Management</span></span>](api-management-howto-policies.md)
  * [<span data-ttu-id="e36d8-201">Policy reference</span><span class="sxs-lookup"><span data-stu-id="e36d8-201">Policy reference</span></span>](https://msdn.microsoft.com/library/azure/dn894081.aspx)
  * [<span data-ttu-id="e36d8-202">Policy expressions</span><span class="sxs-lookup"><span data-stu-id="e36d8-202">Policy expressions</span></span>](https://msdn.microsoft.com/library/azure/dn910913.aspx)

## <a name="watch-a-video-overview"></a><span data-ttu-id="e36d8-203">Watch a video overview</span><span class="sxs-lookup"><span data-stu-id="e36d8-203">Watch a video overview</span></span>
> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Use-Properties-in-Policies/player]
> 
> 

[api-management-properties]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-properties.png
[api-management-properties-add-property]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-properties-add-property.png
[api-management-properties-edit-property]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-properties-edit-property.png
[api-management-properties-add-property-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-properties-add-property-menu.png
[api-management-properties-property-saved]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-properties-property-saved.png
[api-management-properties-delete]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-properties-delete.png
[api-management-properties-edit]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-properties-edit.png
[api-management-delete-confirm]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-delete-confirm.png
[api-management-properties-search]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-properties-search.png
[api-management-send-results]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-send-results.png
[api-management-properties-filter]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-properties-filter.png
[api-management-api-inspector-trace]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-properties/api-management-api-inspector-trace.png













