---
title: Testing Azure Functions | Microsoft Docs
description: Test your Azure functions by using Postman, cURL, and Node.js.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
keywords: azure functions, functions, event processing, webhooks, dynamic compute, serverless architecture, testing
ms.assetid: c00f3082-30d2-46b3-96ea-34faf2f15f77
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 02/02/2017
ms.author: glenga
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 1aa1c3a3c0dd4985662b5ceb4acd7250cf2d0186
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44818290"
---
# <a name="strategies-for-testing-your-code-in-azure-functions"></a><span data-ttu-id="8658e-104">Strategies for testing your code in Azure Functions</span><span class="sxs-lookup"><span data-stu-id="8658e-104">Strategies for testing your code in Azure Functions</span></span>

<span data-ttu-id="8658e-105">This topic demonstrates the various ways to test functions, including using the following general approaches:</span><span class="sxs-lookup"><span data-stu-id="8658e-105">This topic demonstrates the various ways to test functions, including using the following general approaches:</span></span>

+ <span data-ttu-id="8658e-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span><span class="sxs-lookup"><span data-stu-id="8658e-106">HTTP-based tools, such as cURL, Postman, and even a web browser for web-based triggers</span></span>
+ <span data-ttu-id="8658e-107">Azure Storage Explorer, to test Azure Storage-based triggers</span><span class="sxs-lookup"><span data-stu-id="8658e-107">Azure Storage Explorer, to test Azure Storage-based triggers</span></span>
+ <span data-ttu-id="8658e-108">Test tab in the Azure Functions portal</span><span class="sxs-lookup"><span data-stu-id="8658e-108">Test tab in the Azure Functions portal</span></span>
+ <span data-ttu-id="8658e-109">Timer-triggered function</span><span class="sxs-lookup"><span data-stu-id="8658e-109">Timer-triggered function</span></span>
+ <span data-ttu-id="8658e-110">Testing application or framework</span><span class="sxs-lookup"><span data-stu-id="8658e-110">Testing application or framework</span></span>

<span data-ttu-id="8658e-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or the request body.</span><span class="sxs-lookup"><span data-stu-id="8658e-111">All these testing methods use an HTTP trigger function that accepts input through either a query string parameter or the request body.</span></span> <span data-ttu-id="8658e-112">You create this function using the Azure portal in the first section.</span><span class="sxs-lookup"><span data-stu-id="8658e-112">You create this function using the Azure portal in the first section.</span></span>

## <a name="create-a-simple-function-for-testing-using-the-azure-portal"></a><span data-ttu-id="8658e-113">Create a simple function for testing using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="8658e-113">Create a simple function for testing using the Azure portal</span></span>
<span data-ttu-id="8658e-114">For most of this tutorial, we use a slightly modified version of the HttpTrigger JavaScript function template that is available when you create a function.</span><span class="sxs-lookup"><span data-stu-id="8658e-114">For most of this tutorial, we use a slightly modified version of the HttpTrigger JavaScript function template that is available when you create a function.</span></span> <span data-ttu-id="8658e-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span><span class="sxs-lookup"><span data-stu-id="8658e-115">If you need help creating a function, review this [tutorial](functions-create-first-azure-function.md).</span></span> <span data-ttu-id="8658e-116">Choose the **HttpTrigger- JavaScript** template when creating the test function in the [Azure portal].</span><span class="sxs-lookup"><span data-stu-id="8658e-116">Choose the **HttpTrigger- JavaScript** template when creating the test function in the [Azure portal].</span></span>

<span data-ttu-id="8658e-117">The default function template is basically a "hello world" function that echoes back the name from the request body or query string parameter, `name=<your name>`.</span><span class="sxs-lookup"><span data-stu-id="8658e-117">The default function template is basically a "hello world" function that echoes back the name from the request body or query string parameter, `name=<your name>`.</span></span>  <span data-ttu-id="8658e-118">We'll update the code to also allow you to provide the name and an address as JSON content in the request body.</span><span class="sxs-lookup"><span data-stu-id="8658e-118">We'll update the code to also allow you to provide the name and an address as JSON content in the request body.</span></span> <span data-ttu-id="8658e-119">Then the function echoes these back to the client when available.</span><span class="sxs-lookup"><span data-stu-id="8658e-119">Then the function echoes these back to the client when available.</span></span>   

<span data-ttu-id="8658e-120">Update the function with the following code, which we will use for testing:</span><span class="sxs-lookup"><span data-stu-id="8658e-120">Update the function with the following code, which we will use for testing:</span></span>

```javascript
module.exports = function (context, req) {
    context.log("HTTP trigger function processed a request. RequestUri=%s", req.originalUrl);
    context.log("Request Headers = " + JSON.stringify(req.headers));
    var res;

    if (req.query.name || (req.body && req.body.name)) {
        if (typeof req.query.name != "undefined") {
            context.log("Name was provided as a query string param...");
            res = ProcessNewUserInformation(context, req.query.name);
        }
        else {
            context.log("Processing user info from request body...");
            res = ProcessNewUserInformation(context, req.body.name, req.body.address);
        }
    }
    else {
        res = {
            status: 400,
            body: "Please pass a name on the query string or in the request body"
        };
    }
    context.done(null, res);
};
function ProcessNewUserInformation(context, name, address) {
    context.log("Processing user information...");
    context.log("name = " + name);
    var echoString = "Hello " + name;
    var res;

    if (typeof address != "undefined") {
        echoString += "\n" + "The address you provided is " + address;
        context.log("address = " + address);
    }
    res = {
        // status: 200, /* Defaults to 200 */
        body: echoString
    };
    return res;
}
```

