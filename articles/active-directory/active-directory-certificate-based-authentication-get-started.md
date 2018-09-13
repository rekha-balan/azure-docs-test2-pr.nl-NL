---
title: Azure Active Directory certificate-based authentication - Get started  | Microsoft Docs
description: Learn how to configure certificate-based authentication in your environment
author: MarkusVi
documentationcenter: na
manager: femila
ms.assetid: c6ad7640-8172-4541-9255-770f39ecce0e
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 02/09/2017
ms.author: markvi
ms.openlocfilehash: d818cd3a243fb78228706b21a002f295782189be
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552610"
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="ecfb9-103">Get started with certificate-based authentication in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ecfb9-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="ecfb9-104">Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-104">Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to:</span></span> 

- <span data-ttu-id="ecfb9-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="ecfb9-105">Office mobile applications such as Microsoft Outlook and Microsoft Word</span></span>   

- <span data-ttu-id="ecfb9-106">Exchange ActiveSync (EAS) clients</span><span class="sxs-lookup"><span data-stu-id="ecfb9-106">Exchange ActiveSync (EAS) clients</span></span> 

<span data-ttu-id="ecfb9-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span> 

<span data-ttu-id="ecfb9-108">This topic:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-108">This topic:</span></span>

- <span data-ttu-id="ecfb9-109">Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-109">Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="ecfb9-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span> 

- <span data-ttu-id="ecfb9-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>    


## <a name="requirements"></a><span data-ttu-id="ecfb9-112">Requirements</span><span class="sxs-lookup"><span data-stu-id="ecfb9-112">Requirements</span></span>

<span data-ttu-id="ecfb9-113">To configure certificate-based authentication, the following must be true:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-113">To configure certificate-based authentication, the following must be true:</span></span>  

- <span data-ttu-id="ecfb9-114">The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-114">The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>  

- <span data-ttu-id="ecfb9-115">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-115">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>  

- <span data-ttu-id="ecfb9-116">You must have at least one certificate authority configured in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-116">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="ecfb9-117">You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-117">You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>  

- <span data-ttu-id="ecfb9-118">For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-118">For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field.</span></span> <span data-ttu-id="ecfb9-119">Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-119">Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.</span></span>  

- <span data-ttu-id="ecfb9-120">Your client device must have access to at least one certificate authority that issues client certificates.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-120">Your client device must have access to at least one certificate authority that issues client certificates.</span></span>  

- <span data-ttu-id="ecfb9-121">A client certificate for client authentication must have been issued to your client.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-121">A client certificate for client authentication must have been issued to your client.</span></span>  




## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="ecfb9-122">Step 1: Select your device platform</span><span class="sxs-lookup"><span data-stu-id="ecfb9-122">Step 1: Select your device platform</span></span>

<span data-ttu-id="ecfb9-123">As a first step, for the device platform you care about, you need to review the following:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-123">As a first step, for the device platform you care about, you need to review the following:</span></span>

- <span data-ttu-id="ecfb9-124">The Office mobile applications support</span><span class="sxs-lookup"><span data-stu-id="ecfb9-124">The Office mobile applications support</span></span> 
- <span data-ttu-id="ecfb9-125">The specific implementation requirements</span><span class="sxs-lookup"><span data-stu-id="ecfb9-125">The specific implementation requirements</span></span>  

<span data-ttu-id="ecfb9-126">The related information exists for the following device platforms:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-126">The related information exists for the following device platforms:</span></span>

