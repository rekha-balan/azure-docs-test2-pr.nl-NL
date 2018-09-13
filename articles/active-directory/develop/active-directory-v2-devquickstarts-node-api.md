---
title: Azure AD v2.0 NodeJS Web API | Microsoft Docs
description: How to build a NodeJS Web API accepts tokens from both personal Microsoft Account and work or school accounts.
services: active-directory
documentationcenter: nodejs
author: xerners
manager: mbaldwin
editor: ''
ms.assetid: 0b572fc1-2aaf-4cb6-82de-63010fb1941d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 09/16/2016
ms.author: xerners
ms.openlocfilehash: 9d4eba6decd80557c877975ac65565119edd1d05
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44662285"
---
# <a name="secure-a-web-api-using-nodejs"></a><span data-ttu-id="6fd5f-103">Secure a Web API using node.js</span><span class="sxs-lookup"><span data-stu-id="6fd5f-103">Secure a Web API using node.js</span></span>
> [!NOTE]
> <span data-ttu-id="6fd5f-104">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-104">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="6fd5f-105">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="6fd5f-105">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="6fd5f-106">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-106">With Azure Active Directory the v2.0 endpoint, you can protect a Web API using [OAuth 2.0](active-directory-v2-protocols.md) access tokens, enabling users with both personal Microsoft account and work or school accounts to securely access your Web API.</span></span>

<span data-ttu-id="6fd5f-107">**Passport** is authentication middleware for Node.js.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-107">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="6fd5f-108">Extremely flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Resitify web application.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-108">Extremely flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Resitify web application.</span></span> <span data-ttu-id="6fd5f-109">A comprehensive set of strategies support authentication using a username and password, Facebook, Twitter, and more.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-109">A comprehensive set of strategies support authentication using a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="6fd5f-110">We have developed a strategy for Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-110">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="6fd5f-111">We will install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-111">We will install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="6fd5f-112">Download</span><span class="sxs-lookup"><span data-stu-id="6fd5f-112">Download</span></span>
<span data-ttu-id="6fd5f-113">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span><span class="sxs-lookup"><span data-stu-id="6fd5f-113">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs).</span></span>  <span data-ttu-id="6fd5f-114">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip) or clone the skeleton:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-114">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="6fd5f-115">The completed application is provided at the end of this tutorial as well.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-115">The completed application is provided at the end of this tutorial as well.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="6fd5f-116">1. Register an app</span><span class="sxs-lookup"><span data-stu-id="6fd5f-116">1. Register an app</span></span>
<span data-ttu-id="6fd5f-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="6fd5f-117">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="6fd5f-118">Make sure to:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-118">Make sure to:</span></span>

* <span data-ttu-id="6fd5f-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-119">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="6fd5f-120">Add the **Mobile** platform for your app.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-120">Add the **Mobile** platform for your app.</span></span>
* <span data-ttu-id="6fd5f-121">Copy down the **Redirect URI** from the portal.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-121">Copy down the **Redirect URI** from the portal.</span></span> <span data-ttu-id="6fd5f-122">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-122">You must use the default value of `urn:ietf:wg:oauth:2.0:oob`.</span></span>

## <a name="2-download-nodejs-for-your-platform"></a><span data-ttu-id="6fd5f-123">2: Download node.js for your platform</span><span class="sxs-lookup"><span data-stu-id="6fd5f-123">2: Download node.js for your platform</span></span>
<span data-ttu-id="6fd5f-124">To successfully use this sample, you must have a working installation of Node.js.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-124">To successfully use this sample, you must have a working installation of Node.js.</span></span>

