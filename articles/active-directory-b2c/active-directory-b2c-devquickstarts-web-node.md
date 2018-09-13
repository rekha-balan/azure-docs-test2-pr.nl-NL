---
title: Add sign-in to a Node.js web app for Azure B2C | Microsoft Docs
description: How to build a Node.js web app that signs in users by using a B2C tenant.
services: active-directory-b2c
documentationcenter: ''
author: xerners
manager: mbaldwin
editor: ''
ms.assetid: db97f84a-1f24-447b-b6d2-0265c6896b27
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: hero-article
ms.date: 03/10/2017
ms.author: xerners
ms.openlocfilehash: a4d9394983539da52105bda6cf06273205f8b0ad
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551320"
---
# <a name="azure-ad-b2c-add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="62eb4-103">Azure AD B2C: Add sign-in to a Node.js web app</span><span class="sxs-lookup"><span data-stu-id="62eb4-103">Azure AD B2C: Add sign-in to a Node.js web app</span></span>

<span data-ttu-id="62eb4-104">**Passport** is authentication middleware for Node.js.</span><span class="sxs-lookup"><span data-stu-id="62eb4-104">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="62eb4-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span><span class="sxs-lookup"><span data-stu-id="62eb4-105">Extremely flexible and modular, Passport can be unobtrusively installed in any Express-based or Restify web application.</span></span> <span data-ttu-id="62eb4-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span><span class="sxs-lookup"><span data-stu-id="62eb4-106">A comprehensive set of strategies supports authentication by using a user name and password, Facebook, Twitter, and more.</span></span> 

<span data-ttu-id="62eb4-107">We have developed a strategy for Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="62eb4-107">We have developed a strategy for Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="62eb4-108">You will install this module and then add the Azure AD `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="62eb4-108">You will install this module and then add the Azure AD `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="62eb4-109">To do this, you need to:</span><span class="sxs-lookup"><span data-stu-id="62eb4-109">To do this, you need to:</span></span>

