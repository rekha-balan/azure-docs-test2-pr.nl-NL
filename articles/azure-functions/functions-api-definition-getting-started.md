---
title: Getting Started with OpenAPI Metadata in Azure Functions | Microsoft Docs
description: Getting Started with OpenAPI support in Azure Functions
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
ms.openlocfilehash: 9ba17bc9fee0a89bbe45ad7db3e527aedc7b1fd0
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564061"
---
# <a name="creating-openapi-20-swagger-metadata-for-a-function-app-preview"></a><span data-ttu-id="5fa81-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span><span class="sxs-lookup"><span data-stu-id="5fa81-103">Creating OpenAPI 2.0 (Swagger) Metadata for a Function App (Preview)</span></span>

<span data-ttu-id="5fa81-104">This document guides you through the step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span><span class="sxs-lookup"><span data-stu-id="5fa81-104">This document guides you through the step by step process of creating an OpenAPI Definition for a simple API hosted on Azure Functions.</span></span>

[!INCLUDE [intro](../../includes/functions-bindings-intro.md)]

### <a name="what-is-openapi-swagger"></a><span data-ttu-id="5fa81-105">What is OpenAPI (Swagger)?</span><span class="sxs-lookup"><span data-stu-id="5fa81-105">What is OpenAPI (Swagger)?</span></span>
<span data-ttu-id="5fa81-106">[Swagger Metadata](http://swagger.io/) is a file that defines the functionality and operating modes of your API, and allows a function hosting a REST API to be consumed by a wide variety of other software.</span><span class="sxs-lookup"><span data-stu-id="5fa81-106">[Swagger Metadata](http://swagger.io/) is a file that defines the functionality and operating modes of your API, and allows a function hosting a REST API to be consumed by a wide variety of other software.</span></span> <span data-ttu-id="5fa81-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API to be consumed with a Swagger definition.</span><span class="sxs-lookup"><span data-stu-id="5fa81-107">Microsoft offerings like PowerApps and [API Apps](https://docs.microsoft.com/azure/app-service-api/app-service-api-dotnet-get-started#a-idcodegena-generate-client-code-for-the-data-tier), as well as 3rd party developer tooling like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/) all allow your API to be consumed with a Swagger definition.</span></span>

## <a name="prepare-function"></a><span data-ttu-id="5fa81-108">Creating a Function with a simple API</span><span class="sxs-lookup"><span data-stu-id="5fa81-108">Creating a Function with a simple API</span></span>
  <span data-ttu-id="5fa81-109">To create an OpenAPI definition, we first need to create a Function with a simple API.</span><span class="sxs-lookup"><span data-stu-id="5fa81-109">To create an OpenAPI definition, we first need to create a Function with a simple API.</span></span> <span data-ttu-id="5fa81-110">If you already have an API hosted on a Function App, you can skip straight to the next section</span><span class="sxs-lookup"><span data-stu-id="5fa81-110">If you already have an API hosted on a Function App, you can skip straight to the next section</span></span>
1. <span data-ttu-id="5fa81-111">Create a new Function App.</span><span class="sxs-lookup"><span data-stu-id="5fa81-111">Create a new Function App.</span></span>
  1. <span data-ttu-id="5fa81-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span><span class="sxs-lookup"><span data-stu-id="5fa81-112">[Azure portal](https://portal.azure.com) > `+ New` > Search for "Function App"</span></span>
1. <span data-ttu-id="5fa81-113">Create a new HTTP trigger function inside your new Function App</span><span class="sxs-lookup"><span data-stu-id="5fa81-113">Create a new HTTP trigger function inside your new Function App</span></span>
  1. <span data-ttu-id="5fa81-114">Your function is pre-populated with code defining a very simple REST API.</span><span class="sxs-lookup"><span data-stu-id="5fa81-114">Your function is pre-populated with code defining a very simple REST API.</span></span>
  1. <span data-ttu-id="5fa81-115">Any string passed to the Function as a query parameter or in the body is returned as "Hello {input}"</span><span class="sxs-lookup"><span data-stu-id="5fa81-115">Any string passed to the Function as a query parameter or in the body is returned as "Hello {input}"</span></span>
1. <span data-ttu-id="5fa81-116">Go to the `Integrate` tab of your new HTTP Trigger function</span><span class="sxs-lookup"><span data-stu-id="5fa81-116">Go to the `Integrate` tab of your new HTTP Trigger function</span></span>
  1. <span data-ttu-id="5fa81-117">Toggle `Allowed HTTP methods` to `Selected methods`</span><span class="sxs-lookup"><span data-stu-id="5fa81-117">Toggle `Allowed HTTP methods` to `Selected methods`</span></span>
  1. <span data-ttu-id="5fa81-118">In `Selected HTTP methods` uncheck every verb except POST.</span><span class="sxs-lookup"><span data-stu-id="5fa81-118">In `Selected HTTP methods` uncheck every verb except POST.</span></span>
    <span data-ttu-id="5fa81-119">![Selected HTTP Methods](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/selectedHTTPmethods.PNG)</span><span class="sxs-lookup"><span data-stu-id="5fa81-119">![Selected HTTP Methods](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/selectedHTTPmethods.PNG)</span></span>
  1. <span data-ttu-id="5fa81-120">This step will simplify your API definition later on.</span><span class="sxs-lookup"><span data-stu-id="5fa81-120">This step will simplify your API definition later on.</span></span>

## <a name="enable"></a><span data-ttu-id="5fa81-121">Enabling API Definition Support</span><span class="sxs-lookup"><span data-stu-id="5fa81-121">Enabling API Definition Support</span></span>
1. <span data-ttu-id="5fa81-122">Navigate to `your function name` > `API Definition (preview)`</span><span class="sxs-lookup"><span data-stu-id="5fa81-122">Navigate to `your function name` > `API Definition (preview)`</span></span>
1. <span data-ttu-id="5fa81-123">Set `API Definition Source` to `Internal`</span><span class="sxs-lookup"><span data-stu-id="5fa81-123">Set `API Definition Source` to `Internal`</span></span>
  1. <span data-ttu-id="5fa81-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint to host an OpenAPI file from your Function App's domain, an inline copy of the [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span><span class="sxs-lookup"><span data-stu-id="5fa81-124">This step enables a suite of OpenAPI options for your Function App, including an endpoint to host an OpenAPI file from your Function App's domain, an inline copy of the [OpenAPI Editor](http://editor.swagger.io), and a quickstart definition generator.</span></span>
<span data-ttu-id="5fa81-125">![Enabled Definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/enabledefinition.PNG)</span><span class="sxs-lookup"><span data-stu-id="5fa81-125">![Enabled Definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/enabledefinition.PNG)</span></span>

## <a name="create-definition"></a><span data-ttu-id="5fa81-126">Creating your API Definition from a template</span><span class="sxs-lookup"><span data-stu-id="5fa81-126">Creating your API Definition from a template</span></span>
1. <span data-ttu-id="5fa81-127">Click `Generate API Definition template`</span><span class="sxs-lookup"><span data-stu-id="5fa81-127">Click `Generate API Definition template`</span></span>
  1. <span data-ttu-id="5fa81-128">This step scans your Function App for HTTP Trigger functions and uses the info in functions.json to generate an OpenAPI document.</span><span class="sxs-lookup"><span data-stu-id="5fa81-128">This step scans your Function App for HTTP Trigger functions and uses the info in functions.json to generate an OpenAPI document.</span></span>
2. <span data-ttu-id="5fa81-129">Add an operation object to `paths: /api/yourfunctionroute post:`</span><span class="sxs-lookup"><span data-stu-id="5fa81-129">Add an operation object to `paths: /api/yourfunctionroute post:`</span></span>
  1. <span data-ttu-id="5fa81-130">The quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata to be a full OpenAPI definition, such as operation objects and response templates.</span><span class="sxs-lookup"><span data-stu-id="5fa81-130">The quickstart OpenAPI document is an outline of a full OpenAPI doc. It requires more metadata to be a full OpenAPI definition, such as operation objects and response templates.</span></span>
  1. <span data-ttu-id="5fa81-131">The sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span><span class="sxs-lookup"><span data-stu-id="5fa81-131">The sample operation object below has a filled out produces/consumes section, a parameter object, and a response object.</span></span>
  
  ```yaml
      post:
        operationId: /api/yourfunctionroute/post
        consumes: [application/json]
        produces: [application/json]
        parameters:
          - name: name
            in: body
            description: Your name
            x-ms-summary: Your name
            required: true
            schema:
              type: object
              properties:
                name:
                  type: string
        description: >-
          Replace with Operation Object
          #http://swagger.io/specification/#operationObject
        responses:
          '200':
            description: A Greeting
            x-ms-summary: Your name
            schema:
              type: string
        security:
          - apikeyQuery: []
  ```

> [!NOTE]
>  <span data-ttu-id="5fa81-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span><span class="sxs-lookup"><span data-stu-id="5fa81-132">x-ms-summary provides a display name in Logic Apps, Flow, and PowerApps.</span></span>
>
> <span data-ttu-id="5fa81-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) to learn more.</span><span class="sxs-lookup"><span data-stu-id="5fa81-133">Check out [customize your Swagger definition for PowerApps](https://powerapps.microsoft.com/tutorials/customapi-how-to-swagger/) to learn more.</span></span>

3. <span data-ttu-id="5fa81-134">Click `save` to save your changes ![Adding Template Definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/addingtemplate.png)</span><span class="sxs-lookup"><span data-stu-id="5fa81-134">Click `save` to save your changes ![Adding Template Definition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/addingtemplate.png)</span></span>

## <a name="use-definition"></a><span data-ttu-id="5fa81-135">Using Your API Definition</span><span class="sxs-lookup"><span data-stu-id="5fa81-135">Using Your API Definition</span></span>
1. <span data-ttu-id="5fa81-136">Copy your `API definition URL` and paste it into a new browser tab to view your raw OpenAPI document.</span><span class="sxs-lookup"><span data-stu-id="5fa81-136">Copy your `API definition URL` and paste it into a new browser tab to view your raw OpenAPI document.</span></span>
1. <span data-ttu-id="5fa81-137">You can import your OpenAPI document to any number of tools for testing and integration using that URL.</span><span class="sxs-lookup"><span data-stu-id="5fa81-137">You can import your OpenAPI document to any number of tools for testing and integration using that URL.</span></span>
  1. <span data-ttu-id="5fa81-138">Many Azure resources are able to automatically import your OpenAPI doc using the API Definition URL that is saved in your Function application settings.</span><span class="sxs-lookup"><span data-stu-id="5fa81-138">Many Azure resources are able to automatically import your OpenAPI doc using the API Definition URL that is saved in your Function application settings.</span></span> <span data-ttu-id="5fa81-139">As a part of the `Function` API definition source, we update that url for you.</span><span class="sxs-lookup"><span data-stu-id="5fa81-139">As a part of the `Function` API definition source, we update that url for you.</span></span>


## <a name="test-definition"></a><span data-ttu-id="5fa81-140">Using the Swagger UI to test your API definition</span><span class="sxs-lookup"><span data-stu-id="5fa81-140">Using the Swagger UI to test your API definition</span></span>
<span data-ttu-id="5fa81-141">There are testing tools built in to the UI view of the imbedded API definition editor.</span><span class="sxs-lookup"><span data-stu-id="5fa81-141">There are testing tools built in to the UI view of the imbedded API definition editor.</span></span> <span data-ttu-id="5fa81-142">Add your API key, and then use the `Try this operation` button under each method.</span><span class="sxs-lookup"><span data-stu-id="5fa81-142">Add your API key, and then use the `Try this operation` button under each method.</span></span> <span data-ttu-id="5fa81-143">The tool will use your API Definition to format the requests and successful responses will indicate that your definition is correct.</span><span class="sxs-lookup"><span data-stu-id="5fa81-143">The tool will use your API Definition to format the requests and successful responses will indicate that your definition is correct.</span></span>

### <a name="steps"></a><span data-ttu-id="5fa81-144">Steps:</span><span class="sxs-lookup"><span data-stu-id="5fa81-144">Steps:</span></span>

1. <span data-ttu-id="5fa81-145">Copy your function API key</span><span class="sxs-lookup"><span data-stu-id="5fa81-145">Copy your function API key</span></span>
  1. <span data-ttu-id="5fa81-146">The API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
  ![Function key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/functionkey.png)</span><span class="sxs-lookup"><span data-stu-id="5fa81-146">The API key can be found in your HTTP Trigger Function under `function name` > `Keys` > `Function Keys`
![Function key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/functionkey.png)</span></span>
1. <span data-ttu-id="5fa81-147">Navigate to the `API Definition (preview)` page.</span><span class="sxs-lookup"><span data-stu-id="5fa81-147">Navigate to the `API Definition (preview)` page.</span></span>
  1. <span data-ttu-id="5fa81-148">Click `Authenticate` and add your Function API key to the security object at the top.</span><span class="sxs-lookup"><span data-stu-id="5fa81-148">Click `Authenticate` and add your Function API key to the security object at the top.</span></span>
  <span data-ttu-id="5fa81-149">![OpenAPI key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/definitionTest auth.png)</span><span class="sxs-lookup"><span data-stu-id="5fa81-149">![OpenAPI key](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/definitionTest auth.png)</span></span>
1. <span data-ttu-id="5fa81-150">select `/api/yourfunctionroute` > `POST`</span><span class="sxs-lookup"><span data-stu-id="5fa81-150">select `/api/yourfunctionroute` > `POST`</span></span>
1. <span data-ttu-id="5fa81-151">Click `Try it out` and enter a name to test</span><span class="sxs-lookup"><span data-stu-id="5fa81-151">Click `Try it out` and enter a name to test</span></span>
1. <span data-ttu-id="5fa81-152">You should see a SUCCESS result under `Pretty`
![API Definition test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/definitionTest.png)</span><span class="sxs-lookup"><span data-stu-id="5fa81-152">You should see a SUCCESS result under `Pretty`
![API Definition test](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-functions/media/functions-api-definition-getting-started/definitionTest.png)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5fa81-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="5fa81-153">Next steps</span></span>
* [<span data-ttu-id="5fa81-154">OpenAPI Definition in Functions Overview</span><span class="sxs-lookup"><span data-stu-id="5fa81-154">OpenAPI Definition in Functions Overview</span></span>](functions-api-definition.md)
  * <span data-ttu-id="5fa81-155">Read the full documentation for more info on OpenAPI support.</span><span class="sxs-lookup"><span data-stu-id="5fa81-155">Read the full documentation for more info on OpenAPI support.</span></span>
* [<span data-ttu-id="5fa81-156">Azure Functions developer reference</span><span class="sxs-lookup"><span data-stu-id="5fa81-156">Azure Functions developer reference</span></span>](functions-reference.md)  
  * <span data-ttu-id="5fa81-157">Programmer reference for coding functions and defining triggers and bindings.</span><span class="sxs-lookup"><span data-stu-id="5fa81-157">Programmer reference for coding functions and defining triggers and bindings.</span></span>
* [<span data-ttu-id="5fa81-158">Azure Functions Github repository</span><span class="sxs-lookup"><span data-stu-id="5fa81-158">Azure Functions Github repository</span></span>](https://github.com/Azure/Azure-Functions/)
  * <span data-ttu-id="5fa81-159">Check out the Functions Github to give us feedback on the API definition support preview!</span><span class="sxs-lookup"><span data-stu-id="5fa81-159">Check out the Functions Github to give us feedback on the API definition support preview!</span></span> <span data-ttu-id="5fa81-160">Make a github issue for anything you'd like to see updated.</span><span class="sxs-lookup"><span data-stu-id="5fa81-160">Make a github issue for anything you'd like to see updated.</span></span>






