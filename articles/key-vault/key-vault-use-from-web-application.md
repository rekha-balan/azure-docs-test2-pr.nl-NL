---
title: Use Azure Key Vault from a Web Application | Microsoft Docs
description: Use this tutorial to help you learn how to use Azure Key Vault from a web application.
services: key-vault
documentationcenter: ''
author: adhurwit
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: adhurwit
ms.openlocfilehash: b670d66fcc61ae249fc7ccfe97bda793c3dc9552
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540637"
---
# <a name="use-azure-key-vault-from-a-web-application"></a><span data-ttu-id="9697d-103">Use Azure Key Vault from a Web Application</span><span class="sxs-lookup"><span data-stu-id="9697d-103">Use Azure Key Vault from a Web Application</span></span>
## <a name="introduction"></a><span data-ttu-id="9697d-104">Introduction</span><span class="sxs-lookup"><span data-stu-id="9697d-104">Introduction</span></span>
<span data-ttu-id="9697d-105">Use this tutorial to help you learn how to use Azure Key Vault from a web application in Azure.</span><span class="sxs-lookup"><span data-stu-id="9697d-105">Use this tutorial to help you learn how to use Azure Key Vault from a web application in Azure.</span></span> <span data-ttu-id="9697d-106">It walks you through the process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span><span class="sxs-lookup"><span data-stu-id="9697d-106">It walks you through the process of accessing a secret from an Azure Key Vault so that it can be used in your web application.</span></span>

<span data-ttu-id="9697d-107">**Estimated time to complete:** 15 minutes</span><span class="sxs-lookup"><span data-stu-id="9697d-107">**Estimated time to complete:** 15 minutes</span></span>