1. <span data-ttu-id="62eb4-110">Register an application by using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62eb4-110">Register an application by using Azure AD.</span></span>
2. <span data-ttu-id="62eb4-111">Set up your app to use the `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="62eb4-111">Set up your app to use the `passport-azure-ad` plug-in.</span></span>
3. <span data-ttu-id="62eb4-112">Use Passport to issue sign-in and sign-out requests to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="62eb4-112">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="62eb4-113">Print user data.</span><span class="sxs-lookup"><span data-stu-id="62eb4-113">Print user data.</span></span>

<span data-ttu-id="62eb4-114">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="62eb4-114">The code for this tutorial [is maintained on GitHub](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="62eb4-115">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span><span class="sxs-lookup"><span data-stu-id="62eb4-115">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip).</span></span> <span data-ttu-id="62eb4-116">You can also clone the skeleton:</span><span class="sxs-lookup"><span data-stu-id="62eb4-116">You can also clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="62eb4-117">The completed application is provided at the end of this tutorial.</span><span class="sxs-lookup"><span data-stu-id="62eb4-117">The completed application is provided at the end of this tutorial.</span></span>

## <a name="get-an-azure-ad-b2c-directory"></a><span data-ttu-id="62eb4-118">Get an Azure AD B2C directory</span><span class="sxs-lookup"><span data-stu-id="62eb4-118">Get an Azure AD B2C directory</span></span>

<span data-ttu-id="62eb4-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span><span class="sxs-lookup"><span data-stu-id="62eb4-119">Before you can use Azure AD B2C, you must create a directory, or tenant.</span></span>  <span data-ttu-id="62eb4-120">A directory is a container for all of your users, apps, groups, and more.</span><span class="sxs-lookup"><span data-stu-id="62eb4-120">A directory is a container for all of your users, apps, groups, and more.</span></span> <span data-ttu-id="62eb4-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span><span class="sxs-lookup"><span data-stu-id="62eb4-121">If you don't have one already, [create a B2C directory](active-directory-b2c-get-started.md) before you continue in this guide.</span></span>

## <a name="create-an-application"></a><span data-ttu-id="62eb4-122">Create an application</span><span class="sxs-lookup"><span data-stu-id="62eb4-122">Create an application</span></span>

<span data-ttu-id="62eb4-123">Next, you need to create an app in your B2C directory.</span><span class="sxs-lookup"><span data-stu-id="62eb4-123">Next, you need to create an app in your B2C directory.</span></span> <span data-ttu-id="62eb4-124">This gives Azure AD information that it needs to communicate securely with your app.</span><span class="sxs-lookup"><span data-stu-id="62eb4-124">This gives Azure AD information that it needs to communicate securely with your app.</span></span> <span data-ttu-id="62eb4-125">Both the client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span><span class="sxs-lookup"><span data-stu-id="62eb4-125">Both the client app and web API will be represented by a single **Application ID**, because they comprise one logical app.</span></span> <span data-ttu-id="62eb4-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="62eb4-126">To create an app, follow [these instructions](active-directory-b2c-app-registration.md).</span></span> <span data-ttu-id="62eb4-127">Be sure to:</span><span class="sxs-lookup"><span data-stu-id="62eb4-127">Be sure to:</span></span>

- <span data-ttu-id="62eb4-128">Include a **web app**/**web API** in the application.</span><span class="sxs-lookup"><span data-stu-id="62eb4-128">Include a **web app**/**web API** in the application.</span></span>
- <span data-ttu-id="62eb4-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span><span class="sxs-lookup"><span data-stu-id="62eb4-129">Enter `http://localhost:3000/auth/openid/return` as a **Reply URL**.</span></span> <span data-ttu-id="62eb4-130">It is the default URL for this code sample.</span><span class="sxs-lookup"><span data-stu-id="62eb4-130">It is the default URL for this code sample.</span></span>
- <span data-ttu-id="62eb4-131">Create an **Application secret** for your application and copy it.</span><span class="sxs-lookup"><span data-stu-id="62eb4-131">Create an **Application secret** for your application and copy it.</span></span> <span data-ttu-id="62eb4-132">You will need it later.</span><span class="sxs-lookup"><span data-stu-id="62eb4-132">You will need it later.</span></span> <span data-ttu-id="62eb4-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span><span class="sxs-lookup"><span data-stu-id="62eb4-133">Note that this value needs to be [XML escaped](https://www.w3.org/TR/2006/REC-xml11-20060816/#dt-escape) before you use it.</span></span>
- <span data-ttu-id="62eb4-134">Copy the **Application ID** that is assigned to your app.</span><span class="sxs-lookup"><span data-stu-id="62eb4-134">Copy the **Application ID** that is assigned to your app.</span></span> <span data-ttu-id="62eb4-135">You'll also need this later.</span><span class="sxs-lookup"><span data-stu-id="62eb4-135">You'll also need this later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-v2-apps](../../includes/active-directory-b2c-devquickstarts-v2-apps.md)]

## <a name="create-your-policies"></a><span data-ttu-id="62eb4-136">Create your policies</span><span class="sxs-lookup"><span data-stu-id="62eb4-136">Create your policies</span></span>

<span data-ttu-id="62eb4-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span><span class="sxs-lookup"><span data-stu-id="62eb4-137">In Azure AD B2C, every user experience is defined by a [policy](active-directory-b2c-reference-policies.md).</span></span> <span data-ttu-id="62eb4-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span><span class="sxs-lookup"><span data-stu-id="62eb4-138">This app contains three identity experiences: sign up, sign in, and sign in by using Facebook.</span></span> <span data-ttu-id="62eb4-139">You need to create this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span><span class="sxs-lookup"><span data-stu-id="62eb4-139">You need to create this policy of each type, as described in the [policy reference article](active-directory-b2c-reference-policies.md#create-a-sign-up-policy).</span></span> <span data-ttu-id="62eb4-140">When you create your three policies, be sure to:</span><span class="sxs-lookup"><span data-stu-id="62eb4-140">When you create your three policies, be sure to:</span></span>

- <span data-ttu-id="62eb4-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span><span class="sxs-lookup"><span data-stu-id="62eb4-141">Choose the **Display name** and other sign-up attributes in your sign-up policy.</span></span>
- <span data-ttu-id="62eb4-142">Choose the **Display name** and **Object ID** application claims in every policy.</span><span class="sxs-lookup"><span data-stu-id="62eb4-142">Choose the **Display name** and **Object ID** application claims in every policy.</span></span> <span data-ttu-id="62eb4-143">You can choose other claims as well.</span><span class="sxs-lookup"><span data-stu-id="62eb4-143">You can choose other claims as well.</span></span>
- <span data-ttu-id="62eb4-144">Copy the **Name** of each policy after you create it.</span><span class="sxs-lookup"><span data-stu-id="62eb4-144">Copy the **Name** of each policy after you create it.</span></span> <span data-ttu-id="62eb4-145">It should have the prefix `b2c_1_`.</span><span class="sxs-lookup"><span data-stu-id="62eb4-145">It should have the prefix `b2c_1_`.</span></span>  <span data-ttu-id="62eb4-146">You'll need these policy names later.</span><span class="sxs-lookup"><span data-stu-id="62eb4-146">You'll need these policy names later.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-policy](../../includes/active-directory-b2c-devquickstarts-policy.md)]

