---
title: Silent install Azure AD App Proxy connector | Microsoft Docs
description: Covers how to perform an unattended installation of Azure AD Application Proxy Connector to provide secure remote access to your on-premises apps.
services: active-directory
documentationcenter: ''
author: barbkess
manager: mtillman
ms.service: active-directory
ms.component: app-mgmt
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/17/2018
ms.author: barbkess
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 3f8ef9ea3a46dde77ac27e7105148ac886f9212d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967823"
---
# <a name="create-an-unattended-installation-script-for-the-azure-ad-application-proxy-connector"></a><span data-ttu-id="8d208-103">Create an unattended installation script for the Azure AD Application Proxy connector</span><span class="sxs-lookup"><span data-stu-id="8d208-103">Create an unattended installation script for the Azure AD Application Proxy connector</span></span>

<span data-ttu-id="8d208-104">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy connector.</span><span class="sxs-lookup"><span data-stu-id="8d208-104">This topic helps you create a Windows PowerShell script that enables unattended installation and registration for your Azure AD Application Proxy connector.</span></span>

<span data-ttu-id="8d208-105">This capability is useful when you want to:</span><span class="sxs-lookup"><span data-stu-id="8d208-105">This capability is useful when you want to:</span></span>

* <span data-ttu-id="8d208-106">Install the connector on Windows servers that don't have user interface enabled, or that you can't access with Remote Desktop.</span><span class="sxs-lookup"><span data-stu-id="8d208-106">Install the connector on Windows servers that don't have user interface enabled, or that you can't access with Remote Desktop.</span></span>
* <span data-ttu-id="8d208-107">Install and register many connectors at once.</span><span class="sxs-lookup"><span data-stu-id="8d208-107">Install and register many connectors at once.</span></span>
* <span data-ttu-id="8d208-108">Integrate the connector installation and registration as part of another procedure.</span><span class="sxs-lookup"><span data-stu-id="8d208-108">Integrate the connector installation and registration as part of another procedure.</span></span>
* <span data-ttu-id="8d208-109">Create a standard server image that contains the connector bits but is not registered.</span><span class="sxs-lookup"><span data-stu-id="8d208-109">Create a standard server image that contains the connector bits but is not registered.</span></span>

<span data-ttu-id="8d208-110">For the [Application Proxy connector](application-proxy-connectors.md) to work, it has to be registered with your Azure AD directory using a global administrator and password.</span><span class="sxs-lookup"><span data-stu-id="8d208-110">For the [Application Proxy connector](application-proxy-connectors.md) to work, it has to be registered with your Azure AD directory using a global administrator and password.</span></span> <span data-ttu-id="8d208-111">Ordinarily this information is entered during Connector installation in a pop-up dialog box, but you can use PowerShell to automate this process instead.</span><span class="sxs-lookup"><span data-stu-id="8d208-111">Ordinarily this information is entered during Connector installation in a pop-up dialog box, but you can use PowerShell to automate this process instead.</span></span>

<span data-ttu-id="8d208-112">There are two steps for an unattended installation.</span><span class="sxs-lookup"><span data-stu-id="8d208-112">There are two steps for an unattended installation.</span></span> <span data-ttu-id="8d208-113">First, install the connector.</span><span class="sxs-lookup"><span data-stu-id="8d208-113">First, install the connector.</span></span> <span data-ttu-id="8d208-114">Second, register the connector with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8d208-114">Second, register the connector with Azure AD.</span></span> 

## <a name="install-the-connector"></a><span data-ttu-id="8d208-115">Install the connector</span><span class="sxs-lookup"><span data-stu-id="8d208-115">Install the connector</span></span>
<span data-ttu-id="8d208-116">Use the following steps to install the connector without registering it:</span><span class="sxs-lookup"><span data-stu-id="8d208-116">Use the following steps to install the connector without registering it:</span></span>

