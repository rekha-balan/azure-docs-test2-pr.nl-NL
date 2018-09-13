### <a name="server-auth"></a><span data-ttu-id="1842f-101">How to: Authenticate with a provider (Server Flow)</span><span class="sxs-lookup"><span data-stu-id="1842f-101">How to: Authenticate with a provider (Server Flow)</span></span>
<span data-ttu-id="1842f-102">To have Mobile Apps manage the authentication process in your app, you must register your app with your identity provider.</span><span class="sxs-lookup"><span data-stu-id="1842f-102">To have Mobile Apps manage the authentication process in your app, you must register your app with your identity provider.</span></span> <span data-ttu-id="1842f-103">Then in your Azure App Service, you need to configure the application ID and secret provided by your provider.</span><span class="sxs-lookup"><span data-stu-id="1842f-103">Then in your Azure App Service, you need to configure the application ID and secret provided by your provider.</span></span>
<span data-ttu-id="1842f-104">For more information, see the tutorial [Add authentication to your app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span><span class="sxs-lookup"><span data-stu-id="1842f-104">For more information, see the tutorial [Add authentication to your app](../articles/app-service-mobile/app-service-mobile-cordova-get-started-users.md).</span></span>

<span data-ttu-id="1842f-105">Once you have registered your identity provider, call the `.login()` method with the name of your provider.</span><span class="sxs-lookup"><span data-stu-id="1842f-105">Once you have registered your identity provider, call the `.login()` method with the name of your provider.</span></span> <span data-ttu-id="1842f-106">For example, to login with Facebook use the following code:</span><span class="sxs-lookup"><span data-stu-id="1842f-106">For example, to login with Facebook use the following code:</span></span>

```
client.login("facebook").done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});
```

<span data-ttu-id="1842f-107">The valid values for the provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span><span class="sxs-lookup"><span data-stu-id="1842f-107">The valid values for the provider are 'aad', 'facebook', 'google', 'microsoftaccount', and 'twitter'.</span></span>

> [!NOTE]
> <span data-ttu-id="1842f-108">Google Authentication does not currently work via Server Flow.</span><span class="sxs-lookup"><span data-stu-id="1842f-108">Google Authentication does not currently work via Server Flow.</span></span>  <span data-ttu-id="1842f-109">To authenticate with Google, you must use a [client-flow method](#client-auth).</span><span class="sxs-lookup"><span data-stu-id="1842f-109">To authenticate with Google, you must use a [client-flow method](#client-auth).</span></span>

<span data-ttu-id="1842f-110">In this case, Azure App Service manages the OAuth 2.0 authentication flow.</span><span class="sxs-lookup"><span data-stu-id="1842f-110">In this case, Azure App Service manages the OAuth 2.0 authentication flow.</span></span>  <span data-ttu-id="1842f-111">It displays the login page of the selected provider and generates an App Service authentication token after successful login with the identity provider.</span><span class="sxs-lookup"><span data-stu-id="1842f-111">It displays the login page of the selected provider and generates an App Service authentication token after successful login with the identity provider.</span></span> <span data-ttu-id="1842f-112">The login function, when complete, returns a JSON object that exposes both the user ID and App Service authentication token in the userId and authenticationToken fields, respectively.</span><span class="sxs-lookup"><span data-stu-id="1842f-112">The login function, when complete, returns a JSON object that exposes both the user ID and App Service authentication token in the userId and authenticationToken fields, respectively.</span></span> <span data-ttu-id="1842f-113">This token can be cached and reused until it expires.</span><span class="sxs-lookup"><span data-stu-id="1842f-113">This token can be cached and reused until it expires.</span></span>

###<a name="client-auth"></a><span data-ttu-id="1842f-114">How to: Authenticate with a provider (Client Flow)</span><span class="sxs-lookup"><span data-stu-id="1842f-114">How to: Authenticate with a provider (Client Flow)</span></span>

<span data-ttu-id="1842f-115">Your app can also independently contact the identity provider and then provide the returned token to your App Service for authentication.</span><span class="sxs-lookup"><span data-stu-id="1842f-115">Your app can also independently contact the identity provider and then provide the returned token to your App Service for authentication.</span></span> <span data-ttu-id="1842f-116">This client flow enables you to provide a single sign-in experience for users or to retrieve additional user data from the identity provider.</span><span class="sxs-lookup"><span data-stu-id="1842f-116">This client flow enables you to provide a single sign-in experience for users or to retrieve additional user data from the identity provider.</span></span>

#### <a name="social-authentication-basic-example"></a><span data-ttu-id="1842f-117">Social Authentication basic example</span><span class="sxs-lookup"><span data-stu-id="1842f-117">Social Authentication basic example</span></span>

<span data-ttu-id="1842f-118">This example uses Facebook client SDK for authentication:</span><span class="sxs-lookup"><span data-stu-id="1842f-118">This example uses Facebook client SDK for authentication:</span></span>

```
client.login(
     "facebook",
     {"access_token": token})
.done(function (results) {
     alert("You are now logged in as: " + results.userId);
}, function (err) {
     alert("Error: " + err);
});

```
<span data-ttu-id="1842f-119">This example assumes that the token provided by the respective provider SDK is stored in the token variable.</span><span class="sxs-lookup"><span data-stu-id="1842f-119">This example assumes that the token provided by the respective provider SDK is stored in the token variable.</span></span>

#### <a name="microsoft-account-example"></a><span data-ttu-id="1842f-120">Microsoft Account example</span><span class="sxs-lookup"><span data-stu-id="1842f-120">Microsoft Account example</span></span>

<span data-ttu-id="1842f-121">The following example uses the Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span><span class="sxs-lookup"><span data-stu-id="1842f-121">The following example uses the Live SDK, which supports single-sign-on for Windows Store apps by using Microsoft Account:</span></span>

```
WL.login({ scope: "wl.basic"}).then(function (result) {
      client.login(
            "microsoftaccount",
            {"authenticationToken": result.session.authentication_token})
      .done(function(results){
            alert("You are now logged in as: " + results.userId);
      },
      function(error){
            alert("Error: " + err);
      });
});

```

<span data-ttu-id="1842f-122">This example gets a token from Live Connect, which is supplied to your App Service by calling the login function.</span><span class="sxs-lookup"><span data-stu-id="1842f-122">This example gets a token from Live Connect, which is supplied to your App Service by calling the login function.</span></span>

###<a name="auth-getinfo"></a><span data-ttu-id="1842f-123">How to: Obtain information about the authenticated user</span><span class="sxs-lookup"><span data-stu-id="1842f-123">How to: Obtain information about the authenticated user</span></span>

<span data-ttu-id="1842f-124">The authentication information can be retrieved from the `/.auth/me` endpoint using an HTTP call with any AJAX library.</span><span class="sxs-lookup"><span data-stu-id="1842f-124">The authentication information can be retrieved from the `/.auth/me` endpoint using an HTTP call with any AJAX library.</span></span>  <span data-ttu-id="1842f-125">Ensure you set the `X-ZUMO-AUTH` header to your authentication token.</span><span class="sxs-lookup"><span data-stu-id="1842f-125">Ensure you set the `X-ZUMO-AUTH` header to your authentication token.</span></span>  <span data-ttu-id="1842f-126">The authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span><span class="sxs-lookup"><span data-stu-id="1842f-126">The authentication token is stored in `client.currentUser.mobileServiceAuthenticationToken`.</span></span>  <span data-ttu-id="1842f-127">For example, to use the fetch API:</span><span class="sxs-lookup"><span data-stu-id="1842f-127">For example, to use the fetch API:</span></span>

```
var url = client.applicationUrl + '/.auth/me';
var headers = new Headers();
headers.append('X-ZUMO-AUTH', client.currentUser.mobileServiceAuthenticationToken);
fetch(url, { headers: headers })
    .then(function (data) {
        return data.json()
    }).then(function (user) {
        // The user object contains the claims for the authenticated user
    });
```

<span data-ttu-id="1842f-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span><span class="sxs-lookup"><span data-stu-id="1842f-128">Fetch is available as [an npm package](https://www.npmjs.com/package/whatwg-fetch) or for browser download from [CDNJS](https://cdnjs.com/libraries/fetch).</span></span> <span data-ttu-id="1842f-129">You could also use jQuery or another AJAX API to fetch the information.</span><span class="sxs-lookup"><span data-stu-id="1842f-129">You could also use jQuery or another AJAX API to fetch the information.</span></span>  <span data-ttu-id="1842f-130">Data is received as a JSON object.</span><span class="sxs-lookup"><span data-stu-id="1842f-130">Data is received as a JSON object.</span></span>
