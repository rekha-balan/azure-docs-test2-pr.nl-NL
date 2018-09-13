---
title: Secure access to Azure Logic Apps | Microsoft Docs
description: Protect access to triggers, inputs and outputs, action parameters, and services in workflows for Azure Logic Apps
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: kevinlam1
ms.author: klam
ms.reviewer: estfan, LADocs
ms.assetid: 9fab1050-cfbc-4a8b-b1b3-5531bee92856
ms.topic: article
ms.date: 11/22/2016
ms.openlocfilehash: 1307b6df22c51af9710d44abb23178d65e3507aa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44783918"
---
# <a name="secure-access-in-azure-logic-apps"></a><span data-ttu-id="a27de-103">Secure access in Azure Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a27de-103">Secure access in Azure Logic Apps</span></span>

<span data-ttu-id="a27de-104">Here are ways that you can secure access to different components in your logic app:</span><span class="sxs-lookup"><span data-stu-id="a27de-104">Here are ways that you can secure access to different components in your logic app:</span></span>

* <span data-ttu-id="a27de-105">Secure access for triggering a logic app workflow with the HTTP request trigger.</span><span class="sxs-lookup"><span data-stu-id="a27de-105">Secure access for triggering a logic app workflow with the HTTP request trigger.</span></span>
* <span data-ttu-id="a27de-106">Secure access for managing, editing, or reading a logic app.</span><span class="sxs-lookup"><span data-stu-id="a27de-106">Secure access for managing, editing, or reading a logic app.</span></span>
* <span data-ttu-id="a27de-107">Secure access to the contents inside inputs and outputs for a logic app run.</span><span class="sxs-lookup"><span data-stu-id="a27de-107">Secure access to the contents inside inputs and outputs for a logic app run.</span></span>
* <span data-ttu-id="a27de-108">Secure parameters or inputs for actions in a logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="a27de-108">Secure parameters or inputs for actions in a logic app workflow.</span></span>
* <span data-ttu-id="a27de-109">Secure access to services that receive requests from a logic app workflow.</span><span class="sxs-lookup"><span data-stu-id="a27de-109">Secure access to services that receive requests from a logic app workflow.</span></span>

## <a name="secure-access-to-trigger"></a><span data-ttu-id="a27de-110">Secure access to trigger</span><span class="sxs-lookup"><span data-stu-id="a27de-110">Secure access to trigger</span></span>

<span data-ttu-id="a27de-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire the logic app.</span><span class="sxs-lookup"><span data-stu-id="a27de-111">When you work with a logic app that fires on an HTTP Request ([Request](../connectors/connectors-native-reqres.md) or [Webhook](../connectors/connectors-native-webhook.md)), you can restrict access so that only authorized clients can fire the logic app.</span></span> <span data-ttu-id="a27de-112">All requests into a logic app are encrypted and secured via SSL.</span><span class="sxs-lookup"><span data-stu-id="a27de-112">All requests into a logic app are encrypted and secured via SSL.</span></span>

### <a name="shared-access-signature"></a><span data-ttu-id="a27de-113">Shared Access Signature</span><span class="sxs-lookup"><span data-stu-id="a27de-113">Shared Access Signature</span></span>

<span data-ttu-id="a27de-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of the URL.</span><span class="sxs-lookup"><span data-stu-id="a27de-114">Every request endpoint for a logic app includes a [Shared Access Signature (SAS)](../storage/common/storage-dotnet-shared-access-signature-part-1.md) as part of the URL.</span></span> <span data-ttu-id="a27de-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span><span class="sxs-lookup"><span data-stu-id="a27de-115">Each URL contains a `sp`, `sv`, and `sig` query parameter.</span></span> <span data-ttu-id="a27de-116">Permissions are specified by `sp`, and correspond to HTTP methods allowed, `sv` is the version used to generate, and `sig` is used to authenticate access to trigger.</span><span class="sxs-lookup"><span data-stu-id="a27de-116">Permissions are specified by `sp`, and correspond to HTTP methods allowed, `sv` is the version used to generate, and `sig` is used to authenticate access to trigger.</span></span> <span data-ttu-id="a27de-117">The signature is generated using the SHA256 algorithm with a secret key on all the URL paths and properties.</span><span class="sxs-lookup"><span data-stu-id="a27de-117">The signature is generated using the SHA256 algorithm with a secret key on all the URL paths and properties.</span></span> <span data-ttu-id="a27de-118">The secret key is never exposed and published, and is kept encrypted and stored as part of the logic app.</span><span class="sxs-lookup"><span data-stu-id="a27de-118">The secret key is never exposed and published, and is kept encrypted and stored as part of the logic app.</span></span> <span data-ttu-id="a27de-119">Your logic app only authorizes triggers that contain a valid signature created with the secret key.</span><span class="sxs-lookup"><span data-stu-id="a27de-119">Your logic app only authorizes triggers that contain a valid signature created with the secret key.</span></span>

