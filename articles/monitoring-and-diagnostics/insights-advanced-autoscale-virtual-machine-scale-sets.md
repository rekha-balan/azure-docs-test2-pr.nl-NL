---
title: Advanced Autoscale using Azure Virtual Machines | Microsoft Docs
description: Uses Resource Manager and VM Scale Sets with multiple rules and profiles which send email and call webhook URLs with scale actions.
author: kamathashwin
manager: carmonm
editor: ''
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 7e3576e2-4a2b-4736-b5ae-98c4689cdd2b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/22/2016
ms.author: ashwink
ms.openlocfilehash: 17ae2f666364b6c8dbd2121ea57958d771d7e8cd
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555321"
---
# <a name="advanced-autoscale-configuration-using-resource-manager-templates-for-vm-scale-sets"></a><span data-ttu-id="41bf5-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span><span class="sxs-lookup"><span data-stu-id="41bf5-103">Advanced autoscale configuration using Resource Manager templates for VM Scale Sets</span></span>
<span data-ttu-id="41bf5-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span><span class="sxs-lookup"><span data-stu-id="41bf5-104">You can scale-in and scale-out in Virtual Machine Scale Sets based on performance metric thresholds, by a recurring schedule, or by a particular date.</span></span> <span data-ttu-id="41bf5-105">You can also configure email and webhook notifications for scale actions.</span><span class="sxs-lookup"><span data-stu-id="41bf5-105">You can also configure email and webhook notifications for scale actions.</span></span> <span data-ttu-id="41bf5-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span><span class="sxs-lookup"><span data-stu-id="41bf5-106">This walkthrough shows an example of configuring all these objects using a Resource Manager template on a VM Scale Set.</span></span>

> [!NOTE]
> <span data-ttu-id="41bf5-107">While this walkthrough explains the steps for VM Scale Sets, the same information applies to autoscaling Cloud Services and Web Apps.</span><span class="sxs-lookup"><span data-stu-id="41bf5-107">While this walkthrough explains the steps for VM Scale Sets, the same information applies to autoscaling Cloud Services and Web Apps.</span></span>
> <span data-ttu-id="41bf5-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer to the [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span><span class="sxs-lookup"><span data-stu-id="41bf5-108">For a simple scale in/out setting on a VM Scale Set based on a simple performance metric such as CPU, refer to the [Linux](../virtual-machine-scale-sets/virtual-machine-scale-sets-linux-autoscale.md) and [Windows](../virtual-machine-scale-sets/virtual-machine-scale-sets-windows-autoscale.md) documents</span></span>
>
>

## <a name="walkthrough"></a><span data-ttu-id="41bf5-109">Walkthrough</span><span class="sxs-lookup"><span data-stu-id="41bf5-109">Walkthrough</span></span>
<span data-ttu-id="41bf5-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) to configure and update the autoscale setting for a scale set.</span><span class="sxs-lookup"><span data-stu-id="41bf5-110">In this walkthrough, we use [Azure Resource Explorer](https://resources.azure.com/) to configure and update the autoscale setting for a scale set.</span></span> <span data-ttu-id="41bf5-111">Azure Resource Explorer is an easy way to manage Azure resources via Resource Manager templates.</span><span class="sxs-lookup"><span data-stu-id="41bf5-111">Azure Resource Explorer is an easy way to manage Azure resources via Resource Manager templates.</span></span> <span data-ttu-id="41bf5-112">If you are new to Azure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span><span class="sxs-lookup"><span data-stu-id="41bf5-112">If you are new to Azure Resource Explorer tool, read [this introduction](https://azure.microsoft.com/blog/azure-resource-explorer-a-new-tool-to-discover-the-azure-api/).</span></span>

