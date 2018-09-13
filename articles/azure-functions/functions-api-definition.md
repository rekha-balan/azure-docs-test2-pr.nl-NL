---
title: OpenAPI metadata in Azure Functions | Microsoft Docs
description: Overview of OpenAPI support in Azure Functions
services: functions
author: alexkarcher-msft
manager: jeconnoc
ms.assetid: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: 68077e576fe3451627d8a5c8e1ff1b26d06d96b7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44774026"
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a><span data-ttu-id="cfe6e-103">OpenAPI 2.0 metadata support in Azure Functions (preview)</span><span class="sxs-lookup"><span data-stu-id="cfe6e-103">OpenAPI 2.0 metadata support in Azure Functions (preview)</span></span>
<span data-ttu-id="cfe6e-104">OpenAPI 2.0 (formerly Swagger) metadata support in Azure Functions is a preview feature that you can use to write an OpenAPI 2.0 definition inside a function app.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-104">OpenAPI 2.0 (formerly Swagger) metadata support in Azure Functions is a preview feature that you can use to write an OpenAPI 2.0 definition inside a function app.</span></span> <span data-ttu-id="cfe6e-105">You can then host that file by using the function app.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-105">You can then host that file by using the function app.</span></span>

<span data-ttu-id="cfe6e-106">[OpenAPI metadata](http://swagger.io/) allows a function that's hosting a REST API to be consumed by a wide variety of other software.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-106">[OpenAPI metadata](http://swagger.io/) allows a function that's hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="cfe6e-107">This software includes Microsoft offerings like PowerApps and the [API Apps feature of Azure App Service](../app-service/app-service-web-overview.md), third-party developer tools like [Postman](https://www.getpostman.com/docs/importing_swagger), and [many more packages](http://swagger.io/tools/).</span><span class="sxs-lookup"><span data-stu-id="cfe6e-107">This software includes Microsoft offerings like PowerApps and the [API Apps feature of Azure App Service](../app-service/app-service-web-overview.md), third-party developer tools like [Postman](https://www.getpostman.com/docs/importing_swagger), and [many more packages](http://swagger.io/tools/).</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

>[!TIP]
><span data-ttu-id="cfe6e-108">We recommend starting with the [getting started tutorial](./functions-api-definition-getting-started.md) and then returning to this document to learn more about specific features.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-108">We recommend starting with the [getting started tutorial](./functions-api-definition-getting-started.md) and then returning to this document to learn more about specific features.</span></span>

## <a name="enable"></a><span data-ttu-id="cfe6e-109">Enable OpenAPI definition support</span><span class="sxs-lookup"><span data-stu-id="cfe6e-109">Enable OpenAPI definition support</span></span>
<span data-ttu-id="cfe6e-110">You can configure all OpenAPI settings on the **API Definition** page in your function app's **Platform features**.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-110">You can configure all OpenAPI settings on the **API Definition** page in your function app's **Platform features**.</span></span>

> [!NOTE]
> <span data-ttu-id="cfe6e-111">Function API definition feature is not supported for beta runtime currently.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-111">Function API definition feature is not supported for beta runtime currently.</span></span>

<span data-ttu-id="cfe6e-112">To enable the generation of a hosted OpenAPI definition and a quickstart definition, set **API definition source** to **Function (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-112">To enable the generation of a hosted OpenAPI definition and a quickstart definition, set **API definition source** to **Function (Preview)**.</span></span> <span data-ttu-id="cfe6e-113">**External URL** allows your function to use an OpenAPI definition that's hosted elsewhere.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-113">**External URL** allows your function to use an OpenAPI definition that's hosted elsewhere.</span></span>

## <a name="generate-definition"></a><span data-ttu-id="cfe6e-114">Generate a Swagger skeleton from your function's metadata</span><span class="sxs-lookup"><span data-stu-id="cfe6e-114">Generate a Swagger skeleton from your function's metadata</span></span>
<span data-ttu-id="cfe6e-115">A template can help you start writing your first OpenAPI definition.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-115">A template can help you start writing your first OpenAPI definition.</span></span> <span data-ttu-id="cfe6e-116">The definition template feature creates a sparse OpenAPI definition by using all the metadata in the function.json file for each of your HTTP trigger functions.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-116">The definition template feature creates a sparse OpenAPI definition by using all the metadata in the function.json file for each of your HTTP trigger functions.</span></span> <span data-ttu-id="cfe6e-117">You'll need to fill in more information about your API from the [OpenAPI specification](http://swagger.io/specification/), such as request and response templates.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-117">You'll need to fill in more information about your API from the [OpenAPI specification](http://swagger.io/specification/), such as request and response templates.</span></span>

<span data-ttu-id="cfe6e-118">For step-by-step instructions, see the [getting started tutorial](./functions-api-definition-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="cfe6e-118">For step-by-step instructions, see the [getting started tutorial](./functions-api-definition-getting-started.md).</span></span>

### <a name="templates"></a><span data-ttu-id="cfe6e-119">Available templates</span><span class="sxs-lookup"><span data-stu-id="cfe6e-119">Available templates</span></span>

|<span data-ttu-id="cfe6e-120">Name</span><span class="sxs-lookup"><span data-stu-id="cfe6e-120">Name</span></span>| <span data-ttu-id="cfe6e-121">Description</span><span class="sxs-lookup"><span data-stu-id="cfe6e-121">Description</span></span> |
|:-----|:-----|
|<span data-ttu-id="cfe6e-122">Generated Definition</span><span class="sxs-lookup"><span data-stu-id="cfe6e-122">Generated Definition</span></span>|<span data-ttu-id="cfe6e-123">An OpenAPI definition with the maximum amount of information that can be inferred from the function's existing metadata.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-123">An OpenAPI definition with the maximum amount of information that can be inferred from the function's existing metadata.</span></span>|

### <a name="quickstart-details"></a><span data-ttu-id="cfe6e-124">Included metadata in the generated definition</span><span class="sxs-lookup"><span data-stu-id="cfe6e-124">Included metadata in the generated definition</span></span>

<span data-ttu-id="cfe6e-125">The following table represents the Azure portal settings and corresponding data in function.json as it is mapped to the generated Swagger skeleton.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-125">The following table represents the Azure portal settings and corresponding data in function.json as it is mapped to the generated Swagger skeleton.</span></span>

|<span data-ttu-id="cfe6e-126">Swagger.json</span><span class="sxs-lookup"><span data-stu-id="cfe6e-126">Swagger.json</span></span>|<span data-ttu-id="cfe6e-127">Portal UI</span><span class="sxs-lookup"><span data-stu-id="cfe6e-127">Portal UI</span></span>|<span data-ttu-id="cfe6e-128">Function.json</span><span class="sxs-lookup"><span data-stu-id="cfe6e-128">Function.json</span></span>|
|:----|:-----|:-----|
|[<span data-ttu-id="cfe6e-129">Host</span><span class="sxs-lookup"><span data-stu-id="cfe6e-129">Host</span></span>](http://swagger.io/specification/#fixed-fields-15)|<span data-ttu-id="cfe6e-130">**Function app settings** > **App Service settings** > **Overview** > **URL**</span><span class="sxs-lookup"><span data-stu-id="cfe6e-130">**Function app settings** > **App Service settings** > **Overview** > **URL**</span></span>|<span data-ttu-id="cfe6e-131">*Not present*</span><span class="sxs-lookup"><span data-stu-id="cfe6e-131">*Not present*</span></span>
|[<span data-ttu-id="cfe6e-132">Paths</span><span class="sxs-lookup"><span data-stu-id="cfe6e-132">Paths</span></span>](http://swagger.io/specification/#paths-object-29)|<span data-ttu-id="cfe6e-133">**Integrate** > **Selected HTTP methods**</span><span class="sxs-lookup"><span data-stu-id="cfe6e-133">**Integrate** > **Selected HTTP methods**</span></span>|<span data-ttu-id="cfe6e-134">Bindings: Route</span><span class="sxs-lookup"><span data-stu-id="cfe6e-134">Bindings: Route</span></span>
|[<span data-ttu-id="cfe6e-135">Path Item</span><span class="sxs-lookup"><span data-stu-id="cfe6e-135">Path Item</span></span>](http://swagger.io/specification/#path-item-object-32)|<span data-ttu-id="cfe6e-136">**Integrate** > **Route template**</span><span class="sxs-lookup"><span data-stu-id="cfe6e-136">**Integrate** > **Route template**</span></span>|<span data-ttu-id="cfe6e-137">Bindings: Methods</span><span class="sxs-lookup"><span data-stu-id="cfe6e-137">Bindings: Methods</span></span>
|[<span data-ttu-id="cfe6e-138">Security</span><span class="sxs-lookup"><span data-stu-id="cfe6e-138">Security</span></span>](http://swagger.io/specification/#security-scheme-object-112)|<span data-ttu-id="cfe6e-139">**Keys**</span><span class="sxs-lookup"><span data-stu-id="cfe6e-139">**Keys**</span></span>|<span data-ttu-id="cfe6e-140">*Not present*</span><span class="sxs-lookup"><span data-stu-id="cfe6e-140">*Not present*</span></span>|
|<span data-ttu-id="cfe6e-141">operationID\*</span><span class="sxs-lookup"><span data-stu-id="cfe6e-141">operationID\*</span></span>|<span data-ttu-id="cfe6e-142">**Route + Allowed verbs**</span><span class="sxs-lookup"><span data-stu-id="cfe6e-142">**Route + Allowed verbs**</span></span>|<span data-ttu-id="cfe6e-143">Route + Allowed Verbs</span><span class="sxs-lookup"><span data-stu-id="cfe6e-143">Route + Allowed Verbs</span></span>|

<span data-ttu-id="cfe6e-144">\*The operation ID is required only for integrating with PowerApps and Flow.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-144">\*The operation ID is required only for integrating with PowerApps and Flow.</span></span>
> [!NOTE]
> <span data-ttu-id="cfe6e-145">The x-ms-summary extension provides a display name in Logic Apps, PowerApps, and Flow.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-145">The x-ms-summary extension provides a display name in Logic Apps, PowerApps, and Flow.</span></span>
>
> <span data-ttu-id="cfe6e-146">To learn more, see [Customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).</span><span class="sxs-lookup"><span data-stu-id="cfe6e-146">To learn more, see [Customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/).</span></span>

## <a name="CICD"></a><span data-ttu-id="cfe6e-147">Use CI/CD to set an API definition</span><span class="sxs-lookup"><span data-stu-id="cfe6e-147">Use CI/CD to set an API definition</span></span>

 <span data-ttu-id="cfe6e-148">You must enable API definition hosting in the portal before you enable source control to modify your API definition from source control.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-148">You must enable API definition hosting in the portal before you enable source control to modify your API definition from source control.</span></span> <span data-ttu-id="cfe6e-149">Follow these instructions:</span><span class="sxs-lookup"><span data-stu-id="cfe6e-149">Follow these instructions:</span></span>

1. <span data-ttu-id="cfe6e-150">Browse to **API Definition (preview)** in your function app settings.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-150">Browse to **API Definition (preview)** in your function app settings.</span></span>
  1. <span data-ttu-id="cfe6e-151">Set **API definition source** to **Function**.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-151">Set **API definition source** to **Function**.</span></span>
  1. <span data-ttu-id="cfe6e-152">Click **Generate API definition template** and then **Save** to create a template definition for modifying later.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-152">Click **Generate API definition template** and then **Save** to create a template definition for modifying later.</span></span>
  1. <span data-ttu-id="cfe6e-153">Note your API definition URL and key.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-153">Note your API definition URL and key.</span></span>
1. <span data-ttu-id="cfe6e-154">[Set up continuous integration/continuous deployment (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).</span><span class="sxs-lookup"><span data-stu-id="cfe6e-154">[Set up continuous integration/continuous deployment (CI/CD)](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements).</span></span>
2. <span data-ttu-id="cfe6e-155">Modify swagger.json in source control at \site\wwwroot\.azurefunctions\swagger\swagger.json.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-155">Modify swagger.json in source control at \site\wwwroot\.azurefunctions\swagger\swagger.json.</span></span>

<span data-ttu-id="cfe6e-156">Now, changes to swagger.json in your repository are hosted by your function app at the API definition URL and key that you noted in step 1.c.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-156">Now, changes to swagger.json in your repository are hosted by your function app at the API definition URL and key that you noted in step 1.c.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfe6e-157">Next steps</span><span class="sxs-lookup"><span data-stu-id="cfe6e-157">Next steps</span></span>
* <span data-ttu-id="cfe6e-158">[Getting started tutorial](functions-api-definition-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="cfe6e-158">[Getting started tutorial](functions-api-definition-getting-started.md).</span></span> <span data-ttu-id="cfe6e-159">Try our walkthrough to see an OpenAPI definition in action.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-159">Try our walkthrough to see an OpenAPI definition in action.</span></span>
* <span data-ttu-id="cfe6e-160">[Azure Functions GitHub repository](https://github.com/Azure/Azure-Functions/).</span><span class="sxs-lookup"><span data-stu-id="cfe6e-160">[Azure Functions GitHub repository](https://github.com/Azure/Azure-Functions/).</span></span> <span data-ttu-id="cfe6e-161">Check out the Functions repository to give us feedback on the API definition support preview.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-161">Check out the Functions repository to give us feedback on the API definition support preview.</span></span> <span data-ttu-id="cfe6e-162">Make a GitHub issue for anything you want to see updated.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-162">Make a GitHub issue for anything you want to see updated.</span></span>
* <span data-ttu-id="cfe6e-163">[Azure Functions developer reference](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="cfe6e-163">[Azure Functions developer reference](functions-reference.md).</span></span> <span data-ttu-id="cfe6e-164">Learn about coding functions and defining triggers and bindings.</span><span class="sxs-lookup"><span data-stu-id="cfe6e-164">Learn about coding functions and defining triggers and bindings.</span></span>
