---
title: Policies in Azure API Management | Microsoft Docs
description: Learn how to create, edit, and configure policies in API Management.
services: api-management
documentationcenter: ''
author: steved0x
manager: erikre
editor: ''
ms.assetid: 537e5caf-708b-430e-a83f-72b70af28aa9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: 60891705eefb5129323ae40158dd395ea920d168
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549841"
---
# <a name="policies-in-azure-api-management"></a><span data-ttu-id="be916-103">Policies in Azure API Management</span><span class="sxs-lookup"><span data-stu-id="be916-103">Policies in Azure API Management</span></span>
<span data-ttu-id="be916-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span><span class="sxs-lookup"><span data-stu-id="be916-104">In Azure API Management, policies are a powerful capability of the system that allow the publisher to change the behavior of the API through configuration.</span></span> <span data-ttu-id="be916-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span><span class="sxs-lookup"><span data-stu-id="be916-105">Policies are a collection of Statements that are executed sequentially on the request or response of an API.</span></span> <span data-ttu-id="be916-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span><span class="sxs-lookup"><span data-stu-id="be916-106">Popular Statements include format conversion from XML to JSON and call rate limiting to restrict the amount of incoming calls from a developer.</span></span> <span data-ttu-id="be916-107">Many more policies are available out of the box.</span><span class="sxs-lookup"><span data-stu-id="be916-107">Many more policies are available out of the box.</span></span>

<span data-ttu-id="be916-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span><span class="sxs-lookup"><span data-stu-id="be916-108">See the [Policy Reference][Policy Reference] for a full list of policy statements and their settings.</span></span>

<span data-ttu-id="be916-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span><span class="sxs-lookup"><span data-stu-id="be916-109">Policies are applied inside the gateway which sits between the API consumer and the managed API.</span></span> <span data-ttu-id="be916-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span><span class="sxs-lookup"><span data-stu-id="be916-110">The gateway receives all requests and usually forwards them unaltered to the underlying API.</span></span> <span data-ttu-id="be916-111">However a policy can apply changes to both the inbound request and outbound response.</span><span class="sxs-lookup"><span data-stu-id="be916-111">However a policy can apply changes to both the inbound request and outbound response.</span></span>

<span data-ttu-id="be916-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span><span class="sxs-lookup"><span data-stu-id="be916-112">Policy expressions can be used as attribute values or text values in any of the API Management policies, unless the policy specifies otherwise.</span></span> <span data-ttu-id="be916-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span><span class="sxs-lookup"><span data-stu-id="be916-113">Some policies such as the [Control flow][Control flow] and [Set variable][Set variable] policies are based on policy expressions.</span></span> <span data-ttu-id="be916-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span><span class="sxs-lookup"><span data-stu-id="be916-114">For more information, see [Advanced policies][Advanced policies] and [Policy expressions][Policy expressions].</span></span>

## <span data-ttu-id="be916-115"><a name="scopes"> </a>How to configure policies</span><span class="sxs-lookup"><span data-stu-id="be916-115"><a name="scopes"> </a>How to configure policies</span></span>
<span data-ttu-id="be916-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span><span class="sxs-lookup"><span data-stu-id="be916-116">Policies can be configured globally or at the scope of a [Product][Product], [API][API] or [Operation][Operation].</span></span> <span data-ttu-id="be916-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span><span class="sxs-lookup"><span data-stu-id="be916-117">To configure a policy, navigate to the Policies editor in the publisher portal.</span></span>

![Policies menu][policies-menu]

<span data-ttu-id="be916-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span><span class="sxs-lookup"><span data-stu-id="be916-119">The policies editor consists of three main sections: the policy scope (top), the policy definition where policies are edited (left) and the statements list (right):</span></span>

![Policies editor][policies-editor]

<span data-ttu-id="be916-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span><span class="sxs-lookup"><span data-stu-id="be916-121">To begin configuring a policy you must first select the scope at which the policy should apply.</span></span> <span data-ttu-id="be916-122">In the screenshot below the **Starter** product is selected.</span><span class="sxs-lookup"><span data-stu-id="be916-122">In the screenshot below the **Starter** product is selected.</span></span> <span data-ttu-id="be916-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span><span class="sxs-lookup"><span data-stu-id="be916-123">Note that the square symbol next to the policy name indicates that a policy is already applied at this level.</span></span>

![Scope][policies-scope]

<span data-ttu-id="be916-125">Since a policy has already been applied, the configuration is shown in the definition view.</span><span class="sxs-lookup"><span data-stu-id="be916-125">Since a policy has already been applied, the configuration is shown in the definition view.</span></span>

![Configure][policies-configure]