<span data-ttu-id="62eb4-147">After you create your three policies, you're ready to build your app.</span><span class="sxs-lookup"><span data-stu-id="62eb4-147">After you create your three policies, you're ready to build your app.</span></span>

<span data-ttu-id="62eb4-148">Note that this article does not cover how to use the policies you just created.</span><span class="sxs-lookup"><span data-stu-id="62eb4-148">Note that this article does not cover how to use the policies you just created.</span></span> <span data-ttu-id="62eb4-149">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="62eb4-149">To learn about how policies work in Azure AD B2C, start with the [.NET web app getting started tutorial](active-directory-b2c-devquickstarts-web-dotnet.md).</span></span>

## <a name="add-prerequisites-to-your-directory"></a><span data-ttu-id="62eb4-150">Add prerequisites to your directory</span><span class="sxs-lookup"><span data-stu-id="62eb4-150">Add prerequisites to your directory</span></span>

<span data-ttu-id="62eb4-151">From the command line, change directories to your root folder, if you're not already there.</span><span class="sxs-lookup"><span data-stu-id="62eb4-151">From the command line, change directories to your root folder, if you're not already there.</span></span> <span data-ttu-id="62eb4-152">Run the following commands:</span><span class="sxs-lookup"><span data-stu-id="62eb4-152">Run the following commands:</span></span>

- `npm install express`
- `npm install ejs`
- `npm install ejs-locals`
- `npm install restify`
- `npm install mongoose`
- `npm install bunyan`
- `npm install assert-plus`
- `npm install passport`
- `npm install webfinger`
- `npm install body-parser`
- `npm install express-session`
- `npm install cookie-parser`

<span data-ttu-id="62eb4-153">In addition, we used `passport-azure-ad` for our preview in the skeleton of the Quickstart.</span><span class="sxs-lookup"><span data-stu-id="62eb4-153">In addition, we used `passport-azure-ad` for our preview in the skeleton of the Quickstart.</span></span>

- `npm install passport-azure-ad`

<span data-ttu-id="62eb4-154">This will install the libraries that `passport-azure-ad` depends on.</span><span class="sxs-lookup"><span data-stu-id="62eb4-154">This will install the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="set-up-your-app-to-use-the-passport-nodejs-strategy"></a><span data-ttu-id="62eb4-155">Set up your app to use the Passport-Node.js strategy</span><span class="sxs-lookup"><span data-stu-id="62eb4-155">Set up your app to use the Passport-Node.js strategy</span></span>
<span data-ttu-id="62eb4-156">Configure the Express middleware to use the OpenID Connect authentication protocol.</span><span class="sxs-lookup"><span data-stu-id="62eb4-156">Configure the Express middleware to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="62eb4-157">Passport will be used to issue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span><span class="sxs-lookup"><span data-stu-id="62eb4-157">Passport will be used to issue sign-in and sign-out requests, manage user sessions, and get information about users, among other actions.</span></span>

<span data-ttu-id="62eb4-158">Open the `config.js` file in the root of the project and enter your app's configuration values in the `exports.creds` section.</span><span class="sxs-lookup"><span data-stu-id="62eb4-158">Open the `config.js` file in the root of the project and enter your app's configuration values in the `exports.creds` section.</span></span>
- <span data-ttu-id="62eb4-159">`clientID`: The **Application ID** assigned to your app in the registration portal.</span><span class="sxs-lookup"><span data-stu-id="62eb4-159">`clientID`: The **Application ID** assigned to your app in the registration portal.</span></span>
- <span data-ttu-id="62eb4-160">`returnURL`: The **Redirect URI** you entered in the portal.</span><span class="sxs-lookup"><span data-stu-id="62eb4-160">`returnURL`: The **Redirect URI** you entered in the portal.</span></span>
- <span data-ttu-id="62eb4-161">`tenantName`: The tenant name of your app, for example, **contoso.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="62eb4-161">`tenantName`: The tenant name of your app, for example, **contoso.onmicrosoft.com**.</span></span>