#### <a name="regenerate-access-keys"></a><span data-ttu-id="a27de-120">Regenerate access keys</span><span class="sxs-lookup"><span data-stu-id="a27de-120">Regenerate access keys</span></span>

<span data-ttu-id="a27de-121">You can regenerate a new secure key at anytime through the REST API or Azure portal.</span><span class="sxs-lookup"><span data-stu-id="a27de-121">You can regenerate a new secure key at anytime through the REST API or Azure portal.</span></span> <span data-ttu-id="a27de-122">All current URLs that were generated previously using the old key are invalidated and no longer authorized to fire the logic app.</span><span class="sxs-lookup"><span data-stu-id="a27de-122">All current URLs that were generated previously using the old key are invalidated and no longer authorized to fire the logic app.</span></span>

1. <span data-ttu-id="a27de-123">In the Azure portal, open the logic app you want to regenerate a key</span><span class="sxs-lookup"><span data-stu-id="a27de-123">In the Azure portal, open the logic app you want to regenerate a key</span></span>
1. <span data-ttu-id="a27de-124">Click the **Access Keys** menu item under **Settings**</span><span class="sxs-lookup"><span data-stu-id="a27de-124">Click the **Access Keys** menu item under **Settings**</span></span>
1. <span data-ttu-id="a27de-125">Choose the key to regenerate and complete the process</span><span class="sxs-lookup"><span data-stu-id="a27de-125">Choose the key to regenerate and complete the process</span></span>

<span data-ttu-id="a27de-126">URLs you retrieve after regeneration are signed with the new access key.</span><span class="sxs-lookup"><span data-stu-id="a27de-126">URLs you retrieve after regeneration are signed with the new access key.</span></span>

#### <a name="creating-callback-urls-with-an-expiration-date"></a><span data-ttu-id="a27de-127">Creating callback URLs with an expiration date</span><span class="sxs-lookup"><span data-stu-id="a27de-127">Creating callback URLs with an expiration date</span></span>

<span data-ttu-id="a27de-128">If you are sharing the URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span><span class="sxs-lookup"><span data-stu-id="a27de-128">If you are sharing the URL with other parties, you can generate URLs with specific keys and expiration dates as needed.</span></span> <span data-ttu-id="a27de-129">You can then seamlessly roll keys, or ensure access to fire an app is restricted to a certain timespan.</span><span class="sxs-lookup"><span data-stu-id="a27de-129">You can then seamlessly roll keys, or ensure access to fire an app is restricted to a certain timespan.</span></span> <span data-ttu-id="a27de-130">You can specify an expiration date for a URL through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span><span class="sxs-lookup"><span data-stu-id="a27de-130">You can specify an expiration date for a URL through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers):</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="a27de-131">In the body, include the property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until the `NotAfter` date and time.</span><span class="sxs-lookup"><span data-stu-id="a27de-131">In the body, include the property `NotAfter` as a JSON date string, which returns a callback URL that is only valid until the `NotAfter` date and time.</span></span>

#### <a name="creating-urls-with-primary-or-secondary-secret-key"></a><span data-ttu-id="a27de-132">Creating URLs with primary or secondary secret key</span><span class="sxs-lookup"><span data-stu-id="a27de-132">Creating URLs with primary or secondary secret key</span></span>