## <a name="test-a-function-with-tools"></a><span data-ttu-id="8658e-121">Test a function with tools</span><span class="sxs-lookup"><span data-stu-id="8658e-121">Test a function with tools</span></span>
<span data-ttu-id="8658e-122">Outside the Azure portal, there are various tools that you can use to trigger your functions for testing.</span><span class="sxs-lookup"><span data-stu-id="8658e-122">Outside the Azure portal, there are various tools that you can use to trigger your functions for testing.</span></span> <span data-ttu-id="8658e-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span><span class="sxs-lookup"><span data-stu-id="8658e-123">These include HTTP testing tools (both UI-based and command line), Azure Storage access tools, and even a simple web browser.</span></span>

### <a name="test-with-a-browser"></a><span data-ttu-id="8658e-124">Test with a browser</span><span class="sxs-lookup"><span data-stu-id="8658e-124">Test with a browser</span></span>
<span data-ttu-id="8658e-125">The web browser is a simple way to trigger functions via HTTP.</span><span class="sxs-lookup"><span data-stu-id="8658e-125">The web browser is a simple way to trigger functions via HTTP.</span></span> <span data-ttu-id="8658e-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span><span class="sxs-lookup"><span data-stu-id="8658e-126">You can use a browser for GET requests that do not require a body payload, and that use only query string parameters.</span></span>

<span data-ttu-id="8658e-127">To test the function we defined earlier, copy the **Function Url** from the portal.</span><span class="sxs-lookup"><span data-stu-id="8658e-127">To test the function we defined earlier, copy the **Function Url** from the portal.</span></span> <span data-ttu-id="8658e-128">It has the following form:</span><span class="sxs-lookup"><span data-stu-id="8658e-128">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="8658e-129">Append the `name` parameter to the query string.</span><span class="sxs-lookup"><span data-stu-id="8658e-129">Append the `name` parameter to the query string.</span></span> <span data-ttu-id="8658e-130">Use an actual name for the `<Enter a name here>` placeholder.</span><span class="sxs-lookup"><span data-stu-id="8658e-130">Use an actual name for the `<Enter a name here>` placeholder.</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>&name=<Enter a name here>

<span data-ttu-id="8658e-131">Paste the URL into your browser, and you should get a response similar to the following.</span><span class="sxs-lookup"><span data-stu-id="8658e-131">Paste the URL into your browser, and you should get a response similar to the following.</span></span>

![Screenshot of Chrome browser tab with test response](./media/functions-test-a-function/browser-test.png)

<span data-ttu-id="8658e-133">This example is the Chrome browser, which wraps the returned string in XML.</span><span class="sxs-lookup"><span data-stu-id="8658e-133">This example is the Chrome browser, which wraps the returned string in XML.</span></span> <span data-ttu-id="8658e-134">Other browsers display just the string value.</span><span class="sxs-lookup"><span data-stu-id="8658e-134">Other browsers display just the string value.</span></span>

