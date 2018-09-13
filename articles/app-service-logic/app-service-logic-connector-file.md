---
title: Using the File connector in Logic apps | Microsoft Docs
description: How to create and configure the file connector or API app and use it in a Logic app in Azure App Service
author: rajeshramabathiran
manager: erikre
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: 07ceb81a-f8f6-4901-a7a2-06a9ac47efd5
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/01/2016
ms.author: rajram
ms.openlocfilehash: 855c02130600dd7650e31ebc8807ee5e837f5c68
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556347"
---
# <a name="get-started-with-the-file-connector-and-add-it-to-your-logic-app"></a><span data-ttu-id="d11d4-103">Get started with the file connector and add it to your Logic app</span><span class="sxs-lookup"><span data-stu-id="d11d4-103">Get started with the file connector and add it to your Logic app</span></span>
> [!NOTE]
> <span data-ttu-id="d11d4-104">This version of the article applies to Logic apps 2014-12-01-preview schema version.</span><span class="sxs-lookup"><span data-stu-id="d11d4-104">This version of the article applies to Logic apps 2014-12-01-preview schema version.</span></span>
>
>

<span data-ttu-id="d11d4-105">Connect to a file system to upload, download, and more to your files on a host machine.</span><span class="sxs-lookup"><span data-stu-id="d11d4-105">Connect to a file system to upload, download, and more to your files on a host machine.</span></span> <span data-ttu-id="d11d4-106">Logic apps can trigger based on a variety of data sources and offer connectors to get and process data.</span><span class="sxs-lookup"><span data-stu-id="d11d4-106">Logic apps can trigger based on a variety of data sources and offer connectors to get and process data.</span></span> <span data-ttu-id="d11d4-107">You can add the file connector to your business workflow and process data as part of this workflow within a Logic app.</span><span class="sxs-lookup"><span data-stu-id="d11d4-107">You can add the file connector to your business workflow and process data as part of this workflow within a Logic app.</span></span>

<span data-ttu-id="d11d4-108">The file connector uses the Hybrid Connection Manager for hybrid connectivity to the host file system.</span><span class="sxs-lookup"><span data-stu-id="d11d4-108">The file connector uses the Hybrid Connection Manager for hybrid connectivity to the host file system.</span></span>

## <a name="creating-a-file-connector-for-your-logic-app"></a><span data-ttu-id="d11d4-109">Creating a file connector for your Logic app</span><span class="sxs-lookup"><span data-stu-id="d11d4-109">Creating a file connector for your Logic app</span></span>
<span data-ttu-id="d11d4-110">To use the file connector, you need to first create an instance of the file connector API app.</span><span class="sxs-lookup"><span data-stu-id="d11d4-110">To use the file connector, you need to first create an instance of the file connector API app.</span></span> <span data-ttu-id="d11d4-111">This can be done as follows:</span><span class="sxs-lookup"><span data-stu-id="d11d4-111">This can be done as follows:</span></span>