1. <span data-ttu-id="41bf5-113">Deploy a new scale set with a basic autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="41bf5-113">Deploy a new scale set with a basic autoscale setting.</span></span> <span data-ttu-id="41bf5-114">This article uses the one from the Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span><span class="sxs-lookup"><span data-stu-id="41bf5-114">This article uses the one from the Azure QuickStart Gallery, which has a Windows scale set with a basic autoscale template.</span></span> <span data-ttu-id="41bf5-115">Linux scale sets work the same way.</span><span class="sxs-lookup"><span data-stu-id="41bf5-115">Linux scale sets work the same way.</span></span>
2. <span data-ttu-id="41bf5-116">After the scale set is created, navigate to the scale set resource from Azure Resource Explorer.</span><span class="sxs-lookup"><span data-stu-id="41bf5-116">After the scale set is created, navigate to the scale set resource from Azure Resource Explorer.</span></span> <span data-ttu-id="41bf5-117">You see the following under Microsoft.Insights node.</span><span class="sxs-lookup"><span data-stu-id="41bf5-117">You see the following under Microsoft.Insights node.</span></span>

    ![Azure Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-advanced-autoscale-vmss/azure_explorer_navigate.png)

    <span data-ttu-id="41bf5-119">The template execution has created a default autoscale setting with the name **'autoscalewad'**.</span><span class="sxs-lookup"><span data-stu-id="41bf5-119">The template execution has created a default autoscale setting with the name **'autoscalewad'**.</span></span> <span data-ttu-id="41bf5-120">On the right-hand side, you can view the full definition of this autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="41bf5-120">On the right-hand side, you can view the full definition of this autoscale setting.</span></span> <span data-ttu-id="41bf5-121">In this case, the default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span><span class="sxs-lookup"><span data-stu-id="41bf5-121">In this case, the default autoscale setting comes with a CPU% based scale-out and scale-in rule.</span></span>  

3. <span data-ttu-id="41bf5-122">You can now add more profiles and rules based on the schedule or specific requirements.</span><span class="sxs-lookup"><span data-stu-id="41bf5-122">You can now add more profiles and rules based on the schedule or specific requirements.</span></span> <span data-ttu-id="41bf5-123">We create an autoscale setting with three profiles.</span><span class="sxs-lookup"><span data-stu-id="41bf5-123">We create an autoscale setting with three profiles.</span></span> <span data-ttu-id="41bf5-124">To understand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="41bf5-124">To understand profiles and rules in autoscale, review [Autoscale Best Practices](insights-autoscale-best-practices.md).</span></span>  

    | <span data-ttu-id="41bf5-125">Profiles & Rules</span><span class="sxs-lookup"><span data-stu-id="41bf5-125">Profiles & Rules</span></span> | <span data-ttu-id="41bf5-126">Description</span><span class="sxs-lookup"><span data-stu-id="41bf5-126">Description</span></span> |
    |--- | --- |
    | <span data-ttu-id="41bf5-127">**Profile**</span><span class="sxs-lookup"><span data-stu-id="41bf5-127">**Profile**</span></span> |<span data-ttu-id="41bf5-128">**Performance/metric based**</span><span class="sxs-lookup"><span data-stu-id="41bf5-128">**Performance/metric based**</span></span> |
    | <span data-ttu-id="41bf5-129">Rule</span><span class="sxs-lookup"><span data-stu-id="41bf5-129">Rule</span></span> |<span data-ttu-id="41bf5-130">Service Bus Queue Message Count > x</span><span class="sxs-lookup"><span data-stu-id="41bf5-130">Service Bus Queue Message Count > x</span></span> |
    | <span data-ttu-id="41bf5-131">Rule</span><span class="sxs-lookup"><span data-stu-id="41bf5-131">Rule</span></span> |<span data-ttu-id="41bf5-132">Service Bus Queue Message Count < y</span><span class="sxs-lookup"><span data-stu-id="41bf5-132">Service Bus Queue Message Count < y</span></span> |
    | <span data-ttu-id="41bf5-133">Rule</span><span class="sxs-lookup"><span data-stu-id="41bf5-133">Rule</span></span> |<span data-ttu-id="41bf5-134">CPU% > n</span><span class="sxs-lookup"><span data-stu-id="41bf5-134">CPU% > n</span></span> |
    | <span data-ttu-id="41bf5-135">Rule</span><span class="sxs-lookup"><span data-stu-id="41bf5-135">Rule</span></span> |<span data-ttu-id="41bf5-136">CPU% < p</span><span class="sxs-lookup"><span data-stu-id="41bf5-136">CPU% < p</span></span> |
    | <span data-ttu-id="41bf5-137">**Profile**</span><span class="sxs-lookup"><span data-stu-id="41bf5-137">**Profile**</span></span> |<span data-ttu-id="41bf5-138">**Weekday morning hours (no rules)**</span><span class="sxs-lookup"><span data-stu-id="41bf5-138">**Weekday morning hours (no rules)**</span></span> |
    | <span data-ttu-id="41bf5-139">**Profile**</span><span class="sxs-lookup"><span data-stu-id="41bf5-139">**Profile**</span></span> |<span data-ttu-id="41bf5-140">**Product Launch day (no rules)**</span><span class="sxs-lookup"><span data-stu-id="41bf5-140">**Product Launch day (no rules)**</span></span> |