<span data-ttu-id="a27de-133">When you generate or list callback URLs for request-based triggers, you can also specify which key to use to sign the URL.</span><span class="sxs-lookup"><span data-stu-id="a27de-133">When you generate or list callback URLs for request-based triggers, you can also specify which key to use to sign the URL.</span></span>  <span data-ttu-id="a27de-134">You can generate a URL signed by a specific key through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span><span class="sxs-lookup"><span data-stu-id="a27de-134">You can generate a URL signed by a specific key through the [logic apps REST API](https://docs.microsoft.com/rest/api/logic/workflowtriggers) as follows:</span></span>

``` http
POST 
/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Logic/workflows/{workflowName}/triggers/{triggerName}/listCallbackUrl?api-version=2016-06-01
```

<span data-ttu-id="a27de-135">In the body, include the property `KeyType` as either `Primary` or `Secondary`.</span><span class="sxs-lookup"><span data-stu-id="a27de-135">In the body, include the property `KeyType` as either `Primary` or `Secondary`.</span></span>  <span data-ttu-id="a27de-136">This returns a URL signed by the secure key specified.</span><span class="sxs-lookup"><span data-stu-id="a27de-136">This returns a URL signed by the secure key specified.</span></span>

### <a name="restrict-incoming-ip-addresses"></a><span data-ttu-id="a27de-137">Restrict incoming IP addresses</span><span class="sxs-lookup"><span data-stu-id="a27de-137">Restrict incoming IP addresses</span></span>

<span data-ttu-id="a27de-138">In addition to the Shared Access Signature, you may wish to restrict calling a logic app only from specific clients.</span><span class="sxs-lookup"><span data-stu-id="a27de-138">In addition to the Shared Access Signature, you may wish to restrict calling a logic app only from specific clients.</span></span>  <span data-ttu-id="a27de-139">For example, if you manage your endpoint through Azure API Management, you can restrict the logic app to only accept the request when the request comes from the API Management instance IP address.</span><span class="sxs-lookup"><span data-stu-id="a27de-139">For example, if you manage your endpoint through Azure API Management, you can restrict the logic app to only accept the request when the request comes from the API Management instance IP address.</span></span>

<span data-ttu-id="a27de-140">This setting can be configured within the logic app settings:</span><span class="sxs-lookup"><span data-stu-id="a27de-140">This setting can be configured within the logic app settings:</span></span>

1. <span data-ttu-id="a27de-141">In the Azure portal, open the logic app you want to add IP address restrictions</span><span class="sxs-lookup"><span data-stu-id="a27de-141">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
1. <span data-ttu-id="a27de-142">Click the **Workflow Settings** menu item under **Settings**</span><span class="sxs-lookup"><span data-stu-id="a27de-142">Click the **Workflow Settings** menu item under **Settings**</span></span>
1. <span data-ttu-id="a27de-143">Specify the list of IP address ranges to be accepted by the trigger</span><span class="sxs-lookup"><span data-stu-id="a27de-143">Specify the list of IP address ranges to be accepted by the trigger</span></span>

<span data-ttu-id="a27de-144">A valid IP range takes the format `192.168.1.1/32`.</span><span class="sxs-lookup"><span data-stu-id="a27de-144">A valid IP range takes the format `192.168.1.1/32`.</span></span> <span data-ttu-id="a27de-145">If you want the logic app to only fire as a nested logic app, select the **Only other logic apps** option.</span><span class="sxs-lookup"><span data-stu-id="a27de-145">If you want the logic app to only fire as a nested logic app, select the **Only other logic apps** option.</span></span> <span data-ttu-id="a27de-146">This option writes an empty array to the resource, meaning only calls from the service itself (parent logic apps) fire successfully.</span><span class="sxs-lookup"><span data-stu-id="a27de-146">This option writes an empty array to the resource, meaning only calls from the service itself (parent logic apps) fire successfully.</span></span>

> [!NOTE]
> <span data-ttu-id="a27de-147">You can still run a logic app with a request trigger through the REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span><span class="sxs-lookup"><span data-stu-id="a27de-147">You can still run a logic app with a request trigger through the REST API / Management `/triggers/{triggerName}/run` regardless of IP.</span></span> <span data-ttu-id="a27de-148">This scenario requires authentication against the Azure REST API, and all events would appear in the Azure Audit Log.</span><span class="sxs-lookup"><span data-stu-id="a27de-148">This scenario requires authentication against the Azure REST API, and all events would appear in the Azure Audit Log.</span></span> <span data-ttu-id="a27de-149">Set access control policies accordingly.</span><span class="sxs-lookup"><span data-stu-id="a27de-149">Set access control policies accordingly.</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="a27de-150">Setting IP ranges on the resource definition</span><span class="sxs-lookup"><span data-stu-id="a27de-150">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="a27de-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span><span class="sxs-lookup"><span data-stu-id="a27de-151">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "triggers": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}

```

### <a name="adding-azure-active-directory-oauth-or-other-security"></a><span data-ttu-id="a27de-152">Adding Azure Active Directory, OAuth, or other security</span><span class="sxs-lookup"><span data-stu-id="a27de-152">Adding Azure Active Directory, OAuth, or other security</span></span>

<span data-ttu-id="a27de-153">To add more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with the capability to expose a logic app as an API.</span><span class="sxs-lookup"><span data-stu-id="a27de-153">To add more authorization protocols on top of a logic app, [Azure API Management](https://azure.microsoft.com/services/api-management/) offers rich monitoring, security, policy, and documentation for any endpoint with the capability to expose a logic app as an API.</span></span> <span data-ttu-id="a27de-154">Azure API Management can expose a public or private endpoint for the logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span><span class="sxs-lookup"><span data-stu-id="a27de-154">Azure API Management can expose a public or private endpoint for the logic app, which could use Azure Active Directory, certificate, OAuth, or other security standards.</span></span> <span data-ttu-id="a27de-155">When a request is received, Azure API Management forwards the request to the logic app (performing any needed transformations or restrictions in-flight).</span><span class="sxs-lookup"><span data-stu-id="a27de-155">When a request is received, Azure API Management forwards the request to the logic app (performing any needed transformations or restrictions in-flight).</span></span> <span data-ttu-id="a27de-156">You can use the incoming IP range settings on the logic app to only allow the logic app to be triggered from API Management.</span><span class="sxs-lookup"><span data-stu-id="a27de-156">You can use the incoming IP range settings on the logic app to only allow the logic app to be triggered from API Management.</span></span>

## <a name="secure-access-to-manage-or-edit-logic-apps"></a><span data-ttu-id="a27de-157">Secure access to manage or edit logic apps</span><span class="sxs-lookup"><span data-stu-id="a27de-157">Secure access to manage or edit logic apps</span></span>

<span data-ttu-id="a27de-158">You can restrict access to management operations on a logic app so that only specific users or groups are able to perform operations on the resource.</span><span class="sxs-lookup"><span data-stu-id="a27de-158">You can restrict access to management operations on a logic app so that only specific users or groups are able to perform operations on the resource.</span></span> <span data-ttu-id="a27de-159">Logic apps use the Azure [Role-Based Access Control (RBAC)](../role-based-access-control/role-assignments-portal.md) feature, and can be customized with the same tools.</span><span class="sxs-lookup"><span data-stu-id="a27de-159">Logic apps use the Azure [Role-Based Access Control (RBAC)](../role-based-access-control/role-assignments-portal.md) feature, and can be customized with the same tools.</span></span>  <span data-ttu-id="a27de-160">There are a few built-in roles you can assign members of your subscription to as well:</span><span class="sxs-lookup"><span data-stu-id="a27de-160">There are a few built-in roles you can assign members of your subscription to as well:</span></span>

* <span data-ttu-id="a27de-161">**Logic App Contributor** - Provides access to view, edit, and update a logic app.</span><span class="sxs-lookup"><span data-stu-id="a27de-161">**Logic App Contributor** - Provides access to view, edit, and update a logic app.</span></span>  <span data-ttu-id="a27de-162">Cannot remove the resource or perform admin operations.</span><span class="sxs-lookup"><span data-stu-id="a27de-162">Cannot remove the resource or perform admin operations.</span></span>
* <span data-ttu-id="a27de-163">**Logic App Operator** - Can view the logic app and run history, and enable/disable.</span><span class="sxs-lookup"><span data-stu-id="a27de-163">**Logic App Operator** - Can view the logic app and run history, and enable/disable.</span></span>  <span data-ttu-id="a27de-164">Cannot edit or update the definition.</span><span class="sxs-lookup"><span data-stu-id="a27de-164">Cannot edit or update the definition.</span></span>

<span data-ttu-id="a27de-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) to prevent changing or deleting logic apps.</span><span class="sxs-lookup"><span data-stu-id="a27de-165">You can also use [Azure Resource Lock](../azure-resource-manager/resource-group-lock-resources.md) to prevent changing or deleting logic apps.</span></span> <span data-ttu-id="a27de-166">This capability is valuable to prevent production resources from changes or deletions.</span><span class="sxs-lookup"><span data-stu-id="a27de-166">This capability is valuable to prevent production resources from changes or deletions.</span></span>

## <a name="secure-access-to-contents-of-the-run-history"></a><span data-ttu-id="a27de-167">Secure access to contents of the run history</span><span class="sxs-lookup"><span data-stu-id="a27de-167">Secure access to contents of the run history</span></span>

<span data-ttu-id="a27de-168">You can restrict access to contents of inputs or outputs from previous runs to specific IP address ranges.</span><span class="sxs-lookup"><span data-stu-id="a27de-168">You can restrict access to contents of inputs or outputs from previous runs to specific IP address ranges.</span></span>  

<span data-ttu-id="a27de-169">All data within a workflow run is encrypted in transit and at rest.</span><span class="sxs-lookup"><span data-stu-id="a27de-169">All data within a workflow run is encrypted in transit and at rest.</span></span> <span data-ttu-id="a27de-170">When a call to run history is made, the service authenticates the request and provides links to the request and response inputs and outputs.</span><span class="sxs-lookup"><span data-stu-id="a27de-170">When a call to run history is made, the service authenticates the request and provides links to the request and response inputs and outputs.</span></span> <span data-ttu-id="a27de-171">This link can be protected so only requests to view content from a designated IP address range return the contents.</span><span class="sxs-lookup"><span data-stu-id="a27de-171">This link can be protected so only requests to view content from a designated IP address range return the contents.</span></span> <span data-ttu-id="a27de-172">You can use this capability for additional access control.</span><span class="sxs-lookup"><span data-stu-id="a27de-172">You can use this capability for additional access control.</span></span> <span data-ttu-id="a27de-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span><span class="sxs-lookup"><span data-stu-id="a27de-173">You could even specify an IP address like `0.0.0.0` so no one could access inputs/outputs.</span></span> <span data-ttu-id="a27de-174">Only someone with admin permissions could remove this restriction, providing the possibility for 'just-in-time' access to workflow contents.</span><span class="sxs-lookup"><span data-stu-id="a27de-174">Only someone with admin permissions could remove this restriction, providing the possibility for 'just-in-time' access to workflow contents.</span></span>

<span data-ttu-id="a27de-175">This setting can be configured within the resource settings of the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="a27de-175">This setting can be configured within the resource settings of the Azure portal:</span></span>

1. <span data-ttu-id="a27de-176">In the Azure portal, open the logic app you want to add IP address restrictions</span><span class="sxs-lookup"><span data-stu-id="a27de-176">In the Azure portal, open the logic app you want to add IP address restrictions</span></span>
2. <span data-ttu-id="a27de-177">Click the **Access control configuration** menu item under **Settings**</span><span class="sxs-lookup"><span data-stu-id="a27de-177">Click the **Access control configuration** menu item under **Settings**</span></span>
3. <span data-ttu-id="a27de-178">Specify the list of IP address ranges for access to content</span><span class="sxs-lookup"><span data-stu-id="a27de-178">Specify the list of IP address ranges for access to content</span></span>

#### <a name="setting-ip-ranges-on-the-resource-definition"></a><span data-ttu-id="a27de-179">Setting IP ranges on the resource definition</span><span class="sxs-lookup"><span data-stu-id="a27de-179">Setting IP ranges on the resource definition</span></span>

<span data-ttu-id="a27de-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span><span class="sxs-lookup"><span data-stu-id="a27de-180">If you are using a [deployment template](logic-apps-create-deploy-template.md) to automate your deployments, the IP range settings can be configured on the resource template.</span></span>  

``` json
{
    "properties": {
        "definition": {
        },
        "parameters": {},
        "accessControl": {
            "contents": {
                "allowedCallerIpAddresses": [
                    {
                        "addressRange": "192.168.12.0/23"
                    },
                    {
                        "addressRange": "2001:0db8::/64"
                    }
                ]
            }
        }
    },
    "type": "Microsoft.Logic/workflows"
}
```

## <a name="secure-parameters-and-inputs-within-a-workflow"></a><span data-ttu-id="a27de-181">Secure parameters and inputs within a workflow</span><span class="sxs-lookup"><span data-stu-id="a27de-181">Secure parameters and inputs within a workflow</span></span>

<span data-ttu-id="a27de-182">You might want to parameterize some aspects of a workflow definition for deployment across environments.</span><span class="sxs-lookup"><span data-stu-id="a27de-182">You might want to parameterize some aspects of a workflow definition for deployment across environments.</span></span> <span data-ttu-id="a27de-183">Also, some parameters might be secure parameters you don't want to appear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span><span class="sxs-lookup"><span data-stu-id="a27de-183">Also, some parameters might be secure parameters you don't want to appear when editing a workflow, such as a client ID and client secret for [Azure Active Directory authentication](../connectors/connectors-native-http.md#authentication) of an HTTP action.</span></span>

### <a name="using-parameters-and-secure-parameters"></a><span data-ttu-id="a27de-184">Using parameters and secure parameters</span><span class="sxs-lookup"><span data-stu-id="a27de-184">Using parameters and secure parameters</span></span>

<span data-ttu-id="a27de-185">To access the value of a resource parameter at runtime, the [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span><span class="sxs-lookup"><span data-stu-id="a27de-185">To access the value of a resource parameter at runtime, the [workflow definition language](http://aka.ms/logicappsdocs) provides a `@parameters()` operation.</span></span> <span data-ttu-id="a27de-186">Also, you can [specify parameters in the resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="a27de-186">Also, you can [specify parameters in the resource deployment template](../azure-resource-manager/resource-group-authoring-templates.md#parameters).</span></span> <span data-ttu-id="a27de-187">But if you specify the parameter type as `securestring`, the parameter won't be returned with the rest of the resource definition, and won't be accessible by viewing the resource after deployment.</span><span class="sxs-lookup"><span data-stu-id="a27de-187">But if you specify the parameter type as `securestring`, the parameter won't be returned with the rest of the resource definition, and won't be accessible by viewing the resource after deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="a27de-188">If your parameter is used in the headers or body of a request, the parameter might be visible by accessing the run history and outgoing HTTP request.</span><span class="sxs-lookup"><span data-stu-id="a27de-188">If your parameter is used in the headers or body of a request, the parameter might be visible by accessing the run history and outgoing HTTP request.</span></span> <span data-ttu-id="a27de-189">Make sure to set your content access policies accordingly.</span><span class="sxs-lookup"><span data-stu-id="a27de-189">Make sure to set your content access policies accordingly.</span></span>
> <span data-ttu-id="a27de-190">Authorization headers are never visible through inputs or outputs.</span><span class="sxs-lookup"><span data-stu-id="a27de-190">Authorization headers are never visible through inputs or outputs.</span></span> <span data-ttu-id="a27de-191">So if the secret is being used there, the secret is not retrievable.</span><span class="sxs-lookup"><span data-stu-id="a27de-191">So if the secret is being used there, the secret is not retrievable.</span></span>

#### <a name="resource-deployment-template-with-secrets"></a><span data-ttu-id="a27de-192">Resource deployment template with secrets</span><span class="sxs-lookup"><span data-stu-id="a27de-192">Resource deployment template with secrets</span></span>

<span data-ttu-id="a27de-193">The following example shows a deployment that references a secure parameter of `secret` at runtime.</span><span class="sxs-lookup"><span data-stu-id="a27de-193">The following example shows a deployment that references a secure parameter of `secret` at runtime.</span></span> <span data-ttu-id="a27de-194">In a separate parameters file, you could specify the environment value for the `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) to retrieve secrets at deploy time.</span><span class="sxs-lookup"><span data-stu-id="a27de-194">In a separate parameters file, you could specify the environment value for the `secret`, or use [Azure Resource Manager KeyVault](../azure-resource-manager/resource-manager-keyvault-parameter.md) to retrieve secrets at deploy time.</span></span>