<span data-ttu-id="6fd5f-125">Install Node.js from [http://nodejs.org](http://nodejs.org).</span><span class="sxs-lookup"><span data-stu-id="6fd5f-125">Install Node.js from [http://nodejs.org](http://nodejs.org).</span></span>

## <a name="3-install-mongodb-on-to-your-platform"></a><span data-ttu-id="6fd5f-126">3: Install MongoDB on to your platform</span><span class="sxs-lookup"><span data-stu-id="6fd5f-126">3: Install MongoDB on to your platform</span></span>
<span data-ttu-id="6fd5f-127">To successfully use this sample, you must have a working installation of MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-127">To successfully use this sample, you must have a working installation of MongoDB.</span></span> <span data-ttu-id="6fd5f-128">We will use MongoDB to make our REST API persistant across server instances.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-128">We will use MongoDB to make our REST API persistant across server instances.</span></span>

<span data-ttu-id="6fd5f-129">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span><span class="sxs-lookup"><span data-stu-id="6fd5f-129">Install MongoDB from [http://mongodb.org](http://www.mongodb.org).</span></span>

> [!NOTE]
> <span data-ttu-id="6fd5f-130">This walkthrough assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is: mongodb://localhost</span><span class="sxs-lookup"><span data-stu-id="6fd5f-130">This walkthrough assumes that you use the default installation and server endpoints for MongoDB, which at the time of this writing is: mongodb://localhost</span></span>
> 
> 

## <a name="4-install-the-restify-modules-in-to-your-web-api"></a><span data-ttu-id="6fd5f-131">4: Install the Restify modules in to your Web API</span><span class="sxs-lookup"><span data-stu-id="6fd5f-131">4: Install the Restify modules in to your Web API</span></span>
<span data-ttu-id="6fd5f-132">We will be using Resitfy to build our REST API.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-132">We will be using Resitfy to build our REST API.</span></span> <span data-ttu-id="6fd5f-133">Restify is a minimal and flexible Node.js application framework derived from Express that has a robust set of features for building REST APIs on top of Connect.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-133">Restify is a minimal and flexible Node.js application framework derived from Express that has a robust set of features for building REST APIs on top of Connect.</span></span>

### <a name="install-restify"></a><span data-ttu-id="6fd5f-134">Install Restify</span><span class="sxs-lookup"><span data-stu-id="6fd5f-134">Install Restify</span></span>
<span data-ttu-id="6fd5f-135">From the command-line, change directories to the azuread directory.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-135">From the command-line, change directories to the azuread directory.</span></span> <span data-ttu-id="6fd5f-136">If the **azuread** directory does not exist, create it.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-136">If the **azuread** directory does not exist, create it.</span></span>

<span data-ttu-id="6fd5f-137">`cd azuread` - or- `mkdir azuread;`</span><span class="sxs-lookup"><span data-stu-id="6fd5f-137">`cd azuread` - or- `mkdir azuread;`</span></span>

<span data-ttu-id="6fd5f-138">Type the following command:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-138">Type the following command:</span></span>

`npm install restify`

<span data-ttu-id="6fd5f-139">This command installs Restify.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-139">This command installs Restify.</span></span>

#### <a name="did-you-get-an-error"></a><span data-ttu-id="6fd5f-140">Did you get an error?</span><span class="sxs-lookup"><span data-stu-id="6fd5f-140">Did you get an error?</span></span>
<span data-ttu-id="6fd5f-141">When using npm on some operating systems, you may receive an error of Error: EPERM, chmod '/usr/local/bin/..'</span><span class="sxs-lookup"><span data-stu-id="6fd5f-141">When using npm on some operating systems, you may receive an error of Error: EPERM, chmod '/usr/local/bin/..'</span></span> <span data-ttu-id="6fd5f-142">and a request to try running the account as an administrator.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-142">and a request to try running the account as an administrator.</span></span> <span data-ttu-id="6fd5f-143">If this occurs, use the sudo command to run npm at a higher privilege level.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-143">If this occurs, use the sudo command to run npm at a higher privilege level.</span></span>

#### <a name="did-you-get-an-error-regarding-dtrace"></a><span data-ttu-id="6fd5f-144">Did you get an error regarding DTrace?</span><span class="sxs-lookup"><span data-stu-id="6fd5f-144">Did you get an error regarding DTrace?</span></span>
<span data-ttu-id="6fd5f-145">You may see something like this when installing Restify:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-145">You may see something like this when installing Restify:</span></span>

```Shell
clang: error: no such file or directory: 'HD/azuread/node_modules/restify/node_modules/dtrace-provider/libusdt'
make: *** [Release/DTraceProviderBindings.node] Error 1
gyp ERR! build error
gyp ERR! stack Error: `make` failed with exit code: 2
gyp ERR! stack     at ChildProcess.onExit (/usr/local/lib/node_modules/npm/node_modules/node-gyp/lib/build.js:267:23)
gyp ERR! stack     at ChildProcess.EventEmitter.emit (events.js:98:17)
gyp ERR! stack     at Process.ChildProcess._handle.onexit (child_process.js:789:12)
gyp ERR! System Darwin 13.1.0
gyp ERR! command "node" "/usr/local/lib/node_modules/npm/node_modules/node-gyp/bin/node-gyp.js" "rebuild"
gyp ERR! cwd /Volumes/Development HD/azuread/node_modules/restify/node_modules/dtrace-provider
gyp ERR! node -v v0.10.11
gyp ERR! node-gyp -v v0.10.0
gyp ERR! not ok
npm WARN optional dep failed, continuing dtrace-provider@0.2.8
```


<span data-ttu-id="6fd5f-146">Restify provides a powerful mechanism to trace REST calls using DTrace.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-146">Restify provides a powerful mechanism to trace REST calls using DTrace.</span></span> <span data-ttu-id="6fd5f-147">However, many operating systems do not have DTrace available.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-147">However, many operating systems do not have DTrace available.</span></span> <span data-ttu-id="6fd5f-148">You can safely ignore these errors.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-148">You can safely ignore these errors.</span></span>

<span data-ttu-id="6fd5f-149">The output of this command should appear similar to the following:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-149">The output of this command should appear similar to the following:</span></span>

    restify@2.6.1 node_modules/restify
    ├── assert-plus@0.1.4
    ├── once@1.3.0
    ├── deep-equal@0.0.0
    ├── escape-regexp-component@1.0.2
    ├── qs@0.6.5
    ├── tunnel-agent@0.3.0
    ├── keep-alive-agent@0.0.1
    ├── lru-cache@2.3.1
    ├── node-uuid@1.4.0
    ├── negotiator@0.3.0
    ├── mime@1.2.11
    ├── semver@2.2.1
    ├── spdy@1.14.12
    ├── backoff@2.3.0
    ├── formidable@1.0.14
    ├── verror@1.3.6 (extsprintf@1.0.2)
    ├── csv@0.3.6
    ├── http-signature@0.10.0 (assert-plus@0.1.2, asn1@0.1.11, ctype@0.5.2)
    └── bunyan@0.22.0(mv@0.0.5)


## <a name="5-install-passportjs-into-your-web-api"></a><span data-ttu-id="6fd5f-150">5: Install Passport.js into your Web API</span><span class="sxs-lookup"><span data-stu-id="6fd5f-150">5: Install Passport.js into your Web API</span></span>
<span data-ttu-id="6fd5f-151">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-151">[Passport](http://passportjs.org/) is authentication middleware for Node.js.</span></span> <span data-ttu-id="6fd5f-152">Extremely flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Resitify web application.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-152">Extremely flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Resitify web application.</span></span> <span data-ttu-id="6fd5f-153">A comprehensive set of strategies support authentication using a username and password, Facebook, Twitter, and more.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-153">A comprehensive set of strategies support authentication using a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="6fd5f-154">We have developed a strategy for Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-154">We have developed a strategy for Azure Active Directory.</span></span> <span data-ttu-id="6fd5f-155">We will install this module and then add the Azure Active Directory strategy plug-in.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-155">We will install this module and then add the Azure Active Directory strategy plug-in.</span></span>

<span data-ttu-id="6fd5f-156">From the command-line, change directories to the azuread directory.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-156">From the command-line, change directories to the azuread directory.</span></span>

<span data-ttu-id="6fd5f-157">Enter the following command to install passport.js</span><span class="sxs-lookup"><span data-stu-id="6fd5f-157">Enter the following command to install passport.js</span></span>

`npm install passport`

<span data-ttu-id="6fd5f-158">The output of the commadn should appear similar to the following:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-158">The output of the commadn should appear similar to the following:</span></span>

    passport@0.1.17 node_modules\passport
    ├── pause@0.0.1
    └── pkginfo@0.2.3

## <a name="6-add-passport-azure-ad-to-your-web-api"></a><span data-ttu-id="6fd5f-159">6: Add Passport-Azure-AD to your Web API</span><span class="sxs-lookup"><span data-stu-id="6fd5f-159">6: Add Passport-Azure-AD to your Web API</span></span>
<span data-ttu-id="6fd5f-160">Next, we will add the OAuth strategy, using passport-azuread, a suite of strategies that connect Azure Active Directory with  Passport.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-160">Next, we will add the OAuth strategy, using passport-azuread, a suite of strategies that connect Azure Active Directory with  Passport.</span></span> <span data-ttu-id="6fd5f-161">We will use this strategy for Bearer Tokens in this Rest API sample.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-161">We will use this strategy for Bearer Tokens in this Rest API sample.</span></span>

> [!NOTE]
> <span data-ttu-id="6fd5f-162">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained wide-spread use.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-162">Although OAuth2 provides a framework in which any known token type can be issued, only certain token types have gained wide-spread use.</span></span> <span data-ttu-id="6fd5f-163">For protecting endpoints, that has turned out to be Bearer Tokens.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-163">For protecting endpoints, that has turned out to be Bearer Tokens.</span></span> <span data-ttu-id="6fd5f-164">Bearer tokens are the most widely issued type of token in OAuth2, and many implementations assume that bearer tokens are the only type of token issued.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-164">Bearer tokens are the most widely issued type of token in OAuth2, and many implementations assume that bearer tokens are the only type of token issued.</span></span>
> 
> 

<span data-ttu-id="6fd5f-165">From the command-line, change directories to the azuread directory</span><span class="sxs-lookup"><span data-stu-id="6fd5f-165">From the command-line, change directories to the azuread directory</span></span>

<span data-ttu-id="6fd5f-166">Type the following command to install Passport.js passport-azure-ad module:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-166">Type the following command to install Passport.js passport-azure-ad module:</span></span>

`npm install passport-azure-ad`

<span data-ttu-id="6fd5f-167">The output of the command should appear similar to the following:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-167">The output of the command should appear similar to the following:</span></span>

``
passport-azure-ad@1.0.0 node_modules/passport-azure-ad
├── xtend@4.0.0
├── xmldom@0.1.19
├── passport-http-bearer@1.0.1 (passport-strategy@1.0.0)
├── underscore@1.8.3
├── async@1.3.0
├── jsonwebtoken@5.0.2
├── xml-crypto@0.5.27 (xpath.js@1.0.6)
├── ursa@0.8.5 (bindings@1.2.1, nan@1.8.4)
├── jws@3.0.0 (jwa@1.0.1, base64url@1.0.4)
├── request@2.58.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, tunnel-agent@0.4.1, oauth-sign@0.8.0, isstream@0.1.2, extend@2.0.1, json-stringify-safe@5.0.1, node-uuid@1.4.3, qs@3.1.0, combined-stream@1.0.5, mime-types@2.0.14, form-data@1.0.0-rc1, http-signature@0.11.0, bl@0.9.4, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
└── xml2js@0.4.9 (sax@0.6.1, xmlbuilder@2.6.4)
``

## <a name="7-add-mongodb-modules-to-your-web-api"></a><span data-ttu-id="6fd5f-168">7: Add MongoDB modules to your Web API</span><span class="sxs-lookup"><span data-stu-id="6fd5f-168">7: Add MongoDB modules to your Web API</span></span>
<span data-ttu-id="6fd5f-169">We will be using MongoDB as our datastore For that reason, we need to install both the widely used plug-in to manage models and schemas called Mongoose, as well as the database driver for MongoDB, also called MongoDB.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-169">We will be using MongoDB as our datastore For that reason, we need to install both the widely used plug-in to manage models and schemas called Mongoose, as well as the database driver for MongoDB, also called MongoDB.</span></span>

* `npm install mongoose`
* `npm install mongodb`

## <a name="8-install-additional-modules"></a><span data-ttu-id="6fd5f-170">8: Install additional modules</span><span class="sxs-lookup"><span data-stu-id="6fd5f-170">8: Install additional modules</span></span>
<span data-ttu-id="6fd5f-171">Next, we'll install the remaining required modules.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-171">Next, we'll install the remaining required modules.</span></span>

<span data-ttu-id="6fd5f-172">From the command-line, change directories to the **azuread** folder if not already there:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-172">From the command-line, change directories to the **azuread** folder if not already there:</span></span>

`cd azuread`

<span data-ttu-id="6fd5f-173">Enter the following commands to install the following modules in your node_modules directory:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-173">Enter the following commands to install the following modules in your node_modules directory:</span></span>

* `npm install crypto`
* `npm install assert-plus`
* `npm install posix-getopt`
* `npm install util`
* `npm install path`
* `npm install connect`
* `npm install xml-crypto`
* `npm install xml2js`
* `npm install xmldom`
* `npm install async`
* `npm install request`
* `npm install underscore`
* `npm install grunt-contrib-jshint@0.1.1`
* `npm install grunt-contrib-nodeunit@0.1.2`
* `npm install grunt-contrib-watch@0.2.0`
* `npm install grunt@0.4.1`
* `npm install xtend@2.0.3`
* `npm install bunyan`
* `npm update`

## <a name="9-create-a-serverjs-with-your-dependencies"></a><span data-ttu-id="6fd5f-174">9: Create a server.js with your dependencies</span><span class="sxs-lookup"><span data-stu-id="6fd5f-174">9: Create a server.js with your dependencies</span></span>
<span data-ttu-id="6fd5f-175">The server.js file will be providing the majority of our functionality for our Web API server.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-175">The server.js file will be providing the majority of our functionality for our Web API server.</span></span> <span data-ttu-id="6fd5f-176">We will be adding most of our code to this file.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-176">We will be adding most of our code to this file.</span></span> <span data-ttu-id="6fd5f-177">For production purposes you would refactor the functionality in to smaller files, such as separate routes and controllers.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-177">For production purposes you would refactor the functionality in to smaller files, such as separate routes and controllers.</span></span> <span data-ttu-id="6fd5f-178">For the purpose of this demo we will use server.js for this functionality.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-178">For the purpose of this demo we will use server.js for this functionality.</span></span>

<span data-ttu-id="6fd5f-179">From the command-line, change directories to the **azuread** folder if not already there:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-179">From the command-line, change directories to the **azuread** folder if not already there:</span></span>

`cd azuread`

<span data-ttu-id="6fd5f-180">Create a `server.js` file in our favorite editor and add the following information:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-180">Create a `server.js` file in our favorite editor and add the following information:</span></span>

```Javascript
'use strict';
/**
* Module dependencies.
*/
var util = require('util');
var assert = require('assert-plus');
var mongoose = require('mongoose/');
var bunyan = require('bunyan');
var restify = require('restify');
var config = require('./config');
var passport = require('passport');
var OIDCBearerStrategy = require('passport-azure-ad').OIDCStrategy;
```

<span data-ttu-id="6fd5f-181">Save the file.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-181">Save the file.</span></span> <span data-ttu-id="6fd5f-182">We will return to it shortly.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-182">We will return to it shortly.</span></span>

## <a name="10-create-a-config-file-to-store-your-azure-ad-settings"></a><span data-ttu-id="6fd5f-183">10: Create a config file to store your Azure AD settings</span><span class="sxs-lookup"><span data-stu-id="6fd5f-183">10: Create a config file to store your Azure AD settings</span></span>
<span data-ttu-id="6fd5f-184">This code file passes the configuration parameters from your Azure Active Directory Portal to Passport.js.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-184">This code file passes the configuration parameters from your Azure Active Directory Portal to Passport.js.</span></span> <span data-ttu-id="6fd5f-185">You created these configuration values when you added the Web API to the portal in the first part of the walkthrough.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-185">You created these configuration values when you added the Web API to the portal in the first part of the walkthrough.</span></span> <span data-ttu-id="6fd5f-186">We will explain what to put in the values of these parameters after you've copied the code.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-186">We will explain what to put in the values of these parameters after you've copied the code.</span></span>

<span data-ttu-id="6fd5f-187">From the command-line, change directories to the **azuread** folder if not already there:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-187">From the command-line, change directories to the **azuread** folder if not already there:</span></span>

`cd azuread`

<span data-ttu-id="6fd5f-188">Create a `config.js` file in our favorite editor and add the following information:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-188">Create a `config.js` file in our favorite editor and add the following information:</span></span>

```Javascript
// Don't commit this file to your public repos. This config is for first-run
exports.creds = {
mongoose_auth_local: 'mongodb://localhost/tasklist', // Your mongo auth uri goes here
issuer: 'https://sts.windows.net/**<your application id>**/',
audience: '<your redirect URI>',
identityMetadata: 'https://login.microsoftonline.com/common/.well-known/openid-configuration' // For using Microsoft you should never need to change this.
};

```



### <a name="required-values"></a><span data-ttu-id="6fd5f-189">Required Values</span><span class="sxs-lookup"><span data-stu-id="6fd5f-189">Required Values</span></span>
<span data-ttu-id="6fd5f-190">*IdentityMetadata*: This is where passport-azure-ad will look for your configuration data for the IdP as well as the keys to validate the JWT tokens.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-190">*IdentityMetadata*: This is where passport-azure-ad will look for your configuration data for the IdP as well as the keys to validate the JWT tokens.</span></span> <span data-ttu-id="6fd5f-191">You probably do not want to change this if using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-191">You probably do not want to change this if using Azure Active Directory.</span></span>

<span data-ttu-id="6fd5f-192">*audience*: Your redirect URI from the portal.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-192">*audience*: Your redirect URI from the portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6fd5f-193">We roll our keys at frequent intervals.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-193">We roll our keys at frequent intervals.</span></span> <span data-ttu-id="6fd5f-194">Please ensure that you are always pulling from the "openid_keys" URL and that the app can access the internet.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-194">Please ensure that you are always pulling from the "openid_keys" URL and that the app can access the internet.</span></span>
> 
> 

## <a name="11-add-configuration-to-your-serverjs-file"></a><span data-ttu-id="6fd5f-195">11: Add configuration to your server.js file</span><span class="sxs-lookup"><span data-stu-id="6fd5f-195">11: Add configuration to your server.js file</span></span>
<span data-ttu-id="6fd5f-196">We need to read these values from the Config file you just created across our application.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-196">We need to read these values from the Config file you just created across our application.</span></span> <span data-ttu-id="6fd5f-197">To do this, we simply add the .config file as a required resource in our application and then set the global variables to those in the config.js document</span><span class="sxs-lookup"><span data-stu-id="6fd5f-197">To do this, we simply add the .config file as a required resource in our application and then set the global variables to those in the config.js document</span></span>

<span data-ttu-id="6fd5f-198">From the command-line, change directories to the **azuread** folder if not already there:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-198">From the command-line, change directories to the **azuread** folder if not already there:</span></span>

`cd azuread`

<span data-ttu-id="6fd5f-199">Open your `server.js` file in our favorite editor and add the following information:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-199">Open your `server.js` file in our favorite editor and add the following information:</span></span>

```Javascript
var config = require('./config');
```
<span data-ttu-id="6fd5f-200">Then, add a new section to `server.js` with the following code:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-200">Then, add a new section to `server.js` with the following code:</span></span>

```Javascript
// We pass these options in to the ODICBearerStrategy.
var options = {
// The URL of the metadata document for your app. We will put the keys for token validation from the URL found in the jwks_uri tag of the in the metadata.
identityMetadata: config.creds.identityMetadata,
issuer: config.creds.issuer,
audience: config.creds.audience
};
// array to hold logged in users and the current logged in user (owner)
var users = [];
var owner = null;
// Our logger
var log = bunyan.createLogger({
name: 'Microsoft Azure Active Directory Sample'
});
```

## <a name="step-12-add-the-mongodb-model-and-schema-information-using-moongoose"></a><span data-ttu-id="6fd5f-201">Step 12: Add The MongoDB Model and Schema Information using Moongoose</span><span class="sxs-lookup"><span data-stu-id="6fd5f-201">Step 12: Add The MongoDB Model and Schema Information using Moongoose</span></span>
<span data-ttu-id="6fd5f-202">Now all this preparation is going to start paying off as we wind these three files together in to a REST API service.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-202">Now all this preparation is going to start paying off as we wind these three files together in to a REST API service.</span></span>

<span data-ttu-id="6fd5f-203">For this walkthrough we will be using MongoDB to store our Tasks as discussed in ***Step 4***.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-203">For this walkthrough we will be using MongoDB to store our Tasks as discussed in ***Step 4***.</span></span>

<span data-ttu-id="6fd5f-204">If you recall from the config.js file we created in Step 11, we called our database *tasklist*, as that was what we put at the end of our mogoose_auth_local connection URL.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-204">If you recall from the config.js file we created in Step 11, we called our database *tasklist*, as that was what we put at the end of our mogoose_auth_local connection URL.</span></span> <span data-ttu-id="6fd5f-205">You don't need to create this database beforehand in MongoDB, it will create this for us on first run of our server application (assuming it does not already exist).</span><span class="sxs-lookup"><span data-stu-id="6fd5f-205">You don't need to create this database beforehand in MongoDB, it will create this for us on first run of our server application (assuming it does not already exist).</span></span>

<span data-ttu-id="6fd5f-206">Now that we've told the server what MongoDB database we'd like to use, we need to write some additional code to create the model and schema for our server's Tasks.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-206">Now that we've told the server what MongoDB database we'd like to use, we need to write some additional code to create the model and schema for our server's Tasks.</span></span>

#### <a name="discussion-of-the-model"></a><span data-ttu-id="6fd5f-207">Discussion of the model</span><span class="sxs-lookup"><span data-stu-id="6fd5f-207">Discussion of the model</span></span>
<span data-ttu-id="6fd5f-208">Our Schema model is very simple, and you expand it as required.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-208">Our Schema model is very simple, and you expand it as required.</span></span>

<span data-ttu-id="6fd5f-209">NAME - The name of who is assigned to the task.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-209">NAME - The name of who is assigned to the task.</span></span> <span data-ttu-id="6fd5f-210">A ***String***</span><span class="sxs-lookup"><span data-stu-id="6fd5f-210">A ***String***</span></span>

<span data-ttu-id="6fd5f-211">TASK - The task itself.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-211">TASK - The task itself.</span></span> <span data-ttu-id="6fd5f-212">A ***String***</span><span class="sxs-lookup"><span data-stu-id="6fd5f-212">A ***String***</span></span>

<span data-ttu-id="6fd5f-213">DATE - The date that the task is due.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-213">DATE - The date that the task is due.</span></span> <span data-ttu-id="6fd5f-214">A ***DATETIME***</span><span class="sxs-lookup"><span data-stu-id="6fd5f-214">A ***DATETIME***</span></span>

<span data-ttu-id="6fd5f-215">COMPLETED - If the Task is completed or not.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-215">COMPLETED - If the Task is completed or not.</span></span> <span data-ttu-id="6fd5f-216">A ***BOOLEAN***</span><span class="sxs-lookup"><span data-stu-id="6fd5f-216">A ***BOOLEAN***</span></span>

#### <a name="creating-the-schema-in-the-code"></a><span data-ttu-id="6fd5f-217">Creating the schema in the code</span><span class="sxs-lookup"><span data-stu-id="6fd5f-217">Creating the schema in the code</span></span>
<span data-ttu-id="6fd5f-218">From the command-line, change directories to the **azuread** folder if not already there:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-218">From the command-line, change directories to the **azuread** folder if not already there:</span></span>

`cd azuread`

<span data-ttu-id="6fd5f-219">Open your `server.js` file in our favorite editor and add the following information below the configuration entry:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-219">Open your `server.js` file in our favorite editor and add the following information below the configuration entry:</span></span>

```Javascript
// MongoDB setup
// Setup some configuration
var serverPort = process.env.PORT || 8080;
var serverURI = (process.env.PORT) ? config.creds.mongoose_auth_mongohq : config.creds.mongoose_auth_local;
// Connect to MongoDB
global.db = mongoose.connect(serverURI);
var Schema = mongoose.Schema;
log.info('MongoDB Schema loaded');
```
<span data-ttu-id="6fd5f-220">This will connect to the MongoDB server and hand back a Schema object to us.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-220">This will connect to the MongoDB server and hand back a Schema object to us.</span></span>

#### <a name="using-the-schema-create-our-model-in-the-code"></a><span data-ttu-id="6fd5f-221">Using the Schema, create our model in the code</span><span class="sxs-lookup"><span data-stu-id="6fd5f-221">Using the Schema, create our model in the code</span></span>
<span data-ttu-id="6fd5f-222">Below the code you wrote above, add the following code:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-222">Below the code you wrote above, add the following code:</span></span>

```Javascript
// Here we create a schema to store our tasks and users. Pretty simple schema for now.
var TaskSchema = new Schema({
owner: String,
task: String,
completed: Boolean,
date: Date
});
// Use the schema to register a model
mongoose.model('Task', TaskSchema);
var Task = mongoose.model('Task');
```
<span data-ttu-id="6fd5f-223">As you can tell from the code, we create our Schema and then create a model object we will use to store our data throughout the code when we define our ***Routes***.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-223">As you can tell from the code, we create our Schema and then create a model object we will use to store our data throughout the code when we define our ***Routes***.</span></span>

## <a name="step-13-add-our-routes-for-our-task-rest-api-server"></a><span data-ttu-id="6fd5f-224">Step 13: Add our Routes for our Task REST API server</span><span class="sxs-lookup"><span data-stu-id="6fd5f-224">Step 13: Add our Routes for our Task REST API server</span></span>
<span data-ttu-id="6fd5f-225">Now that we have a database model to work with, let's add the routes we will use for our REST API server.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-225">Now that we have a database model to work with, let's add the routes we will use for our REST API server.</span></span>

### <a name="about-routes-in-restify"></a><span data-ttu-id="6fd5f-226">About Routes in Restify</span><span class="sxs-lookup"><span data-stu-id="6fd5f-226">About Routes in Restify</span></span>
<span data-ttu-id="6fd5f-227">Routes work in Restify in the exact same way they do using the Express stack.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-227">Routes work in Restify in the exact same way they do using the Express stack.</span></span> <span data-ttu-id="6fd5f-228">You define routes using the URI that you expect the client applicaitons to call.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-228">You define routes using the URI that you expect the client applicaitons to call.</span></span> <span data-ttu-id="6fd5f-229">Usually, you define your routes in a separate file.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-229">Usually, you define your routes in a separate file.</span></span> <span data-ttu-id="6fd5f-230">For our purposes, we will put our routes in the server.js file.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-230">For our purposes, we will put our routes in the server.js file.</span></span> <span data-ttu-id="6fd5f-231">We recommend you factor these in to their own file for production use.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-231">We recommend you factor these in to their own file for production use.</span></span>

<span data-ttu-id="6fd5f-232">A typical pattern for a Restify Route is:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-232">A typical pattern for a Restify Route is:</span></span>

```Javascript
function createObject(req, res, next) {
// do work on Object
_object.name = req.params.object; // passed value is in req.params under object
///...
return next(); // keep the server going
}
....
server.post('/service/:add/:object', createObject); // calls createObject on routes that match this.
```


<span data-ttu-id="6fd5f-233">This is the pattern at the most basic level.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-233">This is the pattern at the most basic level.</span></span> <span data-ttu-id="6fd5f-234">Resitfy (and Express) provide much deeper functionaltiy such as defining application types and doing complex routing across different endpoints.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-234">Resitfy (and Express) provide much deeper functionaltiy such as defining application types and doing complex routing across different endpoints.</span></span> <span data-ttu-id="6fd5f-235">For our purposes, we will keep these routes very simply.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-235">For our purposes, we will keep these routes very simply.</span></span>

#### <a name="add-default-routes-to-our-server"></a><span data-ttu-id="6fd5f-236">Add default routes to our server</span><span class="sxs-lookup"><span data-stu-id="6fd5f-236">Add default routes to our server</span></span>
<span data-ttu-id="6fd5f-237">We will now add the basic CRUD routes of Create, Retrieve, Update, and Delete.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-237">We will now add the basic CRUD routes of Create, Retrieve, Update, and Delete.</span></span>

<span data-ttu-id="6fd5f-238">From the command-line, change directories to the **azuread** folder if not already there:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-238">From the command-line, change directories to the **azuread** folder if not already there:</span></span>

`cd azuread`

<span data-ttu-id="6fd5f-239">Open your `server.js` file in our favorite editor and add the following information below the database entries you made above:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-239">Open your `server.js` file in our favorite editor and add the following information below the database entries you made above:</span></span>

```Javascript
/**
*
* APIs for our REST Task server
*/
// Create a task
function createTask(req, res, next) {
// Resitify currently has a bug which doesn't allow you to set default headers
// This headers comply with CORS and allow us to mongodbServer our response to any origin
res.header("Access-Control-Allow-Origin", "*");
res.header("Access-Control-Allow-Headers", "X-Requested-With");
// Create a new task model, fill it up and save it to Mongodb
var _task = new Task();
if (!req.params.task) {
req.log.warn({
params: p
}, 'createTodo: missing task');
next(new MissingTaskError());
return;
}
_task.owner = owner;
_task.task = req.params.task;
_task.date = new Date();
_task.save(function(err) {
if (err) {
req.log.warn(err, 'createTask: unable to save');
next(err);
} else {
res.send(201, _task);
}
});
return next();
}
// Delete a task by name
function removeTask(req, res, next) {
Task.remove({
task: req.params.task,
owner: owner
}, function(err) {
if (err) {
req.log.warn(err,
'removeTask: unable to delete %s',
req.params.task);
next(err);
} else {
log.info('Deleted task:', req.params.task);
res.send(204);
next();
}
});
}
// Delete all tasks
function removeAll(req, res, next) {
Task.remove();
res.send(204);
return next();
}
// Get a specific task based on name
function getTask(req, res, next) {
log.info('getTask was called for: ', owner);
Task.find({
owner: owner
}, function(err, data) {
if (err) {
req.log.warn(err, 'get: unable to read %s', owner);
next(err);
return;
}
res.json(data);
});
return next();
}
/// Simple returns the list of TODOs that were loaded.
function listTasks(req, res, next) {
// Resitify currently has a bug which doesn't allow you to set default headers
// This headers comply with CORS and allow us to mongodbServer our response to any origin
res.header("Access-Control-Allow-Origin", "*");
res.header("Access-Control-Allow-Headers", "X-Requested-With");
log.info("listTasks was called for: ", owner);
Task.find({
owner: owner
}).limit(20).sort('date').exec(function(err, data) {
if (err)
return next(err);
if (data.length > 0) {
log.info(data);
}
if (!data.length) {
log.warn(err, "There is no tasks in the database. Add one!");
}
if (!owner) {
log.warn(err, "You did not pass an owner when listing tasks.");
} else {
res.json(data);
}
});
return next();
}
```

### <a name="add-some-error-handling-for-the-routes"></a><span data-ttu-id="6fd5f-240">Add some error handling for the routes</span><span class="sxs-lookup"><span data-stu-id="6fd5f-240">Add some error handling for the routes</span></span>
<span data-ttu-id="6fd5f-241">It makes sense to add some error handling so we can communicate back to the client the problem we encountered in a way it can understand.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-241">It makes sense to add some error handling so we can communicate back to the client the problem we encountered in a way it can understand.</span></span>

<span data-ttu-id="6fd5f-242">Add the following code underneath the code you've written above:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-242">Add the following code underneath the code you've written above:</span></span>

```Javascript
///--- Errors for communicating something interesting back to the client
function MissingTaskError() {
restify.RestError.call(this, {
statusCode: 409,
restCode: 'MissingTask',
message: '"task" is a required parameter',
constructorOpt: MissingTaskError
});
this.name = 'MissingTaskError';
}
util.inherits(MissingTaskError, restify.RestError);
function TaskExistsError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 409,
restCode: 'TaskExists',
message: owner + ' already exists',
constructorOpt: TaskExistsError
});
this.name = 'TaskExistsError';
}
util.inherits(TaskExistsError, restify.RestError);
function TaskNotFoundError(owner) {
assert.string(owner, 'owner');
restify.RestError.call(this, {
statusCode: 404,
restCode: 'TaskNotFound',
message: owner + ' was not found',
constructorOpt: TaskNotFoundError
});
this.name = 'TaskNotFoundError';
}
util.inherits(TaskNotFoundError, restify.RestError);
```


## <a name="step-14-create-your-server"></a><span data-ttu-id="6fd5f-243">Step 14: Create your Server!</span><span class="sxs-lookup"><span data-stu-id="6fd5f-243">Step 14: Create your Server!</span></span>
<span data-ttu-id="6fd5f-244">We have our database defined, we have our routes in place, and the last thing to do is add our server instance that will manage our calls.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-244">We have our database defined, we have our routes in place, and the last thing to do is add our server instance that will manage our calls.</span></span>

<span data-ttu-id="6fd5f-245">Restify (and Express) have a lot of deep customization you can do for a REST API server, but again we will use the most basic setup for our purposes.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-245">Restify (and Express) have a lot of deep customization you can do for a REST API server, but again we will use the most basic setup for our purposes.</span></span>

```Javascript
/**
* Our Server
*/
var server = restify.createServer({
name: "Microsoft Azure Active Directroy TODO Server",
version: "2.0.1"
});
// Ensure we don't drop data on uploads
server.pre(restify.pre.pause());
// Clean up sloppy paths like //todo//////1//
server.pre(restify.pre.sanitizePath());
// Handles annoying user agents (curl)
server.pre(restify.pre.userAgentConnection());
// Set a per request bunyan logger (with requestid filled in)
server.use(restify.requestLogger());
// Allow 5 requests/second by IP, and burst to 10
server.use(restify.throttle({
burst: 10,
rate: 5,
ip: true,
}));
// Use the common stuff you probably want
server.use(restify.acceptParser(server.acceptable));
server.use(restify.dateParser());
server.use(restify.queryParser());
server.use(restify.gzipResponse());
server.use(restify.bodyParser({
mapParams: true
}));
```
## <a name="15-adding-the-routes-without-authentication-for-now"></a><span data-ttu-id="6fd5f-246">15: Adding the routes (without authentication for now)</span><span class="sxs-lookup"><span data-stu-id="6fd5f-246">15: Adding the routes (without authentication for now)</span></span>
```Javascript
/// Now the real handlers. Here we just CRUD
/**
/*
/* Each of these handlers are protected by our OIDCBearerStrategy by invoking 'oidc-bearer'
/* in the pasport.authenticate() method. We set 'session: false' as REST is stateless and
/* we don't need to maintain session state. You can experiement removing API protection
/* by removing the passport.authenticate() method like so:
/*
/* server.get('/tasks', listTasks);
/*
**/
server.get('/tasks', listTasks);
server.get('/tasks', listTasks);
server.get('/tasks/:owner', getTask);
server.head('/tasks/:owner', getTask);
server.post('/tasks/:owner/:task', createTask);
server.post('/tasks', createTask);
server.del('/tasks/:owner/:task', removeTask);
server.del('/tasks/:owner', removeTask);
server.del('/tasks', removeTask);
server.del('/tasks', removeAll, function respond(req, res, next) {
res.send(204);
next();
});
// Register a default '/' handler
server.get('/', function root(req, res, next) {
var routes = [
'GET /',
'POST /tasks/:owner/:task',
'POST /tasks (for JSON body)',
'GET /tasks',
'PUT /tasks/:owner',
'GET /tasks/:owner',
'DELETE /tasks/:owner/:task'
];
res.send(200, routes);
next();
});
server.listen(serverPort, function() {
var consoleMessage = '\n Microsoft Azure Active Directory Tutorial';
consoleMessage += '\n +++++++++++++++++++++++++++++++++++++++++++++++++++++';
consoleMessage += '\n %s server is listening at %s';
consoleMessage += '\n Open your browser to %s/tasks\n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n';
consoleMessage += '\n !!! why not try a $curl -isS %s | json to get some ideas? \n';
consoleMessage += '+++++++++++++++++++++++++++++++++++++++++++++++++++++ \n\n';
});
```
## <a name="16-before-we-add-oauth-support-lets-run-the-server"></a><span data-ttu-id="6fd5f-247">16: Before we add OAuth support, let's run the server.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-247">16: Before we add OAuth support, let's run the server.</span></span>
<span data-ttu-id="6fd5f-248">Test out your server before we add authentication</span><span class="sxs-lookup"><span data-stu-id="6fd5f-248">Test out your server before we add authentication</span></span>

<span data-ttu-id="6fd5f-249">The easiest way to do this is by using curl in a command line.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-249">The easiest way to do this is by using curl in a command line.</span></span> <span data-ttu-id="6fd5f-250">Before we do that, we need a simple utility that allows us to parse output as JSON.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-250">Before we do that, we need a simple utility that allows us to parse output as JSON.</span></span> <span data-ttu-id="6fd5f-251">To do that, install the json tool as all the examples below use that.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-251">To do that, install the json tool as all the examples below use that.</span></span>

`$npm install -g jsontool`

<span data-ttu-id="6fd5f-252">This installs the JSON tool globally.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-252">This installs the JSON tool globally.</span></span> <span data-ttu-id="6fd5f-253">Now that we’ve accomplished that – let’s play with the server:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-253">Now that we’ve accomplished that – let’s play with the server:</span></span>

<span data-ttu-id="6fd5f-254">First, make sure that your monogoDB isntance is running..</span><span class="sxs-lookup"><span data-stu-id="6fd5f-254">First, make sure that your monogoDB isntance is running..</span></span>

`$sudo mongod`

<span data-ttu-id="6fd5f-255">Then, change to the directory and start curling..</span><span class="sxs-lookup"><span data-stu-id="6fd5f-255">Then, change to the directory and start curling..</span></span>

`$ cd azuread`
`$ node server.js`

`$ curl -isS http://127.0.0.1:8080 | json`

```Shell
HTTP/1.1 2.0OK
Connection: close
Content-Type: application/json
Content-Length: 171
Date: Tue, 14 Jul 2015 05:43:38 GMT
[
"GET /",
"POST /tasks/:owner/:task",
"POST /tasks (for JSON body)",
"GET /tasks",
"PUT /tasks/:owner",
"GET /tasks/:owner",
"DELETE /tasks/:owner/:task"
]
```

<span data-ttu-id="6fd5f-256">Then, we can add a task this way:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-256">Then, we can add a task this way:</span></span>

`$ curl -isS -X POST http://127.0.0.1:8888/tasks/brandon/Hello`

<span data-ttu-id="6fd5f-257">The response should be:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-257">The response should be:</span></span>

```Shell
HTTP/1.1 201 Created
Connection: close
Access-Control-Allow-Origin: *
Access-Control-Allow-Headers: X-Requested-With
Content-Type: application/x-www-form-urlencoded
Content-Length: 5
Date: Tue, 04 Feb 2014 01:02:26 GMT
Hello
```
<span data-ttu-id="6fd5f-258">And we can list tasks for Brandon this way:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-258">And we can list tasks for Brandon this way:</span></span>

`$ curl -isS http://127.0.0.1:8080/tasks/brandon/`

<span data-ttu-id="6fd5f-259">If all this works out, we are ready to add OAuth to the REST API server.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-259">If all this works out, we are ready to add OAuth to the REST API server.</span></span>

<span data-ttu-id="6fd5f-260">**You have a REST API server with MongoDB!**</span><span class="sxs-lookup"><span data-stu-id="6fd5f-260">**You have a REST API server with MongoDB!**</span></span>

## <a name="17-add-authentication-to-our-rest-api-server"></a><span data-ttu-id="6fd5f-261">17: Add Authentication to our REST API Server</span><span class="sxs-lookup"><span data-stu-id="6fd5f-261">17: Add Authentication to our REST API Server</span></span>
<span data-ttu-id="6fd5f-262">Now that we have a running REST API (congrats, btw!) let's get to making it useful against Azure AD.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-262">Now that we have a running REST API (congrats, btw!) let's get to making it useful against Azure AD.</span></span>

<span data-ttu-id="6fd5f-263">From the command-line, change directories to the **azuread** folder if not already there:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-263">From the command-line, change directories to the **azuread** folder if not already there:</span></span>

`cd azuread`

### <a name="1-use-the-oidcbearerstrategy-that-is-included-with-passport-azure-ad"></a><span data-ttu-id="6fd5f-264">1: Use the oidcbearerstrategy that is included with passport-azure-ad</span><span class="sxs-lookup"><span data-stu-id="6fd5f-264">1: Use the oidcbearerstrategy that is included with passport-azure-ad</span></span>
<span data-ttu-id="6fd5f-265">So far we have built a typical REST TODO server without any kind of authorization.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-265">So far we have built a typical REST TODO server without any kind of authorization.</span></span> <span data-ttu-id="6fd5f-266">This is where we start putting that together.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-266">This is where we start putting that together.</span></span>

<span data-ttu-id="6fd5f-267">First, we need to indicate that we want to use Passport.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-267">First, we need to indicate that we want to use Passport.</span></span> <span data-ttu-id="6fd5f-268">Put this right after your other server configuration:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-268">Put this right after your other server configuration:</span></span>

```Javascript
// Let's start using Passport.js

server.use(passport.initialize()); // Starts passport
server.use(passport.session()); // Provides session support
```

> [!TIP]
> <span data-ttu-id="6fd5f-269">When writing APIs you should always link the data to something unique from the token that the user can’t spoof.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-269">When writing APIs you should always link the data to something unique from the token that the user can’t spoof.</span></span> <span data-ttu-id="6fd5f-270">When this server stores TODO items, it stores them based on the subscription ID of the user in the token (called through token.sub) which we put in the “owner” field.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-270">When this server stores TODO items, it stores them based on the subscription ID of the user in the token (called through token.sub) which we put in the “owner” field.</span></span> <span data-ttu-id="6fd5f-271">This ensures that only that user can access his TODOs and no one else can access the TODOs entered.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-271">This ensures that only that user can access his TODOs and no one else can access the TODOs entered.</span></span> <span data-ttu-id="6fd5f-272">There is no exposure in the API of “owner” so an external user can request other’s TODOs even if they are authenticated.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-272">There is no exposure in the API of “owner” so an external user can request other’s TODOs even if they are authenticated.</span></span>
> 
> 

<span data-ttu-id="6fd5f-273">Next, let’s use the Open ID Connect Bearer strategy that comes with passport-azure-ad.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-273">Next, let’s use the Open ID Connect Bearer strategy that comes with passport-azure-ad.</span></span> <span data-ttu-id="6fd5f-274">Just look at the code for now, I’ll explain it shortly.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-274">Just look at the code for now, I’ll explain it shortly.</span></span> <span data-ttu-id="6fd5f-275">Put this after what you pated above:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-275">Put this after what you pated above:</span></span>

```Javascript
/**
/*
/* Calling the OIDCBearerStrategy and managing users
/*
/* Passport pattern provides the need to manage users and info tokens
/* with a FindorCreate() method that must be provided by the implementor.
/* Here we just autoregister any user and implement a FindById().
/* You'll want to do something smarter.
**/
var findById = function(id, fn) {
for (var i = 0, len = users.length; i < len; i++) {
var user = users[i];
if (user.sub === id) {
log.info('Found user: ', user);
return fn(null, user);
}
}
return fn(null, null);
};
var oidcStrategy = new OIDCBearerStrategy(options,
function(token, done) {
log.info('verifying the user');
log.info(token, 'was the token retreived');
findById(token.sub, function(err, user) {
if (err) {
return done(err);
}
if (!user) {
// "Auto-registration"
log.info('User was added automatically as they were new. Their sub is: ', token.sub);
users.push(token);
owner = token.sub;
return done(null, token);
}
owner = token.sub;
return done(null, user, token);
});
}
);
passport.use(oidcStrategy);
```

<span data-ttu-id="6fd5f-276">Passport uses a similar pattern for all it’s Strategies (Twitter, Facebook, etc.) that all Strategy writers adhere to.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-276">Passport uses a similar pattern for all it’s Strategies (Twitter, Facebook, etc.) that all Strategy writers adhere to.</span></span> <span data-ttu-id="6fd5f-277">Looking at the strategy you see we pass it a function() that has a token and a done as the parameters.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-277">Looking at the strategy you see we pass it a function() that has a token and a done as the parameters.</span></span> <span data-ttu-id="6fd5f-278">The strategy will dutifully come back to us once it does all it’s work.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-278">The strategy will dutifully come back to us once it does all it’s work.</span></span> <span data-ttu-id="6fd5f-279">Once it does we’ll want to store the user and stash the token so we won’t need to ask for it again.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-279">Once it does we’ll want to store the user and stash the token so we won’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6fd5f-280">The code above takes any user that happens to authenticate to our server.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-280">The code above takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="6fd5f-281">This is known as auto registration.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-281">This is known as auto registration.</span></span> <span data-ttu-id="6fd5f-282">In production servers you wouldn’t want to let anyone in without first having them go through a registration process you decide.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-282">In production servers you wouldn’t want to let anyone in without first having them go through a registration process you decide.</span></span> <span data-ttu-id="6fd5f-283">This is usually the pattern you see in consumer apps who allow you to register with Facebook but then ask you to fill out additional information.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-283">This is usually the pattern you see in consumer apps who allow you to register with Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="6fd5f-284">If this wasn’t a command line program, we could have just extracted the email from the token object that is returned and then asked them to fill out additional information.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-284">If this wasn’t a command line program, we could have just extracted the email from the token object that is returned and then asked them to fill out additional information.</span></span> <span data-ttu-id="6fd5f-285">Since this is a test server we simply add them to the in-memory database.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-285">Since this is a test server we simply add them to the in-memory database.</span></span>
> 
> 

### <a name="2-finally-protect-some-endpoints"></a><span data-ttu-id="6fd5f-286">2. Finally, protect some endpoints</span><span class="sxs-lookup"><span data-stu-id="6fd5f-286">2. Finally, protect some endpoints</span></span>
<span data-ttu-id="6fd5f-287">You protect endpoints by specifying the passport.authenticate() call with the protocol you wish to use.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-287">You protect endpoints by specifying the passport.authenticate() call with the protocol you wish to use.</span></span>

<span data-ttu-id="6fd5f-288">Let’s edit our route in our server code to do something more interesting:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-288">Let’s edit our route in our server code to do something more interesting:</span></span>

```Javascript
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), listTasks);
server.get('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.head('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), getTask);
server.post('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.post('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), createTask);
server.del('/tasks/:owner/:task', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks/:owner', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeTask);
server.del('/tasks', passport.authenticate('oidc-bearer', {
session: false
}), removeAll, function respond(req, res, next) {
res.send(204);
next();
});
```

## <a name="18-run-your-server-application-again-and-ensure-it-rejects-you"></a><span data-ttu-id="6fd5f-289">18: Run your server application again and ensure it rejects you</span><span class="sxs-lookup"><span data-stu-id="6fd5f-289">18: Run your server application again and ensure it rejects you</span></span>
<span data-ttu-id="6fd5f-290">Let's use `curl` again to see if we now have OAuth2 protection against our endpoints.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-290">Let's use `curl` again to see if we now have OAuth2 protection against our endpoints.</span></span> <span data-ttu-id="6fd5f-291">We will do this before runnning any of our client SDKs against this endpoint.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-291">We will do this before runnning any of our client SDKs against this endpoint.</span></span> <span data-ttu-id="6fd5f-292">The headers returned should be enough to tell us we are down the right path.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-292">The headers returned should be enough to tell us we are down the right path.</span></span>

<span data-ttu-id="6fd5f-293">First, make sure that your monogoDB isntance is running..</span><span class="sxs-lookup"><span data-stu-id="6fd5f-293">First, make sure that your monogoDB isntance is running..</span></span>

    $sudo mongod

<span data-ttu-id="6fd5f-294">Then, change to the directory and start curling..</span><span class="sxs-lookup"><span data-stu-id="6fd5f-294">Then, change to the directory and start curling..</span></span>

    $ cd azuread
    $ node server.js

<span data-ttu-id="6fd5f-295">Try a basic POST:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-295">Try a basic POST:</span></span>

`$ curl -isS -X POST http://127.0.0.1:8080/tasks/brandon/Hello`

```Shell
HTTP/1.1 401 Unauthorized
Connection: close
WWW-Authenticate: Bearer realm="Users"
Date: Tue, 14 Jul 2015 05:45:03 GMT
Transfer-Encoding: chunked
```

<span data-ttu-id="6fd5f-296">A 401 is the response you are looking for here, as that indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-296">A 401 is the response you are looking for here, as that indicates that the Passport layer is trying to redirect to the authorize endpoint, which is exactly what you want.</span></span>

## <a name="congratulations-you-have-a-rest-api-service-using-oauth2"></a><span data-ttu-id="6fd5f-297">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="6fd5f-297">Congratulations!</span></span> <span data-ttu-id="6fd5f-298">You have a REST API Service using OAuth2!</span><span class="sxs-lookup"><span data-stu-id="6fd5f-298">You have a REST API Service using OAuth2!</span></span>
<span data-ttu-id="6fd5f-299">You've went as far as you can with this server without using an OAuth2 compatible client.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-299">You've went as far as you can with this server without using an OAuth2 compatible client.</span></span> <span data-ttu-id="6fd5f-300">You will need to go through an additional walkthrough.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-300">You will need to go through an additional walkthrough.</span></span>

<span data-ttu-id="6fd5f-301">If you were just looking for information on how to implement a REST API using Restify and OAuth2, you have more than enough code to keep developing your service and learning how to build on this example.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-301">If you were just looking for information on how to implement a REST API using Restify and OAuth2, you have more than enough code to keep developing your service and learning how to build on this example.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fd5f-302">Next Steps</span><span class="sxs-lookup"><span data-stu-id="6fd5f-302">Next Steps</span></span>
<span data-ttu-id="6fd5f-303">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip), or you can clone it from GitHub:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-303">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebAPI-nodejs.git```

<span data-ttu-id="6fd5f-304">You can now move onto more advanced topics.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-304">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="6fd5f-305">You may want to try:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-305">You may want to try:</span></span>

[<span data-ttu-id="6fd5f-306">Secure a Node.js web app using the v2.0 endpoint >></span><span class="sxs-lookup"><span data-stu-id="6fd5f-306">Secure a Node.js web app using the v2.0 endpoint >></span></span>](active-directory-v2-devquickstarts-node-web.md)

<span data-ttu-id="6fd5f-307">For additional resources, check out:</span><span class="sxs-lookup"><span data-stu-id="6fd5f-307">For additional resources, check out:</span></span>

* [<span data-ttu-id="6fd5f-308">The v2.0 developer guide >></span><span class="sxs-lookup"><span data-stu-id="6fd5f-308">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="6fd5f-309">StackOverflow "azure-active-directory" tag >></span><span class="sxs-lookup"><span data-stu-id="6fd5f-309">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="6fd5f-310">Get security updates for our products</span><span class="sxs-lookup"><span data-stu-id="6fd5f-310">Get security updates for our products</span></span>
<span data-ttu-id="6fd5f-311">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="6fd5f-311">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

