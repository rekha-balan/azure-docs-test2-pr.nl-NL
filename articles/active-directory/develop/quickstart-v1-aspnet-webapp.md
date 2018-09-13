---
title: Azure AD v1 ASP.NET Web Server Getting Started | Microsoft Docs
description: Implementing Microsoft Sign-In on an ASP.NET solution with a traditional web browser based application using OpenID Connect standard
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mtillman
editor: ''
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.component: develop
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/23/2018
ms.author: andret
ms.openlocfilehash: 5353e22d7ae77adecfe126bb589d08c808752550
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857436"
---
<!--start-intro-->
# <a name="add-sign-in-with-microsoft-to-an-aspnet-web-app"></a><span data-ttu-id="9388d-103">Add sign-in with Microsoft to an ASP.NET web app</span><span class="sxs-lookup"><span data-stu-id="9388d-103">Add sign-in with Microsoft to an ASP.NET web app</span></span>

<span data-ttu-id="9388d-104">This guide demonstrates how to implement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="9388d-104">This guide demonstrates how to implement sign-in with Microsoft using an ASP.NET MVC solution with a traditional web browser-based application using OpenID Connect.</span></span> 

<span data-ttu-id="9388d-105">At the end of this guide, your application will accept sign ins of work and school accounts from organizations that have integrated with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9388d-105">At the end of this guide, your application will accept sign ins of work and school accounts from organizations that have integrated with Azure Active Directory.</span></span>

> [!NOTE]
> <span data-ttu-id="9388d-106">This guided setup helps you to enable sign-ins from work and school accounts in your ASP.NET application.</span><span class="sxs-lookup"><span data-stu-id="9388d-106">This guided setup helps you to enable sign-ins from work and school accounts in your ASP.NET application.</span></span> <span data-ttu-id="9388d-107">If you are interested to enable sign-ins for personal accounts in addition to work and school accounts, you can use the [v2 endpoint](azure-ad-endpoint-comparison.md).</span><span class="sxs-lookup"><span data-stu-id="9388d-107">If you are interested to enable sign-ins for personal accounts in addition to work and school accounts, you can use the [v2 endpoint](azure-ad-endpoint-comparison.md).</span></span> <span data-ttu-id="9388d-108">See [this ASP.NET guided setup for the v2 endpoint](tutorial-v2-asp-webapp.md) as well as [this document](active-directory-v2-limitations.md) explaining the current limitations of the v2 endpoint.</span><span class="sxs-lookup"><span data-stu-id="9388d-108">See [this ASP.NET guided setup for the v2 endpoint](tutorial-v2-asp-webapp.md) as well as [this document](active-directory-v2-limitations.md) explaining the current limitations of the v2 endpoint.</span></span>
<br/><br/>

<!--separator-->

