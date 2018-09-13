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
# <a name="what-happened-to-my-mvc-project-visual-studio-azure-active-directory-connected-service"></a>What happened to my MVC project (Visual Studio Azure Active Directory connected service)?
> [!div class="op_single_selector"]
> * [Getting Started](vs-active-directory-dotnet-getting-started.md)
> * [What Happened](vs-active-directory-dotnet-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>References have been added
### <a name="nuget-package-references"></a>NuGet package references
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel.Tokens.Jwt**

### <a name="net-references"></a>.NET references
* **Microsoft.IdentityModel.Protocol.Extensions**
* **Microsoft.Owin**
* **Microsoft.Owin.Host.SystemWeb**
* **Microsoft.Owin.Security**
* **Microsoft.Owin.Security.Cookies**
* **Microsoft.Owin.Security.OpenIdConnect**
* **Owin**
* **System.IdentityModel**
* **System.IdentityModel.Tokens.Jwt**
* **System.Runtime.Serialization**

## <a name="code-has-been-added"></a>Code has been added
### <a name="code-files-were-added-to-your-project"></a>Code files were added to your project
An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication. Also, a controller class, Controllers/AccountController.cs was added which contains **SignIn()** and **SignOut()** methods. Finally, a partial view, **Views/Shared/_LoginPartial.cshtml** was added containing an action link for SignIn/SignOut.

### <a name="startup-code-was-added-to-your-project"></a>Startup code was added to your project
If you already had a Startup class in your project, the **Configuration** method was updated to include a call to **ConfigureAuth(app)**. Otherwise, a Startup class was added to your project.

### <a name="your-appconfig-or-webconfig-has-new-configuration-values"></a>Your app.config or web.config has new configuration values
The following configuration entries have been added.

    <appSettings>
        <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
        <add key="ida:AADInstance" value="https://login.microsoftonline.com/" />
        <add key="ida:Domain" value="The selected Azure AD Domain" />
        <add key="ida:TenantId" value="The Id of your selected Azure AD Tenant" />
        <add key="ida:PostLogoutRedirectUri" value="Your project start page" />
    </appSettings>

### <a name="an-azure-active-directory-ad-app-was-created"></a>An Azure Active Directory (AD) App was created
An Azure AD Application was created in the directory that you selected in the wizard.

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a>If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?
NuGet package references were removed, and files were removed and backed up. Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.

### <a name="nuget-package-references-removed-for-those-present"></a>NuGet package references removed (for those present)
* **Microsoft.AspNet.Identity.Core**
* **Microsoft.AspNet.Identity.EntityFramework**
* **Microsoft.AspNet.Identity.Owin**

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Code files backed up and removed (for those present)
Each of following files was backed up and removed from the project. Backup files are located in a 'Backup' folder at the root of the project's directory.

* **App_Start\IdentityConfig.cs**
* **Controllers\ManageController.cs**
* **Models\IdentityModels.cs**
* **Models\ManageViewModels.cs**

### <a name="code-files-backed-up-for-those-present"></a>Code files backed up (for those present)
Each of following files was backed up before being replaced. Backup files are located in a 'Backup' folder at the root of the project's directory.

* **Startup.cs**
* **App_Start\Startup.Auth.cs**
* **Controllers\AccountController.cs**
* **Views\Shared\_LoginPartial.cshtml**

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a>If I checked *Read directory data*, what additional changes were made to my project?
Additional references have been added.

### <a name="additional-nuget-package-references"></a>Additional NuGet package references
* **EntityFramework**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **System.Spatial**

### <a name="additional-net-references"></a>Additional .NET references
* **EntityFramework**
* **EntityFramework.SqlServer**
* **Microsoft.Azure.ActiveDirectory.GraphClient**
* **Microsoft.Data.Edm**
* **Microsoft.Data.OData**
* **Microsoft.Data.Services.Client**
* **Microsoft.IdentityModel.Clients.ActiveDirectory**
* **Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms**
* **System.Spatial**

### <a name="additional-code-files-were-added-to-your-project"></a>Additional Code files were added to your project
Two files were added to support token caching: **Models\ADALTokenCache.cs** and **Models\ApplicationDbContext.cs**.  An additional controller and view were added to illustrate accessing user profile information using Azure graph APIs.  These files are **Controllers\UserProfileController.cs** and **Views\UserProfile\Index.cshtml**.

### <a name="additional-startup-code-was-added-to-your-project"></a>Additional Startup code was added to your project
In the **startup.auth.cs** file, a new **OpenIdConnectAuthenticationNotifications** object was added to the **Notifications** member of the **OpenIdConnectAuthenticationOptions**.  This is to enable receiving the OAuth code and exchanging it for an access token.

### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a>Additional changes were made to your app.config or web.config
The following additional configuration entries have been added.

    <appSettings>
        <add key="ida:ClientSecret" value="Your Azure AD App's new client secret" />
    </appSettings>

The following configuration sections and connection string have been added.

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


### <a name="your-azure-active-directory-app-was-updated"></a>Your Azure Active Directory App was updated
Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:ClientSecret* in the **web.config** file.

## <a name="next-steps"></a>Next steps
- [Learn more about Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