<span data-ttu-id="9697d-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="9697d-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](key-vault-whatis.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9697d-109">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9697d-109">Prerequisites</span></span>
<span data-ttu-id="9697d-110">To complete this tutorial, you must have the following:</span><span class="sxs-lookup"><span data-stu-id="9697d-110">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="9697d-111">A URI to a secret in an Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9697d-111">A URI to a secret in an Azure Key Vault</span></span>
* <span data-ttu-id="9697d-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access to your Key Vault</span><span class="sxs-lookup"><span data-stu-id="9697d-112">A Client ID and a Client Secret for a web application registered with Azure Active Directory that has access to your Key Vault</span></span>
* <span data-ttu-id="9697d-113">A web application.</span><span class="sxs-lookup"><span data-stu-id="9697d-113">A web application.</span></span> <span data-ttu-id="9697d-114">We will be showing the steps for an ASP.NET MVC application deployed in Azure as a Web App.</span><span class="sxs-lookup"><span data-stu-id="9697d-114">We will be showing the steps for an ASP.NET MVC application deployed in Azure as a Web App.</span></span>

> [!NOTE]
> <span data-ttu-id="9697d-115">It is essential that you have completed the steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have the URI to a secret and the Client ID and Client Secret for a web application.</span><span class="sxs-lookup"><span data-stu-id="9697d-115">It is essential that you have completed the steps listed in [Get Started with Azure Key Vault](key-vault-get-started.md) for this tutorial so that you have the URI to a secret and the Client ID and Client Secret for a web application.</span></span>
> 
> 

<span data-ttu-id="9697d-116">The web application that will be accessing the Key Vault is the one that is registered in Azure Active Directory and has been given access to your Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9697d-116">The web application that will be accessing the Key Vault is the one that is registered in Azure Active Directory and has been given access to your Key Vault.</span></span> <span data-ttu-id="9697d-117">If this is not the case, go back to Register an Application in the Get Started tutorial and repeat the steps listed.</span><span class="sxs-lookup"><span data-stu-id="9697d-117">If this is not the case, go back to Register an Application in the Get Started tutorial and repeat the steps listed.</span></span>

<span data-ttu-id="9697d-118">This tutorial is designed for web developers that understand the basics of creating web applications on Azure.</span><span class="sxs-lookup"><span data-stu-id="9697d-118">This tutorial is designed for web developers that understand the basics of creating web applications on Azure.</span></span> <span data-ttu-id="9697d-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="9697d-119">For more information about Azure Web Apps, see [Web Apps overview](../app-service-web/app-service-web-overview.md).</span></span>

## <a id="packages"></a><span data-ttu-id="9697d-120">Add Nuget Packages</span><span class="sxs-lookup"><span data-stu-id="9697d-120">Add Nuget Packages</span></span>
<span data-ttu-id="9697d-121">There are two packages that your web application needs to have installed.</span><span class="sxs-lookup"><span data-stu-id="9697d-121">There are two packages that your web application needs to have installed.</span></span>

* <span data-ttu-id="9697d-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span><span class="sxs-lookup"><span data-stu-id="9697d-122">Active Directory Authentication Library - contains methods for interacting with Azure Active Directory and managing user identity</span></span>
* <span data-ttu-id="9697d-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span><span class="sxs-lookup"><span data-stu-id="9697d-123">Azure Key Vault Library - contains methods for interacting with Azure Key Vault</span></span>

<span data-ttu-id="9697d-124">Both of these packages can be installed using the Package Manager Console using the Install-Package command.</span><span class="sxs-lookup"><span data-stu-id="9697d-124">Both of these packages can be installed using the Package Manager Console using the Install-Package command.</span></span>

    // this is currently the latest stable version of ADAL
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

    Install-Package Microsoft.Azure.KeyVault


## <a id="webconfig"></a><span data-ttu-id="9697d-125">Modify Web.Config</span><span class="sxs-lookup"><span data-stu-id="9697d-125">Modify Web.Config</span></span>
<span data-ttu-id="9697d-126">There are three application settings that need to be added to the web.config file as follows.</span><span class="sxs-lookup"><span data-stu-id="9697d-126">There are three application settings that need to be added to the web.config file as follows.</span></span>

    <!-- ClientId and ClientSecret refer to the web application registration with Azure Active Directory -->
    <add key="ClientId" value="clientid" />
    <add key="ClientSecret" value="clientsecret" />

    <!-- SecretUri is the URI for the secret in Azure Key Vault -->
    <add key="SecretUri" value="secreturi" />


<span data-ttu-id="9697d-127">If you are not going to host your application as an Azure Web App, then you should add the actual ClientId, Client Secret, and Secret URI values to the web.config. Otherwise leave these dummy values because we will be adding the actual values in the Azure Portal for an additional level of security.</span><span class="sxs-lookup"><span data-stu-id="9697d-127">If you are not going to host your application as an Azure Web App, then you should add the actual ClientId, Client Secret, and Secret URI values to the web.config. Otherwise leave these dummy values because we will be adding the actual values in the Azure Portal for an additional level of security.</span></span>

## <a id="gettoken"></a><span data-ttu-id="9697d-128">Add Method to Get an Access Token</span><span class="sxs-lookup"><span data-stu-id="9697d-128">Add Method to Get an Access Token</span></span>
<span data-ttu-id="9697d-129">In order to use the Key Vault API you need an access token.</span><span class="sxs-lookup"><span data-stu-id="9697d-129">In order to use the Key Vault API you need an access token.</span></span> <span data-ttu-id="9697d-130">The Key Vault Client handles calls to the Key Vault API but you need to supply it with a function that gets the access token.</span><span class="sxs-lookup"><span data-stu-id="9697d-130">The Key Vault Client handles calls to the Key Vault API but you need to supply it with a function that gets the access token.</span></span>  

<span data-ttu-id="9697d-131">Following is the code to get an access token from Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9697d-131">Following is the code to get an access token from Azure Active Directory.</span></span> <span data-ttu-id="9697d-132">This code can go anywhere in your application.</span><span class="sxs-lookup"><span data-stu-id="9697d-132">This code can go anywhere in your application.</span></span> <span data-ttu-id="9697d-133">I like to add a Utils or EncryptionHelper class.</span><span class="sxs-lookup"><span data-stu-id="9697d-133">I like to add a Utils or EncryptionHelper class.</span></span>  

    //add these using statements
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using System.Threading.Tasks;
    using System.Web.Configuration;

    //this is an optional property to hold the secret after it is retrieved
    public static string EncryptSecret { get; set; }

    //the method that will be provided to the KeyVaultClient
    public static async Task<string> GetToken(string authority, string resource, string scope)
    {
        var authContext = new AuthenticationContext(authority);
        ClientCredential clientCred = new ClientCredential(WebConfigurationManager.AppSettings["ClientId"],
                    WebConfigurationManager.AppSettings["ClientSecret"]);
        AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

        if (result == null)
            throw new InvalidOperationException("Failed to obtain the JWT token");

        return result.AccessToken;
    }

> [!NOTE]
> <span data-ttu-id="9697d-134">Using a Client ID and Client Secret is the easiest way to authenticate an Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="9697d-134">Using a Client ID and Client Secret is the easiest way to authenticate an Azure AD application.</span></span> <span data-ttu-id="9697d-135">And using it in your web application allows for a separation of duties and more control over your key management.</span><span class="sxs-lookup"><span data-stu-id="9697d-135">And using it in your web application allows for a separation of duties and more control over your key management.</span></span> <span data-ttu-id="9697d-136">But it does rely on putting the Client Secret in your configuration settings which for some can be as risky as putting the secret that you want to protect in your configuration settings.</span><span class="sxs-lookup"><span data-stu-id="9697d-136">But it does rely on putting the Client Secret in your configuration settings which for some can be as risky as putting the secret that you want to protect in your configuration settings.</span></span> <span data-ttu-id="9697d-137">See below for a discussion on how to use a Client ID and Certificate instead of Client ID and Client Secret to authenticate the Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="9697d-137">See below for a discussion on how to use a Client ID and Certificate instead of Client ID and Client Secret to authenticate the Azure AD application.</span></span>
> 
> 

## <a id="appstart"></a><span data-ttu-id="9697d-138">Retrieve the secret on Application Start</span><span class="sxs-lookup"><span data-stu-id="9697d-138">Retrieve the secret on Application Start</span></span>
<span data-ttu-id="9697d-139">Now we need code to call the Key Vault API and retrieve the secret.</span><span class="sxs-lookup"><span data-stu-id="9697d-139">Now we need code to call the Key Vault API and retrieve the secret.</span></span> <span data-ttu-id="9697d-140">The following code can be put anywhere as long as it is called before you need to use it.</span><span class="sxs-lookup"><span data-stu-id="9697d-140">The following code can be put anywhere as long as it is called before you need to use it.</span></span> <span data-ttu-id="9697d-141">I have put this code in the Application Start event in the Global.asax so that it runs once on start and makes the secret available for the application.</span><span class="sxs-lookup"><span data-stu-id="9697d-141">I have put this code in the Application Start event in the Global.asax so that it runs once on start and makes the secret available for the application.</span></span>

    //add these using statements
    using Microsoft.Azure.KeyVault;
    using System.Web.Configuration;

    // I put my GetToken method in a Utils class. Change for wherever you placed your method.
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

    var sec = await kv.GetSecretAsync(WebConfigurationManager.AppSettings["SecretUri"]);

    //I put a variable in a Utils class to hold the secret for general  application use.
    Utils.EncryptSecret = sec.Value;



## <a id="portalsettings"></a><span data-ttu-id="9697d-142">Add App Settings in the Azure Portal (optional)</span><span class="sxs-lookup"><span data-stu-id="9697d-142">Add App Settings in the Azure Portal (optional)</span></span>
<span data-ttu-id="9697d-143">If you have an Azure Web App you can now add the actual values for the AppSettings in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="9697d-143">If you have an Azure Web App you can now add the actual values for the AppSettings in the Azure Portal.</span></span> <span data-ttu-id="9697d-144">By doing this, the actual values will not be in the web.config but protected via the Portal where you have separate access control capabilities.</span><span class="sxs-lookup"><span data-stu-id="9697d-144">By doing this, the actual values will not be in the web.config but protected via the Portal where you have separate access control capabilities.</span></span> <span data-ttu-id="9697d-145">These values will be substituted for the values that you entered in your web.config. Make sure that the names are the same.</span><span class="sxs-lookup"><span data-stu-id="9697d-145">These values will be substituted for the values that you entered in your web.config. Make sure that the names are the same.</span></span>

![Application Settings displayed in Azure Portal][1]

## <a name="authenticate-with-a-certificate-instead-of-a-client-secret"></a><span data-ttu-id="9697d-147">Authenticate with a Certificate instead of a Client Secret</span><span class="sxs-lookup"><span data-stu-id="9697d-147">Authenticate with a Certificate instead of a Client Secret</span></span>
<span data-ttu-id="9697d-148">Another way to authenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span><span class="sxs-lookup"><span data-stu-id="9697d-148">Another way to authenticate an Azure AD application is by using a Client ID and a Certificate instead of a Client ID and Client Secret.</span></span> <span data-ttu-id="9697d-149">Following are the steps to use a Certificate in an Azure Web App:</span><span class="sxs-lookup"><span data-stu-id="9697d-149">Following are the steps to use a Certificate in an Azure Web App:</span></span>

1. <span data-ttu-id="9697d-150">Get or Create a Certificate</span><span class="sxs-lookup"><span data-stu-id="9697d-150">Get or Create a Certificate</span></span>
2. <span data-ttu-id="9697d-151">Associate the Certificate with an Azure AD application</span><span class="sxs-lookup"><span data-stu-id="9697d-151">Associate the Certificate with an Azure AD application</span></span>
3. <span data-ttu-id="9697d-152">Add code to your Web App to use the Certificate</span><span class="sxs-lookup"><span data-stu-id="9697d-152">Add code to your Web App to use the Certificate</span></span>
4. <span data-ttu-id="9697d-153">Add a Certificate to your Web App</span><span class="sxs-lookup"><span data-stu-id="9697d-153">Add a Certificate to your Web App</span></span>

<span data-ttu-id="9697d-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span><span class="sxs-lookup"><span data-stu-id="9697d-154">**Get or Create a Certificate** For our purposes we will make a test certificate.</span></span> <span data-ttu-id="9697d-155">Here are a couple of commands that you can use in a Developer Command Prompt to create a certificate.</span><span class="sxs-lookup"><span data-stu-id="9697d-155">Here are a couple of commands that you can use in a Developer Command Prompt to create a certificate.</span></span> <span data-ttu-id="9697d-156">Change directory to where you want the cert files created.</span><span class="sxs-lookup"><span data-stu-id="9697d-156">Change directory to where you want the cert files created.</span></span>  <span data-ttu-id="9697d-157">Also, for the beginning and ending date of the certificate, use the current date plus 1 year.</span><span class="sxs-lookup"><span data-stu-id="9697d-157">Also, for the beginning and ending date of the certificate, use the current date plus 1 year.</span></span>
<span data-ttu-id="9697d-158">makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123</span><span class="sxs-lookup"><span data-stu-id="9697d-158">makecert -sv mykey.pvk -n "cn=KVWebApp" KVWebApp.cer -b 03/07/2017 -e 03/07/2018 -r pvk2pfx -pvk mykey.pvk -spc KVWebApp.cer -pfx KVWebApp.pfx -po test123</span></span>

<span data-ttu-id="9697d-159">Make note of the end date and the password for the .pfx (in this example: 07/31/2016 and test123).</span><span class="sxs-lookup"><span data-stu-id="9697d-159">Make note of the end date and the password for the .pfx (in this example: 07/31/2016 and test123).</span></span> <span data-ttu-id="9697d-160">You will need them below.</span><span class="sxs-lookup"><span data-stu-id="9697d-160">You will need them below.</span></span>

<span data-ttu-id="9697d-161">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span><span class="sxs-lookup"><span data-stu-id="9697d-161">For more information on creating a test certificate, see [How to: Create Your Own Test Certificate](https://msdn.microsoft.com/library/ff699202.aspx)</span></span>

<span data-ttu-id="9697d-162">**Associate the Certificate with an Azure AD application** Now that you have a certificate, you need to associate it with an Azure AD application.</span><span class="sxs-lookup"><span data-stu-id="9697d-162">**Associate the Certificate with an Azure AD application** Now that you have a certificate, you need to associate it with an Azure AD application.</span></span> <span data-ttu-id="9697d-163">Presently, the Azure Portal does not support this worklfow; this can be completed through PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9697d-163">Presently, the Azure Portal does not support this worklfow; this can be completed through PowerShell.</span></span> <span data-ttu-id="9697d-164">Run the following commands to assoicate the certificate with the Azure AD application:</span><span class="sxs-lookup"><span data-stu-id="9697d-164">Run the following commands to assoicate the certificate with the Azure AD application:</span></span>

    $x509 = New-Object System.Security.Cryptography.X509Certificates.X509Certificate2
    $x509.Import("C:\data\KVWebApp.cer")
    $credValue = [System.Convert]::ToBase64String($x509.GetRawCertData())

    # If you used different dates for makecert then adjust these values
    $now = [System.DateTime]::Now
    $yearfromnow = $now.AddYears(1)

    $adapp = New-AzureRmADApplication -DisplayName "KVWebApp" -HomePage "http://kvwebapp" -IdentifierUris "http://kvwebapp" -CertValue $credValue -StartDate $now -EndDate $yearfromnow

    $sp = New-AzureRmADServicePrincipal -ApplicationId $adapp.ApplicationId

    Set-AzureRmKeyVaultAccessPolicy -VaultName 'contosokv' -ServicePrincipalName $sp.ServicePrincipalName -PermissionsToSecrets all -ResourceGroupName 'contosorg'

    # get the thumbprint to use in your app settings
    $x509.Thumbprint

<span data-ttu-id="9697d-165">After you have run these commands, you can see the application in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9697d-165">After you have run these commands, you can see the application in Azure AD.</span></span> <span data-ttu-id="9697d-166">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in the search dialog.</span><span class="sxs-lookup"><span data-stu-id="9697d-166">When searching, ensure you select "Applications my company owns" instead of "Applications my company uses" in the search dialog.</span></span>

<span data-ttu-id="9697d-167">To learn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span><span class="sxs-lookup"><span data-stu-id="9697d-167">To learn more about Azure AD Application Objects and ServicePrincipal Objects, see [Application Objects and Service Principal Objects](../active-directory/active-directory-application-objects.md)</span></span>

<span data-ttu-id="9697d-168">**Add code to your Web App to use the Certificate** Now we will add code to your Web App to access the cert and use it for authentication.</span><span class="sxs-lookup"><span data-stu-id="9697d-168">**Add code to your Web App to use the Certificate** Now we will add code to your Web App to access the cert and use it for authentication.</span></span>

<span data-ttu-id="9697d-169">First there is code to access the cert.</span><span class="sxs-lookup"><span data-stu-id="9697d-169">First there is code to access the cert.</span></span>

    public static class CertificateHelper
    {
        public static X509Certificate2 FindCertificateByThumbprint(string findValue)
        {
            X509Store store = new X509Store(StoreName.My, StoreLocation.CurrentUser);
            try
            {
                store.Open(OpenFlags.ReadOnly);
                X509Certificate2Collection col = store.Certificates.Find(X509FindType.FindByThumbprint,
                    findValue, false); // Don't validate certs, since the test root isn't installed.
                if (col == null || col.Count == 0)
                    return null;
                return col[0];
            }
            finally
            {
                store.Close();
            }
        }
    }


<span data-ttu-id="9697d-170">Note that the StoreLocation is CurrentUser instead of LocalMachine.</span><span class="sxs-lookup"><span data-stu-id="9697d-170">Note that the StoreLocation is CurrentUser instead of LocalMachine.</span></span> <span data-ttu-id="9697d-171">And that we are supplying 'false' to the Find method because we are using a test cert.</span><span class="sxs-lookup"><span data-stu-id="9697d-171">And that we are supplying 'false' to the Find method because we are using a test cert.</span></span>

<span data-ttu-id="9697d-172">Next is code that uses the CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span><span class="sxs-lookup"><span data-stu-id="9697d-172">Next is code that uses the CertificateHelper and creates a ClientAssertionCertificate which is needed for authentication.</span></span>

    public static ClientAssertionCertificate AssertionCert { get; set; }

    public static void GetCert()
    {
        var clientAssertionCertPfx = CertificateHelper.FindCertificateByThumbprint(WebConfigurationManager.AppSettings["thumbprint"]);
        AssertionCert = new ClientAssertionCertificate(WebConfigurationManager.AppSettings["clientid"], clientAssertionCertPfx);
    }


<span data-ttu-id="9697d-173">Here is the new code to get the access token.</span><span class="sxs-lookup"><span data-stu-id="9697d-173">Here is the new code to get the access token.</span></span> <span data-ttu-id="9697d-174">This replaces the GetToken method above.</span><span class="sxs-lookup"><span data-stu-id="9697d-174">This replaces the GetToken method above.</span></span> <span data-ttu-id="9697d-175">I have given it a different name for convenience.</span><span class="sxs-lookup"><span data-stu-id="9697d-175">I have given it a different name for convenience.</span></span>

    public static async Task<string> GetAccessToken(string authority, string resource, string scope)
    {
        var context = new AuthenticationContext(authority, TokenCache.DefaultShared);
        var result = await context.AcquireTokenAsync(resource, AssertionCert);
        return result.AccessToken;
    }

<span data-ttu-id="9697d-176">I have put all of this code into my Web App project's Utils class for ease of use.</span><span class="sxs-lookup"><span data-stu-id="9697d-176">I have put all of this code into my Web App project's Utils class for ease of use.</span></span>

<span data-ttu-id="9697d-177">The last code change is in the Application_Start method.</span><span class="sxs-lookup"><span data-stu-id="9697d-177">The last code change is in the Application_Start method.</span></span> <span data-ttu-id="9697d-178">First we need to call the GetCert() method to load the ClientAssertionCertificate.</span><span class="sxs-lookup"><span data-stu-id="9697d-178">First we need to call the GetCert() method to load the ClientAssertionCertificate.</span></span> <span data-ttu-id="9697d-179">And then we change the callback method that we supply when creating a new KeyVaultClient.</span><span class="sxs-lookup"><span data-stu-id="9697d-179">And then we change the callback method that we supply when creating a new KeyVaultClient.</span></span> <span data-ttu-id="9697d-180">Note that this replaces the code that we had above.</span><span class="sxs-lookup"><span data-stu-id="9697d-180">Note that this replaces the code that we had above.</span></span>

    Utils.GetCert();
    var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetAccessToken));