1. <span data-ttu-id="d11d4-112">Open the Azure Marketplace using the + NEW option on the left side of the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="d11d4-112">Open the Azure Marketplace using the + NEW option on the left side of the Azure Portal.</span></span>
2. <span data-ttu-id="d11d4-113">Search for “file connector”.</span><span class="sxs-lookup"><span data-stu-id="d11d4-113">Search for “file connector”.</span></span>
3. <span data-ttu-id="d11d4-114">Select **File Connector (preview)** from the search results.</span><span class="sxs-lookup"><span data-stu-id="d11d4-114">Select **File Connector (preview)** from the search results.</span></span>
4. <span data-ttu-id="d11d4-115">Select the **Create** button</span><span class="sxs-lookup"><span data-stu-id="d11d4-115">Select the **Create** button</span></span>
5. <span data-ttu-id="d11d4-116">Configure the file connector as follows:</span><span class="sxs-lookup"><span data-stu-id="d11d4-116">Configure the file connector as follows:</span></span>  
   ![][1]

   * <span data-ttu-id="d11d4-117">**Name** - give a name for your file connector</span><span class="sxs-lookup"><span data-stu-id="d11d4-117">**Name** - give a name for your file connector</span></span>
   * <span data-ttu-id="d11d4-118">**Package Settings**</span><span class="sxs-lookup"><span data-stu-id="d11d4-118">**Package Settings**</span></span>
     * <span data-ttu-id="d11d4-119">**Root Folder** - Specify the root folder path on your host machine.</span><span class="sxs-lookup"><span data-stu-id="d11d4-119">**Root Folder** - Specify the root folder path on your host machine.</span></span> <span data-ttu-id="d11d4-120">Eg.</span><span class="sxs-lookup"><span data-stu-id="d11d4-120">Eg.</span></span> <span data-ttu-id="d11d4-121">D:\FileConnectorTest</span><span class="sxs-lookup"><span data-stu-id="d11d4-121">D:\FileConnectorTest</span></span>
     * <span data-ttu-id="d11d4-122">**Service Bus Connection String** - Provide a Service Bus Connection String.</span><span class="sxs-lookup"><span data-stu-id="d11d4-122">**Service Bus Connection String** - Provide a Service Bus Connection String.</span></span> <span data-ttu-id="d11d4-123">Make sure that the service bus namespace is of type Standard and NOT Basic to allow for use of Service Bus Relays.</span><span class="sxs-lookup"><span data-stu-id="d11d4-123">Make sure that the service bus namespace is of type Standard and NOT Basic to allow for use of Service Bus Relays.</span></span>  <span data-ttu-id="d11d4-124">Service Bus Relay is used to connect to the Hybrid Connection Manager.</span><span class="sxs-lookup"><span data-stu-id="d11d4-124">Service Bus Relay is used to connect to the Hybrid Connection Manager.</span></span>
   * <span data-ttu-id="d11d4-125">**App Service plan** - select or create a App Service plan</span><span class="sxs-lookup"><span data-stu-id="d11d4-125">**App Service plan** - select or create a App Service plan</span></span>
   * <span data-ttu-id="d11d4-126">**Pricing tier** - choose a pricing tier for the connector</span><span class="sxs-lookup"><span data-stu-id="d11d4-126">**Pricing tier** - choose a pricing tier for the connector</span></span>
   * <span data-ttu-id="d11d4-127">**Resource group** - select or create a resource group where the connector should reside</span><span class="sxs-lookup"><span data-stu-id="d11d4-127">**Resource group** - select or create a resource group where the connector should reside</span></span>
   * <span data-ttu-id="d11d4-128">**Subscription** - choose a subscription you want this connector to be created in</span><span class="sxs-lookup"><span data-stu-id="d11d4-128">**Subscription** - choose a subscription you want this connector to be created in</span></span>
   * <span data-ttu-id="d11d4-129">**Location** - choose the geographic location where you would like the connector to be deployed</span><span class="sxs-lookup"><span data-stu-id="d11d4-129">**Location** - choose the geographic location where you would like the connector to be deployed</span></span>
6. <span data-ttu-id="d11d4-130">Click on Create.</span><span class="sxs-lookup"><span data-stu-id="d11d4-130">Click on Create.</span></span> <span data-ttu-id="d11d4-131">A new file connector will be created</span><span class="sxs-lookup"><span data-stu-id="d11d4-131">A new file connector will be created</span></span>

## <a name="configure-hybrid-connection-manager"></a><span data-ttu-id="d11d4-132">Configure Hybrid Connection Manager</span><span class="sxs-lookup"><span data-stu-id="d11d4-132">Configure Hybrid Connection Manager</span></span>
<span data-ttu-id="d11d4-133">Once the API App instance is created, browse to its dashboard.</span><span class="sxs-lookup"><span data-stu-id="d11d4-133">Once the API App instance is created, browse to its dashboard.</span></span>  <span data-ttu-id="d11d4-134">This can be done by clicking on Browse > API Apps > select your file connector API App.</span><span class="sxs-lookup"><span data-stu-id="d11d4-134">This can be done by clicking on Browse > API Apps > select your file connector API App.</span></span>  <span data-ttu-id="d11d4-135">From here the Hybrid Connection Manager needs to be configured.</span><span class="sxs-lookup"><span data-stu-id="d11d4-135">From here the Hybrid Connection Manager needs to be configured.</span></span>
<span data-ttu-id="d11d4-136">For more information on configuring and trouble shooting the Hybrid Connection Manager see [Using the Hybrid Connection Manager].</span><span class="sxs-lookup"><span data-stu-id="d11d4-136">For more information on configuring and trouble shooting the Hybrid Connection Manager see [Using the Hybrid Connection Manager].</span></span>