[!INCLUDE [active-directory-b2c-devquickstarts-tenant-name](../../includes/active-directory-b2c-devquickstarts-tenant-name.md)]

<span data-ttu-id="62eb4-162">Open the `app.js` file in the root of the project.</span><span class="sxs-lookup"><span data-stu-id="62eb4-162">Open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="62eb4-163">Add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="62eb4-163">Add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>


```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

<span data-ttu-id="62eb4-164">Use the strategy you just referenced to handle sign-in requests.</span><span class="sxs-lookup"><span data-stu-id="62eb4-164">Use the strategy you just referenced to handle sign-in requests.</span></span>

```JavaScript
// Use the OIDCStrategy in Passport (Section 2).
//
//   Strategies in Passport require a "validate" function that accepts
//   credentials (in this case, an OpenID identifier), and invokes a callback
//   by using a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    skipUserProfile: config.creds.skipUserProfile,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    tenantName: config.creds.tenantName
  },
  function(iss, sub, profile, accessToken, refreshToken, done) {
    log.info('Example: Email address we received was: ', profile.email);
    // asynchronous verification, for effect...
    process.nextTick(function () {
      findByEmail(profile.email, function(err, user) {
        if (err) {
          return done(err);
        }
        if (!user) {
          // "Auto-registration"
          users.push(profile);
          return done(null, profile);
        }
        return done(null, user);
      });
    });
  }
));
```
<span data-ttu-id="62eb4-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span><span class="sxs-lookup"><span data-stu-id="62eb4-165">Passport uses a similar pattern for all of its strategies (including Twitter and Facebook).</span></span> <span data-ttu-id="62eb4-166">All strategy writers adhere to this pattern.</span><span class="sxs-lookup"><span data-stu-id="62eb4-166">All strategy writers adhere to this pattern.</span></span> <span data-ttu-id="62eb4-167">When you look at the strategy, you can see that you pass it a `function()` that has a token and a `done` as the parameters.</span><span class="sxs-lookup"><span data-stu-id="62eb4-167">When you look at the strategy, you can see that you pass it a `function()` that has a token and a `done` as the parameters.</span></span> <span data-ttu-id="62eb4-168">The strategy comes back to you after it has done all of its work.</span><span class="sxs-lookup"><span data-stu-id="62eb4-168">The strategy comes back to you after it has done all of its work.</span></span> <span data-ttu-id="62eb4-169">Store the user and stash the token so that you don’t need to ask for it again.</span><span class="sxs-lookup"><span data-stu-id="62eb4-169">Store the user and stash the token so that you don’t need to ask for it again.</span></span>

> [!IMPORTANT]
<span data-ttu-id="62eb4-170">The preceding code takes all users whom the server authenticates.</span><span class="sxs-lookup"><span data-stu-id="62eb4-170">The preceding code takes all users whom the server authenticates.</span></span> <span data-ttu-id="62eb4-171">This is autoregistration.</span><span class="sxs-lookup"><span data-stu-id="62eb4-171">This is autoregistration.</span></span> <span data-ttu-id="62eb4-172">When you use production servers, you don’t want to let in users unless they have gone through a registration process that you have set up.</span><span class="sxs-lookup"><span data-stu-id="62eb4-172">When you use production servers, you don’t want to let in users unless they have gone through a registration process that you have set up.</span></span> <span data-ttu-id="62eb4-173">You can often see this pattern in consumer apps.</span><span class="sxs-lookup"><span data-stu-id="62eb4-173">You can often see this pattern in consumer apps.</span></span> <span data-ttu-id="62eb4-174">These allow you to register by using Facebook, but then they ask you to fill out additional information.</span><span class="sxs-lookup"><span data-stu-id="62eb4-174">These allow you to register by using Facebook, but then they ask you to fill out additional information.</span></span> <span data-ttu-id="62eb4-175">If our application wasn’t a sample, we could extract an email address from the token object that is returned, and then ask the user to fill out additional information.</span><span class="sxs-lookup"><span data-stu-id="62eb4-175">If our application wasn’t a sample, we could extract an email address from the token object that is returned, and then ask the user to fill out additional information.</span></span> <span data-ttu-id="62eb4-176">Because this is a test server, we simply add users to the in-memory database.</span><span class="sxs-lookup"><span data-stu-id="62eb4-176">Because this is a test server, we simply add users to the in-memory database.</span></span>

<span data-ttu-id="62eb4-177">Add the methods that allow you to keep track of users who have signed in, as required by Passport.</span><span class="sxs-lookup"><span data-stu-id="62eb4-177">Add the methods that allow you to keep track of users who have signed in, as required by Passport.</span></span> <span data-ttu-id="62eb4-178">This includes serializing and deserializing user information:</span><span class="sxs-lookup"><span data-stu-id="62eb4-178">This includes serializing and deserializing user information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   To support persistent sign-in sessions, Passport needs to be able to
//   serialize users into and deserialize users out of sessions. Typically,
//   this is as simple as storing the user ID when Passport serializes a user
//   and finding the user by ID when Passport deserializes that user.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// Array to hold users who have signed in
var users = [];

var findByEmail = function(email, fn) {
  for (var i = 0, len = users.length; i < len; i++) {
    var user = users[i];
    log.info('we are using user: ', user);
    if (user.email === email) {
      return fn(null, user);
    }
  }
  return fn(null, null);
};

```