<span data-ttu-id="9697d-181">**Add a Certificate to your Web App through the Azure Portal** Adding a Certificate to your Web App is a simple two-step process.</span><span class="sxs-lookup"><span data-stu-id="9697d-181">**Add a Certificate to your Web App through the Azure Portal** Adding a Certificate to your Web App is a simple two-step process.</span></span> <span data-ttu-id="9697d-182">First, go to the Azure Portal and navigate to your Web App.</span><span class="sxs-lookup"><span data-stu-id="9697d-182">First, go to the Azure Portal and navigate to your Web App.</span></span> <span data-ttu-id="9697d-183">On the Settings blade for your Web App, click on the entry for "Custom domains and SSL".</span><span class="sxs-lookup"><span data-stu-id="9697d-183">On the Settings blade for your Web App, click on the entry for "Custom domains and SSL".</span></span> <span data-ttu-id="9697d-184">On the blade that opens you will be able to upload the Certificate that you created above, KVWebApp.pfx, make sure that you remember the password for the pfx.</span><span class="sxs-lookup"><span data-stu-id="9697d-184">On the blade that opens you will be able to upload the Certificate that you created above, KVWebApp.pfx, make sure that you remember the password for the pfx.</span></span>

![Adding a Certificate to a Web App in the Azure Portal][2]

