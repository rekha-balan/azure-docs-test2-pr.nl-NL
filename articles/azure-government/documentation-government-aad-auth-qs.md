---
title: Azure Government Integrate Azure AD Authentication | Microsoft Docs
description: Integrating Azure AD Authentication on Azure Government Quickstart
services: azure-government
cloud: gov
documentationcenter: ''
author: yujhongmicrosoft
manager: zakramer
ms.assetid: 47e5e535-baa0-457e-8c41-f9fd65478b38
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 11/2/2017
ms.author: yujhongmicrosoft
ms.openlocfilehash: e51e94324c0157449796d75127954042680af526
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869528"
---
# <a name="integrate-azure-ad-authentication-with-web-apps-on-azure-government"></a><span data-ttu-id="d6f10-103">Integrate Azure AD Authentication with Web Apps on Azure Government</span><span class="sxs-lookup"><span data-stu-id="d6f10-103">Integrate Azure AD Authentication with Web Apps on Azure Government</span></span>
<span data-ttu-id="d6f10-104">The following quickstart helps you get started integrating Azure AD Authentication with applications on Azure Government.</span><span class="sxs-lookup"><span data-stu-id="d6f10-104">The following quickstart helps you get started integrating Azure AD Authentication with applications on Azure Government.</span></span> <span data-ttu-id="d6f10-105">Azure Active Directory (Azure AD) Authentication on Azure Government is similar to the Azure commercial platform, with a [few exceptions](documentation-government-services-securityandidentity.md).</span><span class="sxs-lookup"><span data-stu-id="d6f10-105">Azure Active Directory (Azure AD) Authentication on Azure Government is similar to the Azure commercial platform, with a [few exceptions](documentation-government-services-securityandidentity.md).</span></span>

