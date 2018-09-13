---
title: Create an OpenAPI definition for a function | Microsoft Docs
description: Create an OpenAPI definition that enables other apps and services to call your function in Azure.
services: functions
keywords: OpenAPI, Swagger, cloud apps, cloud services,
author: ggailey777
manager: jeconnoc
ms.assetid: ''
ms.service: azure-functions
ms.topic: tutorial
ms.date: 12/15/2017
ms.author: glenga
ms.reviewer: sunayv
ms.custom: mvc, cc996988-fb4f-47
ms.openlocfilehash: f2f4e7d96c4d8725d9d34314854665440d86ce8d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858132"
---
# <a name="create-an-openapi-definition-for-a-function"></a><span data-ttu-id="6a3be-104">Create an OpenAPI definition for a function</span><span class="sxs-lookup"><span data-stu-id="6a3be-104">Create an OpenAPI definition for a function</span></span>
<span data-ttu-id="6a3be-105">REST APIs are often described using an OpenAPI definition (formerly known as a [Swagger](http://swagger.io/) file).</span><span class="sxs-lookup"><span data-stu-id="6a3be-105">REST APIs are often described using an OpenAPI definition (formerly known as a [Swagger](http://swagger.io/) file).</span></span> <span data-ttu-id="6a3be-106">This definition contains information about what operations are available in an API and how the request and response data for the API should be structured.</span><span class="sxs-lookup"><span data-stu-id="6a3be-106">This definition contains information about what operations are available in an API and how the request and response data for the API should be structured.</span></span>

<span data-ttu-id="6a3be-107">In this tutorial, you create a function that determines whether an emergency repair on a wind turbine is cost-effective.</span><span class="sxs-lookup"><span data-stu-id="6a3be-107">In this tutorial, you create a function that determines whether an emergency repair on a wind turbine is cost-effective.</span></span> <span data-ttu-id="6a3be-108">You then create an OpenAPI definition for the function app so that the function can be called from other apps and services.</span><span class="sxs-lookup"><span data-stu-id="6a3be-108">You then create an OpenAPI definition for the function app so that the function can be called from other apps and services.</span></span>

<span data-ttu-id="6a3be-109">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="6a3be-109">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6a3be-110">Create a function in Azure</span><span class="sxs-lookup"><span data-stu-id="6a3be-110">Create a function in Azure</span></span>
> * <span data-ttu-id="6a3be-111">Generate an OpenAPI definition using OpenAPI tools</span><span class="sxs-lookup"><span data-stu-id="6a3be-111">Generate an OpenAPI definition using OpenAPI tools</span></span>
> * <span data-ttu-id="6a3be-112">Modify the definition to provide additional metadata</span><span class="sxs-lookup"><span data-stu-id="6a3be-112">Modify the definition to provide additional metadata</span></span>
> * <span data-ttu-id="6a3be-113">Test the definition by calling the function</span><span class="sxs-lookup"><span data-stu-id="6a3be-113">Test the definition by calling the function</span></span>

## <a name="create-a-function-app"></a><span data-ttu-id="6a3be-114">Create a function app</span><span class="sxs-lookup"><span data-stu-id="6a3be-114">Create a function app</span></span>

<span data-ttu-id="6a3be-115">You must have a function app to host the execution of your functions.</span><span class="sxs-lookup"><span data-stu-id="6a3be-115">You must have a function app to host the execution of your functions.</span></span> <span data-ttu-id="6a3be-116">A function app lets you group functions as a logic unit for easier management, deployment, scaling, and sharing of resources.</span><span class="sxs-lookup"><span data-stu-id="6a3be-116">A function app lets you group functions as a logic unit for easier management, deployment, scaling, and sharing of resources.</span></span> 

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]


## <a name="create-the-function"></a><span data-ttu-id="6a3be-117">Create the function</span><span class="sxs-lookup"><span data-stu-id="6a3be-117">Create the function</span></span>

<span data-ttu-id="6a3be-118">This tutorial uses an HTTP triggered function that takes two parameters: the estimated time to make a turbine repair (in hours); and the capacity of the turbine (in kilowatts).</span><span class="sxs-lookup"><span data-stu-id="6a3be-118">This tutorial uses an HTTP triggered function that takes two parameters: the estimated time to make a turbine repair (in hours); and the capacity of the turbine (in kilowatts).</span></span> <span data-ttu-id="6a3be-119">The function then calculates how much a repair will cost, and how much revenue the turbine could make in a 24 hour period.</span><span class="sxs-lookup"><span data-stu-id="6a3be-119">The function then calculates how much a repair will cost, and how much revenue the turbine could make in a 24 hour period.</span></span>

1. <span data-ttu-id="6a3be-120">Expand your function app and select the **+** button next to **Functions**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-120">Expand your function app and select the **+** button next to **Functions**.</span></span> <span data-ttu-id="6a3be-121">If this is the first function in your function app, select **Custom function**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-121">If this is the first function in your function app, select **Custom function**.</span></span> <span data-ttu-id="6a3be-122">This displays the complete set of function templates.</span><span class="sxs-lookup"><span data-stu-id="6a3be-122">This displays the complete set of function templates.</span></span> 

    ![Functions quickstart page in the Azure portal](media/functions-openapi-definition/add-first-function.png)

2. <span data-ttu-id="6a3be-124">In the search field, type `http` and then choose **C#** for the HTTP trigger template.</span><span class="sxs-lookup"><span data-stu-id="6a3be-124">In the search field, type `http` and then choose **C#** for the HTTP trigger template.</span></span> 
 
    ![Choose the HTTP trigger](./media/functions-openapi-definition/select-http-trigger-portal.png)

3. <span data-ttu-id="6a3be-126">Type `TurbineRepair` for the function **Name**, choose `Function` for **[Authentication level](functions-bindings-http-webhook.md#http-auth)**, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-126">Type `TurbineRepair` for the function **Name**, choose `Function` for **[Authentication level](functions-bindings-http-webhook.md#http-auth)**, and then select **Create**.</span></span>  

    ![Create the HTTP triggered function](./media/functions-openapi-definition/select-http-trigger-portal-2.png)

1. <span data-ttu-id="6a3be-128">Replace the contents of the run.csx file with the following code, then click **Save**:</span><span class="sxs-lookup"><span data-stu-id="6a3be-128">Replace the contents of the run.csx file with the following code, then click **Save**:</span></span>

    ```csharp
    using System.Net;

    const double revenuePerkW = 0.12; 
    const double technicianCost = 250; 
    const double turbineCost = 100;

    public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
    {   

        //Get request body
        dynamic data = await req.Content.ReadAsAsync<object>();
        int hours = data.hours;
        int capacity = data.capacity;

        //Formulas to calculate revenue and cost
        double revenueOpportunity = capacity * revenuePerkW * 24;  
        double costToFix = (hours * technicianCost) +  turbineCost;
        string repairTurbine;

        if (revenueOpportunity > costToFix){
            repairTurbine = "Yes";
        }
        else {
            repairTurbine = "No";
        }

        return req.CreateResponse(HttpStatusCode.OK, new{
            message = repairTurbine,
            revenueOpportunity = "$"+ revenueOpportunity,
            costToFix = "$"+ costToFix         
        }); 
    }
    ```
    <span data-ttu-id="6a3be-129">This function code returns a message of `Yes` or `No` to indicate whether an emergency repair is cost-effective, as well as the revenue opportunity that the turbine represents, and the cost to fix the turbine.</span><span class="sxs-lookup"><span data-stu-id="6a3be-129">This function code returns a message of `Yes` or `No` to indicate whether an emergency repair is cost-effective, as well as the revenue opportunity that the turbine represents, and the cost to fix the turbine.</span></span> 

1. <span data-ttu-id="6a3be-130">To test the function, click **Test** at the far right to expand the test tab. Enter the following value for the **Request body**, and then click **Run**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-130">To test the function, click **Test** at the far right to expand the test tab. Enter the following value for the **Request body**, and then click **Run**.</span></span>

    ```json
    {
    "hours": "6",
    "capacity": "2500"
    }
    ```

    ![Test the function in the Azure portal](media/functions-openapi-definition/test-function.png)

    <span data-ttu-id="6a3be-132">The following value is returned in the body of the response.</span><span class="sxs-lookup"><span data-stu-id="6a3be-132">The following value is returned in the body of the response.</span></span>

    ```json
    {"message":"Yes","revenueOpportunity":"$7200","costToFix":"$1600"}
    ```

<span data-ttu-id="6a3be-133">Now you have a function that determines the cost-effectiveness of emergency repairs.</span><span class="sxs-lookup"><span data-stu-id="6a3be-133">Now you have a function that determines the cost-effectiveness of emergency repairs.</span></span> <span data-ttu-id="6a3be-134">Next, you generate and modify an OpenAPI definition for the function app.</span><span class="sxs-lookup"><span data-stu-id="6a3be-134">Next, you generate and modify an OpenAPI definition for the function app.</span></span>

## <a name="generate-the-openapi-definition"></a><span data-ttu-id="6a3be-135">Generate the OpenAPI definition</span><span class="sxs-lookup"><span data-stu-id="6a3be-135">Generate the OpenAPI definition</span></span>

<span data-ttu-id="6a3be-136">Now you're ready to generate the OpenAPI definition.</span><span class="sxs-lookup"><span data-stu-id="6a3be-136">Now you're ready to generate the OpenAPI definition.</span></span> <span data-ttu-id="6a3be-137">This definition can be used by other Microsoft technologies, like API Apps, [PowerApps](functions-powerapps-scenario.md) and [Microsoft Flow](../azure-functions/app-service-export-api-to-powerapps-and-flow.md), as well as third party developer tools like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/).</span><span class="sxs-lookup"><span data-stu-id="6a3be-137">This definition can be used by other Microsoft technologies, like API Apps, [PowerApps](functions-powerapps-scenario.md) and [Microsoft Flow](../azure-functions/app-service-export-api-to-powerapps-and-flow.md), as well as third party developer tools like [Postman](https://www.getpostman.com/docs/importing_swagger) and [many more packages](http://swagger.io/tools/).</span></span>

1. <span data-ttu-id="6a3be-138">Select only the *verbs* that your API supports (in this case POST).</span><span class="sxs-lookup"><span data-stu-id="6a3be-138">Select only the *verbs* that your API supports (in this case POST).</span></span> <span data-ttu-id="6a3be-139">This makes the generated API definition cleaner.</span><span class="sxs-lookup"><span data-stu-id="6a3be-139">This makes the generated API definition cleaner.</span></span>

    1. <span data-ttu-id="6a3be-140">On the **Integrate** tab of your new HTTP Trigger function, change **Allowed HTTP methods** to **Selected methods**</span><span class="sxs-lookup"><span data-stu-id="6a3be-140">On the **Integrate** tab of your new HTTP Trigger function, change **Allowed HTTP methods** to **Selected methods**</span></span>

    1. <span data-ttu-id="6a3be-141">In **Selected HTTP methods**, clear every option except **POST**, then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-141">In **Selected HTTP methods**, clear every option except **POST**, then click **Save**.</span></span>

        ![Selected HTTP methods](media/functions-openapi-definition/selected-http-methods.png)
        
1. <span data-ttu-id="6a3be-143">Click your function app name (like **function-demo-energy**) > **Platform features** > **API definition**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-143">Click your function app name (like **function-demo-energy**) > **Platform features** > **API definition**.</span></span>

    ![API definition](media/functions-openapi-definition/api-definition.png)

1. <span data-ttu-id="6a3be-145">On the **API definition** tab, click **Function**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-145">On the **API definition** tab, click **Function**.</span></span>

    ![API definition source](media/functions-openapi-definition/api-definition-source.png)

    <span data-ttu-id="6a3be-147">This step enables a suite of OpenAPI options for your function app, including an endpoint to host an OpenAPI file from your function app's domain, an inline copy of the [OpenAPI Editor](http://editor.swagger.io), and an API definition template generator.</span><span class="sxs-lookup"><span data-stu-id="6a3be-147">This step enables a suite of OpenAPI options for your function app, including an endpoint to host an OpenAPI file from your function app's domain, an inline copy of the [OpenAPI Editor](http://editor.swagger.io), and an API definition template generator.</span></span>

1. <span data-ttu-id="6a3be-148">Click **Generate API definition template** > **Save**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-148">Click **Generate API definition template** > **Save**.</span></span>

    ![Generate API definition template](media/functions-openapi-definition/generate-template.png)

    <span data-ttu-id="6a3be-150">Azure scans your function app for HTTP Trigger functions and uses the info in functions.json to generate an OpenAPI definition.</span><span class="sxs-lookup"><span data-stu-id="6a3be-150">Azure scans your function app for HTTP Trigger functions and uses the info in functions.json to generate an OpenAPI definition.</span></span> <span data-ttu-id="6a3be-151">Here's the definition that is generated:</span><span class="sxs-lookup"><span data-stu-id="6a3be-151">Here's the definition that is generated:</span></span>

    ```yaml
    swagger: '2.0'
    info:
    title: function-demo-energy.azurewebsites.net
    version: 1.0.0
    host: function-demo-energy.azurewebsites.net
    basePath: /
    schemes:
    - https
    - http
    paths:
    /api/TurbineRepair:
        post:
        operationId: /api/TurbineRepair/post
        produces: []
        consumes: []
        parameters: []
        description: >-
            Replace with Operation Object
            #http://swagger.io/specification/#operationObject
        responses:
            '200':
            description: Success operation
        security:
            - apikeyQuery: []
    definitions: {}
    securityDefinitions:
    apikeyQuery:
        type: apiKey
        name: code
        in: query
    ```

    <span data-ttu-id="6a3be-152">This definition is described as a _template_ because it requires more metadata to be a full OpenAPI definition.</span><span class="sxs-lookup"><span data-stu-id="6a3be-152">This definition is described as a _template_ because it requires more metadata to be a full OpenAPI definition.</span></span> <span data-ttu-id="6a3be-153">You'll modify the definition in the next step.</span><span class="sxs-lookup"><span data-stu-id="6a3be-153">You'll modify the definition in the next step.</span></span>

## <a name="modify-the-openapi-definition"></a><span data-ttu-id="6a3be-154">Modify the OpenAPI definition</span><span class="sxs-lookup"><span data-stu-id="6a3be-154">Modify the OpenAPI definition</span></span>
<span data-ttu-id="6a3be-155">Now that you have a template definition, you modify it to provide additional metadata about the API's operations and data structures.</span><span class="sxs-lookup"><span data-stu-id="6a3be-155">Now that you have a template definition, you modify it to provide additional metadata about the API's operations and data structures.</span></span> <span data-ttu-id="6a3be-156">In **API definition**, delete the generated definition from `post` to the bottom of the definition, paste in the content below, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-156">In **API definition**, delete the generated definition from `post` to the bottom of the definition, paste in the content below, and click **Save**.</span></span>

```yaml
    post:
      operationId: CalculateCosts
      description: Determines if a technician should be sent for repair
      summary: Calculates costs
      x-ms-summary: Calculates costs
      x-ms-visibility: important
      produces:
        - application/json
      consumes:
        - application/json
      parameters:
        - name: body
          in: body
          description: Hours and capacity used to calculate costs
          x-ms-summary: Hours and capacity
          x-ms-visibility: important
          required: true
          schema:
            type: object
            properties:
              hours:
                description: The amount of effort in hours required to conduct repair
                type: number
                x-ms-summary: Hours
                x-ms-visibility: important
              capacity:
                description: The max output of a turbine in kilowatts
                type: number
                x-ms-summary: Capacity
                x-ms-visibility: important
      responses:
        200:
          description: Message with cost and revenue numbers
          x-ms-summary: Message
          schema:
           type: object
           properties:
            message:
              type: string
              description: Returns Yes or No depending on calculations
              x-ms-summary: Message 
            revenueOpportunity:
              type: string
              description: The revenue opportunity cost
              x-ms-summary: RevenueOpportunity 
            costToFix:
              type: string
              description: The cost in $ to fix the turbine
              x-ms-summary: CostToFix
      security:
        - apikeyQuery: []
definitions: {}
securityDefinitions:
  apikeyQuery:
    type: apiKey
    name: code
    in: query
```

<span data-ttu-id="6a3be-157">In this case you could just paste in updated metadata, but it's important to understand the types of modifications we made to the default template:</span><span class="sxs-lookup"><span data-stu-id="6a3be-157">In this case you could just paste in updated metadata, but it's important to understand the types of modifications we made to the default template:</span></span>

+ <span data-ttu-id="6a3be-158">Specified that the API produces and consumes data in a JSON format.</span><span class="sxs-lookup"><span data-stu-id="6a3be-158">Specified that the API produces and consumes data in a JSON format.</span></span>

+ <span data-ttu-id="6a3be-159">Specified the required parameters, with their names and data types.</span><span class="sxs-lookup"><span data-stu-id="6a3be-159">Specified the required parameters, with their names and data types.</span></span>

+ <span data-ttu-id="6a3be-160">Specified the return values for a successful response, with their names and data types.</span><span class="sxs-lookup"><span data-stu-id="6a3be-160">Specified the return values for a successful response, with their names and data types.</span></span>

+ <span data-ttu-id="6a3be-161">Provided friendly summaries and descriptions for the API, and its operations and parameters.</span><span class="sxs-lookup"><span data-stu-id="6a3be-161">Provided friendly summaries and descriptions for the API, and its operations and parameters.</span></span> <span data-ttu-id="6a3be-162">This is important for people who will use this function.</span><span class="sxs-lookup"><span data-stu-id="6a3be-162">This is important for people who will use this function.</span></span>

+ <span data-ttu-id="6a3be-163">Added x-ms-summary and x-ms-visibility, which are used in the UI for Microsoft Flow and Logic Apps.</span><span class="sxs-lookup"><span data-stu-id="6a3be-163">Added x-ms-summary and x-ms-visibility, which are used in the UI for Microsoft Flow and Logic Apps.</span></span> <span data-ttu-id="6a3be-164">For more information, see [OpenAPI extensions for custom APIs in Microsoft Flow](https://preview.flow.microsoft.com/documentation/customapi-how-to-swagger/).</span><span class="sxs-lookup"><span data-stu-id="6a3be-164">For more information, see [OpenAPI extensions for custom APIs in Microsoft Flow](https://preview.flow.microsoft.com/documentation/customapi-how-to-swagger/).</span></span>

> [!NOTE]
> <span data-ttu-id="6a3be-165">We left the security definition with the default authentication method of API key.</span><span class="sxs-lookup"><span data-stu-id="6a3be-165">We left the security definition with the default authentication method of API key.</span></span> <span data-ttu-id="6a3be-166">You would change this section of the definition if you used a different type of authentication.</span><span class="sxs-lookup"><span data-stu-id="6a3be-166">You would change this section of the definition if you used a different type of authentication.</span></span>

<span data-ttu-id="6a3be-167">For more information about defining API operations, see the [Open API specification](https://swagger.io/specification/#operationObject).</span><span class="sxs-lookup"><span data-stu-id="6a3be-167">For more information about defining API operations, see the [Open API specification](https://swagger.io/specification/#operationObject).</span></span>

## <a name="test-the-openapi-definition"></a><span data-ttu-id="6a3be-168">Test the OpenAPI definition</span><span class="sxs-lookup"><span data-stu-id="6a3be-168">Test the OpenAPI definition</span></span>
<span data-ttu-id="6a3be-169">Before you use the API definition, it's a good idea to test it in the Azure Functions UI.</span><span class="sxs-lookup"><span data-stu-id="6a3be-169">Before you use the API definition, it's a good idea to test it in the Azure Functions UI.</span></span>

1. <span data-ttu-id="6a3be-170">On the **Manage** tab of your function, under **Host Keys**, copy the **default** key.</span><span class="sxs-lookup"><span data-stu-id="6a3be-170">On the **Manage** tab of your function, under **Host Keys**, copy the **default** key.</span></span>

    ![Copy API key](media/functions-openapi-definition/copy-api-key.png)

    > [!NOTE]
    ><span data-ttu-id="6a3be-172">You use this key for testing, and you also use it when you call the API from an app or service.</span><span class="sxs-lookup"><span data-stu-id="6a3be-172">You use this key for testing, and you also use it when you call the API from an app or service.</span></span>

1. <span data-ttu-id="6a3be-173">Go back to the API definition: **function-demo-energy** > **Platform features** > **API definition**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-173">Go back to the API definition: **function-demo-energy** > **Platform features** > **API definition**.</span></span>

1. <span data-ttu-id="6a3be-174">In the right pane, click **Authenticate**, enter the API key that you copied, and click **Authenticate**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-174">In the right pane, click **Authenticate**, enter the API key that you copied, and click **Authenticate**.</span></span>

    ![Authenticate with API key](media/functions-openapi-definition/authenticate-api-key.png)

1. <span data-ttu-id="6a3be-176">Scroll down and click **Try this operation**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-176">Scroll down and click **Try this operation**.</span></span>

    ![Try this operation](media/functions-openapi-definition/try-operation.png)

1. <span data-ttu-id="6a3be-178">Enter values for **hours** and **capacity**.</span><span class="sxs-lookup"><span data-stu-id="6a3be-178">Enter values for **hours** and **capacity**.</span></span>

    ![Enter parameters](media/functions-openapi-definition/parameters.png)

    <span data-ttu-id="6a3be-180">Notice how the UI uses the descriptions from the API definition.</span><span class="sxs-lookup"><span data-stu-id="6a3be-180">Notice how the UI uses the descriptions from the API definition.</span></span>

1. <span data-ttu-id="6a3be-181">Click **Send Request**, then click the **Pretty** tab to see the output.</span><span class="sxs-lookup"><span data-stu-id="6a3be-181">Click **Send Request**, then click the **Pretty** tab to see the output.</span></span>

    ![Send a request](media/functions-openapi-definition/send-request.png)

## <a name="next-steps"></a><span data-ttu-id="6a3be-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="6a3be-183">Next steps</span></span>

<span data-ttu-id="6a3be-184">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="6a3be-184">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6a3be-185">Create a function in Azure</span><span class="sxs-lookup"><span data-stu-id="6a3be-185">Create a function in Azure</span></span>
> * <span data-ttu-id="6a3be-186">Generate an OpenAPI definition using OpenAPI tools</span><span class="sxs-lookup"><span data-stu-id="6a3be-186">Generate an OpenAPI definition using OpenAPI tools</span></span>
> * <span data-ttu-id="6a3be-187">Modify the definition to provide additional metadata</span><span class="sxs-lookup"><span data-stu-id="6a3be-187">Modify the definition to provide additional metadata</span></span>
> * <span data-ttu-id="6a3be-188">Test the definition by calling the function</span><span class="sxs-lookup"><span data-stu-id="6a3be-188">Test the definition by calling the function</span></span>

<span data-ttu-id="6a3be-189">Advance to the next topic to learn how to create a PowerApps app that uses the OpenAPI definition you created.</span><span class="sxs-lookup"><span data-stu-id="6a3be-189">Advance to the next topic to learn how to create a PowerApps app that uses the OpenAPI definition you created.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6a3be-190">Call a function from PowerApps</span><span class="sxs-lookup"><span data-stu-id="6a3be-190">Call a function from PowerApps</span></span>](functions-powerapps-scenario.md)
