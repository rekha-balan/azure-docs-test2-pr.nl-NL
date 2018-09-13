---
title: Azure AD v2.0 NodeJS Web App | Microsoft Docs
description: How to build a Node JS web app that signs users in with both personal Microsoft Account and work or school accounts.
services: active-directory
documentationcenter: nodejs
author: xerners
manager: mbaldwin
editor: ''
ms.assetid: 1b889e72-f5c3-464a-af57-79abf5e2e147
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: javascript
ms.topic: article
ms.date: 09/16/2016
ms.author: xerners
ms.openlocfilehash: 037f47677a9ae3dbfe1aa85118735e82a731b9e3
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555681"
---
# <a name="add-sign-in-to-a-nodejs-web-app"></a><span data-ttu-id="466fd-103">Add sign-in to a nodeJS Web App</span><span class="sxs-lookup"><span data-stu-id="466fd-103">Add sign-in to a nodeJS Web App</span></span>
> [!NOTE]
> <span data-ttu-id="466fd-104">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="466fd-104">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="466fd-105">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span><span class="sxs-lookup"><span data-stu-id="466fd-105">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

<span data-ttu-id="466fd-106">Here we'll use Passport to:</span><span class="sxs-lookup"><span data-stu-id="466fd-106">Here we'll use Passport to:</span></span>

* <span data-ttu-id="466fd-107">Sign the user into the app using Azure AD and the v2.0 endpoint.</span><span class="sxs-lookup"><span data-stu-id="466fd-107">Sign the user into the app using Azure AD and the v2.0 endpoint.</span></span>
* <span data-ttu-id="466fd-108">Display some information about the user.</span><span class="sxs-lookup"><span data-stu-id="466fd-108">Display some information about the user.</span></span>
* <span data-ttu-id="466fd-109">Sign the user out of the app.</span><span class="sxs-lookup"><span data-stu-id="466fd-109">Sign the user out of the app.</span></span>

<span data-ttu-id="466fd-110">**Passport** is authentication middleware for Node.js.</span><span class="sxs-lookup"><span data-stu-id="466fd-110">**Passport** is authentication middleware for Node.js.</span></span> <span data-ttu-id="466fd-111">Extremely flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Resitify web application.</span><span class="sxs-lookup"><span data-stu-id="466fd-111">Extremely flexible and modular, Passport can be unobtrusively dropped in to any Express-based or Resitify web application.</span></span> <span data-ttu-id="466fd-112">A comprehensive set of strategies support authentication using a username and password, Facebook, Twitter, and more.</span><span class="sxs-lookup"><span data-stu-id="466fd-112">A comprehensive set of strategies support authentication using a username and password, Facebook, Twitter, and more.</span></span> <span data-ttu-id="466fd-113">We have developed a strategy for Microsoft Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="466fd-113">We have developed a strategy for Microsoft Azure Active Directory.</span></span> <span data-ttu-id="466fd-114">We will install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span><span class="sxs-lookup"><span data-stu-id="466fd-114">We will install this module and then add the Microsoft Azure Active Directory `passport-azure-ad` plug-in.</span></span>

