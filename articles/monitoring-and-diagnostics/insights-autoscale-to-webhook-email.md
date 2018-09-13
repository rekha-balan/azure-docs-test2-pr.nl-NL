---
title: Use autoscale actions to send email and webhook alert notifications. | Microsoft Docs
description: 'See how to use autoscale actions to call web URLs or send email notifications in Azure Monitor. '
author: kamathashwin
manager: carolz
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: eb9a4c98-0894-488c-8ee8-5df0065d094f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: ashwink
ms.openlocfilehash: bbf189c8c3a8925e46674c0bb759dca64b0054f1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671440"
---
# <a name="use-autoscale-actions-to-send-email-and-webhook-alert-notifications-in-azure-monitor"></a><span data-ttu-id="4d6c8-104">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span><span class="sxs-lookup"><span data-stu-id="4d6c8-104">Use autoscale actions to send email and webhook alert notifications in Azure Monitor</span></span>
<span data-ttu-id="4d6c8-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-105">This article shows you how set up triggers so that you can call specific web URLs or send emails based on autoscale actions in Azure.</span></span>  

## <a name="webhooks"></a><span data-ttu-id="4d6c8-106">Webhooks</span><span class="sxs-lookup"><span data-stu-id="4d6c8-106">Webhooks</span></span>
<span data-ttu-id="4d6c8-107">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-107">Webhooks allow you to route the Azure alert notifications to other systems for post-processing or custom notifications.</span></span> <span data-ttu-id="4d6c8-108">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-108">For example, routing the alert to services that can handle an incoming web request to send SMS, log bugs, notify a team using chat or messaging services, etc. The webhook URI must be a valid HTTP or HTTPS endpoint.</span></span>

## <a name="email"></a><span data-ttu-id="4d6c8-109">Email</span><span class="sxs-lookup"><span data-stu-id="4d6c8-109">Email</span></span>
<span data-ttu-id="4d6c8-110">Email can be sent to any valid email address.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-110">Email can be sent to any valid email address.</span></span> <span data-ttu-id="4d6c8-111">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-111">Administrators and co-administrators of the subscription where the rule is running will also be notified.</span></span>

## <a name="cloud-services-and-web-apps"></a><span data-ttu-id="4d6c8-112">Cloud Services and Web Apps</span><span class="sxs-lookup"><span data-stu-id="4d6c8-112">Cloud Services and Web Apps</span></span>
<span data-ttu-id="4d6c8-113">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span><span class="sxs-lookup"><span data-stu-id="4d6c8-113">You can opt-in from the Azure portal for Cloud Services and Server Farms (Web Apps).</span></span>

* <span data-ttu-id="4d6c8-114">Choose the **scale by** metric.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-114">Choose the **scale by** metric.</span></span>

![scale by](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-autoscale-to-webhook-email/insights-autoscale-scale-by.png)