``` json
{
   "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
   "contentVersion": "1.0.0.0",
   "parameters": {
      "secretDeploymentParam": {
         "type": "securestring"
      }
   },
   "variables": {},
   "resources": [ {
      "name": "secret-deploy",
      "type": "Microsoft.Logic/workflows",
      "location": "westus",
      "tags": {
         "displayName": "LogicApp"
      },
      "apiVersion": "2016-06-01",
      "properties": {
         "definition": {
            "$schema": "https://schema.management.azure.com/schemas/2016-06-01/Microsoft.Logic.json",
            "actions": {
               "Call_External_API": {
                  "type": "Http",
                  "inputs": {
                     "headers": {
                        "Authorization": "@parameters('secret')"
                     },
                     "body": "This is the request"
                  },
                  "runAfter": {}
               }
            },
            "parameters": {
               "secret": {
                  "type": "SecureString"
               }
            },
            "triggers": {
               "manual": {
                  "type": "Request",
                  "kind": "Http",
                  "inputs": {
                     "schema": {}
                  }
               }
            },
            "contentVersion": "1.0.0.0",
            "outputs": {}
         },
         "parameters": {
            "secret": {
               "value": "[parameters('secretDeploymentParam')]"
            }
         }
      }
   } ],
   "outputs": {}
}
```

