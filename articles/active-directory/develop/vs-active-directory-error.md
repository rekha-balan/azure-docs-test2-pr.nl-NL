---
title: How to diagnose errors with the Azure Active Directory connected service
description: The active directory connected service detected an incompatible authentication type
services: active-directory
author: ghogen
manager: douge
ms.assetid: dd89ea63-4e45-4da1-9642-645b9309670a
ms.prod: visual-studio-dev15
ms.technology: vs-azure
ms.workload: azure-vs
ms.topic: conceptual
ms.date: 03/12/2018
ms.author: ghogen
ms.custom: aaddev, vs-azure
ms.openlocfilehash: 82449c3a8154142a64aa264f72d2dec75fe2f23c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44826644"
---
# <a name="diagnosing-errors-with-the-azure-active-directory-connected-service"></a><span data-ttu-id="2c16c-103">Diagnosing errors with the Azure Active Directory Connected Service</span><span class="sxs-lookup"><span data-stu-id="2c16c-103">Diagnosing errors with the Azure Active Directory Connected Service</span></span>

<span data-ttu-id="2c16c-104">While detecting previous authentication code, the Azure Active Director connect server detected an incompatible authentication type.</span><span class="sxs-lookup"><span data-stu-id="2c16c-104">While detecting previous authentication code, the Azure Active Director connect server detected an incompatible authentication type.</span></span>

<span data-ttu-id="2c16c-105">To correctly detect previous authentication code in a project, the project must be built.</span><span class="sxs-lookup"><span data-stu-id="2c16c-105">To correctly detect previous authentication code in a project, the project must be built.</span></span>  <span data-ttu-id="2c16c-106">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span><span class="sxs-lookup"><span data-stu-id="2c16c-106">If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.</span></span>

## <a name="project-types"></a><span data-ttu-id="2c16c-107">Project types</span><span class="sxs-lookup"><span data-stu-id="2c16c-107">Project types</span></span>

<span data-ttu-id="2c16c-108">The connected service checks the type of project you’re developing so it can inject the right authentication logic into the project.</span><span class="sxs-lookup"><span data-stu-id="2c16c-108">The connected service checks the type of project you’re developing so it can inject the right authentication logic into the project.</span></span> <span data-ttu-id="2c16c-109">If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.</span><span class="sxs-lookup"><span data-stu-id="2c16c-109">If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.</span></span> <span data-ttu-id="2c16c-110">If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.</span><span class="sxs-lookup"><span data-stu-id="2c16c-110">If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.</span></span> <span data-ttu-id="2c16c-111">The connected service doesn't support any other project type.</span><span class="sxs-lookup"><span data-stu-id="2c16c-111">The connected service doesn't support any other project type.</span></span>

## <a name="compatible-authentication-code"></a><span data-ttu-id="2c16c-112">Compatible authentication code</span><span class="sxs-lookup"><span data-stu-id="2c16c-112">Compatible authentication code</span></span>

<span data-ttu-id="2c16c-113">The connected service also checks for authentication settings that have been previously configured or are compatible with the service.</span><span class="sxs-lookup"><span data-stu-id="2c16c-113">The connected service also checks for authentication settings that have been previously configured or are compatible with the service.</span></span> <span data-ttu-id="2c16c-114">If all settings are present, it is considered a re-entrant case, and the connected service opens display the settings.</span><span class="sxs-lookup"><span data-stu-id="2c16c-114">If all settings are present, it is considered a re-entrant case, and the connected service opens display the settings.</span></span>  <span data-ttu-id="2c16c-115">If only some of the settings are present, it is considered an error case.</span><span class="sxs-lookup"><span data-stu-id="2c16c-115">If only some of the settings are present, it is considered an error case.</span></span>

<span data-ttu-id="2c16c-116">In an MVC project, the connected service checks for any of the following settings, which result from previous use of the service:</span><span class="sxs-lookup"><span data-stu-id="2c16c-116">In an MVC project, the connected service checks for any of the following settings, which result from previous use of the service:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