## <a name="download"></a><span data-ttu-id="466fd-115">Download</span><span class="sxs-lookup"><span data-stu-id="466fd-115">Download</span></span>
<span data-ttu-id="466fd-116">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span><span class="sxs-lookup"><span data-stu-id="466fd-116">The code for this tutorial is maintained [on GitHub](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs).</span></span>  <span data-ttu-id="466fd-117">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone the skeleton:</span><span class="sxs-lookup"><span data-stu-id="466fd-117">To follow along, you can [download the app's skeleton as a .zip](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/skeleton.zip) or clone the skeleton:</span></span>

```git clone --branch skeleton https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="466fd-118">The completed application is provided at the end of this tutorial as well.</span><span class="sxs-lookup"><span data-stu-id="466fd-118">The completed application is provided at the end of this tutorial as well.</span></span>

## <a name="1-register-an-app"></a><span data-ttu-id="466fd-119">1. Register an App</span><span class="sxs-lookup"><span data-stu-id="466fd-119">1. Register an App</span></span>
<span data-ttu-id="466fd-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span><span class="sxs-lookup"><span data-stu-id="466fd-120">Create a new app at [apps.dev.microsoft.com](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), or follow these [detailed steps](active-directory-v2-app-registration.md).</span></span>  <span data-ttu-id="466fd-121">Make sure to:</span><span class="sxs-lookup"><span data-stu-id="466fd-121">Make sure to:</span></span>

* <span data-ttu-id="466fd-122">Copy down the **Application Id** assigned to your app, you'll need it soon.</span><span class="sxs-lookup"><span data-stu-id="466fd-122">Copy down the **Application Id** assigned to your app, you'll need it soon.</span></span>
* <span data-ttu-id="466fd-123">Add the **Web** platform for your app.</span><span class="sxs-lookup"><span data-stu-id="466fd-123">Add the **Web** platform for your app.</span></span>
* <span data-ttu-id="466fd-124">Enter the correct **Redirect URI**.</span><span class="sxs-lookup"><span data-stu-id="466fd-124">Enter the correct **Redirect URI**.</span></span> <span data-ttu-id="466fd-125">The redirect URI indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `http://localhost:3000/auth/openid/return`.</span><span class="sxs-lookup"><span data-stu-id="466fd-125">The redirect URI indicates to Azure AD where authentication responses should be directed - the default for this tutorial is `http://localhost:3000/auth/openid/return`.</span></span>

## <a name="2-add-pre-requisities-to-your-directory"></a><span data-ttu-id="466fd-126">2. Add pre-requisities to your directory</span><span class="sxs-lookup"><span data-stu-id="466fd-126">2. Add pre-requisities to your directory</span></span>
<span data-ttu-id="466fd-127">From the command-line, change directories to your root folder if not already there and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="466fd-127">From the command-line, change directories to your root folder if not already there and run the following commands:</span></span>

* `npm install express`
* `npm install ejs`
* `npm install ejs-locals`
* `npm install restify`
* `npm install mongoose`
* `npm install bunyan`
* `npm install assert-plus`
* `npm install passport`
* `npm install webfinger`
* `npm install body-parser`
* `npm install express-session`
* `npm install cookie-parser`
* <span data-ttu-id="466fd-128">In addition, we've use `passport-azure-ad` in the skeleton of the quickstart.</span><span class="sxs-lookup"><span data-stu-id="466fd-128">In addition, we've use `passport-azure-ad` in the skeleton of the quickstart.</span></span>
* `npm install passport-azure-ad`

<span data-ttu-id="466fd-129">This will install the libraries that passport-azure-ad depend on.</span><span class="sxs-lookup"><span data-stu-id="466fd-129">This will install the libraries that passport-azure-ad depend on.</span></span>

## <a name="3-set-up-your-app-to-use-the-passport-node-js-strategy"></a><span data-ttu-id="466fd-130">3. Set up your app to use the passport-node-js strategy</span><span class="sxs-lookup"><span data-stu-id="466fd-130">3. Set up your app to use the passport-node-js strategy</span></span>
<span data-ttu-id="466fd-131">Here, we'll configure the Express middleware to use the OpenID Connect authentication protocol.</span><span class="sxs-lookup"><span data-stu-id="466fd-131">Here, we'll configure the Express middleware to use the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="466fd-132">Passport will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span><span class="sxs-lookup"><span data-stu-id="466fd-132">Passport will be used to issue sign-in and sign-out requests, manage the user's session, and get information about the user, amongst other things.</span></span>

* <span data-ttu-id="466fd-133">To begin, open the `config.js` file in the root of the project, and enter your app's configuration values in the `exports.creds` section.</span><span class="sxs-lookup"><span data-stu-id="466fd-133">To begin, open the `config.js` file in the root of the project, and enter your app's configuration values in the `exports.creds` section.</span></span>
  
  * <span data-ttu-id="466fd-134">The `clientID:` is the **Application Id** assigned to your app in the registration portal.</span><span class="sxs-lookup"><span data-stu-id="466fd-134">The `clientID:` is the **Application Id** assigned to your app in the registration portal.</span></span>
  * <span data-ttu-id="466fd-135">The `returnURL` is the **Redirect URI** you entered in the portal.</span><span class="sxs-lookup"><span data-stu-id="466fd-135">The `returnURL` is the **Redirect URI** you entered in the portal.</span></span>
  * <span data-ttu-id="466fd-136">The `clientSecret` is the secret you generated in the portal.</span><span class="sxs-lookup"><span data-stu-id="466fd-136">The `clientSecret` is the secret you generated in the portal.</span></span>
* <span data-ttu-id="466fd-137">Next open `app.js` file in the root of the proejct and add the follwing call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`</span><span class="sxs-lookup"><span data-stu-id="466fd-137">Next open `app.js` file in the root of the proejct and add the follwing call to invoke the `OIDCStrategy` strategy that comes with `passport-azure-ad`</span></span>

```JavaScript
var OIDCStrategy = require('passport-azure-ad').OIDCStrategy;

// Add some logging
var log = bunyan.createLogger({
    name: 'Microsoft OIDC Example Web Application'
});
```

* <span data-ttu-id="466fd-138">After that, use the strategy we just referenced to handle our login requests</span><span class="sxs-lookup"><span data-stu-id="466fd-138">After that, use the strategy we just referenced to handle our login requests</span></span>

```JavaScript
// Use the OIDCStrategy within Passport. (Section 2)
//
//   Strategies in passport require a `validate` function, which accept
//   credentials (in this case, an OpenID identifier), and invoke a callback
//   with a user object.
passport.use(new OIDCStrategy({
    callbackURL: config.creds.returnURL,
    realm: config.creds.realm,
    clientID: config.creds.clientID,
    clientSecret: config.creds.clientSecret,
    oidcIssuer: config.creds.issuer,
    identityMetadata: config.creds.identityMetadata,
    responseType: config.creds.responseType,
    responseMode: config.creds.responseMode,
    skipUserProfile: config.creds.skipUserProfile
    scope: config.creds.scope
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
<span data-ttu-id="466fd-139">Passport uses a similar pattern for all it’s Strategies (Twitter, Facebook, etc.) that all Strategy writers adhere to.</span><span class="sxs-lookup"><span data-stu-id="466fd-139">Passport uses a similar pattern for all it’s Strategies (Twitter, Facebook, etc.) that all Strategy writers adhere to.</span></span> <span data-ttu-id="466fd-140">Looking at the strategy you see we pass it a function() that has a token and a done as the parameters.</span><span class="sxs-lookup"><span data-stu-id="466fd-140">Looking at the strategy you see we pass it a function() that has a token and a done as the parameters.</span></span> <span data-ttu-id="466fd-141">The strategy will dutifully come back to us once it does all it’s work.</span><span class="sxs-lookup"><span data-stu-id="466fd-141">The strategy will dutifully come back to us once it does all it’s work.</span></span> <span data-ttu-id="466fd-142">Once it does we’ll want to store the user and stash the token so we won’t need to ask for it again.</span><span class="sxs-lookup"><span data-stu-id="466fd-142">Once it does we’ll want to store the user and stash the token so we won’t need to ask for it again.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="466fd-143">The code above takes any user that happens to authenticate to our server.</span><span class="sxs-lookup"><span data-stu-id="466fd-143">The code above takes any user that happens to authenticate to our server.</span></span> <span data-ttu-id="466fd-144">This is known as auto registration.</span><span class="sxs-lookup"><span data-stu-id="466fd-144">This is known as auto registration.</span></span> <span data-ttu-id="466fd-145">In production servers you wouldn’t want to let anyone in without first having them go through a registration process you decide.</span><span class="sxs-lookup"><span data-stu-id="466fd-145">In production servers you wouldn’t want to let anyone in without first having them go through a registration process you decide.</span></span> <span data-ttu-id="466fd-146">This is usually the pattern you see in consumer apps who allow you to register with Facebook but then ask you to fill out additional information.</span><span class="sxs-lookup"><span data-stu-id="466fd-146">This is usually the pattern you see in consumer apps who allow you to register with Facebook but then ask you to fill out additional information.</span></span> <span data-ttu-id="466fd-147">If this wasn’t a sample application, we could have just extracted the email from the token object that is returned and then asked them to fill out additional information.</span><span class="sxs-lookup"><span data-stu-id="466fd-147">If this wasn’t a sample application, we could have just extracted the email from the token object that is returned and then asked them to fill out additional information.</span></span> <span data-ttu-id="466fd-148">Since this is a test server we simply add them to the in-memory database.</span><span class="sxs-lookup"><span data-stu-id="466fd-148">Since this is a test server we simply add them to the in-memory database.</span></span>
> 
> 

* <span data-ttu-id="466fd-149">Next, let's add the methods that will allow us to keep track of the logged in users as required by Passport.</span><span class="sxs-lookup"><span data-stu-id="466fd-149">Next, let's add the methods that will allow us to keep track of the logged in users as required by Passport.</span></span> <span data-ttu-id="466fd-150">This includes serializing and deserializing the user's information:</span><span class="sxs-lookup"><span data-stu-id="466fd-150">This includes serializing and deserializing the user's information:</span></span>

```JavaScript

// Passport session setup. (Section 2)

//   To support persistent login sessions, Passport needs to be able to
//   serialize users into and deserialize users out of the session.  Typically,
//   this will be as simple as storing the user ID when serializing, and finding
//   the user by ID when deserializing.
passport.serializeUser(function(user, done) {
  done(null, user.email);
});

passport.deserializeUser(function(id, done) {
  findByEmail(id, function (err, user) {
    done(err, user);
  });
});

// array to hold logged in users
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

* <span data-ttu-id="466fd-151">Next, let's add the code to load the express engine.</span><span class="sxs-lookup"><span data-stu-id="466fd-151">Next, let's add the code to load the express engine.</span></span> <span data-ttu-id="466fd-152">Here you see we use the default /views and /routes pattern that Express provides.</span><span class="sxs-lookup"><span data-stu-id="466fd-152">Here you see we use the default /views and /routes pattern that Express provides.</span></span>

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
  // Initialize Passport!  Also use passport.session() middleware, to support
  // persistent login sessions (recommended).
  app.use(passport.initialize());
  app.use(passport.session());
  app.use(app.router);
  app.use(express.static(__dirname + '/../../public'));
});

```

* <span data-ttu-id="466fd-153">Finally, let's add the POST routes that will hand off the actual login requests to the `passport-azure-ad` engine:</span><span class="sxs-lookup"><span data-stu-id="466fd-153">Finally, let's add the POST routes that will hand off the actual login requests to the `passport-azure-ad` engine:</span></span>

```JavaScript

// Our Auth routes (Section 3)

// GET /auth/openid
//   Use passport.authenticate() as route middleware to authenticate the
//   request.  The first step in OpenID authentication will involve redirecting
//   the user to their OpenID provider.  After authenticating, the OpenID
//   provider will redirect the user back to this application at
//   /auth/openid/return

app.get('/auth/openid',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {
    log.info('Authenitcation was called in the Sample');
    res.redirect('/');
  });

// GET /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request.  If authentication fails, the user will be redirected back to the
//   login page.  Otherwise, the primary route function function will be called,
//   which, in this example, will redirect the user to the home page.
app.get('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });

// POST /auth/openid/return
//   Use passport.authenticate() as route middleware to authenticate the
//   request.  If authentication fails, the user will be redirected back to the
//   login page.  Otherwise, the primary route function function will be called,
//   which, in this example, will redirect the user to the home page.

app.post('/auth/openid/return',
  passport.authenticate('azuread-openidconnect', { failureRedirect: '/login' }),
  function(req, res) {

    res.redirect('/');
  });
```

## <a name="4-use-passport-to-issue-sign-in-and-sign-out-requests-to-azure-ad"></a><span data-ttu-id="466fd-154">4. Use Passport to issue sign-in and sign-out requests to Azure AD</span><span class="sxs-lookup"><span data-stu-id="466fd-154">4. Use Passport to issue sign-in and sign-out requests to Azure AD</span></span>
<span data-ttu-id="466fd-155">Your app is now properly configured to communicate with the v2.0 endpoint using the OpenID Connect authentication protocol.</span><span class="sxs-lookup"><span data-stu-id="466fd-155">Your app is now properly configured to communicate with the v2.0 endpoint using the OpenID Connect authentication protocol.</span></span>  <span data-ttu-id="466fd-156">`passport-azure-ad` has taken care of all of the ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span><span class="sxs-lookup"><span data-stu-id="466fd-156">`passport-azure-ad` has taken care of all of the ugly details of crafting authentication messages, validating tokens from Azure AD, and maintaining user session.</span></span>  <span data-ttu-id="466fd-157">All that remains is to give your users a way to sign in, sign out, and gather additional info on the logged in user.</span><span class="sxs-lookup"><span data-stu-id="466fd-157">All that remains is to give your users a way to sign in, sign out, and gather additional info on the logged in user.</span></span>

* <span data-ttu-id="466fd-158">First, lets add the default, login, account, and logout methods to our `app.js` file:</span><span class="sxs-lookup"><span data-stu-id="466fd-158">First, lets add the default, login, account, and logout methods to our `app.js` file:</span></span>

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

* <span data-ttu-id="466fd-159">Let's review these in detail:</span><span class="sxs-lookup"><span data-stu-id="466fd-159">Let's review these in detail:</span></span>
  
  * <span data-ttu-id="466fd-160">The `/` route will redirect to the index.ejs view passing the user in the request (if it exists)</span><span class="sxs-lookup"><span data-stu-id="466fd-160">The `/` route will redirect to the index.ejs view passing the user in the request (if it exists)</span></span>
  * <span data-ttu-id="466fd-161">The `/account` route will first ***ensure we are authenticated*** (we implement that below) and then pass the user in the request so that we can get additional information about the user.</span><span class="sxs-lookup"><span data-stu-id="466fd-161">The `/account` route will first ***ensure we are authenticated*** (we implement that below) and then pass the user in the request so that we can get additional information about the user.</span></span>
  * <span data-ttu-id="466fd-162">The `/login` route will call our azuread-openidconnect authenticator from `passport-azuread` and if that doesn't succeed will redirect the user back to /login</span><span class="sxs-lookup"><span data-stu-id="466fd-162">The `/login` route will call our azuread-openidconnect authenticator from `passport-azuread` and if that doesn't succeed will redirect the user back to /login</span></span>
  * <span data-ttu-id="466fd-163">The `/logout` will simply call the logout.ejs (and route) which clears cookies and then return the user back to index.ejs</span><span class="sxs-lookup"><span data-stu-id="466fd-163">The `/logout` will simply call the logout.ejs (and route) which clears cookies and then return the user back to index.ejs</span></span>
* <span data-ttu-id="466fd-164">For the last part of `app.js`, let's add the EnsureAuthenticated method that is used in `/account` above.</span><span class="sxs-lookup"><span data-stu-id="466fd-164">For the last part of `app.js`, let's add the EnsureAuthenticated method that is used in `/account` above.</span></span>

```JavaScript

// Simple route middleware to ensure user is authenticated. (Section 4)

//   Use this route middleware on any resource that needs to be protected.  If
//   the request is authenticated (typically via a persistent login session),
//   the request will proceed.  Otherwise, the user will be redirected to the
//   login page.
function ensureAuthenticated(req, res, next) {
  if (req.isAuthenticated()) { return next(); }
  res.redirect('/login')
}

```

* <span data-ttu-id="466fd-165">Finally, let's actually create the server itself in `app.js`:</span><span class="sxs-lookup"><span data-stu-id="466fd-165">Finally, let's actually create the server itself in `app.js`:</span></span>

```JavaScript

app.listen(3000);

```


## <a name="5-create-the-views-and-routes-in-express-to-display-our-user-in-the-website"></a><span data-ttu-id="466fd-166">5. Create the views and routes in express to display our user in the website</span><span class="sxs-lookup"><span data-stu-id="466fd-166">5. Create the views and routes in express to display our user in the website</span></span>
<span data-ttu-id="466fd-167">We have our `app.js` complete.</span><span class="sxs-lookup"><span data-stu-id="466fd-167">We have our `app.js` complete.</span></span> <span data-ttu-id="466fd-168">Now we simply need to add the routes and views that will show the information we get to the user as well as handle the `/logout` and `/login` routes we've created.</span><span class="sxs-lookup"><span data-stu-id="466fd-168">Now we simply need to add the routes and views that will show the information we get to the user as well as handle the `/logout` and `/login` routes we've created.</span></span>

* <span data-ttu-id="466fd-169">Create the `/routes/index.js` route under the root directory.</span><span class="sxs-lookup"><span data-stu-id="466fd-169">Create the `/routes/index.js` route under the root directory.</span></span>

```JavaScript

/*
 * GET home page.
 */

exports.index = function(req, res){
  res.render('index', { title: 'Express' });
};
```

* <span data-ttu-id="466fd-170">Create the `/routes/user.js` route under the root directory</span><span class="sxs-lookup"><span data-stu-id="466fd-170">Create the `/routes/user.js` route under the root directory</span></span>

```JavaScript

/*
 * GET users listing.
 */

exports.list = function(req, res){
  res.send("respond with a resource");
};
```

<span data-ttu-id="466fd-171">These simple routes will just pass along the request to our views, including the user if present.</span><span class="sxs-lookup"><span data-stu-id="466fd-171">These simple routes will just pass along the request to our views, including the user if present.</span></span>

* <span data-ttu-id="466fd-172">Create the `/views/index.ejs` view under the root directory.</span><span class="sxs-lookup"><span data-stu-id="466fd-172">Create the `/views/index.ejs` view under the root directory.</span></span> <span data-ttu-id="466fd-173">this is a simple page that will call our login and logout methods and allow us to grab account information.</span><span class="sxs-lookup"><span data-stu-id="466fd-173">this is a simple page that will call our login and logout methods and allow us to grab account information.</span></span> <span data-ttu-id="466fd-174">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a logged in user.</span><span class="sxs-lookup"><span data-stu-id="466fd-174">Notice that we can use the conditional `if (!user)` as the user being passed through in the request is evidence we have a logged in user.</span></span>

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

* <span data-ttu-id="466fd-175">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azuread` has put in the user request.</span><span class="sxs-lookup"><span data-stu-id="466fd-175">Create the `/views/account.ejs` view under the root directory so that we can view additional information that `passport-azuread` has put in the user request.</span></span>

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
<p>Full Claimes</p>
<%- JSON.stringify(user) %>
<p></p>
<a href="/logout">Log Out</a>
<% } %>
```

* <span data-ttu-id="466fd-176">Finally, let's make this look pretty by adding a layout.</span><span class="sxs-lookup"><span data-stu-id="466fd-176">Finally, let's make this look pretty by adding a layout.</span></span> <span data-ttu-id="466fd-177">Create the '/views/layout.ejs' view under the root directory</span><span class="sxs-lookup"><span data-stu-id="466fd-177">Create the '/views/layout.ejs' view under the root directory</span></span>

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

<span data-ttu-id="466fd-178">Finally, build and run your app!</span><span class="sxs-lookup"><span data-stu-id="466fd-178">Finally, build and run your app!</span></span>

<span data-ttu-id="466fd-179">Run `node app.js` and navigate to `http://localhost:3000`</span><span class="sxs-lookup"><span data-stu-id="466fd-179">Run `node app.js` and navigate to `http://localhost:3000`</span></span>

<span data-ttu-id="466fd-180">Sign in with either a personal Microsoft Account or a work or school account, and notice how the user's identity is reflected in the /account list.</span><span class="sxs-lookup"><span data-stu-id="466fd-180">Sign in with either a personal Microsoft Account or a work or school account, and notice how the user's identity is reflected in the /account list.</span></span>  <span data-ttu-id="466fd-181">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span><span class="sxs-lookup"><span data-stu-id="466fd-181">You now have a web app secured using industry standard protocols that can authenticate users with both their personal and work/school accounts.</span></span>

## <a name="next-steps"></a><span data-ttu-id="466fd-182">Next Steps</span><span class="sxs-lookup"><span data-stu-id="466fd-182">Next Steps</span></span>
<span data-ttu-id="466fd-183">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip), or you can clone it from GitHub:</span><span class="sxs-lookup"><span data-stu-id="466fd-183">For reference, the completed sample (without your configuration values) [is provided as a .zip here](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs/archive/complete.zip), or you can clone it from GitHub:</span></span>

```git clone --branch complete https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-nodejs.git```

<span data-ttu-id="466fd-184">You can now move onto more advanced topics.</span><span class="sxs-lookup"><span data-stu-id="466fd-184">You can now move onto more advanced topics.</span></span>  <span data-ttu-id="466fd-185">You may want to try:</span><span class="sxs-lookup"><span data-stu-id="466fd-185">You may want to try:</span></span>

[<span data-ttu-id="466fd-186">Secure a node.js web api using the v2.0 endpoint >></span><span class="sxs-lookup"><span data-stu-id="466fd-186">Secure a node.js web api using the v2.0 endpoint >></span></span>](active-directory-v2-devquickstarts-node-api.md)

<span data-ttu-id="466fd-187">For additional resources, check out:</span><span class="sxs-lookup"><span data-stu-id="466fd-187">For additional resources, check out:</span></span>

* [<span data-ttu-id="466fd-188">The v2.0 developer guide >></span><span class="sxs-lookup"><span data-stu-id="466fd-188">The v2.0 developer guide >></span></span>](active-directory-appmodel-v2-overview.md)
* [<span data-ttu-id="466fd-189">StackOverflow "azure-active-directory" tag >></span><span class="sxs-lookup"><span data-stu-id="466fd-189">StackOverflow "azure-active-directory" tag >></span></span>](http://stackoverflow.com/questions/tagged/azure-active-directory)

## <a name="get-security-updates-for-our-products"></a><span data-ttu-id="466fd-190">Get security updates for our products</span><span class="sxs-lookup"><span data-stu-id="466fd-190">Get security updates for our products</span></span>
<span data-ttu-id="466fd-191">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span><span class="sxs-lookup"><span data-stu-id="466fd-191">We encourage you to get notifications of when security incidents occur by visiting [this page](https://technet.microsoft.com/security/dd252948) and subscribing to Security Advisory Alerts.</span></span>

