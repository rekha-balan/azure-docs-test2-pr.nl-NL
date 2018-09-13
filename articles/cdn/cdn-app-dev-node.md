---
title: Get started with the Azure CDN SDK for Node.js | Microsoft Docs
description: Learn how to write Node.js applications to manage Azure CDN.
services: cdn
documentationcenter: nodejs
author: zhangmanling
manager: erikre
editor: ''
ms.assetid: c4bb6a61-de3d-4f0c-9dca-202554c43dfa
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f38056835e06667b805caeff8f48e4515713a90c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554203"
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="6d8a3-103">Get started with Azure CDN development</span><span class="sxs-lookup"><span data-stu-id="6d8a3-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [Node.js](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="6d8a3-106">You can use the [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) to automate creation and management of CDN profiles and endpoints.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-106">You can use the [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="6d8a3-107">This tutorial walks through the creation of a simple Node.js console application that demonstrates several of the available operations.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-107">This tutorial walks through the creation of a simple Node.js console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="6d8a3-108">This tutorial is not intended to describe all aspects of the Azure CDN SDK for Node.js in detail.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-108">This tutorial is not intended to describe all aspects of the Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="6d8a3-109">To complete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-109">To complete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="6d8a3-110">You can use any text editor you want to create your Node.js application.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-110">You can use any text editor you want to create your Node.js application.</span></span>  <span data-ttu-id="6d8a3-111">To write this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="6d8a3-111">To write this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="6d8a3-113">Create your project and add NPM dependencies</span><span class="sxs-lookup"><span data-stu-id="6d8a3-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="6d8a3-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="6d8a3-115">Create a folder to store your application.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-115">Create a folder to store your application.</span></span>  <span data-ttu-id="6d8a3-116">From a console with the Node.js tools in your current path, set your current location to this new folder and initialize your project by executing:</span><span class="sxs-lookup"><span data-stu-id="6d8a3-116">From a console with the Node.js tools in your current path, set your current location to this new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="6d8a3-117">You will then be presented a series of questions to initialize your project.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-117">You will then be presented a series of questions to initialize your project.</span></span>  <span data-ttu-id="6d8a3-118">For **entry point**, this tutorial uses *app.js*.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="6d8a3-119">You can see my other choices in the following example.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-119">You can see my other choices in the following example.</span></span>

![NPM init output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="6d8a3-121">Our project is now initialized with a *packages.json* file.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="6d8a3-122">Our project is going to use some Azure libraries contained in NPM packages.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-122">Our project is going to use some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="6d8a3-123">We'll use the Azure Client Runtime for Node.js (ms-rest-azure) and the Azure CDN Client Library for Node.js (azure-arm-cd).</span><span class="sxs-lookup"><span data-stu-id="6d8a3-123">We'll use the Azure Client Runtime for Node.js (ms-rest-azure) and the Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="6d8a3-124">Let's add those to the project as dependencies.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-124">Let's add those to the project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="6d8a3-125">After the packages are done installing, the *package.json* file should look similar to this example (version numbers may differ):</span><span class="sxs-lookup"><span data-stu-id="6d8a3-125">After the packages are done installing, the *package.json* file should look similar to this example (version numbers may differ):</span></span>

``` json
{
  "name": "cdn_node",
  "version": "1.0.0",
  "description": "Azure CDN Node.js tutorial project",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Cam Soper",
  "license": "MIT",
  "dependencies": {
    "azure-arm-cdn": "^0.2.1",
    "ms-rest-azure": "^1.14.4"
  }
}
```

<span data-ttu-id="6d8a3-126">Finally, using your text editor, create a blank text file and save it in the root of our project folder as *app.js*.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-126">Finally, using your text editor, create a blank text file and save it in the root of our project folder as *app.js*.</span></span>  <span data-ttu-id="6d8a3-127">We're now ready to begin writing code.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-127">We're now ready to begin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="6d8a3-128">Requires, constants, authentication, and structure</span><span class="sxs-lookup"><span data-stu-id="6d8a3-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="6d8a3-129">With *app.js* open in our editor, let's get the basic structure of our program written.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-129">With *app.js* open in our editor, let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="6d8a3-130">Add the "requires" for our NPM packages at the top with the following:</span><span class="sxs-lookup"><span data-stu-id="6d8a3-130">Add the "requires" for our NPM packages at the top with the following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="6d8a3-131">We need to define some constants our methods will use.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-131">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="6d8a3-132">Add the following.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-132">Add the following.</span></span>  <span data-ttu-id="6d8a3-133">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-133">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
    ``` javascript
    //Tenant app constants
    const clientId = "<YOUR CLIENT ID>";
    const clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    const tenantId = "<YOUR TENANT ID>";
   
    //Application constants
    const subscriptionId = "<YOUR SUBSCRIPTION ID>";
    const resourceGroupName = "CdnConsoleTutorial";
    const resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. <span data-ttu-id="6d8a3-134">Next, we'll instantiate the CDN management client and give it our credentials.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-134">Next, we'll instantiate the CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="6d8a3-135">If you are using individual user authentication, these two lines will look slightly different.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > Only use this code sample if you are choosing to have individual user authentication instead of a service principal.  Be careful to guard your individual user credentials and keep them secret.
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="6d8a3-138">Be sure to replace the items in **&lt;angle brackets&gt;** with the correct information.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-138">Be sure to replace the items in **&lt;angle brackets&gt;** with the correct information.</span></span>  <span data-ttu-id="6d8a3-139">For `<redirect URI>`, use the redirect URI you entered when you registered the application in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-139">For `<redirect URI>`, use the redirect URI you entered when you registered the application in Azure AD.</span></span>
4. <span data-ttu-id="6d8a3-140">Our Node.js console application is going to take some command-line parameters.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-140">Our Node.js console application is going to take some command-line parameters.</span></span>  <span data-ttu-id="6d8a3-141">Let's validate that at least one parameter was passed.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-141">Let's validate that at least one parameter was passed.</span></span>
   
   ```javascript
   //Collect command-line parameters
   var parms = process.argv.slice(2);
   
   //Do we have parameters?
   if(parms == null || parms.length == 0)
   {
       console.log("Not enough parameters!");
       console.log("Valid commands are list, delete, create, and purge.");
       process.exit(1);
   }
   ```
5. <span data-ttu-id="6d8a3-142">That brings us to the main part of our program, where we branch off to other functions based on what parameters were passed.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-142">That brings us to the main part of our program, where we branch off to other functions based on what parameters were passed.</span></span>
   
    ```javascript
    switch(parms[0].toLowerCase())
    {
        case "list":
            cdnList();
            break;
   
        case "create":
            cdnCreate();
            break;
   
        case "delete":
            cdnDelete();
            break;
   
        case "purge":
            cdnPurge();
            break;
   
        default:
            console.log("Valid commands are list, delete, create, and purge.");
            process.exit(1);
    }
    ```
6. <span data-ttu-id="6d8a3-143">At several places in our program, we'll need to make sure the right number of parameters were passed in and display some help if they don't look correct.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-143">At several places in our program, we'll need to make sure the right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="6d8a3-144">Let's create functions to do that.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-144">Let's create functions to do that.</span></span>
   
   ```javascript
   function requireParms(parmCount) {
       if(parms.length < parmCount) {
           usageHelp(parms[0].toLowerCase());
           process.exit(1);
       }
   }
   
   function usageHelp(cmd) {
       console.log("Usage for " + cmd + ":");
       switch(cmd)
       {
           case "list":
               console.log("list profiles");
               console.log("list endpoints <profile name>");
               break;
   
           case "create":
               console.log("create profile <profile name>");
               console.log("create endpoint <profile name> <endpoint name> <origin hostname>");
               break;
   
           case "delete":
               console.log("delete profile <profile name>");
               console.log("delete endpoint <profile name> <endpoint name>");
               break;
   
           case "purge":
               console.log("purge <profile name> <endpoint name> <path>");
               break;
   
           default:
               console.log("Invalid command.");
       }
   }
   ```
7. <span data-ttu-id="6d8a3-145">Finally, the functions we'll be using on the CDN management client are asynchronous, so they need a method to call back when they're done.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-145">Finally, the functions we'll be using on the CDN management client are asynchronous, so they need a method to call back when they're done.</span></span>  <span data-ttu-id="6d8a3-146">Let's make one that can display the output from the CDN management client (if any) and exit the program gracefully.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-146">Let's make one that can display the output from the CDN management client (if any) and exit the program gracefully.</span></span>
   
    ```javascript
    function callback(err, result, request, response) {
        if (err) {
            console.log(err);
            process.exit(1);
        } else {
            console.log((result == null) ? "Done!" : result);
            process.exit(0);
        }
    }
    ```

<span data-ttu-id="6d8a3-147">Now that the basic structure of our program is written, we should create the functions called based on our parameters.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-147">Now that the basic structure of our program is written, we should create the functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="6d8a3-148">List CDN profiles and endpoints</span><span class="sxs-lookup"><span data-stu-id="6d8a3-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="6d8a3-149">Let's start with code to list our existing profiles and endpoints.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-149">Let's start with code to list our existing profiles and endpoints.</span></span>  <span data-ttu-id="6d8a3-150">My code comments provide the expected syntax so we know where each parameter goes.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-150">My code comments provide the expected syntax so we know where each parameter goes.</span></span>

```javascript
// list profiles
// list endpoints <profile name>
function cdnList(){
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profiles":
            console.log("Listing profiles...");
            cdnClient.profiles.listByResourceGroup(resourceGroupName, callback);
            break;

        case "endpoints":
            requireParms(3);
            console.log("Listing endpoints...");
            cdnClient.endpoints.listByProfile(parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="6d8a3-151">Create CDN profiles and endpoints</span><span class="sxs-lookup"><span data-stu-id="6d8a3-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="6d8a3-152">Next, we'll write the functions to create profiles and endpoints.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-152">Next, we'll write the functions to create profiles and endpoints.</span></span>

```javascript
function cdnCreate() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profile":
            cdnCreateProfile();
            break;

        case "endpoint":
            cdnCreateEndpoint();
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}

// create profile <profile name>
function cdnCreateProfile() {
    requireParms(3);
    console.log("Creating profile...");
    var standardCreateParameters = {
        location: resourceLocation,
        sku: {
            name: 'Standard_Verizon'
        }
    };

    cdnClient.profiles.create(parms[2], standardCreateParameters, resourceGroupName, callback);
}

// create endpoint <profile name> <endpoint name> <origin hostname>        
function cdnCreateEndpoint() {
    requireParms(5);
    console.log("Creating endpoint...");
    var endpointProperties = {
        location: resourceLocation,
        origins: [{
            name: parms[4],
            hostName: parms[4]
        }]
    };

    cdnClient.endpoints.create(parms[3], endpointProperties, parms[2], resourceGroupName, callback);
}
```

## <a name="purge-an-endpoint"></a><span data-ttu-id="6d8a3-153">Purge an endpoint</span><span class="sxs-lookup"><span data-stu-id="6d8a3-153">Purge an endpoint</span></span>
<span data-ttu-id="6d8a3-154">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging content in our endpoint.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-154">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="6d8a3-155">Delete CDN profiles and endpoints</span><span class="sxs-lookup"><span data-stu-id="6d8a3-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="6d8a3-156">The last function we will include deletes endpoints and profiles.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-156">The last function we will include deletes endpoints and profiles.</span></span>

```javascript
function cdnDelete() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        // delete profile <profile name>
        case "profile":
            requireParms(3);
            console.log("Deleting profile...");
            cdnClient.profiles.deleteIfExists(parms[2], resourceGroupName, callback);
            break;

        // delete endpoint <profile name> <endpoint name>
        case "endpoint":
            requireParms(4);
            console.log("Deleting endpoint...");
            cdnClient.endpoints.deleteIfExists(parms[3], parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="running-the-program"></a><span data-ttu-id="6d8a3-157">Running the program</span><span class="sxs-lookup"><span data-stu-id="6d8a3-157">Running the program</span></span>
<span data-ttu-id="6d8a3-158">We can now execute our Node.js program using our favorite debugger or at the console.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-158">We can now execute our Node.js program using our favorite debugger or at the console.</span></span>

> [!TIP]
> If you're using Visual Studio Code as your debugger, you'll need to set up your environment to pass in the command-line parameters.  Visual Studio Code does this in the **lanuch.json** file.  Look for a property named **args** and add an array of string values for your parameters, so that it looks similar to this:  `"args": ["list", "profiles"]`.
> 
> 

<span data-ttu-id="6d8a3-162">Let's start by listing our profiles.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-162">Let's start by listing our profiles.</span></span>

![List profiles](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="6d8a3-164">We got back an empty array.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-164">We got back an empty array.</span></span>  <span data-ttu-id="6d8a3-165">Since we don't have any profiles in our resource group, that's expected.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="6d8a3-166">Let's create a profile now.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-166">Let's create a profile now.</span></span>

![Create profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="6d8a3-168">Now, let's add an endpoint.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-168">Now, let's add an endpoint.</span></span>

![Create endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="6d8a3-170">Finally, let's delete our profile.</span><span class="sxs-lookup"><span data-stu-id="6d8a3-170">Finally, let's delete our profile.</span></span>

![Delete profile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cdn/media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="6d8a3-172">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6d8a3-172">Next Steps</span></span>
<span data-ttu-id="6d8a3-173">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="6d8a3-173">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="6d8a3-174">To see the reference for the Azure CDN SDK for Node.js, view the [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="6d8a3-174">To see the reference for the Azure CDN SDK for Node.js, view the [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="6d8a3-175">To find additional documentation on the Azure SDK for Node.js, view the [full reference](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="6d8a3-175">To find additional documentation on the Azure SDK for Node.js, view the [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="6d8a3-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="6d8a3-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>