## <a name="using-the-file-connector-in-your-logic-app"></a><span data-ttu-id="d11d4-137">Using the file connector in your Logic app</span><span class="sxs-lookup"><span data-stu-id="d11d4-137">Using the file connector in your Logic app</span></span>
<span data-ttu-id="d11d4-138">Once your API app is created, you can now use the file connector as an action for your Logic app.</span><span class="sxs-lookup"><span data-stu-id="d11d4-138">Once your API app is created, you can now use the file connector as an action for your Logic app.</span></span> <span data-ttu-id="d11d4-139">To do this, you need to:</span><span class="sxs-lookup"><span data-stu-id="d11d4-139">To do this, you need to:</span></span>

1. <span data-ttu-id="d11d4-140">Create a new Logic app and choose the same resource group which has the file connector.</span><span class="sxs-lookup"><span data-stu-id="d11d4-140">Create a new Logic app and choose the same resource group which has the file connector.</span></span> <span data-ttu-id="d11d4-141">Follow instructions to [Create a new Logic app].</span><span class="sxs-lookup"><span data-stu-id="d11d4-141">Follow instructions to [Create a new Logic app].</span></span>
2. <span data-ttu-id="d11d4-142">Open “Triggers and Actions” within the created Logic app to open the Logic App Designer and configure your flow.</span><span class="sxs-lookup"><span data-stu-id="d11d4-142">Open “Triggers and Actions” within the created Logic app to open the Logic App Designer and configure your flow.</span></span>
3. <span data-ttu-id="d11d4-143">The file connector would appear in the “API Apps in this resource group” section in the gallery on the right hand side.</span><span class="sxs-lookup"><span data-stu-id="d11d4-143">The file connector would appear in the “API Apps in this resource group” section in the gallery on the right hand side.</span></span>
4. <span data-ttu-id="d11d4-144">You can drop the file connector API app into the editor by clicking on the “file connector”.</span><span class="sxs-lookup"><span data-stu-id="d11d4-144">You can drop the file connector API app into the editor by clicking on the “file connector”.</span></span> <span data-ttu-id="d11d4-145">file connector exposes one trigger and 4 Actions:</span><span class="sxs-lookup"><span data-stu-id="d11d4-145">file connector exposes one trigger and 4 Actions:</span></span>  
   ![][5]
5. <span data-ttu-id="d11d4-146">Each one of these exposes certain properties.</span><span class="sxs-lookup"><span data-stu-id="d11d4-146">Each one of these exposes certain properties.</span></span> <span data-ttu-id="d11d4-147">The image below lists the properties for the trigger and Get file Action:</span><span class="sxs-lookup"><span data-stu-id="d11d4-147">The image below lists the properties for the trigger and Get file Action:</span></span>  
   ![][6]
6. <span data-ttu-id="d11d4-148">Once these are configured, the Trigger and Action can be used in your flow.</span><span class="sxs-lookup"><span data-stu-id="d11d4-148">Once these are configured, the Trigger and Action can be used in your flow.</span></span> <span data-ttu-id="d11d4-149">Similarly, other actions can be configured as well.</span><span class="sxs-lookup"><span data-stu-id="d11d4-149">Similarly, other actions can be configured as well.</span></span>

> [!NOTE]
> <span data-ttu-id="d11d4-150">The file trigger will delete the file after it is successfully read from the folder.</span><span class="sxs-lookup"><span data-stu-id="d11d4-150">The file trigger will delete the file after it is successfully read from the folder.</span></span>
>
>