## <a name="virtual-machine-scale-sets"></a><span data-ttu-id="4d6c8-116">Virtual Machine scale sets</span><span class="sxs-lookup"><span data-stu-id="4d6c8-116">Virtual Machine scale sets</span></span>
<span data-ttu-id="4d6c8-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-117">For newer Virtual Machines created with Resource Manager (Virtual Machine scale sets), you can configure this using REST API, Resource Manager templates, PowerShell, and CLI.</span></span> <span data-ttu-id="4d6c8-118">A portal interface is not yet available.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-118">A portal interface is not yet available.</span></span>
<span data-ttu-id="4d6c8-119">When using the REST API or Resource Manager template, include the notifications element with the following options.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-119">When using the REST API or Resource Manager template, include the notifications element with the following options.</span></span>

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
| <span data-ttu-id="4d6c8-120">Field</span><span class="sxs-lookup"><span data-stu-id="4d6c8-120">Field</span></span> | <span data-ttu-id="4d6c8-121">Mandatory?</span><span class="sxs-lookup"><span data-stu-id="4d6c8-121">Mandatory?</span></span> | <span data-ttu-id="4d6c8-122">Description</span><span class="sxs-lookup"><span data-stu-id="4d6c8-122">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d6c8-123">operation</span><span class="sxs-lookup"><span data-stu-id="4d6c8-123">operation</span></span> |<span data-ttu-id="4d6c8-124">yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-124">yes</span></span> |<span data-ttu-id="4d6c8-125">value must be "Scale"</span><span class="sxs-lookup"><span data-stu-id="4d6c8-125">value must be "Scale"</span></span> |
| <span data-ttu-id="4d6c8-126">sendToSubscriptionAdministrator</span><span class="sxs-lookup"><span data-stu-id="4d6c8-126">sendToSubscriptionAdministrator</span></span> |<span data-ttu-id="4d6c8-127">yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-127">yes</span></span> |<span data-ttu-id="4d6c8-128">value must be "true" or "false"</span><span class="sxs-lookup"><span data-stu-id="4d6c8-128">value must be "true" or "false"</span></span> |
| <span data-ttu-id="4d6c8-129">sendToSubscriptionCoAdministrators</span><span class="sxs-lookup"><span data-stu-id="4d6c8-129">sendToSubscriptionCoAdministrators</span></span> |<span data-ttu-id="4d6c8-130">yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-130">yes</span></span> |<span data-ttu-id="4d6c8-131">value must be "true" or "false"</span><span class="sxs-lookup"><span data-stu-id="4d6c8-131">value must be "true" or "false"</span></span> |
| <span data-ttu-id="4d6c8-132">customEmails</span><span class="sxs-lookup"><span data-stu-id="4d6c8-132">customEmails</span></span> |<span data-ttu-id="4d6c8-133">yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-133">yes</span></span> |<span data-ttu-id="4d6c8-134">value can be null [] or string array of emails</span><span class="sxs-lookup"><span data-stu-id="4d6c8-134">value can be null [] or string array of emails</span></span> |
| <span data-ttu-id="4d6c8-135">webhooks</span><span class="sxs-lookup"><span data-stu-id="4d6c8-135">webhooks</span></span> |<span data-ttu-id="4d6c8-136">yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-136">yes</span></span> |<span data-ttu-id="4d6c8-137">value can be null or valid Uri</span><span class="sxs-lookup"><span data-stu-id="4d6c8-137">value can be null or valid Uri</span></span> |
| <span data-ttu-id="4d6c8-138">serviceUri</span><span class="sxs-lookup"><span data-stu-id="4d6c8-138">serviceUri</span></span> |<span data-ttu-id="4d6c8-139">yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-139">yes</span></span> |<span data-ttu-id="4d6c8-140">a valid https Uri</span><span class="sxs-lookup"><span data-stu-id="4d6c8-140">a valid https Uri</span></span> |
| <span data-ttu-id="4d6c8-141">properties</span><span class="sxs-lookup"><span data-stu-id="4d6c8-141">properties</span></span> |<span data-ttu-id="4d6c8-142">yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-142">yes</span></span> |<span data-ttu-id="4d6c8-143">value must be empty {} or can contain key-value pairs</span><span class="sxs-lookup"><span data-stu-id="4d6c8-143">value must be empty {} or can contain key-value pairs</span></span> |

## <a name="authentication-in-webhooks"></a><span data-ttu-id="4d6c8-144">Authentication in webhooks</span><span class="sxs-lookup"><span data-stu-id="4d6c8-144">Authentication in webhooks</span></span>
<span data-ttu-id="4d6c8-145">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-145">The webhook can authenticate using token-based authentication, where you save the webhook URI with a token ID as a query parameter.</span></span> <span data-ttu-id="4d6c8-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span><span class="sxs-lookup"><span data-stu-id="4d6c8-146">For example, https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue</span></span>

## <a name="autoscale-notification-webhook-payload-schema"></a><span data-ttu-id="4d6c8-147">Autoscale notification webhook payload schema</span><span class="sxs-lookup"><span data-stu-id="4d6c8-147">Autoscale notification webhook payload schema</span></span>
<span data-ttu-id="4d6c8-148">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span><span class="sxs-lookup"><span data-stu-id="4d6c8-148">When the autoscale notification is generated, the following metadata is included in the webhook payload:</span></span>

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