<span data-ttu-id="9697d-186">The last thing that you need to do is to add an Application Setting to your Web App that has the name WEBSITE\_LOAD\_CERTIFICATES and a value of \*.</span><span class="sxs-lookup"><span data-stu-id="9697d-186">The last thing that you need to do is to add an Application Setting to your Web App that has the name WEBSITE\_LOAD\_CERTIFICATES and a value of \*.</span></span> <span data-ttu-id="9697d-187">This will ensure that all Certificates are loaded.</span><span class="sxs-lookup"><span data-stu-id="9697d-187">This will ensure that all Certificates are loaded.</span></span> <span data-ttu-id="9697d-188">If you wanted to load only the Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span><span class="sxs-lookup"><span data-stu-id="9697d-188">If you wanted to load only the Certificates that you have uploaded, then you can enter a comma-separated list of their thumbprints.</span></span>

<span data-ttu-id="9697d-189">To learn more about adding a Certificate to a Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span><span class="sxs-lookup"><span data-stu-id="9697d-189">To learn more about adding a Certificate to a Web App, see [Using Certificates in Azure Websites Applications](https://azure.microsoft.com/blog/2014/10/27/using-certificates-in-azure-websites-applications/)</span></span>

<span data-ttu-id="9697d-190">**Add a Certificate to Key Vault as a secret** Instead of uploading your certificate to the Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span><span class="sxs-lookup"><span data-stu-id="9697d-190">**Add a Certificate to Key Vault as a secret** Instead of uploading your certificate to the Web App service directly, you can store it in Key Vault as a secret and deploy it from there.</span></span> <span data-ttu-id="9697d-191">This is a two-step process that is outlined in the following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span><span class="sxs-lookup"><span data-stu-id="9697d-191">This is a two-step process that is outlined in the following blog post, [Deploying Azure Web App Certificate through Key Vault](https://blogs.msdn.microsoft.com/appserviceteam/2016/05/24/deploying-azure-web-app-certificate-through-key-vault/)</span></span>

## <a id="next"></a><span data-ttu-id="9697d-192">Next steps</span><span class="sxs-lookup"><span data-stu-id="9697d-192">Next steps</span></span>
<span data-ttu-id="9697d-193">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span><span class="sxs-lookup"><span data-stu-id="9697d-193">For programming references, see [Azure Key Vault C# Client API Reference](https://msdn.microsoft.com/library/azure/dn903628.aspx).</span></span>

<!--Image references-->
[1]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/key-vault-use-from-web-application/PortalAppSettings.png
[2]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/key-vault/media/key-vault-use-from-web-application/PortalAddCertificate.png


