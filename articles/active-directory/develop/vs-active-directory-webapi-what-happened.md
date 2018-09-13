---
title: Changes made to a WebAPI project when you connect to Azure AD
description: Describes what happens to your WebAPI project when you connect to Azure AD by using Visual Studio
services: active-directory
author: ghogen
manager: douge
ms.assetid: 57630aee-26a2-4326-9dbb-ea2a66daa8b0
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/12/2018
ms.author: ghogen
ms.custom: aaddev, vs-azure
ms.openlocfilehash: 04732d6541fd6132360d4c235b35979c70772922
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44776210"
---
# <a name="what-happened-to-my-webapi-project-visual-studio-azure-active-directory-connected-service"></a><span data-ttu-id="5e0b3-103">What happened to my WebAPI project (Visual Studio Azure Active Directory connected service)</span><span class="sxs-lookup"><span data-stu-id="5e0b3-103">What happened to my WebAPI project (Visual Studio Azure Active Directory connected service)</span></span>

> [!div class="op_single_selector"]
> - [Getting Started](vs-active-directory-webapi-getting-started.md)
> - [What Happened](vs-active-directory-webapi-what-happened.md)

<span data-ttu-id="5e0b3-106">This article identifies the exact changes made to ASP.NET WebAPI, ASP.NET Single-Page Application, and ASP.NET Azure API projects when adding the [Azure Active Directory connected service using Visual Studio](vs-active-directory-add-connected-service.md).</span><span class="sxs-lookup"><span data-stu-id="5e0b3-106">This article identifies the exact changes made to ASP.NET WebAPI, ASP.NET Single-Page Application, and ASP.NET Azure API projects when adding the [Azure Active Directory connected service using Visual Studio](vs-active-directory-add-connected-service.md).</span></span> <span data-ttu-id="5e0b3-107">Also applies to the ASP.NET Azure Mobile Service projects in Visual Studio 2015.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-107">Also applies to the ASP.NET Azure Mobile Service projects in Visual Studio 2015.</span></span>

<span data-ttu-id="5e0b3-108">For information on working with the connected service, see [Getting Started](vs-active-directory-webapi-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="5e0b3-108">For information on working with the connected service, see [Getting Started](vs-active-directory-webapi-getting-started.md).</span></span>

## <a name="added-references"></a><span data-ttu-id="5e0b3-109">Added references</span><span class="sxs-lookup"><span data-stu-id="5e0b3-109">Added references</span></span>

<span data-ttu-id="5e0b3-110">Affects the project file \*.NET references) and `packages.config` (NuGet references).</span><span class="sxs-lookup"><span data-stu-id="5e0b3-110">Affects the project file \*.NET references) and `packages.config` (NuGet references).</span></span>

| <span data-ttu-id="5e0b3-111">Type</span><span class="sxs-lookup"><span data-stu-id="5e0b3-111">Type</span></span> | <span data-ttu-id="5e0b3-112">Reference</span><span class="sxs-lookup"><span data-stu-id="5e0b3-112">Reference</span></span> |
| --- | --- |
| <span data-ttu-id="5e0b3-113">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-113">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-114">Microsoft.Owin</span><span class="sxs-lookup"><span data-stu-id="5e0b3-114">Microsoft.Owin</span></span> |
| <span data-ttu-id="5e0b3-115">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-115">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-116">Microsoft.Owin.Host.SystemWeb</span><span class="sxs-lookup"><span data-stu-id="5e0b3-116">Microsoft.Owin.Host.SystemWeb</span></span> |
| <span data-ttu-id="5e0b3-117">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-117">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-118">Microsoft.Owin.Security</span><span class="sxs-lookup"><span data-stu-id="5e0b3-118">Microsoft.Owin.Security</span></span> |
| <span data-ttu-id="5e0b3-119">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-119">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-120">Microsoft.Owin.Security.ActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="5e0b3-120">Microsoft.Owin.Security.ActiveDirectory</span></span> |
| <span data-ttu-id="5e0b3-121">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-121">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-122">Microsoft.Owin.Security.Jwt</span><span class="sxs-lookup"><span data-stu-id="5e0b3-122">Microsoft.Owin.Security.Jwt</span></span> |
| <span data-ttu-id="5e0b3-123">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-123">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-124">Microsoft.Owin.Security.OAuth</span><span class="sxs-lookup"><span data-stu-id="5e0b3-124">Microsoft.Owin.Security.OAuth</span></span> |
| <span data-ttu-id="5e0b3-125">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-125">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-126">Owin</span><span class="sxs-lookup"><span data-stu-id="5e0b3-126">Owin</span></span> |
| <span data-ttu-id="5e0b3-127">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-127">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-128">System.IdentityModel.Tokens.Jwt</span><span class="sxs-lookup"><span data-stu-id="5e0b3-128">System.IdentityModel.Tokens.Jwt</span></span> |