| <span data-ttu-id="4d6c8-149">Field</span><span class="sxs-lookup"><span data-stu-id="4d6c8-149">Field</span></span> | <span data-ttu-id="4d6c8-150">Mandatory?</span><span class="sxs-lookup"><span data-stu-id="4d6c8-150">Mandatory?</span></span> | <span data-ttu-id="4d6c8-151">Description</span><span class="sxs-lookup"><span data-stu-id="4d6c8-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4d6c8-152">status</span><span class="sxs-lookup"><span data-stu-id="4d6c8-152">status</span></span> |<span data-ttu-id="4d6c8-153">yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-153">yes</span></span> |<span data-ttu-id="4d6c8-154">The status that indicates that an autoscale action was generated</span><span class="sxs-lookup"><span data-stu-id="4d6c8-154">The status that indicates that an autoscale action was generated</span></span> |
| <span data-ttu-id="4d6c8-155">operation</span><span class="sxs-lookup"><span data-stu-id="4d6c8-155">operation</span></span> |<span data-ttu-id="4d6c8-156">yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-156">yes</span></span> |<span data-ttu-id="4d6c8-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span><span class="sxs-lookup"><span data-stu-id="4d6c8-157">For an increase of instances, it will be "Scale Out" and for a decrease in instances, it will be "Scale In"</span></span> |
| <span data-ttu-id="4d6c8-158">context</span><span class="sxs-lookup"><span data-stu-id="4d6c8-158">context</span></span> |<span data-ttu-id="4d6c8-159">yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-159">yes</span></span> |<span data-ttu-id="4d6c8-160">The autoscale action context</span><span class="sxs-lookup"><span data-stu-id="4d6c8-160">The autoscale action context</span></span> |
| <span data-ttu-id="4d6c8-161">timestamp</span><span class="sxs-lookup"><span data-stu-id="4d6c8-161">timestamp</span></span> |<span data-ttu-id="4d6c8-162">yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-162">yes</span></span> |<span data-ttu-id="4d6c8-163">Time stamp when the autoscale action was triggered</span><span class="sxs-lookup"><span data-stu-id="4d6c8-163">Time stamp when the autoscale action was triggered</span></span> |
| <span data-ttu-id="4d6c8-164">id</span><span class="sxs-lookup"><span data-stu-id="4d6c8-164">id</span></span> |<span data-ttu-id="4d6c8-165">Yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-165">Yes</span></span> |<span data-ttu-id="4d6c8-166">Resource Manager ID of the autoscale setting</span><span class="sxs-lookup"><span data-stu-id="4d6c8-166">Resource Manager ID of the autoscale setting</span></span> |
| <span data-ttu-id="4d6c8-167">name</span><span class="sxs-lookup"><span data-stu-id="4d6c8-167">name</span></span> |<span data-ttu-id="4d6c8-168">Yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-168">Yes</span></span> |<span data-ttu-id="4d6c8-169">The name of the autoscale setting</span><span class="sxs-lookup"><span data-stu-id="4d6c8-169">The name of the autoscale setting</span></span> |
| <span data-ttu-id="4d6c8-170">details</span><span class="sxs-lookup"><span data-stu-id="4d6c8-170">details</span></span> |<span data-ttu-id="4d6c8-171">Yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-171">Yes</span></span> |<span data-ttu-id="4d6c8-172">Explanation of the action that the autoscale service took and the change in the instance count</span><span class="sxs-lookup"><span data-stu-id="4d6c8-172">Explanation of the action that the autoscale service took and the change in the instance count</span></span> |
| <span data-ttu-id="4d6c8-173">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4d6c8-173">subscriptionId</span></span> |<span data-ttu-id="4d6c8-174">Yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-174">Yes</span></span> |<span data-ttu-id="4d6c8-175">Subscription ID of the target resource that is being scaled</span><span class="sxs-lookup"><span data-stu-id="4d6c8-175">Subscription ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="4d6c8-176">resourceGroupName</span><span class="sxs-lookup"><span data-stu-id="4d6c8-176">resourceGroupName</span></span> |<span data-ttu-id="4d6c8-177">Yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-177">Yes</span></span> |<span data-ttu-id="4d6c8-178">Resource Group name of the target resource that is being scaled</span><span class="sxs-lookup"><span data-stu-id="4d6c8-178">Resource Group name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="4d6c8-179">resourceName</span><span class="sxs-lookup"><span data-stu-id="4d6c8-179">resourceName</span></span> |<span data-ttu-id="4d6c8-180">Yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-180">Yes</span></span> |<span data-ttu-id="4d6c8-181">Name of the target resource that is being scaled</span><span class="sxs-lookup"><span data-stu-id="4d6c8-181">Name of the target resource that is being scaled</span></span> |
| <span data-ttu-id="4d6c8-182">resourceType</span><span class="sxs-lookup"><span data-stu-id="4d6c8-182">resourceType</span></span> |<span data-ttu-id="4d6c8-183">Yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-183">Yes</span></span> |<span data-ttu-id="4d6c8-184">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span><span class="sxs-lookup"><span data-stu-id="4d6c8-184">The three supported values: "microsoft.classiccompute/domainnames/slots/roles" - Cloud Service roles, "microsoft.compute/virtualmachinescalesets" - Virtual Machine Scale Sets,  and "Microsoft.Web/serverfarms" - Web App</span></span> |
| <span data-ttu-id="4d6c8-185">resourceId</span><span class="sxs-lookup"><span data-stu-id="4d6c8-185">resourceId</span></span> |<span data-ttu-id="4d6c8-186">Yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-186">Yes</span></span> |<span data-ttu-id="4d6c8-187">Resource Manager ID of the target resource that is being scaled</span><span class="sxs-lookup"><span data-stu-id="4d6c8-187">Resource Manager ID of the target resource that is being scaled</span></span> |
| <span data-ttu-id="4d6c8-188">portalLink</span><span class="sxs-lookup"><span data-stu-id="4d6c8-188">portalLink</span></span> |<span data-ttu-id="4d6c8-189">Yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-189">Yes</span></span> |<span data-ttu-id="4d6c8-190">Azure portal link to the summary page of the target resource</span><span class="sxs-lookup"><span data-stu-id="4d6c8-190">Azure portal link to the summary page of the target resource</span></span> |
| <span data-ttu-id="4d6c8-191">oldCapacity</span><span class="sxs-lookup"><span data-stu-id="4d6c8-191">oldCapacity</span></span> |<span data-ttu-id="4d6c8-192">Yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-192">Yes</span></span> |<span data-ttu-id="4d6c8-193">The current (old) instance count when Autoscale took a scale action</span><span class="sxs-lookup"><span data-stu-id="4d6c8-193">The current (old) instance count when Autoscale took a scale action</span></span> |
| <span data-ttu-id="4d6c8-194">newCapacity</span><span class="sxs-lookup"><span data-stu-id="4d6c8-194">newCapacity</span></span> |<span data-ttu-id="4d6c8-195">Yes</span><span class="sxs-lookup"><span data-stu-id="4d6c8-195">Yes</span></span> |<span data-ttu-id="4d6c8-196">The new instance count that Autoscale scaled the resource to</span><span class="sxs-lookup"><span data-stu-id="4d6c8-196">The new instance count that Autoscale scaled the resource to</span></span> |
| <span data-ttu-id="4d6c8-197">Properties</span><span class="sxs-lookup"><span data-stu-id="4d6c8-197">Properties</span></span> |<span data-ttu-id="4d6c8-198">No</span><span class="sxs-lookup"><span data-stu-id="4d6c8-198">No</span></span> |<span data-ttu-id="4d6c8-199">Optional.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-199">Optional.</span></span> <span data-ttu-id="4d6c8-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span><span class="sxs-lookup"><span data-stu-id="4d6c8-200">Set of <Key, Value> pairs (for example,  Dictionary <String, String>).</span></span> <span data-ttu-id="4d6c8-201">The properties field is optional.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-201">The properties field is optional.</span></span> <span data-ttu-id="4d6c8-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span><span class="sxs-lookup"><span data-stu-id="4d6c8-202">In a custom user interface  or Logic app based workflow, you can enter keys and values that can be passed using the payload.</span></span> <span data-ttu-id="4d6c8-203">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span><span class="sxs-lookup"><span data-stu-id="4d6c8-203">An alternate way to pass custom properties back to the outgoing webhook call is to use the webhook URI itself (as query parameters)</span></span> |


