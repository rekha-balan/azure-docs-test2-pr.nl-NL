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
# <a name="diagnosing-errors-with-the-azure-active-directory-connection-wizard"></a>Diagnosing errors with the Azure Active Directory Connection Wizard
While detecting previous authentication code, the wizard detected an incompatible authentication type.   

## <a name="what-is-being-checked"></a>What is being checked?
**Note:** To correctly detect previous authentication code in a project, the project must be built.  If you encountered this error and you don't have a previous authentication code in your project, rebuild and try again.

### <a name="project-types"></a>Project Types
The wizard checks the type of project you’re developing so it can inject the right authentication logic into the project.  If there is any controller that derives from `ApiController` in the project, the project is considered a WebAPI project.  If there are only controllers that derive from `MVC.Controller` in the project, the project is considered an MVC project.  Anything else is not supported by the wizard.

### <a name="compatible-authentication-code"></a>Compatible Authentication Code
The wizard also checks for authentication settings that have been previously configured with the wizard or are compatible with the wizard.  If all settings are present, it is considered a re-entrant case, and the wizard opens display the settings.  If only some of the settings are present, it is considered an error case.

In an MVC project, the wizard checks for any of the following settings, which result from previous use of the wizard:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:AADInstance" value="" />
    <add key="ida:PostLogoutRedirectUri" value="" />

In addition, the wizard checks for any of the following settings in a Web API project, which result from previous use of the wizard:

    <add key="ida:ClientId" value="" />
    <add key="ida:Tenant" value="" />
    <add key="ida:Audience" value="" />

### <a name="incompatible-authentication-code"></a>Incompatible Authentication Code
Finally, the wizard attempts to detect versions of authentication code that have been configured with previous versions of Visual Studio. If you received this error, it means your project contains an incompatible authentication type. The wizard detects the following types of authentication from previous versions of Visual Studio:

* Windows Authentication 
* Individual User Accounts 
* Organizational Accounts 

To detect Windows Authentication in an MVC project, the wizard looks for the `authentication` element from your **web.config** file.

<pre>
    &lt;configuration&gt;
        &lt;system.web&gt;
            <span style="background-color: yellow">&lt;authentication mode="Windows" /&gt;</span>
        &lt;/system.web&gt;
    &lt;/configuration&gt;
</pre>

To detect Windows Authentication in a Web API project, the wizard looks for the `IISExpressWindowsAuthentication` element from your project's **.csproj** file:

<pre>
    &lt;Project&gt;
        &lt;PropertyGroup&gt;
            <span style="background-color: yellow">&lt;IISExpressWindowsAuthentication&gt;enabled&lt;/IISExpressWindowsAuthentication&gt;</span>
        &lt;/PropertyGroup>
    &lt;/Project&gt;
</pre>

To detect Individual User Accounts authentication, the wizard looks for the package element from your **Packages.config** file.

<pre>
    &lt;packages&gt;
        <span style="background-color: yellow">&lt;package id="Microsoft.AspNet.Identity.EntityFramework" version="2.1.0" targetFramework="net45" /&gt;</span>
    &lt;/packages&gt;
</pre>

To detect an old form of Organizational Account authentication, the wizard looks for the following element from **web.config**:

<pre>
    &lt;configuration&gt;
        &lt;appSettings&gt;
            <span style="background-color: yellow">&lt;add key="ida:Realm" value="***" /&gt;</span>
        &lt;/appSettings&gt;
    &lt;/configuration&gt;
</pre>

To change the authentication type, remove the incompatible authentication type and run the wizard again.

For more information, see [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md).

#<a name="next-steps"></a>Next steps
- [Authentication Scenarios for Azure AD](active-directory-authentication-scenarios.md)