<span data-ttu-id="62eb4-179">Add the code to load the Express engine.</span><span class="sxs-lookup"><span data-stu-id="62eb4-179">Add the code to load the Express engine.</span></span> <span data-ttu-id="62eb4-180">In the following, you can see that we use the default `/views` and `/routes` pattern that Express provides.</span><span class="sxs-lookup"><span data-stu-id="62eb4-180">In the following, you can see that we use the default `/views` and `/routes` pattern that Express provides.</span></span>

```JavaScript

// configure Express (Section 2)

var app = express();


app.configure(function() {
  app.set('views', __dirname + '/views');
  app.set('view engine', 'ejs');
  app.use(express.logger());
  app.use(express.methodOverride());
  app.use(cookieParser());
  app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
  app.use(bodyParser.urlencoded({ extended : true }));
  // Initialize Passport!  Also use passport.session() middleware to support
  // persistent sign-in sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

<span data-ttu-id="62eb4-181">Add the `POST` routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span><span class="sxs-lookup"><span data-stu-id="62eb4-181">Add the `POST` routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware to authenticate the
//   request. The first step in OpenID authentication involves redirecting
//   the user to an OpenID provider. After the user is authenticated,
//   the OpenID provider redirects the user back to this application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authentication was called in the Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it redirects the user to the home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request. If authentication fails, the user will be redirected back to the
//   sign-in page. Otherwise, the primary route function will be called.
//   In this example, it will redirect the user to the home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="62eb4-182">Use Passport to issue sign-in and sign-out requests to Azure AD</span><span class="sxs-lookup"><span data-stu-id="62eb4-182">Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>

<span data-ttu-id="62eb4-183">Your app is now properly configured to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span><span class="sxs-lookup"><span data-stu-id="62eb4-183">Your app is now properly configured to communicate with the v2.0 endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="62eb4-184">`passport-azure-ad` has taken care of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span><span class="sxs-lookup"><span data-stu-id="62eb4-184">`passport-azure-ad` has taken care of the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span> <span data-ttu-id="62eb4-185">All that remains is to give your users a way to sign in and sign out, and to gather additional information on users who have signed in.</span><span class="sxs-lookup"><span data-stu-id="62eb4-185">All that remains is to give your users a way to sign in and sign out, and to gather additional information on users who have signed in.</span></span>

<span data-ttu-id="62eb4-186">First, add the default, sign-in, account, and sign-out methods to your `app.js` file:</span><span class="sxs-lookup"><span data-stu-id="62eb4-186">First, add the default, sign-in, account, and sign-out methods to your `app.js` file:</span></span>

```JavaScript

//Routes (Section 4)

app.get('/', function(req, res){
  res.render('index', { user: req.user });
});

app.get('/account', ensureAuthenticated, function(req, res){
  res.render('account', { user: req.user });
});

app.get('/login',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Login was called in the Sample');
    res.redirect('/');
});

app.get('/logout', function(req, res){
  req.logout();
  res.redirect('/');
});

