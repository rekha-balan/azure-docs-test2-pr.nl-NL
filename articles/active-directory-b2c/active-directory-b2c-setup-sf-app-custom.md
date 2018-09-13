---
title: Adding a Salesforce SAML provider by using custom policies in Azure Active Directory B2C | Microsoft Docs
description: Learn about how to create and manage Azure Active Directory B2C custom policies.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 08/15/2018
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 5b7621bde0be02b4656c4678438b94499bb82b5b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856841"
---
# <a name="azure-active-directory-b2c-sign-in-by-using-salesforce-accounts-via-saml"></a><span data-ttu-id="42cd2-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span><span class="sxs-lookup"><span data-stu-id="42cd2-103">Azure Active Directory B2C: Sign in by using Salesforce accounts via SAML</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="42cd2-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span><span class="sxs-lookup"><span data-stu-id="42cd2-104">This article shows you how to use [custom policies](active-directory-b2c-overview-custom.md) to set up sign-in for users from a specific Salesforce organization.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42cd2-105">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="42cd2-105">Prerequisites</span></span>

### <a name="azure-ad-b2c-setup"></a><span data-ttu-id="42cd2-106">Azure AD B2C setup</span><span class="sxs-lookup"><span data-stu-id="42cd2-106">Azure AD B2C setup</span></span>

<span data-ttu-id="42cd2-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="42cd2-107">Ensure that you have completed all of the steps that show you how to [get started with custom policies](active-directory-b2c-get-started-custom.md) in Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="42cd2-108">These include:</span><span class="sxs-lookup"><span data-stu-id="42cd2-108">These include:</span></span>

* <span data-ttu-id="42cd2-109">Create an Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="42cd2-109">Create an Azure AD B2C tenant.</span></span>
* <span data-ttu-id="42cd2-110">Create an Azure AD B2C application.</span><span class="sxs-lookup"><span data-stu-id="42cd2-110">Create an Azure AD B2C application.</span></span>
* <span data-ttu-id="42cd2-111">Register two policy engine applications.</span><span class="sxs-lookup"><span data-stu-id="42cd2-111">Register two policy engine applications.</span></span>
* <span data-ttu-id="42cd2-112">Set up keys.</span><span class="sxs-lookup"><span data-stu-id="42cd2-112">Set up keys.</span></span>
* <span data-ttu-id="42cd2-113">Set up the starter pack.</span><span class="sxs-lookup"><span data-stu-id="42cd2-113">Set up the starter pack.</span></span>

### <a name="salesforce-setup"></a><span data-ttu-id="42cd2-114">Salesforce setup</span><span class="sxs-lookup"><span data-stu-id="42cd2-114">Salesforce setup</span></span>

<span data-ttu-id="42cd2-115">In this article, we assume that you have already done the following:</span><span class="sxs-lookup"><span data-stu-id="42cd2-115">In this article, we assume that you have already done the following:</span></span>

* <span data-ttu-id="42cd2-116">Signed up for a Salesforce account.</span><span class="sxs-lookup"><span data-stu-id="42cd2-116">Signed up for a Salesforce account.</span></span> <span data-ttu-id="42cd2-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span><span class="sxs-lookup"><span data-stu-id="42cd2-117">You can sign up for a [free Developer Edition account](https://developer.salesforce.com/signup).</span></span>
* <span data-ttu-id="42cd2-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span><span class="sxs-lookup"><span data-stu-id="42cd2-118">[Set up a My Domain](https://help.salesforce.com/articleView?id=domain_name_setup.htm&language=en_US&type=0) for your Salesforce organization.</span></span>

## <a name="set-up-salesforce-so-users-can-federate"></a><span data-ttu-id="42cd2-119">Set up Salesforce so users can federate</span><span class="sxs-lookup"><span data-stu-id="42cd2-119">Set up Salesforce so users can federate</span></span>

<span data-ttu-id="42cd2-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span><span class="sxs-lookup"><span data-stu-id="42cd2-120">To help Azure AD B2C communicate with Salesforce, you need to get the Salesforce metadata URL.</span></span>