## <a name="secure-access-to-services-receiving-requests-from-a-workflow"></a><span data-ttu-id="a27de-195">Secure access to services receiving requests from a workflow</span><span class="sxs-lookup"><span data-stu-id="a27de-195">Secure access to services receiving requests from a workflow</span></span>

<span data-ttu-id="a27de-196">There are many ways to help secure any endpoint the logic app needs to access.</span><span class="sxs-lookup"><span data-stu-id="a27de-196">There are many ways to help secure any endpoint the logic app needs to access.</span></span>

### <a name="using-authentication-on-outbound-requests"></a><span data-ttu-id="a27de-197">Using authentication on outbound requests</span><span class="sxs-lookup"><span data-stu-id="a27de-197">Using authentication on outbound requests</span></span>

<span data-ttu-id="a27de-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication to the request being sent.</span><span class="sxs-lookup"><span data-stu-id="a27de-198">When working with an HTTP, HTTP + Swagger (Open API), or Webhook action, you can add authentication to the request being sent.</span></span> <span data-ttu-id="a27de-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span><span class="sxs-lookup"><span data-stu-id="a27de-199">You could include basic authentication, certificate authentication, or Azure Active Directory authentication.</span></span> <span data-ttu-id="a27de-200">Details on how to configure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span><span class="sxs-lookup"><span data-stu-id="a27de-200">Details on how to configure this authentication can be found [in this article](../connectors/connectors-native-http.md#authentication).</span></span>

### <a name="restricting-access-to-logic-app-ip-addresses"></a><span data-ttu-id="a27de-201">Restricting access to logic app IP addresses</span><span class="sxs-lookup"><span data-stu-id="a27de-201">Restricting access to logic app IP addresses</span></span>

<span data-ttu-id="a27de-202">All calls from logic apps come from a specific set of IP addresses per region.</span><span class="sxs-lookup"><span data-stu-id="a27de-202">All calls from logic apps come from a specific set of IP addresses per region.</span></span> <span data-ttu-id="a27de-203">You can add additional filtering to only accept requests from those designated IP addresses.</span><span class="sxs-lookup"><span data-stu-id="a27de-203">You can add additional filtering to only accept requests from those designated IP addresses.</span></span> <span data-ttu-id="a27de-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span><span class="sxs-lookup"><span data-stu-id="a27de-204">For a list of those IP addresses, see [logic app limits and configuration](logic-apps-limits-and-config.md#configuration).</span></span>

### <a name="on-premises-connectivity"></a><span data-ttu-id="a27de-205">On-premises connectivity</span><span class="sxs-lookup"><span data-stu-id="a27de-205">On-premises connectivity</span></span>

<span data-ttu-id="a27de-206">Logic apps provide integration with several services to provide secure and reliable on-premises communication.</span><span class="sxs-lookup"><span data-stu-id="a27de-206">Logic apps provide integration with several services to provide secure and reliable on-premises communication.</span></span>

#### <a name="on-premises-data-gateway"></a><span data-ttu-id="a27de-207">On-premises data gateway</span><span class="sxs-lookup"><span data-stu-id="a27de-207">On-premises data gateway</span></span>

<span data-ttu-id="a27de-208">Many managed connectors for logic apps provide secure connectivity to on-premises systems, including File System, SQL, SharePoint, DB2, and more.</span><span class="sxs-lookup"><span data-stu-id="a27de-208">Many managed connectors for logic apps provide secure connectivity to on-premises systems, including File System, SQL, SharePoint, DB2, and more.</span></span> <span data-ttu-id="a27de-209">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="a27de-209">The gateway relays data from on-premises sources on encrypted channels through the Azure Service Bus.</span></span> <span data-ttu-id="a27de-210">All traffic originates as secure outbound traffic from the gateway agent.</span><span class="sxs-lookup"><span data-stu-id="a27de-210">All traffic originates as secure outbound traffic from the gateway agent.</span></span> <span data-ttu-id="a27de-211">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span><span class="sxs-lookup"><span data-stu-id="a27de-211">Learn more about [how the data gateway works](logic-apps-gateway-install.md#gateway-cloud-service).</span></span>

#### <a name="azure-api-management"></a><span data-ttu-id="a27de-212">Azure API Management</span><span class="sxs-lookup"><span data-stu-id="a27de-212">Azure API Management</span></span>

<span data-ttu-id="a27de-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication to on-premises systems.</span><span class="sxs-lookup"><span data-stu-id="a27de-213">[Azure API Management](https://azure.microsoft.com/services/api-management/) has on-premises connectivity options, including site-to-site VPN and ExpressRoute integration for secured proxy and communication to on-premises systems.</span></span> <span data-ttu-id="a27de-214">In the Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access to on-premises systems.</span><span class="sxs-lookup"><span data-stu-id="a27de-214">In the Logic App Designer, you can quickly select an API exposed from Azure API Management within a workflow, providing quick access to on-premises systems.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a27de-215">Next steps</span><span class="sxs-lookup"><span data-stu-id="a27de-215">Next steps</span></span>
[<span data-ttu-id="a27de-216">Create a deployment template</span><span class="sxs-lookup"><span data-stu-id="a27de-216">Create a deployment template</span></span>](logic-apps-create-deploy-template.md)  
[<span data-ttu-id="a27de-217">Exception handling</span><span class="sxs-lookup"><span data-stu-id="a27de-217">Exception handling</span></span>](logic-apps-exception-handling.md)  
[<span data-ttu-id="a27de-218">Monitor your logic apps</span><span class="sxs-lookup"><span data-stu-id="a27de-218">Monitor your logic apps</span></span>](logic-apps-monitor-your-logic-apps.md)  
[<span data-ttu-id="a27de-219">Diagnosing logic app failures and issues</span><span class="sxs-lookup"><span data-stu-id="a27de-219">Diagnosing logic app failures and issues</span></span>](logic-apps-diagnosing-failures.md)  