> <span data-ttu-id="9388d-109">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="9388d-109">This guide requires Visual Studio 2015 Update 3 or Visual Studio 2017.</span></span>  <span data-ttu-id="9388d-110">Don’t have it?</span><span class="sxs-lookup"><span data-stu-id="9388d-110">Don’t have it?</span></span>  [<span data-ttu-id="9388d-111">Download Visual Studio 2017 for free</span><span class="sxs-lookup"><span data-stu-id="9388d-111">Download Visual Studio 2017 for free</span></span>](https://www.visualstudio.com/downloads/)

## <a name="how-this-guide-works"></a><span data-ttu-id="9388d-112">How this guide works</span><span class="sxs-lookup"><span data-stu-id="9388d-112">How this guide works</span></span>

![How this guide works](./media/quickstart-v1-aspnet-webapp/aspnet-intro.png)

<span data-ttu-id="9388d-114">This guide is based on the scenario where a browser accesses an ASP.NET web site, requesting a user to authenticate via a sign-in button.</span><span class="sxs-lookup"><span data-stu-id="9388d-114">This guide is based on the scenario where a browser accesses an ASP.NET web site, requesting a user to authenticate via a sign-in button.</span></span> <span data-ttu-id="9388d-115">In this scenario, most of the work to render the web page occurs on the server side.</span><span class="sxs-lookup"><span data-stu-id="9388d-115">In this scenario, most of the work to render the web page occurs on the server side.</span></span>

> [!NOTE]
> <span data-ttu-id="9388d-116">This guided setup demonstrates how to sign in users on an ASP.NET Web Application starting from an empty template, and include steps such as adding a sign in button and every controller and methods, while also explaining some concepts.</span><span class="sxs-lookup"><span data-stu-id="9388d-116">This guided setup demonstrates how to sign in users on an ASP.NET Web Application starting from an empty template, and include steps such as adding a sign in button and every controller and methods, while also explaining some concepts.</span></span> <span data-ttu-id="9388d-117">Alternatively, you can also create a project to sign-in Azure Active Directory users (work and school accounts) by using the [Visual Studio web template](https://docs.microsoft.com/aspnet/visual-studio/overview/2013/creating-web-projects-in-visual-studio#organizational-account-authentication-options) and selecting *Organizational Accounts* and then one of the cloud options - this option uses a richer template, with additional controllers, methods and views.</span><span class="sxs-lookup"><span data-stu-id="9388d-117">Alternatively, you can also create a project to sign-in Azure Active Directory users (work and school accounts) by using the [Visual Studio web template](https://docs.microsoft.com/aspnet/visual-studio/overview/2013/creating-web-projects-in-visual-studio#organizational-account-authentication-options) and selecting *Organizational Accounts* and then one of the cloud options - this option uses a richer template, with additional controllers, methods and views.</span></span>

## <a name="libraries"></a><span data-ttu-id="9388d-118">Libraries</span><span class="sxs-lookup"><span data-stu-id="9388d-118">Libraries</span></span>

<span data-ttu-id="9388d-119">This guide uses the following packages:</span><span class="sxs-lookup"><span data-stu-id="9388d-119">This guide uses the following packages:</span></span>

|<span data-ttu-id="9388d-120">Library</span><span class="sxs-lookup"><span data-stu-id="9388d-120">Library</span></span>|<span data-ttu-id="9388d-121">Description</span><span class="sxs-lookup"><span data-stu-id="9388d-121">Description</span></span>|
|---|---|
|[<span data-ttu-id="9388d-122">Microsoft.Owin.Security.OpenIdConnect</span><span class="sxs-lookup"><span data-stu-id="9388d-122">Microsoft.Owin.Security.OpenIdConnect</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.OpenIdConnect/)|<span data-ttu-id="9388d-123">Middleware that enables an application to use OpenIdConnect for authentication</span><span class="sxs-lookup"><span data-stu-id="9388d-123">Middleware that enables an application to use OpenIdConnect for authentication</span></span>|
|[<span data-ttu-id="9388d-124">Microsoft.Owin.Security.Cookies</span><span class="sxs-lookup"><span data-stu-id="9388d-124">Microsoft.Owin.Security.Cookies</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Security.Cookies)|<span data-ttu-id="9388d-125">Middleware that enables an application to maintain user session using cookies</span><span class="sxs-lookup"><span data-stu-id="9388d-125">Middleware that enables an application to maintain user session using cookies</span></span>|
|[<span data-ttu-id="9388d-126">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="9388d-126">Microsoft.Owin.Host.SystemWeb</span></span>](https://www.nuget.org/packages/Microsoft.Owin.Host.SystemWeb)|<span data-ttu-id="9388d-127">Enables OWIN-based applications to run on IIS using the ASP.NET request pipeline</span><span class="sxs-lookup"><span data-stu-id="9388d-127">Enables OWIN-based applications to run on IIS using the ASP.NET request pipeline</span></span>|


<!--end-intro-->

<!--start-setup-->

## <a name="set-up-your-project"></a><span data-ttu-id="9388d-128">Set up your project</span><span class="sxs-lookup"><span data-stu-id="9388d-128">Set up your project</span></span>

<span data-ttu-id="9388d-129">This section shows the steps to install and configure the authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span><span class="sxs-lookup"><span data-stu-id="9388d-129">This section shows the steps to install and configure the authentication pipeline via OWIN middleware on an ASP.NET project using OpenID Connect.</span></span> 

> <span data-ttu-id="9388d-130">Prefer to download this sample's Visual Studio project instead?</span><span class="sxs-lookup"><span data-stu-id="9388d-130">Prefer to download this sample's Visual Studio project instead?</span></span> <span data-ttu-id="9388d-131">[Download a project](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/GuidedSetup.zip) and skip to the [Configuration step](#configure-your-webconfig-and-register-an-application) to configure the code sample before executing.</span><span class="sxs-lookup"><span data-stu-id="9388d-131">[Download a project](https://github.com/AzureADQuickStarts/WebApp-OpenIdConnect-DotNet/archive/GuidedSetup.zip) and skip to the [Configuration step](#configure-your-webconfig-and-register-an-application) to configure the code sample before executing.</span></span>

## <a name="create-your-aspnet-project"></a><span data-ttu-id="9388d-132">Create your ASP.NET project</span><span class="sxs-lookup"><span data-stu-id="9388d-132">Create your ASP.NET project</span></span>
1. <span data-ttu-id="9388d-133">In Visual Studio: `File` > `New` > `Project`</span><span class="sxs-lookup"><span data-stu-id="9388d-133">In Visual Studio: `File` > `New` > `Project`</span></span><br/>
2. <span data-ttu-id="9388d-134">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span><span class="sxs-lookup"><span data-stu-id="9388d-134">Under *Visual C#\Web*, select `ASP.NET Web Application (.NET Framework)`.</span></span>
3. <span data-ttu-id="9388d-135">Name your application and click *OK*</span><span class="sxs-lookup"><span data-stu-id="9388d-135">Name your application and click *OK*</span></span>
4. <span data-ttu-id="9388d-136">Select `Empty` and then select the checkbox to add `MVC` references</span><span class="sxs-lookup"><span data-stu-id="9388d-136">Select `Empty` and then select the checkbox to add `MVC` references</span></span>

## <a name="add-authentication-components"></a><span data-ttu-id="9388d-137">Add authentication components</span><span class="sxs-lookup"><span data-stu-id="9388d-137">Add authentication components</span></span>

1. <span data-ttu-id="9388d-138">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span><span class="sxs-lookup"><span data-stu-id="9388d-138">In Visual Studio: `Tools` > `Nuget Package Manager` > `Package Manager Console`</span></span>
2. <span data-ttu-id="9388d-139">Add *OWIN middleware NuGet packages* by typing the following in the Package Manager Console window:</span><span class="sxs-lookup"><span data-stu-id="9388d-139">Add *OWIN middleware NuGet packages* by typing the following in the Package Manager Console window:</span></span>

    ```powershell
    Install-Package Microsoft.Owin.Security.OpenIdConnect
    Install-Package Microsoft.Owin.Security.Cookies
    Install-Package Microsoft.Owin.Host.SystemWeb
    ```

<!--start-collapse-->
> ### <a name="about-these-packages"></a><span data-ttu-id="9388d-140">About these packages</span><span class="sxs-lookup"><span data-stu-id="9388d-140">About these packages</span></span>
><span data-ttu-id="9388d-141">The libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span><span class="sxs-lookup"><span data-stu-id="9388d-141">The libraries above enable single sign-on (SSO) using OpenID Connect via cookie-based authentication.</span></span> <span data-ttu-id="9388d-142">After authentication is completed and the token representing the user is sent to your application, OWIN middleware creates a session cookie.</span><span class="sxs-lookup"><span data-stu-id="9388d-142">After authentication is completed and the token representing the user is sent to your application, OWIN middleware creates a session cookie.</span></span> <span data-ttu-id="9388d-143">The browser then uses this cookie on subsequent requests so the user doesn't need to reauthenticate, and no additional verification is needed.</span><span class="sxs-lookup"><span data-stu-id="9388d-143">The browser then uses this cookie on subsequent requests so the user doesn't need to reauthenticate, and no additional verification is needed.</span></span>
<!--end-collapse-->

## <a name="configure-the-authentication-pipeline"></a><span data-ttu-id="9388d-144">Configure the authentication pipeline</span><span class="sxs-lookup"><span data-stu-id="9388d-144">Configure the authentication pipeline</span></span>
<span data-ttu-id="9388d-145">The following steps are used to create an OWIN middleware *Startup Class* to configure OpenID Connect authentication.</span><span class="sxs-lookup"><span data-stu-id="9388d-145">The following steps are used to create an OWIN middleware *Startup Class* to configure OpenID Connect authentication.</span></span> <span data-ttu-id="9388d-146">This class is executed automatically.</span><span class="sxs-lookup"><span data-stu-id="9388d-146">This class is executed automatically.</span></span>

> [!TIP]
> <span data-ttu-id="9388d-147">If your project doesn't have a `Startup.cs` file in the root folder:</span><span class="sxs-lookup"><span data-stu-id="9388d-147">If your project doesn't have a `Startup.cs` file in the root folder:</span></span><br/>
> 1. <span data-ttu-id="9388d-148">Right-click on the project's root folder: >    `Add` > `New Item...` > `OWIN Startup class`</span><span class="sxs-lookup"><span data-stu-id="9388d-148">Right-click on the project's root folder: >    `Add` > `New Item...` > `OWIN Startup class`</span></span><br/>
> 2. <span data-ttu-id="9388d-149">Name it `Startup.cs`</span><span class="sxs-lookup"><span data-stu-id="9388d-149">Name it `Startup.cs`</span></span><br/>
>
>> <span data-ttu-id="9388d-150">Make sure the class selected is an OWIN Startup Class and not a standard C# class.</span><span class="sxs-lookup"><span data-stu-id="9388d-150">Make sure the class selected is an OWIN Startup Class and not a standard C# class.</span></span> <span data-ttu-id="9388d-151">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above the namespace.</span><span class="sxs-lookup"><span data-stu-id="9388d-151">Confirm this by checking if you see `[assembly: OwinStartup(typeof({NameSpace}.Startup))]` above the namespace.</span></span>


1. <span data-ttu-id="9388d-152">Add *OWIN* and *Microsoft.IdentityModel* namespaces to `Startup.cs`:</span><span class="sxs-lookup"><span data-stu-id="9388d-152">Add *OWIN* and *Microsoft.IdentityModel* namespaces to `Startup.cs`:</span></span>

    [!code-csharp[main](../../../WebApp-OpenIDConnect-DotNet/WebApp-OpenIDConnect-DotNet\Startup.cs?name=AddedNameSpaces "Startup.cs")]

2. <span data-ttu-id="9388d-153">Replace Startup class with the following code:</span><span class="sxs-lookup"><span data-stu-id="9388d-153">Replace Startup class with the following code:</span></span>

    [!code-csharp[main](../../../WebApp-OpenIDConnect-DotNet/WebApp-OpenIDConnect-DotNet\Startup.cs?name=Startup "Startup.cs")]
    
<!--start-collapse-->
> [!NOTE]
> <span data-ttu-id="9388d-154">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the application to communicate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9388d-154">The parameters you provide in *OpenIDConnectAuthenticationOptions* serve as coordinates for the application to communicate with Azure AD.</span></span> <span data-ttu-id="9388d-155">Because the OpenID Connect middleware uses cookies, you also need to set up cookie authentication as the preceding code shows.</span><span class="sxs-lookup"><span data-stu-id="9388d-155">Because the OpenID Connect middleware uses cookies, you also need to set up cookie authentication as the preceding code shows.</span></span> <span data-ttu-id="9388d-156">The *ValidateIssuer* value tells OpenIdConnect to not restrict access to one specific organization.</span><span class="sxs-lookup"><span data-stu-id="9388d-156">The *ValidateIssuer* value tells OpenIdConnect to not restrict access to one specific organization.</span></span>
<!--end-collapse-->

<!--end-setup-->

<!--start-use-->

## <a name="add-a-controller-to-handle-sign-in-and-sign-out-requests"></a><span data-ttu-id="9388d-157">Add a controller to handle sign-in and sign-out requests</span><span class="sxs-lookup"><span data-stu-id="9388d-157">Add a controller to handle sign-in and sign-out requests</span></span>

<span data-ttu-id="9388d-158">This step shows how to create a new controller to expose sign-in and sign-out methods.</span><span class="sxs-lookup"><span data-stu-id="9388d-158">This step shows how to create a new controller to expose sign-in and sign-out methods.</span></span>

1.  <span data-ttu-id="9388d-159">Right-click the `Controllers` folder and select `Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="9388d-159">Right-click the `Controllers` folder and select `Add` > `Controller`</span></span>
2.  <span data-ttu-id="9388d-160">Select `MVC (.NET version) Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="9388d-160">Select `MVC (.NET version) Controller – Empty`.</span></span>
3.  <span data-ttu-id="9388d-161">Click *Add*</span><span class="sxs-lookup"><span data-stu-id="9388d-161">Click *Add*</span></span>
4.  <span data-ttu-id="9388d-162">Name it `HomeController` and click *Add*</span><span class="sxs-lookup"><span data-stu-id="9388d-162">Name it `HomeController` and click *Add*</span></span>
5.  <span data-ttu-id="9388d-163">Add *OWIN* namespaces to the class:</span><span class="sxs-lookup"><span data-stu-id="9388d-163">Add *OWIN* namespaces to the class:</span></span>

    [!code-csharp[main](../../../WebApp-OpenIDConnect-DotNet/WebApp-OpenIDConnect-DotNet\Controllers\HomeController.cs?name=AddedNameSpaces "HomeController.cs")]

6. <span data-ttu-id="9388d-164">Add the following methods to handle sign-in and sign-out to your controller by initiating an authentication challenge via code:</span><span class="sxs-lookup"><span data-stu-id="9388d-164">Add the following methods to handle sign-in and sign-out to your controller by initiating an authentication challenge via code:</span></span>

    [!code-csharp[main](../../../WebApp-OpenIDConnect-DotNet/WebApp-OpenIDConnect-DotNet\Controllers\HomeController.cs?name=SigInAndSignOut "HomeController.cs")]
    
## <a name="create-the-apps-home-page-to-sign-in-users-via-a-sign-in-button"></a><span data-ttu-id="9388d-165">Create the app's home page to sign in users via a sign-in button</span><span class="sxs-lookup"><span data-stu-id="9388d-165">Create the app's home page to sign in users via a sign-in button</span></span>

<span data-ttu-id="9388d-166">In Visual Studio, create a new view to add the sign-in button and display user information after authentication:</span><span class="sxs-lookup"><span data-stu-id="9388d-166">In Visual Studio, create a new view to add the sign-in button and display user information after authentication:</span></span>

1.  <span data-ttu-id="9388d-167">Right-click the `Views\Home` folder and select `Add View`</span><span class="sxs-lookup"><span data-stu-id="9388d-167">Right-click the `Views\Home` folder and select `Add View`</span></span>
2.  <span data-ttu-id="9388d-168">Name it `Index`.</span><span class="sxs-lookup"><span data-stu-id="9388d-168">Name it `Index`.</span></span>
3.  <span data-ttu-id="9388d-169">Add the following HTML, which includes the sign-in button, to the file:</span><span class="sxs-lookup"><span data-stu-id="9388d-169">Add the following HTML, which includes the sign-in button, to the file:</span></span>

    [!code-html[main](../../../WebApp-OpenIDConnect-DotNet/WebApp-OpenIDConnect-DotNet/Views/Home/Index.cshtml "Index.cshtml")]

<!--start-collapse-->
> [!NOTE]
> <span data-ttu-id="9388d-170">This page adds a sign-in button in SVG format with a black background:</span><span class="sxs-lookup"><span data-stu-id="9388d-170">This page adds a sign-in button in SVG format with a black background:</span></span><br/><span data-ttu-id="9388d-171">![Sign-in with Microsoft](./media/quickstart-v1-aspnet-webapp/aspnetsigninbuttonsample.png)</span><span class="sxs-lookup"><span data-stu-id="9388d-171">![Sign-in with Microsoft](./media/quickstart-v1-aspnet-webapp/aspnetsigninbuttonsample.png)</span></span><br/> <span data-ttu-id="9388d-172">For more sign-in buttons, go to [this page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span><span class="sxs-lookup"><span data-stu-id="9388d-172">For more sign-in buttons, go to [this page](https://docs.microsoft.com/azure/active-directory/develop/active-directory-branding-guidelines "Branding guidelines").</span></span>
<!--end-collapse-->

## <a name="display-users-claims-by-adding-a-controller"></a><span data-ttu-id="9388d-173">Display user's claims by adding a controller</span><span class="sxs-lookup"><span data-stu-id="9388d-173">Display user's claims by adding a controller</span></span>
<span data-ttu-id="9388d-174">This controller demonstrates the uses of the `[Authorize]` attribute to protect a controller.</span><span class="sxs-lookup"><span data-stu-id="9388d-174">This controller demonstrates the uses of the `[Authorize]` attribute to protect a controller.</span></span> <span data-ttu-id="9388d-175">This attribute restricts access to the controller by only allowing authenticated users.</span><span class="sxs-lookup"><span data-stu-id="9388d-175">This attribute restricts access to the controller by only allowing authenticated users.</span></span> <span data-ttu-id="9388d-176">The following code makes use of the attribute to display user claims that were retrieved as part of the sign-in.</span><span class="sxs-lookup"><span data-stu-id="9388d-176">The following code makes use of the attribute to display user claims that were retrieved as part of the sign-in.</span></span>

1.  <span data-ttu-id="9388d-177">Right-click the `Controllers` folder: `Add` > `Controller`</span><span class="sxs-lookup"><span data-stu-id="9388d-177">Right-click the `Controllers` folder: `Add` > `Controller`</span></span>
2.  <span data-ttu-id="9388d-178">Select `MVC {version} Controller – Empty`.</span><span class="sxs-lookup"><span data-stu-id="9388d-178">Select `MVC {version} Controller – Empty`.</span></span>
3.  <span data-ttu-id="9388d-179">Click *Add*</span><span class="sxs-lookup"><span data-stu-id="9388d-179">Click *Add*</span></span>
4.  <span data-ttu-id="9388d-180">Name it `ClaimsController`</span><span class="sxs-lookup"><span data-stu-id="9388d-180">Name it `ClaimsController`</span></span>
5.  <span data-ttu-id="9388d-181">Replace the code of your controller class with the following code - this adds the `[Authorize]` attribute to the class:</span><span class="sxs-lookup"><span data-stu-id="9388d-181">Replace the code of your controller class with the following code - this adds the `[Authorize]` attribute to the class:</span></span>

    [!code-csharp[main](../../../WebApp-OpenIDConnect-DotNet/WebApp-OpenIDConnect-DotNet\Controllers\ClaimsController.cs?name=ClaimsController "ClaimsController.cs")]

<!--start-collapse-->
> [!NOTE]
> <span data-ttu-id="9388d-182">Because of the use of the `[Authorize]` attribute, all methods of this controller can only be executed if the user is authenticated.</span><span class="sxs-lookup"><span data-stu-id="9388d-182">Because of the use of the `[Authorize]` attribute, all methods of this controller can only be executed if the user is authenticated.</span></span> <span data-ttu-id="9388d-183">If the user is not authenticated and tries to access the controller, OWIN initiates an authentication challenge and force the user to authenticate.</span><span class="sxs-lookup"><span data-stu-id="9388d-183">If the user is not authenticated and tries to access the controller, OWIN initiates an authentication challenge and force the user to authenticate.</span></span> <span data-ttu-id="9388d-184">The code above looks at the claims collection of the user for specific attributes included in the user’s token.</span><span class="sxs-lookup"><span data-stu-id="9388d-184">The code above looks at the claims collection of the user for specific attributes included in the user’s token.</span></span> <span data-ttu-id="9388d-185">These attributes include the user’s full name and username, as well as the global user identifier subject.</span><span class="sxs-lookup"><span data-stu-id="9388d-185">These attributes include the user’s full name and username, as well as the global user identifier subject.</span></span> <span data-ttu-id="9388d-186">It also contains the *Tenant ID*, which represents the ID for the user’s organization.</span><span class="sxs-lookup"><span data-stu-id="9388d-186">It also contains the *Tenant ID*, which represents the ID for the user’s organization.</span></span> 
<!--end-collapse-->

## <a name="create-a-view-to-display-the-users-claims"></a><span data-ttu-id="9388d-187">Create a view to display the user's claims</span><span class="sxs-lookup"><span data-stu-id="9388d-187">Create a view to display the user's claims</span></span>

<span data-ttu-id="9388d-188">In Visual Studio, create a new view to display the user's claims in a web page:</span><span class="sxs-lookup"><span data-stu-id="9388d-188">In Visual Studio, create a new view to display the user's claims in a web page:</span></span>

1.  <span data-ttu-id="9388d-189">Right-click the `Views\Claims` folder and: `Add View`</span><span class="sxs-lookup"><span data-stu-id="9388d-189">Right-click the `Views\Claims` folder and: `Add View`</span></span>
2.  <span data-ttu-id="9388d-190">Name it `Index`.</span><span class="sxs-lookup"><span data-stu-id="9388d-190">Name it `Index`.</span></span>
3.  <span data-ttu-id="9388d-191">Add the following HTML to the file:</span><span class="sxs-lookup"><span data-stu-id="9388d-191">Add the following HTML to the file:</span></span>

    [!code-html[main](../../../WebApp-OpenIDConnect-DotNet/WebApp-OpenIDConnect-DotNet/Views/Claims/Index.cshtml "Index.cshtml")]
    
<!--end-use-->

<!--start-configure-->
## <a name="configure-your-webconfig-and-register-an-application"></a><span data-ttu-id="9388d-192">Configure your *web.config* and register an application</span><span class="sxs-lookup"><span data-stu-id="9388d-192">Configure your *web.config* and register an application</span></span>

1. <span data-ttu-id="9388d-193">In Visual Studio, add the following to `web.config` (located in the root folder) under the section `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="9388d-193">In Visual Studio, add the following to `web.config` (located in the root folder) under the section `configuration\appSettings`:</span></span>

    ```xml
    <add key="ClientId" value="Enter_the_Application_Id_here" />
    <add key="RedirectUrl" value="Enter_the_Redirect_Url_here" />
    <add key="Tenant" value="common" />
    <add key="Authority" value="https://login.microsoftonline.com/{0}" /> 
    ```
2. <span data-ttu-id="9388d-194">In Solution Explorer, select the project and look at the <i>Properties</i> window (if you don’t see a Properties window, press F4)</span><span class="sxs-lookup"><span data-stu-id="9388d-194">In Solution Explorer, select the project and look at the <i>Properties</i> window (if you don’t see a Properties window, press F4)</span></span>
3. <span data-ttu-id="9388d-195">Change SSL Enabled to <code>True</code></span><span class="sxs-lookup"><span data-stu-id="9388d-195">Change SSL Enabled to <code>True</code></span></span>
4. <span data-ttu-id="9388d-196">Copy the project's SSL URL to the clipboard:</span><span class="sxs-lookup"><span data-stu-id="9388d-196">Copy the project's SSL URL to the clipboard:</span></span><br/><br/>![Project properties](./media/quickstart-v1-aspnet-webapp/visual-studio-project-properties.png)<br />
5. <span data-ttu-id="9388d-198">In <code>web.config</code>, replace <code>Enter_the_Redirect_URL_here</code> with the SSL URL of your project</span><span class="sxs-lookup"><span data-stu-id="9388d-198">In <code>web.config</code>, replace <code>Enter_the_Redirect_URL_here</code> with the SSL URL of your project</span></span> 

### <a name="register-your-application-in-the-azure-portal-then-add-its-information-to-webconfig"></a><span data-ttu-id="9388d-199">Register your application in the Azure Portal, then add its information to *web.config*</span><span class="sxs-lookup"><span data-stu-id="9388d-199">Register your application in the Azure Portal, then add its information to *web.config*</span></span>

1. <span data-ttu-id="9388d-200">Go to the [Microsoft Azure Portal - App registrations](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) to register an application</span><span class="sxs-lookup"><span data-stu-id="9388d-200">Go to the [Microsoft Azure Portal - App registrations](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) to register an application</span></span>
2. <span data-ttu-id="9388d-201">Select `New application registration`</span><span class="sxs-lookup"><span data-stu-id="9388d-201">Select `New application registration`</span></span>
3. <span data-ttu-id="9388d-202">Enter a name for your application</span><span class="sxs-lookup"><span data-stu-id="9388d-202">Enter a name for your application</span></span>
4. <span data-ttu-id="9388d-203">Paste the Visual Studio project's *SSL URL* in `Sign-on URL` (This URL is also added automatically to the list of Reply URLs for the application you are registering)</span><span class="sxs-lookup"><span data-stu-id="9388d-203">Paste the Visual Studio project's *SSL URL* in `Sign-on URL` (This URL is also added automatically to the list of Reply URLs for the application you are registering)</span></span>
5. <span data-ttu-id="9388d-204">Click `Create` to register the application.</span><span class="sxs-lookup"><span data-stu-id="9388d-204">Click `Create` to register the application.</span></span> <span data-ttu-id="9388d-205">This action takes you back to the list of applications</span><span class="sxs-lookup"><span data-stu-id="9388d-205">This action takes you back to the list of applications</span></span>
6. <span data-ttu-id="9388d-206">Now, search and/or select the application you just created to open its properties</span><span class="sxs-lookup"><span data-stu-id="9388d-206">Now, search and/or select the application you just created to open its properties</span></span>
7. <span data-ttu-id="9388d-207">Copy the guid under `Application ID` to the clipboard</span><span class="sxs-lookup"><span data-stu-id="9388d-207">Copy the guid under `Application ID` to the clipboard</span></span>
8. <span data-ttu-id="9388d-208">Go back to Visual Studio and, in `web.config`, replace `Enter_the_Application_Id_here` with the Application ID from the application you just registered</span><span class="sxs-lookup"><span data-stu-id="9388d-208">Go back to Visual Studio and, in `web.config`, replace `Enter_the_Application_Id_here` with the Application ID from the application you just registered</span></span>

> [!TIP]
> <span data-ttu-id="9388d-209">If your account is configured to access to multiple directories, make sure you have selected the right directory for the organization you want the application to be registered by clicking on your account name in the top right in the Azure Portal, and then verifying the selected directory as indicated:</span><span class="sxs-lookup"><span data-stu-id="9388d-209">If your account is configured to access to multiple directories, make sure you have selected the right directory for the organization you want the application to be registered by clicking on your account name in the top right in the Azure Portal, and then verifying the selected directory as indicated:</span></span><br/><span data-ttu-id="9388d-210">![Selecting the right directory](./media/quickstart-v1-aspnet-webapp/tenantselector.png)</span><span class="sxs-lookup"><span data-stu-id="9388d-210">![Selecting the right directory](./media/quickstart-v1-aspnet-webapp/tenantselector.png)</span></span>

## <a name="configure-sign-in-options"></a><span data-ttu-id="9388d-211">Configure sign-in options</span><span class="sxs-lookup"><span data-stu-id="9388d-211">Configure sign-in options</span></span>

<span data-ttu-id="9388d-212">You can configure your application to allow only users that belong to one organization's Azure Active Directory instance to sign-in, or accept sign-ins from users that belong to any organization.</span><span class="sxs-lookup"><span data-stu-id="9388d-212">You can configure your application to allow only users that belong to one organization's Azure Active Directory instance to sign-in, or accept sign-ins from users that belong to any organization.</span></span> <span data-ttu-id="9388d-213">Please follow the instructions of one of following choices:</span><span class="sxs-lookup"><span data-stu-id="9388d-213">Please follow the instructions of one of following choices:</span></span>

### <a name="configure-your-application-to-allow-sign-ins-of-work-and-school-accounts-from-any-company-or-organization-multi-tenant"></a><span data-ttu-id="9388d-214">Configure your application to allow sign ins of work and school accounts from any company or organization (multi-tenant)</span><span class="sxs-lookup"><span data-stu-id="9388d-214">Configure your application to allow sign ins of work and school accounts from any company or organization (multi-tenant)</span></span>

<span data-ttu-id="9388d-215">Follow the following steps if you want to accept sign ins of work and school accounts from any company or organization that has integrated with Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9388d-215">Follow the following steps if you want to accept sign ins of work and school accounts from any company or organization that has integrated with Azure Active Directory.</span></span> <span data-ttu-id="9388d-216">This is a common scenario for *SaaS applications*:</span><span class="sxs-lookup"><span data-stu-id="9388d-216">This is a common scenario for *SaaS applications*:</span></span>

1. <span data-ttu-id="9388d-217">Go back to [Microsoft Azure Portal - App registrations](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) and locate the application you just registered</span><span class="sxs-lookup"><span data-stu-id="9388d-217">Go back to [Microsoft Azure Portal - App registrations](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps) and locate the application you just registered</span></span>
2. <span data-ttu-id="9388d-218">Under `All Settings` select `Properties`</span><span class="sxs-lookup"><span data-stu-id="9388d-218">Under `All Settings` select `Properties`</span></span>
3. <span data-ttu-id="9388d-219">Change `Multi-tenanted` property to `Yes` and click `Save`</span><span class="sxs-lookup"><span data-stu-id="9388d-219">Change `Multi-tenanted` property to `Yes` and click `Save`</span></span>

<span data-ttu-id="9388d-220">For more information about this setting and the concept of multi-tenant applications, see [this article](howto-convert-app-to-be-multi-tenant.md "Multi-tenant overview").</span><span class="sxs-lookup"><span data-stu-id="9388d-220">For more information about this setting and the concept of multi-tenant applications, see [this article](howto-convert-app-to-be-multi-tenant.md "Multi-tenant overview").</span></span>

### <a name="restrict-users-from-only-one-organizations-active-directory-instance-to-sign-in-to-your-application-single-tenant"></a><span data-ttu-id="9388d-221">Restrict users from only one organization's Active Directory instance to sign in to your application (single-tenant)</span><span class="sxs-lookup"><span data-stu-id="9388d-221">Restrict users from only one organization's Active Directory instance to sign in to your application (single-tenant)</span></span>

<span data-ttu-id="9388d-222">This option is a common scenario for *LOB applications*: If you want your application to accept sign-ins only from accounts that belong to a specific Azure Active Directory instance (including *guest accounts* of that instance), replace the `Tenant` parameter in *web.config* from `Common` with the tenant name of the organization – example, *contoso.onmicrosoft.com*.</span><span class="sxs-lookup"><span data-stu-id="9388d-222">This option is a common scenario for *LOB applications*: If you want your application to accept sign-ins only from accounts that belong to a specific Azure Active Directory instance (including *guest accounts* of that instance), replace the `Tenant` parameter in *web.config* from `Common` with the tenant name of the organization – example, *contoso.onmicrosoft.com*.</span></span> <span data-ttu-id="9388d-223">After that, change the `ValidateIssuer` argument in your [*OWIN Startup class*](#configure-the-authentication-pipeline) to `true`.</span><span class="sxs-lookup"><span data-stu-id="9388d-223">After that, change the `ValidateIssuer` argument in your [*OWIN Startup class*](#configure-the-authentication-pipeline) to `true`.</span></span>

<span data-ttu-id="9388d-224">To allow users from only a list of specific organizations, set `ValidateIssuer` to true and use the `ValidIssuers` parameter to specify a list of organizations.</span><span class="sxs-lookup"><span data-stu-id="9388d-224">To allow users from only a list of specific organizations, set `ValidateIssuer` to true and use the `ValidIssuers` parameter to specify a list of organizations.</span></span>

<span data-ttu-id="9388d-225">Another option is to implement a custom method to validate the issuers using *IssuerValidator* parameter.</span><span class="sxs-lookup"><span data-stu-id="9388d-225">Another option is to implement a custom method to validate the issuers using *IssuerValidator* parameter.</span></span> <span data-ttu-id="9388d-226">For more information about `TokenValidationParameters`, please see [this MSDN article](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article").</span><span class="sxs-lookup"><span data-stu-id="9388d-226">For more information about `TokenValidationParameters`, please see [this MSDN article](https://msdn.microsoft.com/library/system.identitymodel.tokens.tokenvalidationparameters.aspx "TokenValidationParameters MSDN article").</span></span>

<!--end-configure-->

<!--start-configure-arp-->
<!--
## Configure your ASP.NET Web App with the application's registration information

In this step, you will configure your project to use SSL, and then use the SSL URL to configure your application’s registration information. After this, add the application’ registration information to your solution via *web.config*.

1.  In Solution Explorer, select the project and look at the `Properties` window (if you don’t see a Properties window, press F4)
2.  Change `SSL Enabled` to `True`
3.  Copy the value from `SSL URL` above and paste it in the `Redirect URL` field on the top of this page, then click *Update*:<br/><br/>![Project properties](./media/quickstart-v1-aspnet-webapp/vsprojectproperties.png)<br />
4.  Add the following in `web.config` file located in root’s folder, under section `configuration\appSettings`:

```xml
<add key="ClientId" value="[Enter the application Id here]" />
<add key="RedirectUri" value="[Enter the Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}" /> 
```
-->
<!--end-configure-arp-->
<!--start-test-->
## <a name="test-your-code"></a><span data-ttu-id="9388d-227">Test your code</span><span class="sxs-lookup"><span data-stu-id="9388d-227">Test your code</span></span>

<span data-ttu-id="9388d-228">Press `F5` to run your project in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9388d-228">Press `F5` to run your project in Visual Studio.</span></span> <span data-ttu-id="9388d-229">The browser opens and directs you to *http://localhost:{port}* where you see the *Sign in with Microsoft* button.</span><span class="sxs-lookup"><span data-stu-id="9388d-229">The browser opens and directs you to *http://localhost:{port}* where you see the *Sign in with Microsoft* button.</span></span> <span data-ttu-id="9388d-230">Go ahead and click it to sign in.</span><span class="sxs-lookup"><span data-stu-id="9388d-230">Go ahead and click it to sign in.</span></span>

<span data-ttu-id="9388d-231">When you're ready to test, use a work account (Azure Active Directory) to sign in.</span><span class="sxs-lookup"><span data-stu-id="9388d-231">When you're ready to test, use a work account (Azure Active Directory) to sign in.</span></span> 

![Sign in with Microsoft browser window](./media/quickstart-v1-aspnet-webapp/aspnetbrowsersignin.png)

![Sign in with Microsoft browser window](./media/quickstart-v1-aspnet-webapp/aspnetbrowsersignin2.png)

#### <a name="expected-results"></a><span data-ttu-id="9388d-234">Expected results</span><span class="sxs-lookup"><span data-stu-id="9388d-234">Expected results</span></span>
<span data-ttu-id="9388d-235">After sign-in, the user is redirected to the home page of your web site, which is the HTTPS URL specified in your application's registration information in the Microsoft Application Registration Portal.</span><span class="sxs-lookup"><span data-stu-id="9388d-235">After sign-in, the user is redirected to the home page of your web site, which is the HTTPS URL specified in your application's registration information in the Microsoft Application Registration Portal.</span></span> <span data-ttu-id="9388d-236">This page now shows *Hello {User}* and a link to sign out, and a link to see the user’s claims – which is a link to the Authorize controller created earlier.</span><span class="sxs-lookup"><span data-stu-id="9388d-236">This page now shows *Hello {User}* and a link to sign out, and a link to see the user’s claims – which is a link to the Authorize controller created earlier.</span></span>

### <a name="see-users-claims"></a><span data-ttu-id="9388d-237">See user's claims</span><span class="sxs-lookup"><span data-stu-id="9388d-237">See user's claims</span></span>
<span data-ttu-id="9388d-238">Select the hyperlink to see the user's claims.</span><span class="sxs-lookup"><span data-stu-id="9388d-238">Select the hyperlink to see the user's claims.</span></span> <span data-ttu-id="9388d-239">This action leads you to the controller and view that is only available to users that are authenticated.</span><span class="sxs-lookup"><span data-stu-id="9388d-239">This action leads you to the controller and view that is only available to users that are authenticated.</span></span>

#### <a name="expected-results"></a><span data-ttu-id="9388d-240">Expected results</span><span class="sxs-lookup"><span data-stu-id="9388d-240">Expected results</span></span>
 <span data-ttu-id="9388d-241">You should see a table containing the basic properties of the logged user:</span><span class="sxs-lookup"><span data-stu-id="9388d-241">You should see a table containing the basic properties of the logged user:</span></span>

| <span data-ttu-id="9388d-242">Property</span><span class="sxs-lookup"><span data-stu-id="9388d-242">Property</span></span> | <span data-ttu-id="9388d-243">Value</span><span class="sxs-lookup"><span data-stu-id="9388d-243">Value</span></span> | <span data-ttu-id="9388d-244">Description</span><span class="sxs-lookup"><span data-stu-id="9388d-244">Description</span></span>|
|---|---|---|
| <span data-ttu-id="9388d-245">Name</span><span class="sxs-lookup"><span data-stu-id="9388d-245">Name</span></span> | <span data-ttu-id="9388d-246">{User Full Name}</span><span class="sxs-lookup"><span data-stu-id="9388d-246">{User Full Name}</span></span> | <span data-ttu-id="9388d-247">The user’s first and last name</span><span class="sxs-lookup"><span data-stu-id="9388d-247">The user’s first and last name</span></span>
|<span data-ttu-id="9388d-248">Username</span><span class="sxs-lookup"><span data-stu-id="9388d-248">Username</span></span> | <span>user@domain.com</span>| <span data-ttu-id="9388d-249">The username used to identify the logged user</span><span class="sxs-lookup"><span data-stu-id="9388d-249">The username used to identify the logged user</span></span>
| <span data-ttu-id="9388d-250">Subject</span><span class="sxs-lookup"><span data-stu-id="9388d-250">Subject</span></span>| <span data-ttu-id="9388d-251">{Subject}</span><span class="sxs-lookup"><span data-stu-id="9388d-251">{Subject}</span></span>|<span data-ttu-id="9388d-252">A string to uniquely identify the user logon across the web</span><span class="sxs-lookup"><span data-stu-id="9388d-252">A string to uniquely identify the user logon across the web</span></span>|
| <span data-ttu-id="9388d-253">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="9388d-253">Tenant ID</span></span>| <span data-ttu-id="9388d-254">{Guid}</span><span class="sxs-lookup"><span data-stu-id="9388d-254">{Guid}</span></span>| <span data-ttu-id="9388d-255">A *guid* to uniquely represent the user’s Azure Active Directory organization.</span><span class="sxs-lookup"><span data-stu-id="9388d-255">A *guid* to uniquely represent the user’s Azure Active Directory organization.</span></span>|

<span data-ttu-id="9388d-256">In addition, you see a table including all user claims included in authentication request.</span><span class="sxs-lookup"><span data-stu-id="9388d-256">In addition, you see a table including all user claims included in authentication request.</span></span> <span data-ttu-id="9388d-257">For a list of all claims in an ID Token and their explanation, see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in ID Token").</span><span class="sxs-lookup"><span data-stu-id="9388d-257">For a list of all claims in an ID Token and their explanation, see this [article](https://docs.microsoft.com/azure/active-directory/develop/active-directory-token-and-claims "List of Claims in ID Token").</span></span>


### <a name="test-accessing-a-method-that-has-an-authorize-attribute-optional"></a><span data-ttu-id="9388d-258">Test accessing a method that has an *[Authorize]* attribute (Optional)</span><span class="sxs-lookup"><span data-stu-id="9388d-258">Test accessing a method that has an *[Authorize]* attribute (Optional)</span></span>
<span data-ttu-id="9388d-259">In this step, you test accessing the Claims controller as an anonymous user:</span><span class="sxs-lookup"><span data-stu-id="9388d-259">In this step, you test accessing the Claims controller as an anonymous user:</span></span><br/>
<span data-ttu-id="9388d-260">Select the link to sign-out the user and complete the sign-out process.</span><span class="sxs-lookup"><span data-stu-id="9388d-260">Select the link to sign-out the user and complete the sign-out process.</span></span><br/>
<span data-ttu-id="9388d-261">Now in your browser, type http://localhost:{port}/claims to access your controller that is protected with the `[Authorize]` attribute</span><span class="sxs-lookup"><span data-stu-id="9388d-261">Now in your browser, type http://localhost:{port}/claims to access your controller that is protected with the `[Authorize]` attribute</span></span>

#### <a name="expected-results"></a><span data-ttu-id="9388d-262">Expected results</span><span class="sxs-lookup"><span data-stu-id="9388d-262">Expected results</span></span>
<span data-ttu-id="9388d-263">You should receive the prompt requiring you to authenticate to see the view.</span><span class="sxs-lookup"><span data-stu-id="9388d-263">You should receive the prompt requiring you to authenticate to see the view.</span></span>

## <a name="additional-information"></a><span data-ttu-id="9388d-264">Additional information</span><span class="sxs-lookup"><span data-stu-id="9388d-264">Additional information</span></span>

<!--start-collapse-->
### <a name="protect-your-entire-web-site"></a><span data-ttu-id="9388d-265">Protect your entire web site</span><span class="sxs-lookup"><span data-stu-id="9388d-265">Protect your entire web site</span></span>
<span data-ttu-id="9388d-266">To protect your entire web site, add the `AuthorizeAttribute` to `GlobalFilters` in `Global.asax` `Application_Start` method:</span><span class="sxs-lookup"><span data-stu-id="9388d-266">To protect your entire web site, add the `AuthorizeAttribute` to `GlobalFilters` in `Global.asax` `Application_Start` method:</span></span>

```csharp
GlobalFilters.Filters.Add(new AuthorizeAttribute());
```
<!--end-collapse-->

<div></div>
<br/>

<!--end-test-->