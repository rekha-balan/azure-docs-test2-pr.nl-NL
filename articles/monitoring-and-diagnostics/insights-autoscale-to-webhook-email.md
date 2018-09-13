---
title: Use autoscale to send email and webhook alert notifications
description: 'See how to use autoscale actions to call web URLs or send email notifications in Azure Monitor. '
author: anirudhcavale
services: azure-monitor
ms.service: azure-monitor
ms.topic: conceptual
ms.date: 04/03/2017
ms.author: ancav
ms.component: autoscale
ms.openlocfilehash: 65405a6d7f1d49911da1e2a5d26b02098a261c01
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44779381"
---
# <a name="use-autoscale-actions-to-send-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="9f1bc-103">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="9f1bc-103">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="9f1bc-104">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-104">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="9f1bc-105">Webhooks</span><span class="sxs-lookup"><span data-stu-id="9f1bc-105">Webhooks</span></span>
<span data-ttu-id="9f1bc-106">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-106">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span></span> <span data-ttu-id="9f1bc-107">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-107">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="9f1bc-108">Email</span><span class="sxs-lookup"><span data-stu-id="9f1bc-108">Email</span></span>
<span data-ttu-id="9f1bc-109">Email can be sent to any valid email address.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-109">Email can be sent to any valid email address.</span></span> <span data-ttu-id="9f1bc-110">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-110">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="9f1bc-111">Cloud Services and Web Apps</span><span class="sxs-lookup"><span data-stu-id="9f1bc-111">Cloud Services and Web Apps</span></span>
<span data-ttu-id="9f1bc-112">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span><span class="sxs-lookup"><span data-stu-id="9f1bc-112">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="9f1bc-113">Choose the **scale by** metric.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-113">Choose the **scale by** metric.</span></span>

