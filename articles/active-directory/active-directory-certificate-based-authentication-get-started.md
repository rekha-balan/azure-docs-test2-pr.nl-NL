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
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a>Get started with certificate-based authentication in Azure Active Directory

Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android or iOS device when connecting your Exchange online account to: 

- Office mobile applications such as Microsoft Outlook and Microsoft Word   

- Exchange ActiveSync (EAS) clients 

Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device. 

This topic:

- Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans. This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans. 

- Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](connect/active-directory-aadconnectfed-whatis.md) configured.    


## <a name="requirements"></a>Requirements

To configure certificate-based authentication, the following must be true:  

- The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.  

- Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.  

- You must have at least one certificate authority configured in Azure Active Directory. You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.  

- For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field. Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.  

- Your client device must have access to at least one certificate authority that issues client certificates.  

- A client certificate for client authentication must have been issued to your client.  




## <a name="step-1-select-your-device-platform"></a>Step 1: Select your device platform

As a first step, for the device platform you care about, you need to review the following:

- The Office mobile applications support 
- The specific implementation requirements  

The related information exists for the following device platforms:

- [Android](active-directory-certificate-based-authentication-android.md)
- [iOS](active-directory-certificate-based-authentication-ios.md)


## <a name="step-2-configure-the-certificate-authorities"></a>Step 2: Configure the certificate authorities 

To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following: 

* The public portion of the certificate, in *.cer* format 
* The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside

The schema for a certificate authority looks as follows: 

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

For the configuration, you can use the [Azure Active Directory PowerShell Version 2](https://docs.microsoft.com/powershell/azuread/):  

1. Start Windows PowerShell with administrator privileges. 
2. Install the Azure AD module. You need to install Version [2.0.0.33 ](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.  
   
        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33 

As a first configuration step, you need to establish a connection with your tenant. As soon as a connection to your tenant exists, you can review, add, delete and modify the trusted certificate authorities that are defined in your directory. 

### <a name="connect"></a>Connect

To establish a connection with your tenant, use the [Connect-AzureAD](https://docs.microsoft.com/powershell/azuread/v2/connect-azuread) cmdlet:

    Connect-AzureAD 


### <a name="retrieve"></a>Retrieve 

To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/get-azureadtrustedcertificateauthority) cmdlet. 

    Get-AzureADTrustedCertificateAuthority 
 

### <a name="add"></a>Add

To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/new-azureadtrustedcertificateauthority) cmdlet: 
   
    $cert=Get-Content -Encoding byte "[LOCATION OF THE CER FILE]" 
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation 
    $new_ca.AuthorityType=0 
    $new_ca.TrustedCertificate=$cert 
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca 


### <a name="remove"></a>Remove

To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/remove-azureadtrustedcertificateauthority) cmdlet:
   
    $c=Get-AzureADTrustedCertificateAuthority 
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2] 


### <a name="modfiy"></a>Modfiy

To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](https://docs.microsoft.com/powershell/azuread/v2/set-azureadtrustedcertificateauthority) cmdlet:

    $c=Get-AzureADTrustedCertificateAuthority 
    $c[0].AuthorityType=1 
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0] 


## <a name="step-3-configure-revocation"></a>Step 3: Configure revocation

To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it. The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid. The CRL is periodically referenced to revoke access to certificates that are a part of the list.

If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated. To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell. You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.

To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.

The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field. 

**To configure revocation:** 

1. Connect with admin credentials to the MSOL service: 
   
        $msolcred = get-credential 
        connect-msolservice -credential $msolcred 

2. Retrieve the current StsRefreshTokensValidFrom value for a user: 
   
        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com` 
        $user.StsRefreshTokensValidFrom 

3. Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp: 
   
        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

The date you set must be in the future. If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set. If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command). 


## <a name="step-4-test-your-configuration"></a>Step 4: Test your configuration

### <a name="testing-your-certificate"></a>Testing your certificate

As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.

If your sign-in is successful, then you know that:

- The user certificate has been provisioned to your test device
- AD FS is configured correctly  


### <a name="testing-office-mobile-applications"></a>Testing Office mobile applications

**To test certificate-based authentication on your mobile Office application:** 

1. On your test device, install an Office mobile application (e.g., OneDrive).
3. Launch the application. 
4. Enter your user name, and then select the user certificate you want to use. 

You should be successfully signed in. 

### <a name="testing-exchange-activesync-client-applications"></a>Testing Exchange ActiveSync client applications

To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application. 

The EAS profile must contain the following information:

- The user certificate to be used for authentication 

- The EAS endpoint (for example, outlook.office365.com)

An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.  

### <a name="testing-eas-client-applications-on-android"></a>Testing EAS client applications on Android

**To test certificate authentication:**  

1. Configure an EAS profile in the application that satisfies the requirements above.  
2. Open the application, and verify that mail is synchronizing. 

