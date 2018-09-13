---
title: Move Azure resources to new subscription or resource group | Microsoft Docs
description: Use Azure Resource Manager to move resources to a new resource group or subscription.
services: azure-resource-manager
documentationcenter: ''
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: ab7d42bd-8434-4026-a892-df4a97b60a9b
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/10/2017
ms.author: tomfitz
ms.openlocfilehash: 30562988624b55aa817f2cd951d9c7461ad77510
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661270"
---
# <a name="move-resources-to-new-resource-group-or-subscription"></a><span data-ttu-id="b5727-103">Move resources to new resource group or subscription</span><span class="sxs-lookup"><span data-stu-id="b5727-103">Move resources to new resource group or subscription</span></span>
<span data-ttu-id="b5727-104">This topic shows you how to move resources to either a new subscription or a new resource group in the same subscription.</span><span class="sxs-lookup"><span data-stu-id="b5727-104">This topic shows you how to move resources to either a new subscription or a new resource group in the same subscription.</span></span> <span data-ttu-id="b5727-105">You can use the portal, PowerShell, Azure CLI, or the REST API to move resource.</span><span class="sxs-lookup"><span data-stu-id="b5727-105">You can use the portal, PowerShell, Azure CLI, or the REST API to move resource.</span></span> <span data-ttu-id="b5727-106">The move operations in this topic are available to you without any assistance from Azure support.</span><span class="sxs-lookup"><span data-stu-id="b5727-106">The move operations in this topic are available to you without any assistance from Azure support.</span></span>

<span data-ttu-id="b5727-107">When moving resources, both the source group and the target group are locked during the operation.</span><span class="sxs-lookup"><span data-stu-id="b5727-107">When moving resources, both the source group and the target group are locked during the operation.</span></span> <span data-ttu-id="b5727-108">Write and delete operations are blocked on the resource groups until the move completes.</span><span class="sxs-lookup"><span data-stu-id="b5727-108">Write and delete operations are blocked on the resource groups until the move completes.</span></span> <span data-ttu-id="b5727-109">This lock means you cannot add, update, or delete resources in the resource groups, but it does not mean the resources are frozen.</span><span class="sxs-lookup"><span data-stu-id="b5727-109">This lock means you cannot add, update, or delete resources in the resource groups, but it does not mean the resources are frozen.</span></span> <span data-ttu-id="b5727-110">For example, if you move a SQL Server and its database to a new resource group, an application that uses the database experiences no downtime.</span><span class="sxs-lookup"><span data-stu-id="b5727-110">For example, if you move a SQL Server and its database to a new resource group, an application that uses the database experiences no downtime.</span></span> <span data-ttu-id="b5727-111">It can still read and write to the database.</span><span class="sxs-lookup"><span data-stu-id="b5727-111">It can still read and write to the database.</span></span> 

<span data-ttu-id="b5727-112">You cannot change the location of the resource.</span><span class="sxs-lookup"><span data-stu-id="b5727-112">You cannot change the location of the resource.</span></span> <span data-ttu-id="b5727-113">Moving a resource only moves it to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="b5727-113">Moving a resource only moves it to a new resource group.</span></span> <span data-ttu-id="b5727-114">The new resource group may have a different location, but that does not change the location of the resource.</span><span class="sxs-lookup"><span data-stu-id="b5727-114">The new resource group may have a different location, but that does not change the location of the resource.</span></span>

> [!NOTE]
> <span data-ttu-id="b5727-115">This article describes how to move resources within an existing Azure account offering.</span><span class="sxs-lookup"><span data-stu-id="b5727-115">This article describes how to move resources within an existing Azure account offering.</span></span> <span data-ttu-id="b5727-116">If you actually want to change your Azure account offering (such as upgrading from pay-as-you-go to pre-pay) while continuing to work with your existing resources, see [Switch your Azure subscription to another offer](../billing/billing-how-to-switch-azure-offer.md).</span><span class="sxs-lookup"><span data-stu-id="b5727-116">If you actually want to change your Azure account offering (such as upgrading from pay-as-you-go to pre-pay) while continuing to work with your existing resources, see [Switch your Azure subscription to another offer](../billing/billing-how-to-switch-azure-offer.md).</span></span> 
> 
> 

## <a name="checklist-before-moving-resources"></a><span data-ttu-id="b5727-117">Checklist before moving resources</span><span class="sxs-lookup"><span data-stu-id="b5727-117">Checklist before moving resources</span></span>
<span data-ttu-id="b5727-118">There are some important steps to perform before moving a resource.</span><span class="sxs-lookup"><span data-stu-id="b5727-118">There are some important steps to perform before moving a resource.</span></span> <span data-ttu-id="b5727-119">By verifying these conditions, you can avoid errors.</span><span class="sxs-lookup"><span data-stu-id="b5727-119">By verifying these conditions, you can avoid errors.</span></span>