1. <span data-ttu-id="8d208-117">Open a command prompt.</span><span class="sxs-lookup"><span data-stu-id="8d208-117">Open a command prompt.</span></span>
2. <span data-ttu-id="8d208-118">Run the following command, in which the /q means quiet installation.</span><span class="sxs-lookup"><span data-stu-id="8d208-118">Run the following command, in which the /q means quiet installation.</span></span> <span data-ttu-id="8d208-119">A quiet installation doesn't prompt you to accept the End-User License Agreement.</span><span class="sxs-lookup"><span data-stu-id="8d208-119">A quiet installation doesn't prompt you to accept the End-User License Agreement.</span></span>
   
        AADApplicationProxyConnectorInstaller.exe REGISTERCONNECTOR="false" /q

## <a name="register-the-connector-with-azure-ad"></a><span data-ttu-id="8d208-120">Register the connector with Azure AD</span><span class="sxs-lookup"><span data-stu-id="8d208-120">Register the connector with Azure AD</span></span>
<span data-ttu-id="8d208-121">There are two methods you can use to register the connector:</span><span class="sxs-lookup"><span data-stu-id="8d208-121">There are two methods you can use to register the connector:</span></span>

* <span data-ttu-id="8d208-122">Register the connector using a Windows PowerShell credential object</span><span class="sxs-lookup"><span data-stu-id="8d208-122">Register the connector using a Windows PowerShell credential object</span></span>
* <span data-ttu-id="8d208-123">Register the connector using a token created offline</span><span class="sxs-lookup"><span data-stu-id="8d208-123">Register the connector using a token created offline</span></span>

### <a name="register-the-connector-using-a-windows-powershell-credential-object"></a><span data-ttu-id="8d208-124">Register the connector using a Windows PowerShell credential object</span><span class="sxs-lookup"><span data-stu-id="8d208-124">Register the connector using a Windows PowerShell credential object</span></span>
1. <span data-ttu-id="8d208-125">Create a Windows PowerShell Credentials object `$cred` that contains an administrative username and password for your directory.</span><span class="sxs-lookup"><span data-stu-id="8d208-125">Create a Windows PowerShell Credentials object `$cred` that contains an administrative username and password for your directory.</span></span> <span data-ttu-id="8d208-126">Run the following command, replacing *\<username\>* and *\<password\>*:</span><span class="sxs-lookup"><span data-stu-id="8d208-126">Run the following command, replacing *\<username\>* and *\<password\>*:</span></span>
   
        $User = "<username>"
        $PlainPassword = '<password>'
        $SecurePassword = $PlainPassword | ConvertTo-SecureString -AsPlainText -Force
        $cred = New-Object –TypeName System.Management.Automation.PSCredential –ArgumentList $User, $SecurePassword
2. <span data-ttu-id="8d208-127">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the following script using the `$cred` object that you created:</span><span class="sxs-lookup"><span data-stu-id="8d208-127">Go to **C:\Program Files\Microsoft AAD App Proxy Connector** and run the following script using the `$cred` object that you created:</span></span>
   
        .\RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Credentials -Usercredentials $cred -Feature ApplicationProxy

