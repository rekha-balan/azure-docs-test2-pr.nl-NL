---
title: Azure AD Node.js web app getting started | Microsoft Docs
description: Learn how to build a Node.js Express MVC web app that integrates with Azure AD for sign-in.
services: active-directory
documentationcenter: nodejs
author: CelesteDG
manager: mtillman
editor: ''
ms.assetid: 81deecec-dbe2-4e75-8bc0-cf3788645f99
ms.service: active-directory
ms.component: develop
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 04/20/2018
ms.author: celested
ms.reviewer: nacanuma
ms.custom: aaddev
ms.openlocfilehash: 1f8f19944f64a5dfd5421a99734c5fd0fc3be1bc
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969530"
---
# <a name="azure-ad-nodejs-web-app-getting-started"></a><span data-ttu-id="26e81-103">Azure AD Node.js web app getting started</span><span class="sxs-lookup"><span data-stu-id="26e81-103">Azure AD Node.js web app getting started</span></span>
<span data-ttu-id="26e81-104">Here we use Passport to:</span><span class="sxs-lookup"><span data-stu-id="26e81-104">Here we use Passport to:</span></span>

* <span data-ttu-id="26e81-105">Sign the user in to the app with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="26e81-105">Sign the user in to the app with Azure Active Directory (Azure AD).</span></span>
* <span data-ttu-id="26e81-106">Display information about the user.</span><span class="sxs-lookup"><span data-stu-id="26e81-106">Display information about the user.</span></span>
* <span data-ttu-id="26e81-107">Sign the user out of the app.</span><span class="sxs-lookup"><span data-stu-id="26e81-107">Sign the user out of the app.</span></span>

<span data-ttu-id="26e81-108">Passport is authentication middleware for Node.js.</span><span class="sxs-lookup"><span data-stu-id="26e81-108">Passport is authentication middleware for Node.js.</span></span> <span data-ttu-id="26e81-109">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or restify web application.</span><span class="sxs-lookup"><span data-stu-id="26e81-109">Flexible and modular, Passport can be unobtrusively dropped in to any Express-based or restify web application.</span></span> <span data-ttu-id="26e81-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span><span class="sxs-lookup"><span data-stu-id="26e81-110">A comprehensive set of strategies support authentication that uses a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="26e81-111">We have developed a strategy for Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="26e81-111">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="26e81-112">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="26e81-112">We install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

<span data-ttu-id="26e81-113">To do this, take the following steps:</span><span class="sxs-lookup"><span data-stu-id="26e81-113">To do this, take the following steps:</span></span>

1. <span data-ttu-id="26e81-114">Register an app.</span><span class="sxs-lookup"><span data-stu-id="26e81-114">Register an app.</span></span>
2. <span data-ttu-id="26e81-115">Set up your app to use the `passport-azure-ad` strategy.</span><span class="sxs-lookup"><span data-stu-id="26e81-115">Set up your app to use the `passport-azure-ad` strategy.</span></span>
3. <span data-ttu-id="26e81-116">Use Passport to issue sign-in and sign-out requests to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="26e81-116">Use Passport to issue sign-in and sign-out requests to Azure AD.</span></span>
4. <span data-ttu-id="26e81-117">Print data about the user.</span><span class="sxs-lookup"><span data-stu-id="26e81-117">Print data about the user.</span></span>