4. <span data-ttu-id="41bf5-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span><span class="sxs-lookup"><span data-stu-id="41bf5-141">Here is a hypothetical scaling scenario that we use for this walk-through.</span></span>

    * <span data-ttu-id="41bf5-142">**Load based** - I'd like to scale out or in based on the load on my application hosted on my scale set.\*</span><span class="sxs-lookup"><span data-stu-id="41bf5-142">**Load based** - I'd like to scale out or in based on the load on my application hosted on my scale set.\*</span></span>
    * <span data-ttu-id="41bf5-143">**Message Queue size** - I use a Service Bus Queue for the incoming messages to my application.</span><span class="sxs-lookup"><span data-stu-id="41bf5-143">**Message Queue size** - I use a Service Bus Queue for the incoming messages to my application.</span></span> <span data-ttu-id="41bf5-144">I use the queue's message count and CPU% and configure a default profile to trigger a scale action if either of message count or CPU hits the threshold.\*</span><span class="sxs-lookup"><span data-stu-id="41bf5-144">I use the queue's message count and CPU% and configure a default profile to trigger a scale action if either of message count or CPU hits the threshold.\*</span></span>
    * <span data-ttu-id="41bf5-145">**Time of week and day** - I want a weekly recurring 'time of the day' based profile called 'Weekday Morning Hours'.</span><span class="sxs-lookup"><span data-stu-id="41bf5-145">**Time of week and day** - I want a weekly recurring 'time of the day' based profile called 'Weekday Morning Hours'.</span></span> <span data-ttu-id="41bf5-146">Based on historical data, I know it is better to have certain number of VM instances to handle my application's load during this time.\*</span><span class="sxs-lookup"><span data-stu-id="41bf5-146">Based on historical data, I know it is better to have certain number of VM instances to handle my application's load during this time.\*</span></span>
    * <span data-ttu-id="41bf5-147">**Special Dates** - I added a 'Product Launch Day' profile.</span><span class="sxs-lookup"><span data-stu-id="41bf5-147">**Special Dates** - I added a 'Product Launch Day' profile.</span></span> <span data-ttu-id="41bf5-148">I plan ahead for specific dates so my application is ready to handle the load due marketing announcements and when we put a new product in the application.\*</span><span class="sxs-lookup"><span data-stu-id="41bf5-148">I plan ahead for specific dates so my application is ready to handle the load due marketing announcements and when we put a new product in the application.\*</span></span>
    * <span data-ttu-id="41bf5-149">*The last two profiles can also have other performance metric based rules within them. In this case, I decided not to have one and instead to rely on the default performance metric based rules. Rules are optional for the recurring and date-based profiles.*</span><span class="sxs-lookup"><span data-stu-id="41bf5-149">*The last two profiles can also have other performance metric based rules within them. In this case, I decided not to have one and instead to rely on the default performance metric based rules. Rules are optional for the recurring and date-based profiles.*</span></span>

    <span data-ttu-id="41bf5-150">Autoscale engine's prioritization of the profiles and rules is also captured in the [autoscaling best practices](insights-autoscale-best-practices.md) article.</span><span class="sxs-lookup"><span data-stu-id="41bf5-150">Autoscale engine's prioritization of the profiles and rules is also captured in the [autoscaling best practices](insights-autoscale-best-practices.md) article.</span></span>
    <span data-ttu-id="41bf5-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span><span class="sxs-lookup"><span data-stu-id="41bf5-151">For a list of common metrics for autoscale, refer [Common metrics for Autoscale](insights-autoscale-common-metrics.md)</span></span>