<span data-ttu-id="8658e-135">In the portal **Logs** window, output similar to the following is logged in executing the function:</span><span class="sxs-lookup"><span data-stu-id="8658e-135">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T07:34:59  Welcome, you are now connected to log-streaming service.
    2016-03-23T07:35:09.195 Function started (Id=61a8c5a9-5e44-4da0-909d-91d293f20445)
    2016-03-23T07:35:10.338 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==&name=Glenn from a browser
    2016-03-23T07:35:10.338 Request Headers = {"cache-control":"max-age=0","connection":"Keep-Alive","accept":"text/html","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T07:35:10.338 Name was provided as a query string param.
    2016-03-23T07:35:10.338 Processing User Information...
    2016-03-23T07:35:10.369 Function completed (Success, Id=61a8c5a9-5e44-4da0-909d-91d293f20445)

### <a name="test-with-postman"></a><span data-ttu-id="8658e-136">Test with Postman</span><span class="sxs-lookup"><span data-stu-id="8658e-136">Test with Postman</span></span>
<span data-ttu-id="8658e-137">The recommended tool to test most of your functions is Postman, which integrates with the Chrome browser.</span><span class="sxs-lookup"><span data-stu-id="8658e-137">The recommended tool to test most of your functions is Postman, which integrates with the Chrome browser.</span></span> <span data-ttu-id="8658e-138">To install Postman, see [Get Postman](https://www.getpostman.com/).</span><span class="sxs-lookup"><span data-stu-id="8658e-138">To install Postman, see [Get Postman](https://www.getpostman.com/).</span></span> <span data-ttu-id="8658e-139">Postman provides control over many more attributes of an HTTP request.</span><span class="sxs-lookup"><span data-stu-id="8658e-139">Postman provides control over many more attributes of an HTTP request.</span></span>

> [!TIP]
> <span data-ttu-id="8658e-140">Use the HTTP testing tool that you are most comfortable with.</span><span class="sxs-lookup"><span data-stu-id="8658e-140">Use the HTTP testing tool that you are most comfortable with.</span></span> <span data-ttu-id="8658e-141">Here are some alternatives to Postman:</span><span class="sxs-lookup"><span data-stu-id="8658e-141">Here are some alternatives to Postman:</span></span>  
>
> * [<span data-ttu-id="8658e-142">Fiddler</span><span class="sxs-lookup"><span data-stu-id="8658e-142">Fiddler</span></span>](http://www.telerik.com/fiddler)  
> * [<span data-ttu-id="8658e-143">Paw</span><span class="sxs-lookup"><span data-stu-id="8658e-143">Paw</span></span>](https://luckymarmot.com/paw)  
>
>

<span data-ttu-id="8658e-144">To test the function with a request body in Postman:</span><span class="sxs-lookup"><span data-stu-id="8658e-144">To test the function with a request body in Postman:</span></span>

1. <span data-ttu-id="8658e-145">Start Postman from the **Apps** button in the upper-left corner of a Chrome browser window.</span><span class="sxs-lookup"><span data-stu-id="8658e-145">Start Postman from the **Apps** button in the upper-left corner of a Chrome browser window.</span></span>
2. <span data-ttu-id="8658e-146">Copy your **Function Url**, and paste it into Postman.</span><span class="sxs-lookup"><span data-stu-id="8658e-146">Copy your **Function Url**, and paste it into Postman.</span></span> <span data-ttu-id="8658e-147">It includes the access code query string parameter.</span><span class="sxs-lookup"><span data-stu-id="8658e-147">It includes the access code query string parameter.</span></span>
3. <span data-ttu-id="8658e-148">Change the HTTP method to **POST**.</span><span class="sxs-lookup"><span data-stu-id="8658e-148">Change the HTTP method to **POST**.</span></span>
4. <span data-ttu-id="8658e-149">Click **Body** > **raw**, and add a JSON request body similar to the following:</span><span class="sxs-lookup"><span data-stu-id="8658e-149">Click **Body** > **raw**, and add a JSON request body similar to the following:</span></span>

    ```json
    {
        "name" : "Wes testing with Postman",
        "address" : "Seattle, WA 98101"
    }
    ```
5. <span data-ttu-id="8658e-150">Click **Send**.</span><span class="sxs-lookup"><span data-stu-id="8658e-150">Click **Send**.</span></span>

<span data-ttu-id="8658e-151">The following image shows testing the simple echo function example in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="8658e-151">The following image shows testing the simple echo function example in this tutorial.</span></span>

![Screenshot of Postman user interface](./media/functions-test-a-function/postman-test.png)

<span data-ttu-id="8658e-153">In the portal **Logs** window, output similar to the following is logged in executing the function:</span><span class="sxs-lookup"><span data-stu-id="8658e-153">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:04:51  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:04:57.107 Function started (Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)
    2016-03-23T08:04:57.763 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/WesmcHttpTriggerNodeJS1?code=XXXXXXXXXX==
    2016-03-23T08:04:57.763 Request Headers = {"cache-control":"no-cache","connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:04:57.763 Processing user info from request body...
    2016-03-23T08:04:57.763 Processing User Information...
    2016-03-23T08:04:57.763 name = Wes testing with Postman
    2016-03-23T08:04:57.763 address = Seattle, W.A. 98101
    2016-03-23T08:04:57.795 Function completed (Success, Id=dc5db8b1-6f1c-4117-b5c4-f6b602d538f7)

### <a name="test-with-curl-from-the-command-line"></a><span data-ttu-id="8658e-154">Test with cURL from the command line</span><span class="sxs-lookup"><span data-stu-id="8658e-154">Test with cURL from the command line</span></span>
<span data-ttu-id="8658e-155">Often when you're testing software, it's not necessary to look any further than the command line to help debug your application.</span><span class="sxs-lookup"><span data-stu-id="8658e-155">Often when you're testing software, it's not necessary to look any further than the command line to help debug your application.</span></span> <span data-ttu-id="8658e-156">This is no different with testing functions.</span><span class="sxs-lookup"><span data-stu-id="8658e-156">This is no different with testing functions.</span></span> <span data-ttu-id="8658e-157">Note that the cURL is available by default on Linux-based systems.</span><span class="sxs-lookup"><span data-stu-id="8658e-157">Note that the cURL is available by default on Linux-based systems.</span></span> <span data-ttu-id="8658e-158">On Windows, you must first download and install the [cURL tool](https://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="8658e-158">On Windows, you must first download and install the [cURL tool](https://curl.haxx.se/).</span></span>

<span data-ttu-id="8658e-159">To test the function that we defined earlier, copy the **Function URL** from the portal.</span><span class="sxs-lookup"><span data-stu-id="8658e-159">To test the function that we defined earlier, copy the **Function URL** from the portal.</span></span> <span data-ttu-id="8658e-160">It has the following form:</span><span class="sxs-lookup"><span data-stu-id="8658e-160">It has the following form:</span></span>

    https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="8658e-161">This is the URL for triggering your function.</span><span class="sxs-lookup"><span data-stu-id="8658e-161">This is the URL for triggering your function.</span></span> <span data-ttu-id="8658e-162">Test this by using the cURL command on the command line to make a GET (`-G` or `--get`) request against the function:</span><span class="sxs-lookup"><span data-stu-id="8658e-162">Test this by using the cURL command on the command line to make a GET (`-G` or `--get`) request against the function:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code>

<span data-ttu-id="8658e-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in the cURL command:</span><span class="sxs-lookup"><span data-stu-id="8658e-163">This particular example requires a query string parameter, which can be passed as Data (`-d`) in the cURL command:</span></span>

    curl -G https://<Your Function App>.azurewebsites.net/api/<Your Function Name>?code=<your access code> -d name=<Enter a name here>

<span data-ttu-id="8658e-164">Run the command, and you see the following output of the function on the command line:</span><span class="sxs-lookup"><span data-stu-id="8658e-164">Run the command, and you see the following output of the function on the command line:</span></span>

![Screenshot of Command Prompt output](./media/functions-test-a-function/curl-test.png)

<span data-ttu-id="8658e-166">In the portal **Logs** window, output similar to the following is logged in executing the function:</span><span class="sxs-lookup"><span data-stu-id="8658e-166">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-04-05T21:55:09  Welcome, you are now connected to log-streaming service.
    2016-04-05T21:55:30.738 Function started (Id=ae6955da-29db-401a-b706-482fcd1b8f7a)
    2016-04-05T21:55:30.738 Node.js HTTP trigger function processed a request. RequestUri=https://functionsExample.azurewebsites.net/api/HttpTriggerNodeJS1?code=XXXXXXX&name=Azure Functions
    2016-04-05T21:55:30.738 Function completed (Success, Id=ae6955da-29db-401a-b706-482fcd1b8f7a)

### <a name="test-a-blob-trigger-by-using-storage-explorer"></a><span data-ttu-id="8658e-167">Test a blob trigger by using Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="8658e-167">Test a blob trigger by using Storage Explorer</span></span>
<span data-ttu-id="8658e-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="8658e-168">You can test a blob trigger function by using [Azure Storage Explorer](http://storageexplorer.com/).</span></span>

1. <span data-ttu-id="8658e-169">In the [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span><span class="sxs-lookup"><span data-stu-id="8658e-169">In the [Azure portal] for your function app, create a C#, F# or JavaScript blob trigger function.</span></span> <span data-ttu-id="8658e-170">Set the path to monitor to the name of your blob container.</span><span class="sxs-lookup"><span data-stu-id="8658e-170">Set the path to monitor to the name of your blob container.</span></span> <span data-ttu-id="8658e-171">For example:</span><span class="sxs-lookup"><span data-stu-id="8658e-171">For example:</span></span>

        files
2. <span data-ttu-id="8658e-172">Click the **+** button to select or create the storage account you want to use.</span><span class="sxs-lookup"><span data-stu-id="8658e-172">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="8658e-173">Then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8658e-173">Then click **Create**.</span></span>
3. <span data-ttu-id="8658e-174">Create a text file with the following text, and save it:</span><span class="sxs-lookup"><span data-stu-id="8658e-174">Create a text file with the following text, and save it:</span></span>

        A text file for blob trigger function testing.
4. <span data-ttu-id="8658e-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect to the blob container in the storage account being monitored.</span><span class="sxs-lookup"><span data-stu-id="8658e-175">Run [Azure Storage Explorer](http://storageexplorer.com/), and connect to the blob container in the storage account being monitored.</span></span>
5. <span data-ttu-id="8658e-176">Click **Upload** to upload the text file.</span><span class="sxs-lookup"><span data-stu-id="8658e-176">Click **Upload** to upload the text file.</span></span>

    ![Screenshot of Storage Explorer](./media/functions-test-a-function/azure-storage-explorer-test.png)

<span data-ttu-id="8658e-178">The default blob trigger function code reports the processing of the blob in the logs:</span><span class="sxs-lookup"><span data-stu-id="8658e-178">The default blob trigger function code reports the processing of the blob in the logs:</span></span>

    2016-03-24T11:30:10  Welcome, you are now connected to log-streaming service.
    2016-03-24T11:30:34.472 Function started (Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)
    2016-03-24T11:30:34.472 C# Blob trigger function processed: A text file for blob trigger function testing.
    2016-03-24T11:30:34.472 Function completed (Success, Id=739ebc07-ff9e-4ec4-a444-e479cec2e460)

## <a name="test-a-function-within-functions"></a><span data-ttu-id="8658e-179">Test a function within functions</span><span class="sxs-lookup"><span data-stu-id="8658e-179">Test a function within functions</span></span>
<span data-ttu-id="8658e-180">The Azure Functions portal is designed to let you test HTTP and timer triggered functions.</span><span class="sxs-lookup"><span data-stu-id="8658e-180">The Azure Functions portal is designed to let you test HTTP and timer triggered functions.</span></span> <span data-ttu-id="8658e-181">You can also create functions to trigger other functions that you are testing.</span><span class="sxs-lookup"><span data-stu-id="8658e-181">You can also create functions to trigger other functions that you are testing.</span></span>

### <a name="test-with-the-functions-portal-run-button"></a><span data-ttu-id="8658e-182">Test with the Functions portal Run button</span><span class="sxs-lookup"><span data-stu-id="8658e-182">Test with the Functions portal Run button</span></span>
<span data-ttu-id="8658e-183">The portal provides a **Run** button that you can use to do some limited testing.</span><span class="sxs-lookup"><span data-stu-id="8658e-183">The portal provides a **Run** button that you can use to do some limited testing.</span></span> <span data-ttu-id="8658e-184">You can provide a request body by using the button, but you can't provide query string parameters or update request headers.</span><span class="sxs-lookup"><span data-stu-id="8658e-184">You can provide a request body by using the button, but you can't provide query string parameters or update request headers.</span></span>

<span data-ttu-id="8658e-185">Test the HTTP trigger function we created earlier by adding a JSON string similar to the following in the **Request body** field.</span><span class="sxs-lookup"><span data-stu-id="8658e-185">Test the HTTP trigger function we created earlier by adding a JSON string similar to the following in the **Request body** field.</span></span> <span data-ttu-id="8658e-186">Then click the **Run** button.</span><span class="sxs-lookup"><span data-stu-id="8658e-186">Then click the **Run** button.</span></span>

```json
{
    "name" : "Wes testing Run button",
    "address" : "USA"
}
```

<span data-ttu-id="8658e-187">In the portal **Logs** window, output similar to the following is logged in executing the function:</span><span class="sxs-lookup"><span data-stu-id="8658e-187">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:03:12  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:03:17.357 Function started (Id=753a01b0-45a8-4125-a030-3ad543a89409)
    2016-03-23T08:03:18.697 HTTP trigger function processed a request. RequestUri=https://functions841def78.azurewebsites.net/api/wesmchttptriggernodejs1
    2016-03-23T08:03:18.697 Request Headers = {"connection":"Keep-Alive","accept":"*/*","accept-encoding":"gzip","accept-language":"en-US"}
    2016-03-23T08:03:18.697 Processing user info from request body...
    2016-03-23T08:03:18.697 Processing User Information...
    2016-03-23T08:03:18.697 name = Wes testing Run button
    2016-03-23T08:03:18.697 address = USA
    2016-03-23T08:03:18.744 Function completed (Success, Id=753a01b0-45a8-4125-a030-3ad543a89409)


### <a name="test-with-a-timer-trigger"></a><span data-ttu-id="8658e-188">Test with a timer trigger</span><span class="sxs-lookup"><span data-stu-id="8658e-188">Test with a timer trigger</span></span>
<span data-ttu-id="8658e-189">Some functions can't be adequately tested with the tools mentioned previously.</span><span class="sxs-lookup"><span data-stu-id="8658e-189">Some functions can't be adequately tested with the tools mentioned previously.</span></span> <span data-ttu-id="8658e-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="8658e-190">For example, consider a queue trigger function that runs when a message is dropped into [Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span> <span data-ttu-id="8658e-191">You can always write code to drop a message into your queue, and an example of this in a console project is provided later in this article.</span><span class="sxs-lookup"><span data-stu-id="8658e-191">You can always write code to drop a message into your queue, and an example of this in a console project is provided later in this article.</span></span> <span data-ttu-id="8658e-192">However, there is another approach you can use that tests functions directly.</span><span class="sxs-lookup"><span data-stu-id="8658e-192">However, there is another approach you can use that tests functions directly.</span></span>  

<span data-ttu-id="8658e-193">You can use a timer trigger configured with a queue output binding.</span><span class="sxs-lookup"><span data-stu-id="8658e-193">You can use a timer trigger configured with a queue output binding.</span></span> <span data-ttu-id="8658e-194">That timer trigger code can then write the test messages to the queue.</span><span class="sxs-lookup"><span data-stu-id="8658e-194">That timer trigger code can then write the test messages to the queue.</span></span> <span data-ttu-id="8658e-195">This section walks through an example.</span><span class="sxs-lookup"><span data-stu-id="8658e-195">This section walks through an example.</span></span>

<span data-ttu-id="8658e-196">For more in-depth information on using bindings with Azure Functions, see the [Azure Functions developer reference](functions-reference.md).</span><span class="sxs-lookup"><span data-stu-id="8658e-196">For more in-depth information on using bindings with Azure Functions, see the [Azure Functions developer reference](functions-reference.md).</span></span>

#### <a name="create-a-queue-trigger-for-testing"></a><span data-ttu-id="8658e-197">Create a queue trigger for testing</span><span class="sxs-lookup"><span data-stu-id="8658e-197">Create a queue trigger for testing</span></span>
<span data-ttu-id="8658e-198">To demonstrate this approach, we first create a queue trigger function that we want to test for a queue named `queue-newusers`.</span><span class="sxs-lookup"><span data-stu-id="8658e-198">To demonstrate this approach, we first create a queue trigger function that we want to test for a queue named `queue-newusers`.</span></span> <span data-ttu-id="8658e-199">This function processes name and address information dropped into Queue storage for a new user.</span><span class="sxs-lookup"><span data-stu-id="8658e-199">This function processes name and address information dropped into Queue storage for a new user.</span></span>

> [!NOTE]
> <span data-ttu-id="8658e-200">If you use a different queue name, make sure the name you use conforms to the [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span><span class="sxs-lookup"><span data-stu-id="8658e-200">If you use a different queue name, make sure the name you use conforms to the [Naming Queues and MetaData](https://msdn.microsoft.com/library/dd179349.aspx) rules.</span></span> <span data-ttu-id="8658e-201">Otherwise, you get an error.</span><span class="sxs-lookup"><span data-stu-id="8658e-201">Otherwise, you get an error.</span></span>
>
>

1. <span data-ttu-id="8658e-202">In the [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="8658e-202">In the [Azure portal] for your function app, click **New Function** > **QueueTrigger - C#**.</span></span>
2. <span data-ttu-id="8658e-203">Enter the queue name to be monitored by the queue function:</span><span class="sxs-lookup"><span data-stu-id="8658e-203">Enter the queue name to be monitored by the queue function:</span></span>

        queue-newusers
3. <span data-ttu-id="8658e-204">Click the **+** button to select or create the storage account you want to use.</span><span class="sxs-lookup"><span data-stu-id="8658e-204">Click the **+** button to select or create the storage account you want to use.</span></span> <span data-ttu-id="8658e-205">Then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8658e-205">Then click **Create**.</span></span>
4. <span data-ttu-id="8658e-206">Leave this portal browser window open, so you can monitor the log entries for the default queue function template code.</span><span class="sxs-lookup"><span data-stu-id="8658e-206">Leave this portal browser window open, so you can monitor the log entries for the default queue function template code.</span></span>

#### <a name="create-a-timer-trigger-to-drop-a-message-in-the-queue"></a><span data-ttu-id="8658e-207">Create a timer trigger to drop a message in the queue</span><span class="sxs-lookup"><span data-stu-id="8658e-207">Create a timer trigger to drop a message in the queue</span></span>
1. <span data-ttu-id="8658e-208">Open the [Azure portal] in a new browser window, and navigate to your function app.</span><span class="sxs-lookup"><span data-stu-id="8658e-208">Open the [Azure portal] in a new browser window, and navigate to your function app.</span></span>
2. <span data-ttu-id="8658e-209">Click **New Function** > **TimerTrigger - C#**.</span><span class="sxs-lookup"><span data-stu-id="8658e-209">Click **New Function** > **TimerTrigger - C#**.</span></span> <span data-ttu-id="8658e-210">Enter a cron expression to set how often the timer code tests your queue function.</span><span class="sxs-lookup"><span data-stu-id="8658e-210">Enter a cron expression to set how often the timer code tests your queue function.</span></span> <span data-ttu-id="8658e-211">Then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="8658e-211">Then click **Create**.</span></span> <span data-ttu-id="8658e-212">If you want the test to run every 30 seconds, you can use the following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span><span class="sxs-lookup"><span data-stu-id="8658e-212">If you want the test to run every 30 seconds, you can use the following [CRON expression](https://wikipedia.org/wiki/Cron#CRON_expression):</span></span>

        */30 * * * * *
3. <span data-ttu-id="8658e-213">Click the **Integrate** tab for your new timer trigger.</span><span class="sxs-lookup"><span data-stu-id="8658e-213">Click the **Integrate** tab for your new timer trigger.</span></span>
4. <span data-ttu-id="8658e-214">Under **Output**, click **+ New Output**.</span><span class="sxs-lookup"><span data-stu-id="8658e-214">Under **Output**, click **+ New Output**.</span></span> <span data-ttu-id="8658e-215">Then click **queue** and **Select**.</span><span class="sxs-lookup"><span data-stu-id="8658e-215">Then click **queue** and **Select**.</span></span>
5. <span data-ttu-id="8658e-216">Note the name you use for the **queue message object**.</span><span class="sxs-lookup"><span data-stu-id="8658e-216">Note the name you use for the **queue message object**.</span></span> <span data-ttu-id="8658e-217">You use this in the timer function code.</span><span class="sxs-lookup"><span data-stu-id="8658e-217">You use this in the timer function code.</span></span>

        myQueue
6. <span data-ttu-id="8658e-218">Enter the queue name where the message is sent:</span><span class="sxs-lookup"><span data-stu-id="8658e-218">Enter the queue name where the message is sent:</span></span>

        queue-newusers
7. <span data-ttu-id="8658e-219">Click the **+** button to select the storage account you used previously with the queue trigger.</span><span class="sxs-lookup"><span data-stu-id="8658e-219">Click the **+** button to select the storage account you used previously with the queue trigger.</span></span> <span data-ttu-id="8658e-220">Then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8658e-220">Then click **Save**.</span></span>
8. <span data-ttu-id="8658e-221">Click the **Develop** tab for your timer trigger.</span><span class="sxs-lookup"><span data-stu-id="8658e-221">Click the **Develop** tab for your timer trigger.</span></span>
9. <span data-ttu-id="8658e-222">You can use the following code for the C# timer function, as long as you used the same queue message object name shown earlier.</span><span class="sxs-lookup"><span data-stu-id="8658e-222">You can use the following code for the C# timer function, as long as you used the same queue message object name shown earlier.</span></span> <span data-ttu-id="8658e-223">Then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="8658e-223">Then click **Save**.</span></span>

    ```cs
    using System;

    public static void Run(TimerInfo myTimer, out String myQueue, TraceWriter log)
    {
        String newUser =
        "{\"name\":\"User testing from C# timer function\",\"address\":\"XYZ\"}";

        log.Verbose($"C# Timer trigger function executed at: {DateTime.Now}");   
        log.Verbose($"{newUser}");   

        myQueue = newUser;
    }
    ```

<span data-ttu-id="8658e-224">At this point, the C# timer function executes every 30 seconds if you used the example cron expression.</span><span class="sxs-lookup"><span data-stu-id="8658e-224">At this point, the C# timer function executes every 30 seconds if you used the example cron expression.</span></span> <span data-ttu-id="8658e-225">The logs for the timer function report each execution:</span><span class="sxs-lookup"><span data-stu-id="8658e-225">The logs for the timer function report each execution:</span></span>

    2016-03-24T10:27:02  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.004 Function started (Id=04061790-974f-4043-b851-48bd4ac424d1)
    2016-03-24T10:27:30.004 C# Timer trigger function executed at: 3/24/2016 10:27:30 AM
    2016-03-24T10:27:30.004 {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.004 Function completed (Success, Id=04061790-974f-4043-b851-48bd4ac424d1)

<span data-ttu-id="8658e-226">In the browser window for the queue function, you can see each message being processed:</span><span class="sxs-lookup"><span data-stu-id="8658e-226">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"User testing from C# timer function","address":"XYZ"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)

## <a name="test-a-function-with-code"></a><span data-ttu-id="8658e-227">Test a function with code</span><span class="sxs-lookup"><span data-stu-id="8658e-227">Test a function with code</span></span>
<span data-ttu-id="8658e-228">You may need to create an external application or framework to test your functions.</span><span class="sxs-lookup"><span data-stu-id="8658e-228">You may need to create an external application or framework to test your functions.</span></span>

### <a name="test-an-http-trigger-function-with-code-nodejs"></a><span data-ttu-id="8658e-229">Test an HTTP trigger function with code: Node.js</span><span class="sxs-lookup"><span data-stu-id="8658e-229">Test an HTTP trigger function with code: Node.js</span></span>
<span data-ttu-id="8658e-230">You can use a Node.js app to execute an HTTP request to test your function.</span><span class="sxs-lookup"><span data-stu-id="8658e-230">You can use a Node.js app to execute an HTTP request to test your function.</span></span>
<span data-ttu-id="8658e-231">Make sure to set:</span><span class="sxs-lookup"><span data-stu-id="8658e-231">Make sure to set:</span></span>

* <span data-ttu-id="8658e-232">The `host` in the request options to your function app host.</span><span class="sxs-lookup"><span data-stu-id="8658e-232">The `host` in the request options to your function app host.</span></span>
* <span data-ttu-id="8658e-233">Your function name in the `path`.</span><span class="sxs-lookup"><span data-stu-id="8658e-233">Your function name in the `path`.</span></span>
* <span data-ttu-id="8658e-234">Your access code (`<your code>`) in the `path`.</span><span class="sxs-lookup"><span data-stu-id="8658e-234">Your access code (`<your code>`) in the `path`.</span></span>

<span data-ttu-id="8658e-235">Code example:</span><span class="sxs-lookup"><span data-stu-id="8658e-235">Code example:</span></span>

```javascript
var http = require("http");

var nameQueryString = "name=Wes%20Query%20String%20Test%20From%20Node.js";

var nameBodyJSON = {
    name : "Wes testing with Node.JS code",
    address : "Dallas, T.X. 75201"
};

var bodyString = JSON.stringify(nameBodyJSON);

var options = {
  host: "functions841def78.azurewebsites.net",
  //path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9&" + nameQueryString,
  path: "/api/HttpTriggerNodeJS2?code=sc1wt62opn7k9buhrm8jpds4ikxvvj42m5ojdt0p91lz5jnhfr2c74ipoujyq26wab3wk5gkfbt9",
  method: "POST",
  headers : {
      "Content-Type":"application/json",
      "Content-Length": Buffer.byteLength(bodyString)
    }    
};

callback = function(response) {
  var str = ""
  response.on("data", function (chunk) {
    str += chunk;
  });

  response.on("end", function () {
    console.log(str);
  });
}

var req = http.request(options, callback);
console.log("*** Sending name and address in body ***");
console.log(bodyString);
req.end(bodyString);
```


<span data-ttu-id="8658e-236">Output:</span><span class="sxs-lookup"><span data-stu-id="8658e-236">Output:</span></span>

    C:\Users\Wesley\testing\Node.js>node testHttpTriggerExample.js
    *** Sending name and address in body ***
    {"name" : "Wes testing with Node.JS code","address" : "Dallas, T.X. 75201"}
    Hello Wes testing with Node.JS code
    The address you provided is Dallas, T.X. 75201

<span data-ttu-id="8658e-237">In the portal **Logs** window, output similar to the following is logged in executing the function:</span><span class="sxs-lookup"><span data-stu-id="8658e-237">In the portal **Logs** window, output similar to the following is logged in executing the function:</span></span>

    2016-03-23T08:08:55  Welcome, you are now connected to log-streaming service.
    2016-03-23T08:08:59.736 Function started (Id=607b891c-08a1-427f-910c-af64ae4f7f9c)
    2016-03-23T08:09:01.153 HTTP trigger function processed a request. RequestUri=http://functionsExample.azurewebsites.net/api/WesmcHttpTriggerNodeJS1/?code=XXXXXXXXXX==
    2016-03-23T08:09:01.153 Request Headers = {"connection":"Keep-Alive","host":"functionsExample.azurewebsites.net"}
    2016-03-23T08:09:01.153 Name not provided as query string param. Checking body...
    2016-03-23T08:09:01.153 Request Body Type = object
    2016-03-23T08:09:01.153 Request Body = [object Object]
    2016-03-23T08:09:01.153 Processing User Information...
    2016-03-23T08:09:01.215 Function completed (Success, Id=607b891c-08a1-427f-910c-af64ae4f7f9c)


### <a name="test-a-queue-trigger-function-with-code-c"></a><span data-ttu-id="8658e-238">Test a queue trigger function with code: C#</span><span class="sxs-lookup"><span data-stu-id="8658e-238">Test a queue trigger function with code: C#</span></span> #
<span data-ttu-id="8658e-239">We mentioned earlier that you can test a queue trigger by using code to drop a message in your queue.</span><span class="sxs-lookup"><span data-stu-id="8658e-239">We mentioned earlier that you can test a queue trigger by using code to drop a message in your queue.</span></span> <span data-ttu-id="8658e-240">The following example code is based on the C# code presented in the [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="8658e-240">The following example code is based on the C# code presented in the [Getting started with Azure Queue storage](../storage/queues/storage-dotnet-how-to-use-queues.md) tutorial.</span></span> <span data-ttu-id="8658e-241">Code for other languages is also available from that link.</span><span class="sxs-lookup"><span data-stu-id="8658e-241">Code for other languages is also available from that link.</span></span>

<span data-ttu-id="8658e-242">To test this code in a console app, you must:</span><span class="sxs-lookup"><span data-stu-id="8658e-242">To test this code in a console app, you must:</span></span>

* <span data-ttu-id="8658e-243">[Configure your storage connection string in the app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span><span class="sxs-lookup"><span data-stu-id="8658e-243">[Configure your storage connection string in the app.config file](../storage/queues/storage-dotnet-how-to-use-queues.md).</span></span>
* <span data-ttu-id="8658e-244">Pass a `name` and `address` as parameters to the app.</span><span class="sxs-lookup"><span data-stu-id="8658e-244">Pass a `name` and `address` as parameters to the app.</span></span> <span data-ttu-id="8658e-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span><span class="sxs-lookup"><span data-stu-id="8658e-245">For example, `C:\myQueueConsoleApp\test.exe "Wes testing queues" "in a console app"`.</span></span> <span data-ttu-id="8658e-246">(This code accepts the name and address for a new user as command-line arguments during runtime.)</span><span class="sxs-lookup"><span data-stu-id="8658e-246">(This code accepts the name and address for a new user as command-line arguments during runtime.)</span></span>

<span data-ttu-id="8658e-247">Example C# code:</span><span class="sxs-lookup"><span data-stu-id="8658e-247">Example C# code:</span></span>

```cs
static void Main(string[] args)
{
    string name = null;
    string address = null;
    string queueName = "queue-newusers";
    string JSON = null;

    if (args.Length > 0)
    {
        name = args[0];
    }
    if (args.Length > 1)
    {
        address = args[1];
    }

    // Retrieve storage account from connection string
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConfigurationManager.AppSettings["StorageConnectionString"]);

    // Create the queue client
    CloudQueueClient queueClient = storageAccount.CreateCloudQueueClient();

    // Retrieve a reference to a queue
    CloudQueue queue = queueClient.GetQueueReference(queueName);

    // Create the queue if it doesn't already exist
    queue.CreateIfNotExists();

    // Create a message and add it to the queue.
    if (name != null)
    {
        if (address != null)
            JSON = String.Format("{{\"name\":\"{0}\",\"address\":\"{1}\"}}", name, address);
        else
            JSON = String.Format("{{\"name\":\"{0}\"}}", name);
    }

    Console.WriteLine("Adding message to " + queueName + "...");
    Console.WriteLine(JSON);

    CloudQueueMessage message = new CloudQueueMessage(JSON);
    queue.AddMessage(message);
}
```

<span data-ttu-id="8658e-248">In the browser window for the queue function, you can see each message being processed:</span><span class="sxs-lookup"><span data-stu-id="8658e-248">In the browser window for the queue function, you can see each message being processed:</span></span>

    2016-03-24T10:27:06  Welcome, you are now connected to log-streaming service.
    2016-03-24T10:27:30.607 Function started (Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)
    2016-03-24T10:27:30.607 C# Queue trigger function processed: {"name":"Wes testing queues","address":"in a console app"}
    2016-03-24T10:27:30.607 Function completed (Success, Id=e304450c-ff48-44dc-ba2e-1df7209a9d22)


<!-- URLs. -->

[Azure portal]: https://portal.azure.com