<span data-ttu-id="be916-127">The policy is displayed read-only at first.</span><span class="sxs-lookup"><span data-stu-id="be916-127">The policy is displayed read-only at first.</span></span> <span data-ttu-id="be916-128">In order to edit the definition click the **Configure Policy** action.</span><span class="sxs-lookup"><span data-stu-id="be916-128">In order to edit the definition click the **Configure Policy** action.</span></span>

![Edit][policies-edit]

<span data-ttu-id="be916-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span><span class="sxs-lookup"><span data-stu-id="be916-130">The policy definition is a simple XML document that describes a sequence of inbound and outbound statements.</span></span> <span data-ttu-id="be916-131">The XML can be edited directly in the definition window.</span><span class="sxs-lookup"><span data-stu-id="be916-131">The XML can be edited directly in the definition window.</span></span> <span data-ttu-id="be916-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span><span class="sxs-lookup"><span data-stu-id="be916-132">A list of statements is provided to the right and statements applicable to the current scope are enabled and highlighted; as demonstrated by the **Limit Call Rate** statement in the screenshot above.</span></span>

<span data-ttu-id="be916-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span><span class="sxs-lookup"><span data-stu-id="be916-133">Clicking an enabled statement will add the appropriate XML at the location of the cursor in the definition view.</span></span> 

> [!NOTE]
> <span data-ttu-id="be916-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span><span class="sxs-lookup"><span data-stu-id="be916-134">If the policy that you want to add is not enabled, ensure that you are in the correct scope for that policy.</span></span> <span data-ttu-id="be916-135">Each policy statement is designed for use in certain scopes and policy sections.</span><span class="sxs-lookup"><span data-stu-id="be916-135">Each policy statement is designed for use in certain scopes and policy sections.</span></span> <span data-ttu-id="be916-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="be916-136">To review the policy sections and scopes for a policy, check the **Usage** section for that policy in the [Policy Reference][Policy Reference].</span></span>
> 
> 

<span data-ttu-id="be916-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span><span class="sxs-lookup"><span data-stu-id="be916-137">A full list of policy statements and their settings are available in the [Policy Reference][Policy Reference].</span></span>

<span data-ttu-id="be916-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span><span class="sxs-lookup"><span data-stu-id="be916-138">For example, to add a new statement to restrict incoming requests to specified IP addresses, place the cursor just inside the content of the `inbound` XML element and click the **Restrict caller IPs** statement.</span></span>

![Restriction policies][policies-restrict]

<span data-ttu-id="be916-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span><span class="sxs-lookup"><span data-stu-id="be916-140">This will add an XML snippet to the `inbound` element that provides guidance on how to configure the statement.</span></span>

```xml
<ip-filter action="allow | forbid">
    <address>address</address>
    <address-range from="address" to="address"/>
</ip-filter>
```

<span data-ttu-id="be916-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span><span class="sxs-lookup"><span data-stu-id="be916-141">To limit inbound requests and accept only those from an IP address of 1.2.3.4 modify the XML as follows:</span></span>

```xml
<ip-filter action="allow">
    <address>1.2.3.4</address>
</ip-filter>
```

![Save][policies-save]

<span data-ttu-id="be916-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span><span class="sxs-lookup"><span data-stu-id="be916-143">When complete configuring the statements for the policy, click **Save** and the changes will be propagated to the API Management gateway immediately.</span></span>

## <span data-ttu-id="be916-144"><a name="sections"> </a>Understanding policy configuration</span><span class="sxs-lookup"><span data-stu-id="be916-144"><a name="sections"> </a>Understanding policy configuration</span></span>
<span data-ttu-id="be916-145">A policy is a series of statements that execute in order for a request and a response.</span><span class="sxs-lookup"><span data-stu-id="be916-145">A policy is a series of statements that execute in order for a request and a response.</span></span> <span data-ttu-id="be916-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span><span class="sxs-lookup"><span data-stu-id="be916-146">The configuration is divided appropriately into `inbound`, `backend`, `outbound`, and `on-error` sections as shown in the following configuration.</span></span>

```xml
<policies>
  <inbound>
    <!-- statements to be applied to the request go here -->
  </inbound>
  <backend>
    <!-- statements to be applied before the request is forwarded to 
         the backend service go here -->
  </backend>
  <outbound>
    <!-- statements to be applied to the response go here -->
  </outbound>
  <on-error>
    <!-- statements to be applied if there is an error condition go here -->
  </on-error>
</policies> 
```