<span data-ttu-id="2c16c-117">In addition, the connected service checks for any of the following settings in a Web API project, which result from previous use of the service:</span><span class="sxs-lookup"><span data-stu-id="2c16c-117">In addition, the connected service checks for any of the following settings in a Web API project, which result from previous use of the service:</span></span>

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

## <a name="incompatible-authentication-code"></a><span data-ttu-id="2c16c-118">Incompatible authentication code</span><span class="sxs-lookup"><span data-stu-id="2c16c-118">Incompatible authentication code</span></span>

<span data-ttu-id="2c16c-119">Finally, the connected service attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2c16c-119">Finally, the connected service attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio.</span></span> <span data-ttu-id="2c16c-120">If you received this error, it means your project contains an incompatible authentication type.</span><span class="sxs-lookup"><span data-stu-id="2c16c-120">If you received this error, it means your project contains an incompatible authentication type.</span></span> <span data-ttu-id="2c16c-121">The connected service detects the following types of authentication from previous versions of Visual Studio:</span><span class="sxs-lookup"><span data-stu-id="2c16c-121">The connected service detects the following types of authentication from previous versions of Visual Studio:</span></span>

* <span data-ttu-id="2c16c-122">Windows Authentication</span><span class="sxs-lookup"><span data-stu-id="2c16c-122">Windows Authentication</span></span>
* <span data-ttu-id="2c16c-123">Individual User Accounts</span><span class="sxs-lookup"><span data-stu-id="2c16c-123">Individual User Accounts</span></span>
* <span data-ttu-id="2c16c-124">Organizational Accounts</span><span class="sxs-lookup"><span data-stu-id="2c16c-124">Organizational Accounts</span></span>

<span data-ttu-id="2c16c-125">To detect Windows Authentication in an MVC project, the connected looks for the `authentication` element in your `web.config` file.</span><span class="sxs-lookup"><span data-stu-id="2c16c-125">To detect Windows Authentication in an MVC project, the connected looks for the `authentication` element in your `web.config` file.</span></span>

```xml
<configuration>
    <system.web>
        <span style="background-color: yellow"><authentication mode="Windows" /></span>
    </system.web>
</configuration>
```

<span data-ttu-id="2c16c-126">To detect Windows Authentication in a Web API project, the connected service looks for the `IISExpressWindowsAuthentication` element in your project's `.csproj` file:</span><span class="sxs-lookup"><span data-stu-id="2c16c-126">To detect Windows Authentication in a Web API project, the connected service looks for the `IISExpressWindowsAuthentication` element in your project's `.csproj` file:</span></span>

```xml
<Project>
    <PropertyGroup>
        <span style="background-color: yellow"><IISExpressWindowsAuthentication>enabled</IISExpressWindowsAuthentication></span>
    </PropertyGroup>
</Project>
```

<span data-ttu-id="2c16c-127">To detect Individual User Accounts authentication, the connected service looks for the package element in your `packages.config` file.</span><span class="sxs-lookup"><span data-stu-id="2c16c-127">To detect Individual User Accounts authentication, the connected service looks for the package element in your `packages.config` file.</span></span>

```xml
<packages>
    <span style="background-color: yellow"><package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /></span>
</packages>
```

<span data-ttu-id="2c16c-128">To detect an old form of Organizational Account authentication, the connected service looks for the following element in`web.config`:</span><span class="sxs-lookup"><span data-stu-id="2c16c-128">To detect an old form of Organizational Account authentication, the connected service looks for the following element in`web.config`:</span></span>

```xml
<configuration>
    <appSettings>
        <span style="background-color: yellow"><add key="ida:Realm" value="***" /></span>
    </appSettings>
</configuration>
```

<span data-ttu-id="2c16c-129">To change the authentication type, remove the incompatible authentication type and try adding the connected service again.</span><span class="sxs-lookup"><span data-stu-id="2c16c-129">To change the authentication type, remove the incompatible authentication type and try adding the connected service again.</span></span>

<span data-ttu-id="2c16c-130">For more information, see [Authentication Scenarios for Azure AD](authentication-scenarios.md).</span><span class="sxs-lookup"><span data-stu-id="2c16c-130">For more information, see [Authentication Scenarios for Azure AD](authentication-scenarios.md).</span></span>