<span data-ttu-id="d6f10-106">Learn more about [Azure Active Directory Authentication Scenarios](../active-directory/develop/authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="d6f10-106">Learn more about [Azure Active Directory Authentication Scenarios](../active-directory/develop/authentication-scenarios.md).</span></span> 

## <a name="integrate-azure-ad-login-into-a-web-application-using-openid-connect"></a><span data-ttu-id="d6f10-107">Integrate Azure AD login into a web application using OpenID Connect</span><span class="sxs-lookup"><span data-stu-id="d6f10-107">Integrate Azure AD login into a web application using OpenID Connect</span></span>
<span data-ttu-id="d6f10-108">This section shows how to integrate Azure AD using the OpenID Connect protocol for signing in users into a web app.</span><span class="sxs-lookup"><span data-stu-id="d6f10-108">This section shows how to integrate Azure AD using the OpenID Connect protocol for signing in users into a web app.</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="d6f10-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d6f10-109">Prerequisites</span></span> 
- <span data-ttu-id="d6f10-110">An Azure AD tenant in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="d6f10-110">An Azure AD tenant in Azure Government.</span></span> <span data-ttu-id="d6f10-111">You must have an [Azure Government subscription](https://azure.microsoft.com/overview/clouds/government/request/) in order to have an Azure AD tenant in Azure Government.</span><span class="sxs-lookup"><span data-stu-id="d6f10-111">You must have an [Azure Government subscription](https://azure.microsoft.com/overview/clouds/government/request/) in order to have an Azure AD tenant in Azure Government.</span></span> <span data-ttu-id="d6f10-112">For more information on how to get an Azure AD tenant, see [How to get an Azure AD tenant](../active-directory/develop/quickstart-create-new-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="d6f10-112">For more information on how to get an Azure AD tenant, see [How to get an Azure AD tenant](../active-directory/develop/quickstart-create-new-tenant.md)</span></span> 
- <span data-ttu-id="d6f10-113">A user account in your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="d6f10-113">A user account in your Azure AD tenant.</span></span> <span data-ttu-id="d6f10-114">This sample does not work with a Microsoft account, so if you signed in to the Azure Government portal with a Microsoft account and have never created a user account in your directory before, you need to do that now.</span><span class="sxs-lookup"><span data-stu-id="d6f10-114">This sample does not work with a Microsoft account, so if you signed in to the Azure Government portal with a Microsoft account and have never created a user account in your directory before, you need to do that now.</span></span>
- <span data-ttu-id="d6f10-115">Have an [ASP.NET Core application deployed and running in Azure Government](documentation-government-howto-deploy-webandmobile.md)</span><span class="sxs-lookup"><span data-stu-id="d6f10-115">Have an [ASP.NET Core application deployed and running in Azure Government](documentation-government-howto-deploy-webandmobile.md)</span></span>

### <a name="step-1-register-your-web-application-with-your-azure-ad-tenant"></a><span data-ttu-id="d6f10-116">Step 1: Register your web application with your Azure AD Tenant</span><span class="sxs-lookup"><span data-stu-id="d6f10-116">Step 1: Register your web application with your Azure AD Tenant</span></span> 

1. <span data-ttu-id="d6f10-117">Sign in to the [Azure Government portal](https://portal.azure.us).</span><span class="sxs-lookup"><span data-stu-id="d6f10-117">Sign in to the [Azure Government portal](https://portal.azure.us).</span></span>
2. <span data-ttu-id="d6f10-118">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span><span class="sxs-lookup"><span data-stu-id="d6f10-118">On the top bar, click on your account and under the **Directory** list, choose the Active Directory tenant where you wish to register your application.</span></span>
3. <span data-ttu-id="d6f10-119">Click on **All Services** in the left-hand nav, and choose **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="d6f10-119">Click on **All Services** in the left-hand nav, and choose **Azure Active Directory**.</span></span>
4. <span data-ttu-id="d6f10-120">Click on **App registrations** and choose **Add**.</span><span class="sxs-lookup"><span data-stu-id="d6f10-120">Click on **App registrations** and choose **Add**.</span></span>
5. <span data-ttu-id="d6f10-121">Enter the name for your application, and select 'Web Application and/or Web API' as the Application Type.</span><span class="sxs-lookup"><span data-stu-id="d6f10-121">Enter the name for your application, and select 'Web Application and/or Web API' as the Application Type.</span></span> <span data-ttu-id="d6f10-122">For the sign-on URL, enter the base URL for your application, which is your Azure App URL + "/signin-oidc."</span><span class="sxs-lookup"><span data-stu-id="d6f10-122">For the sign-on URL, enter the base URL for your application, which is your Azure App URL + "/signin-oidc."</span></span> 

    >[!Note] 
    > <span data-ttu-id="d6f10-123">If you have not deployed your application and want to run it locally, your App URL would be your local host address.</span><span class="sxs-lookup"><span data-stu-id="d6f10-123">If you have not deployed your application and want to run it locally, your App URL would be your local host address.</span></span>
    >
    >

    <span data-ttu-id="d6f10-124">Click on **Create** to create the application.</span><span class="sxs-lookup"><span data-stu-id="d6f10-124">Click on **Create** to create the application.</span></span>
6. <span data-ttu-id="d6f10-125">While still in the Azure portal, choose your application, click on **Settings**, and choose **Properties**.</span><span class="sxs-lookup"><span data-stu-id="d6f10-125">While still in the Azure portal, choose your application, click on **Settings**, and choose **Properties**.</span></span>
7. <span data-ttu-id="d6f10-126">Find the Application ID value and copy it to the clipboard.</span><span class="sxs-lookup"><span data-stu-id="d6f10-126">Find the Application ID value and copy it to the clipboard.</span></span>
8. <span data-ttu-id="d6f10-127">For the App ID URI, enter https://\<your_tenant_name\>/\<name_of_your_app\>, replacing \<your_tenant_name\> with the name of your Azure AD tenant and \<name_of_your_app\> with the name of your application.</span><span class="sxs-lookup"><span data-stu-id="d6f10-127">For the App ID URI, enter https://\<your_tenant_name\>/\<name_of_your_app\>, replacing \<your_tenant_name\> with the name of your Azure AD tenant and \<name_of_your_app\> with the name of your application.</span></span>

### <a name="step-2--configure-your-app-to-use-your-azure-ad-tenant"></a><span data-ttu-id="d6f10-128">Step 2:  Configure your app to use your Azure AD tenant</span><span class="sxs-lookup"><span data-stu-id="d6f10-128">Step 2:  Configure your app to use your Azure AD tenant</span></span>
#### <a name="azure-government-variations"></a><span data-ttu-id="d6f10-129">Azure Government Variations</span><span class="sxs-lookup"><span data-stu-id="d6f10-129">Azure Government Variations</span></span>
<span data-ttu-id="d6f10-130">The only variation when setting up Azure AD Authorization on the Azure Government cloud is in the Azure AD Instance:</span><span class="sxs-lookup"><span data-stu-id="d6f10-130">The only variation when setting up Azure AD Authorization on the Azure Government cloud is in the Azure AD Instance:</span></span>
 - <span data-ttu-id="d6f10-131">"https://login.microsoftonline.us"</span><span class="sxs-lookup"><span data-stu-id="d6f10-131">"https://login.microsoftonline.us"</span></span>

#### <a name="configure-the-inventoryapp-project"></a><span data-ttu-id="d6f10-132">Configure the InventoryApp project</span><span class="sxs-lookup"><span data-stu-id="d6f10-132">Configure the InventoryApp project</span></span>
1. <span data-ttu-id="d6f10-133">Open your application in Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="d6f10-133">Open your application in Visual Studio 2017.</span></span>
2. <span data-ttu-id="d6f10-134">Open the `appsettings.json` file.</span><span class="sxs-lookup"><span data-stu-id="d6f10-134">Open the `appsettings.json` file.</span></span>
3. <span data-ttu-id="d6f10-135">Add an `Authentication` section and fill out the properties with your Azure AD tenant information.</span><span class="sxs-lookup"><span data-stu-id="d6f10-135">Add an `Authentication` section and fill out the properties with your Azure AD tenant information.</span></span>
    
    ```cs
    //ClientId: Azure AD->  App registrations -> Application ID
    //Domain: <tenantname>.onmicrosoft.com
    //TenantId: Azure AD -> Properties -> Directory ID

    "Authentication": {
        "AzureAd": {

        "Azure ADInstance": "https://login.microsoftonline.us/",
        "CallbackPath": "/signin-oidc",
        "ClientId": "<clientid>",
        "Domain": "<domainname>",
        "TenantId": "<tenantid>"
        }
    }
    ```
4. <span data-ttu-id="d6f10-136">Fill out the `ClientId` property with the Client ID for your app from the Azure Government portal.</span><span class="sxs-lookup"><span data-stu-id="d6f10-136">Fill out the `ClientId` property with the Client ID for your app from the Azure Government portal.</span></span> <span data-ttu-id="d6f10-137">You can find the Client ID by navigating to Azure AD -> App Registrations -> Your Application -> Application ID.</span><span class="sxs-lookup"><span data-stu-id="d6f10-137">You can find the Client ID by navigating to Azure AD -> App Registrations -> Your Application -> Application ID.</span></span> 
5. <span data-ttu-id="d6f10-138">Fill out the `TenantId` property with the Tenant ID for your app from the Azure Government portal.</span><span class="sxs-lookup"><span data-stu-id="d6f10-138">Fill out the `TenantId` property with the Tenant ID for your app from the Azure Government portal.</span></span> <span data-ttu-id="d6f10-139">You can find the Tenant ID by navigating to Azure AD -> Properties -> Directory ID.</span><span class="sxs-lookup"><span data-stu-id="d6f10-139">You can find the Tenant ID by navigating to Azure AD -> Properties -> Directory ID.</span></span> 
6. <span data-ttu-id="d6f10-140">Fill out the `Domain` property with "<tenantname>.onmicrosoft.com."</span><span class="sxs-lookup"><span data-stu-id="d6f10-140">Fill out the `Domain` property with "<tenantname>.onmicrosoft.com."</span></span>
7. <span data-ttu-id="d6f10-141">Open the `startup.cs` file.</span><span class="sxs-lookup"><span data-stu-id="d6f10-141">Open the `startup.cs` file.</span></span>
8. <span data-ttu-id="d6f10-142">In your `ConfigureServices` method, add the following code:</span><span class="sxs-lookup"><span data-stu-id="d6f10-142">In your `ConfigureServices` method, add the following code:</span></span>

    ```cs
        public void ConfigureServices(IServiceCollection services)
        {      
            //Add Azure AD authentication
            services.AddAuthentication(options => {
                options.DefaultScheme = CookieAuthenticationDefaults.AuthenticationScheme;
                options.DefaultChallengeScheme = OpenIdConnectDefaults.AuthenticationScheme;
            })
            .AddCookie()
            .AddOpenIdConnect(options => {
                options.Authority = Configuration["Authentication:AzureAd:Azure ADInstance"] + Configuration["Authentication:AzureAd:TenantId"];
                options.ClientId = Configuration["Authentication:AzureAd:ClientId"];
                options.CallbackPath = Configuration["Authentication:AzureAd:CallbackPath"];
            });
        
        }
    ```

    <span data-ttu-id="d6f10-143">In the same file, add this one line of code to the `Configure` method:</span><span class="sxs-lookup"><span data-stu-id="d6f10-143">In the same file, add this one line of code to the `Configure` method:</span></span>

    ```cs
    app.UseAuthentication();
    ```
9. <span data-ttu-id="d6f10-144">Navigate to your **Home** controller or whichever controller file is your home page, **where you want your users to log in**.</span><span class="sxs-lookup"><span data-stu-id="d6f10-144">Navigate to your **Home** controller or whichever controller file is your home page, **where you want your users to log in**.</span></span> <span data-ttu-id="d6f10-145">Add the `[Authorize]` tag before the class definition.</span><span class="sxs-lookup"><span data-stu-id="d6f10-145">Add the `[Authorize]` tag before the class definition.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d6f10-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="d6f10-146">Next steps</span></span>

* <span data-ttu-id="d6f10-147">Navigate to the [Azure Government PaaS Sample](https://github.com/Azure-Samples/gov-paas-sample) to see Azure AD Authentication as well as other services being integrated in an Application running on Azure Government.</span><span class="sxs-lookup"><span data-stu-id="d6f10-147">Navigate to the [Azure Government PaaS Sample](https://github.com/Azure-Samples/gov-paas-sample) to see Azure AD Authentication as well as other services being integrated in an Application running on Azure Government.</span></span> 
* <span data-ttu-id="d6f10-148">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span><span class="sxs-lookup"><span data-stu-id="d6f10-148">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span></span>
* <span data-ttu-id="d6f10-149">Get help on Stack Overflow by using the "[azure-gov](https://stackoverflow.com/questions/tagged/azure-gov)" tag</span><span class="sxs-lookup"><span data-stu-id="d6f10-149">Get help on Stack Overflow by using the "[azure-gov](https://stackoverflow.com/questions/tagged/azure-gov)" tag</span></span>
* <span data-ttu-id="d6f10-150">Give feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span><span class="sxs-lookup"><span data-stu-id="d6f10-150">Give feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span></span>
