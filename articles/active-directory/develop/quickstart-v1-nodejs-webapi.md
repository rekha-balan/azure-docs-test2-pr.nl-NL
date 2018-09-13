---
title: Azure AD Node.js web API getting started | Microsoft Docs
description: How to build a Node.js REST web API that integrates with Azure AD for authentication.
services: active-directory
documentationcenter: nodejs
author: CelesteDG
manager: mtillman
ms.assetid: 7654ab4c-4489-4ea5-aba9-d7cdc256e42a
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 11/30/2017
ms.author: celested
ms.custom: aaddev
ms.openlocfilehash: 3b203e5be82c01e7d586c90bae454aca23ebd630
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856834"
---
# <a name="azure-ad-nodejs-web-api-getting-started"></a><span data-ttu-id="f0047-103">Azure AD Node.js web API getting started</span><span class="sxs-lookup"><span data-stu-id="f0047-103">Azure AD Node.js web API getting started</span></span>

<span data-ttu-id="f0047-104">This article demonstrates how to secure a [Restify](http://restify.com/) API endpoint with [Passport](http://passportjs.org/) using the [passport-azure-ad](https://github.com/AzureAD/passport-azure-ad) module to handle communication with Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="f0047-104">This article demonstrates how to secure a [Restify](http://restify.com/) API endpoint with [Passport](http://passportjs.org/) using the [passport-azure-ad](https://github.com/AzureAD/passport-azure-ad) module to handle communication with Azure Active Directory (AAD).</span></span> 

<span data-ttu-id="f0047-105">The scope of this tutorial covers the concerns regarding securing API endpoints.</span><span class="sxs-lookup"><span data-stu-id="f0047-105">The scope of this tutorial covers the concerns regarding securing API endpoints.</span></span> <span data-ttu-id="f0047-106">The concerns of signing in and retaining authentication tokens are not implemented here and are the responsibility of a client application.</span><span class="sxs-lookup"><span data-stu-id="f0047-106">The concerns of signing in and retaining authentication tokens are not implemented here and are the responsibility of a client application.</span></span> <span data-ttu-id="f0047-107">For details surrounding a client implementation, review [Node.js web app sign-in and sign-out with Azure AD](quickstart-v1-openid-connect-code.md).</span><span class="sxs-lookup"><span data-stu-id="f0047-107">For details surrounding a client implementation, review [Node.js web app sign-in and sign-out with Azure AD](quickstart-v1-openid-connect-code.md).</span></span>

<span data-ttu-id="f0047-108">The full code sample associated with this article is available on [GitHub](https://github.com/Azure-Samples/active-directory-node-webapi-basic).</span><span class="sxs-lookup"><span data-stu-id="f0047-108">The full code sample associated with this article is available on [GitHub](https://github.com/Azure-Samples/active-directory-node-webapi-basic).</span></span>

## <a name="create-the-sample-project"></a><span data-ttu-id="f0047-109">Create the sample project</span><span class="sxs-lookup"><span data-stu-id="f0047-109">Create the sample project</span></span>
<span data-ttu-id="f0047-110">This server application requires a few package dependencies to support Restify and Passport as well as account information that is passed to AAD.</span><span class="sxs-lookup"><span data-stu-id="f0047-110">This server application requires a few package dependencies to support Restify and Passport as well as account information that is passed to AAD.</span></span>

<span data-ttu-id="f0047-111">To begin, add the following code into a file named `package.json`:</span><span class="sxs-lookup"><span data-stu-id="f0047-111">To begin, add the following code into a file named `package.json`:</span></span>

```Shell
{
  "name": "node-aad-demo",
  "version": "0.0.1",
  "scripts": {
    "start": "node app.js"
  },
  "dependencies": {
    "passport": "0.4.0",
    "passport-azure-ad": "3.0.8",
    "restify": "6.0.1",
    "restify-plugins": "1.6.0"
  }
}
```

<span data-ttu-id="f0047-112">Once `package.json` is created, run `npm install` in your command prompt to install the package dependencies.</span><span class="sxs-lookup"><span data-stu-id="f0047-112">Once `package.json` is created, run `npm install` in your command prompt to install the package dependencies.</span></span> 

### <a name="configure-the-project-to-use-active-directory"></a><span data-ttu-id="f0047-113">Configure the project to use Active Directory</span><span class="sxs-lookup"><span data-stu-id="f0047-113">Configure the project to use Active Directory</span></span>

<span data-ttu-id="f0047-114">To get started configuring the application, there are a few account-specific values you can obtain from the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="f0047-114">To get started configuring the application, there are a few account-specific values you can obtain from the Azure CLI.</span></span> <span data-ttu-id="f0047-115">The easiest way to get started with the CLI is to use the Azure Cloud Shell.</span><span class="sxs-lookup"><span data-stu-id="f0047-115">The easiest way to get started with the CLI is to use the Azure Cloud Shell.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="f0047-116">Enter the following command in the cloud shell:</span><span class="sxs-lookup"><span data-stu-id="f0047-116">Enter the following command in the cloud shell:</span></span> 

```azurecli-interactive
az ad app create --display-name node-aad-demo --homepage http://localhost --identifier-uris http://node-aad-demo
```

<span data-ttu-id="f0047-117">The [arguments](/cli/azure/ad/app?view=azure-cli-latest#az-ad-app-create) for the `create` command include:</span><span class="sxs-lookup"><span data-stu-id="f0047-117">The [arguments](/cli/azure/ad/app?view=azure-cli-latest#az-ad-app-create) for the `create` command include:</span></span>

| <span data-ttu-id="f0047-118">Argument</span><span class="sxs-lookup"><span data-stu-id="f0047-118">Argument</span></span>  | <span data-ttu-id="f0047-119">Description</span><span class="sxs-lookup"><span data-stu-id="f0047-119">Description</span></span> |
|---------|---------|
|`display-name` | <span data-ttu-id="f0047-120">Friendly name of the registration</span><span class="sxs-lookup"><span data-stu-id="f0047-120">Friendly name of the registration</span></span> |
|`homepage` | <span data-ttu-id="f0047-121">Url where users can sign in and use your application</span><span class="sxs-lookup"><span data-stu-id="f0047-121">Url where users can sign in and use your application</span></span> |
|`identifier-uris` | <span data-ttu-id="f0047-122">Space separated unique URIs that Azure AD can use for this application</span><span class="sxs-lookup"><span data-stu-id="f0047-122">Space separated unique URIs that Azure AD can use for this application</span></span> |

<span data-ttu-id="f0047-123">Before you can connect to Azure Active Directory, you need the following information:</span><span class="sxs-lookup"><span data-stu-id="f0047-123">Before you can connect to Azure Active Directory, you need the following information:</span></span>

| <span data-ttu-id="f0047-124">Name</span><span class="sxs-lookup"><span data-stu-id="f0047-124">Name</span></span>  | <span data-ttu-id="f0047-125">Description</span><span class="sxs-lookup"><span data-stu-id="f0047-125">Description</span></span> | <span data-ttu-id="f0047-126">Variable Name in Config File</span><span class="sxs-lookup"><span data-stu-id="f0047-126">Variable Name in Config File</span></span> |
| ------------- | ------------- | ------------- |
| <span data-ttu-id="f0047-127">Tenant Name</span><span class="sxs-lookup"><span data-stu-id="f0047-127">Tenant Name</span></span>  | <span data-ttu-id="f0047-128">[Tenant name](quickstart-create-new-tenant.md) you want to use for authentication</span><span class="sxs-lookup"><span data-stu-id="f0047-128">[Tenant name](quickstart-create-new-tenant.md) you want to use for authentication</span></span> | `tenantName`  |
| <span data-ttu-id="f0047-129">Client ID</span><span class="sxs-lookup"><span data-stu-id="f0047-129">Client ID</span></span>  | <span data-ttu-id="f0047-130">Client ID is the OAuth term used for the AAD _Application ID_.</span><span class="sxs-lookup"><span data-stu-id="f0047-130">Client ID is the OAuth term used for the AAD _Application ID_.</span></span> |  `clientID`  |

<span data-ttu-id="f0047-131">From the registration response in the Azure Cloud Shell, copy the `appId` value and create a new file named `config.js`.</span><span class="sxs-lookup"><span data-stu-id="f0047-131">From the registration response in the Azure Cloud Shell, copy the `appId` value and create a new file named `config.js`.</span></span> <span data-ttu-id="f0047-132">Next, add in the following code and replace your values with the bracketed tokens:</span><span class="sxs-lookup"><span data-stu-id="f0047-132">Next, add in the following code and replace your values with the bracketed tokens:</span></span>

```JavaScript
const tenantName    = //<YOUR_TENANT_NAME>;
const clientID      = //<YOUR_APP_ID_FROM_CLOUD_SHELL>;
const serverPort    = 3000;

module.exports.serverPort = serverPort;

module.exports.credentials = {
  identityMetadata: `https://login.microsoftonline.com/${tenantName}.onmicrosoft.com/.well-known/openid-configuration`, 
  clientID: clientID
};
```
<span data-ttu-id="f0047-133">For more information regarding the individual configuration settings, review the [passport-azure-ad](https://github.com/AzureAD/passport-azure-ad#5-usage) module documentation.</span><span class="sxs-lookup"><span data-stu-id="f0047-133">For more information regarding the individual configuration settings, review the [passport-azure-ad](https://github.com/AzureAD/passport-azure-ad#5-usage) module documentation.</span></span>

## <a name="implement-the-server"></a><span data-ttu-id="f0047-134">Implement the server</span><span class="sxs-lookup"><span data-stu-id="f0047-134">Implement the server</span></span>
<span data-ttu-id="f0047-135">The [passport-azure-ad](https://github.com/AzureAD/passport-azure-ad#5-usage) module  features two authentication strategies: [OIDC](https://github.com/AzureAD/passport-azure-ad#51-oidcstrategy) and [Bearer](https://github.com/AzureAD/passport-azure-ad#52-bearerstrategy) strategies.</span><span class="sxs-lookup"><span data-stu-id="f0047-135">The [passport-azure-ad](https://github.com/AzureAD/passport-azure-ad#5-usage) module  features two authentication strategies: [OIDC](https://github.com/AzureAD/passport-azure-ad#51-oidcstrategy) and [Bearer](https://github.com/AzureAD/passport-azure-ad#52-bearerstrategy) strategies.</span></span> <span data-ttu-id="f0047-136">The server implemented in this article uses the Bearer strategy to secure the API endpoint.</span><span class="sxs-lookup"><span data-stu-id="f0047-136">The server implemented in this article uses the Bearer strategy to secure the API endpoint.</span></span>

### <a name="step-1-import-dependencies"></a><span data-ttu-id="f0047-137">Step 1: Import dependencies</span><span class="sxs-lookup"><span data-stu-id="f0047-137">Step 1: Import dependencies</span></span>
<span data-ttu-id="f0047-138">Create a new file named `app.js` and paste in the following text:</span><span class="sxs-lookup"><span data-stu-id="f0047-138">Create a new file named `app.js` and paste in the following text:</span></span>

```JavaScript
const
      restify = require('restify')
    , restifyPlugins = require('restify-plugins')
    , passport = require('passport')
    , BearerStrategy = require('passport-azure-ad').BearerStrategy
    , config = require('./config')
    , authenticatedUserTokens = []
    , serverPort = process.env.PORT || config.serverPort
;
```

<span data-ttu-id="f0047-139">In this section of code:</span><span class="sxs-lookup"><span data-stu-id="f0047-139">In this section of code:</span></span>

- <span data-ttu-id="f0047-140">The `restify` and `restify-plugins` modules are referenced in order to set up a Restify server.</span><span class="sxs-lookup"><span data-stu-id="f0047-140">The `restify` and `restify-plugins` modules are referenced in order to set up a Restify server.</span></span>

- <span data-ttu-id="f0047-141">The `passport` and `passport-azure-ad` modules are responsible for communicating with AAD.</span><span class="sxs-lookup"><span data-stu-id="f0047-141">The `passport` and `passport-azure-ad` modules are responsible for communicating with AAD.</span></span>

- <span data-ttu-id="f0047-142">The `config` variable is initialized with values from the `config.js` file created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="f0047-142">The `config` variable is initialized with values from the `config.js` file created in the previous step.</span></span>

- <span data-ttu-id="f0047-143">An array is created for `authenticatedUserTokens` to store user tokens as they are passed into secured endpoints.</span><span class="sxs-lookup"><span data-stu-id="f0047-143">An array is created for `authenticatedUserTokens` to store user tokens as they are passed into secured endpoints.</span></span>

- <span data-ttu-id="f0047-144">The `serverPort` is either defined from the process environment's port or from the configuration file.</span><span class="sxs-lookup"><span data-stu-id="f0047-144">The `serverPort` is either defined from the process environment's port or from the configuration file.</span></span>

### <a name="step-2-instantiate-an-authentication-strategy"></a><span data-ttu-id="f0047-145">Step 2: Instantiate an authentication strategy</span><span class="sxs-lookup"><span data-stu-id="f0047-145">Step 2: Instantiate an authentication strategy</span></span>
<span data-ttu-id="f0047-146">As you secure an endpoint, you must provide a strategy responsible for determining whether or not the current request originates from an authenticated user.</span><span class="sxs-lookup"><span data-stu-id="f0047-146">As you secure an endpoint, you must provide a strategy responsible for determining whether or not the current request originates from an authenticated user.</span></span> <span data-ttu-id="f0047-147">Here the `authenticatonStrategy` variable is an instance of the `passport-azure-ad` `BearerStrategy` class.</span><span class="sxs-lookup"><span data-stu-id="f0047-147">Here the `authenticatonStrategy` variable is an instance of the `passport-azure-ad` `BearerStrategy` class.</span></span> <span data-ttu-id="f0047-148">Add the following code after the `require` statements.</span><span class="sxs-lookup"><span data-stu-id="f0047-148">Add the following code after the `require` statements.</span></span>

```JavaScript
const authenticationStrategy = new BearerStrategy(config.credentials, (token, done) => {
    let currentUser = null;

    let userToken = authenticatedUserTokens.find((user) => {
        currentUser = user;
        user.sub === token.sub;
    });

    if(!userToken) {
        authenticatedUserTokens.push(token);
    }

    return done(null, currentUser, token);
});
```
<span data-ttu-id="f0047-149">This implementation uses auto-registration by adding authentication tokens into the `authenticatedUserTokens` array if they do not already exist.</span><span class="sxs-lookup"><span data-stu-id="f0047-149">This implementation uses auto-registration by adding authentication tokens into the `authenticatedUserTokens` array if they do not already exist.</span></span>

<span data-ttu-id="f0047-150">Once a new instance of the strategy is created, you must pass it into Passport via the `use` method.</span><span class="sxs-lookup"><span data-stu-id="f0047-150">Once a new instance of the strategy is created, you must pass it into Passport via the `use` method.</span></span> <span data-ttu-id="f0047-151">Add the following code to `app.js` to use the strategy in Passport.</span><span class="sxs-lookup"><span data-stu-id="f0047-151">Add the following code to `app.js` to use the strategy in Passport.</span></span>

```JavaScript
passport.use(authenticationStrategy);
```

### <a name="step-3-server-configuration"></a><span data-ttu-id="f0047-152">Step 3: Server configuration</span><span class="sxs-lookup"><span data-stu-id="f0047-152">Step 3: Server configuration</span></span>
<span data-ttu-id="f0047-153">With the authentication strategy defined, you can now set up the Restify server with some basic settings and set to use Passport for security.</span><span class="sxs-lookup"><span data-stu-id="f0047-153">With the authentication strategy defined, you can now set up the Restify server with some basic settings and set to use Passport for security.</span></span>

```JavaScript
const server = restify.createServer({ name: 'Azure Active Directroy with Node.js Demo' });
server.use(restifyPlugins.authorizationParser());
server.use(passport.initialize());
server.use(passport.session());
```
<span data-ttu-id="f0047-154">This server is initialized and configured to parse authorization headers and then set to use Passport.</span><span class="sxs-lookup"><span data-stu-id="f0047-154">This server is initialized and configured to parse authorization headers and then set to use Passport.</span></span>


### <a name="step-4-define-routes"></a><span data-ttu-id="f0047-155">Step 4: Define routes</span><span class="sxs-lookup"><span data-stu-id="f0047-155">Step 4: Define routes</span></span>
<span data-ttu-id="f0047-156">You can now define routes and decide which to secure with AAD.</span><span class="sxs-lookup"><span data-stu-id="f0047-156">You can now define routes and decide which to secure with AAD.</span></span> <span data-ttu-id="f0047-157">This project includes two routes where the root level is open and the `/api` route is set to require authentication.</span><span class="sxs-lookup"><span data-stu-id="f0047-157">This project includes two routes where the root level is open and the `/api` route is set to require authentication.</span></span>

<span data-ttu-id="f0047-158">In `app.js` add the following code for the root level route:</span><span class="sxs-lookup"><span data-stu-id="f0047-158">In `app.js` add the following code for the root level route:</span></span>

```JavaScript
server.get('/', (req, res, next) => {
    res.send(200, 'Try: curl -isS -X GET http://127.0.0.1:3000/api');
    next();
});
```

<span data-ttu-id="f0047-159">The root route allows all requests through the route and returns a message that includes a command to test the `/api` route.</span><span class="sxs-lookup"><span data-stu-id="f0047-159">The root route allows all requests through the route and returns a message that includes a command to test the `/api` route.</span></span> <span data-ttu-id="f0047-160">By contrast, the `/api` route is locked down using [`passport.authenticate`](http://passportjs.org/docs/authenticate).</span><span class="sxs-lookup"><span data-stu-id="f0047-160">By contrast, the `/api` route is locked down using [`passport.authenticate`](http://passportjs.org/docs/authenticate).</span></span> <span data-ttu-id="f0047-161">Add the following code after the root route.</span><span class="sxs-lookup"><span data-stu-id="f0047-161">Add the following code after the root route.</span></span>

```JavaScript
server.get('/api', passport.authenticate('oauth-bearer', { session: false }), (req, res, next) => {
    res.json({ message: 'response from API endpoint' });
    return next();
});
```

<span data-ttu-id="f0047-162">This configuration only allows authenticated requests that include a bearer token access to `/api`.</span><span class="sxs-lookup"><span data-stu-id="f0047-162">This configuration only allows authenticated requests that include a bearer token access to `/api`.</span></span> <span data-ttu-id="f0047-163">The option of `session: false` is used to disable sessions to require that a token is passed with each request to the API.</span><span class="sxs-lookup"><span data-stu-id="f0047-163">The option of `session: false` is used to disable sessions to require that a token is passed with each request to the API.</span></span>

<span data-ttu-id="f0047-164">Finally, the server is set to listen on the configured port by calling the `listen` method.</span><span class="sxs-lookup"><span data-stu-id="f0047-164">Finally, the server is set to listen on the configured port by calling the `listen` method.</span></span>

```JavaScript
server.listen(serverPort);
```

## <a name="run-the-sample"></a><span data-ttu-id="f0047-165">Run the sample</span><span class="sxs-lookup"><span data-stu-id="f0047-165">Run the sample</span></span>

<span data-ttu-id="f0047-166">Now that the server is implemented, you can start the server by opening up a command prompt and enter:</span><span class="sxs-lookup"><span data-stu-id="f0047-166">Now that the server is implemented, you can start the server by opening up a command prompt and enter:</span></span>

```Shell
npm start
```

<span data-ttu-id="f0047-167">With the server running, you can submit a request to the server to test the results.</span><span class="sxs-lookup"><span data-stu-id="f0047-167">With the server running, you can submit a request to the server to test the results.</span></span> <span data-ttu-id="f0047-168">To demonstrate the response from the root route, open a bash shell and enter the following code:</span><span class="sxs-lookup"><span data-stu-id="f0047-168">To demonstrate the response from the root route, open a bash shell and enter the following code:</span></span>

```Shell 
curl -isS -X GET http://127.0.0.1:3000/
```

<span data-ttu-id="f0047-169">If you have configured your server correctly, the response should look similar to:</span><span class="sxs-lookup"><span data-stu-id="f0047-169">If you have configured your server correctly, the response should look similar to:</span></span>

```Shell
HTTP/1.1 200 OK
Server: Azure Active Directroy with Node.js Demo
Content-Type: application/json
Content-Length: 49
Date: Tue, 10 Oct 2017 18:35:13 GMT
Connection: keep-alive

Try: curl -isS -X GET http://127.0.0.1:3000/api
```

<span data-ttu-id="f0047-170">Next, you can test the route that requires authentication by entering the following command into your bash shell:</span><span class="sxs-lookup"><span data-stu-id="f0047-170">Next, you can test the route that requires authentication by entering the following command into your bash shell:</span></span>

```Shell 
curl -isS -X GET http://127.0.0.1:3000/api
```

<span data-ttu-id="f0047-171">If you have configured the server correctly, then the server should respond with a status of `Unauthorized`.</span><span class="sxs-lookup"><span data-stu-id="f0047-171">If you have configured the server correctly, then the server should respond with a status of `Unauthorized`.</span></span>

```Shell
HTTP/1.1 401 Unauthorized
Server: Azure Active Directroy with Node.js Demo
WWW-Authenticate: token is not found
Date: Tue, 10 Oct 2017 16:22:03 GMT
Connection: keep-alive
Content-Length: 12

Unauthorized
```
<span data-ttu-id="f0047-172">Now that you have created a secure API, you can implement a client that is able to pass authentication tokens to the API.</span><span class="sxs-lookup"><span data-stu-id="f0047-172">Now that you have created a secure API, you can implement a client that is able to pass authentication tokens to the API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f0047-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="f0047-173">Next steps</span></span>
<span data-ttu-id="f0047-174">As stated in the introduction, you must implement a client counterpart to connect to the server that handles signing in, signing out and managing tokens.</span><span class="sxs-lookup"><span data-stu-id="f0047-174">As stated in the introduction, you must implement a client counterpart to connect to the server that handles signing in, signing out and managing tokens.</span></span> <span data-ttu-id="f0047-175">For code-based examples, you may refer to the client applications in [iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios) and [Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android).</span><span class="sxs-lookup"><span data-stu-id="f0047-175">For code-based examples, you may refer to the client applications in [iOS](https://github.com/MSOpenTech/azure-activedirectory-library-for-ios) and [Android](https://github.com/MSOpenTech/azure-activedirectory-library-for-android).</span></span> <span data-ttu-id="f0047-176">For a step-by-step tutorial refer to the following article:</span><span class="sxs-lookup"><span data-stu-id="f0047-176">For a step-by-step tutorial refer to the following article:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f0047-177">Node.js web app sign-in and sign-out with Azure AD</span><span class="sxs-lookup"><span data-stu-id="f0047-177">Node.js web app sign-in and sign-out with Azure AD</span></span>](quickstart-v1-openid-connect-code.md)