5. <span data-ttu-id="41bf5-152">Make sure you are on the **Read/Write** mode in Resource Explorer</span><span class="sxs-lookup"><span data-stu-id="41bf5-152">Make sure you are on the **Read/Write** mode in Resource Explorer</span></span>

    ![Autoscalewad, default autoscale setting](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-advanced-autoscale-vmss/autoscalewad.png)

6. <span data-ttu-id="41bf5-154">Click Edit.</span><span class="sxs-lookup"><span data-stu-id="41bf5-154">Click Edit.</span></span> <span data-ttu-id="41bf5-155">**Replace** the 'profiles' element in autoscale setting with the following configuration:</span><span class="sxs-lookup"><span data-stu-id="41bf5-155">**Replace** the 'profiles' element in autoscale setting with the following configuration:</span></span>

    ![profiles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/monitoring-and-diagnostics/media/insights-advanced-autoscale-vmss/profiles.png)

    ```
    {
            "name": "Perf_Based_Scale",
            "capacity": {
              "minimum": "2",
              "maximum": "12",
              "default": "2"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 10
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "MessageCount",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 3
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 85
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              },
              {
                "metricTrigger": {
                  "metricName": "Percentage CPU",
                  "metricNamespace": "",
                  "metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.Compute/virtualMachineScaleSets/<this_vmss_name>",
                  "timeGrain": "PT5M",
                  "statistic": "Average",
                  "timeWindow": "PT30M",
                  "timeAggregation": "Average",
                  "operator": "LessThan",
                  "threshold": 60
                },
                "scaleAction": {
                  "direction": "Decrease",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          },
          {
            "name": "Weekday_Morning_Hours_Scale",
            "capacity": {
              "minimum": "4",
              "maximum": "12",
              "default": "4"
            },
            "rules": [],
            "recurrence": {
              "frequency": "Week",
              "schedule": {
                "timeZone": "Pacific Standard Time",
                "days": [
                  "Monday",
                  "Tuesday",
                  "Wednesday",
                  "Thursday",
                  "Friday"
                ],
                "hours": [
                  6
                ],
                "minutes": [
                  0
                ]
              }
            }
          },
          {
            "name": "Product_Launch_Day",
            "capacity": {
              "minimum": "6",
              "maximum": "20",
              "default": "6"
            },
            "rules": [],
            "fixedDate": {
              "timeZone": "Pacific Standard Time",
              "start": "2016-06-20T00:06:00Z",
              "end": "2016-06-21T23:59:00Z"
            }
          }
    ```
    <span data-ttu-id="41bf5-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span><span class="sxs-lookup"><span data-stu-id="41bf5-157">For supported fields and their values, see [Autoscale REST API documentation](https://msdn.microsoft.com/en-us/library/azure/dn931928.aspx).</span></span> <span data-ttu-id="41bf5-158">Now your autoscale setting contains the three profiles explained previously.</span><span class="sxs-lookup"><span data-stu-id="41bf5-158">Now your autoscale setting contains the three profiles explained previously.</span></span>