### <a name="set-up-salesforce-as-an-identity-provider"></a><span data-ttu-id="42cd2-121">Set up Salesforce as an identity provider</span><span class="sxs-lookup"><span data-stu-id="42cd2-121">Set up Salesforce as an identity provider</span></span>

> [!NOTE]
> <span data-ttu-id="42cd2-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span><span class="sxs-lookup"><span data-stu-id="42cd2-122">In this article, we assume you are using [Salesforce Lightning Experience](https://developer.salesforce.com/page/Lightning_Experience_FAQ).</span></span>

1. <span data-ttu-id="42cd2-123">[Sign in to Salesforce](https://login.salesforce.com/).</span><span class="sxs-lookup"><span data-stu-id="42cd2-123">[Sign in to Salesforce](https://login.salesforce.com/).</span></span> 
2. <span data-ttu-id="42cd2-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-124">On the left menu, under **Settings**, expand **Identity**, and then click **Identity Provider**.</span></span>
3. <span data-ttu-id="42cd2-125">Click **Enable Identity Provider**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-125">Click **Enable Identity Provider**.</span></span>
4. <span data-ttu-id="42cd2-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="42cd2-126">Under **Select the certificate**, select the certificate you want Salesforce to use to communicate with Azure AD B2C.</span></span> <span data-ttu-id="42cd2-127">(You can use the default certificate.) Click **Save**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-127">(You can use the default certificate.) Click **Save**.</span></span> 

### <a name="create-a-connected-app-in-salesforce"></a><span data-ttu-id="42cd2-128">Create a connected app in Salesforce</span><span class="sxs-lookup"><span data-stu-id="42cd2-128">Create a connected app in Salesforce</span></span>

1. <span data-ttu-id="42cd2-129">On the **Identity Provider** page, go to **Service Providers**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-129">On the **Identity Provider** page, go to **Service Providers**.</span></span>
2. <span data-ttu-id="42cd2-130">Click **Service Providers are now created via Connected Apps. Click here.**</span><span class="sxs-lookup"><span data-stu-id="42cd2-130">Click **Service Providers are now created via Connected Apps. Click here.**</span></span>
3. <span data-ttu-id="42cd2-131">Under **Basic Information**,  enter the required values for your connected app.</span><span class="sxs-lookup"><span data-stu-id="42cd2-131">Under **Basic Information**,  enter the required values for your connected app.</span></span>
4. <span data-ttu-id="42cd2-132">Under **Web App Settings**, select the **Enable SAML** check box.</span><span class="sxs-lookup"><span data-stu-id="42cd2-132">Under **Web App Settings**, select the **Enable SAML** check box.</span></span>
5. <span data-ttu-id="42cd2-133">In the **Entity ID** field, enter the following URL.</span><span class="sxs-lookup"><span data-stu-id="42cd2-133">In the **Entity ID** field, enter the following URL.</span></span> <span data-ttu-id="42cd2-134">Ensure that you replace the value for `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="42cd2-134">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://tenantName.b2clogin.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase
      ```
6. <span data-ttu-id="42cd2-135">In the **ACS URL** field, enter the following URL.</span><span class="sxs-lookup"><span data-stu-id="42cd2-135">In the **ACS URL** field, enter the following URL.</span></span> <span data-ttu-id="42cd2-136">Ensure that you replace the value for `tenantName`.</span><span class="sxs-lookup"><span data-stu-id="42cd2-136">Ensure that you replace the value for `tenantName`.</span></span>
      ```
      https://tenantName.b2clogin.com/te/tenantName.onmicrosoft.com/B2C_1A_TrustFrameworkBase/samlp/sso/assertionconsumer
      ```
7. <span data-ttu-id="42cd2-137">Leave the default values for all other settings.</span><span class="sxs-lookup"><span data-stu-id="42cd2-137">Leave the default values for all other settings.</span></span>
8. <span data-ttu-id="42cd2-138">Scroll to the bottom of the list, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-138">Scroll to the bottom of the list, and then click **Save**.</span></span>

### <a name="get-the-metadata-url"></a><span data-ttu-id="42cd2-139">Get the metadata URL</span><span class="sxs-lookup"><span data-stu-id="42cd2-139">Get the metadata URL</span></span>

1. <span data-ttu-id="42cd2-140">On the overview page of your connected app, click **Manage**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-140">On the overview page of your connected app, click **Manage**.</span></span>
2. <span data-ttu-id="42cd2-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span><span class="sxs-lookup"><span data-stu-id="42cd2-141">Copy the value for **Metadata Discovery Endpoint**, and then save it.</span></span> <span data-ttu-id="42cd2-142">You'll use it later in this article.</span><span class="sxs-lookup"><span data-stu-id="42cd2-142">You'll use it later in this article.</span></span>

### <a name="set-up-salesforce-users-to-federate"></a><span data-ttu-id="42cd2-143">Set up Salesforce users to federate</span><span class="sxs-lookup"><span data-stu-id="42cd2-143">Set up Salesforce users to federate</span></span>

1. <span data-ttu-id="42cd2-144">On the **Manage** page of your connected app, go to **Profiles**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-144">On the **Manage** page of your connected app, go to **Profiles**.</span></span>
2. <span data-ttu-id="42cd2-145">Click **Manage Profiles**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-145">Click **Manage Profiles**.</span></span>
3. <span data-ttu-id="42cd2-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="42cd2-146">Select the profiles (or groups of users) that you want to federate with Azure AD B2C.</span></span> <span data-ttu-id="42cd2-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span><span class="sxs-lookup"><span data-stu-id="42cd2-147">As a system administrator, select the **System Administrator** check box, so that you can federate by using your Salesforce account.</span></span>

## <a name="generate-a-signing-certificate-for-azure-ad-b2c"></a><span data-ttu-id="42cd2-148">Generate a signing certificate for Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="42cd2-148">Generate a signing certificate for Azure AD B2C</span></span>

<span data-ttu-id="42cd2-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="42cd2-149">Requests sent to Salesforce need to be signed by Azure AD B2C.</span></span> <span data-ttu-id="42cd2-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span><span class="sxs-lookup"><span data-stu-id="42cd2-150">To generate a signing certificate, open Azure PowerShell, and then run the following commands.</span></span>

> [!NOTE]
> <span data-ttu-id="42cd2-151">Make sure that you update the tenant name and password in the top two lines.</span><span class="sxs-lookup"><span data-stu-id="42cd2-151">Make sure that you update the tenant name and password in the top two lines.</span></span>

```PowerShell
$tenantName = "<YOUR TENANT NAME>.onmicrosoft.com"
$pwdText = "<YOUR PASSWORD HERE>"

$Cert = New-SelfSignedCertificate -CertStoreLocation Cert:\CurrentUser\My -DnsName "SamlIdp.$tenantName" -Subject "B2C SAML Signing Cert" -HashAlgorithm SHA256 -KeySpec Signature -KeyLength 2048

$pwd = ConvertTo-SecureString -String $pwdText -Force -AsPlainText

Export-PfxCertificate -Cert $Cert -FilePath .\B2CSigningCert.pfx -Password $pwd
```

## <a name="add-the-saml-signing-certificate-to-azure-ad-b2c"></a><span data-ttu-id="42cd2-152">Add the SAML signing certificate to Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="42cd2-152">Add the SAML signing certificate to Azure AD B2C</span></span>

<span data-ttu-id="42cd2-153">Upload the signing certificate to your Azure AD B2C tenant:</span><span class="sxs-lookup"><span data-stu-id="42cd2-153">Upload the signing certificate to your Azure AD B2C tenant:</span></span> 

1. <span data-ttu-id="42cd2-154">Go to your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="42cd2-154">Go to your Azure AD B2C tenant.</span></span> <span data-ttu-id="42cd2-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-155">Click **Settings** > **Identity Experience Framework** > **Policy Keys**.</span></span>
2. <span data-ttu-id="42cd2-156">Click **+Add**, and then:</span><span class="sxs-lookup"><span data-stu-id="42cd2-156">Click **+Add**, and then:</span></span>
    1. <span data-ttu-id="42cd2-157">Click **Options** > **Upload**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-157">Click **Options** > **Upload**.</span></span>
    2. <span data-ttu-id="42cd2-158">Enter a **Name** (for example, SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="42cd2-158">Enter a **Name** (for example, SAMLSigningCert).</span></span> <span data-ttu-id="42cd2-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span><span class="sxs-lookup"><span data-stu-id="42cd2-159">The prefix *B2C_1A_* is automatically added to the name of your key.</span></span>
    3. <span data-ttu-id="42cd2-160">To select your certificate, select **upload file control**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-160">To select your certificate, select **upload file control**.</span></span> 
    4. <span data-ttu-id="42cd2-161">Enter the certificate's password that you set in the PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="42cd2-161">Enter the certificate's password that you set in the PowerShell script.</span></span>
3. <span data-ttu-id="42cd2-162">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-162">Click **Create**.</span></span>
4. <span data-ttu-id="42cd2-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="42cd2-163">Verify that you've created a key (for example, B2C_1A_SAMLSigningCert).</span></span> <span data-ttu-id="42cd2-164">Take note of the full name (including *B2C_1A_*).</span><span class="sxs-lookup"><span data-stu-id="42cd2-164">Take note of the full name (including *B2C_1A_*).</span></span> <span data-ttu-id="42cd2-165">You will refer to this key later in the policy.</span><span class="sxs-lookup"><span data-stu-id="42cd2-165">You will refer to this key later in the policy.</span></span>

## <a name="create-the-salesforce-saml-claims-provider-in-your-base-policy"></a><span data-ttu-id="42cd2-166">Create the Salesforce SAML claims provider in your base policy</span><span class="sxs-lookup"><span data-stu-id="42cd2-166">Create the Salesforce SAML claims provider in your base policy</span></span>

<span data-ttu-id="42cd2-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span><span class="sxs-lookup"><span data-stu-id="42cd2-167">You need to define Salesforce as a claims provider so users can sign in by using Salesforce.</span></span> <span data-ttu-id="42cd2-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span><span class="sxs-lookup"><span data-stu-id="42cd2-168">In other words, you need to specify the endpoint that Azure AD B2C will communicate with.</span></span> <span data-ttu-id="42cd2-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span><span class="sxs-lookup"><span data-stu-id="42cd2-169">The endpoint will *provide* a set of *claims* that Azure AD B2C uses to verify that a specific user has authenticated.</span></span> <span data-ttu-id="42cd2-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span><span class="sxs-lookup"><span data-stu-id="42cd2-170">To do this, add a `<ClaimsProvider>` for Salesforce in the extension file of your policy:</span></span>

1. <span data-ttu-id="42cd2-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="42cd2-171">In your working directory, open the extension file (TrustFrameworkExtensions.xml).</span></span>
2. <span data-ttu-id="42cd2-172">Find the `<ClaimsProviders>` section.</span><span class="sxs-lookup"><span data-stu-id="42cd2-172">Find the `<ClaimsProviders>` section.</span></span> <span data-ttu-id="42cd2-173">If it does not exist, create it under the root node.</span><span class="sxs-lookup"><span data-stu-id="42cd2-173">If it does not exist, create it under the root node.</span></span>
3. <span data-ttu-id="42cd2-174">Add a new `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="42cd2-174">Add a new `<ClaimsProvider>`:</span></span>

    ```XML
    <ClaimsProvider>
      <Domain>salesforce</Domain>
      <DisplayName>Salesforce</DisplayName>
      <TechnicalProfiles>
        <TechnicalProfile Id="salesforce">
          <DisplayName>Salesforce</DisplayName>
          <Description>Login with your Salesforce account</Description>
          <Protocol Name="SAML2"/>
          <Metadata>
            <Item Key="RequestsSigned">false</Item>
            <Item Key="WantsEncryptedAssertions">false</Item>
            <Item Key="WantsSignedAssertions">false</Item>
            <Item Key="PartnerEntity">https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp.xml</Item>
          </Metadata>
          <CryptographicKeys>
            <Key Id="SamlAssertionSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
            <Key Id="SamlMessageSigning" StorageReferenceId="B2C_1A_SAMLSigningCert"/>
          </CryptographicKeys>
          <OutputClaims>
            <OutputClaim ClaimTypeReferenceId="socialIdpUserId" PartnerClaimType="userId"/>
            <OutputClaim ClaimTypeReferenceId="givenName" PartnerClaimType="given_name"/>
            <OutputClaim ClaimTypeReferenceId="surname" PartnerClaimType="family_name"/>
            <OutputClaim ClaimTypeReferenceId="email" PartnerClaimType="email"/>
            <OutputClaim ClaimTypeReferenceId="displayName" PartnerClaimType="username"/>
            <OutputClaim ClaimTypeReferenceId="authenticationSource" DefaultValue="socialIdpAuthentication"/>
            <OutputClaim ClaimTypeReferenceId="identityProvider" DefaultValue="SAMLIdp" />
          </OutputClaims>
          <OutputClaimsTransformations>
            <OutputClaimsTransformation ReferenceId="CreateRandomUPNUserName"/>
            <OutputClaimsTransformation ReferenceId="CreateUserPrincipalName"/>
            <OutputClaimsTransformation ReferenceId="CreateAlternativeSecurityId"/>
            <OutputClaimsTransformation ReferenceId="CreateSubjectClaimFromAlternativeSecurityId"/>
          </OutputClaimsTransformations>
          <UseTechnicalProfileForSessionManagement ReferenceId="SM-Noop"/>
        </TechnicalProfile>
      </TechnicalProfiles>
    </ClaimsProvider>
    ```

<span data-ttu-id="42cd2-175">Under the `<ClaimsProvider>` node:</span><span class="sxs-lookup"><span data-stu-id="42cd2-175">Under the `<ClaimsProvider>` node:</span></span>

1. <span data-ttu-id="42cd2-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span><span class="sxs-lookup"><span data-stu-id="42cd2-176">Change the value for `<Domain>` to a unique value that distinguishes `<ClaimsProvider>` from other identity providers.</span></span>
2. <span data-ttu-id="42cd2-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span><span class="sxs-lookup"><span data-stu-id="42cd2-177">Update the value for `<DisplayName>` to a display name for the claims provider.</span></span> <span data-ttu-id="42cd2-178">Currently, this value is not used.</span><span class="sxs-lookup"><span data-stu-id="42cd2-178">Currently, this value is not used.</span></span>

### <a name="update-the-technical-profile"></a><span data-ttu-id="42cd2-179">Update the technical profile</span><span class="sxs-lookup"><span data-stu-id="42cd2-179">Update the technical profile</span></span>

<span data-ttu-id="42cd2-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="42cd2-180">To get a SAML token from Salesforce, define the protocols that Azure AD B2C will use to communicate with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="42cd2-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span><span class="sxs-lookup"><span data-stu-id="42cd2-181">Do this in the `<TechnicalProfile>` element of `<ClaimsProvider>`:</span></span>

1. <span data-ttu-id="42cd2-182">Update the ID of the `<TechnicalProfile>` node.</span><span class="sxs-lookup"><span data-stu-id="42cd2-182">Update the ID of the `<TechnicalProfile>` node.</span></span> <span data-ttu-id="42cd2-183">This ID is used to refer to this technical profile from other parts of the policy.</span><span class="sxs-lookup"><span data-stu-id="42cd2-183">This ID is used to refer to this technical profile from other parts of the policy.</span></span>
2. <span data-ttu-id="42cd2-184">Update the value for `<DisplayName>`.</span><span class="sxs-lookup"><span data-stu-id="42cd2-184">Update the value for `<DisplayName>`.</span></span> <span data-ttu-id="42cd2-185">This value is displayed on the sign-in button on your sign-in page.</span><span class="sxs-lookup"><span data-stu-id="42cd2-185">This value is displayed on the sign-in button on your sign-in page.</span></span>
3. <span data-ttu-id="42cd2-186">Update the value for `<Description>`.</span><span class="sxs-lookup"><span data-stu-id="42cd2-186">Update the value for `<Description>`.</span></span>
4. <span data-ttu-id="42cd2-187">Salesforce uses the SAML 2.0 protocol.</span><span class="sxs-lookup"><span data-stu-id="42cd2-187">Salesforce uses the SAML 2.0 protocol.</span></span> <span data-ttu-id="42cd2-188">Ensure that the value for `<Protocol>` is **SAML2**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-188">Ensure that the value for `<Protocol>` is **SAML2**.</span></span>

<span data-ttu-id="42cd2-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span><span class="sxs-lookup"><span data-stu-id="42cd2-189">Update the `<Metadata>` section in the preceding XML to reflect the settings for your specific Salesforce account.</span></span> <span data-ttu-id="42cd2-190">In the XML, update the metadata values:</span><span class="sxs-lookup"><span data-stu-id="42cd2-190">In the XML, update the metadata values:</span></span>

1. <span data-ttu-id="42cd2-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span><span class="sxs-lookup"><span data-stu-id="42cd2-191">Update the value of `<Item Key="PartnerEntity">` with the Salesforce metadata URL you copied earlier.</span></span> <span data-ttu-id="42cd2-192">It has the following format:</span><span class="sxs-lookup"><span data-stu-id="42cd2-192">It has the following format:</span></span> 

    `https://contoso-dev-ed.my.salesforce.com/.well-known/samlidp/connectedapp.xml`

2. <span data-ttu-id="42cd2-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span><span class="sxs-lookup"><span data-stu-id="42cd2-193">In the `<CryptographicKeys>` section, update the value for both instances of `StorageReferenceId` to the name of the key of your signing certificate (for example, B2C_1A_SAMLSigningCert).</span></span>

### <a name="upload-the-extension-file-for-verification"></a><span data-ttu-id="42cd2-194">Upload the extension file for verification</span><span class="sxs-lookup"><span data-stu-id="42cd2-194">Upload the extension file for verification</span></span>

<span data-ttu-id="42cd2-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span><span class="sxs-lookup"><span data-stu-id="42cd2-195">Your policy is now configured so that Azure AD B2C knows how to communicate with Salesforce.</span></span> <span data-ttu-id="42cd2-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span><span class="sxs-lookup"><span data-stu-id="42cd2-196">Try uploading the extension file of your policy, to verify that there aren't any issues so far.</span></span> <span data-ttu-id="42cd2-197">To upload the extension file of your policy:</span><span class="sxs-lookup"><span data-stu-id="42cd2-197">To upload the extension file of your policy:</span></span>

1. <span data-ttu-id="42cd2-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span><span class="sxs-lookup"><span data-stu-id="42cd2-198">In your Azure AD B2C tenant, go to the **All Policies** blade.</span></span>
2. <span data-ttu-id="42cd2-199">Select the **Overwrite the policy if it exists** check box.</span><span class="sxs-lookup"><span data-stu-id="42cd2-199">Select the **Overwrite the policy if it exists** check box.</span></span>
3. <span data-ttu-id="42cd2-200">Upload the extension file (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="42cd2-200">Upload the extension file (TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="42cd2-201">Ensure that it doesn't fail validation.</span><span class="sxs-lookup"><span data-stu-id="42cd2-201">Ensure that it doesn't fail validation.</span></span>

## <a name="register-the-salesforce-saml-claims-provider-to-a-user-journey"></a><span data-ttu-id="42cd2-202">Register the Salesforce SAML claims provider to a user journey</span><span class="sxs-lookup"><span data-stu-id="42cd2-202">Register the Salesforce SAML claims provider to a user journey</span></span>

<span data-ttu-id="42cd2-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span><span class="sxs-lookup"><span data-stu-id="42cd2-203">Next, add the Salesforce SAML identity provider to one of your user journeys.</span></span> <span data-ttu-id="42cd2-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span><span class="sxs-lookup"><span data-stu-id="42cd2-204">At this point, the identity provider has been set up, but it’s not available on any of the user sign-up or sign-in pages.</span></span> <span data-ttu-id="42cd2-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span><span class="sxs-lookup"><span data-stu-id="42cd2-205">To add the identity provider to a sign-in page, first, create a duplicate of an existing template user journey.</span></span> <span data-ttu-id="42cd2-206">Then, modify the template so that it also has the Azure AD identity provider.</span><span class="sxs-lookup"><span data-stu-id="42cd2-206">Then, modify the template so that it also has the Azure AD identity provider.</span></span>

1. <span data-ttu-id="42cd2-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span><span class="sxs-lookup"><span data-stu-id="42cd2-207">Open the base file of your policy (for example, TrustFrameworkBase.xml).</span></span>
2. <span data-ttu-id="42cd2-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span><span class="sxs-lookup"><span data-stu-id="42cd2-208">Find the `<UserJourneys>` element, and then copy the entire `<UserJourney>` value, including Id=”SignUpOrSignIn”.</span></span>
3. <span data-ttu-id="42cd2-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="42cd2-209">Open the extension file (for example, TrustFrameworkExtensions.xml).</span></span> <span data-ttu-id="42cd2-210">Find the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="42cd2-210">Find the `<UserJourneys>` element.</span></span> <span data-ttu-id="42cd2-211">If the element doesn't exist, create one.</span><span class="sxs-lookup"><span data-stu-id="42cd2-211">If the element doesn't exist, create one.</span></span>
4. <span data-ttu-id="42cd2-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span><span class="sxs-lookup"><span data-stu-id="42cd2-212">Paste the entire copied `<UserJourney>` as a child of the `<UserJourneys>` element.</span></span>
5. <span data-ttu-id="42cd2-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="42cd2-213">Rename the ID of the new `<UserJourney>` (for example, SignUpOrSignUsingContoso).</span></span>

### <a name="display-the-identity-provider-button"></a><span data-ttu-id="42cd2-214">Display the identity provider button</span><span class="sxs-lookup"><span data-stu-id="42cd2-214">Display the identity provider button</span></span>

<span data-ttu-id="42cd2-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span><span class="sxs-lookup"><span data-stu-id="42cd2-215">The `<ClaimsProviderSelection>` element is analogous to an identity provider button on a sign-up or sign-in page.</span></span> <span data-ttu-id="42cd2-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span><span class="sxs-lookup"><span data-stu-id="42cd2-216">By adding an `<ClaimsProviderSelection>` element for Salesforce, a new button appears when a user goes to this page.</span></span> <span data-ttu-id="42cd2-217">To display the identity provider button:</span><span class="sxs-lookup"><span data-stu-id="42cd2-217">To display the identity provider button:</span></span>

1. <span data-ttu-id="42cd2-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span><span class="sxs-lookup"><span data-stu-id="42cd2-218">In the `<UserJourney>` that you created, find the `<OrchestrationStep>` with `Order="1"`.</span></span>
2. <span data-ttu-id="42cd2-219">Add the following XML:</span><span class="sxs-lookup"><span data-stu-id="42cd2-219">Add the following XML:</span></span>

    ```XML
    <ClaimsProviderSelection TargetClaimsExchangeId="ContosoExchange" />
    ```

3. <span data-ttu-id="42cd2-220">Set `TargetClaimsExchangeId` to a logical value.</span><span class="sxs-lookup"><span data-stu-id="42cd2-220">Set `TargetClaimsExchangeId` to a logical value.</span></span> <span data-ttu-id="42cd2-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span><span class="sxs-lookup"><span data-stu-id="42cd2-221">We recommend following the same convention as others (for example, *\[ClaimProviderName\]Exchange*).</span></span>

### <a name="link-the-identity-provider-button-to-an-action"></a><span data-ttu-id="42cd2-222">Link the identity provider button to an action</span><span class="sxs-lookup"><span data-stu-id="42cd2-222">Link the identity provider button to an action</span></span>

<span data-ttu-id="42cd2-223">Now that you have an identity provider button in place, link it to an action.</span><span class="sxs-lookup"><span data-stu-id="42cd2-223">Now that you have an identity provider button in place, link it to an action.</span></span> <span data-ttu-id="42cd2-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span><span class="sxs-lookup"><span data-stu-id="42cd2-224">In this case, the action is for Azure AD B2C to communicate with Salesforce to receive a SAML token.</span></span> <span data-ttu-id="42cd2-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span><span class="sxs-lookup"><span data-stu-id="42cd2-225">You can do this by linking the technical profile for your Salesforce SAML claims provider:</span></span>

1. <span data-ttu-id="42cd2-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span><span class="sxs-lookup"><span data-stu-id="42cd2-226">In the `<UserJourney>` node, find the `<OrchestrationStep>` with `Order="2"`.</span></span>
2. <span data-ttu-id="42cd2-227">Add the following XML:</span><span class="sxs-lookup"><span data-stu-id="42cd2-227">Add the following XML:</span></span>

    ```XML
    <ClaimsExchange Id="ContosoExchange" TechnicalProfileReferenceId="ContosoProfile" />
    ```

3. <span data-ttu-id="42cd2-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span><span class="sxs-lookup"><span data-stu-id="42cd2-228">Update `Id` to the same value that you used earlier for `TargetClaimsExchangeId`.</span></span>
4. <span data-ttu-id="42cd2-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span><span class="sxs-lookup"><span data-stu-id="42cd2-229">Update `TechnicalProfileReferenceId` to the `Id` of the technical profile you created earlier (for example, ContosoProfile).</span></span>

### <a name="upload-the-updated-extension-file"></a><span data-ttu-id="42cd2-230">Upload the updated extension file</span><span class="sxs-lookup"><span data-stu-id="42cd2-230">Upload the updated extension file</span></span>

<span data-ttu-id="42cd2-231">You are done modifying the extension file.</span><span class="sxs-lookup"><span data-stu-id="42cd2-231">You are done modifying the extension file.</span></span> <span data-ttu-id="42cd2-232">Save and upload this file.</span><span class="sxs-lookup"><span data-stu-id="42cd2-232">Save and upload this file.</span></span> <span data-ttu-id="42cd2-233">Ensure that all validations succeed.</span><span class="sxs-lookup"><span data-stu-id="42cd2-233">Ensure that all validations succeed.</span></span>

### <a name="update-the-relying-party-file"></a><span data-ttu-id="42cd2-234">Update the relying party file</span><span class="sxs-lookup"><span data-stu-id="42cd2-234">Update the relying party file</span></span>

<span data-ttu-id="42cd2-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span><span class="sxs-lookup"><span data-stu-id="42cd2-235">Next, update the relying party (RP) file that initiates the user journey that you created:</span></span>

1. <span data-ttu-id="42cd2-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span><span class="sxs-lookup"><span data-stu-id="42cd2-236">Make a copy of SignUpOrSignIn.xml in your working directory.</span></span> <span data-ttu-id="42cd2-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span><span class="sxs-lookup"><span data-stu-id="42cd2-237">Then, rename it (for example, SignUpOrSignInWithAAD.xml).</span></span>
2. <span data-ttu-id="42cd2-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span><span class="sxs-lookup"><span data-stu-id="42cd2-238">Open the new file and update the `PolicyId` attribute for `<TrustFrameworkPolicy>` with a unique value.</span></span> <span data-ttu-id="42cd2-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span><span class="sxs-lookup"><span data-stu-id="42cd2-239">This is the name of your policy (for example, SignUpOrSignInWithAAD).</span></span>
3. <span data-ttu-id="42cd2-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span><span class="sxs-lookup"><span data-stu-id="42cd2-240">Modify the `ReferenceId` attribute in `<DefaultUserJourney>` to match the `Id` of the new user journey that you created (for example, SignUpOrSignUsingContoso).</span></span>
4. <span data-ttu-id="42cd2-241">Save your changes, and then upload the file.</span><span class="sxs-lookup"><span data-stu-id="42cd2-241">Save your changes, and then upload the file.</span></span>

## <a name="test-and-troubleshoot"></a><span data-ttu-id="42cd2-242">Test and troubleshoot</span><span class="sxs-lookup"><span data-stu-id="42cd2-242">Test and troubleshoot</span></span>

<span data-ttu-id="42cd2-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span><span class="sxs-lookup"><span data-stu-id="42cd2-243">To test the custom policy that you just uploaded, in the Azure portal, go to the policy blade, and then click **Run now**.</span></span> <span data-ttu-id="42cd2-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="42cd2-244">If it fails, see [Troubleshoot custom policies](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="42cd2-245">Next steps</span><span class="sxs-lookup"><span data-stu-id="42cd2-245">Next steps</span></span>

<span data-ttu-id="42cd2-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="42cd2-246">Provide feedback to [AADB2CPreview@microsoft.com](mailto:AADB2CPreview@microsoft.com).</span></span>
