---
title: How to diagnose errors with the Azure Active Directory Connection Wizard
description: The active directory connection wizard detected an incompatible authentication type
services: active-directory
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/05/2017
ms.author: tarcher
ms.openlocfilehash: 76a60d16d975efa18da27fda87cf447bd1223acb
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661535"
---
# <a name="diagnosing-errors-with-the-azure-active-directory-connection-wizard"></a><span data-ttu-id="2f6b6-103">Diagnosing errors with the Azure Active Directory Connection Wizard</span><span class="sxs-lookup"><span data-stu-id="2f6b6-103">Diagnosing errors with the Azure Active Directory Connection Wizard</span></span>
<span data-ttu-id="2f6b6-104">While detecting previous authentication code, the wizard detected an incompatible authentication type.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-104">While detecting previous authentication code, the wizard detected an incompatible authentication type.</span></span>   

## <a name="what-is-being-checked"></a><span data-ttu-id="2f6b6-105">What is being checked?</span><span class="sxs-lookup"><span data-stu-id="2f6b6-105">What is being checked?</span></span>
<span data-ttu-id="2f6b6-106">**Note:** To correctly detect previous authentication code in a project, the project must be built.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-106">**Note:** To correctly detect previous authentication code in a project, the project must be built.</span></span>  <span data-ttu-id="2f6b6-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-107">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

### <a name="project-types"></a><span data-ttu-id="2f6b6-108">Project Types</span><span class="sxs-lookup"><span data-stu-id="2f6b6-108">Project Types</span></span>
<span data-ttu-id="2f6b6-109">The wizard checks the type of project you’re developing so it can inject the right authentication logic into the project.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-109">The wizard checks the type of project you’re developing so it can inject the right authentication logic into the project.</span></span>  <span data-ttu-id="2f6b6-110">If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-110">If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.</span></span>  <span data-ttu-id="2f6b6-111">If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-111">If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.</span></span>  <span data-ttu-id="2f6b6-112">Anything else is not supported by the wizard.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-112">Anything else is not supported by the wizard.</span></span>

### <a name="compatible-authentication-code"></a><span data-ttu-id="2f6b6-113">Compatible Authentication Code</span><span class="sxs-lookup"><span data-stu-id="2f6b6-113">Compatible Authentication Code</span></span>
<span data-ttu-id="2f6b6-114">The wizard also checks for authentication settings that have been previously configured with the wizard or are compatible with the wizard.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-114">The wizard also checks for authentication settings that have been previously configured with the wizard or are compatible with the wizard.</span></span>  <span data-ttu-id="2f6b6-115">If all settings are present, it is considered a re-entrant case, and the wizard opens display the settings.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-115">If all settings are present, it is considered a re-entrant case, and the wizard opens display the settings.</span></span>  <span data-ttu-id="2f6b6-116">If only some of the settings are present, it is considered an error case.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-116">If only some of the settings are present, it is considered an error case.</span></span>

<span data-ttu-id="2f6b6-117">In an MVC project, the wizard checks for any of the following settings, which result from previous use of the wizard:</span><span class="sxs-lookup"><span data-stu-id="2f6b6-117">In an MVC project, the wizard checks for any of the following settings, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="2f6b6-118">In addition, the wizard checks for any of the following settings in a Web API project, which result from previous use of the wizard:</span><span class="sxs-lookup"><span data-stu-id="2f6b6-118">In addition, the wizard checks for any of the following settings in a Web API project, which result from previous use of the wizard:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a><span data-ttu-id="2f6b6-119">Incompatible Authentication Code</span><span class="sxs-lookup"><span data-stu-id="2f6b6-119">Incompatible Authentication Code</span></span>
<span data-ttu-id="2f6b6-120">Finally, the wizard attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-120">Finally, the wizard attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="2f6b6-121">If you received this error, it means your project contains an incompatible authentication type.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-121">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="2f6b6-122">The wizard detects the following types of authentication from previous versions of Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="2f6b6-122">The wizard detects the following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="2f6b6-123">Windows Authentication</span><span class="sxs-lookup"><span data-stu-id="2f6b6-123">Windows Authentication</span></span> 
* <span data-ttu-id="2f6b6-124">Individual User Accounts</span><span class="sxs-lookup"><span data-stu-id="2f6b6-124">Individual User Accounts</span></span> 
* <span data-ttu-id="2f6b6-125">Organizational Accounts</span><span class="sxs-lookup"><span data-stu-id="2f6b6-125">Organizational Accounts</span></span> 

<span data-ttu-id="2f6b6-126">To detect Windows Authentication in an MVC project, the wizard looks for the `authentication` element from your **web.config** file.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-126">To detect Windows Authentication in an MVC project, the wizard looks for the `authentication` element from your **web.config** file.</span></span>

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="2f6b6-127">To detect Windows Authentication in a Web API project, the wizard looks for the `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span><span class="sxs-lookup"><span data-stu-id="2f6b6-127">To detect Windows Authentication in a Web API project, the wizard looks for the `IISExpressWindowsAuthentication` element from your project's **.csproj** file:</span></span>

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

<span data-ttu-id="2f6b6-128">To detect Individual User Accounts authentication, the wizard looks for the package element from your **Packages.config** file.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-128">To detect Individual User Accounts authentication, the wizard looks for the package element from your **Packages.config** file.</span></span>

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

<span data-ttu-id="2f6b6-129">To detect an old form of Organizational Account authentication, the wizard looks for the following element from **web.config**:</span><span class="sxs-lookup"><span data-stu-id="2f6b6-129">To detect an old form of Organizational Account authentication, the wizard looks for the following element from **web.config**:</span></span>

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

<span data-ttu-id="2f6b6-130">To change the authentication type, remove the incompatible authentication type and run the wizard again.</span><span class="sxs-lookup"><span data-stu-id="2f6b6-130">To change the authentication type, remove the incompatible authentication type and run the wizard again.</span></span>

<span data-ttu-id="2f6b6-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="2f6b6-131">For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).</span></span>

#<a name="next-steps"></a><span data-ttu-id="2f6b6-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="2f6b6-132">Next steps</span></span>
- [<span data-ttu-id="2f6b6-133">Authentication Scenarios for Azure AD</span><span class="sxs-lookup"><span data-stu-id="2f6b6-133">Authentication Scenarios for Azure AD</span></span>](active-directory-authentication-scenarios.md)