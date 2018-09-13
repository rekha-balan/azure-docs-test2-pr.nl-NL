---
title: Get started with Azure Active Directory certificate-based authentication
description: Learn how to configure certificate-based authentication in your environment
services: active-directory
ms.service: active-directory
ms.component: authentication
ms.topic: article
ms.date: 01/15/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: mtillman
ms.reviewer: annaba
ms.openlocfilehash: 62ee6aae825d822a1d87858ea6a7eab953a33318
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866291"
---
# <a name="get-started-with-certificate-based-authentication-in-azure-active-directory"></a><span data-ttu-id="3f863-103">Get started with certificate-based authentication in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="3f863-103">Get started with certificate-based authentication in Azure Active Directory</span></span>

<span data-ttu-id="3f863-104">Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android, or iOS device when connecting your Exchange online account to:</span><span class="sxs-lookup"><span data-stu-id="3f863-104">Certificate-based authentication enables you to be authenticated by Azure Active Directory with a client certificate on a Windows, Android, or iOS device when connecting your Exchange online account to:</span></span>

- <span data-ttu-id="3f863-105">Microsoft mobile applications such as Microsoft Outlook and Microsoft Word</span><span class="sxs-lookup"><span data-stu-id="3f863-105">Microsoft mobile applications such as Microsoft Outlook and Microsoft Word</span></span>
- <span data-ttu-id="3f863-106">Exchange ActiveSync (EAS) clients</span><span class="sxs-lookup"><span data-stu-id="3f863-106">Exchange ActiveSync (EAS) clients</span></span>

<span data-ttu-id="3f863-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span><span class="sxs-lookup"><span data-stu-id="3f863-107">Configuring this feature eliminates the need to enter a username and password combination into certain mail and Microsoft Office applications on your mobile device.</span></span>

<span data-ttu-id="3f863-108">This topic:</span><span class="sxs-lookup"><span data-stu-id="3f863-108">This topic:</span></span>

- <span data-ttu-id="3f863-109">Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span><span class="sxs-lookup"><span data-stu-id="3f863-109">Provides you with the steps to configure and utilize certificate-based authentication for users of tenants in Office 365 Enterprise, Business, Education, and US Government plans.</span></span> <span data-ttu-id="3f863-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span><span class="sxs-lookup"><span data-stu-id="3f863-110">This feature is available in preview in Office 365 China, US Government Defense, and US Government Federal plans.</span></span>
- <span data-ttu-id="3f863-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](../connect/active-directory-aadconnectfed-whatis.md) configured.</span><span class="sxs-lookup"><span data-stu-id="3f863-111">Assumes that you already have a [public key infrastructure (PKI)](https://go.microsoft.com/fwlink/?linkid=841737) and [AD FS](../connect/active-directory-aadconnectfed-whatis.md) configured.</span></span>

## <a name="requirements"></a><span data-ttu-id="3f863-112">Requirements</span><span class="sxs-lookup"><span data-stu-id="3f863-112">Requirements</span></span>

<span data-ttu-id="3f863-113">To configure certificate-based authentication, the following statements must be true:</span><span class="sxs-lookup"><span data-stu-id="3f863-113">To configure certificate-based authentication, the following statements must be true:</span></span>

- <span data-ttu-id="3f863-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span><span class="sxs-lookup"><span data-stu-id="3f863-114">Certificate-based authentication (CBA) is only supported for Federated environments for browser applications or native clients using modern authentication (ADAL).</span></span> <span data-ttu-id="3f863-115">The one exception is Exchange Active Sync (EAS) for Exchange Online (EXO), which can be used for  federated and managed accounts.</span><span class="sxs-lookup"><span data-stu-id="3f863-115">The one exception is Exchange Active Sync (EAS) for Exchange Online (EXO), which can be used for  federated and managed accounts.</span></span>
- <span data-ttu-id="3f863-116">The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f863-116">The root certificate authority and any intermediate certificate authorities must be configured in Azure Active Directory.</span></span>
- <span data-ttu-id="3f863-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span><span class="sxs-lookup"><span data-stu-id="3f863-117">Each certificate authority must have a certificate revocation list (CRL) that can be referenced via an Internet facing URL.</span></span>
- <span data-ttu-id="3f863-118">You must have at least one certificate authority configured in Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3f863-118">You must have at least one certificate authority configured in Azure Active Directory.</span></span> <span data-ttu-id="3f863-119">You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.</span><span class="sxs-lookup"><span data-stu-id="3f863-119">You can find related steps in the [Configure the certificate authorities](#step-2-configure-the-certificate-authorities) section.</span></span>
- <span data-ttu-id="3f863-120">For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field.</span><span class="sxs-lookup"><span data-stu-id="3f863-120">For Exchange ActiveSync clients, the client certificate must have the user’s routable email address in Exchange online in either the Principal Name or the RFC822 Name value of the Subject Alternative Name field.</span></span> <span data-ttu-id="3f863-121">Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.</span><span class="sxs-lookup"><span data-stu-id="3f863-121">Azure Active Directory maps the RFC822 value to the Proxy Address attribute in the directory.</span></span>
- <span data-ttu-id="3f863-122">Your client device must have access to at least one certificate authority that issues client certificates.</span><span class="sxs-lookup"><span data-stu-id="3f863-122">Your client device must have access to at least one certificate authority that issues client certificates.</span></span>
- <span data-ttu-id="3f863-123">A client certificate for client authentication must have been issued to your client.</span><span class="sxs-lookup"><span data-stu-id="3f863-123">A client certificate for client authentication must have been issued to your client.</span></span>

