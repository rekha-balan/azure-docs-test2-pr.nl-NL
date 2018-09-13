---
title: Silent install Azure AD Application Proxy Connector | Microsoft Docs
description: Covers how to perform an unattended installation of Azure AD Application Proxy Connector to provide secure remote access to your on-premises apps.
services: active-directory
documentationcenter: ''
author: kgremban
manager: femila
editor: harshja
ms.assetid: 3aa1c7f2-fb2a-4693-abd5-95bb53700cbb
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: kgremban
ms.openlocfilehash: cf00d47efc613f7bdc152c1b5f0d0830fb44a785
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44671508"
---
# <a name="how-to-silently-install-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="69dcc-103">How to silently install the Azure AD Application Proxy Connector</span><span class="sxs-lookup"><span data-stu-id="69dcc-103">How to silently install the Azure AD Application Proxy Connector</span></span>
<span data-ttu-id="69dcc-104">You want to be able to send an installation script to multiple Windows servers or to Windows Servers that don't have user interface enabled.</span><span class="sxs-lookup"><span data-stu-id="69dcc-104">You want to be able to send an installation script to multiple Windows servers or to Windows Servers that don't have user interface enabled.</span></span> <span data-ttu-id="69dcc-105">This topic explains how to create a Windows PowerShell script that enables unattended installation to install and register your Azure AD Application Proxy Connector.</span><span class="sxs-lookup"><span data-stu-id="69dcc-105">This topic explains how to create a Windows PowerShell script that enables unattended installation to install and register your Azure AD Application Proxy Connector.</span></span>

<span data-ttu-id="69dcc-106">This capability is useful when you want to:</span><span class="sxs-lookup"><span data-stu-id="69dcc-106">This capability is useful when you want to:</span></span>

* <span data-ttu-id="69dcc-107">Install the connector on machines with no UI layer or when you cannot RDP to the machine.</span><span class="sxs-lookup"><span data-stu-id="69dcc-107">Install the connector on machines with no UI layer or when you cannot RDP to the machine.</span></span>
* <span data-ttu-id="69dcc-108">Install and register many connectors at once.</span><span class="sxs-lookup"><span data-stu-id="69dcc-108">Install and register many connectors at once.</span></span>
* <span data-ttu-id="69dcc-109">Integrate the connector installation and registration as part of another procedure.</span><span class="sxs-lookup"><span data-stu-id="69dcc-109">Integrate the connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="69dcc-110">Create a standard server image that contains the connector bits but is not registered.</span><span class="sxs-lookup"><span data-stu-id="69dcc-110">Create a standard server image that contains the connector bits but is not registered.</span></span>

## <a name="enabling-access"></a><span data-ttu-id="69dcc-111">Enabling Access</span><span class="sxs-lookup"><span data-stu-id="69dcc-111">Enabling Access</span></span>
<span data-ttu-id="69dcc-112">Application Proxy works by installing a slim Windows Server service called the Connector inside your network.</span><span class="sxs-lookup"><span data-stu-id="69dcc-112">Application Proxy works by installing a slim Windows Server service called the Connector inside your network.</span></span> <span data-ttu-id="69dcc-113">For the Application Proxy Connector to work it has to be registered with your Azure AD directory using a global administrator and password.</span><span class="sxs-lookup"><span data-stu-id="69dcc-113">For the Application Proxy Connector to work it has to be registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="69dcc-114">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span><span class="sxs-lookup"><span data-stu-id="69dcc-114">Ordinarily this information is entered during Connector installation in a pop-up dialog box.</span></span> <span data-ttu-id="69dcc-115">Alternatively, you can use Windows PowerShell to create a credential object to enter your registration information, or you can create your own token and use it to enter your registration information.</span><span class="sxs-lookup"><span data-stu-id="69dcc-115">Alternatively, you can use Windows PowerShell to create a credential object to enter your registration information, or you can create your own token and use it to enter your registration information.</span></span>

## <a name="step-1--install-the-connector-without-registration"></a><span data-ttu-id="69dcc-116">Step 1:  Install the Connector without registration</span><span class="sxs-lookup"><span data-stu-id="69dcc-116">Step 1:  Install the Connector without registration</span></span>
<span data-ttu-id="69dcc-117">Install the Connector MSIs without registering the Connector as follows:</span><span class="sxs-lookup"><span data-stu-id="69dcc-117">Install the Connector MSIs without registering the Connector as follows:</span></span>

