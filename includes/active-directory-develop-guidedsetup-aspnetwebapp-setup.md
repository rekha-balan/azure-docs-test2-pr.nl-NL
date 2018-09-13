---
title: include file
description: include file
services: active-directory
author: andretms
ms.service: active-directory
ms.topic: include
ms.date: 05/08/2018
ms.author: andret
ms.custom: include file
ms.openlocfilehash: 9c7daf7bc947b08835148f6d09c58b47c9e0186b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "45068036"
---
## <a name="set-up-your-project"></a><span data-ttu-id="506cd-103">Set up your project</span><span class="sxs-lookup"><span data-stu-id="506cd-103">Set up your project</span></span>

<span data-ttu-id="506cd-104">This section shows the steps to install and configure the authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="506cd-104">This section shows the steps to install and configure the authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="506cd-105">Prefer to download this sample's Visual Studio project instead?</span><span class="sxs-lookup"><span data-stu-id="506cd-105">Prefer to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="506cd-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip to the [Configuration step](#register-your-application) to configure the code sample before executing.</span><span class="sxs-lookup"><span data-stu-id="506cd-106">[Download a project](https://github.com/AzureADQuickStarts/AppModelv2-WebApp-OpenIDConnect-DotNet/archive/master.zip) and skip to the [Configuration step](#register-your-application) to configure the code sample before executing.</span></span>

### <a name="create-your-aspnet-project"></a><span data-ttu-id="506cd-107">Create your ASP.NET project</span><span class="sxs-lookup"><span data-stu-id="506cd-107">Create your ASP.NET project</span></span>

1. <span data-ttu-id="506cd-108">In Visual Studio: `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="506cd-108">In Visual Studio: `File` > `New` > `Project`</span></span>
2. <span data-ttu-id="506cd-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="506cd-109">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
3. <span data-ttu-id="506cd-110">Name your application and click *OK*</span><span class="sxs-lookup"><span data-stu-id="506cd-110">Name your application and click *OK*</span></span>
4. <span data-ttu-id="506cd-111">Select `Empty` and select the checkbox to add `MVC` references</span><span class="sxs-lookup"><span data-stu-id="506cd-111">Select `Empty` and select the checkbox to add `MVC` references</span></span>

## <a name="add-authentication-components"></a><span data-ttu-id="506cd-112">Add authentication components</span><span class="sxs-lookup"><span data-stu-id="506cd-112">Add authentication components</span></span>

1. <span data-ttu-id="506cd-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="506cd-113">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="506cd-114">Add *OWIN middleware NuGet packages* by typing the following in the Package Manager Console window:</span><span class="sxs-lookup"><span data-stu-id="506cd-114">Add *OWIN middleware NuGet packages* by typing the following in the Package Manager Console window:</span></span>

    ```powershell
    Install-Package Microsoft.Owin.Security.OpenIdConnect
    Install-Package Microsoft.Owin.Security.Cookies
    Install-Package Microsoft.Owin.Host.SystemWeb
    ```

<!--start-collapse-->
> ### <a name="about-these-libraries"></a><span data-ttu-id="506cd-115">About these libraries</span><span class="sxs-lookup"><span data-stu-id="506cd-115">About these libraries</span></span>
><span data-ttu-id="506cd-116">The libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span><span class="sxs-lookup"><span data-stu-id="506cd-116">The libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="506cd-117">After authentication is completed and the token representing the user is sent to your application, OWIN middleware creates a session cookie.</span><span class="sxs-lookup"><span data-stu-id="506cd-117">After authentication is completed and the token representing the user is sent to your application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="506cd-118">The browser then uses this cookie on subsequent requests so the user doesn't need to retype the password, and no additional verification is needed.</span><span class="sxs-lookup"><span data-stu-id="506cd-118">The browser then uses this cookie on subsequent requests so the user doesn't need to retype the password, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-the-authentication-pipeline"></a><span data-ttu-id="506cd-119">Configure the authentication pipeline</span><span class="sxs-lookup"><span data-stu-id="506cd-119">Configure the authentication pipeline</span></span>
<span data-ttu-id="506cd-120">The steps below are used to create an OWIN middleware Startup Class to configure OpenID Connect authentication.</span><span class="sxs-lookup"><span data-stu-id="506cd-120">The steps below are used to create an OWIN middleware Startup Class to configure OpenID Connect authentication.</span></span> <span data-ttu-id="506cd-121">This class will be executed automatically when your IIS process starts.</span><span class="sxs-lookup"><span data-stu-id="506cd-121">This class will be executed automatically when your IIS process starts.</span></span>

> [!TIP]
> <span data-ttu-id="506cd-122">If your project doesn't have a `Startup.cs` file in the root folder:</span><span class="sxs-lookup"><span data-stu-id="506cd-122">If your project doesn't have a `Startup.cs` file in the root folder:</span></span>
> 1. <span data-ttu-id="506cd-123">Right-click on the project's root folder: > `Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="506cd-123">Right-click on the project's root folder: > `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="506cd-124">Name it `Startup.cs`</span><span class="sxs-lookup"><span data-stu-id="506cd-124">Name it `Startup.cs`</span></span>
>
>> <span data-ttu-id="506cd-125">Make sure the class selected is an OWIN Startup Class and not a standard C# class.</span><span class="sxs-lookup"><span data-stu-id="506cd-125">Make sure the class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="506cd-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above the namespace.</span><span class="sxs-lookup"><span data-stu-id="506cd-126">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above the namespace.</span></span>

