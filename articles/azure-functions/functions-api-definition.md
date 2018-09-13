---
title: OpenAPI Metadata in Azure Functions | Microsoft Docs
description: Overview of OpenAPI support in Azure Functions
services: functions
documentationcenter: ''
author: alexkarcher-msft
manager: erikre
editor: ''
ms.assetid: ''
ms.service: functions
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 03/23/2017
ms.author: alkarche
ms.openlocfilehash: 08063960d3956ca65dd32d9fe726c366799a2087
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549432"
---
# <a name="openapi-20-metadata-support-in-azure-functions-preview"></a><span data-ttu-id="13078-103">OpenAPI 2.0 Metadata support in Azure Functions (Preview)</span><span class="sxs-lookup"><span data-stu-id="13078-103">OpenAPI 2.0 Metadata support in Azure Functions (Preview)</span></span>
<span data-ttu-id="13078-104">This preview feature allows you to write an OpenAPI 2.0 (formerly Swagger) definition inside a Function App, and host that file using the Function App.</span><span class="sxs-lookup"><span data-stu-id="13078-104">This preview feature allows you to write an OpenAPI 2.0 (formerly Swagger) definition inside a Function App, and host that file using the Function App.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-metadata"></a><span data-ttu-id="13078-105">What is OpenAPI metadata?</span><span class="sxs-lookup"><span data-stu-id="13078-105">What is OpenAPI metadata?</span></span>
<span data-ttu-id="13078-106">[OpenAPI Metadata](http://swagger.io/) allows a function hosting a REST API to be consumed by a wide variety of other software.</span><span class="sxs-lookup"><span data-stu-id="13078-106">[OpenAPI Metadata](http://swagger.io/) allows a function hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="13078-107">From 1st party offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), to 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger), and [many more packages](http://swagger.io/tools/).</span><span class="sxs-lookup"><span data-stu-id="13078-107">From 1st party offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), to 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger), and [many more packages](http://swagger.io/tools/).</span></span>

>[!TIP]
><span data-ttu-id="13078-108">We recommend starting with the [getting started tutorial](./functions-api-definition-getting-started.md) and then returning to this document to learn more about specific features.</span><span class="sxs-lookup"><span data-stu-id="13078-108">We recommend starting with the [getting started tutorial](./functions-api-definition-getting-started.md) and then returning to this document to learn more about specific features.</span></span>

## <a name="enable"></a><span data-ttu-id="13078-109">Enabling OpenAPI definition Support</span><span class="sxs-lookup"><span data-stu-id="13078-109">Enabling OpenAPI definition Support</span></span>
* <span data-ttu-id="13078-110">All OpenAPI settings can be configured in the `API Definition (preview)` page in your Function App settings.</span><span class="sxs-lookup"><span data-stu-id="13078-110">All OpenAPI settings can be configured in the `API Definition (preview)` page in your Function App settings.</span></span>
* <span data-ttu-id="13078-111">Set `API defintion source` to `Function` to enable a hosted OpenAPI definition and quickstart definition generation.</span><span class="sxs-lookup"><span data-stu-id="13078-111">Set `API defintion source` to `Function` to enable a hosted OpenAPI definition and quickstart definition generation.</span></span>
  * <span data-ttu-id="13078-112">`External URL` allows your Function to use an OpenAPI definition that is hosted elsewhere.</span><span class="sxs-lookup"><span data-stu-id="13078-112">`External URL` allows your Function to use an OpenAPI definition that is hosted elsewhere.</span></span>

## <a name="generate-defintion"></a><span data-ttu-id="13078-113">Generate a Swagger Skeleton from your Function Metadata</span><span class="sxs-lookup"><span data-stu-id="13078-113">Generate a Swagger Skeleton from your Function Metadata</span></span>
<span data-ttu-id="13078-114">A template is an awesome way to get started writing your first OpenAPI definition.</span><span class="sxs-lookup"><span data-stu-id="13078-114">A template is an awesome way to get started writing your first OpenAPI definition.</span></span> <span data-ttu-id="13078-115">The definition template feature creates a sparse OpenAPI definition using all the metadata in the function.json for each of your HTTP trigger functions.</span><span class="sxs-lookup"><span data-stu-id="13078-115">The definition template feature creates a sparse OpenAPI definition using all the metadata in the function.json for each of your HTTP trigger functions.</span></span> <span data-ttu-id="13078-116">**You will need to fill in more information about your API from the [OpenAPI specification](http://swagger.io/specification/), such as request and response templates.**</span><span class="sxs-lookup"><span data-stu-id="13078-116">**You will need to fill in more information about your API from the [OpenAPI specification](http://swagger.io/specification/), such as request and response templates.**</span></span>

[<span data-ttu-id="13078-117">Check out this getting started tutorial for step by step instructions</span><span class="sxs-lookup"><span data-stu-id="13078-117">Check out this getting started tutorial for step by step instructions</span></span>](./functions-api-definition-getting-started.md)

### <a name="templates"></a><span data-ttu-id="13078-118">Available templates</span><span class="sxs-lookup"><span data-stu-id="13078-118">Available templates</span></span>

|<span data-ttu-id="13078-119">Name</span><span class="sxs-lookup"><span data-stu-id="13078-119">Name</span></span>| <span data-ttu-id="13078-120">Description</span><span class="sxs-lookup"><span data-stu-id="13078-120">Description</span></span> |
|:-----|:-----|
|<span data-ttu-id="13078-121">Generated Definition</span><span class="sxs-lookup"><span data-stu-id="13078-121">Generated Definition</span></span>|<span data-ttu-id="13078-122">An OpenAPI definition with the maximum amount of information that can be inferred from the Function's existing metadata</span><span class="sxs-lookup"><span data-stu-id="13078-122">An OpenAPI definition with the maximum amount of information that can be inferred from the Function's existing metadata</span></span>|

### <a name="quickstart-details"></a><span data-ttu-id="13078-123">Included Metadata in Generated Definition</span><span class="sxs-lookup"><span data-stu-id="13078-123">Included Metadata in Generated Definition</span></span>

<span data-ttu-id="13078-124">The following table represents the portal settings and corresponding data in function.json as it is mapped to the generated skeleton Swagger.</span><span class="sxs-lookup"><span data-stu-id="13078-124">The following table represents the portal settings and corresponding data in function.json as it is mapped to the generated skeleton Swagger.</span></span>

|<span data-ttu-id="13078-125">Swagger.json</span><span class="sxs-lookup"><span data-stu-id="13078-125">Swagger.json</span></span>|<span data-ttu-id="13078-126">Portal UI</span><span class="sxs-lookup"><span data-stu-id="13078-126">Portal UI</span></span>|<span data-ttu-id="13078-127">Function.json</span><span class="sxs-lookup"><span data-stu-id="13078-127">Function.json</span></span>|
|:----|:-----|:-----|
|[<span data-ttu-id="13078-128">Host</span><span class="sxs-lookup"><span data-stu-id="13078-128">Host</span></span>](http://swagger.io/specification/#fixed-fields-15)|`Function app settings` > `Go to App Service Settings` > `Overview` > `URL`|<span data-ttu-id="13078-129">*not present*</span><span class="sxs-lookup"><span data-stu-id="13078-129">*not present*</span></span>
|[<span data-ttu-id="13078-130">Paths</span><span class="sxs-lookup"><span data-stu-id="13078-130">Paths</span></span>](http://swagger.io/specification/#paths-object-29)|`Integrate` > `Selected HTTP methods`|<span data-ttu-id="13078-131">Bindings: Route</span><span class="sxs-lookup"><span data-stu-id="13078-131">Bindings: Route</span></span>
|[<span data-ttu-id="13078-132">Path Item</span><span class="sxs-lookup"><span data-stu-id="13078-132">Path Item</span></span>](http://swagger.io/specification/#path-item-object-32)|`Integrate` > `Route template`|<span data-ttu-id="13078-133">Bindings: Methods</span><span class="sxs-lookup"><span data-stu-id="13078-133">Bindings: Methods</span></span>
|[<span data-ttu-id="13078-134">Security</span><span class="sxs-lookup"><span data-stu-id="13078-134">Security</span></span>](http://swagger.io/specification/#security-scheme-object-112)|<span data-ttu-id="13078-135">Keys</span><span class="sxs-lookup"><span data-stu-id="13078-135">Keys</span></span>|<span data-ttu-id="13078-136">*not present*</span><span class="sxs-lookup"><span data-stu-id="13078-136">*not present*</span></span>|
|<span data-ttu-id="13078-137">operationID\*</span><span class="sxs-lookup"><span data-stu-id="13078-137">operationID\*</span></span>|<span data-ttu-id="13078-138">Route + Allowed verbs</span><span class="sxs-lookup"><span data-stu-id="13078-138">Route + Allowed verbs</span></span>|<span data-ttu-id="13078-139">Route + Allowed Verbs</span><span class="sxs-lookup"><span data-stu-id="13078-139">Route + Allowed Verbs</span></span>|

<span data-ttu-id="13078-140">\*Operation ID is only required for integrating with PowerApps + Flow</span><span class="sxs-lookup"><span data-stu-id="13078-140">\*Operation ID is only required for integrating with PowerApps + Flow</span></span>
> [!NOTE]
>  <span data-ttu-id="13078-141">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span><span class="sxs-lookup"><span data-stu-id="13078-141">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
>
> <span data-ttu-id="13078-142">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) to learn more.</span><span class="sxs-lookup"><span data-stu-id="13078-142">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) to learn more.</span></span>

## <a name="CICD"></a><span data-ttu-id="13078-143">Using CI/CD to set an API Definition</span><span class="sxs-lookup"><span data-stu-id="13078-143">Using CI/CD to set an API Definition</span></span>

 <span data-ttu-id="13078-144">You must enable API Definition hosting in the portal before enabling source control to modify your API Definition from source control.</span><span class="sxs-lookup"><span data-stu-id="13078-144">You must enable API Definition hosting in the portal before enabling source control to modify your API Definition from source control.</span></span> <span data-ttu-id="13078-145">Follow the instructions below.</span><span class="sxs-lookup"><span data-stu-id="13078-145">Follow the instructions below.</span></span>

1. <span data-ttu-id="13078-146">Navigate to `API Definition (preview)` in your Function App settings.</span><span class="sxs-lookup"><span data-stu-id="13078-146">Navigate to `API Definition (preview)` in your Function App settings.</span></span>
  1. <span data-ttu-id="13078-147">Set `API definition source` to `Function`</span><span class="sxs-lookup"><span data-stu-id="13078-147">Set `API definition source` to `Function`</span></span>
  1. <span data-ttu-id="13078-148">Click `Generate API definition template` then `Save` to create a template definition for modifying later.</span><span class="sxs-lookup"><span data-stu-id="13078-148">Click `Generate API definition template` then `Save` to create a template definition for modifying later.</span></span>
  1. <span data-ttu-id="13078-149">Note your `API definition URL` and `key`</span><span class="sxs-lookup"><span data-stu-id="13078-149">Note your `API definition URL` and `key`</span></span>
1. [<span data-ttu-id="13078-150">Set up CI/CD</span><span class="sxs-lookup"><span data-stu-id="13078-150">Set up CI/CD</span></span>](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment#continuous-deployment-requirements)
2. <span data-ttu-id="13078-151">Modify your `swagger.json` in source control at `\site\wwwroot\.azurefunctions\swagger\swagger.json`</span><span class="sxs-lookup"><span data-stu-id="13078-151">Modify your `swagger.json` in source control at `\site\wwwroot\.azurefunctions\swagger\swagger.json`</span></span>

<span data-ttu-id="13078-152">Now changes to `swagger.json` in your repository are hosted by your Function App at the `API definition URL` and `key` noted in step 1.3</span><span class="sxs-lookup"><span data-stu-id="13078-152">Now changes to `swagger.json` in your repository are hosted by your Function App at the `API definition URL` and `key` noted in step 1.3</span></span>

## <a name="next-steps"></a><span data-ttu-id="13078-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="13078-153">Next steps</span></span>
* [<span data-ttu-id="13078-154">Getting started tutorial</span><span class="sxs-lookup"><span data-stu-id="13078-154">Getting started tutorial</span></span>](functions-api-definition-getting-started.md)
  * <span data-ttu-id="13078-155">Try our walkthrough to see an OpenAPI definition in action!</span><span class="sxs-lookup"><span data-stu-id="13078-155">Try our walkthrough to see an OpenAPI definition in action!</span></span>
* [<span data-ttu-id="13078-156">Azure Functions Github repository</span><span class="sxs-lookup"><span data-stu-id="13078-156">Azure Functions Github repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="13078-157">Check out the Functions Github to give us feedback on the API definition support preview!</span><span class="sxs-lookup"><span data-stu-id="13078-157">Check out the Functions Github to give us feedback on the API definition support preview!</span></span> <span data-ttu-id="13078-158">Make a github issue for anything you'd like to see updated.</span><span class="sxs-lookup"><span data-stu-id="13078-158">Make a github issue for anything you'd like to see updated.</span></span>
* [<span data-ttu-id="13078-159">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="13078-159">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="13078-160">Programmer reference for coding functions and defining triggers and bindings.</span><span class="sxs-lookup"><span data-stu-id="13078-160">Programmer reference for coding functions and defining triggers and bindings.</span></span>