1. <span data-ttu-id="69dcc-118">Open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="69dcc-118">Open a command prompt.</span></span>
2. <span data-ttu-id="69dcc-119">Run the following command in which the /q means quiet installation - the installation will not prompt you to accept the End-User License Agreement.</span><span class="sxs-lookup"><span data-stu-id="69dcc-119">Run the following command in which the /q means quiet installation - the installation will not prompt you to accept the End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="step-2-register-the-connector-with-azure-active-directory"></a><span data-ttu-id="69dcc-120">Step 2: Register the Connector with Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="69dcc-120">Step 2: Register the Connector with Azure Active Directory</span></span>
<span data-ttu-id="69dcc-121">This can be accomplished using either of the following methods:</span><span class="sxs-lookup"><span data-stu-id="69dcc-121">This can be accomplished using either of the following methods:</span></span>

* <span data-ttu-id="69dcc-122">Register the Connector using a Windows PowerShell credential object</span><span class="sxs-lookup"><span data-stu-id="69dcc-122">Register the Connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="69dcc-123">Register the Connector using a token created offline</span><span class="sxs-lookup"><span data-stu-id="69dcc-123">Register the Connector using a token created offline</span></span>

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="69dcc-124">Register the Connector using a Windows PowerShell credential object</span><span class="sxs-lookup"><span data-stu-id="69dcc-124">Register the Connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="69dcc-125">Create the Windows PowerShell Credentials object by running the following, where \<username\> and \<password\> should be replaced with the username and password for your directory:</span><span class="sxs-lookup"><span data-stu-id="69dcc-125">Create the Windows PowerShell Credentials object by running the following, where \<username\> and \<password\> should be replaced with the username and password for your directory:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="69dcc-126">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the script using the PowerShell credentials object you created, where $cred is the name of the PowerShell credentials object you created:</span><span class="sxs-lookup"><span data-stu-id="69dcc-126">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the script using the PowerShell credentials object you created, where $cred is the name of the PowerShell credentials object you created:</span></span>
   
        RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred

### <a name="register-the-connector-using-a-token-created-offline"></a><span data-ttu-id="69dcc-127">Register the Connector using a token created offline</span><span class="sxs-lookup"><span data-stu-id="69dcc-127">Register the Connector using a token created offline</span></span>
1. <span data-ttu-id="69dcc-128">Create an offline token using the AuthenticationContext class using the values in the code snippet:</span><span class="sxs-lookup"><span data-stu-id="69dcc-128">Create an offline token using the AuthenticationContext class using the values in the code snippet:</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// The AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.windows.net/common/oauth2/token?api-version=1.0");

        /// <summary>
        /// The application ID of the connector in AAD
        /// </summary>
        static readonly string ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489";

        /// <summary>
        /// The reply address of the connector application in AAD
        /// </summary>
        static readonly Uri ConnectorRedirectAddress = new Uri("urn:ietf:wg:oauth:2.0:oob");

        /// <summary>
        /// The AppIdUri of the registration service in AAD
        /// </summary>
        static readonly Uri RegistrationServiceAppIdUri = new Uri("https://proxy.cloudwebappproxy.net/registerapp");

        #endregion

        #region private members
        private string token;
        private string tenantID;
        #endregion

        public void GetAuthenticationToken()
        {
            AuthenticationContext authContext = new AuthenticationContext(AadAuthenticationEndpoint.AbsoluteUri);

            AuthenticationResult authResult = authContext.AcquireToken(RegistrationServiceAppIdUri.AbsoluteUri,
                ConnectorAppId,
                ConnectorRedirectAddress,
                PromptBehavior.Always);

            if (authResult == null || string.IsNullOrEmpty(authResult.AccessToken) || string.IsNullOrEmpty(authResult.TenantId))
            {
                Trace.TraceError("Authentication result, token or tenant id returned are null");
                throw new InvalidOperationException("Authentication result, token or tenant id returned are null");
            }

            token = authResult.AccessToken;
            tenantID = authResult.TenantId;
        }


2. <span data-ttu-id="69dcc-129">Once you have the token, create a SecureString using the token:</span><span class="sxs-lookup"><span data-stu-id="69dcc-129">Once you have the token, create a SecureString using the token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="69dcc-130">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span><span class="sxs-lookup"><span data-stu-id="69dcc-130">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID>`

## <a name="next-steps"></a><span data-ttu-id="69dcc-131">Next steps</span><span class="sxs-lookup"><span data-stu-id="69dcc-131">Next steps</span></span> 
* [<span data-ttu-id="69dcc-132">Publish applications using your own domain name</span><span class="sxs-lookup"><span data-stu-id="69dcc-132">Publish applications using your own domain name</span></span>](active-directory-application-proxy-custom-domains.md)
* [<span data-ttu-id="69dcc-133">Enable single-sign on</span><span class="sxs-lookup"><span data-stu-id="69dcc-133">Enable single-sign on</span></span>](active-directory-application-proxy-sso-using-kcd.md)
* [<span data-ttu-id="69dcc-134">Troubleshoot issues you're having with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="69dcc-134">Troubleshoot issues you're having with Application Proxy</span></span>](active-directory-application-proxy-troubleshoot.md)


