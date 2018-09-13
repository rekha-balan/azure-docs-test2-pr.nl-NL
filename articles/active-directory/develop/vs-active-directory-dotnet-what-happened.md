---
title: Changes made to a MVC project when you connect to Azure AD | Microsoft Docs
description: Describes what happens to your MVC project when you connect to Azure AD by using Visual Studio connected services
services: active-directory
documentationcenter: na
author: TomArcher
manager: douge
editor: ''
ms.assetid: 8b24adde-547e-4ffe-824a-2029ba210216
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: tarcher
ms.openlocfilehash: 72cd94ba16cb4fe234c898b093c7de6a08f71239
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44670279"
---
# <a name="what-happened-to-my-mvc-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="e4d43-103">What happened to my MVC project (Visual Studio Azure Active Directory connected service)?</span><span class="sxs-lookup"><span data-stu-id="e4d43-103">What happened to my MVC project (Visual Studio Azure Active Directory connected service)?</span></span>
> [!div class="op_single_selector"]
> * [Getting Started](vs-active-directory-dotnet-getting-started.md)
> * [What Happened](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="e4d43-106">References have been added</span><span class="sxs-lookup"><span data-stu-id="e4d43-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="e4d43-107">NuGet package references</span><span class="sxs-lookup"><span data-stu-id="e4d43-107">NuGet package references</span></span>
* <span data-ttu-id="e4d43-108">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="e4d43-108">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="e4d43-109">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="e4d43-109">**Microsoft.Owin**</span></span>
* <span data-ttu-id="e4d43-110">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="e4d43-110">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="e4d43-111">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="e4d43-111">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="e4d43-112">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="e4d43-112">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="e4d43-113">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="e4d43-113">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="e4d43-114">**Owin**</span><span class="sxs-lookup"><span data-stu-id="e4d43-114">**Owin**</span></span>
* <span data-ttu-id="e4d43-115">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="e4d43-115">**System.IdentityModel.Tokens.Jwt**</span></span>

### <a name="net-references"></a><span data-ttu-id="e4d43-116">.NET references</span><span class="sxs-lookup"><span data-stu-id="e4d43-116">.NET references</span></span>
* <span data-ttu-id="e4d43-117">**Microsoft.IdentityModel.Protocol.Extensions**</span><span class="sxs-lookup"><span data-stu-id="e4d43-117">**Microsoft.IdentityModel.Protocol.Extensions**</span></span>
* <span data-ttu-id="e4d43-118">**Microsoft.Owin**</span><span class="sxs-lookup"><span data-stu-id="e4d43-118">**Microsoft.Owin**</span></span>
* <span data-ttu-id="e4d43-119">**Microsoft.Owin.Host.SystemWeb**</span><span class="sxs-lookup"><span data-stu-id="e4d43-119">**Microsoft.Owin.Host.SystemWeb**</span></span>
* <span data-ttu-id="e4d43-120">**Microsoft.Owin.Security**</span><span class="sxs-lookup"><span data-stu-id="e4d43-120">**Microsoft.Owin.Security**</span></span>
* <span data-ttu-id="e4d43-121">**Microsoft.Owin.Security.Cookies**</span><span class="sxs-lookup"><span data-stu-id="e4d43-121">**Microsoft.Owin.Security.Cookies**</span></span>
* <span data-ttu-id="e4d43-122">**Microsoft.Owin.Security.OpenIdConnect**</span><span class="sxs-lookup"><span data-stu-id="e4d43-122">**Microsoft.Owin.Security.OpenIdConnect**</span></span>
* <span data-ttu-id="e4d43-123">**Owin**</span><span class="sxs-lookup"><span data-stu-id="e4d43-123">**Owin**</span></span>
* <span data-ttu-id="e4d43-124">**System.IdentityModel**</span><span class="sxs-lookup"><span data-stu-id="e4d43-124">**System.IdentityModel**</span></span>
* <span data-ttu-id="e4d43-125">**System.IdentityModel.Tokens.Jwt**</span><span class="sxs-lookup"><span data-stu-id="e4d43-125">**System.IdentityModel.Tokens.Jwt**</span></span>
* <span data-ttu-id="e4d43-126">**System.Runtime.Serialization**</span><span class="sxs-lookup"><span data-stu-id="e4d43-126">**System.Runtime.Serialization**</span></span>

## <a name="code-has-been-added"></a><span data-ttu-id="e4d43-127">Code has been added</span><span class="sxs-lookup"><span data-stu-id="e4d43-127">Code has been added</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="e4d43-128">Code files were added to your project</span><span class="sxs-lookup"><span data-stu-id="e4d43-128">Code files were added to your project</span></span>
<span data-ttu-id="e4d43-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="e4d43-129">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span> <span data-ttu-id="e4d43-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span><span class="sxs-lookup"><span data-stu-id="e4d43-130">Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods.</span></span> <span data-ttu-id="e4d43-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span><span class="sxs-lookup"><span data-stu-id="e4d43-131">Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="e4d43-132">Startup code was added to your project</span><span class="sxs-lookup"><span data-stu-id="e4d43-132">Startup code was added to your project</span></span>
<span data-ttu-id="e4d43-133">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**.</span><span class="sxs-lookup"><span data-stu-id="e4d43-133">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**.</span></span> <span data-ttu-id="e4d43-134">Otherwise, a Startup class was added to your project.</span><span class="sxs-lookup"><span data-stu-id="e4d43-134">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a><span data-ttu-id="e4d43-135">Your app.config or web.config has new configuration values</span><span class="sxs-lookup"><span data-stu-id="e4d43-135">Your app.config or web.config has new configuration values</span></span>
<span data-ttu-id="e4d43-136">The following configuration entries have been added.</span><span class="sxs-lookup"><span data-stu-id="e4d43-136">The following configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="The selected Azure AD Domain" />
        <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a><span data-ttu-id="e4d43-137">An Azure Active Directory (AD) App was created</span><span class="sxs-lookup"><span data-stu-id="e4d43-137">An Azure Active Directory (AD) App was created</span></span>
<span data-ttu-id="e4d43-138">An Azure AD Application was created in the directory that you selected in the wizard.</span><span class="sxs-lookup"><span data-stu-id="e4d43-138">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="e4d43-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span><span class="sxs-lookup"><span data-stu-id="e4d43-139">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="e4d43-140">NuGet package references were removed, and files were removed and backed up.</span><span class="sxs-lookup"><span data-stu-id="e4d43-140">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="e4d43-141">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span><span class="sxs-lookup"><span data-stu-id="e4d43-141">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="e4d43-142">NuGet package references removed (for those present)</span><span class="sxs-lookup"><span data-stu-id="e4d43-142">NuGet package references removed (for those present)</span></span>
* <span data-ttu-id="e4d43-143">**Microsoft.AspNet.Identity.Core**</span><span class="sxs-lookup"><span data-stu-id="e4d43-143">**Microsoft.AspNet.Identity.Core**</span></span>
* <span data-ttu-id="e4d43-144">**Microsoft.AspNet.Identity.EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="e4d43-144">**Microsoft.AspNet.Identity.EntityFramework**</span></span>
* <span data-ttu-id="e4d43-145">**Microsoft.AspNet.Identity.Owin**</span><span class="sxs-lookup"><span data-stu-id="e4d43-145">**Microsoft.AspNet.Identity.Owin**</span></span>

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="e4d43-146">Code files backed up and removed (for those present)</span><span class="sxs-lookup"><span data-stu-id="e4d43-146">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="e4d43-147">Each of following files was backed up and removed from the project.</span><span class="sxs-lookup"><span data-stu-id="e4d43-147">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="e4d43-148">Backup files are located in a 'Backup' folder at the root of the project's directory.</span><span class="sxs-lookup"><span data-stu-id="e4d43-148">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="e4d43-149">**App_Start\IdentityConfig.cs**</span><span class="sxs-lookup"><span data-stu-id="e4d43-149">**App_Start\IdentityConfig.cs**</span></span>
* <span data-ttu-id="e4d43-150">**Controllers\ManageController.cs**</span><span class="sxs-lookup"><span data-stu-id="e4d43-150">**Controllers\ManageController.cs**</span></span>
* <span data-ttu-id="e4d43-151">**Models\IdentityModels.cs**</span><span class="sxs-lookup"><span data-stu-id="e4d43-151">**Models\IdentityModels.cs**</span></span>
* <span data-ttu-id="e4d43-152">**Models\ManageViewModels.cs**</span><span class="sxs-lookup"><span data-stu-id="e4d43-152">**Models\ManageViewModels.cs**</span></span>

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="e4d43-153">Code files backed up (for those present)</span><span class="sxs-lookup"><span data-stu-id="e4d43-153">Code files backed up (for those present)</span></span>
<span data-ttu-id="e4d43-154">Each of following files was backed up before being replaced.</span><span class="sxs-lookup"><span data-stu-id="e4d43-154">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="e4d43-155">Backup files are located in a 'Backup' folder at the root of the project's directory.</span><span class="sxs-lookup"><span data-stu-id="e4d43-155">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* <span data-ttu-id="e4d43-156">**Startup.cs**</span><span class="sxs-lookup"><span data-stu-id="e4d43-156">**Startup.cs**</span></span>
* <span data-ttu-id="e4d43-157">**App_Start\Startup.Auth.cs**</span><span class="sxs-lookup"><span data-stu-id="e4d43-157">**App_Start\Startup.Auth.cs**</span></span>
* <span data-ttu-id="e4d43-158">**Controllers\AccountController.cs**</span><span class="sxs-lookup"><span data-stu-id="e4d43-158">**Controllers\AccountController.cs**</span></span>
* <span data-ttu-id="e4d43-159">**Views\Shared\_LoginPartial.cshtml**</span><span class="sxs-lookup"><span data-stu-id="e4d43-159">**Views\Shared\_LoginPartial.cshtml**</span></span>

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="e4d43-160">If I checked *Read directory data*, what additional changes were made to my project?</span><span class="sxs-lookup"><span data-stu-id="e4d43-160">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
<span data-ttu-id="e4d43-161">Additional references have been added.</span><span class="sxs-lookup"><span data-stu-id="e4d43-161">Additional references have been added.</span></span>

### <a name="additional-nuget-package-references"></a><span data-ttu-id="e4d43-162">Additional NuGet package references</span><span class="sxs-lookup"><span data-stu-id="e4d43-162">Additional NuGet package references</span></span>
* <span data-ttu-id="e4d43-163">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="e4d43-163">**EntityFramework**</span></span>
* <span data-ttu-id="e4d43-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="e4d43-164">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="e4d43-165">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="e4d43-165">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="e4d43-166">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="e4d43-166">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="e4d43-167">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="e4d43-167">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="e4d43-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="e4d43-168">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="e4d43-169">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="e4d43-169">**System.Spatial**</span></span>

### <a name="additional-net-references"></a><span data-ttu-id="e4d43-170">Additional .NET references</span><span class="sxs-lookup"><span data-stu-id="e4d43-170">Additional .NET references</span></span>
* <span data-ttu-id="e4d43-171">**EntityFramework**</span><span class="sxs-lookup"><span data-stu-id="e4d43-171">**EntityFramework**</span></span>
* <span data-ttu-id="e4d43-172">**EntityFramework.SqlServer**</span><span class="sxs-lookup"><span data-stu-id="e4d43-172">**EntityFramework.SqlServer**</span></span>
* <span data-ttu-id="e4d43-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span><span class="sxs-lookup"><span data-stu-id="e4d43-173">**Microsoft.Azure.ActiveDirectory.GraphClient**</span></span>
* <span data-ttu-id="e4d43-174">**Microsoft.Data.Edm**</span><span class="sxs-lookup"><span data-stu-id="e4d43-174">**Microsoft.Data.Edm**</span></span>
* <span data-ttu-id="e4d43-175">**Microsoft.Data.OData**</span><span class="sxs-lookup"><span data-stu-id="e4d43-175">**Microsoft.Data.OData**</span></span>
* <span data-ttu-id="e4d43-176">**Microsoft.Data.Services.Client**</span><span class="sxs-lookup"><span data-stu-id="e4d43-176">**Microsoft.Data.Services.Client**</span></span>
* <span data-ttu-id="e4d43-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span><span class="sxs-lookup"><span data-stu-id="e4d43-177">**Microsoft.IdentityModel.Clients.ActiveDirectory**</span></span>
* <span data-ttu-id="e4d43-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span><span class="sxs-lookup"><span data-stu-id="e4d43-178">**Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**</span></span>
* <span data-ttu-id="e4d43-179">**System.Spatial**</span><span class="sxs-lookup"><span data-stu-id="e4d43-179">**System.Spatial**</span></span>

### <a name="additional-code-files-were-added-to-your-project"></a><span data-ttu-id="e4d43-180">Additional Code files were added to your project</span><span class="sxs-lookup"><span data-stu-id="e4d43-180">Additional Code files were added to your project</span></span>
<span data-ttu-id="e4d43-181">Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span><span class="sxs-lookup"><span data-stu-id="e4d43-181">Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.</span></span>  <span data-ttu-id="e4d43-182">An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.</span><span class="sxs-lookup"><span data-stu-id="e4d43-182">An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.</span></span>  <span data-ttu-id="e4d43-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span><span class="sxs-lookup"><span data-stu-id="e4d43-183">These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.</span></span>

### <a name="additional-startup-code-was-added-to-your-project"></a><span data-ttu-id="e4d43-184">Additional Startup code was added to your project</span><span class="sxs-lookup"><span data-stu-id="e4d43-184">Additional Startup code was added to your project</span></span>
<span data-ttu-id="e4d43-185">In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.</span><span class="sxs-lookup"><span data-stu-id="e4d43-185">In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.</span></span>  <span data-ttu-id="e4d43-186">This is to enable receiving the OAuth code and exchanging it for an access token.</span><span class="sxs-lookup"><span data-stu-id="e4d43-186">This is to enable receiving the OAuth code and exchanging it for an access token.</span></span>

### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="e4d43-187">Additional changes were made to your app.config or web.config</span><span class="sxs-lookup"><span data-stu-id="e4d43-187">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="e4d43-188">The following additional configuration entries have been added.</span><span class="sxs-lookup"><span data-stu-id="e4d43-188">The following additional configuration entries have been added.</span></span>

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

<span data-ttu-id="e4d43-189">The following configuration sections and connection string have been added.</span><span class="sxs-lookup"><span data-stu-id="e4d43-189">The following configuration sections and connection string have been added.</span></span>

    <configSections>
        <!-- For more information on Entity Framework configuration, visit http://go.microsoft.com/fwlink/?LinkID=237468 -->
        <section name="entityFramework" type="System.Data.Entity.Internal.ConfigFile.EntityFrameworkSection, EntityFramework, Version=6.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" requirePermission="false" />
    </configSections>
    <connectionStrings>
        <add name="DefaultConnection" connectionString="Data Source=(localdb)\MSSQLLocalDB;AttachDbFilename=|DataDirectory|\aspnet-[AppName + Generated Id].mdf;Initial Catalog=aspnet-[AppName + Generated Id];Integrated Security=True" providerName="System.Data.SqlClient" />
    </connectionStrings>
    <entityFramework>
        <defaultConnectionFactory type="System.Data.Entity.Infrastructure.LocalDbConnectionFactory, EntityFramework">
          <parameters>
            <parameter value="mssqllocaldb" />
          </parameters>
        </defaultConnectionFactory>
        <providers>
          <provider invariantName="System.Data.SqlClient" type="System.Data.Entity.SqlServer.SqlProviderServices, EntityFramework.SqlServer" />
        </providers>
    </entityFramework>


### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="e4d43-190">Your Azure Active Directory App was updated</span><span class="sxs-lookup"><span data-stu-id="e4d43-190">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="e4d43-191">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.</span><span class="sxs-lookup"><span data-stu-id="e4d43-191">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e4d43-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="e4d43-192">Next steps</span></span>
- [<span data-ttu-id="e4d43-193">Learn more about Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e4d43-193">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