<span data-ttu-id="5e0b3-129">Additional references if you selected the **Read directory data** option:</span><span class="sxs-lookup"><span data-stu-id="5e0b3-129">Additional references if you selected the **Read directory data** option:</span></span>

| <span data-ttu-id="5e0b3-130">Type</span><span class="sxs-lookup"><span data-stu-id="5e0b3-130">Type</span></span> | <span data-ttu-id="5e0b3-131">Reference</span><span class="sxs-lookup"><span data-stu-id="5e0b3-131">Reference</span></span> |
| --- | --- |
| <span data-ttu-id="5e0b3-132">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-132">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-133">EntityFramework</span><span class="sxs-lookup"><span data-stu-id="5e0b3-133">EntityFramework</span></span> |
| <span data-ttu-id="5e0b3-134">.NET</span><span class="sxs-lookup"><span data-stu-id="5e0b3-134">.NET</span></span>        | <span data-ttu-id="5e0b3-135">EntityFramework.SqlServer (Visual Studio 2015 only)</span><span class="sxs-lookup"><span data-stu-id="5e0b3-135">EntityFramework.SqlServer (Visual Studio 2015 only)</span></span> |
| <span data-ttu-id="5e0b3-136">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-136">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-137">Microsoft.Azure.ActiveDirectory.GraphClient</span><span class="sxs-lookup"><span data-stu-id="5e0b3-137">Microsoft.Azure.ActiveDirectory.GraphClient</span></span> |
| <span data-ttu-id="5e0b3-138">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-138">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-139">Microsoft.Data.Edm</span><span class="sxs-lookup"><span data-stu-id="5e0b3-139">Microsoft.Data.Edm</span></span> |
| <span data-ttu-id="5e0b3-140">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-140">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-141">Microsoft.Data.OData</span><span class="sxs-lookup"><span data-stu-id="5e0b3-141">Microsoft.Data.OData</span></span> |
| <span data-ttu-id="5e0b3-142">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-142">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-143">Microsoft.Data.Services.Client</span><span class="sxs-lookup"><span data-stu-id="5e0b3-143">Microsoft.Data.Services.Client</span></span> |
| <span data-ttu-id="5e0b3-144">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-144">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-145">Microsoft.IdentityModel.Clients.ActiveDirectory</span><span class="sxs-lookup"><span data-stu-id="5e0b3-145">Microsoft.IdentityModel.Clients.ActiveDirectory</span></span> |
| <span data-ttu-id="5e0b3-146">.NET</span><span class="sxs-lookup"><span data-stu-id="5e0b3-146">.NET</span></span>        | <span data-ttu-id="5e0b3-147">Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms</span><span class="sxs-lookup"><span data-stu-id="5e0b3-147">Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms</span></span><br><span data-ttu-id="5e0b3-148">(Visual Studio 2015 only)</span><span class="sxs-lookup"><span data-stu-id="5e0b3-148">(Visual Studio 2015 only)</span></span> |
| <span data-ttu-id="5e0b3-149">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-149">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-150">System.Spatial</span><span class="sxs-lookup"><span data-stu-id="5e0b3-150">System.Spatial</span></span> |

<span data-ttu-id="5e0b3-151">The following references are removed (ASP.NET 4 projects only, as in Visual Studio 2015):</span><span class="sxs-lookup"><span data-stu-id="5e0b3-151">The following references are removed (ASP.NET 4 projects only, as in Visual Studio 2015):</span></span>