### <a name="register-the-connector-using-a-token-created-offline"></a><span data-ttu-id="8d208-128">Register the connector using a token created offline</span><span class="sxs-lookup"><span data-stu-id="8d208-128">Register the connector using a token created offline</span></span>
1. <span data-ttu-id="8d208-129">Create an offline token using the AuthenticationContext class using the values in this code snippet or PowerShell cmdlets below:</span><span class="sxs-lookup"><span data-stu-id="8d208-129">Create an offline token using the AuthenticationContext class using the values in this code snippet or PowerShell cmdlets below:</span></span>

    <span data-ttu-id="8d208-130">**Using C#:**</span><span class="sxs-lookup"><span data-stu-id="8d208-130">**Using C#:**</span></span>

        using System;
        using System.Diagnostics;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

        class Program
        {
        #region constants
        /// <summary>
        /// The AAD authentication endpoint uri
        /// </summary>
        static readonly Uri AadAuthenticationEndpoint = new Uri("https://login.microsoftonline.com/common/oauth2/token?api-version=1.0");

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

    <span data-ttu-id="8d208-131">**Using PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="8d208-131">**Using PowerShell:**</span></span>

        # Locate AzureAD PowerShell Module
        # Change Name of Module to AzureAD after what you have installed
        $AADPoshPath = (Get-InstalledModule -Name AzureAD).InstalledLocation
        # Set Location for ADAL Helper Library
        $ADALPath = $(Get-ChildItem -Path $($AADPoshPath) -Filter Microsoft.IdentityModel.Clients.ActiveDirectory.dll -Recurse ).FullName | Select-Object -Last 1
        
        # Add ADAL Helper Library
        Add-Type -Path $ADALPath
        
        #region constants
        
        # The AAD authentication endpoint uri
        [uri]$AadAuthenticationEndpoint = "https://login.microsoftonline.com/common/oauth2/token?api-version=1.0/" 
        
        # The application ID of the connector in AAD
        [string]$ConnectorAppId = "55747057-9b5d-4bd4-b387-abf52a8bd489"
        
        # The reply address of the connector application in AAD
        [uri]$ConnectorRedirectAddress = "urn:ietf:wg:oauth:2.0:oob" 
        
        # The AppIdUri of the registration service in AAD
        [uri]$RegistrationServiceAppIdUri = "https://proxy.cloudwebappproxy.net/registerapp"
        
        #endregion
        
        #region GetAuthenticationToken
        
        # Set AuthN context
        $authContext = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext" -ArgumentList $AadAuthenticationEndpoint
        
        # Build platform parameters
        $promptBehavior = [Microsoft.IdentityModel.Clients.ActiveDirectory.PromptBehavior]::Always
        $platformParam = New-Object "Microsoft.IdentityModel.Clients.ActiveDirectory.PlatformParameters" -ArgumentList $promptBehavior
        
        # Do AuthN and get token
        $authResult = $authContext.AcquireTokenAsync($RegistrationServiceAppIdUri.AbsoluteUri, $ConnectorAppId, $ConnectorRedirectAddress, $platformParam).Result
        
        # Check AuthN result
        If (($authResult) -and ($authResult.AccessToken) -and ($authResult.TenantId) ) {
        $token = $authResult.AccessToken
        $tenantId = $authResult.TenantId
        }
        Else {
        Write-Output "Authentication result, token or tenant id returned are null"
        }
        
        #endregion

2. <span data-ttu-id="8d208-132">Once you have the token, create a SecureString using the token:</span><span class="sxs-lookup"><span data-stu-id="8d208-132">Once you have the token, create a SecureString using the token:</span></span>

   `$SecureToken = $Token | ConvertTo-SecureString -AsPlainText -Force`

3. <span data-ttu-id="8d208-133">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span><span class="sxs-lookup"><span data-stu-id="8d208-133">Run the following Windows PowerShell command, replacing \<tenant GUID\> with your directory ID:</span></span>

   `.\RegisterConnector.ps1 -modulePath "C:\Program Files\Microsoft AAD App Proxy Connector\Modules\" -moduleName "AppProxyPSModule" -Authenticationmode Token -Token $SecureToken -TenantId <tenant GUID> -Feature ApplicationProxy`

## <a name="next-steps"></a><span data-ttu-id="8d208-134">Next steps</span><span class="sxs-lookup"><span data-stu-id="8d208-134">Next steps</span></span> 
* [<span data-ttu-id="8d208-135">Publish applications using your own domain name</span><span class="sxs-lookup"><span data-stu-id="8d208-135">Publish applications using your own domain name</span></span>](application-proxy-configure-custom-domain.md)
* [<span data-ttu-id="8d208-136">Enable single-sign on</span><span class="sxs-lookup"><span data-stu-id="8d208-136">Enable single-sign on</span></span>](application-proxy-configure-single-sign-on-with-kcd.md)
* [<span data-ttu-id="8d208-137">Troubleshoot issues you're having with Application Proxy</span><span class="sxs-lookup"><span data-stu-id="8d208-137">Troubleshoot issues you're having with Application Proxy</span></span>](application-proxy-troubleshoot.md)