```

<span data-ttu-id="62eb4-187">To review these methods in detail:</span><span class="sxs-lookup"><span data-stu-id="62eb4-187">To review these methods in detail:</span></span>
- <span data-ttu-id="62eb4-188">The `/` route redirects to the `index.ejs` view by passing the user in the request (if it exists).</span><span class="sxs-lookup"><span data-stu-id="62eb4-188">The `/` route redirects to the `index.ejs` view by passing the user in the request (if it exists).</span></span>
- <span data-ttu-id="62eb4-189">The `/account` route first verifies that you are authenticated (the implementation for this is below).</span><span class="sxs-lookup"><span data-stu-id="62eb4-189">The `/account` route first verifies that you are authenticated (the implementation for this is below).</span></span> <span data-ttu-id="62eb4-190">It then passes the user in the request so that you can get additional information about the user.</span><span class="sxs-lookup"><span data-stu-id="62eb4-190">It then passes the user in the request so that you can get additional information about the user.</span></span>
- <span data-ttu-id="62eb4-191">The `/login` route calls the `azuread-openidconnect` authenticator from `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="62eb4-191">The `/login` route calls the `azuread-openidconnect` authenticator from `passport-azure-ad`.</span></span> <span data-ttu-id="62eb4-192">If it doesn't succeed, the route redirects the user back to `/login`.</span><span class="sxs-lookup"><span data-stu-id="62eb4-192">If it doesn't succeed, the route redirects the user back to `/login`.</span></span>
- <span data-ttu-id="62eb4-193">`/logout` simply calls `logout.ejs` (and its route).</span><span class="sxs-lookup"><span data-stu-id="62eb4-193">`/logout` simply calls `logout.ejs` (and its route).</span></span> <span data-ttu-id="62eb4-194">This clears cookies and then returns the user back to `index.ejs`.</span><span class="sxs-lookup"><span data-stu-id="62eb4-194">This clears cookies and then returns the user back to `index.ejs`.</span></span>


<span data-ttu-id="62eb4-195">For the last part of `app.js`, add the `EnsureAuthenticated` method that is used in the `/account` route.</span><span class="sxs-lookup"><span data-stu-id="62eb4-195">For the last part of `app.js`, add the `EnsureAuthenticated` method that is used in the `/account` route.</span></span>

```JavaScript

// Simple route middleware to ensure that the user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs to be protected. If
//   the request is authenticated (typically via a persistent sign-in session),
//   then the request will proceed. Otherwise, the user will be redirected to the
//   sign-in page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

<span data-ttu-id="62eb4-196">Finally, create the server itself in `app.js`.</span><span class="sxs-lookup"><span data-stu-id="62eb4-196">Finally, create the server itself in `app.js`.</span></span>

```JavaScript

app.listen(3000);

```


## <a name="create-the-views-and-routes-in-express-to-call-your-policies"></a><span data-ttu-id="62eb4-197">Create the views and routes in Express to call your policies</span><span class="sxs-lookup"><span data-stu-id="62eb4-197">Create the views and routes in Express to call your policies</span></span>

<span data-ttu-id="62eb4-198">Your `app.js` is now complete.</span><span class="sxs-lookup"><span data-stu-id="62eb4-198">Your `app.js` is now complete.</span></span> <span data-ttu-id="62eb4-199">You just need to add the routes and views that allow you to call the sign-in and sign-up policies.</span><span class="sxs-lookup"><span data-stu-id="62eb4-199">You just need to add the routes and views that allow you to call the sign-in and sign-up policies.</span></span> <span data-ttu-id="62eb4-200">These also handle the `/logout` and `/login` routes you created.</span><span class="sxs-lookup"><span data-stu-id="62eb4-200">These also handle the `/logout` and `/login` routes you created.</span></span>

<span data-ttu-id="62eb4-201">Create the `/routes/index.js` route under the root directory.</span><span class="sxs-lookup"><span data-stu-id="62eb4-201">Create the `/routes/index.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

