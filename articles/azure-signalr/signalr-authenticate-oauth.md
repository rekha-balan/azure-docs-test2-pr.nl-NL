---
title: Tutorial for authenticating Azure SignalR Service clients | Microsoft Docs
description: In this tutorial, you learn how to authenticate Azure SignalR Service clients
services: signalr
documentationcenter: ''
author: sffamily
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: signalr
ms.workload: tbd
ms.devlang: na
ms.topic: tutorial
ms.custom: mvc
ms.date: 06/13/2018
ms.author: zhshang
ms.openlocfilehash: 4856f4cdba7618884a42341f16d4828cb062e75c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868930"
---
# <a name="tutorial-azure-signalr-service-authentication"></a><span data-ttu-id="ca412-103">Tutorial: Azure SignalR Service authentication</span><span class="sxs-lookup"><span data-stu-id="ca412-103">Tutorial: Azure SignalR Service authentication</span></span>

<span data-ttu-id="ca412-104">Microsoft Azure SignalR Service is currently in [Public Preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span><span class="sxs-lookup"><span data-stu-id="ca412-104">Microsoft Azure SignalR Service is currently in [Public Preview](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).</span></span>

<span data-ttu-id="ca412-105">This tutorial builds on the chat room application introduced in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="ca412-105">This tutorial builds on the chat room application introduced in the quickstart.</span></span> <span data-ttu-id="ca412-106">If you have not completed [Create a chat room with SignalR Service](signalr-quickstart-dotnet-core.md), complete that exercise first.</span><span class="sxs-lookup"><span data-stu-id="ca412-106">If you have not completed [Create a chat room with SignalR Service](signalr-quickstart-dotnet-core.md), complete that exercise first.</span></span> 

<span data-ttu-id="ca412-107">In this tutorial, you'll learn how to implement your own authentication and integrate it with the Microsoft Azure SignalR Service.</span><span class="sxs-lookup"><span data-stu-id="ca412-107">In this tutorial, you'll learn how to implement your own authentication and integrate it with the Microsoft Azure SignalR Service.</span></span> 

<span data-ttu-id="ca412-108">The authentication initially used in the quickstart's chat room application is too simple for real-world scenarios.</span><span class="sxs-lookup"><span data-stu-id="ca412-108">The authentication initially used in the quickstart's chat room application is too simple for real-world scenarios.</span></span> <span data-ttu-id="ca412-109">The application allows each client to claim who they are, and the server simply accepts that.</span><span class="sxs-lookup"><span data-stu-id="ca412-109">The application allows each client to claim who they are, and the server simply accepts that.</span></span> <span data-ttu-id="ca412-110">This approach is not very useful in real-world applications where a rogue user would impersonate others to access sensitive data.</span><span class="sxs-lookup"><span data-stu-id="ca412-110">This approach is not very useful in real-world applications where a rogue user would impersonate others to access sensitive data.</span></span> 

<span data-ttu-id="ca412-111">[GitHub](https://github.com/) provides authentication APIs based on a popular industry-standard protocol called [OAuth](https://oauth.net/).</span><span class="sxs-lookup"><span data-stu-id="ca412-111">[GitHub](https://github.com/) provides authentication APIs based on a popular industry-standard protocol called [OAuth](https://oauth.net/).</span></span> <span data-ttu-id="ca412-112">These APIs allow third-party applications to authenticate GitHub accounts.</span><span class="sxs-lookup"><span data-stu-id="ca412-112">These APIs allow third-party applications to authenticate GitHub accounts.</span></span> <span data-ttu-id="ca412-113">In this tutorial, you will use these APIs to implement authentication through a Github account before allowing client logins to the chat room application.</span><span class="sxs-lookup"><span data-stu-id="ca412-113">In this tutorial, you will use these APIs to implement authentication through a Github account before allowing client logins to the chat room application.</span></span> <span data-ttu-id="ca412-114">After authenticating a GitHub account, the account information will be added as a cookie to be used by the web client to authenticate.</span><span class="sxs-lookup"><span data-stu-id="ca412-114">After authenticating a GitHub account, the account information will be added as a cookie to be used by the web client to authenticate.</span></span>

<span data-ttu-id="ca412-115">For more information on the OAuth authentication APIs provided through GitHub, see [Basics of Authentication](https://developer.github.com/v3/guides/basics-of-authentication/).</span><span class="sxs-lookup"><span data-stu-id="ca412-115">For more information on the OAuth authentication APIs provided through GitHub, see [Basics of Authentication](https://developer.github.com/v3/guides/basics-of-authentication/).</span></span>

<span data-ttu-id="ca412-116">You can use any code editor to complete the steps in this quickstart.</span><span class="sxs-lookup"><span data-stu-id="ca412-116">You can use any code editor to complete the steps in this quickstart.</span></span> <span data-ttu-id="ca412-117">However, [Visual Studio Code](https://code.visualstudio.com/) is an excellent option available on the Windows, macOS, and Linux platforms.</span><span class="sxs-lookup"><span data-stu-id="ca412-117">However, [Visual Studio Code](https://code.visualstudio.com/) is an excellent option available on the Windows, macOS, and Linux platforms.</span></span>

<span data-ttu-id="ca412-118">The code for this tutorial is available for download in the [AzureSignalR-samples GitHub repository](https://github.com/aspnet/AzureSignalR-samples/tree/master/samples/GitHubChat).</span><span class="sxs-lookup"><span data-stu-id="ca412-118">The code for this tutorial is available for download in the [AzureSignalR-samples GitHub repository](https://github.com/aspnet/AzureSignalR-samples/tree/master/samples/GitHubChat).</span></span>


![OAuth Complete hosted in Azure](media/signalr-authenticate-oauth/signalr-oauth-complete-azure.png)


<span data-ttu-id="ca412-120">In this tutorial, you learn how to:</span><span class="sxs-lookup"><span data-stu-id="ca412-120">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="ca412-121">Register a new OAuth app with your GitHub account</span><span class="sxs-lookup"><span data-stu-id="ca412-121">Register a new OAuth app with your GitHub account</span></span>
> * <span data-ttu-id="ca412-122">Add an authentication controller to support GitHub authentication</span><span class="sxs-lookup"><span data-stu-id="ca412-122">Add an authentication controller to support GitHub authentication</span></span>
> * <span data-ttu-id="ca412-123">Deploy your ASP.NET Core web app to Azure</span><span class="sxs-lookup"><span data-stu-id="ca412-123">Deploy your ASP.NET Core web app to Azure</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a><span data-ttu-id="ca412-124">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ca412-124">Prerequisites</span></span>

<span data-ttu-id="ca412-125">To complete this tutorial, you must have the following prerequisites:</span><span class="sxs-lookup"><span data-stu-id="ca412-125">To complete this tutorial, you must have the following prerequisites:</span></span>

* <span data-ttu-id="ca412-126">An account created on [GitHub](https://github.com/)</span><span class="sxs-lookup"><span data-stu-id="ca412-126">An account created on [GitHub](https://github.com/)</span></span>
* [<span data-ttu-id="ca412-127">Git</span><span class="sxs-lookup"><span data-stu-id="ca412-127">Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="ca412-128">.NET Core SDK</span><span class="sxs-lookup"><span data-stu-id="ca412-128">.NET Core SDK</span></span>](https://www.microsoft.com/net/download/windows) 
* [<span data-ttu-id="ca412-129">Azure Cloud Shell configured</span><span class="sxs-lookup"><span data-stu-id="ca412-129">Azure Cloud Shell configured</span></span>](https://docs.microsoft.com/azure/cloud-shell/quickstart)
* <span data-ttu-id="ca412-130">Download or clone the [AzureSignalR-sample](https://github.com/aspnet/AzureSignalR-samples) github repository.</span><span class="sxs-lookup"><span data-stu-id="ca412-130">Download or clone the [AzureSignalR-sample](https://github.com/aspnet/AzureSignalR-samples) github repository.</span></span>


## <a name="create-an-oauth-app"></a><span data-ttu-id="ca412-131">Create an OAuth app</span><span class="sxs-lookup"><span data-stu-id="ca412-131">Create an OAuth app</span></span>

1. <span data-ttu-id="ca412-132">Open a web browser and navigate to `https://github.com` and sign into your account.</span><span class="sxs-lookup"><span data-stu-id="ca412-132">Open a web browser and navigate to `https://github.com` and sign into your account.</span></span>

2. <span data-ttu-id="ca412-133">For your account, navigate to **Settings** > **Developer settings** and click **Register a new application**, or **New OAuth App** under *OAuth Apps*.</span><span class="sxs-lookup"><span data-stu-id="ca412-133">For your account, navigate to **Settings** > **Developer settings** and click **Register a new application**, or **New OAuth App** under *OAuth Apps*.</span></span>

3. <span data-ttu-id="ca412-134">Use the following settings for the new OAuth App, then click **Register application**:</span><span class="sxs-lookup"><span data-stu-id="ca412-134">Use the following settings for the new OAuth App, then click **Register application**:</span></span>

    | <span data-ttu-id="ca412-135">Setting Name</span><span class="sxs-lookup"><span data-stu-id="ca412-135">Setting Name</span></span> | <span data-ttu-id="ca412-136">Suggested Value</span><span class="sxs-lookup"><span data-stu-id="ca412-136">Suggested Value</span></span> | <span data-ttu-id="ca412-137">Description</span><span class="sxs-lookup"><span data-stu-id="ca412-137">Description</span></span> |
    | ------------ | --------------- | ----------- |
    | <span data-ttu-id="ca412-138">Application name</span><span class="sxs-lookup"><span data-stu-id="ca412-138">Application name</span></span> | <span data-ttu-id="ca412-139">*Azure SignalR Chat*</span><span class="sxs-lookup"><span data-stu-id="ca412-139">*Azure SignalR Chat*</span></span> | <span data-ttu-id="ca412-140">The github user should be able to recognize and trust the app they are authenticating with.</span><span class="sxs-lookup"><span data-stu-id="ca412-140">The github user should be able to recognize and trust the app they are authenticating with.</span></span>   |
    | <span data-ttu-id="ca412-141">Homepage URL</span><span class="sxs-lookup"><span data-stu-id="ca412-141">Homepage URL</span></span> | *http://localhost:5000/home* | |
    | <span data-ttu-id="ca412-142">Application description</span><span class="sxs-lookup"><span data-stu-id="ca412-142">Application description</span></span> | <span data-ttu-id="ca412-143">*A chat room sample using the Azure SignalR Service with Github authentication*</span><span class="sxs-lookup"><span data-stu-id="ca412-143">*A chat room sample using the Azure SignalR Service with Github authentication*</span></span> | <span data-ttu-id="ca412-144">A useful description of the application that will help your application users understand the context of the authentication being used.</span><span class="sxs-lookup"><span data-stu-id="ca412-144">A useful description of the application that will help your application users understand the context of the authentication being used.</span></span> |
    | <span data-ttu-id="ca412-145">Authorization callback URL</span><span class="sxs-lookup"><span data-stu-id="ca412-145">Authorization callback URL</span></span> | *http://localhost:5000/signin-github* | <span data-ttu-id="ca412-146">This setting is the most important setting for your OAuth application.</span><span class="sxs-lookup"><span data-stu-id="ca412-146">This setting is the most important setting for your OAuth application.</span></span> <span data-ttu-id="ca412-147">It's the callback URL that GitHub returns the user to after successful authentication.</span><span class="sxs-lookup"><span data-stu-id="ca412-147">It's the callback URL that GitHub returns the user to after successful authentication.</span></span> <span data-ttu-id="ca412-148">In this tutorial, you must use the default callback URL for the *AspNet.Security.OAuth.GitHub* package, */signin-github*.</span><span class="sxs-lookup"><span data-stu-id="ca412-148">In this tutorial, you must use the default callback URL for the *AspNet.Security.OAuth.GitHub* package, */signin-github*.</span></span>  |

4. <span data-ttu-id="ca412-149">Once the new OAuth app registration is complete, add the *Client ID* and *Client Secret* to Secret Manager using the following commands.</span><span class="sxs-lookup"><span data-stu-id="ca412-149">Once the new OAuth app registration is complete, add the *Client ID* and *Client Secret* to Secret Manager using the following commands.</span></span> <span data-ttu-id="ca412-150">Replace *Your_GitHub_Client_Id* and *Your_GitHub_Client_Secret* with the values for your OAuth app.</span><span class="sxs-lookup"><span data-stu-id="ca412-150">Replace *Your_GitHub_Client_Id* and *Your_GitHub_Client_Secret* with the values for your OAuth app.</span></span>

        dotnet user-secrets set GitHubClientId Your_GitHub_Client_Id
        dotnet user-secrets set GitHubClientSecret Your_GitHub_Client_Secret


## <a name="implement-the-oauth-flow"></a><span data-ttu-id="ca412-151">Implement the OAuth flow</span><span class="sxs-lookup"><span data-stu-id="ca412-151">Implement the OAuth flow</span></span>

### <a name="update-the-startup-class-to-support-github-authentication"></a><span data-ttu-id="ca412-152">Update the Startup class to support GitHub authentication</span><span class="sxs-lookup"><span data-stu-id="ca412-152">Update the Startup class to support GitHub authentication</span></span>

1. <span data-ttu-id="ca412-153">Add a reference to the latest *Microsoft.AspNetCore.Authentication.Cookies* and *AspNet.Security.OAuth.GitHub* packages and restore all packages.</span><span class="sxs-lookup"><span data-stu-id="ca412-153">Add a reference to the latest *Microsoft.AspNetCore.Authentication.Cookies* and *AspNet.Security.OAuth.GitHub* packages and restore all packages.</span></span>

        dotnet add package Microsoft.AspNetCore.Authentication.Cookies -v 2.1.0-rc1-30656
        dotnet add package AspNet.Security.OAuth.GitHub -v 2.0.0-rc2-final
        dotnet restore

1. <span data-ttu-id="ca412-154">Open *Startup.cs*, and add `using` statements for the following namespaces:</span><span class="sxs-lookup"><span data-stu-id="ca412-154">Open *Startup.cs*, and add `using` statements for the following namespaces:</span></span>

    ```csharp
    using System.Net.Http;
    using System.Net.Http.Headers;
    using System.Security.Claims;
    using Microsoft.AspNetCore.Authentication.Cookies;
    using Microsoft.AspNetCore.Authentication.OAuth;
    using Newtonsoft.Json.Linq;
    ```

2. <span data-ttu-id="ca412-155">At the top of the `Startup` class, add constants for the Secret Manager keys that hold the GitHub OAuth app secrets.</span><span class="sxs-lookup"><span data-stu-id="ca412-155">At the top of the `Startup` class, add constants for the Secret Manager keys that hold the GitHub OAuth app secrets.</span></span>

    ```csharp
    private const string GitHubClientId = "GitHubClientId";
    private const string GitHubClientSecret = "GitHubClientSecret";
    ```

3. <span data-ttu-id="ca412-156">Add the following code to the `ConfigureServices` method to support authentication with the GitHub OAuth app:</span><span class="sxs-lookup"><span data-stu-id="ca412-156">Add the following code to the `ConfigureServices` method to support authentication with the GitHub OAuth app:</span></span>

    ```csharp
    services.AddAuthentication(CookieAuthenticationDefaults.AuthenticationScheme)
        .AddCookie()
        .AddGitHub(options =>
        {
            options.ClientId = Configuration[GitHubClientId];
            options.ClientSecret = Configuration[GitHubClientSecret];
            options.Scope.Add("user:email");
            options.Events = new OAuthEvents
            {
                OnCreatingTicket = GetUserCompanyInfoAsync
            };
        });
    ```

4. <span data-ttu-id="ca412-157">Add the `GetUserCompanyInfoAsync` helper method to the `Startup` class.</span><span class="sxs-lookup"><span data-stu-id="ca412-157">Add the `GetUserCompanyInfoAsync` helper method to the `Startup` class.</span></span>    

    ```csharp
    private static async Task GetUserCompanyInfoAsync(OAuthCreatingTicketContext context)
    {
        var request = new HttpRequestMessage(HttpMethod.Get, context.Options.UserInformationEndpoint);
        request.Headers.Accept.Add(new MediaTypeWithQualityHeaderValue("application/json"));
        request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", context.AccessToken);

        var response = await context.Backchannel.SendAsync(request,
            HttpCompletionOption.ResponseHeadersRead, context.HttpContext.RequestAborted);

        var user = JObject.Parse(await response.Content.ReadAsStringAsync());
        if (user.ContainsKey("company"))
        {
            var company = user["company"].ToString();
            var companyIdentity = new ClaimsIdentity(new[]
            {
                new Claim("Company", company)
            });
            context.Principal.AddIdentity(companyIdentity);
        }
    }        
    ```

5. <span data-ttu-id="ca412-158">Update the `Configure` method of the Startup class with the following line of code, and save the file.</span><span class="sxs-lookup"><span data-stu-id="ca412-158">Update the `Configure` method of the Startup class with the following line of code, and save the file.</span></span>

        app.UseAuthentication();



### <a name="add-an-authentication-controller"></a><span data-ttu-id="ca412-159">Add an authentication controller</span><span class="sxs-lookup"><span data-stu-id="ca412-159">Add an authentication controller</span></span>

<span data-ttu-id="ca412-160">In this section, you will implement a `Login` API that authenticates clients using the GitHub OAuth app.</span><span class="sxs-lookup"><span data-stu-id="ca412-160">In this section, you will implement a `Login` API that authenticates clients using the GitHub OAuth app.</span></span> <span data-ttu-id="ca412-161">Once authenticated, the API will add a cookie to the web client response before redirecting the client back to the chat app.</span><span class="sxs-lookup"><span data-stu-id="ca412-161">Once authenticated, the API will add a cookie to the web client response before redirecting the client back to the chat app.</span></span> <span data-ttu-id="ca412-162">That cookie will then be used to identify the client.</span><span class="sxs-lookup"><span data-stu-id="ca412-162">That cookie will then be used to identify the client.</span></span>

1. <span data-ttu-id="ca412-163">Add a new controller code file to the *chattest\Controllers* directory.</span><span class="sxs-lookup"><span data-stu-id="ca412-163">Add a new controller code file to the *chattest\Controllers* directory.</span></span> <span data-ttu-id="ca412-164">Name the file *AuthController.cs*.</span><span class="sxs-lookup"><span data-stu-id="ca412-164">Name the file *AuthController.cs*.</span></span>

2. <span data-ttu-id="ca412-165">Add the following code for the authentication controller.</span><span class="sxs-lookup"><span data-stu-id="ca412-165">Add the following code for the authentication controller.</span></span> <span data-ttu-id="ca412-166">Make sure to update the namespace, if your project directory was not *chattest*:</span><span class="sxs-lookup"><span data-stu-id="ca412-166">Make sure to update the namespace, if your project directory was not *chattest*:</span></span>

    ```csharp
    using AspNet.Security.OAuth.GitHub;
    using Microsoft.AspNetCore.Authentication;
    using Microsoft.AspNetCore.Mvc;

    namespace chattest.Controllers
    {
        [Route("/")]
        public class AuthController : Controller
        {
            [HttpGet("login")]
            public IActionResult Login()
            {
                if (!User.Identity.IsAuthenticated)
                {
                    return Challenge(GitHubAuthenticationDefaults.AuthenticationScheme);
                }

                HttpContext.Response.Cookies.Append("githubchat_username", User.Identity.Name);
                HttpContext.SignInAsync(User);
                return Redirect("/");
            }
        }
    }    
    ```

3. <span data-ttu-id="ca412-167">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="ca412-167">Save your changes.</span></span>    

### <a name="update-the-hub-class"></a><span data-ttu-id="ca412-168">Update the Hub class</span><span class="sxs-lookup"><span data-stu-id="ca412-168">Update the Hub class</span></span>

<span data-ttu-id="ca412-169">By default when a web client attempts to connect to SignalR Service, the connection is granted based on an access token that is provided internally.</span><span class="sxs-lookup"><span data-stu-id="ca412-169">By default when a web client attempts to connect to SignalR Service, the connection is granted based on an access token that is provided internally.</span></span> <span data-ttu-id="ca412-170">This access token is not associated with an authenticated identity.</span><span class="sxs-lookup"><span data-stu-id="ca412-170">This access token is not associated with an authenticated identity.</span></span> <span data-ttu-id="ca412-171">This access is actually anonymous access.</span><span class="sxs-lookup"><span data-stu-id="ca412-171">This access is actually anonymous access.</span></span> 

<span data-ttu-id="ca412-172">In this section, you will turn on real authentication by adding the `Authorize` attribute to the hub class, and updating the hub methods to read the username from the authenticated user's claim.</span><span class="sxs-lookup"><span data-stu-id="ca412-172">In this section, you will turn on real authentication by adding the `Authorize` attribute to the hub class, and updating the hub methods to read the username from the authenticated user's claim.</span></span>

1. <span data-ttu-id="ca412-173">Open *Hub\Chat.cs* and add references to these namespaces:</span><span class="sxs-lookup"><span data-stu-id="ca412-173">Open *Hub\Chat.cs* and add references to these namespaces:</span></span>

    ```csharp
    using System.Threading.Tasks;
    using Microsoft.AspNetCore.Authorization;
    ```

2. <span data-ttu-id="ca412-174">Update the hub code as shown below.</span><span class="sxs-lookup"><span data-stu-id="ca412-174">Update the hub code as shown below.</span></span> <span data-ttu-id="ca412-175">This code adds the `Authorize` attribute to the `Chat` class, and uses the user's authenticated identity in the hub methods.</span><span class="sxs-lookup"><span data-stu-id="ca412-175">This code adds the `Authorize` attribute to the `Chat` class, and uses the user's authenticated identity in the hub methods.</span></span> <span data-ttu-id="ca412-176">Also, the `OnConnectedAsync` method is added, which will log a system message to the chat room each time a new client connects.</span><span class="sxs-lookup"><span data-stu-id="ca412-176">Also, the `OnConnectedAsync` method is added, which will log a system message to the chat room each time a new client connects.</span></span>

    ```csharp
    [Authorize]
    public class Chat : Hub
    {
        public override Task OnConnectedAsync()
        {
            return Clients.All.SendAsync("broadcastMessage", "_SYSTEM_", $"{Context.User.Identity.Name} JOINED");
        }

        // Uncomment this line to only allow user in Microsoft to send message
        //[Authorize(Policy = "Microsoft_Only")]
        public void BroadcastMessage(string message)
        {
            Clients.All.SendAsync("broadcastMessage", Context.User.Identity.Name, message);
        }

        public void Echo(string message)
        {
            var echoMessage = $"{message} (echo from server)";
            Clients.Client(Context.ConnectionId).SendAsync("echo", Context.User.Identity.Name, echoMessage);
        }
    }
    ```

3. <span data-ttu-id="ca412-177">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="ca412-177">Save your changes.</span></span>

### <a name="update-the-web-client-code"></a><span data-ttu-id="ca412-178">Update the web client code</span><span class="sxs-lookup"><span data-stu-id="ca412-178">Update the web client code</span></span>

1. <span data-ttu-id="ca412-179">Open *wwwroot\index.html* and replace the code that prompts for the username with code to use the cookie returned by the authentication controller.</span><span class="sxs-lookup"><span data-stu-id="ca412-179">Open *wwwroot\index.html* and replace the code that prompts for the username with code to use the cookie returned by the authentication controller.</span></span>

    <span data-ttu-id="ca412-180">Remove the following code from *index.html*:</span><span class="sxs-lookup"><span data-stu-id="ca412-180">Remove the following code from *index.html*:</span></span>

    ```javascript
    // Get the user name and store it to prepend to messages.
    var username = generateRandomName();
    var promptMessage = 'Enter your name:';
    do {
        username = prompt(promptMessage, username);
        if (!username || username.startsWith('_') || username.indexOf('<') > -1 || username.indexOf('>') > -1) {
            username = '';
            promptMessage = 'Invalid input. Enter your name:';
        }
    } while(!username)
    ```

    <span data-ttu-id="ca412-181">Add the following code in place of the code above to use the cookie:</span><span class="sxs-lookup"><span data-stu-id="ca412-181">Add the following code in place of the code above to use the cookie:</span></span>

    ```javascript
    // Get the user name cookie.
    function getCookie(key) {
        var cookies = document.cookie.split(';').map(c => c.trim());
        for (var i = 0; i < cookies.length; i++) {
            if (cookies[i].startsWith(key + '=')) return unescape(cookies[i].slice(key.length + 1));
        }
        return '';
    }
    var username = getCookie('githubchat_username');    
    ```

2. <span data-ttu-id="ca412-182">Just beneath the line of code you added to use the cookie, add the following definition for the `appendMessage` function:</span><span class="sxs-lookup"><span data-stu-id="ca412-182">Just beneath the line of code you added to use the cookie, add the following definition for the `appendMessage` function:</span></span>

    ```javascript
    function appendMessage(encodedName, encodedMsg) {
        var messageEntry = createMessageEntry(encodedName, encodedMsg);
        var messageBox = document.getElementById('messages');
        messageBox.appendChild(messageEntry);
        messageBox.scrollTop = messageBox.scrollHeight;
    }
    ```

3. <span data-ttu-id="ca412-183">Update the `bindConnectionMessage` and `onConnected` functions with the following code to use `appendMessage`.</span><span class="sxs-lookup"><span data-stu-id="ca412-183">Update the `bindConnectionMessage` and `onConnected` functions with the following code to use `appendMessage`.</span></span>

    ```javascript
    function bindConnectionMessage(connection) {
        var messageCallback = function(name, message) {
            if (!message) return;
            // Html encode display name and message.
            var encodedName = name;
            var encodedMsg = message.replace(/&/g, "&amp;").replace(/</g, "&lt;").replace(/>/g, "&gt;");
            appendMessage(encodedName, encodedMsg);
        };
        // Create a function that the hub can call to broadcast messages.
        connection.on('broadcastMessage', messageCallback);
        connection.on('echo', messageCallback);
        connection.onclose(onConnectionError);
    }

    function onConnected(connection) {
        console.log('connection started');
        document.getElementById('sendmessage').addEventListener('click', function (event) {
            // Call the broadcastMessage method on the hub.
            if (messageInput.value) {
                connection
                    .invoke('broadcastMessage', messageInput.value)
                    .catch(e => appendMessage('_BROADCAST_', e.message));
            }

            // Clear text box and reset focus for next comment.
            messageInput.value = '';
            messageInput.focus();
            event.preventDefault();
        });
        document.getElementById('message').addEventListener('keypress', function (event) {
            if (event.keyCode === 13) {
                event.preventDefault();
                document.getElementById('sendmessage').click();
                return false;
            }
        });
        document.getElementById('echo').addEventListener('click', function (event) {
            // Call the echo method on the hub.
            connection.send('echo', messageInput.value);

            // Clear text box and reset focus for next comment.
            messageInput.value = '';
            messageInput.focus();
            event.preventDefault();
        });
    }    
    ```    

4. <span data-ttu-id="ca412-184">At the bottom of *index.html*, update the error handler for `connection.start()` as shown below to prompt the user to log in.</span><span class="sxs-lookup"><span data-stu-id="ca412-184">At the bottom of *index.html*, update the error handler for `connection.start()` as shown below to prompt the user to log in.</span></span>

    ```javascript
    connection.start()
        .then(function () {
            onConnected(connection);
        })
        .catch(function (error) {
            if (error) {
                if (error.message) {
                    console.error(error.message);
                }
                if (error.statusCode && error.statusCode === 401) {
                    appendMessage('_BROADCAST_', 'You\'re not logged in. Click <a href="/login">here</a> to login with GitHub.');
                }
            }
        });
    ```

5. <span data-ttu-id="ca412-185">Save your changes.</span><span class="sxs-lookup"><span data-stu-id="ca412-185">Save your changes.</span></span>    



## <a name="build-and-run-the-app-locally"></a><span data-ttu-id="ca412-186">Build and Run the app locally</span><span class="sxs-lookup"><span data-stu-id="ca412-186">Build and Run the app locally</span></span>

1. <span data-ttu-id="ca412-187">Save changes to all files.</span><span class="sxs-lookup"><span data-stu-id="ca412-187">Save changes to all files.</span></span> 

2. <span data-ttu-id="ca412-188">Build the app using the .NET Core CLI, execute the following command in the command shell:</span><span class="sxs-lookup"><span data-stu-id="ca412-188">Build the app using the .NET Core CLI, execute the following command in the command shell:</span></span>

        dotnet build

3. <span data-ttu-id="ca412-189">Once the build successfully completes, execute the following command to run the web app locally:</span><span class="sxs-lookup"><span data-stu-id="ca412-189">Once the build successfully completes, execute the following command to run the web app locally:</span></span>

        dotnet run

    <span data-ttu-id="ca412-190">By default, the app will be hosted locally on port 5000:</span><span class="sxs-lookup"><span data-stu-id="ca412-190">By default, the app will be hosted locally on port 5000:</span></span>

        E:\Testing\chattest>dotnet run
        Hosting environment: Production
        Content root path: E:\Testing\chattest
        Now listening on: http://localhost:5000
        Application started. Press Ctrl+C to shut down.    

4. <span data-ttu-id="ca412-191">Launch a browser window and navigate to `http://localhost:5000`.</span><span class="sxs-lookup"><span data-stu-id="ca412-191">Launch a browser window and navigate to `http://localhost:5000`.</span></span> <span data-ttu-id="ca412-192">Click the **here** link at the top to log in with GitHub.</span><span class="sxs-lookup"><span data-stu-id="ca412-192">Click the **here** link at the top to log in with GitHub.</span></span> 

    ![OAuth Complete hosted in Azure](media/signalr-authenticate-oauth/signalr-oauth-complete-azure.png)

    <span data-ttu-id="ca412-194">You will be prompted to authorize the chat app's access to your GitHub account.</span><span class="sxs-lookup"><span data-stu-id="ca412-194">You will be prompted to authorize the chat app's access to your GitHub account.</span></span> <span data-ttu-id="ca412-195">Click the **Authorize** button.</span><span class="sxs-lookup"><span data-stu-id="ca412-195">Click the **Authorize** button.</span></span> 
    
    ![Authorize OAuth App](media/signalr-authenticate-oauth/signalr-authorize-oauth-app.png)
    
    <span data-ttu-id="ca412-197">You will be redirected back to the chat application and logged in with your GitHub account name.</span><span class="sxs-lookup"><span data-stu-id="ca412-197">You will be redirected back to the chat application and logged in with your GitHub account name.</span></span> <span data-ttu-id="ca412-198">The web application determined you account name by authenticating you using the new authentication you added.</span><span class="sxs-lookup"><span data-stu-id="ca412-198">The web application determined you account name by authenticating you using the new authentication you added.</span></span>

    ![Account identified](media/signalr-authenticate-oauth/signalr-oauth-account-identified.png)

    <span data-ttu-id="ca412-200">Now that the chat app performs authentication with GitHub and stores the authentication information as cookies, you should deploy it to Azure so other users can authenticate with their accounts and communicate from other workstations.</span><span class="sxs-lookup"><span data-stu-id="ca412-200">Now that the chat app performs authentication with GitHub and stores the authentication information as cookies, you should deploy it to Azure so other users can authenticate with their accounts and communicate from other workstations.</span></span> 


[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="deploy-the-app-to-azure"></a><span data-ttu-id="ca412-201">Deploy the app to Azure</span><span class="sxs-lookup"><span data-stu-id="ca412-201">Deploy the app to Azure</span></span>

<span data-ttu-id="ca412-202">In this section, you will use the Azure command-line interface (CLI) from the Azure Cloud Shell to create a new [Azure Web App](https://docs.microsoft.com/azure/app-service/) to host your ASP.NET application in Azure.</span><span class="sxs-lookup"><span data-stu-id="ca412-202">In this section, you will use the Azure command-line interface (CLI) from the Azure Cloud Shell to create a new [Azure Web App](https://docs.microsoft.com/azure/app-service/) to host your ASP.NET application in Azure.</span></span> <span data-ttu-id="ca412-203">The web app will be configured to use local Git deployment.</span><span class="sxs-lookup"><span data-stu-id="ca412-203">The web app will be configured to use local Git deployment.</span></span> <span data-ttu-id="ca412-204">The web app will also be configured with your SignalR connection string, GitHub OAuth app secrets, and a deployment user.</span><span class="sxs-lookup"><span data-stu-id="ca412-204">The web app will also be configured with your SignalR connection string, GitHub OAuth app secrets, and a deployment user.</span></span>

<span data-ttu-id="ca412-205">The steps in this section use the *signalr* extension for the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="ca412-205">The steps in this section use the *signalr* extension for the Azure CLI.</span></span> <span data-ttu-id="ca412-206">Execute the following command to install the *signalr* extension for the Azure CLI 2.0:</span><span class="sxs-lookup"><span data-stu-id="ca412-206">Execute the following command to install the *signalr* extension for the Azure CLI 2.0:</span></span>

```azurecli-interactive
az extension add -n signalr
```

<span data-ttu-id="ca412-207">When creating the following resources, make sure to use the same resource group that your SignalR Service resource resides in.</span><span class="sxs-lookup"><span data-stu-id="ca412-207">When creating the following resources, make sure to use the same resource group that your SignalR Service resource resides in.</span></span> <span data-ttu-id="ca412-208">This approach will make clean up a lot easier later when you want to remove all the resources.</span><span class="sxs-lookup"><span data-stu-id="ca412-208">This approach will make clean up a lot easier later when you want to remove all the resources.</span></span> <span data-ttu-id="ca412-209">The examples given assume you used the group name recommended in previous tutorials, *SignalRTestResources*.</span><span class="sxs-lookup"><span data-stu-id="ca412-209">The examples given assume you used the group name recommended in previous tutorials, *SignalRTestResources*.</span></span>


### <a name="create-the-web-app-and-plan"></a><span data-ttu-id="ca412-210">Create the web app and plan</span><span class="sxs-lookup"><span data-stu-id="ca412-210">Create the web app and plan</span></span>

<span data-ttu-id="ca412-211">Copy the text for the commands below and update the parameters.</span><span class="sxs-lookup"><span data-stu-id="ca412-211">Copy the text for the commands below and update the parameters.</span></span> <span data-ttu-id="ca412-212">Paste the updated script into the Azure Cloud Shell, and press **Enter** to create a new App Service plan and web app.</span><span class="sxs-lookup"><span data-stu-id="ca412-212">Paste the updated script into the Azure Cloud Shell, and press **Enter** to create a new App Service plan and web app.</span></span>

```azurecli-interactive
#========================================================================
#=== Update these variable for your resource group name.              ===
#========================================================================
ResourceGroupName=SignalRTestResources

#========================================================================
#=== Update these variable for your web app.                          ===
#========================================================================
WebAppName=myWebAppName
WebAppPlan=myAppServicePlanName

# Create an App Service plan.
az appservice plan create --name $WebAppPlan --resource-group $ResourceGroupName \
    --sku FREE

# Create the new Web App
az webapp create --name $WebAppName --resource-group $ResourceGroupName \
    --plan $WebAppPlan


```


| <span data-ttu-id="ca412-213">Parameter</span><span class="sxs-lookup"><span data-stu-id="ca412-213">Parameter</span></span> | <span data-ttu-id="ca412-214">Description</span><span class="sxs-lookup"><span data-stu-id="ca412-214">Description</span></span> |
| -------------------- | --------------- |
| <span data-ttu-id="ca412-215">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ca412-215">ResourceGroupName</span></span> | <span data-ttu-id="ca412-216">This resource group name was suggested in previous tutorials.</span><span class="sxs-lookup"><span data-stu-id="ca412-216">This resource group name was suggested in previous tutorials.</span></span> <span data-ttu-id="ca412-217">It is a good idea to keep all tutorial resources grouped together.</span><span class="sxs-lookup"><span data-stu-id="ca412-217">It is a good idea to keep all tutorial resources grouped together.</span></span> <span data-ttu-id="ca412-218">Use the same resource group you used in the previous tutorials.</span><span class="sxs-lookup"><span data-stu-id="ca412-218">Use the same resource group you used in the previous tutorials.</span></span> | 
| <span data-ttu-id="ca412-219">WebAppPlan</span><span class="sxs-lookup"><span data-stu-id="ca412-219">WebAppPlan</span></span> | <span data-ttu-id="ca412-220">Enter a new, unique, App Service Plan name.</span><span class="sxs-lookup"><span data-stu-id="ca412-220">Enter a new, unique, App Service Plan name.</span></span> | 
| <span data-ttu-id="ca412-221">WebAppName</span><span class="sxs-lookup"><span data-stu-id="ca412-221">WebAppName</span></span> | <span data-ttu-id="ca412-222">This will be the name of the new web app and part of the URL.</span><span class="sxs-lookup"><span data-stu-id="ca412-222">This will be the name of the new web app and part of the URL.</span></span> <span data-ttu-id="ca412-223">Use a unique name.</span><span class="sxs-lookup"><span data-stu-id="ca412-223">Use a unique name.</span></span> <span data-ttu-id="ca412-224">For example, signalrtestwebapp22665120.</span><span class="sxs-lookup"><span data-stu-id="ca412-224">For example, signalrtestwebapp22665120.</span></span>   | 



### <a name="add-app-settings-to-the-web-app"></a><span data-ttu-id="ca412-225">Add app settings to the web app</span><span class="sxs-lookup"><span data-stu-id="ca412-225">Add app settings to the web app</span></span>

<span data-ttu-id="ca412-226">In this section, you will add app settings for the following components:</span><span class="sxs-lookup"><span data-stu-id="ca412-226">In this section, you will add app settings for the following components:</span></span>

* <span data-ttu-id="ca412-227">SignalR Service resource connection string</span><span class="sxs-lookup"><span data-stu-id="ca412-227">SignalR Service resource connection string</span></span>
* <span data-ttu-id="ca412-228">GitHub OAuth app client ID</span><span class="sxs-lookup"><span data-stu-id="ca412-228">GitHub OAuth app client ID</span></span>
* <span data-ttu-id="ca412-229">GitHub OAuth app client secret</span><span class="sxs-lookup"><span data-stu-id="ca412-229">GitHub OAuth app client secret</span></span>

<span data-ttu-id="ca412-230">Copy the text for the commands below and update the parameters.</span><span class="sxs-lookup"><span data-stu-id="ca412-230">Copy the text for the commands below and update the parameters.</span></span> <span data-ttu-id="ca412-231">Paste the updated script into the Azure Cloud Shell, and press **Enter** to add the app settings:</span><span class="sxs-lookup"><span data-stu-id="ca412-231">Paste the updated script into the Azure Cloud Shell, and press **Enter** to add the app settings:</span></span>

```azurecli-interactive
#========================================================================
#=== Update these variables for your GitHub OAuth App.                ===
#========================================================================
GitHubClientId=1234567890
GitHubClientSecret=1234567890

#========================================================================
#=== Update these variables for your resources.                       ===
#========================================================================
ResourceGroupName=SignalRTestResources
SignalRServiceResource=mySignalRresourcename
WebAppName=myWebAppName

# Get the SignalR Service resource hostName
signalRhostname=$(az signalr show --name $SignalRServiceResource \
    --resource-group $ResourceGroupName --query hostName -o tsv)

# Get the SignalR primary key 
signalRprimarykey=$(az signalr key list --name $SignalRServiceResource \
    --resource-group $ResourceGroupName --query primaryKey -o tsv)

# Form the connection string to the service resource
connstring="Endpoint=https://$signalRhostname;AccessKey=$signalRprimarykey;"

#Add an app setting to the web app for the SignalR connection
az webapp config appsettings set --name $WebAppName \
    --resource-group $ResourceGroupName \
    --settings "Azure__SignalR__ConnectionString=$connstring" 

#Add the app settings to use with GitHub authentication
az webapp config appsettings set --name $WebAppName \
    --resource-group $ResourceGroupName \
    --settings "GitHubClientId=$GitHubClientId" 
az webapp config appsettings set --name $WebAppName \
    --resource-group $ResourceGroupName \
    --settings "GitHubClientSecret=$GitHubClientSecret" 

```

| <span data-ttu-id="ca412-232">Parameter</span><span class="sxs-lookup"><span data-stu-id="ca412-232">Parameter</span></span> | <span data-ttu-id="ca412-233">Description</span><span class="sxs-lookup"><span data-stu-id="ca412-233">Description</span></span> |
| -------------------- | --------------- |
| <span data-ttu-id="ca412-234">GitHubClientId</span><span class="sxs-lookup"><span data-stu-id="ca412-234">GitHubClientId</span></span> | <span data-ttu-id="ca412-235">Assign this variable the secret Client Id for your GitHub OAuth App.</span><span class="sxs-lookup"><span data-stu-id="ca412-235">Assign this variable the secret Client Id for your GitHub OAuth App.</span></span> |
| <span data-ttu-id="ca412-236">GitHubClientSecret</span><span class="sxs-lookup"><span data-stu-id="ca412-236">GitHubClientSecret</span></span> | <span data-ttu-id="ca412-237">Assign this variable the secret password for your GitHub OAuth App.</span><span class="sxs-lookup"><span data-stu-id="ca412-237">Assign this variable the secret password for your GitHub OAuth App.</span></span> |
| <span data-ttu-id="ca412-238">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ca412-238">ResourceGroupName</span></span> | <span data-ttu-id="ca412-239">Update this variable to be the same resource group name you used in the previous section.</span><span class="sxs-lookup"><span data-stu-id="ca412-239">Update this variable to be the same resource group name you used in the previous section.</span></span> | 
| <span data-ttu-id="ca412-240">SignalRServiceResource</span><span class="sxs-lookup"><span data-stu-id="ca412-240">SignalRServiceResource</span></span> | <span data-ttu-id="ca412-241">Update this variable with the name of the SignalR Service resource you created in the quickstart.</span><span class="sxs-lookup"><span data-stu-id="ca412-241">Update this variable with the name of the SignalR Service resource you created in the quickstart.</span></span> <span data-ttu-id="ca412-242">For example, signalrtestsvc48778624.</span><span class="sxs-lookup"><span data-stu-id="ca412-242">For example, signalrtestsvc48778624.</span></span> | 
| <span data-ttu-id="ca412-243">WebAppName</span><span class="sxs-lookup"><span data-stu-id="ca412-243">WebAppName</span></span> | <span data-ttu-id="ca412-244">Update this variable with the name of the new web app you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="ca412-244">Update this variable with the name of the new web app you created in the previous section.</span></span> | 



### <a name="configure-the-web-app-for-local-git-deployment"></a><span data-ttu-id="ca412-245">Configure the web app for local Git deployment</span><span class="sxs-lookup"><span data-stu-id="ca412-245">Configure the web app for local Git deployment</span></span>

<span data-ttu-id="ca412-246">In the Azure Cloud Shell, paste the following script.</span><span class="sxs-lookup"><span data-stu-id="ca412-246">In the Azure Cloud Shell, paste the following script.</span></span> <span data-ttu-id="ca412-247">This script creates a new deployment user name and password that you will use when deploying your code to the web app with Git.</span><span class="sxs-lookup"><span data-stu-id="ca412-247">This script creates a new deployment user name and password that you will use when deploying your code to the web app with Git.</span></span> <span data-ttu-id="ca412-248">The script also configures the web app for deployment with a local Git repository, and returns the Git deployment URL.</span><span class="sxs-lookup"><span data-stu-id="ca412-248">The script also configures the web app for deployment with a local Git repository, and returns the Git deployment URL.</span></span>

```azurecli-interactive
#========================================================================
#=== Update these variables for your resources.                       ===
#========================================================================
ResourceGroupName=SignalRTestResources
WebAppName=myWebAppName

#========================================================================
#=== Update these variables for your deployment user.                 ===
#========================================================================
DeploymentUserName=myUserName
DeploymentUserPassword=myPassword

# Add the desired deployment user name and password
az webapp deployment user set --user-name $DeploymentUserName \
    --password $DeploymentUserPassword

# Configure Git deployment and note the deployment URL in the output
az webapp deployment source config-local-git --name $WebAppName \
    --resource-group $ResourceGroupName \
    --query [url] -o tsv

```

| <span data-ttu-id="ca412-249">Parameter</span><span class="sxs-lookup"><span data-stu-id="ca412-249">Parameter</span></span> | <span data-ttu-id="ca412-250">Description</span><span class="sxs-lookup"><span data-stu-id="ca412-250">Description</span></span> |
| -------------------- | --------------- |
| <span data-ttu-id="ca412-251">DeploymentUserName</span><span class="sxs-lookup"><span data-stu-id="ca412-251">DeploymentUserName</span></span> | <span data-ttu-id="ca412-252">Choose a new deployment user name.</span><span class="sxs-lookup"><span data-stu-id="ca412-252">Choose a new deployment user name.</span></span> |
| <span data-ttu-id="ca412-253">DeploymentUserPassword</span><span class="sxs-lookup"><span data-stu-id="ca412-253">DeploymentUserPassword</span></span> | <span data-ttu-id="ca412-254">Choose a password for the new deployment user.</span><span class="sxs-lookup"><span data-stu-id="ca412-254">Choose a password for the new deployment user.</span></span> |
| <span data-ttu-id="ca412-255">ResourceGroupName</span><span class="sxs-lookup"><span data-stu-id="ca412-255">ResourceGroupName</span></span> | <span data-ttu-id="ca412-256">Use the same resource group name you used in the previous section.</span><span class="sxs-lookup"><span data-stu-id="ca412-256">Use the same resource group name you used in the previous section.</span></span> | 
| <span data-ttu-id="ca412-257">WebAppName</span><span class="sxs-lookup"><span data-stu-id="ca412-257">WebAppName</span></span> | <span data-ttu-id="ca412-258">This will be the name of the new web app you created previously.</span><span class="sxs-lookup"><span data-stu-id="ca412-258">This will be the name of the new web app you created previously.</span></span> | 


<span data-ttu-id="ca412-259">Make a note the Git deployment URL returned from this command.</span><span class="sxs-lookup"><span data-stu-id="ca412-259">Make a note the Git deployment URL returned from this command.</span></span> <span data-ttu-id="ca412-260">You will use this URL later.</span><span class="sxs-lookup"><span data-stu-id="ca412-260">You will use this URL later.</span></span>


### <a name="deploy-your-code-to-the-azure-web-app"></a><span data-ttu-id="ca412-261">Deploy your code to the Azure web app</span><span class="sxs-lookup"><span data-stu-id="ca412-261">Deploy your code to the Azure web app</span></span>

<span data-ttu-id="ca412-262">To deploy your code, execute the following commands in a Git shell.</span><span class="sxs-lookup"><span data-stu-id="ca412-262">To deploy your code, execute the following commands in a Git shell.</span></span>

1. <span data-ttu-id="ca412-263">Navigate to the root of your project directory.</span><span class="sxs-lookup"><span data-stu-id="ca412-263">Navigate to the root of your project directory.</span></span> <span data-ttu-id="ca412-264">If you don't have the project initialized with a Git repository, execute following command:</span><span class="sxs-lookup"><span data-stu-id="ca412-264">If you don't have the project initialized with a Git repository, execute following command:</span></span>

        git init

2. <span data-ttu-id="ca412-265">Add a remote for the Git deployment URL you noted earlier:</span><span class="sxs-lookup"><span data-stu-id="ca412-265">Add a remote for the Git deployment URL you noted earlier:</span></span>

        git remote add Azure <your git deployment url>

3. <span data-ttu-id="ca412-266">Stage all files in the initialized repository and add a commit.</span><span class="sxs-lookup"><span data-stu-id="ca412-266">Stage all files in the initialized repository and add a commit.</span></span>

        git add -A
        git commit -m "init commit"

4. <span data-ttu-id="ca412-267">Deploy your code to the web app in Azure.</span><span class="sxs-lookup"><span data-stu-id="ca412-267">Deploy your code to the web app in Azure.</span></span>        

        git push Azure master

    <span data-ttu-id="ca412-268">You will be prompted to authenticate in order to deploy the code to Azure.</span><span class="sxs-lookup"><span data-stu-id="ca412-268">You will be prompted to authenticate in order to deploy the code to Azure.</span></span> <span data-ttu-id="ca412-269">Enter the user name and password of the deployment user you created above.</span><span class="sxs-lookup"><span data-stu-id="ca412-269">Enter the user name and password of the deployment user you created above.</span></span>

### <a name="update-the-github-oauth-app"></a><span data-ttu-id="ca412-270">Update the GitHub OAuth app</span><span class="sxs-lookup"><span data-stu-id="ca412-270">Update the GitHub OAuth app</span></span> 

<span data-ttu-id="ca412-271">The last thing you need to do is update the **Homepage URL** and **Authorization callback URL** of the GitHub OAuth app to point to the new hosted app.</span><span class="sxs-lookup"><span data-stu-id="ca412-271">The last thing you need to do is update the **Homepage URL** and **Authorization callback URL** of the GitHub OAuth app to point to the new hosted app.</span></span>

1. <span data-ttu-id="ca412-272">Open [http://github.com](http://github.com) in a browser and navigate to your account's **Settings** > **Developer settings** > **Oauth Apps**.</span><span class="sxs-lookup"><span data-stu-id="ca412-272">Open [http://github.com](http://github.com) in a browser and navigate to your account's **Settings** > **Developer settings** > **Oauth Apps**.</span></span>

2. <span data-ttu-id="ca412-273">Click on your authentication app and update the **Homepage URL** and **Authorization callback URL** as shown below:</span><span class="sxs-lookup"><span data-stu-id="ca412-273">Click on your authentication app and update the **Homepage URL** and **Authorization callback URL** as shown below:</span></span>

    | <span data-ttu-id="ca412-274">Setting</span><span class="sxs-lookup"><span data-stu-id="ca412-274">Setting</span></span> | <span data-ttu-id="ca412-275">Example</span><span class="sxs-lookup"><span data-stu-id="ca412-275">Example</span></span> |
    | ------- | ------- |
    | <span data-ttu-id="ca412-276">Homepage URL</span><span class="sxs-lookup"><span data-stu-id="ca412-276">Homepage URL</span></span> | https://signalrtestwebapp22665120.azurewebsites.net/home |
    | <span data-ttu-id="ca412-277">Authorization callback URL</span><span class="sxs-lookup"><span data-stu-id="ca412-277">Authorization callback URL</span></span> | https://signalrtestwebapp22665120.azurewebsites.net/signin-github |


3. <span data-ttu-id="ca412-278">Navigate to your web app URL and test the application.</span><span class="sxs-lookup"><span data-stu-id="ca412-278">Navigate to your web app URL and test the application.</span></span>

    ![OAuth Complete hosted in Azure](media/signalr-authenticate-oauth/signalr-oauth-complete-azure.png)


## <a name="clean-up-resources"></a><span data-ttu-id="ca412-280">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ca412-280">Clean up resources</span></span>

<span data-ttu-id="ca412-281">If you will be continuing to the next tutorial, you can keep the resources created in this quickstart and reuse them with the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="ca412-281">If you will be continuing to the next tutorial, you can keep the resources created in this quickstart and reuse them with the next tutorial.</span></span>

<span data-ttu-id="ca412-282">Otherwise, if you are finished with the quickstart sample application, you can delete the Azure resources created in this quickstart to avoid charges.</span><span class="sxs-lookup"><span data-stu-id="ca412-282">Otherwise, if you are finished with the quickstart sample application, you can delete the Azure resources created in this quickstart to avoid charges.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="ca412-283">Deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span><span class="sxs-lookup"><span data-stu-id="ca412-283">Deleting a resource group is irreversible and that the resource group and all the resources in it are permanently deleted.</span></span> <span data-ttu-id="ca412-284">Make sure that you do not accidentally delete the wrong resource group or resources.</span><span class="sxs-lookup"><span data-stu-id="ca412-284">Make sure that you do not accidentally delete the wrong resource group or resources.</span></span> <span data-ttu-id="ca412-285">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span><span class="sxs-lookup"><span data-stu-id="ca412-285">If you created the resources for hosting this sample inside an existing resource group that contains resources you want to keep, you can delete each resource individually from their respective blades instead of deleting the resource group.</span></span>
> 
> 

<span data-ttu-id="ca412-286">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span><span class="sxs-lookup"><span data-stu-id="ca412-286">Sign in to the [Azure portal](https://portal.azure.com) and click **Resource groups**.</span></span>

<span data-ttu-id="ca412-287">In the **Filter by name...** textbox, type the name of your resource group.</span><span class="sxs-lookup"><span data-stu-id="ca412-287">In the **Filter by name...** textbox, type the name of your resource group.</span></span> <span data-ttu-id="ca412-288">The instructions for this article used a resource group named *SignalRTestResources*.</span><span class="sxs-lookup"><span data-stu-id="ca412-288">The instructions for this article used a resource group named *SignalRTestResources*.</span></span> <span data-ttu-id="ca412-289">On your resource group in the result list, click **...** then **Delete resource group**.</span><span class="sxs-lookup"><span data-stu-id="ca412-289">On your resource group in the result list, click **...** then **Delete resource group**.</span></span>

   
![Delete](./media/signalr-authenticate-oauth/signalr-delete-resource-group.png)


<span data-ttu-id="ca412-291">You will be asked to confirm the deletion of the resource group.</span><span class="sxs-lookup"><span data-stu-id="ca412-291">You will be asked to confirm the deletion of the resource group.</span></span> <span data-ttu-id="ca412-292">Type the name of your resource group to confirm, and click **Delete**.</span><span class="sxs-lookup"><span data-stu-id="ca412-292">Type the name of your resource group to confirm, and click **Delete**.</span></span>
   
<span data-ttu-id="ca412-293">After a few moments, the resource group and all of its contained resources are deleted.</span><span class="sxs-lookup"><span data-stu-id="ca412-293">After a few moments, the resource group and all of its contained resources are deleted.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca412-294">Next steps</span><span class="sxs-lookup"><span data-stu-id="ca412-294">Next steps</span></span>

<span data-ttu-id="ca412-295">In this tutorial, you added authentication with OAuth to provide a better approach to authentication with Azure SignalR Service.</span><span class="sxs-lookup"><span data-stu-id="ca412-295">In this tutorial, you added authentication with OAuth to provide a better approach to authentication with Azure SignalR Service.</span></span> <span data-ttu-id="ca412-296">To learn more about using Azure SignalR Server, continue to the Azure CLI samples for SignalR Service.</span><span class="sxs-lookup"><span data-stu-id="ca412-296">To learn more about using Azure SignalR Server, continue to the Azure CLI samples for SignalR Service.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ca412-297">Azure SignalR CLI Samples</span><span class="sxs-lookup"><span data-stu-id="ca412-297">Azure SignalR CLI Samples</span></span>](./signalr-cli-samples.md)