1. <span data-ttu-id="506cd-127">Add *OWIN* and *Microsoft.IdentityModel* references to `Startup.cs`:</span><span class="sxs-lookup"><span data-stu-id="506cd-127">Add *OWIN* and *Microsoft.IdentityModel* references to `Startup.cs`:</span></span>

    ```csharp
    using Microsoft.Owin;
    using Owin;
    using Microsoft.IdentityModel.Protocols.OpenIdConnect;
    using Microsoft.IdentityModel.Tokens;
    using Microsoft.Owin.Security;
    using Microsoft.Owin.Security.Cookies;
    using Microsoft.Owin.Security.OpenIdConnect;
    using Microsoft.Owin.Security.Notifications;
    ```

2. <span data-ttu-id="506cd-128">Replace Startup class with the code below:</span><span class="sxs-lookup"><span data-stu-id="506cd-128">Replace Startup class with the code below:</span></span>

    ```csharp
    public class Startup
    {
        // The Client ID is used by the application to uniquely identify itself to Azure AD.
        string clientId = System.Configuration.ConfigurationManager.AppSettings["ClientId"];

        // RedirectUri is the URL where the user will be redirected to after they sign in.
        string redirectUri = System.Configuration.ConfigurationManager.AppSettings["RedirectUri"];

        // Tenant is the tenant ID (e.g. contoso.onmicrosoft.com, or 'common' for multi-tenant)
        static string tenant = System.Configuration.ConfigurationManager.AppSettings["Tenant"];

        // Authority is the URL for authority, composed by Azure Active Directory v2 endpoint and the tenant name (e.g. https://login.microsoftonline.com/contoso.onmicrosoft.com/v2.0)
        string authority = String.Format(System.Globalization.CultureInfo.InvariantCulture, System.Configuration.ConfigurationManager.AppSettings["Authority"], tenant);

        /// <summary>
        /// Configure OWIN to use OpenIdConnect 
        /// </summary>
        /// <param name="app"></param>
        public void Configuration(IAppBuilder app)
        {
            app.SetDefaultSignInAsAuthenticationType(CookieAuthenticationDefaults.AuthenticationType);

            app.UseCookieAuthentication(new CookieAuthenticationOptions());
            app.UseOpenIdConnectAuthentication(
                new OpenIdConnectAuthenticationOptions
                {
                    // Sets the ClientId, authority, RedirectUri as obtained from web.config
                    ClientId = clientId,
                    Authority = authority,
                    RedirectUri = redirectUri,
                    // PostLogoutRedirectUri is the page that users will be redirected to after sign-out. In this case, it is using the home page
                    PostLogoutRedirectUri = redirectUri,
                    Scope = OpenIdConnectScope.OpenIdProfile,
                    // ResponseType is set to request the id_token - which contains basic information about the signed-in user
                    ResponseType = OpenIdConnectResponseType.IdToken,
                    // ValidateIssuer set to false to allow personal and work accounts from any organization to sign in to your application
                    // To only allow users from a single organizations, set ValidateIssuer to true and 'tenant' setting in web.config to the tenant name
                    // To allow users from only a list of specific organizations, set ValidateIssuer to true and use ValidIssuers parameter 
                    TokenValidationParameters = new TokenValidationParameters()
                    {
                        ValidateIssuer = false
                    },
                    // OpenIdConnectAuthenticationNotifications configures OWIN to send notification of failed authentications to OnAuthenticationFailed method
                    Notifications = new OpenIdConnectAuthenticationNotifications
                    {
                        AuthenticationFailed = OnAuthenticationFailed
                    }
                }
            );
        }

        /// <summary>
        /// Handle failed authentication requests by redirecting the user to the home page with an error in the query string
        /// </summary>
        /// <param name="context"></param>
        /// <returns></returns>
        private Task OnAuthenticationFailed(AuthenticationFailedNotification<OpenIdConnectMessage, OpenIdConnectAuthenticationOptions> context)
        {
            context.HandleResponse();
            context.Response.Redirect("/?errormessage=" + context.Exception.Message);
            return Task.FromResult(0);
        }
    }
    ```

<!--start-collapse-->
> ### <a name="more-information"></a><span data-ttu-id="506cd-129">More Information</span><span class="sxs-lookup"><span data-stu-id="506cd-129">More Information</span></span>
> <span data-ttu-id="506cd-130">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the application to communicate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="506cd-130">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the application to communicate with Azure AD.</span></span> <span data-ttu-id="506cd-131">Because the OpenID Connect middleware uses cookies in the background, you also need to set up cookie authentication as the code above shows.</span><span class="sxs-lookup"><span data-stu-id="506cd-131">Because the OpenID Connect middleware uses cookies in the background, you also need to set up cookie authentication as the code above shows.</span></span> <span data-ttu-id="506cd-132">The *ValidateIssuer* value tells OpenIdConnect to not restrict access to one specific organization.</span><span class="sxs-lookup"><span data-stu-id="506cd-132">The *ValidateIssuer* value tells OpenIdConnect to not restrict access to one specific organization.</span></span>
<!--end-collapse-->