1. <span data-ttu-id="b5727-120">The source and destination subscriptions must exist within the same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span><span class="sxs-lookup"><span data-stu-id="b5727-120">The source and destination subscriptions must exist within the same [Azure Active Directory tenant](../active-directory/active-directory-howto-tenant.md).</span></span> <span data-ttu-id="b5727-121">To check that both subscriptions have the same tenant ID, use Azure PowerShell or Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b5727-121">To check that both subscriptions have the same tenant ID, use Azure PowerShell or Azure CLI.</span></span>

  <span data-ttu-id="b5727-122">For Azure PowerShell, use:</span><span class="sxs-lookup"><span data-stu-id="b5727-122">For Azure PowerShell, use:</span></span>

  ```powershell
  (Get-AzureRmSubscription -SubscriptionName "Example Subscription").TenantId
  ```

  <span data-ttu-id="b5727-123">For Azure CLI 2.0, use:</span><span class="sxs-lookup"><span data-stu-id="b5727-123">For Azure CLI 2.0, use:</span></span>

  ```azurecli
  az account show --subscription "Example Subscription" --query tenantId
  ```

  <span data-ttu-id="b5727-124">If the tenant IDs for the source and destination subscriptions are not the same, you can attempt to change the directory for the subscription.</span><span class="sxs-lookup"><span data-stu-id="b5727-124">If the tenant IDs for the source and destination subscriptions are not the same, you can attempt to change the directory for the subscription.</span></span> <span data-ttu-id="b5727-125">However, this option is only available to Service Administrators who are signed in with a Microsoft account (not an organizational account).</span><span class="sxs-lookup"><span data-stu-id="b5727-125">However, this option is only available to Service Administrators who are signed in with a Microsoft account (not an organizational account).</span></span> <span data-ttu-id="b5727-126">To attempt changing the directory, log in to the [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select the subscription.</span><span class="sxs-lookup"><span data-stu-id="b5727-126">To attempt changing the directory, log in to the [classic portal](https://manage.windowsazure.com/), and select **Settings**, and select the subscription.</span></span> <span data-ttu-id="b5727-127">If the **Edit Directory** icon is available, select it to change the associated Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b5727-127">If the **Edit Directory** icon is available, select it to change the associated Azure Active Directory.</span></span> 

  ![edit directory](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-move-resources/edit-directory.png) 

  <span data-ttu-id="b5727-129">If that icon is not available, you must contact support to move the resources to a new tenant.</span><span class="sxs-lookup"><span data-stu-id="b5727-129">If that icon is not available, you must contact support to move the resources to a new tenant.</span></span>

2. <span data-ttu-id="b5727-130">The service must enable the ability to move resources.</span><span class="sxs-lookup"><span data-stu-id="b5727-130">The service must enable the ability to move resources.</span></span> <span data-ttu-id="b5727-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span><span class="sxs-lookup"><span data-stu-id="b5727-131">This topic lists which services enable moving resources and which services do not enable moving resources.</span></span>
3. <span data-ttu-id="b5727-132">The destination subscription must be registered for the resource provider of the resource being moved.</span><span class="sxs-lookup"><span data-stu-id="b5727-132">The destination subscription must be registered for the resource provider of the resource being moved.</span></span> <span data-ttu-id="b5727-133">If not, you receive an error stating that the **subscription is not registered for a resource type**.</span><span class="sxs-lookup"><span data-stu-id="b5727-133">If not, you receive an error stating that the **subscription is not registered for a resource type**.</span></span> <span data-ttu-id="b5727-134">You might encounter this problem when moving a resource to a new subscription, but that subscription has never been used with that resource type.</span><span class="sxs-lookup"><span data-stu-id="b5727-134">You might encounter this problem when moving a resource to a new subscription, but that subscription has never been used with that resource type.</span></span> <span data-ttu-id="b5727-135">To learn how to check the registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md#resource-providers-and-types).</span><span class="sxs-lookup"><span data-stu-id="b5727-135">To learn how to check the registration status and register resource providers, see [Resource providers and types](resource-manager-supported-services.md#resource-providers-and-types).</span></span>

## <a name="when-to-call-support"></a><span data-ttu-id="b5727-136">When to call support</span><span class="sxs-lookup"><span data-stu-id="b5727-136">When to call support</span></span>
<span data-ttu-id="b5727-137">You can move most resources through the self-service operations shown in this topic.</span><span class="sxs-lookup"><span data-stu-id="b5727-137">You can move most resources through the self-service operations shown in this topic.</span></span> <span data-ttu-id="b5727-138">Use the self-service operations to:</span><span class="sxs-lookup"><span data-stu-id="b5727-138">Use the self-service operations to:</span></span>

* <span data-ttu-id="b5727-139">Move Resource Manager resources.</span><span class="sxs-lookup"><span data-stu-id="b5727-139">Move Resource Manager resources.</span></span>
* <span data-ttu-id="b5727-140">Move classic resources according to the [classic deployment limitations](#classic-deployment-limitations).</span><span class="sxs-lookup"><span data-stu-id="b5727-140">Move classic resources according to the [classic deployment limitations](#classic-deployment-limitations).</span></span> 

<span data-ttu-id="b5727-141">Call support when you need to:</span><span class="sxs-lookup"><span data-stu-id="b5727-141">Call support when you need to:</span></span>

* <span data-ttu-id="b5727-142">Move your resources to a new Azure account (and Azure Active Directory tenant).</span><span class="sxs-lookup"><span data-stu-id="b5727-142">Move your resources to a new Azure account (and Azure Active Directory tenant).</span></span>
* <span data-ttu-id="b5727-143">Move classic resources but are having trouble with the limitations.</span><span class="sxs-lookup"><span data-stu-id="b5727-143">Move classic resources but are having trouble with the limitations.</span></span>

## <a name="services-that-enable-move"></a><span data-ttu-id="b5727-144">Services that enable move</span><span class="sxs-lookup"><span data-stu-id="b5727-144">Services that enable move</span></span>
<span data-ttu-id="b5727-145">For now, the services that enable moving to both a new resource group and subscription are:</span><span class="sxs-lookup"><span data-stu-id="b5727-145">For now, the services that enable moving to both a new resource group and subscription are:</span></span>

* <span data-ttu-id="b5727-146">API Management</span><span class="sxs-lookup"><span data-stu-id="b5727-146">API Management</span></span>
* <span data-ttu-id="b5727-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span><span class="sxs-lookup"><span data-stu-id="b5727-147">App Service apps (web apps) - see [App Service limitations](#app-service-limitations)</span></span>
* <span data-ttu-id="b5727-148">Automation</span><span class="sxs-lookup"><span data-stu-id="b5727-148">Automation</span></span>
* <span data-ttu-id="b5727-149">Batch</span><span class="sxs-lookup"><span data-stu-id="b5727-149">Batch</span></span>
* <span data-ttu-id="b5727-150">Bing Maps</span><span class="sxs-lookup"><span data-stu-id="b5727-150">Bing Maps</span></span>
* <span data-ttu-id="b5727-151">CDN</span><span class="sxs-lookup"><span data-stu-id="b5727-151">CDN</span></span>
* <span data-ttu-id="b5727-152">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="b5727-152">Cloud Services - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="b5727-153">Cognitive Services</span><span class="sxs-lookup"><span data-stu-id="b5727-153">Cognitive Services</span></span>
* <span data-ttu-id="b5727-154">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="b5727-154">Content Moderator</span></span>
* <span data-ttu-id="b5727-155">Data Catalog</span><span class="sxs-lookup"><span data-stu-id="b5727-155">Data Catalog</span></span>
* <span data-ttu-id="b5727-156">Data Factory</span><span class="sxs-lookup"><span data-stu-id="b5727-156">Data Factory</span></span>
* <span data-ttu-id="b5727-157">Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="b5727-157">Data Lake Analytics</span></span>
* <span data-ttu-id="b5727-158">Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="b5727-158">Data Lake Store</span></span>
* <span data-ttu-id="b5727-159">DNS</span><span class="sxs-lookup"><span data-stu-id="b5727-159">DNS</span></span>
* <span data-ttu-id="b5727-160">DocumentDB</span><span class="sxs-lookup"><span data-stu-id="b5727-160">DocumentDB</span></span>
* <span data-ttu-id="b5727-161">Event Hubs</span><span class="sxs-lookup"><span data-stu-id="b5727-161">Event Hubs</span></span>
* <span data-ttu-id="b5727-162">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span><span class="sxs-lookup"><span data-stu-id="b5727-162">HDInsight clusters - see [HDInsight limitations](#hdinsight-limitations)</span></span>
* <span data-ttu-id="b5727-163">IoT Hubs</span><span class="sxs-lookup"><span data-stu-id="b5727-163">IoT Hubs</span></span>
* <span data-ttu-id="b5727-164">Key Vault</span><span class="sxs-lookup"><span data-stu-id="b5727-164">Key Vault</span></span> 
* <span data-ttu-id="b5727-165">Load Balancers</span><span class="sxs-lookup"><span data-stu-id="b5727-165">Load Balancers</span></span>
* <span data-ttu-id="b5727-166">Logic Apps</span><span class="sxs-lookup"><span data-stu-id="b5727-166">Logic Apps</span></span>
* <span data-ttu-id="b5727-167">Machine Learning</span><span class="sxs-lookup"><span data-stu-id="b5727-167">Machine Learning</span></span>
* <span data-ttu-id="b5727-168">Media Services</span><span class="sxs-lookup"><span data-stu-id="b5727-168">Media Services</span></span>
* <span data-ttu-id="b5727-169">Mobile Engagement</span><span class="sxs-lookup"><span data-stu-id="b5727-169">Mobile Engagement</span></span>
* <span data-ttu-id="b5727-170">Notification Hubs</span><span class="sxs-lookup"><span data-stu-id="b5727-170">Notification Hubs</span></span>
* <span data-ttu-id="b5727-171">Operational Insights</span><span class="sxs-lookup"><span data-stu-id="b5727-171">Operational Insights</span></span>
* <span data-ttu-id="b5727-172">Operations Management</span><span class="sxs-lookup"><span data-stu-id="b5727-172">Operations Management</span></span>
* <span data-ttu-id="b5727-173">Power BI</span><span class="sxs-lookup"><span data-stu-id="b5727-173">Power BI</span></span>
* <span data-ttu-id="b5727-174">Redis Cache</span><span class="sxs-lookup"><span data-stu-id="b5727-174">Redis Cache</span></span>
* <span data-ttu-id="b5727-175">Scheduler</span><span class="sxs-lookup"><span data-stu-id="b5727-175">Scheduler</span></span>
* <span data-ttu-id="b5727-176">Search</span><span class="sxs-lookup"><span data-stu-id="b5727-176">Search</span></span>
* <span data-ttu-id="b5727-177">Server Management</span><span class="sxs-lookup"><span data-stu-id="b5727-177">Server Management</span></span>
* <span data-ttu-id="b5727-178">Service Bus</span><span class="sxs-lookup"><span data-stu-id="b5727-178">Service Bus</span></span>
* <span data-ttu-id="b5727-179">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b5727-179">Service Fabric</span></span>
* <span data-ttu-id="b5727-180">Storage</span><span class="sxs-lookup"><span data-stu-id="b5727-180">Storage</span></span>
* <span data-ttu-id="b5727-181">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="b5727-181">Storage (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="b5727-182">Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="b5727-182">Stream Analytics</span></span>
* <span data-ttu-id="b5727-183">SQL Database server - The database and server must reside in the same resource group.</span><span class="sxs-lookup"><span data-stu-id="b5727-183">SQL Database server - The database and server must reside in the same resource group.</span></span> <span data-ttu-id="b5727-184">When you move a SQL server, all its databases are also moved.</span><span class="sxs-lookup"><span data-stu-id="b5727-184">When you move a SQL server, all its databases are also moved.</span></span>
* <span data-ttu-id="b5727-185">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="b5727-185">Traffic Manager</span></span>
* <span data-ttu-id="b5727-186">Virtual Machines - Does not support move to a new subscription when its certificates are stored in a Key Vault</span><span class="sxs-lookup"><span data-stu-id="b5727-186">Virtual Machines - Does not support move to a new subscription when its certificates are stored in a Key Vault</span></span>
* <span data-ttu-id="b5727-187">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="b5727-187">Virtual Machines (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="b5727-188">Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="b5727-188">Virtual Machine Scale Sets</span></span>
* <span data-ttu-id="b5727-189">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span><span class="sxs-lookup"><span data-stu-id="b5727-189">Virtual Networks - Currently, a peered Virtual Network cannot be moved until VNet peering has been disabled.</span></span> <span data-ttu-id="b5727-190">Once disabled, the Virtual Network can be moved successfully and the VNet peering can be enabled.</span><span class="sxs-lookup"><span data-stu-id="b5727-190">Once disabled, the Virtual Network can be moved successfully and the VNet peering can be enabled.</span></span>
* <span data-ttu-id="b5727-191">VPN Gateway</span><span class="sxs-lookup"><span data-stu-id="b5727-191">VPN Gateway</span></span> 

 
## <a name="services-that-do-not-enable-move"></a><span data-ttu-id="b5727-192">Services that do not enable move</span><span class="sxs-lookup"><span data-stu-id="b5727-192">Services that do not enable move</span></span>
<span data-ttu-id="b5727-193">The services that currently do not enable moving a resource are:</span><span class="sxs-lookup"><span data-stu-id="b5727-193">The services that currently do not enable moving a resource are:</span></span>

* <span data-ttu-id="b5727-194">AD Hybrid Health Service</span><span class="sxs-lookup"><span data-stu-id="b5727-194">AD Hybrid Health Service</span></span>
* <span data-ttu-id="b5727-195">Application Gateway</span><span class="sxs-lookup"><span data-stu-id="b5727-195">Application Gateway</span></span>
* <span data-ttu-id="b5727-196">Application Insights</span><span class="sxs-lookup"><span data-stu-id="b5727-196">Application Insights</span></span>
* <span data-ttu-id="b5727-197">BizTalk Services</span><span class="sxs-lookup"><span data-stu-id="b5727-197">BizTalk Services</span></span>
* <span data-ttu-id="b5727-198">Container Service</span><span class="sxs-lookup"><span data-stu-id="b5727-198">Container Service</span></span>
* <span data-ttu-id="b5727-199">Express Route</span><span class="sxs-lookup"><span data-stu-id="b5727-199">Express Route</span></span>
* <span data-ttu-id="b5727-200">DevTest Labs - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span><span class="sxs-lookup"><span data-stu-id="b5727-200">DevTest Labs - Move to new resource group in same subscription is enabled, but cross subscription move is not enabled.</span></span>
* <span data-ttu-id="b5727-201">Dynamics LCS</span><span class="sxs-lookup"><span data-stu-id="b5727-201">Dynamics LCS</span></span>
* <span data-ttu-id="b5727-202">Recovery Services vault - also do not move the Compute, Network, and Storage resources associated with the Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span><span class="sxs-lookup"><span data-stu-id="b5727-202">Recovery Services vault - also do not move the Compute, Network, and Storage resources associated with the Recovery Services vault, see [Recovery Services limitations](#recovery-services-limitations).</span></span>
* <span data-ttu-id="b5727-203">Security</span><span class="sxs-lookup"><span data-stu-id="b5727-203">Security</span></span>
* <span data-ttu-id="b5727-204">Virtual Machines with certificate stored in Key Vault</span><span class="sxs-lookup"><span data-stu-id="b5727-204">Virtual Machines with certificate stored in Key Vault</span></span>
* <span data-ttu-id="b5727-205">Virtual Machines with Managed Disks</span><span class="sxs-lookup"><span data-stu-id="b5727-205">Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="b5727-206">Availability sets with Virtual Machines with Managed Disks</span><span class="sxs-lookup"><span data-stu-id="b5727-206">Availability sets with Virtual Machines with Managed Disks</span></span>
* <span data-ttu-id="b5727-207">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="b5727-207">Managed Disks</span></span>
* <span data-ttu-id="b5727-208">Images created from Managed Disks</span><span class="sxs-lookup"><span data-stu-id="b5727-208">Images created from Managed Disks</span></span>
* <span data-ttu-id="b5727-209">Snapshots created from Managed Disks</span><span class="sxs-lookup"><span data-stu-id="b5727-209">Snapshots created from Managed Disks</span></span>
* <span data-ttu-id="b5727-210">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span><span class="sxs-lookup"><span data-stu-id="b5727-210">Virtual Networks (classic) - see [Classic deployment limitations](#classic-deployment-limitations)</span></span>
* <span data-ttu-id="b5727-211">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span><span class="sxs-lookup"><span data-stu-id="b5727-211">Virtual Machines created from Marketplace resources - cannot be moved across subscriptions.</span></span> <span data-ttu-id="b5727-212">Resource needs to be deprovisioned in the current subscription and deployed again in the new subscription</span><span class="sxs-lookup"><span data-stu-id="b5727-212">Resource needs to be deprovisioned in the current subscription and deployed again in the new subscription</span></span>

## <a name="app-service-limitations"></a><span data-ttu-id="b5727-213">App Service limitations</span><span class="sxs-lookup"><span data-stu-id="b5727-213">App Service limitations</span></span>
<span data-ttu-id="b5727-214">When working with App Service apps, you cannot move only an App Service plan.</span><span class="sxs-lookup"><span data-stu-id="b5727-214">When working with App Service apps, you cannot move only an App Service plan.</span></span> <span data-ttu-id="b5727-215">To move App Service apps, your options are:</span><span class="sxs-lookup"><span data-stu-id="b5727-215">To move App Service apps, your options are:</span></span>

* <span data-ttu-id="b5727-216">Move the App Service plan and all other App Service resources in that resource group to a new resource group that does not already have App Service resources.</span><span class="sxs-lookup"><span data-stu-id="b5727-216">Move the App Service plan and all other App Service resources in that resource group to a new resource group that does not already have App Service resources.</span></span> <span data-ttu-id="b5727-217">This requirement means you must move even the App Service resources that are not associated with the App Service plan.</span><span class="sxs-lookup"><span data-stu-id="b5727-217">This requirement means you must move even the App Service resources that are not associated with the App Service plan.</span></span> 
* <span data-ttu-id="b5727-218">Move the apps to a different resource group, but keep all App Service plans in the original resource group.</span><span class="sxs-lookup"><span data-stu-id="b5727-218">Move the apps to a different resource group, but keep all App Service plans in the original resource group.</span></span>

<span data-ttu-id="b5727-219">If your original resource group also includes an Application Insights resource, you cannot move that resource because Application Insights does not currently enable the move operation.</span><span class="sxs-lookup"><span data-stu-id="b5727-219">If your original resource group also includes an Application Insights resource, you cannot move that resource because Application Insights does not currently enable the move operation.</span></span> <span data-ttu-id="b5727-220">If you include the Application Insights resource when moving App Service apps, the entire move operation fails.</span><span class="sxs-lookup"><span data-stu-id="b5727-220">If you include the Application Insights resource when moving App Service apps, the entire move operation fails.</span></span> <span data-ttu-id="b5727-221">However, the Application Insights and App Service plan do not need to reside in the same resource group as the app for the app to function correctly.</span><span class="sxs-lookup"><span data-stu-id="b5727-221">However, the Application Insights and App Service plan do not need to reside in the same resource group as the app for the app to function correctly.</span></span>

<span data-ttu-id="b5727-222">For example, if your resource group contains:</span><span class="sxs-lookup"><span data-stu-id="b5727-222">For example, if your resource group contains:</span></span>

* <span data-ttu-id="b5727-223">**web-a** which is associated with **plan-a** and **app-insights-a**</span><span class="sxs-lookup"><span data-stu-id="b5727-223">**web-a** which is associated with **plan-a** and **app-insights-a**</span></span>
* <span data-ttu-id="b5727-224">**web-b** which is associated with **plan-b** and **app-insights-b**</span><span class="sxs-lookup"><span data-stu-id="b5727-224">**web-b** which is associated with **plan-b** and **app-insights-b**</span></span>

<span data-ttu-id="b5727-225">Your options are:</span><span class="sxs-lookup"><span data-stu-id="b5727-225">Your options are:</span></span>

* <span data-ttu-id="b5727-226">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span><span class="sxs-lookup"><span data-stu-id="b5727-226">Move **web-a**, **plan-a**, **web-b**, and **plan-b**</span></span>
* <span data-ttu-id="b5727-227">Move **web-a** and **web-b**</span><span class="sxs-lookup"><span data-stu-id="b5727-227">Move **web-a** and **web-b**</span></span>
* <span data-ttu-id="b5727-228">Move **web-a**</span><span class="sxs-lookup"><span data-stu-id="b5727-228">Move **web-a**</span></span>
* <span data-ttu-id="b5727-229">Move **web-b**</span><span class="sxs-lookup"><span data-stu-id="b5727-229">Move **web-b**</span></span>

<span data-ttu-id="b5727-230">All other combinations involve either moving a resource type that can't move (Application Insights) or leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span><span class="sxs-lookup"><span data-stu-id="b5727-230">All other combinations involve either moving a resource type that can't move (Application Insights) or leaving behind a resource type that can't be left behind when moving an App Service plan (any type of App Service resource).</span></span>

<span data-ttu-id="b5727-231">If your web app resides in a different resource group than its App Service plan but you want to move both to a new resource group, you must perform the move in two steps.</span><span class="sxs-lookup"><span data-stu-id="b5727-231">If your web app resides in a different resource group than its App Service plan but you want to move both to a new resource group, you must perform the move in two steps.</span></span> <span data-ttu-id="b5727-232">For example:</span><span class="sxs-lookup"><span data-stu-id="b5727-232">For example:</span></span>

* <span data-ttu-id="b5727-233">**web-a** resides in **web-group**</span><span class="sxs-lookup"><span data-stu-id="b5727-233">**web-a** resides in **web-group**</span></span>
* <span data-ttu-id="b5727-234">**plan-a** resides in **plan-group**</span><span class="sxs-lookup"><span data-stu-id="b5727-234">**plan-a** resides in **plan-group**</span></span>
* <span data-ttu-id="b5727-235">You want **web-a** and **plan-a** to reside in **combined-group**</span><span class="sxs-lookup"><span data-stu-id="b5727-235">You want **web-a** and **plan-a** to reside in **combined-group**</span></span>

<span data-ttu-id="b5727-236">To accomplish this move, perform two separate move operations in the following sequence:</span><span class="sxs-lookup"><span data-stu-id="b5727-236">To accomplish this move, perform two separate move operations in the following sequence:</span></span>

1. <span data-ttu-id="b5727-237">Move the **web-a** to **plan-group**</span><span class="sxs-lookup"><span data-stu-id="b5727-237">Move the **web-a** to **plan-group**</span></span>
2. <span data-ttu-id="b5727-238">Move **web-a** and **plan-a** to **combined-group**.</span><span class="sxs-lookup"><span data-stu-id="b5727-238">Move **web-a** and **plan-a** to **combined-group**.</span></span>

<span data-ttu-id="b5727-239">You can move an App Service Certificate to a new resource group or subscription without any issues.</span><span class="sxs-lookup"><span data-stu-id="b5727-239">You can move an App Service Certificate to a new resource group or subscription without any issues.</span></span> <span data-ttu-id="b5727-240">However, if your web app includes an SSL certificate that you purchased externally and uploaded to the app, you must delete the certificate before moving the web app.</span><span class="sxs-lookup"><span data-stu-id="b5727-240">However, if your web app includes an SSL certificate that you purchased externally and uploaded to the app, you must delete the certificate before moving the web app.</span></span> <span data-ttu-id="b5727-241">For example, you can perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b5727-241">For example, you can perform the following steps:</span></span>

1. <span data-ttu-id="b5727-242">Delete the uploaded certificate from the web app</span><span class="sxs-lookup"><span data-stu-id="b5727-242">Delete the uploaded certificate from the web app</span></span>
2. <span data-ttu-id="b5727-243">Move the web app</span><span class="sxs-lookup"><span data-stu-id="b5727-243">Move the web app</span></span>
3. <span data-ttu-id="b5727-244">Upload the certificate to the web app</span><span class="sxs-lookup"><span data-stu-id="b5727-244">Upload the certificate to the web app</span></span>

## <a name="recovery-services-limitations"></a><span data-ttu-id="b5727-245">Recovery Services limitations</span><span class="sxs-lookup"><span data-stu-id="b5727-245">Recovery Services limitations</span></span>
<span data-ttu-id="b5727-246">Move is not enabled for Storage, Network, or Compute resources used to set up disaster recovery with Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="b5727-246">Move is not enabled for Storage, Network, or Compute resources used to set up disaster recovery with Azure Site Recovery.</span></span> 

<span data-ttu-id="b5727-247">For example, suppose you have set up replication of your on-premises machines to a storage account (Storage1) and want the protected machine to come up after failover to Azure as a virtual machine (VM1) attached to a virtual network (Network1).</span><span class="sxs-lookup"><span data-stu-id="b5727-247">For example, suppose you have set up replication of your on-premises machines to a storage account (Storage1) and want the protected machine to come up after failover to Azure as a virtual machine (VM1) attached to a virtual network (Network1).</span></span> <span data-ttu-id="b5727-248">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within the same subscription or across subscriptions.</span><span class="sxs-lookup"><span data-stu-id="b5727-248">You cannot move any of these Azure resources - Storage1, VM1, and Network1 - across resource groups within the same subscription or across subscriptions.</span></span>

## <a name="hdinsight-limitations"></a><span data-ttu-id="b5727-249">HDInsight limitations</span><span class="sxs-lookup"><span data-stu-id="b5727-249">HDInsight limitations</span></span>

<span data-ttu-id="b5727-250">You can move HDInsight clusters to a new subscription or resource group.</span><span class="sxs-lookup"><span data-stu-id="b5727-250">You can move HDInsight clusters to a new subscription or resource group.</span></span> <span data-ttu-id="b5727-251">However, you cannot move across subscriptions the networking resources linked to the HDInsight cluster (such as the virtual network, NIC, or load balancer).</span><span class="sxs-lookup"><span data-stu-id="b5727-251">However, you cannot move across subscriptions the networking resources linked to the HDInsight cluster (such as the virtual network, NIC, or load balancer).</span></span> <span data-ttu-id="b5727-252">In addition, you cannot move to a new resource group a NIC that is attached to a virtual machine for the cluster.</span><span class="sxs-lookup"><span data-stu-id="b5727-252">In addition, you cannot move to a new resource group a NIC that is attached to a virtual machine for the cluster.</span></span>

<span data-ttu-id="b5727-253">When moving an HDInsight cluster to a new subscription, first move other resources (like the storage account).</span><span class="sxs-lookup"><span data-stu-id="b5727-253">When moving an HDInsight cluster to a new subscription, first move other resources (like the storage account).</span></span> <span data-ttu-id="b5727-254">Then, move the HDInsight cluster by itself.</span><span class="sxs-lookup"><span data-stu-id="b5727-254">Then, move the HDInsight cluster by itself.</span></span>

## <a name="classic-deployment-limitations"></a><span data-ttu-id="b5727-255">Classic deployment limitations</span><span class="sxs-lookup"><span data-stu-id="b5727-255">Classic deployment limitations</span></span>
<span data-ttu-id="b5727-256">The options for moving resources deployed through the classic model differ based on whether you are moving the resources within a subscription or to a new subscription.</span><span class="sxs-lookup"><span data-stu-id="b5727-256">The options for moving resources deployed through the classic model differ based on whether you are moving the resources within a subscription or to a new subscription.</span></span> 

### <a name="same-subscription"></a><span data-ttu-id="b5727-257">Same subscription</span><span class="sxs-lookup"><span data-stu-id="b5727-257">Same subscription</span></span>
<span data-ttu-id="b5727-258">When moving resources from one resource group to another resource group within the same subscription, the following restrictions apply:</span><span class="sxs-lookup"><span data-stu-id="b5727-258">When moving resources from one resource group to another resource group within the same subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="b5727-259">Virtual networks (classic) cannot be moved.</span><span class="sxs-lookup"><span data-stu-id="b5727-259">Virtual networks (classic) cannot be moved.</span></span>
* <span data-ttu-id="b5727-260">Virtual machines (classic) must be moved with the cloud service.</span><span class="sxs-lookup"><span data-stu-id="b5727-260">Virtual machines (classic) must be moved with the cloud service.</span></span> 
* <span data-ttu-id="b5727-261">Cloud service can only be moved when the move includes all its virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b5727-261">Cloud service can only be moved when the move includes all its virtual machines.</span></span>
* <span data-ttu-id="b5727-262">Only one cloud service can be moved at a time.</span><span class="sxs-lookup"><span data-stu-id="b5727-262">Only one cloud service can be moved at a time.</span></span>
* <span data-ttu-id="b5727-263">Only one storage account (classic) can be moved at a time.</span><span class="sxs-lookup"><span data-stu-id="b5727-263">Only one storage account (classic) can be moved at a time.</span></span>
* <span data-ttu-id="b5727-264">Storage account (classic) cannot be moved in the same operation with a virtual machine or a cloud service.</span><span class="sxs-lookup"><span data-stu-id="b5727-264">Storage account (classic) cannot be moved in the same operation with a virtual machine or a cloud service.</span></span>

<span data-ttu-id="b5727-265">To move classic resources to a new resource group within the same subscription, use the standard move operations through the [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span><span class="sxs-lookup"><span data-stu-id="b5727-265">To move classic resources to a new resource group within the same subscription, use the standard move operations through the [portal](#use-portal), [Azure PowerShell](#use-powershell), [Azure CLI](#use-azure-cli), or [REST API](#use-rest-api).</span></span> <span data-ttu-id="b5727-266">You use the same operations as you use for moving Resource Manager resources.</span><span class="sxs-lookup"><span data-stu-id="b5727-266">You use the same operations as you use for moving Resource Manager resources.</span></span>

### <a name="new-subscription"></a><span data-ttu-id="b5727-267">New subscription</span><span class="sxs-lookup"><span data-stu-id="b5727-267">New subscription</span></span>
<span data-ttu-id="b5727-268">When moving resources to a new subscription, the following restrictions apply:</span><span class="sxs-lookup"><span data-stu-id="b5727-268">When moving resources to a new subscription, the following restrictions apply:</span></span>

* <span data-ttu-id="b5727-269">All classic resources in the subscription must be moved in the same operation.</span><span class="sxs-lookup"><span data-stu-id="b5727-269">All classic resources in the subscription must be moved in the same operation.</span></span>
* <span data-ttu-id="b5727-270">The target subscription must not contain any other classic resources.</span><span class="sxs-lookup"><span data-stu-id="b5727-270">The target subscription must not contain any other classic resources.</span></span>
* <span data-ttu-id="b5727-271">The move can only be requested through a separate REST API for classic moves.</span><span class="sxs-lookup"><span data-stu-id="b5727-271">The move can only be requested through a separate REST API for classic moves.</span></span> <span data-ttu-id="b5727-272">The standard Resource Manager move commands do not work when moving classic resources to a new subscription.</span><span class="sxs-lookup"><span data-stu-id="b5727-272">The standard Resource Manager move commands do not work when moving classic resources to a new subscription.</span></span>

<span data-ttu-id="b5727-273">To move classic resources to a new subscription, use either the portal or REST operations that are specific to classic resources.</span><span class="sxs-lookup"><span data-stu-id="b5727-273">To move classic resources to a new subscription, use either the portal or REST operations that are specific to classic resources.</span></span> <span data-ttu-id="b5727-274">For information about moving classic resources through the portal, see [Use portal](#use-portal).</span><span class="sxs-lookup"><span data-stu-id="b5727-274">For information about moving classic resources through the portal, see [Use portal](#use-portal).</span></span> <span data-ttu-id="b5727-275">To use REST, perform the following steps:</span><span class="sxs-lookup"><span data-stu-id="b5727-275">To use REST, perform the following steps:</span></span>

1. <span data-ttu-id="b5727-276">Check if the source subscription can participate in a cross-subscription move.</span><span class="sxs-lookup"><span data-stu-id="b5727-276">Check if the source subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="b5727-277">Use the following operation:</span><span class="sxs-lookup"><span data-stu-id="b5727-277">Use the following operation:</span></span>

  ```HTTP   
  POST https://management.azure.com/subscriptions/{sourceSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```
   
     <span data-ttu-id="b5727-278">In the request body, include:</span><span class="sxs-lookup"><span data-stu-id="b5727-278">In the request body, include:</span></span>

  ```json 
  {
    "role": "source"
  }
  ```
  
     <span data-ttu-id="b5727-279">The response for the validation operation is in the following format:</span><span class="sxs-lookup"><span data-stu-id="b5727-279">The response for the validation operation is in the following format:</span></span>

  ```json 
  {
    "status": "{status}",
    "reasons": [
      "reason1",
      "reason2"
    ]
  }
  ```

2. <span data-ttu-id="b5727-280">Check if the destination subscription can participate in a cross-subscription move.</span><span class="sxs-lookup"><span data-stu-id="b5727-280">Check if the destination subscription can participate in a cross-subscription move.</span></span> <span data-ttu-id="b5727-281">Use the following operation:</span><span class="sxs-lookup"><span data-stu-id="b5727-281">Use the following operation:</span></span>

  ```HTTP 
  POST https://management.azure.com/subscriptions/{destinationSubscriptionId}/providers/Microsoft.ClassicCompute/validateSubscriptionMoveAvailability?api-version=2016-04-01
  ```

     <span data-ttu-id="b5727-282">In the request body, include:</span><span class="sxs-lookup"><span data-stu-id="b5727-282">In the request body, include:</span></span>

  ```json 
  {
    "role": "target"
  }
  ```
   
     <span data-ttu-id="b5727-283">The response is in the same format as the source subscription validation.</span><span class="sxs-lookup"><span data-stu-id="b5727-283">The response is in the same format as the source subscription validation.</span></span>
3. <span data-ttu-id="b5727-284">If both subscriptions pass validation, move all classic resources from one subscription to another subscription with the following operation:</span><span class="sxs-lookup"><span data-stu-id="b5727-284">If both subscriptions pass validation, move all classic resources from one subscription to another subscription with the following operation:</span></span>

  ```HTTP 
  POST https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.ClassicCompute/moveSubscriptionResources?api-version=2016-04-01
  ```

    <span data-ttu-id="b5727-285">In the request body, include:</span><span class="sxs-lookup"><span data-stu-id="b5727-285">In the request body, include:</span></span>

  ```json 
  {
    "target": "/subscriptions/{target-subscription-id}"
  }
  ```

<span data-ttu-id="b5727-286">The operation may run for several minutes.</span><span class="sxs-lookup"><span data-stu-id="b5727-286">The operation may run for several minutes.</span></span> 

## <a name="use-portal"></a><span data-ttu-id="b5727-287">Use portal</span><span class="sxs-lookup"><span data-stu-id="b5727-287">Use portal</span></span>
<span data-ttu-id="b5727-288">To move resources, select the resource group containing those resources, and then select the **Move** button.</span><span class="sxs-lookup"><span data-stu-id="b5727-288">To move resources, select the resource group containing those resources, and then select the **Move** button.</span></span>

![move resources](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-move-resources/select-move.png)

<span data-ttu-id="b5727-290">Select whether you are moving the resources to a new resource group or a new subscription.</span><span class="sxs-lookup"><span data-stu-id="b5727-290">Select whether you are moving the resources to a new resource group or a new subscription.</span></span>

<span data-ttu-id="b5727-291">Select the resources to move and the destination resource group.</span><span class="sxs-lookup"><span data-stu-id="b5727-291">Select the resources to move and the destination resource group.</span></span> <span data-ttu-id="b5727-292">Acknowledge that you need to update scripts for these resources and select **OK**.</span><span class="sxs-lookup"><span data-stu-id="b5727-292">Acknowledge that you need to update scripts for these resources and select **OK**.</span></span> <span data-ttu-id="b5727-293">If you selected the edit subscription icon in the previous step, you must also select the destination subscription.</span><span class="sxs-lookup"><span data-stu-id="b5727-293">If you selected the edit subscription icon in the previous step, you must also select the destination subscription.</span></span>

![select destination](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-move-resources/select-destination.png)

<span data-ttu-id="b5727-295">In **Notifications**, you see that the move operation is running.</span><span class="sxs-lookup"><span data-stu-id="b5727-295">In **Notifications**, you see that the move operation is running.</span></span>

![show move status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-move-resources/show-status.png)

<span data-ttu-id="b5727-297">When it has completed, you are notified of the result.</span><span class="sxs-lookup"><span data-stu-id="b5727-297">When it has completed, you are notified of the result.</span></span>

![show move result](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-resource-manager/media/resource-group-move-resources/show-result.png)

## <a name="use-powershell"></a><span data-ttu-id="b5727-299">Use PowerShell</span><span class="sxs-lookup"><span data-stu-id="b5727-299">Use PowerShell</span></span>
<span data-ttu-id="b5727-300">To move existing resources to another resource group or subscription, use the `Move-AzureRmResource` command.</span><span class="sxs-lookup"><span data-stu-id="b5727-300">To move existing resources to another resource group or subscription, use the `Move-AzureRmResource` command.</span></span>

<span data-ttu-id="b5727-301">The first example shows how to move one resource to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="b5727-301">The first example shows how to move one resource to a new resource group.</span></span>

```powershell
$resource = Get-AzureRmResource -ResourceName ExampleApp -ResourceGroupName OldRG
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $resource.ResourceId
```

<span data-ttu-id="b5727-302">The second example shows how to move multiple resources to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="b5727-302">The second example shows how to move multiple resources to a new resource group.</span></span>

```powershell
$webapp = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExampleSite
$plan = Get-AzureRmResource -ResourceGroupName OldRG -ResourceName ExamplePlan
Move-AzureRmResource -DestinationResourceGroupName NewRG -ResourceId $webapp.ResourceId, $plan.ResourceId
```

<span data-ttu-id="b5727-303">To move to a new subscription, include a value for the `DestinationSubscriptionId` parameter.</span><span class="sxs-lookup"><span data-stu-id="b5727-303">To move to a new subscription, include a value for the `DestinationSubscriptionId` parameter.</span></span>

<span data-ttu-id="b5727-304">You are asked to confirm that you want to move the specified resources.</span><span class="sxs-lookup"><span data-stu-id="b5727-304">You are asked to confirm that you want to move the specified resources.</span></span>

```powershell
Confirm
Are you sure you want to move these resources to the resource group
'/subscriptions/{guid}/resourceGroups/newRG' the resources:

/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/serverFarms/exampleplan
/subscriptions/{guid}/resourceGroups/destinationgroup/providers/Microsoft.Web/sites/examplesite
[Y] Yes  [N] No  [S] Suspend  [?] Help (default is "Y"): y
```

## <a name="use-azure-cli-20"></a><span data-ttu-id="b5727-305">Use Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="b5727-305">Use Azure CLI 2.0</span></span>
<span data-ttu-id="b5727-306">To move existing resources to another resource group or subscription, use the `az resource move` command.</span><span class="sxs-lookup"><span data-stu-id="b5727-306">To move existing resources to another resource group or subscription, use the `az resource move` command.</span></span> <span data-ttu-id="b5727-307">Provide the resource IDs of the resources to move.</span><span class="sxs-lookup"><span data-stu-id="b5727-307">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="b5727-308">You can get resource IDs with the following command:</span><span class="sxs-lookup"><span data-stu-id="b5727-308">You can get resource IDs with the following command:</span></span>

```azurecli
az resource show -g sourceGroup -n storagedemo --resource-type "Microsoft.Storage/storageAccounts" --query id
```

<span data-ttu-id="b5727-309">The following example shows how to move a storage account to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="b5727-309">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="b5727-310">In the `--ids` parameter, provide a space-separated list of the resource IDs to move.</span><span class="sxs-lookup"><span data-stu-id="b5727-310">In the `--ids` parameter, provide a space-separated list of the resource IDs to move.</span></span>

```azurecli
az resource move --destination-group newgroup --ids "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo"
```

<span data-ttu-id="b5727-311">To move to a new subscription, provide the `--destination-subscription-id` parameter.</span><span class="sxs-lookup"><span data-stu-id="b5727-311">To move to a new subscription, provide the `--destination-subscription-id` parameter.</span></span>

## <a name="use-azure-cli-10"></a><span data-ttu-id="b5727-312">Use Azure CLI 1.0</span><span class="sxs-lookup"><span data-stu-id="b5727-312">Use Azure CLI 1.0</span></span>
<span data-ttu-id="b5727-313">To move existing resources to another resource group or subscription, use the `azure resource move` command.</span><span class="sxs-lookup"><span data-stu-id="b5727-313">To move existing resources to another resource group or subscription, use the `azure resource move` command.</span></span> <span data-ttu-id="b5727-314">Provide the resource IDs of the resources to move.</span><span class="sxs-lookup"><span data-stu-id="b5727-314">Provide the resource IDs of the resources to move.</span></span> <span data-ttu-id="b5727-315">You can get resource IDs with the following command:</span><span class="sxs-lookup"><span data-stu-id="b5727-315">You can get resource IDs with the following command:</span></span>

```azurecli
azure resource list -g sourceGroup --json
```

<span data-ttu-id="b5727-316">Which returns the following format:</span><span class="sxs-lookup"><span data-stu-id="b5727-316">Which returns the following format:</span></span>

```azurecli
[
  {
    "id": "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo",
    "name": "storagedemo",
    "type": "Microsoft.Storage/storageAccounts",
    "location": "southcentralus",
    "tags": {},
    "kind": "Storage",
    "sku": {
      "name": "Standard_RAGRS",
      "tier": "Standard"
    }
  }
]
```

<span data-ttu-id="b5727-317">The following example shows how to move a storage account to a new resource group.</span><span class="sxs-lookup"><span data-stu-id="b5727-317">The following example shows how to move a storage account to a new resource group.</span></span> <span data-ttu-id="b5727-318">In the `-i` parameter, provide a comma-separated list of the resource IDs to move.</span><span class="sxs-lookup"><span data-stu-id="b5727-318">In the `-i` parameter, provide a comma-separated list of the resource IDs to move.</span></span>

```azurecli
azure resource move -i "/subscriptions/{guid}/resourceGroups/sourceGroup/providers/Microsoft.Storage/storageAccounts/storagedemo" -d "destinationGroup"
```

<span data-ttu-id="b5727-319">You are asked to confirm that you want to move the specified resource.</span><span class="sxs-lookup"><span data-stu-id="b5727-319">You are asked to confirm that you want to move the specified resource.</span></span>

## <a name="use-rest-api"></a><span data-ttu-id="b5727-320">Use REST API</span><span class="sxs-lookup"><span data-stu-id="b5727-320">Use REST API</span></span>
<span data-ttu-id="b5727-321">To move existing resources to another resource group or subscription, run:</span><span class="sxs-lookup"><span data-stu-id="b5727-321">To move existing resources to another resource group or subscription, run:</span></span>

```HTTP
POST https://management.azure.com/subscriptions/{source-subscription-id}/resourcegroups/{source-resource-group-name}/moveResources?api-version={api-version} 
```

<span data-ttu-id="b5727-322">In the request body, you specify the target resource group and the resources to move.</span><span class="sxs-lookup"><span data-stu-id="b5727-322">In the request body, you specify the target resource group and the resources to move.</span></span> <span data-ttu-id="b5727-323">For more information about the move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span><span class="sxs-lookup"><span data-stu-id="b5727-323">For more information about the move REST operation, see [Move resources](https://msdn.microsoft.com/library/azure/mt218710.aspx).</span></span>

## <a name="next-steps"></a><span data-ttu-id="b5727-324">Next steps</span><span class="sxs-lookup"><span data-stu-id="b5727-324">Next steps</span></span>
* <span data-ttu-id="b5727-325">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b5727-325">To learn about PowerShell cmdlets for managing your subscription, see [Using Azure PowerShell with Resource Manager](powershell-azure-resource-manager.md).</span></span>
* <span data-ttu-id="b5727-326">To learn about Azure CLI commands for managing your subscription, see [Using the Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="b5727-326">To learn about Azure CLI commands for managing your subscription, see [Using the Azure CLI with Resource Manager](xplat-cli-azure-resource-manager.md).</span></span>
* <span data-ttu-id="b5727-327">To learn about portal features for managing your subscription, see [Using the Azure portal to manage resources](resource-group-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b5727-327">To learn about portal features for managing your subscription, see [Using the Azure portal to manage resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="b5727-328">To learn about applying a logical organization to your resources, see [Using tags to organize your resources](resource-group-using-tags.md).</span><span class="sxs-lookup"><span data-stu-id="b5727-328">To learn about applying a logical organization to your resources, see [Using tags to organize your resources](resource-group-using-tags.md).</span></span>