- [<span data-ttu-id="ecfb9-127">Android</span><span class="sxs-lookup"><span data-stu-id="ecfb9-127">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="ecfb9-128">iOS</span><span class="sxs-lookup"><span data-stu-id="ecfb9-128">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-the-certificate-authorities"></a><span data-ttu-id="ecfb9-129">Step 2: Configure the certificate authorities</span><span class="sxs-lookup"><span data-stu-id="ecfb9-129">Step 2: Configure the certificate authorities</span></span> 

<span data-ttu-id="ecfb9-130">To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-130">To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following:</span></span> 

* <span data-ttu-id="ecfb9-131">The public portion of the certificate, in *.cer* format</span><span class="sxs-lookup"><span data-stu-id="ecfb9-131">The public portion of the certificate, in *.cer* format</span></span> 
* <span data-ttu-id="ecfb9-132">The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside</span><span class="sxs-lookup"><span data-stu-id="ecfb9-132">The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="ecfb9-133">The schema for a certificate authority looks as follows:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-133">The schema for a certificate authority looks as follows:</span></span> 

    class TrustedCAsForPasswordlessAuth 
    { 
       CertificateAuthorityInformation[] certificateAuthorities;    
    } 

    class CertificateAuthorityInformation 

    { 
        CertAuthorityType authorityType; 
        X509Certificate trustedCertificate; 
        string crlDistributionPoint; 
        string deltaCrlDistributionPoint; 
        string trustedIssuer; 
        string trustedIssuerSKI; 
    }                

    enum CertAuthorityType 
    { 
        RootAuthority = 0, 
        IntermediateAuthority = 1 
    } 

<span data-ttu-id="ecfb9-134">For the configuration, you can use the [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/):</span><span class="sxs-lookup"><span data-stu-id="ecfb9-134">For the configuration, you can use the [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/):</span></span>  

1. <span data-ttu-id="ecfb9-135">Start Windows PowerShell with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-135">Start Windows PowerShell with administrator privileges.</span></span> 
2. <span data-ttu-id="ecfb9-136">Install the Azure AD module.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-136">Install the Azure AD module.</span></span> <span data-ttu-id="ecfb9-137">You need to install Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-137">You need to install Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

<span data-ttu-id="ecfb9-138">As a first configuration step, you need to establish a connection with your tenant.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-138">As a first configuration step, you need to establish a connection with your tenant.</span></span> <span data-ttu-id="ecfb9-139">As soon as a connection to your tenant exists, you can review, add, delete and modify the trusted certificate authorities that are defined in your directory.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-139">As soon as a connection to your tenant exists, you can review, add, delete and modify the trusted certificate authorities that are defined in your directory.</span></span> 

### <a name="connect"></a><span data-ttu-id="ecfb9-140">Connect</span><span class="sxs-lookup"><span data-stu-id="ecfb9-140">Connect</span></span>

<span data-ttu-id="ecfb9-141">To establish a connection with your tenant, use the [Connect-AzureAD](https://docs.microsoft.com/powershell/azuread/v2/connect-azuread) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-141">To establish a connection with your tenant, use the [Connect-AzureAD](https://docs.microsoft.com/powershell/azuread/v2/connect-azuread) cmdlet:</span></span>

    Connect-AzureAD 


### <a name="retrieve"></a><span data-ttu-id="ecfb9-142">Retrieve</span><span class="sxs-lookup"><span data-stu-id="ecfb9-142">Retrieve</span></span> 

<span data-ttu-id="ecfb9-143">To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/get-azureadtrustedcertificateauthority) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-143">To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/get-azureadtrustedcertificateauthority) cmdlet.</span></span> 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a><span data-ttu-id="ecfb9-144">Add</span><span class="sxs-lookup"><span data-stu-id="ecfb9-144">Add</span></span>

<span data-ttu-id="ecfb9-145">To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/new-azureadtrustedcertificateauthority) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-145">To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/new-azureadtrustedcertificateauthority) cmdlet:</span></span> 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF THE CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a><span data-ttu-id="ecfb9-146">Remove</span><span class="sxs-lookup"><span data-stu-id="ecfb9-146">Remove</span></span>

<span data-ttu-id="ecfb9-147">To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/remove-azureadtrustedcertificateauthority) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-147">To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/remove-azureadtrustedcertificateauthority) cmdlet:</span></span>
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a><span data-ttu-id="ecfb9-148">Modfiy</span><span class="sxs-lookup"><span data-stu-id="ecfb9-148">Modfiy</span></span>

<span data-ttu-id="ecfb9-149">To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/set-azureadtrustedcertificateauthority) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-149">To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/set-azureadtrustedcertificateauthority) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a><span data-ttu-id="ecfb9-150">Step 3: Configure revocation</span><span class="sxs-lookup"><span data-stu-id="ecfb9-150">Step 3: Configure revocation</span></span>

<span data-ttu-id="ecfb9-151">To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-151">To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="ecfb9-152">The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-152">The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid.</span></span> <span data-ttu-id="ecfb9-153">The CRL is periodically referenced to revoke access to certificates that are a part of the list.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-153">The CRL is periodically referenced to revoke access to certificates that are a part of the list.</span></span>

<span data-ttu-id="ecfb9-154">If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-154">If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated.</span></span> <span data-ttu-id="ecfb9-155">To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-155">To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="ecfb9-156">You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-156">You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.</span></span>

<span data-ttu-id="ecfb9-157">To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-157">To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.</span></span>

<span data-ttu-id="ecfb9-158">The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-158">The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field.</span></span> 

