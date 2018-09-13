---
title: Changes made to a WebApi project when you connect to Azure AD | Microsoft Docs
description: Describes what happens to your WebApi project when you connect to Azure AD by using Visual Studio
services: active-directory
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-what-happened
ms.devlang: na
ms.topic: article
ms.date: 03/01/2017
ms.author: tarcher
ms.openlocfilehash: 8ca3234e54d8736aa187195640a103ac6eb145e7
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661107"
---
# <a name="what-happened-to-my-webapi-project-visual-studio-azure-active-directory-connected-service"></a>What happened to my WebApi project (Visual Studio Azure Active Directory connected service)
> [!div class="op_single_selector"]
> * [Getting Started](vs-active-directory-webapi-getting-started.md)
> * [What Happened](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a>References have been added
### <a name="nuget-package-references"></a>NuGet package references
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a>.NET references
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a>Code changes
### <a name="code-files-were-added-to-your-project"></a>Code files were added to your project
An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.

### <a name="startup-code-was-added-to-your-project"></a>Startup code was added to your project
If you already had a Startup class in your project, the **Configuration** method was updated to include a call to `ConfigureAuth(app)`. Otherwise, a Startup class was added to your project.

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a>Your app.config or web.config file has new configuration values.
The following configuration entries have been added.

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="The App ID Uri from the wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a>An Azure AD App was created
An Azure AD Application was created in the directory that you selected in the wizard.

[Learn more about Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a>If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?
NuGet package references were removed, and files were removed and backed up. Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.

### <a name="nuget-package-references-removed-for-those-present"></a>NuGet package references removed (for those present)
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a>Code files backed up and removed (for those present)
Each of following files was backed up and removed from the project. Backup files are located in a 'Backup' folder at the root of the project's directory.

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a>Code files backed up (for those present)
Each of following files was backed up before being replaced. Backup files are located in a 'Backup' folder at the root of the project's directory.

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a>If I checked *Read directory data*, what additional changes were made to my project?
### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a>Additional changes were made to your app.config or web.config
The following additional configuration entries have been added.

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a>Your Azure Active Directory App was updated
Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:Password* in the `web.config` file.

## <a name="next-steps"></a>Next steps
- [Learn more about Azure Active Directory](https://azure.microsoft.com/services/active-directory/)