| <span data-ttu-id="5e0b3-152">Type</span><span class="sxs-lookup"><span data-stu-id="5e0b3-152">Type</span></span> | <span data-ttu-id="5e0b3-153">Reference</span><span class="sxs-lookup"><span data-stu-id="5e0b3-153">Reference</span></span> |
| --- | --- |
| <span data-ttu-id="5e0b3-154">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-154">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-155">Microsoft.AspNet.Identity.Core</span><span class="sxs-lookup"><span data-stu-id="5e0b3-155">Microsoft.AspNet.Identity.Core</span></span> |
| <span data-ttu-id="5e0b3-156">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-156">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-157">Microsoft.AspNet.Identity.EntityFramework</span><span class="sxs-lookup"><span data-stu-id="5e0b3-157">Microsoft.AspNet.Identity.EntityFramework</span></span> |
| <span data-ttu-id="5e0b3-158">.NET; NuGet</span><span class="sxs-lookup"><span data-stu-id="5e0b3-158">.NET; NuGet</span></span> | <span data-ttu-id="5e0b3-159">Microsoft.AspNet.Identity.Owin</span><span class="sxs-lookup"><span data-stu-id="5e0b3-159">Microsoft.AspNet.Identity.Owin</span></span> |

## <a name="project-file-changes"></a><span data-ttu-id="5e0b3-160">Project file changes</span><span class="sxs-lookup"><span data-stu-id="5e0b3-160">Project file changes</span></span>

- <span data-ttu-id="5e0b3-161">Set the property `IISExpressSSLPort` to a distinct number.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-161">Set the property `IISExpressSSLPort` to a distinct number.</span></span>
- <span data-ttu-id="5e0b3-162">Set the property `WebProject_DirectoryAccessLevelKey` to 0, or 1 if you selected the **Read directory data** option.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-162">Set the property `WebProject_DirectoryAccessLevelKey` to 0, or 1 if you selected the **Read directory data** option.</span></span>
- <span data-ttu-id="5e0b3-163">Set the property `IISUrl` to `https://localhost:<port>/` where `<port>` matches the `IISExpressSSLPort` value.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-163">Set the property `IISUrl` to `https://localhost:<port>/` where `<port>` matches the `IISExpressSSLPort` value.</span></span>

## <a name="webconfig-or-appconfig-changes"></a><span data-ttu-id="5e0b3-164">web.config or app.config changes</span><span class="sxs-lookup"><span data-stu-id="5e0b3-164">web.config or app.config changes</span></span>

- <span data-ttu-id="5e0b3-165">Added the following configuration entries:</span><span class="sxs-lookup"><span data-stu-id="5e0b3-165">Added the following configuration entries:</span></span>

    ```xml
    <appSettings>
        <add key="ida:ClientId" value="<ClientId from the new Azure AD app>" />
        <add key="ida:Tenant" value="<your selected Azure domain>" />
        <add key="ida:Audience" value="<your selected domain + / + project name>" />
    </appSettings>
    ```

- <span data-ttu-id="5e0b3-166">Visual Studio 2017 only: Also added the following entry under `<appSettings>`"</span><span class="sxs-lookup"><span data-stu-id="5e0b3-166">Visual Studio 2017 only: Also added the following entry under `<appSettings>`"</span></span>

    ```xml
    <add key="ida:MetadataAddress" value="<domain URL + /federationmetadata/2007-06/federationmetadata.xml>" />
    ```

- <span data-ttu-id="5e0b3-167">Added `<dependentAssembly>` elements under the `<runtime><assemblyBinding>` node for `System.IdentityModel.Tokens.Jwt`.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-167">Added `<dependentAssembly>` elements under the `<runtime><assemblyBinding>` node for `System.IdentityModel.Tokens.Jwt`.</span></span>

- <span data-ttu-id="5e0b3-168">If you selected the **Read directory data** option, added the following configuration entry under `<appSettings>`:</span><span class="sxs-lookup"><span data-stu-id="5e0b3-168">If you selected the **Read directory data** option, added the following configuration entry under `<appSettings>`:</span></span>

    ```xml
    <add key="ida:Password" value="<Your Azure AD app's new password>" />
    ```

## <a name="code-changes-and-additions"></a><span data-ttu-id="5e0b3-169">Code changes and additions</span><span class="sxs-lookup"><span data-stu-id="5e0b3-169">Code changes and additions</span></span>

- <span data-ttu-id="5e0b3-170">Added the `[Authorize]` attribute to `Controllers/ValueController.cs` and any other existing controllers.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-170">Added the `[Authorize]` attribute to `Controllers/ValueController.cs` and any other existing controllers.</span></span>