<span data-ttu-id="26e81-118">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span><span class="sxs-lookup"><span data-stu-id="26e81-118">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS).</span></span> <span data-ttu-id="26e81-119">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone the skeleton:</span><span class="sxs-lookup"><span data-stu-id="26e81-119">To follow along, you can [download the app's skeleton as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="26e81-120">The completed application is provided at the end of this tutorial as well.</span><span class="sxs-lookup"><span data-stu-id="26e81-120">The completed application is provided at the end of this tutorial as well.</span></span>

## <a name="step-1-register-an-app"></a><span data-ttu-id="26e81-121">Step 1: Register an app</span><span class="sxs-lookup"><span data-stu-id="26e81-121">Step 1: Register an app</span></span>
1. <span data-ttu-id="26e81-122">Sign in to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="26e81-122">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="26e81-123">In the menu at the top of the page, select your account.</span><span class="sxs-lookup"><span data-stu-id="26e81-123">In the menu at the top of the page, select your account.</span></span> <span data-ttu-id="26e81-124">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span><span class="sxs-lookup"><span data-stu-id="26e81-124">Under the **Directory** list, choose the Active Directory tenant where you want to register your application.</span></span>

3. <span data-ttu-id="26e81-125">Select **All services** in the menu on the left side of the screen, and then select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="26e81-125">Select **All services** in the menu on the left side of the screen, and then select **Azure Active Directory**.</span></span>

4. <span data-ttu-id="26e81-126">Select **App registrations**, and then select **Add**.</span><span class="sxs-lookup"><span data-stu-id="26e81-126">Select **App registrations**, and then select **Add**.</span></span>

5. <span data-ttu-id="26e81-127">Follow the prompts to create a **Web Application** and/or **WebAPI**.</span><span class="sxs-lookup"><span data-stu-id="26e81-127">Follow the prompts to create a **Web Application** and/or **WebAPI**.</span></span>
  * <span data-ttu-id="26e81-128">The **name** of the application describes your application to users.</span><span class="sxs-lookup"><span data-stu-id="26e81-128">The **name** of the application describes your application to users.</span></span>

  * <span data-ttu-id="26e81-129">The **Sign-On URL** is the base URL of your app.</span><span class="sxs-lookup"><span data-stu-id="26e81-129">The **Sign-On URL** is the base URL of your app.</span></span> <span data-ttu-id="26e81-130">The skeleton's default is `http://localhost:3000/auth/openid/return`.</span><span class="sxs-lookup"><span data-stu-id="26e81-130">The skeleton's default is `http://localhost:3000/auth/openid/return`.</span></span>

6. <span data-ttu-id="26e81-131">After you register, Azure AD assigns your app a unique application ID.</span><span class="sxs-lookup"><span data-stu-id="26e81-131">After you register, Azure AD assigns your app a unique application ID.</span></span> <span data-ttu-id="26e81-132">You need this value in the following sections, so copy it from the application page.</span><span class="sxs-lookup"><span data-stu-id="26e81-132">You need this value in the following sections, so copy it from the application page.</span></span>
7. <span data-ttu-id="26e81-133">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span><span class="sxs-lookup"><span data-stu-id="26e81-133">From the **Settings** -> **Properties** page for your application, update the App ID URI.</span></span> <span data-ttu-id="26e81-134">The **App ID URI** is a unique identifier for your application.</span><span class="sxs-lookup"><span data-stu-id="26e81-134">The **App ID URI** is a unique identifier for your application.</span></span> <span data-ttu-id="26e81-135">The convention is to use the format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span><span class="sxs-lookup"><span data-stu-id="26e81-135">The convention is to use the format `https://<tenant-domain>/<app-name>`, for example: `https://contoso.onmicrosoft.com/my-first-aad-app`.</span></span>

8. <span data-ttu-id="26e81-136">From the **Settings** -> **Reply URLs** page for your application, add the URL added in Sign-on URL from Step 5 and click on Save.</span><span class="sxs-lookup"><span data-stu-id="26e81-136">From the **Settings** -> **Reply URLs** page for your application, add the URL added in Sign-on URL from Step 5 and click on Save.</span></span>

9. <span data-ttu-id="26e81-137">To create a secret key, follow step 4 in [To add application credentials, or permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-application-credentials-or-permissions-to-access-web-apis).</span><span class="sxs-lookup"><span data-stu-id="26e81-137">To create a secret key, follow step 4 in [To add application credentials, or permissions to access web APIs](https://docs.microsoft.com/azure/active-directory/develop/active-directory-integrating-applications#to-add-application-credentials-or-permissions-to-access-web-apis).</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="26e81-138">Copy the application key value.</span><span class="sxs-lookup"><span data-stu-id="26e81-138">Copy the application key value.</span></span> <span data-ttu-id="26e81-139">This is the value for the `clientSecret`, which you'll need for **Step 3** below.</span><span class="sxs-lookup"><span data-stu-id="26e81-139">This is the value for the `clientSecret`, which you'll need for **Step 3** below.</span></span> 

## <a name="step-2-add-prerequisites-to-your-directory"></a><span data-ttu-id="26e81-140">Step 2: Add prerequisites to your directory</span><span class="sxs-lookup"><span data-stu-id="26e81-140">Step 2: Add prerequisites to your directory</span></span>
1. <span data-ttu-id="26e81-141">From the command line, change directories to your root folder if you're not already there, and then run the following commands:</span><span class="sxs-lookup"><span data-stu-id="26e81-141">From the command line, change directories to your root folder if you're not already there, and then run the following commands:</span></span>

    * `npm install express`
    * `npm install ejs`
    * `npm install ejs-locals`
    * `npm install restify`
    * `npm install mongoose`
    * `npm install bunyan`
    * `npm install assert-plus`
    * `npm install passport`

2. <span data-ttu-id="26e81-142">In addition, you need `passport-azure-ad`:</span><span class="sxs-lookup"><span data-stu-id="26e81-142">In addition, you need `passport-azure-ad`:</span></span>
    * `npm install passport-azure-ad`

<span data-ttu-id="26e81-143">This installs the libraries that `passport-azure-ad` depends on.</span><span class="sxs-lookup"><span data-stu-id="26e81-143">This installs the libraries that `passport-azure-ad` depends on.</span></span>

## <a name="step-3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="26e81-144">Step 3: Set up your app to use the passport-node-js strategy</span><span class="sxs-lookup"><span data-stu-id="26e81-144">Step 3: Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="26e81-145">Here, we configure Express to use the OpenID Connect authentication protocol.</span><span class="sxs-lookup"><span data-stu-id="26e81-145">Here, we configure Express to use the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="26e81-146">Passport is used to do various things, including issue sign-in and sign-out requests, manage the user's session, and get information about the user.</span><span class="sxs-lookup"><span data-stu-id="26e81-146">Passport is used to do various things, including issue sign-in and sign-out requests, manage the user's session, and get information about the user.</span></span>

1. <span data-ttu-id="26e81-147">To begin, open the `config.js` file at the root of the project, and then enter your app's configuration values in the `exports.creds` section.</span><span class="sxs-lookup"><span data-stu-id="26e81-147">To begin, open the `config.js` file at the root of the project, and then enter your app's configuration values in the `exports.creds` section.</span></span>

  * <span data-ttu-id="26e81-148">The `clientID` is the **Application Id** that's assigned to your app in the registration portal.</span><span class="sxs-lookup"><span data-stu-id="26e81-148">The `clientID` is the **Application Id** that's assigned to your app in the registration portal.</span></span>

  * <span data-ttu-id="26e81-149">The `returnURL` is the **Reply URL** that you entered in the portal.</span><span class="sxs-lookup"><span data-stu-id="26e81-149">The `returnURL` is the **Reply URL** that you entered in the portal.</span></span>

  * <span data-ttu-id="26e81-150">The `clientSecret` is the secret that you generated in the portal.</span><span class="sxs-lookup"><span data-stu-id="26e81-150">The `clientSecret` is the secret that you generated in the portal.</span></span>

2. <span data-ttu-id="26e81-151">Next, open the `app.js` file in the root of the project.</span><span class="sxs-lookup"><span data-stu-id="26e81-151">Next, open the `app.js` file in the root of the project.</span></span> <span data-ttu-id="26e81-152">Then add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span><span class="sxs-lookup"><span data-stu-id="26e81-152">Then add the following call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`.</span></span>

    ```JavaScript
    var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

    // add a logger

    var log = bunyan.createLogger({
        name: 'Microsoft OIDC Example Web Application'
    });
    ```

3. <span data-ttu-id="26e81-153">After that, use the strategy we just referenced to handle our sign-in requests.</span><span class="sxs-lookup"><span data-stu-id="26e81-153">After that, use the strategy we just referenced to handle our sign-in requests.</span></span>

    ```JavaScript
    // Use the OIDCStrategy within Passport. (Section 2)
    //
    //   Strategies in passport require a `validate` function that accepts
    //   credentials (in this case, an OpenID identifier), and invokes a callback
    //   with a user object.
    passport.use(new OIDCStrategy({
        callbackURL: config.creds.returnURL,
        realm: config.creds.realm,
        clientID: config.creds.clientID,
        clientSecret: config.creds.clientSecret,
        oidcIssuer: config.creds.issuer,
        identityMetadata: config.creds.identityMetadata,
        skipUserProfile: config.creds.skipUserProfile,
        responseType: config.creds.responseType,
        responseMode: config.creds.responseMode
    },
    function(iss, sub, profile, accessToken, refreshToken, done) {
        if (!profile.email) {
        return done(new Error("No email found"), null);
        }
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
   <span data-ttu-id="26e81-154">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span><span class="sxs-lookup"><span data-stu-id="26e81-154">Passport uses a similar pattern for all its strategies (Twitter, Facebook, and so on) that all strategy writers adhere to.</span></span> <span data-ttu-id="26e81-155">Looking at the strategy, you see that we pass it a function that has a token and a done as the parameters.</span><span class="sxs-lookup"><span data-stu-id="26e81-155">Looking at the strategy, you see that we pass it a function that has a token and a done as the parameters.</span></span> <span data-ttu-id="26e81-156">The strategy comes back to us after it does its work.</span><span class="sxs-lookup"><span data-stu-id="26e81-156">The strategy comes back to us after it does its work.</span></span> <span data-ttu-id="26e81-157">Then we want to store the user and stash the token so we don't need to ask for it again.</span><span class="sxs-lookup"><span data-stu-id="26e81-157">Then we want to store the user and stash the token so we don't need to ask for it again.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="26e81-158">The previous code takes any user that happens to authenticate to our server.</span><span class="sxs-lookup"><span data-stu-id="26e81-158">The previous code takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="26e81-159">This is known as auto-registration.</span><span class="sxs-lookup"><span data-stu-id="26e81-159">This is known as auto-registration.</span></span> <span data-ttu-id="26e81-160">We    recommend that you don't let anyone authenticate to a production server without first having them register via a process that you decide on.</span><span class="sxs-lookup"><span data-stu-id="26e81-160">We    recommend that you don't let anyone authenticate to a production server without first having them register via a process that you decide on.</span></span> <span data-ttu-id="26e81-161">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to provide additional information.</span><span class="sxs-lookup"><span data-stu-id="26e81-161">This is usually the pattern you see in consumer apps, which allow you to register with Facebook but then ask you to provide additional information.</span></span> <span data-ttu-id="26e81-162">If this weren't a sample application, we could have extracted the user's email address from the token object that is returned and then asked the user to fill out additional information.</span><span class="sxs-lookup"><span data-stu-id="26e81-162">If this weren't a sample application, we could have extracted the user's email address from the token object that is returned and then asked the user to fill out additional information.</span></span> <span data-ttu-id="26e81-163">Because this is a test server, we add them to the in-memory database.</span><span class="sxs-lookup"><span data-stu-id="26e81-163">Because this is a test server, we add them to the in-memory database.</span></span>


4. <span data-ttu-id="26e81-164">Next, let's add the methods that enable us to track the signed-in users as required by Passport.</span><span class="sxs-lookup"><span data-stu-id="26e81-164">Next, let's add the methods that enable us to track the signed-in users as required by Passport.</span></span> <span data-ttu-id="26e81-165">These methods include serializing and deserializing the user's information.</span><span class="sxs-lookup"><span data-stu-id="26e81-165">These methods include serializing and deserializing the user's information.</span></span>

    ```JavaScript
    // Passport session setup. (Section 2)

    //   To support persistent sign-in sessions, Passport needs to be able to
    //   serialize users into the session and deserialize them out of the session. Typically,
    //   this is done simply by storing the user ID when serializing and finding
    //   the user by ID when deserializing.
    passport.serializeUser(function(user, done) {
        done(null, user.email);
    });

    passport.deserializeUser(function(id, done) {
        findByEmail(id, function (err, user) {
            done(err, user);
        });
    });

    // array to hold signed-in users
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

5. <span data-ttu-id="26e81-166">Next, let's add the code to load the Express engine.</span><span class="sxs-lookup"><span data-stu-id="26e81-166">Next, let's add the code to load the Express engine.</span></span> <span data-ttu-id="26e81-167">Here we use the default /views and /routes pattern that Express provides.</span><span class="sxs-lookup"><span data-stu-id="26e81-167">Here we use the default /views and /routes pattern that Express provides.</span></span>

    ```JavaScript
    // configure Express (section 2)

      var app = express();
      app.configure(function() {
      app.set('views', __dirname + '/views');
      app.set('view engine', 'ejs');
      app.use(express.logger());
      app.use(express.methodOverride());
      app.use(cookieParser());
      app.use(expressSession({ secret: 'keyboard cat', resave: true, saveUninitialized: false }));
      app.use(bodyParser.urlencoded({ extended : true }));
      // Initialize Passport!  Also use passport.session() middleware, to support
      // persistent login sessions (recommended).
      app.use(passport.initialize());
      app.use(passport.session());
      app.use(app.router);
      app.use(express.static(__dirname + '/../../public'));
    });
    ```

6. <span data-ttu-id="26e81-168">Finally, let's add the routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span><span class="sxs-lookup"><span data-stu-id="26e81-168">Finally, let's add the routes that hand off the actual sign-in requests to the `passport-azure-ad` engine:</span></span>

    ```JavaScript
    // Our Auth routes (section 3)

    // GET /auth/openid
    //   Use passport.authenticate() as route middleware to authenticate the
    //   request. The first step in OpenID authentication involves redirecting
    //   the user to their OpenID provider. After authenticating, the OpenID
    //   provider redirects the user back to this application at
    //   /auth/openid/return.
    app.get('/auth/openid',
    passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
    function(req, res) {
        log.info('Authentication was called in the Sample');
        res.redirect('/');
    });

    // GET /auth/openid/return
    //   Use passport.authenticate() as route middleware to authenticate the
    //   request. If authentication fails, the user is redirected back to the
    //   sign-in page. Otherwise, the primary route function is called,
    //   which, in this example, redirects the user to the home page.
    app.get('/auth/openid/return',
      passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
      function(req, res) {
        log.info('We received a return from AzureAD.');
        res.redirect('/');
      });

    // POST /auth/openid/return
    //   Use passport.authenticate() as route middleware to authenticate the
    //   request. If authentication fails, the user is redirected back to the
    //   sign-in page. Otherwise, the primary route function is called,
    //   which, in this example, redirects the user to the home page.
    app.post('/auth/openid/return',
      passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
      function(req, res) {
        log.info('We received a return from AzureAD.');
        res.redirect('/');
      });
    ```


## <a name="step-4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="26e81-169">Step 4: Use Passport to issue sign-in and sign-out requests to Azure AD</span><span class="sxs-lookup"><span data-stu-id="26e81-169">Step 4: Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="26e81-170">Your app is now properly configured to communicate with the endpoint by using the OpenID Connect authentication protocol.</span><span class="sxs-lookup"><span data-stu-id="26e81-170">Your app is now properly configured to communicate with the endpoint by using the OpenID Connect authentication protocol.</span></span> <span data-ttu-id="26e81-171">`passport-azure-ad` has taken care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span><span class="sxs-lookup"><span data-stu-id="26e81-171">`passport-azure-ad` has taken care of all the details of crafting authentication messages, validating tokens from Azure AD, and maintaining user sessions.</span></span> <span data-ttu-id="26e81-172">All that remains is giving your users a way to sign in and sign out, and gathering additional information about the signed-in users.</span><span class="sxs-lookup"><span data-stu-id="26e81-172">All that remains is giving your users a way to sign in and sign out, and gathering additional information about the signed-in users.</span></span>

1. <span data-ttu-id="26e81-173">First, let's add the default, sign-in, account, and sign-out methods to our `app.js` file:</span><span class="sxs-lookup"><span data-stu-id="26e81-173">First, let's add the default, sign-in, account, and sign-out methods to our `app.js` file:</span></span>

    ```JavaScript
    //Routes (section 4)

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

2. <span data-ttu-id="26e81-174">Let's review these in detail:</span><span class="sxs-lookup"><span data-stu-id="26e81-174">Let's review these in detail:</span></span>

  * <span data-ttu-id="26e81-175">The `/`route redirects to the index.ejs view, passing the user in the request (if it exists).</span><span class="sxs-lookup"><span data-stu-id="26e81-175">The `/`route redirects to the index.ejs view, passing the user in the request (if it exists).</span></span>
  * <span data-ttu-id="26e81-176">The `/account` route first *ensures we are authenticated* (we implement that in the following example), and then passes the user in the request so that we can get additional information about the user.</span><span class="sxs-lookup"><span data-stu-id="26e81-176">The `/account` route first *ensures we are authenticated* (we implement that in the following example), and then passes the user in the request so that we can get additional information about the user.</span></span>
  * <span data-ttu-id="26e81-177">The `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span><span class="sxs-lookup"><span data-stu-id="26e81-177">The `/login` route calls our azuread-openidconnect authenticator from `passport-azuread`.</span></span> <span data-ttu-id="26e81-178">If that doesn't succeed, it redirects the user back to /login.</span><span class="sxs-lookup"><span data-stu-id="26e81-178">If that doesn't succeed, it redirects the user back to /login.</span></span>
  * <span data-ttu-id="26e81-179">The `/logout` route simply calls the logout.ejs (and route), which clears cookies and then returns the user back to index.ejs.</span><span class="sxs-lookup"><span data-stu-id="26e81-179">The `/logout` route simply calls the logout.ejs (and route), which clears cookies and then returns the user back to index.ejs.</span></span>

3. <span data-ttu-id="26e81-180">For the last part of `app.js`, let's add the **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span><span class="sxs-lookup"><span data-stu-id="26e81-180">For the last part of `app.js`, let's add the **EnsureAuthenticated** method that is used in `/account`, as shown earlier.</span></span>

    ```JavaScript
    // Simple route middleware to ensure user is authenticated. (section 4)

    //   Use this route middleware on any resource that needs to be protected. If
    //   the request is authenticated (typically via a persistent sign-in session),
    //   the request proceeds. Otherwise, the user is redirected to the
    //   sign-in page.
    function ensureAuthenticated(req, res, next) {
      if (req.isAuthenticated()) { return next(); }
      res.redirect('/login')
    }
    ```

4. <span data-ttu-id="26e81-181">Finally, let's create the server itself in `app.js`:</span><span class="sxs-lookup"><span data-stu-id="26e81-181">Finally, let's create the server itself in `app.js`:</span></span>

```JavaScript
app.listen(3000);
```


## <a name="step-5-to-display-our-user-in-the-website-create-the-views-and-routes-in-express"></a><span data-ttu-id="26e81-182">Step 5: To display our user in the website, create the views and routes in Express</span><span class="sxs-lookup"><span data-stu-id="26e81-182">Step 5: To display our user in the website, create the views and routes in Express</span></span>
<span data-ttu-id="26e81-183">Now `app.js` is complete.</span><span class="sxs-lookup"><span data-stu-id="26e81-183">Now `app.js` is complete.</span></span> <span data-ttu-id="26e81-184">We simply need to add the routes and views that show the information we get to the user, as well as handle the `/logout` and `/login` routes that we  created.</span><span class="sxs-lookup"><span data-stu-id="26e81-184">We simply need to add the routes and views that show the information we get to the user, as well as handle the `/logout` and `/login` routes that we  created.</span></span>

1. <span data-ttu-id="26e81-185">Create the `/routes/index.js` route under the root directory.</span><span class="sxs-lookup"><span data-stu-id="26e81-185">Create the `/routes/index.js` route under the root directory.</span></span>

    ```JavaScript
    /*
     * GET home page.
     */

    exports.index = function(req, res){
      res.render('index', { title: 'Express' });
    };
    ```

2. <span data-ttu-id="26e81-186">Create the `/routes/user.js` route under the root directory.</span><span class="sxs-lookup"><span data-stu-id="26e81-186">Create the `/routes/user.js` route under the root directory.</span></span>

    ```JavaScript
    /*
     * GET users listing.
     */

    exports.list = function(req, res){
      res.send("respond with a resource");
    };
    ```

 <span data-ttu-id="26e81-187">These pass along the request to our views, including the user if present.</span><span class="sxs-lookup"><span data-stu-id="26e81-187">These pass along the request to our views, including the user if present.</span></span>

3. <span data-ttu-id="26e81-188">Create the `/views/index.ejs` view under the root directory.</span><span class="sxs-lookup"><span data-stu-id="26e81-188">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="26e81-189">This is a simple page that calls our login and logout methods and enables us to grab account information.</span><span class="sxs-lookup"><span data-stu-id="26e81-189">This is a simple page that calls our login and logout methods and enables us to grab account information.</span></span> <span data-ttu-id="26e81-190">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a signed-in user.</span><span class="sxs-lookup"><span data-stu-id="26e81-190">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a signed-in user.</span></span>

    ```JavaScript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
        <h2>Hello, <%= user.displayName %>.</h2>
        <a href="/account">Account Info</a></br>
        <a href="/logout">Log Out</a>
    <% } %>
    ```

4. <span data-ttu-id="26e81-191">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azure-ad` has put in the user request.</span><span class="sxs-lookup"><span data-stu-id="26e81-191">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azure-ad` has put in the user request.</span></span>

    ```Javascript
    <% if (!user) { %>
        <h2>Welcome! Please log in.</h2>
        <a href="/login">Log In</a>
    <% } else { %>
    <p>displayName: <%= user.displayName %></p>
    <p>givenName: <%= user.name.givenName %></p>
    <p>familyName: <%= user.name.familyName %></p>
    <p>UPN: <%= user._json.upn %></p>
    <p>Profile ID: <%= user.id %></p>
  ##Next steps  <p>Full Claimes</p>
    <%- JSON.stringify(user) %>
    <p></p>
    <a href="/logout">Log Out</a>
    <% } %>
    ```

5. <span data-ttu-id="26e81-192">Let's make this look good by adding a layout.</span><span class="sxs-lookup"><span data-stu-id="26e81-192">Let's make this look good by adding a layout.</span></span> <span data-ttu-id="26e81-193">Create the `/views/layout.ejs` view under the root directory.</span><span class="sxs-lookup"><span data-stu-id="26e81-193">Create the `/views/layout.ejs` view under the root directory.</span></span>

    ```HTML

    <!DOCTYPE html>
    <html>
        <head>
            <title>Passport-OpenID Example</title>
        </head>
        <body>
            <% if (!user) { %>
                <p>
                <a href="/">Home</a> |
                <a href="/login">Log In</a>
                </p>
            <% } else { %>
                <p>
                <a href="/">Home</a> |
                <a href="/account">Account</a> |
                <a href="/logout">Log Out</a>
                </p>
            <% } %>
            <%- body %>
        </body>
    </html>
    ```

## <a name="next-steps"></a><span data-ttu-id="26e81-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="26e81-194">Next steps</span></span>
<span data-ttu-id="26e81-195">Finally, build and run your app.</span><span class="sxs-lookup"><span data-stu-id="26e81-195">Finally, build and run your app.</span></span> <span data-ttu-id="26e81-196">Run `node app.js`, and then go to `http://localhost:3000`.</span><span class="sxs-lookup"><span data-stu-id="26e81-196">Run `node app.js`, and then go to `http://localhost:3000`.</span></span>

<span data-ttu-id="26e81-197">Sign in with either a personal Microsoft account or a work or school account, and notice how the user's identity is reflected in the /account list.</span><span class="sxs-lookup"><span data-stu-id="26e81-197">Sign in with either a personal Microsoft account or a work or school account, and notice how the user's identity is reflected in the /account list.</span></span> <span data-ttu-id="26e81-198">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span><span class="sxs-lookup"><span data-stu-id="26e81-198">You now have a web app that's secured with industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

<span data-ttu-id="26e81-199">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/master.zip).</span><span class="sxs-lookup"><span data-stu-id="26e81-199">For reference, the completed sample (without your configuration values) [is provided as a .zip file](https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS/archive/master.zip).</span></span> <span data-ttu-id="26e81-200">Alternatively, you can clone it from GitHub:</span><span class="sxs-lookup"><span data-stu-id="26e81-200">Alternatively, you can clone it from GitHub:</span></span>

```git clone --branch master https://github.com/AzureADQuickStarts/WebApp-OpenIDConnect-NodeJS.git```

<span data-ttu-id="26e81-201">You can now move onto more advanced topics.</span><span class="sxs-lookup"><span data-stu-id="26e81-201">You can now move onto more advanced topics.</span></span> <span data-ttu-id="26e81-202">You might want to try:</span><span class="sxs-lookup"><span data-stu-id="26e81-202">You might want to try:</span></span>

[<span data-ttu-id="26e81-203">Secure a Web API with Azure AD</span><span class="sxs-lookup"><span data-stu-id="26e81-203">Secure a Web API with Azure AD</span></span>](quickstart-v1-nodejs-webapi.md)

[!INCLUDE [active-directory-devquickstarts-additional-resources](../../../includes/active-directory-devquickstarts-additional-resources.md)]