7. <span data-ttu-id="41bf5-159">Finally, look at the Autoscale **notification** section.</span><span class="sxs-lookup"><span data-stu-id="41bf5-159">Finally, look at the Autoscale **notification** section.</span></span> <span data-ttu-id="41bf5-160">Autoscale notifications allow you to do three things when a scale-out or in action is successfully triggered.</span><span class="sxs-lookup"><span data-stu-id="41bf5-160">Autoscale notifications allow you to do three things when a scale-out or in action is successfully triggered.</span></span>
   - <span data-ttu-id="41bf5-161">Notify the admin and co-admins of your subscription</span><span class="sxs-lookup"><span data-stu-id="41bf5-161">Notify the admin and co-admins of your subscription</span></span>
   - <span data-ttu-id="41bf5-162">Email a set of users</span><span class="sxs-lookup"><span data-stu-id="41bf5-162">Email a set of users</span></span>
   - <span data-ttu-id="41bf5-163">Trigger a webhook call.</span><span class="sxs-lookup"><span data-stu-id="41bf5-163">Trigger a webhook call.</span></span> <span data-ttu-id="41bf5-164">When fired, this webhook sends metadata about the autoscaling condition and the scale set resource.</span><span class="sxs-lookup"><span data-stu-id="41bf5-164">When fired, this webhook sends metadata about the autoscaling condition and the scale set resource.</span></span> <span data-ttu-id="41bf5-165">To learn more about the payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span><span class="sxs-lookup"><span data-stu-id="41bf5-165">To learn more about the payload of autoscale webhook, see [Configure Webhook & Email Notifications for Autoscale](insights-autoscale-to-webhook-email.md).</span></span>

   <span data-ttu-id="41bf5-166">Add the following to the Autoscale setting replacing your **notification** element whose value is null</span><span class="sxs-lookup"><span data-stu-id="41bf5-166">Add the following to the Autoscale setting replacing your **notification** element whose value is null</span></span>

   ```
   "notifications": [
      {
        "operation": "Scale",
        "email": {
          "sendToSubscriptionAdministrator": true,
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

   <span data-ttu-id="41bf5-167">Hit **Put** button in Resource Explorer to update the autoscale setting.</span><span class="sxs-lookup"><span data-stu-id="41bf5-167">Hit **Put** button in Resource Explorer to update the autoscale setting.</span></span>

<span data-ttu-id="41bf5-168">You have updated an autoscale setting on a VM Scale set to include multiple scale profiles and scale notifications.</span><span class="sxs-lookup"><span data-stu-id="41bf5-168">You have updated an autoscale setting on a VM Scale set to include multiple scale profiles and scale notifications.</span></span>

## <a name="next-steps"></a><span data-ttu-id="41bf5-169">Next Steps</span><span class="sxs-lookup"><span data-stu-id="41bf5-169">Next Steps</span></span>
<span data-ttu-id="41bf5-170">Use these links to learn more about autoscaling.</span><span class="sxs-lookup"><span data-stu-id="41bf5-170">Use these links to learn more about autoscaling.</span></span>

[<span data-ttu-id="41bf5-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="41bf5-171">TroubleShoot Autoscale with Virtual Machine Scale Sets</span></span>](../virtual-machine-scale-sets/virtual-machine-scale-sets-troubleshoot.md)

[<span data-ttu-id="41bf5-172">Common Metrics for Autoscale</span><span class="sxs-lookup"><span data-stu-id="41bf5-172">Common Metrics for Autoscale</span></span>](insights-autoscale-common-metrics.md)

[<span data-ttu-id="41bf5-173">Best Practices for Azure Autoscale</span><span class="sxs-lookup"><span data-stu-id="41bf5-173">Best Practices for Azure Autoscale</span></span>](insights-autoscale-best-practices.md)

[<span data-ttu-id="41bf5-174">Manage Autoscale using PowerShell</span><span class="sxs-lookup"><span data-stu-id="41bf5-174">Manage Autoscale using PowerShell</span></span>](insights-powershell-samples.md#create-and-manage-autoscale-settings)

[<span data-ttu-id="41bf5-175">Manage Autoscale using CLI</span><span class="sxs-lookup"><span data-stu-id="41bf5-175">Manage Autoscale using CLI</span></span>](insights-cli-samples.md#autoscale)

[<span data-ttu-id="41bf5-176">Configure Webhook & Email Notifications for Autoscale</span><span class="sxs-lookup"><span data-stu-id="41bf5-176">Configure Webhook & Email Notifications for Autoscale</span></span>](insights-autoscale-to-webhook-email.md)