![scale by](./media/insights-autoscale-to-webhook-email/insights-autoscale-notify.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="9f1bc-115">Virtual Machine scale sets</span><span class="sxs-lookup"><span data-stu-id="9f1bc-115">Virtual Machine scale sets</span></span>
<span data-ttu-id="9f1bc-116">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-116">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="9f1bc-117">A portal interface is not yet available.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-117">A portal interface is not yet available.</span></span>
<span data-ttu-id="9f1bc-118">When using the REST API or Resource Manager template, include the notifications element with the following options.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-118">When using the REST API or Resource Manager template, include the notifications element with the following options.</span></span>

```
"notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": false,
          "sendToSubscriptionCoAdministrators": false,
          "customEmails": [
              "user1@mycompany.com",
              "user2@mycompany.com"
              ]
        },
        "webhooks": [
          {
            "serviceUri": "https://foo.webhook.example.com?token=abcd1234",
            "properties": {
              "optional_key1": "optional_value1",
              "optional_key2": "optional_value2"
            }
          }
        ]
      }
    ]
```
| <span data-ttu-id="9f1bc-119">Field</span><span class="sxs-lookup"><span data-stu-id="9f1bc-119">Field</span></span> | <span data-ttu-id="9f1bc-120">Mandatory?</span><span class="sxs-lookup"><span data-stu-id="9f1bc-120">Mandatory?</span></span> | <span data-ttu-id="9f1bc-121">Description</span><span class="sxs-lookup"><span data-stu-id="9f1bc-121">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f1bc-122">operation</span><span class="sxs-lookup"><span data-stu-id="9f1bc-122">operation</span></span> |<span data-ttu-id="9f1bc-123">yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-123">yes</span></span> |<span data-ttu-id="9f1bc-124">value must be "Scale"</span><span class="sxs-lookup"><span data-stu-id="9f1bc-124">value must be "Scale"</span></span> |
| <span data-ttu-id="9f1bc-125">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="9f1bc-125">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="9f1bc-126">yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-126">yes</span></span> |<span data-ttu-id="9f1bc-127">value must be "true" or "false"</span><span class="sxs-lookup"><span data-stu-id="9f1bc-127">value must be "true" or "false"</span></span> |
| <span data-ttu-id="9f1bc-128">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="9f1bc-128">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="9f1bc-129">yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-129">yes</span></span> |<span data-ttu-id="9f1bc-130">value must be "true" or "false"</span><span class="sxs-lookup"><span data-stu-id="9f1bc-130">value must be "true" or "false"</span></span> |
| <span data-ttu-id="9f1bc-131">customEmails</span><span class="sxs-lookup"><span data-stu-id="9f1bc-131">customEmails</span></span> |<span data-ttu-id="9f1bc-132">yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-132">yes</span></span> |<span data-ttu-id="9f1bc-133">value can be null [] or string array of emails</span><span class="sxs-lookup"><span data-stu-id="9f1bc-133">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="9f1bc-134">webhooks</span><span class="sxs-lookup"><span data-stu-id="9f1bc-134">webhooks</span></span> |<span data-ttu-id="9f1bc-135">yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-135">yes</span></span> |<span data-ttu-id="9f1bc-136">value can be null or valid Uri</span><span class="sxs-lookup"><span data-stu-id="9f1bc-136">value can be null or valid Uri</span></span> |
| <span data-ttu-id="9f1bc-137">serviceUri</span><span class="sxs-lookup"><span data-stu-id="9f1bc-137">serviceUri</span></span> |<span data-ttu-id="9f1bc-138">yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-138">yes</span></span> |<span data-ttu-id="9f1bc-139">a valid https Uri</span><span class="sxs-lookup"><span data-stu-id="9f1bc-139">a valid https Uri</span></span> |
| <span data-ttu-id="9f1bc-140">properties</span><span class="sxs-lookup"><span data-stu-id="9f1bc-140">properties</span></span> |<span data-ttu-id="9f1bc-141">yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-141">yes</span></span> |<span data-ttu-id="9f1bc-142">value must be empty {} or can contain key-value pairs</span><span class="sxs-lookup"><span data-stu-id="9f1bc-142">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="9f1bc-143">Authentication in webhooks</span><span class="sxs-lookup"><span data-stu-id="9f1bc-143">Authentication in webhooks</span></span>
<span data-ttu-id="9f1bc-144">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-144">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="9f1bc-145">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="9f1bc-145">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="9f1bc-146">Autoscale notification webhook payload schema</span><span class="sxs-lookup"><span data-stu-id="9f1bc-146">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="9f1bc-147">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span><span class="sxs-lookup"><span data-stu-id="9f1bc-147">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span></span>

```
{
        "version": "1.0",
        "status": "Activated",
        "operation": "Scale In",
        "context": {
                "timestamp": "2016-03-11T07:31:04.5834118Z",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/autoscalesettings/myautoscaleSetting",
                "name": "myautoscaleSetting",
                "details": "Autoscale successfully started scale operation for resource 'MyCSRole' from capacity '3' to capacity '2'",
                "subscriptionId": "s1",
                "resourceGroupName": "rg1",
                "resourceName": "MyCSRole",
                "resourceType": "microsoft.classiccompute/domainnames/slots/roles",
                "resourceId": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService/slots/Production/roles/MyCSRole",
                "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/rg1/providers/microsoft.classicCompute/domainNames/myCloudService",
                "oldCapacity": "3",
                "newCapacity": "2"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```


| <span data-ttu-id="9f1bc-148">Field</span><span class="sxs-lookup"><span data-stu-id="9f1bc-148">Field</span></span> | <span data-ttu-id="9f1bc-149">Mandatory?</span><span class="sxs-lookup"><span data-stu-id="9f1bc-149">Mandatory?</span></span> | <span data-ttu-id="9f1bc-150">Description</span><span class="sxs-lookup"><span data-stu-id="9f1bc-150">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="9f1bc-151">status</span><span class="sxs-lookup"><span data-stu-id="9f1bc-151">status</span></span> |<span data-ttu-id="9f1bc-152">yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-152">yes</span></span> |<span data-ttu-id="9f1bc-153">The status that indicates that an autoscale action was generated</span><span class="sxs-lookup"><span data-stu-id="9f1bc-153">The status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="9f1bc-154">operation</span><span class="sxs-lookup"><span data-stu-id="9f1bc-154">operation</span></span> |<span data-ttu-id="9f1bc-155">yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-155">yes</span></span> |<span data-ttu-id="9f1bc-156">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span><span class="sxs-lookup"><span data-stu-id="9f1bc-156">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="9f1bc-157">context</span><span class="sxs-lookup"><span data-stu-id="9f1bc-157">context</span></span> |<span data-ttu-id="9f1bc-158">yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-158">yes</span></span> |<span data-ttu-id="9f1bc-159">The autoscale action context</span><span class="sxs-lookup"><span data-stu-id="9f1bc-159">The autoscale action context</span></span> |
| <span data-ttu-id="9f1bc-160">timestamp</span><span class="sxs-lookup"><span data-stu-id="9f1bc-160">timestamp</span></span> |<span data-ttu-id="9f1bc-161">yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-161">yes</span></span> |<span data-ttu-id="9f1bc-162">Time stamp when the autoscale action was triggered</span><span class="sxs-lookup"><span data-stu-id="9f1bc-162">Time stamp when the autoscale action was triggered</span></span> |
| <span data-ttu-id="9f1bc-163">id</span><span class="sxs-lookup"><span data-stu-id="9f1bc-163">id</span></span> |<span data-ttu-id="9f1bc-164">Yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-164">Yes</span></span> |<span data-ttu-id="9f1bc-165">Resource Manager ID of the autoscale setting</span><span class="sxs-lookup"><span data-stu-id="9f1bc-165">Resource Manager ID of the autoscale setting</span></span> |
| <span data-ttu-id="9f1bc-166">name</span><span class="sxs-lookup"><span data-stu-id="9f1bc-166">name</span></span> |<span data-ttu-id="9f1bc-167">Yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-167">Yes</span></span> |<span data-ttu-id="9f1bc-168">The name of the autoscale setting</span><span class="sxs-lookup"><span data-stu-id="9f1bc-168">The name of the autoscale setting</span></span> |
| <span data-ttu-id="9f1bc-169">details</span><span class="sxs-lookup"><span data-stu-id="9f1bc-169">details</span></span> |<span data-ttu-id="9f1bc-170">Yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-170">Yes</span></span> |<span data-ttu-id="9f1bc-171">Explanation of the action that the autoscale service took and the change in the instance count</span><span class="sxs-lookup"><span data-stu-id="9f1bc-171">Explanation of the action that the autoscale service took and the change in the instance count</span></span> |
| <span data-ttu-id="9f1bc-172">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="9f1bc-172">subscriptionId</span></span> |<span data-ttu-id="9f1bc-173">Yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-173">Yes</span></span> |<span data-ttu-id="9f1bc-174">Subscription ID of the target resource that is being scaled</span><span class="sxs-lookup"><span data-stu-id="9f1bc-174">Subscription ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="9f1bc-175">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="9f1bc-175">resourceGroupName</span></span> |<span data-ttu-id="9f1bc-176">Yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-176">Yes</span></span> |<span data-ttu-id="9f1bc-177">Resource Group name of the target resource that is being scaled</span><span class="sxs-lookup"><span data-stu-id="9f1bc-177">Resource Group name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="9f1bc-178">resourceName</span><span class="sxs-lookup"><span data-stu-id="9f1bc-178">resourceName</span></span> |<span data-ttu-id="9f1bc-179">Yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-179">Yes</span></span> |<span data-ttu-id="9f1bc-180">Name of the target resource that is being scaled</span><span class="sxs-lookup"><span data-stu-id="9f1bc-180">Name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="9f1bc-181">resourceType</span><span class="sxs-lookup"><span data-stu-id="9f1bc-181">resourceType</span></span> |<span data-ttu-id="9f1bc-182">Yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-182">Yes</span></span> |<span data-ttu-id="9f1bc-183">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span><span class="sxs-lookup"><span data-stu-id="9f1bc-183">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="9f1bc-184">resourceId</span><span class="sxs-lookup"><span data-stu-id="9f1bc-184">resourceId</span></span> |<span data-ttu-id="9f1bc-185">Yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-185">Yes</span></span> |<span data-ttu-id="9f1bc-186">Resource Manager ID of the target resource that is being scaled</span><span class="sxs-lookup"><span data-stu-id="9f1bc-186">Resource Manager ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="9f1bc-187">portalLink</span><span class="sxs-lookup"><span data-stu-id="9f1bc-187">portalLink</span></span> |<span data-ttu-id="9f1bc-188">Yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-188">Yes</span></span> |<span data-ttu-id="9f1bc-189">Azure portal link to the summary page of the target resource</span><span class="sxs-lookup"><span data-stu-id="9f1bc-189">Azure portal link to the summary page of the target resource</span></span> |
| <span data-ttu-id="9f1bc-190">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="9f1bc-190">oldCapacity</span></span> |<span data-ttu-id="9f1bc-191">Yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-191">Yes</span></span> |<span data-ttu-id="9f1bc-192">The current (old) instance count when Autoscale took a scale action</span><span class="sxs-lookup"><span data-stu-id="9f1bc-192">The current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="9f1bc-193">newCapacity</span><span class="sxs-lookup"><span data-stu-id="9f1bc-193">newCapacity</span></span> |<span data-ttu-id="9f1bc-194">Yes</span><span class="sxs-lookup"><span data-stu-id="9f1bc-194">Yes</span></span> |<span data-ttu-id="9f1bc-195">The new instance count that Autoscale scaled the resource to</span><span class="sxs-lookup"><span data-stu-id="9f1bc-195">The new instance count that Autoscale scaled the resource to</span></span> |
| <span data-ttu-id="9f1bc-196">Properties</span><span class="sxs-lookup"><span data-stu-id="9f1bc-196">Properties</span></span> |<span data-ttu-id="9f1bc-197">No</span><span class="sxs-lookup"><span data-stu-id="9f1bc-197">No</span></span> |<span data-ttu-id="9f1bc-198">Optional.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-198">Optional.</span></span> <span data-ttu-id="9f1bc-199">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span><span class="sxs-lookup"><span data-stu-id="9f1bc-199">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="9f1bc-200">The properties field is optional.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-200">The properties field is optional.</span></span> <span data-ttu-id="9f1bc-201">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span><span class="sxs-lookup"><span data-stu-id="9f1bc-201">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span></span> <span data-ttu-id="9f1bc-202">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span><span class="sxs-lookup"><span data-stu-id="9f1bc-202">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span></span> |