- <span data-ttu-id="5e0b3-171">Added an authentication startup class, `App_Start/Startup.Auth.cs`, containing startup logic for Azure AD authentication, or modified it accordingly.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-171">Added an authentication startup class, `App_Start/Startup.Auth.cs`, containing startup logic for Azure AD authentication, or modified it accordingly.</span></span> <span data-ttu-id="5e0b3-172">If you selected the **Read directory data** option, this file also contains code to receive an OAuth code and exchange it for an access token.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-172">If you selected the **Read directory data** option, this file also contains code to receive an OAuth code and exchange it for an access token.</span></span>

- <span data-ttu-id="5e0b3-173">(Visual Studio 2015 with ASP.NET 4 app only) Removed `App_Start/IdentityConfig.cs` and added `Controllers/AccountController.cs`, `Models/IdentityModel.cs`, and `Providers/ApplicationAuthProvider.cs`.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-173">(Visual Studio 2015 with ASP.NET 4 app only) Removed `App_Start/IdentityConfig.cs` and added `Controllers/AccountController.cs`, `Models/IdentityModel.cs`, and `Providers/ApplicationAuthProvider.cs`.</span></span>

- <span data-ttu-id="5e0b3-174">Added `Connected Services/AzureAD/ConnectedService.json` (Visual Studio 2017) or `Service References/Azure AD/ConnectedService.json` (Visual Studio 2015), containing information that Visual Studio uses to track the addition of the connected service.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-174">Added `Connected Services/AzureAD/ConnectedService.json` (Visual Studio 2017) or `Service References/Azure AD/ConnectedService.json` (Visual Studio 2015), containing information that Visual Studio uses to track the addition of the connected service.</span></span>

### <a name="file-backup-visual-studio-2015"></a><span data-ttu-id="5e0b3-175">File backup (Visual Studio 2015)</span><span class="sxs-lookup"><span data-stu-id="5e0b3-175">File backup (Visual Studio 2015)</span></span>

<span data-ttu-id="5e0b3-176">When adding the connected service, Visual Studio 2015 backs up changed and removed files.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-176">When adding the connected service, Visual Studio 2015 backs up changed and removed files.</span></span> <span data-ttu-id="5e0b3-177">All affected files are saved in the folder `Backup/AzureAD`.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-177">All affected files are saved in the folder `Backup/AzureAD`.</span></span> <span data-ttu-id="5e0b3-178">Visual Studio 2017 does not create backups.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-178">Visual Studio 2017 does not create backups.</span></span>

- `Startup.cs`
- `App_Start\IdentityConfig.cs`
- `App_Start\Startup.Auth.cs`
- `Controllers\AccountController.cs`
- `Controllers\ManageController.cs`
- `Models\IdentityModels.cs`
- `Models\ApplicationOAuthProvider.cs`

## <a name="changes-on-azure"></a><span data-ttu-id="5e0b3-179">Changes on Azure</span><span class="sxs-lookup"><span data-stu-id="5e0b3-179">Changes on Azure</span></span>

- <span data-ttu-id="5e0b3-180">Created an Azure AD Application in the domain that you selected when adding the connected service.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-180">Created an Azure AD Application in the domain that you selected when adding the connected service.</span></span>
- <span data-ttu-id="5e0b3-181">Updated the app to include the **Read directory data** permission if that option was selected.</span><span class="sxs-lookup"><span data-stu-id="5e0b3-181">Updated the app to include the **Read directory data** permission if that option was selected.</span></span>

<span data-ttu-id="5e0b3-182">[Learn more about Azure Active Directory](https://azure.microsoft.com/services/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="5e0b3-182">[Learn more about Azure Active Directory](https://azure.microsoft.com/services/active-directory/).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e0b3-183">Next steps</span><span class="sxs-lookup"><span data-stu-id="5e0b3-183">Next steps</span></span>

- [<span data-ttu-id="5e0b3-184">Authentication scenarios for Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="5e0b3-184">Authentication scenarios for Azure Active Directory</span></span>](authentication-scenarios.md)
- [<span data-ttu-id="5e0b3-185">Add sign-in with Microsoft to an ASP.NET web app</span><span class="sxs-lookup"><span data-stu-id="5e0b3-185">Add sign-in with Microsoft to an ASP.NET web app</span></span>](quickstart-v1-aspnet-webapp.md)