## <a name="file-connector-rest-apis"></a><span data-ttu-id="d11d4-151">File connector REST APIs</span><span class="sxs-lookup"><span data-stu-id="d11d4-151">File connector REST APIs</span></span>
<span data-ttu-id="d11d4-152">To use the connector outside of a Logic app, the REST APIs exposed by the connector can be leveraged.</span><span class="sxs-lookup"><span data-stu-id="d11d4-152">To use the connector outside of a Logic app, the REST APIs exposed by the connector can be leveraged.</span></span> <span data-ttu-id="d11d4-153">You can view this API Definitions using Browse->Api App->file connector.</span><span class="sxs-lookup"><span data-stu-id="d11d4-153">You can view this API Definitions using Browse->Api App->file connector.</span></span> <span data-ttu-id="d11d4-154">Now click on the API Definition lens under the Summary Section to view all the APIs exposed by this connector:</span><span class="sxs-lookup"><span data-stu-id="d11d4-154">Now click on the API Definition lens under the Summary Section to view all the APIs exposed by this connector:</span></span>  
![][7]

<span data-ttu-id="d11d4-155">Details of the APIs can be found at [file connector API definition].</span><span class="sxs-lookup"><span data-stu-id="d11d4-155">Details of the APIs can be found at [file connector API definition].</span></span>

## <a name="do-more-with-your-connector"></a><span data-ttu-id="d11d4-156">Do more with your connector</span><span class="sxs-lookup"><span data-stu-id="d11d4-156">Do more with your connector</span></span>
<span data-ttu-id="d11d4-157">Now that the connector is created, you can add it to a business workflow using a Logic app.</span><span class="sxs-lookup"><span data-stu-id="d11d4-157">Now that the connector is created, you can add it to a business workflow using a Logic app.</span></span> <span data-ttu-id="d11d4-158">See [What are Logic apps?](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d11d4-158">See [What are Logic apps?](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span>

> [!NOTE]
> <span data-ttu-id="d11d4-159">If you want to get started with Azure Logic apps before signing up for an Azure account, go to [Try Logic app](https://azure.microsoft.com/try/app-service/logic/), where you can immediately create a short-lived starter Logic app in App Service.</span><span class="sxs-lookup"><span data-stu-id="d11d4-159">If you want to get started with Azure Logic apps before signing up for an Azure account, go to [Try Logic app](https://azure.microsoft.com/try/app-service/logic/), where you can immediately create a short-lived starter Logic app in App Service.</span></span> <span data-ttu-id="d11d4-160">No credit cards required; no commitments.</span><span class="sxs-lookup"><span data-stu-id="d11d4-160">No credit cards required; no commitments.</span></span>
>
>

<span data-ttu-id="d11d4-161">View the Swagger REST API reference at [Connectors and API Apps Reference](http://go.microsoft.com/fwlink/p/?LinkId=529766).</span><span class="sxs-lookup"><span data-stu-id="d11d4-161">View the Swagger REST API reference at [Connectors and API Apps Reference](http://go.microsoft.com/fwlink/p/?LinkId=529766).</span></span>

<span data-ttu-id="d11d4-162">You can also review performance statistics and control security to the connector.</span><span class="sxs-lookup"><span data-stu-id="d11d4-162">You can also review performance statistics and control security to the connector.</span></span> <span data-ttu-id="d11d4-163">See [Monitor your Logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="d11d4-163">See [Monitor your Logic apps](../logic-apps/logic-apps-monitor-your-logic-apps.md).</span></span>

<!-- Image reference -->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-logic/media/app-service-logic-connector-file/img1.PNG
[5]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-logic/media/app-service-logic-connector-file/img5.PNG
[6]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-logic/media/app-service-logic-connector-file/img6.PNG
[7]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/app-service-logic/media/app-service-logic-connector-file/img7.PNG

<!-- Links -->
[Create a new Logic app]: app-service-logic-create-a-logic-app.md
[File connector API definition]: https://msdn.microsoft.com/library/dn936296.aspx
[Using the Hybrid Connection Manager]: ../app-service-web/web-sites-hybrid-connection-get-started.md




