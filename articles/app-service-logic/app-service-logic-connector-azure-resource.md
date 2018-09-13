---
title: Using the Azure Resource Connector in Logic apps | Microsoft Docs
description: How to create and configure the Azure Resource Connector or API app and use it in a Logic app in Azure App Service
services: logic-apps
documentationcenter: .net,nodejs,java
author: stepsic-microsoft-com
manager: erikre
editor: ''
ms.assetid: a32e5a5c-34d7-4422-b0f7-c5cf7b8abffa
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 09/01/2016
ms.author: stepsic
ms.openlocfilehash: d230450535613e85c607ef120929ea61bc2085bc
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555107"
---
# <a name="get-started-with-the-azure-resource-connector-and-add-it-to-your-logic-app"></a><span data-ttu-id="de846-103">Get started with the Azure Resource Connector and add it to your Logic app</span><span class="sxs-lookup"><span data-stu-id="de846-103">Get started with the Azure Resource Connector and add it to your Logic app</span></span>
> [!NOTE]
> <span data-ttu-id="de846-104">This version of the article applies to Logic apps 2014-12-01-preview schema version.</span><span class="sxs-lookup"><span data-stu-id="de846-104">This version of the article applies to Logic apps 2014-12-01-preview schema version.</span></span>
> 
> 

<span data-ttu-id="de846-105">Use the Azure Resource Connector to easily manage Azure Resources inside of your Logic app.</span><span class="sxs-lookup"><span data-stu-id="de846-105">Use the Azure Resource Connector to easily manage Azure Resources inside of your Logic app.</span></span>

## <a name="create-the-azure-resource-connector"></a><span data-ttu-id="de846-106">Create the Azure Resource Connector</span><span class="sxs-lookup"><span data-stu-id="de846-106">Create the Azure Resource Connector</span></span>
<span data-ttu-id="de846-107">To use the Azure Resource Connector API app, you need to first create an instance of it.</span><span class="sxs-lookup"><span data-stu-id="de846-107">To use the Azure Resource Connector API app, you need to first create an instance of it.</span></span> <span data-ttu-id="de846-108">This can be done either inline while creating a Logic app or by selecting the Azure Resource Manger Connector API app from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="de846-108">This can be done either inline while creating a Logic app or by selecting the Azure Resource Manger Connector API app from the Azure Marketplace.</span></span>

<span data-ttu-id="de846-109">To configure it, you have you need to set up a Service Principal with permissions to do whatever it is you want to do in Azure.</span><span class="sxs-lookup"><span data-stu-id="de846-109">To configure it, you have you need to set up a Service Principal with permissions to do whatever it is you want to do in Azure.</span></span> <span data-ttu-id="de846-110">All calls will be made on-behalf-of this Service Principal that you set up.</span><span class="sxs-lookup"><span data-stu-id="de846-110">All calls will be made on-behalf-of this Service Principal that you set up.</span></span> <span data-ttu-id="de846-111">This allows you to scope the Connector to use only exactly what you want it to do, and nothing more.</span><span class="sxs-lookup"><span data-stu-id="de846-111">This allows you to scope the Connector to use only exactly what you want it to do, and nothing more.</span></span>