## <a name="step-1-select-your-device-platform"></a><span data-ttu-id="3f863-124">Step 1: Select your device platform</span><span class="sxs-lookup"><span data-stu-id="3f863-124">Step 1: Select your device platform</span></span>

<span data-ttu-id="3f863-125">As a first step, for the device platform you care about, you need to review the following:</span><span class="sxs-lookup"><span data-stu-id="3f863-125">As a first step, for the device platform you care about, you need to review the following:</span></span>

- <span data-ttu-id="3f863-126">The Office mobile applications support</span><span class="sxs-lookup"><span data-stu-id="3f863-126">The Office mobile applications support</span></span>
- <span data-ttu-id="3f863-127">The specific implementation requirements</span><span class="sxs-lookup"><span data-stu-id="3f863-127">The specific implementation requirements</span></span>

<span data-ttu-id="3f863-128">The related information exists for the following device platforms:</span><span class="sxs-lookup"><span data-stu-id="3f863-128">The related information exists for the following device platforms:</span></span>

- [<span data-ttu-id="3f863-129">Android</span><span class="sxs-lookup"><span data-stu-id="3f863-129">Android</span></span>](active-directory-certificate-based-authentication-android.md)
- [<span data-ttu-id="3f863-130">iOS</span><span class="sxs-lookup"><span data-stu-id="3f863-130">iOS</span></span>](active-directory-certificate-based-authentication-ios.md)

## <a name="step-2-configure-the-certificate-authorities"></a><span data-ttu-id="3f863-131">Step 2: Configure the certificate authorities</span><span class="sxs-lookup"><span data-stu-id="3f863-131">Step 2: Configure the certificate authorities</span></span>

<span data-ttu-id="3f863-132">To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following:</span><span class="sxs-lookup"><span data-stu-id="3f863-132">To configure your certificate authorities in Azure Active Directory, for each certificate authority, upload the following:</span></span>

* <span data-ttu-id="3f863-133">The public portion of the certificate, in *.cer* format</span><span class="sxs-lookup"><span data-stu-id="3f863-133">The public portion of the certificate, in *.cer* format</span></span>
* <span data-ttu-id="3f863-134">The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside</span><span class="sxs-lookup"><span data-stu-id="3f863-134">The Internet facing URLs where the Certificate Revocation Lists (CRLs) reside</span></span>

<span data-ttu-id="3f863-135">The schema for a certificate authority looks as follows:</span><span class="sxs-lookup"><span data-stu-id="3f863-135">The schema for a certificate authority looks as follows:</span></span>

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

<span data-ttu-id="3f863-136">For the configuration, you can use the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span><span class="sxs-lookup"><span data-stu-id="3f863-136">For the configuration, you can use the [Azure Active Directory PowerShell Version 2](/powershell/azure/install-adv2?view=azureadps-2.0):</span></span>