<span data-ttu-id="62eb4-202">Create the `/routes/user.js` route under the root directory.</span><span class="sxs-lookup"><span data-stu-id="62eb4-202">Create the `/routes/user.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="62eb4-203">These simple routes pass along requests to your views.</span><span class="sxs-lookup"><span data-stu-id="62eb4-203">These simple routes pass along requests to your views.</span></span> <span data-ttu-id="62eb4-204">They include the user, if one is present.</span><span class="sxs-lookup"><span data-stu-id="62eb4-204">They include the user, if one is present.</span></span>

<span data-ttu-id="62eb4-205">Create the `/views/index.ejs` view under the root directory.</span><span class="sxs-lookup"><span data-stu-id="62eb4-205">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="62eb4-206">This is a simple page that calls policies for sign-in and sign-out. You can also use it to grab account information.</span><span class="sxs-lookup"><span data-stu-id="62eb4-206">This is a simple page that calls policies for sign-in and sign-out. You can also use it to grab account information.</span></span> <span data-ttu-id="62eb4-207">Note that you can use the conditional `if (!user)` as the user is passed through in the request to provide evidence that the user is signed in.</span><span class="sxs-lookup"><span data-stu-id="62eb4-207">Note that you can use the conditional `if (!user)` as the user is passed through in the request to provide evidence that the user is signed in.</span></span>

```JavaScript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login/?p=your facebook policy">Sign in with Facebook</a>
    <a href="/login/?p=your email sign-in policy">Sign in with email</a>
    <a href="/login/?p=your email sign-up policy">Sign up with email</a>
<% } else { %>
    <h2>Hello, <%= user.displayName %>.</h2>
    <a href="/account">Account info</a></br>
    <a href="/logout">Log out</a>
<% } %>
```

<span data-ttu-id="62eb4-208">Create the `/views/account.ejs` view under the root directory so that you can view additional information that `passport-azure-ad` put in the user request.</span><span class="sxs-lookup"><span data-stu-id="62eb4-208">Create the `/views/account.ejs` view under the root directory so that you can view additional information that `passport-azure-ad` put in the user request.</span></span>

```Javascript
<% if (!user) { %>
    <h2>Welcome! Please sign in.</h2>
    <a href="/login">Sign in</a>
<% } else { %>
<p>displayName: <%= user.displayName %></p>
<p>givenName: <%= user.name.givenName %></p>
<p>familyName: <%= user.name.familyName %></p>
<p>UPN: <%= user._json.upn %></p>
<p>Profile ID: <%= user.id %></p>
<p>Full Claims</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

<span data-ttu-id="62eb4-209">You can now build and run your app.</span><span class="sxs-lookup"><span data-stu-id="62eb4-209">You can now build and run your app.</span></span>

<span data-ttu-id="62eb4-210">Run `node app.js` and navigate to `http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="62eb4-210">Run `node app.js` and navigate to `http://localhost:3000`</span></span>


<span data-ttu-id="62eb4-211">Sign up or sign in to the app by using email or Facebook.</span><span class="sxs-lookup"><span data-stu-id="62eb4-211">Sign up or sign in to the app by using email or Facebook.</span></span> <span data-ttu-id="62eb4-212">Sign out and sign back in as a different user.</span><span class="sxs-lookup"><span data-stu-id="62eb4-212">Sign out and sign back in as a different user.</span></span>

##<a name="next-steps"></a><span data-ttu-id="62eb4-213">Next steps</span><span class="sxs-lookup"><span data-stu-id="62eb4-213">Next steps</span></span>

<span data-ttu-id="62eb4-214">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span><span class="sxs-lookup"><span data-stu-id="62eb4-214">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-NodeJS/archive/complete.zip).</span></span> <span data-ttu-id="62eb4-215">You can also clone it from GitHub:</span><span class="sxs-lookup"><span data-stu-id="62eb4-215">You can also clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/B2C-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="62eb4-216">You can now move on to more advanced topics.</span><span class="sxs-lookup"><span data-stu-id="62eb4-216">You can now move on to more advanced topics.</span></span> <span data-ttu-id="62eb4-217">You might try:</span><span class="sxs-lookup"><span data-stu-id="62eb4-217">You might try:</span></span>

[<span data-ttu-id="62eb4-218">Secure a web API by using the B2C model in Node.js</span><span class="sxs-lookup"><span data-stu-id="62eb4-218">Secure a web API by using the B2C model in Node.js</span></span>](active-directory-b2c-devquickstarts-api-node.md)

<!--

For additional resources, check out:
You can now move on to more advanced B2C topics. You might try:

[Call a Node.js web API from a Node.js web app]()

[Customizing the your B2C App's UX >>]()

-->