<span data-ttu-id="de846-112">David Ebbo has written [a great blog post](http://blog.davidebbo.com/2014/12/azure-service-principal.html) on how to set this up.</span><span class="sxs-lookup"><span data-stu-id="de846-112">David Ebbo has written [a great blog post](http://blog.davidebbo.com/2014/12/azure-service-principal.html) on how to set this up.</span></span> <span data-ttu-id="de846-113">Please follow all the instructions there and get your **Tenant ID**, **Client ID** and **Secret**.</span><span class="sxs-lookup"><span data-stu-id="de846-113">Please follow all the instructions there and get your **Tenant ID**, **Client ID** and **Secret**.</span></span> <span data-ttu-id="de846-114">These three fields, plus the **Subscription ID**, are what are required to configure the Connector.</span><span class="sxs-lookup"><span data-stu-id="de846-114">These three fields, plus the **Subscription ID**, are what are required to configure the Connector.</span></span>

## <a name="using-the-azure-resource-connector-in-logic-app-designer"></a><span data-ttu-id="de846-115">Using the Azure Resource Connector in Logic App Designer</span><span class="sxs-lookup"><span data-stu-id="de846-115">Using the Azure Resource Connector in Logic App Designer</span></span>
### <a name="trigger"></a><span data-ttu-id="de846-116">Trigger</span><span class="sxs-lookup"><span data-stu-id="de846-116">Trigger</span></span>
<span data-ttu-id="de846-117">There are two triggers that are supported in the Connector:</span><span class="sxs-lookup"><span data-stu-id="de846-117">There are two triggers that are supported in the Connector:</span></span>

| <span data-ttu-id="de846-118">Name</span><span class="sxs-lookup"><span data-stu-id="de846-118">Name</span></span> | <span data-ttu-id="de846-119">Description</span><span class="sxs-lookup"><span data-stu-id="de846-119">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de846-120">Event occurs</span><span class="sxs-lookup"><span data-stu-id="de846-120">Event occurs</span></span> |<span data-ttu-id="de846-121">Trigger when an event occurs to a resource in your subscription.</span><span class="sxs-lookup"><span data-stu-id="de846-121">Trigger when an event occurs to a resource in your subscription.</span></span> |
| <span data-ttu-id="de846-122">Metric crosses threshold</span><span class="sxs-lookup"><span data-stu-id="de846-122">Metric crosses threshold</span></span> |<span data-ttu-id="de846-123">Trigger when a metric meets a certain threshold.</span><span class="sxs-lookup"><span data-stu-id="de846-123">Trigger when a metric meets a certain threshold.</span></span> |

### <a name="action"></a><span data-ttu-id="de846-124">Action</span><span class="sxs-lookup"><span data-stu-id="de846-124">Action</span></span>
<span data-ttu-id="de846-125">Likewise, you can provide a large number of actions inside your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="de846-125">Likewise, you can provide a large number of actions inside your Azure subscription:</span></span>

<span data-ttu-id="de846-126">For **Resource groups** you can:</span><span class="sxs-lookup"><span data-stu-id="de846-126">For **Resource groups** you can:</span></span>

| <span data-ttu-id="de846-127">Name</span><span class="sxs-lookup"><span data-stu-id="de846-127">Name</span></span> | <span data-ttu-id="de846-128">Description</span><span class="sxs-lookup"><span data-stu-id="de846-128">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de846-129">List resource groups</span><span class="sxs-lookup"><span data-stu-id="de846-129">List resource groups</span></span> |<span data-ttu-id="de846-130">List all of the resource groups in the subscription.</span><span class="sxs-lookup"><span data-stu-id="de846-130">List all of the resource groups in the subscription.</span></span> |
| <span data-ttu-id="de846-131">Get resource group</span><span class="sxs-lookup"><span data-stu-id="de846-131">Get resource group</span></span> |<span data-ttu-id="de846-132">Get a resource group by its id.</span><span class="sxs-lookup"><span data-stu-id="de846-132">Get a resource group by its id.</span></span> |
| <span data-ttu-id="de846-133">Create resource group</span><span class="sxs-lookup"><span data-stu-id="de846-133">Create resource group</span></span> |<span data-ttu-id="de846-134">Create or update a resource group.</span><span class="sxs-lookup"><span data-stu-id="de846-134">Create or update a resource group.</span></span> |
| <span data-ttu-id="de846-135">Delete resource group</span><span class="sxs-lookup"><span data-stu-id="de846-135">Delete resource group</span></span> |<span data-ttu-id="de846-136">Delete a resource group.</span><span class="sxs-lookup"><span data-stu-id="de846-136">Delete a resource group.</span></span> |

<span data-ttu-id="de846-137">For **Resources** you can:</span><span class="sxs-lookup"><span data-stu-id="de846-137">For **Resources** you can:</span></span>

| <span data-ttu-id="de846-138">Name</span><span class="sxs-lookup"><span data-stu-id="de846-138">Name</span></span> | <span data-ttu-id="de846-139">Description</span><span class="sxs-lookup"><span data-stu-id="de846-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de846-140">List resources</span><span class="sxs-lookup"><span data-stu-id="de846-140">List resources</span></span> |<span data-ttu-id="de846-141">List resources in your subscription by different types of filters.</span><span class="sxs-lookup"><span data-stu-id="de846-141">List resources in your subscription by different types of filters.</span></span> |
| <span data-ttu-id="de846-142">Get resource</span><span class="sxs-lookup"><span data-stu-id="de846-142">Get resource</span></span> |<span data-ttu-id="de846-143">Get a single resource by its resource Id.</span><span class="sxs-lookup"><span data-stu-id="de846-143">Get a single resource by its resource Id.</span></span> |
| <span data-ttu-id="de846-144">Create or update resource</span><span class="sxs-lookup"><span data-stu-id="de846-144">Create or update resource</span></span> |<span data-ttu-id="de846-145">Create a resource, or, update an existing resource.</span><span class="sxs-lookup"><span data-stu-id="de846-145">Create a resource, or, update an existing resource.</span></span> <span data-ttu-id="de846-146">You must provide all of the properties for that resource.</span><span class="sxs-lookup"><span data-stu-id="de846-146">You must provide all of the properties for that resource.</span></span> |
| <span data-ttu-id="de846-147">Resource action</span><span class="sxs-lookup"><span data-stu-id="de846-147">Resource action</span></span> |<span data-ttu-id="de846-148">Perform any other action on a resource.</span><span class="sxs-lookup"><span data-stu-id="de846-148">Perform any other action on a resource.</span></span> <span data-ttu-id="de846-149">You need to know the action name and the payload that this action takes (if any).</span><span class="sxs-lookup"><span data-stu-id="de846-149">You need to know the action name and the payload that this action takes (if any).</span></span> |
| <span data-ttu-id="de846-150">Delete resource</span><span class="sxs-lookup"><span data-stu-id="de846-150">Delete resource</span></span> |<span data-ttu-id="de846-151">Delete a resource.</span><span class="sxs-lookup"><span data-stu-id="de846-151">Delete a resource.</span></span> |

<span data-ttu-id="de846-152">For **Resource Providers** you can:</span><span class="sxs-lookup"><span data-stu-id="de846-152">For **Resource Providers** you can:</span></span>

| <span data-ttu-id="de846-153">Name</span><span class="sxs-lookup"><span data-stu-id="de846-153">Name</span></span> | <span data-ttu-id="de846-154">Description</span><span class="sxs-lookup"><span data-stu-id="de846-154">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de846-155">List resource providers</span><span class="sxs-lookup"><span data-stu-id="de846-155">List resource providers</span></span> |<span data-ttu-id="de846-156">List all of the available resource providers in the subscription.</span><span class="sxs-lookup"><span data-stu-id="de846-156">List all of the available resource providers in the subscription.</span></span> |

<span data-ttu-id="de846-157">For **Resource Group Deployments** you can:</span><span class="sxs-lookup"><span data-stu-id="de846-157">For **Resource Group Deployments** you can:</span></span>

| <span data-ttu-id="de846-158">Name</span><span class="sxs-lookup"><span data-stu-id="de846-158">Name</span></span> | <span data-ttu-id="de846-159">Description</span><span class="sxs-lookup"><span data-stu-id="de846-159">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de846-160">List deployments</span><span class="sxs-lookup"><span data-stu-id="de846-160">List deployments</span></span> |<span data-ttu-id="de846-161">List all of the deployments in a resource group.</span><span class="sxs-lookup"><span data-stu-id="de846-161">List all of the deployments in a resource group.</span></span> |
| <span data-ttu-id="de846-162">Get deployment</span><span class="sxs-lookup"><span data-stu-id="de846-162">Get deployment</span></span> |<span data-ttu-id="de846-163">Get a template deployment by its id.</span><span class="sxs-lookup"><span data-stu-id="de846-163">Get a template deployment by its id.</span></span> |
| <span data-ttu-id="de846-164">Create deployment</span><span class="sxs-lookup"><span data-stu-id="de846-164">Create deployment</span></span> |<span data-ttu-id="de846-165">Create a new resource group deployment by providing a template.</span><span class="sxs-lookup"><span data-stu-id="de846-165">Create a new resource group deployment by providing a template.</span></span> |

<span data-ttu-id="de846-166">For **Events** about resources you can:</span><span class="sxs-lookup"><span data-stu-id="de846-166">For **Events** about resources you can:</span></span>

| <span data-ttu-id="de846-167">Name</span><span class="sxs-lookup"><span data-stu-id="de846-167">Name</span></span> | <span data-ttu-id="de846-168">Description</span><span class="sxs-lookup"><span data-stu-id="de846-168">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de846-169">Get events</span><span class="sxs-lookup"><span data-stu-id="de846-169">Get events</span></span> |<span data-ttu-id="de846-170">Get events in a subscription or for a resource.</span><span class="sxs-lookup"><span data-stu-id="de846-170">Get events in a subscription or for a resource.</span></span> |

<span data-ttu-id="de846-171">For **Metrics** about resources you can:</span><span class="sxs-lookup"><span data-stu-id="de846-171">For **Metrics** about resources you can:</span></span>

| <span data-ttu-id="de846-172">Name</span><span class="sxs-lookup"><span data-stu-id="de846-172">Name</span></span> | <span data-ttu-id="de846-173">Description</span><span class="sxs-lookup"><span data-stu-id="de846-173">Description</span></span> |
| --- | --- |
| <span data-ttu-id="de846-174">Get metrics</span><span class="sxs-lookup"><span data-stu-id="de846-174">Get metrics</span></span> |<span data-ttu-id="de846-175">Get a metric for a resource Id.</span><span class="sxs-lookup"><span data-stu-id="de846-175">Get a metric for a resource Id.</span></span> |

## <a name="do-more-with-your-connector"></a><span data-ttu-id="de846-176">Do more with your connector</span><span class="sxs-lookup"><span data-stu-id="de846-176">Do more with your connector</span></span>
<span data-ttu-id="de846-177">Now that the connector is created, you can add it to a business flow using a Logic app.</span><span class="sxs-lookup"><span data-stu-id="de846-177">Now that the connector is created, you can add it to a business flow using a Logic app.</span></span> <span data-ttu-id="de846-178">See [What are Logic apps?](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="de846-178">See [What are Logic apps?](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

> [!NOTE]
> <span data-ttu-id="de846-179">If you want to get started with Azure Logic apps before signing up for an Azure account, go to [Try Logic app](https://azure.microsoft.com/try/app-service/logic/), where you can immediately create a short-lived starter Logic app in App Service.</span><span class="sxs-lookup"><span data-stu-id="de846-179">If you want to get started with Azure Logic apps before signing up for an Azure account, go to [Try Logic app](https://azure.microsoft.com/try/app-service/logic/), where you can immediately create a short-lived starter Logic app in App Service.</span></span> <span data-ttu-id="de846-180">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="de846-180">No credit cards required; no commitments.</span></span>
> 
> 

<span data-ttu-id="de846-181">View the Swagger REST API reference at [Connectors and API apps Reference](http://go.microsoft.com/fwlink/p/?LinkId=529766).</span><span class="sxs-lookup"><span data-stu-id="de846-181">View the Swagger REST API reference at [Connectors and API apps Reference](http://go.microsoft.com/fwlink/p/?LinkId=529766).</span></span>

<!--References -->

<!--Links -->
[Creating a Logic app]: app-service-logic-create-a-logic-app.md