1. <span data-ttu-id="3f863-137">Start Windows PowerShell with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="3f863-137">Start Windows PowerShell with administrator privileges.</span></span>
2. <span data-ttu-id="3f863-138">Install the Azure AD module version [2.0.0.33](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span><span class="sxs-lookup"><span data-stu-id="3f863-138">Install the Azure AD module version [2.0.0.33](https://www.powershellgallery.com/packages/AzureAD/2.0.0.33) or higher.</span></span>

        Install-Module -Name AzureAD –RequiredVersion 2.0.0.33

<span data-ttu-id="3f863-139">As a first configuration step, you need to establish a connection with your tenant.</span><span class="sxs-lookup"><span data-stu-id="3f863-139">As a first configuration step, you need to establish a connection with your tenant.</span></span> <span data-ttu-id="3f863-140">As soon as a connection to your tenant exists, you can review, add, delete, and modify the trusted certificate authorities that are defined in your directory.</span><span class="sxs-lookup"><span data-stu-id="3f863-140">As soon as a connection to your tenant exists, you can review, add, delete, and modify the trusted certificate authorities that are defined in your directory.</span></span>

### <a name="connect"></a><span data-ttu-id="3f863-141">Connect</span><span class="sxs-lookup"><span data-stu-id="3f863-141">Connect</span></span>

<span data-ttu-id="3f863-142">To establish a connection with your tenant, use the [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3f863-142">To establish a connection with your tenant, use the [Connect-AzureAD](/powershell/module/azuread/connect-azuread?view=azureadps-2.0) cmdlet:</span></span>

    Connect-AzureAD

### <a name="retrieve"></a><span data-ttu-id="3f863-143">Retrieve</span><span class="sxs-lookup"><span data-stu-id="3f863-143">Retrieve</span></span>

<span data-ttu-id="3f863-144">To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="3f863-144">To retrieve the trusted certificate authorities that are defined in your directory, use the [Get-AzureADTrustedCertificateAuthority](/powershell/module/azuread/get-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet.</span></span>

    Get-AzureADTrustedCertificateAuthority

### <a name="add"></a><span data-ttu-id="3f863-145">Add</span><span class="sxs-lookup"><span data-stu-id="3f863-145">Add</span></span>

<span data-ttu-id="3f863-146">To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set the **crlDistributionPoint** attribute to a correct value:</span><span class="sxs-lookup"><span data-stu-id="3f863-146">To create a trusted certificate authority, use the [New-AzureADTrustedCertificateAuthority](/powershell/module/azuread/new-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet and set the **crlDistributionPoint** attribute to a correct value:</span></span>

    $cert=Get-Content -Encoding byte "[LOCATION OF THE CER FILE]"
    $new_ca=New-Object -TypeName Microsoft.Open.AzureAD.Model.CertificateAuthorityInformation
    $new_ca.AuthorityType=0
    $new_ca.TrustedCertificate=$cert
    $new_ca.crlDistributionPoint=”<CRL Distribution URL>”
    New-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $new_ca

### <a name="remove"></a><span data-ttu-id="3f863-147">Remove</span><span class="sxs-lookup"><span data-stu-id="3f863-147">Remove</span></span>

<span data-ttu-id="3f863-148">To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3f863-148">To remove a trusted certificate authority, use the [Remove-AzureADTrustedCertificateAuthority](/powershell/module/azuread/remove-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority
    Remove-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[2]

### <a name="modify"></a><span data-ttu-id="3f863-149">Modify</span><span class="sxs-lookup"><span data-stu-id="3f863-149">Modify</span></span>

<span data-ttu-id="3f863-150">To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span><span class="sxs-lookup"><span data-stu-id="3f863-150">To modify a trusted certificate authority, use the [Set-AzureADTrustedCertificateAuthority](/powershell/module/azuread/set-azureadtrustedcertificateauthority?view=azureadps-2.0) cmdlet:</span></span>

    $c=Get-AzureADTrustedCertificateAuthority
    $c[0].AuthorityType=1
    Set-AzureADTrustedCertificateAuthority -CertificateAuthorityInformation $c[0]

## <a name="step-3-configure-revocation"></a><span data-ttu-id="3f863-151">Step 3: Configure revocation</span><span class="sxs-lookup"><span data-stu-id="3f863-151">Step 3: Configure revocation</span></span>

<span data-ttu-id="3f863-152">To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it.</span><span class="sxs-lookup"><span data-stu-id="3f863-152">To revoke a client certificate, Azure Active Directory fetches the certificate revocation list (CRL) from the URLs uploaded as part of certificate authority information and caches it.</span></span> <span data-ttu-id="3f863-153">The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid.</span><span class="sxs-lookup"><span data-stu-id="3f863-153">The last publish timestamp (**Effective Date** property) in the CRL is used to ensure the CRL is still valid.</span></span> <span data-ttu-id="3f863-154">The CRL is periodically referenced to revoke access to certificates that are a part of the list.</span><span class="sxs-lookup"><span data-stu-id="3f863-154">The CRL is periodically referenced to revoke access to certificates that are a part of the list.</span></span>

<span data-ttu-id="3f863-155">If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated.</span><span class="sxs-lookup"><span data-stu-id="3f863-155">If a more instant revocation is required (for example, if a user loses a device), the authorization token of the user can be invalidated.</span></span> <span data-ttu-id="3f863-156">To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3f863-156">To invalidate the authorization token, set the **StsRefreshTokenValidFrom** field for this particular user using Windows PowerShell.</span></span> <span data-ttu-id="3f863-157">You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.</span><span class="sxs-lookup"><span data-stu-id="3f863-157">You must update the **StsRefreshTokenValidFrom** field for each user you want to revoke access for.</span></span>

<span data-ttu-id="3f863-158">To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.</span><span class="sxs-lookup"><span data-stu-id="3f863-158">To ensure that the revocation persists, you must set the **Effective Date** of the CRL to a date after the value set by **StsRefreshTokenValidFrom** and ensure the certificate in question is in the CRL.</span></span>

<span data-ttu-id="3f863-159">The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field.</span><span class="sxs-lookup"><span data-stu-id="3f863-159">The following steps outline the process for updating and invalidating the authorization token by setting the **StsRefreshTokenValidFrom** field.</span></span>

<span data-ttu-id="3f863-160">**To configure revocation:**</span><span class="sxs-lookup"><span data-stu-id="3f863-160">**To configure revocation:**</span></span>

1. <span data-ttu-id="3f863-161">Connect with admin credentials to the MSOL service:</span><span class="sxs-lookup"><span data-stu-id="3f863-161">Connect with admin credentials to the MSOL service:</span></span>

        $msolcred = get-credential
        connect-msolservice -credential $msolcred

2. <span data-ttu-id="3f863-162">Retrieve the current StsRefreshTokensValidFrom value for a user:</span><span class="sxs-lookup"><span data-stu-id="3f863-162">Retrieve the current StsRefreshTokensValidFrom value for a user:</span></span>

        $user = Get-MsolUser -UserPrincipalName test@yourdomain.com`
        $user.StsRefreshTokensValidFrom

3. <span data-ttu-id="3f863-163">Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:</span><span class="sxs-lookup"><span data-stu-id="3f863-163">Configure a new StsRefreshTokensValidFrom value for the user equal to the current timestamp:</span></span>

        Set-MsolUser -UserPrincipalName test@yourdomain.com -StsRefreshTokensValidFrom ("03/05/2016")

<span data-ttu-id="3f863-164">The date you set must be in the future.</span><span class="sxs-lookup"><span data-stu-id="3f863-164">The date you set must be in the future.</span></span> <span data-ttu-id="3f863-165">If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set.</span><span class="sxs-lookup"><span data-stu-id="3f863-165">If the date is not in the future, the **StsRefreshTokensValidFrom** property is not set.</span></span> <span data-ttu-id="3f863-166">If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).</span><span class="sxs-lookup"><span data-stu-id="3f863-166">If the date is in the future, **StsRefreshTokensValidFrom** is set to the current time (not the date indicated by Set-MsolUser command).</span></span>

## <a name="step-4-test-your-configuration"></a><span data-ttu-id="3f863-167">Step 4: Test your configuration</span><span class="sxs-lookup"><span data-stu-id="3f863-167">Step 4: Test your configuration</span></span>

### <a name="testing-your-certificate"></a><span data-ttu-id="3f863-168">Testing your certificate</span><span class="sxs-lookup"><span data-stu-id="3f863-168">Testing your certificate</span></span>

<span data-ttu-id="3f863-169">As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span><span class="sxs-lookup"><span data-stu-id="3f863-169">As a first configuration test, you should try to sign in to [Outlook Web Access](https://outlook.office365.com) or [SharePoint Online](https://microsoft.sharepoint.com) using your **on-device browser**.</span></span>

<span data-ttu-id="3f863-170">If your sign-in is successful, then you know that:</span><span class="sxs-lookup"><span data-stu-id="3f863-170">If your sign-in is successful, then you know that:</span></span>

- <span data-ttu-id="3f863-171">The user certificate has been provisioned to your test device</span><span class="sxs-lookup"><span data-stu-id="3f863-171">The user certificate has been provisioned to your test device</span></span>
- <span data-ttu-id="3f863-172">AD FS is configured correctly</span><span class="sxs-lookup"><span data-stu-id="3f863-172">AD FS is configured correctly</span></span>

### <a name="testing-office-mobile-applications"></a><span data-ttu-id="3f863-173">Testing Office mobile applications</span><span class="sxs-lookup"><span data-stu-id="3f863-173">Testing Office mobile applications</span></span>

<span data-ttu-id="3f863-174">**To test certificate-based authentication on your mobile Office application:**</span><span class="sxs-lookup"><span data-stu-id="3f863-174">**To test certificate-based authentication on your mobile Office application:**</span></span>

1. <span data-ttu-id="3f863-175">On your test device, install an Office mobile application (for example, OneDrive).</span><span class="sxs-lookup"><span data-stu-id="3f863-175">On your test device, install an Office mobile application (for example, OneDrive).</span></span>
3. <span data-ttu-id="3f863-176">Launch the application.</span><span class="sxs-lookup"><span data-stu-id="3f863-176">Launch the application.</span></span>
4. <span data-ttu-id="3f863-177">Enter your user name, and then select the user certificate you want to use.</span><span class="sxs-lookup"><span data-stu-id="3f863-177">Enter your user name, and then select the user certificate you want to use.</span></span>

<span data-ttu-id="3f863-178">You should be successfully signed in.</span><span class="sxs-lookup"><span data-stu-id="3f863-178">You should be successfully signed in.</span></span>

### <a name="testing-exchange-activesync-client-applications"></a><span data-ttu-id="3f863-179">Testing Exchange ActiveSync client applications</span><span class="sxs-lookup"><span data-stu-id="3f863-179">Testing Exchange ActiveSync client applications</span></span>

<span data-ttu-id="3f863-180">To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.</span><span class="sxs-lookup"><span data-stu-id="3f863-180">To access Exchange ActiveSync (EAS) via certificate-based authentication, an EAS profile containing the client certificate must be available to the application.</span></span>

<span data-ttu-id="3f863-181">The EAS profile must contain the following information:</span><span class="sxs-lookup"><span data-stu-id="3f863-181">The EAS profile must contain the following information:</span></span>

- <span data-ttu-id="3f863-182">The user certificate to be used for authentication</span><span class="sxs-lookup"><span data-stu-id="3f863-182">The user certificate to be used for authentication</span></span>

- <span data-ttu-id="3f863-183">The EAS endpoint (for example, outlook.office365.com)</span><span class="sxs-lookup"><span data-stu-id="3f863-183">The EAS endpoint (for example, outlook.office365.com)</span></span>

<span data-ttu-id="3f863-184">An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.</span><span class="sxs-lookup"><span data-stu-id="3f863-184">An EAS profile can be configured and placed on the device through the utilization of Mobile device management (MDM) such as Intune or by manually placing the certificate in the EAS profile on the device.</span></span>

### <a name="testing-eas-client-applications-on-android"></a><span data-ttu-id="3f863-185">Testing EAS client applications on Android</span><span class="sxs-lookup"><span data-stu-id="3f863-185">Testing EAS client applications on Android</span></span>

<span data-ttu-id="3f863-186">**To test certificate authentication:**</span><span class="sxs-lookup"><span data-stu-id="3f863-186">**To test certificate authentication:**</span></span>

1. <span data-ttu-id="3f863-187">Configure an EAS profile in the application that satisfies the requirements in the prior section.</span><span class="sxs-lookup"><span data-stu-id="3f863-187">Configure an EAS profile in the application that satisfies the requirements in the prior section.</span></span>
2. <span data-ttu-id="3f863-188">Open the application, and verify that mail is synchronizing.</span><span class="sxs-lookup"><span data-stu-id="3f863-188">Open the application, and verify that mail is synchronizing.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f863-189">Next steps</span><span class="sxs-lookup"><span data-stu-id="3f863-189">Next steps</span></span>

[<span data-ttu-id="3f863-190">Additional information about certificate-based authenticaion on Android devices.</span><span class="sxs-lookup"><span data-stu-id="3f863-190">Additional information about certificate-based authenticaion on Android devices.</span></span>](active-directory-certificate-based-authentication-android.md)

[<span data-ttu-id="3f863-191">Additional information about certificate-based authenticaion on iOS devices.</span><span class="sxs-lookup"><span data-stu-id="3f863-191">Additional information about certificate-based authenticaion on iOS devices.</span></span>](active-directory-certificate-based-authentication-ios.md)