<span data-ttu-id="ecfb9-159">**To configure revocation:**</span><span class="sxs-lookup"><span data-stu-id="ecfb9-159">**To configure revocation:**</span></span> 

1. <span data-ttu-id="ecfb9-160">Connect with admin credentials to the MSOL service:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-160">Connect with admin credentials to the MSOL service:</span></span> 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. <span data-ttu-id="ecfb9-161">Retrieve the current StsRefreshTokensValidFrom value for a user:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-161">Retrieve the current StsRefreshTokensValidFrom value for a user:</span></span> 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. <span data-ttu-id="ecfb9-162">Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-162">Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:</span></span> 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="ecfb9-163">The date you set must be in the future.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-163">The date you set must be in the future.</span></span> <span data-ttu-id="ecfb9-164">If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-164">If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="ecfb9-165">If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).</span><span class="sxs-lookup"><span data-stu-id="ecfb9-165">If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).</span></span> 


## <a name="step-4-test-your-configuration"></a><span data-ttu-id="ecfb9-166">Step 4: Test your configuration</span><span class="sxs-lookup"><span data-stu-id="ecfb9-166">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="ecfb9-167">Testing your certificate</span><span class="sxs-lookup"><span data-stu-id="ecfb9-167">Testing your certificate</span></span>

<span data-ttu-id="ecfb9-168">As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-168">As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="ecfb9-169">If your sign-in is successful, then you know that:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-169">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="ecfb9-170">The user certificate has been provisioned to your test device</span><span class="sxs-lookup"><span data-stu-id="ecfb9-170">The user certificate has been provisioned to your test device</span></span>
- <span data-ttu-id="ecfb9-171">AD FS is configured correctly</span><span class="sxs-lookup"><span data-stu-id="ecfb9-171">AD FS is configured correctly</span></span>  


### <a name="testing-office-mobile-applications"></a><span data-ttu-id="ecfb9-172">Testing Office mobile applications</span><span class="sxs-lookup"><span data-stu-id="ecfb9-172">Testing Office mobile applications</span></span>

<span data-ttu-id="ecfb9-173">**To test certificate-based authentication on your mobile Office application:**</span><span class="sxs-lookup"><span data-stu-id="ecfb9-173">**To test certificate-based authentication on your mobile Office application:**</span></span> 

1. <span data-ttu-id="ecfb9-174">On your test device, install an Office mobile application (e.g., OneDrive).</span><span class="sxs-lookup"><span data-stu-id="ecfb9-174">On your test device, install an Office mobile application (e.g., OneDrive).</span></span>
3. <span data-ttu-id="ecfb9-175">Launch the application.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-175">Launch the application.</span></span> 
4. <span data-ttu-id="ecfb9-176">Enter your user name, and then select the user certificate you want to use.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-176">Enter your user name, and then select the user certificate you want to use.</span></span> 

<span data-ttu-id="ecfb9-177">You should be successfully signed in.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-177">You should be successfully signed in.</span></span> 

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="ecfb9-178">Testing Exchange ActiveSync client applications</span><span class="sxs-lookup"><span data-stu-id="ecfb9-178">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="ecfb9-179">To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-179">To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.</span></span> 

<span data-ttu-id="ecfb9-180">The EAS profile must contain the following information:</span><span class="sxs-lookup"><span data-stu-id="ecfb9-180">The EAS profile must contain the following information:</span></span>

- <span data-ttu-id="ecfb9-181">The user certificate to be used for authentication</span><span class="sxs-lookup"><span data-stu-id="ecfb9-181">The user certificate to be used for authentication</span></span> 

- <span data-ttu-id="ecfb9-182">The EAS endpoint (for example, outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="ecfb9-182">The EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="ecfb9-183">An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-183">An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.</span></span>  

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="ecfb9-184">Testing EAS client applications on Android</span><span class="sxs-lookup"><span data-stu-id="ecfb9-184">Testing EAS client applications on Android</span></span>

<span data-ttu-id="ecfb9-185">**To test certificate authentication:**</span><span class="sxs-lookup"><span data-stu-id="ecfb9-185">**To test certificate authentication:**</span></span>  

1. <span data-ttu-id="ecfb9-186">Configure an EAS profile in the application that satisfies the requirements above.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-186">Configure an EAS profile in the application that satisfies the requirements above.</span></span>  
2. <span data-ttu-id="ecfb9-187">Open the application, and verify that mail is synchronizing.</span><span class="sxs-lookup"><span data-stu-id="ecfb9-187">Open the application, and verify that mail is synchronizing.</span></span> 