<span data-ttu-id="be916-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span><span class="sxs-lookup"><span data-stu-id="be916-147">If there is an error during the processing of a request, any remaining steps in the `inbound`, `backend`, or `outbound` sections are skipped and execution jumps to the statements in the `on-error` section.</span></span> <span data-ttu-id="be916-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span><span class="sxs-lookup"><span data-stu-id="be916-148">By placing policy statements in the `on-error` section you can review the error by using the `context.LastError` property, inspect and customize the error response using the `set-body` policy, and configure what happens if an error occurs.</span></span> <span data-ttu-id="be916-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span><span class="sxs-lookup"><span data-stu-id="be916-149">There are error codes for built-in steps and for errors that may occur during the processing of policy statements.</span></span> <span data-ttu-id="be916-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span><span class="sxs-lookup"><span data-stu-id="be916-150">For more information, see [Error handling in API Management policies](https://msdn.microsoft.com/library/azure/mt629506.aspx).</span></span>

<span data-ttu-id="be916-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span><span class="sxs-lookup"><span data-stu-id="be916-151">Since policies can be specified at different levels (global, product, api and operation) the configuration provides a way for you to specify the order in which the policy definition's statements execute with respect to the parent policy.</span></span> 

<span data-ttu-id="be916-152">Policy scopes are evaluated in the following order.</span><span class="sxs-lookup"><span data-stu-id="be916-152">Policy scopes are evaluated in the following order.</span></span>

1. <span data-ttu-id="be916-153">Global scope</span><span class="sxs-lookup"><span data-stu-id="be916-153">Global scope</span></span>
2. <span data-ttu-id="be916-154">Product scope</span><span class="sxs-lookup"><span data-stu-id="be916-154">Product scope</span></span>
3. <span data-ttu-id="be916-155">API scope</span><span class="sxs-lookup"><span data-stu-id="be916-155">API scope</span></span>
4. <span data-ttu-id="be916-156">Operation scope</span><span class="sxs-lookup"><span data-stu-id="be916-156">Operation scope</span></span>

<span data-ttu-id="be916-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span><span class="sxs-lookup"><span data-stu-id="be916-157">The statements within them are evaluated according to the placement of the `base` element, if it is present.</span></span> <span data-ttu-id="be916-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span><span class="sxs-lookup"><span data-stu-id="be916-158">Global policy has no parent policy and using the `<base>` element in it has no effect.</span></span>

<span data-ttu-id="be916-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span><span class="sxs-lookup"><span data-stu-id="be916-159">For example, if you have a policy at the global level and a policy configured for an API, then whenever that particular API is used both policies will be applied.</span></span> <span data-ttu-id="be916-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span><span class="sxs-lookup"><span data-stu-id="be916-160">API Management allows for deterministic ordering of combined policy statements via the base element.</span></span> 

```xml
<policies>
    <inbound>
        <cross-domain />
        <base />
        <find-and-replace from="xyz" to="abc" />
    </inbound>
</policies>
```

<span data-ttu-id="be916-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span><span class="sxs-lookup"><span data-stu-id="be916-161">In the example policy definition above, the `cross-domain` statement would execute before any higher policies which would in turn, be followed by the `find-and-replace` policy.</span></span> 

<span data-ttu-id="be916-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span><span class="sxs-lookup"><span data-stu-id="be916-162">To see the policies in the current scope in the policy editor, click **Recalculate effective policy for selected scope**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="be916-163">Next steps</span><span class="sxs-lookup"><span data-stu-id="be916-163">Next steps</span></span>
<span data-ttu-id="be916-164">Check out following video on policy expressions.</span><span class="sxs-lookup"><span data-stu-id="be916-164">Check out following video on policy expressions.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Policy-Expressions-in-Azure-API-Management/player]
> 
> 

[Policy Reference]: api-management-policy-reference.md
[Product]: api-management-howto-add-products.md
[API]: api-management-howto-add-products.md#add-apis 
[Operation]: api-management-howto-add-operations.md

[Advanced policies]: https://msdn.microsoft.com/library/azure/dn894085.aspx
[Control flow]: https://msdn.microsoft.com/library/azure/dn894085.aspx#choose
[Set variable]: https://msdn.microsoft.com/library/azure/dn894085.aspx#set_variable
[Policy expressions]: https://msdn.microsoft.com/library/azure/dn910913.aspx

[policies-menu]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-policies/api-management-policies-menu.png
[policies-editor]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-policies/api-management-policies-editor.png
[policies-scope]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-policies/api-management-policies-scope.png
[policies-configure]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-policies/api-management-policies-configure.png
[policies-edit]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-policies/api-management-policies-edit.png
[policies-restrict]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-policies/api-management-policies-restrict.png
[policies-save]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/api-management/media/api-management-howto-policies/api-management-policies-save.png







