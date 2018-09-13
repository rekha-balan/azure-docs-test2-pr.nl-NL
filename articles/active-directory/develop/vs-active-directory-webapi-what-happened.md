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
# <a name="what-happened-to-my-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="82285-103">What happened to my WebApi project (Visual Studio Azure Active Directory connected service)</span><span class="sxs-lookup"><span data-stu-id="82285-103">What happened to my WebApi project (Visual Studio Azure Active Directory connected service)</span></span>
> [!div class="op_single_selector"]
> * [Getting Started](vs-active-directory-webapi-getting-started.md)
> * [What Happened](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="references-have-been-added"></a><span data-ttu-id="82285-106">References have been added</span><span class="sxs-lookup"><span data-stu-id="82285-106">References have been added</span></span>
### <a name="nuget-package-references"></a><span data-ttu-id="82285-107">NuGet package references</span><span class="sxs-lookup"><span data-stu-id="82285-107">NuGet package references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

### <a name="net-references"></a><span data-ttu-id="82285-108">.NET references</span><span class="sxs-lookup"><span data-stu-id="82285-108">.NET references</span></span>
* `Microsoft.Owin`
* `Microsoft.Owin.Host.SystemWeb`
* `Microsoft.Owin.Security`
* `Microsoft.Owin.Security.ActiveDirectory`
* `Microsoft.Owin.Security.Jwt`
* `Microsoft.Owin.Security.OAuth`
* `Owin`
* `System.IdentityModel.Tokens.Jwt`

## <a name="code-changes"></a><span data-ttu-id="82285-109">Code changes</span><span class="sxs-lookup"><span data-stu-id="82285-109">Code changes</span></span>
### <a name="code-files-were-added-to-your-project"></a><span data-ttu-id="82285-110">Code files were added to your project</span><span class="sxs-lookup"><span data-stu-id="82285-110">Code files were added to your project</span></span>
<span data-ttu-id="82285-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span><span class="sxs-lookup"><span data-stu-id="82285-111">An authentication startup class, **App_Start/Startup.Auth.cs** was added to your project containing startup logic for Azure AD authentication.</span></span>

### <a name="startup-code-was-added-to-your-project"></a><span data-ttu-id="82285-112">Startup code was added to your project</span><span class="sxs-lookup"><span data-stu-id="82285-112">Startup code was added to your project</span></span>
<span data-ttu-id="82285-113">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to `ConfigureAuth(app)`.</span><span class="sxs-lookup"><span data-stu-id="82285-113">If you already had a Startup class in your project, the **Configuration** method was updated to include a call to `ConfigureAuth(app)`.</span></span> <span data-ttu-id="82285-114">Otherwise, a Startup class was added to your project.</span><span class="sxs-lookup"><span data-stu-id="82285-114">Otherwise, a Startup class was added to your project.</span></span>

### <a name="your-appconfig-or-webconfig-file-has-new-configuration-values"></a><span data-ttu-id="82285-115">Your app.config or web.config file has new configuration values.</span><span class="sxs-lookup"><span data-stu-id="82285-115">Your app.config or web.config file has new configuration values.</span></span>
<span data-ttu-id="82285-116">The following configuration entries have been added.</span><span class="sxs-lookup"><span data-stu-id="82285-116">The following configuration entries have been added.</span></span>

```
    <appSettings>
            <add key="ida:ClientId" value="ClientId from the new Azure AD App" />
            <add key="ida:Tenant" value="Your selected Azure AD Tenant" />
            <add key="ida:Audience" value="The App ID Uri from the wizard" />
    </appSettings>`
```

### <a name="an-azure-ad-app-was-created"></a><span data-ttu-id="82285-117">An Azure AD App was created</span><span class="sxs-lookup"><span data-stu-id="82285-117">An Azure AD App was created</span></span>
<span data-ttu-id="82285-118">An Azure AD Application was created in the directory that you selected in the wizard.</span><span class="sxs-lookup"><span data-stu-id="82285-118">An Azure AD Application was created in the directory that you selected in the wizard.</span></span>

[<span data-ttu-id="82285-119">Learn more about Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82285-119">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

## <a name="if-i-checked-disable-individual-user-accounts-authentication-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="82285-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span><span class="sxs-lookup"><span data-stu-id="82285-120">If I checked *disable Individual User Accounts authentication*, what additional changes were made to my project?</span></span>
<span data-ttu-id="82285-121">NuGet package references were removed, and files were removed and backed up.</span><span class="sxs-lookup"><span data-stu-id="82285-121">NuGet package references were removed, and files were removed and backed up.</span></span> <span data-ttu-id="82285-122">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span><span class="sxs-lookup"><span data-stu-id="82285-122">Depending on the state of your project, you may have to manually remove additional references or files, or modify code as appropriate.</span></span>

### <a name="nuget-package-references-removed-for-those-present"></a><span data-ttu-id="82285-123">NuGet package references removed (for those present)</span><span class="sxs-lookup"><span data-stu-id="82285-123">NuGet package references removed (for those present)</span></span>
* `Microsoft.AspNet.Identity.Core`
* `Microsoft.AspNet.Identity.EntityFramework`
* `Microsoft.AspNet.Identity.Owin`

### <a name="code-files-backed-up-and-removed-for-those-present"></a><span data-ttu-id="82285-124">Code files backed up and removed (for those present)</span><span class="sxs-lookup"><span data-stu-id="82285-124">Code files backed up and removed (for those present)</span></span>
<span data-ttu-id="82285-125">Each of following files was backed up and removed from the project.</span><span class="sxs-lookup"><span data-stu-id="82285-125">Each of following files was backed up and removed from the project.</span></span> <span data-ttu-id="82285-126">Backup files are located in a 'Backup' folder at the root of the project's directory.</span><span class="sxs-lookup"><span data-stu-id="82285-126">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `App_Start\IdentityConfig.cs`
* `Controllers\AccountController.cs`
* `Controllers\ManageController.cs`
* `Models\IdentityModels.cs`
* `Providers\ApplicationOAuthProvider.cs`

### <a name="code-files-backed-up-for-those-present"></a><span data-ttu-id="82285-127">Code files backed up (for those present)</span><span class="sxs-lookup"><span data-stu-id="82285-127">Code files backed up (for those present)</span></span>
<span data-ttu-id="82285-128">Each of following files was backed up before being replaced.</span><span class="sxs-lookup"><span data-stu-id="82285-128">Each of following files was backed up before being replaced.</span></span> <span data-ttu-id="82285-129">Backup files are located in a 'Backup' folder at the root of the project's directory.</span><span class="sxs-lookup"><span data-stu-id="82285-129">Backup files are located in a 'Backup' folder at the root of the project's directory.</span></span>

* `Startup.cs`
* `App_Start\Startup.Auth.cs`

## <a name="if-i-checked-read-directory-data-what-additional-changes-were-made-to-my-project"></a><span data-ttu-id="82285-130">If I checked *Read directory data*, what additional changes were made to my project?</span><span class="sxs-lookup"><span data-stu-id="82285-130">If I checked *Read directory data*, what additional changes were made to my project?</span></span>
### <a name="additional-changes-were-made-to-your-appconfig-or-webconfig"></a><span data-ttu-id="82285-131">Additional changes were made to your app.config or web.config</span><span class="sxs-lookup"><span data-stu-id="82285-131">Additional changes were made to your app.config or web.config</span></span>
<span data-ttu-id="82285-132">The following additional configuration entries have been added.</span><span class="sxs-lookup"><span data-stu-id="82285-132">The following additional configuration entries have been added.</span></span>

```
    <appSettings>
        <add key="ida:Password" value="Your Azure AD App's new password" />
    </appSettings>`
```

### <a name="your-azure-active-directory-app-was-updated"></a><span data-ttu-id="82285-133">Your Azure Active Directory App was updated</span><span class="sxs-lookup"><span data-stu-id="82285-133">Your Azure Active Directory App was updated</span></span>
<span data-ttu-id="82285-134">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:Password* in the `web.config` file.</span><span class="sxs-lookup"><span data-stu-id="82285-134">Your Azure Active Directory App was updated to include the *Read directory data* permission and an additional key was created which was then used as the *ida:Password* in the `web.config` file.</span></span>

## <a name="next-steps"></a><span data-ttu-id="82285-135">Next steps</span><span class="sxs-lookup"><span data-stu-id="82285-135">Next steps</span></span>
- [<span data-ttu-id="82285-136">Learn more about Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="82285-136">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

