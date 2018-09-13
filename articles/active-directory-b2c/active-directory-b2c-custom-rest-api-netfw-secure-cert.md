---
title: Secure your RESTful service by using client certificates in Azure Active Directory B2C | Microsoft Docs
description: Secure your custom REST API claims exchanges in your Azure AD B2C by using client certificates
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 09/25/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: 7bf7add75f60bf64f64119979e5eee81be0f6e7b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869183"
---
# <a name="secure-your-restful-service-by-using-client-certificates"></a><span data-ttu-id="04867-103">Secure your RESTful service by using client certificates</span><span class="sxs-lookup"><span data-stu-id="04867-103">Secure your RESTful service by using client certificates</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="04867-104">In a related article, you [create a RESTful service](active-directory-b2c-custom-rest-api-netfw.md) that interacts with Azure Active Directory B2C (Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="04867-104">In a related article, you [create a RESTful service](active-directory-b2c-custom-rest-api-netfw.md) that interacts with Azure Active Directory B2C (Azure AD B2C).</span></span>

<span data-ttu-id="04867-105">In this article, you learn how to restrict access to your Azure web app (RESTful API) by using a client certificate.</span><span class="sxs-lookup"><span data-stu-id="04867-105">In this article, you learn how to restrict access to your Azure web app (RESTful API) by using a client certificate.</span></span> <span data-ttu-id="04867-106">This mechanism is called TLS mutual authentication, or *client certificate authentication*.</span><span class="sxs-lookup"><span data-stu-id="04867-106">This mechanism is called TLS mutual authentication, or *client certificate authentication*.</span></span> <span data-ttu-id="04867-107">Only services that have proper certificates, such as Azure AD B2C, can access your service.</span><span class="sxs-lookup"><span data-stu-id="04867-107">Only services that have proper certificates, such as Azure AD B2C, can access your service.</span></span>

>[!NOTE]
><span data-ttu-id="04867-108">You can also secure your RESTful service by using [HTTP basic authentication](active-directory-b2c-custom-rest-api-netfw-secure-basic.md).</span><span class="sxs-lookup"><span data-stu-id="04867-108">You can also secure your RESTful service by using [HTTP basic authentication](active-directory-b2c-custom-rest-api-netfw-secure-basic.md).</span></span> <span data-ttu-id="04867-109">However, HTTP basic authentication is considered less secure over a client certificate.</span><span class="sxs-lookup"><span data-stu-id="04867-109">However, HTTP basic authentication is considered less secure over a client certificate.</span></span> <span data-ttu-id="04867-110">Our recommendation is to secure the RESTful service by using client certificate authentication as described in this article.</span><span class="sxs-lookup"><span data-stu-id="04867-110">Our recommendation is to secure the RESTful service by using client certificate authentication as described in this article.</span></span>

<span data-ttu-id="04867-111">This article details how to:</span><span class="sxs-lookup"><span data-stu-id="04867-111">This article details how to:</span></span>
* <span data-ttu-id="04867-112">Set up your web app to use client certificate authentication.</span><span class="sxs-lookup"><span data-stu-id="04867-112">Set up your web app to use client certificate authentication.</span></span>
* <span data-ttu-id="04867-113">Upload the certificate to Azure AD B2C policy keys.</span><span class="sxs-lookup"><span data-stu-id="04867-113">Upload the certificate to Azure AD B2C policy keys.</span></span>
* <span data-ttu-id="04867-114">Configure your custom policy to use the client certificate.</span><span class="sxs-lookup"><span data-stu-id="04867-114">Configure your custom policy to use the client certificate.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04867-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="04867-115">Prerequisites</span></span>
* <span data-ttu-id="04867-116">Complete the steps in the [Integrate REST API claims exchanges](active-directory-b2c-custom-rest-api-netfw.md) article.</span><span class="sxs-lookup"><span data-stu-id="04867-116">Complete the steps in the [Integrate REST API claims exchanges](active-directory-b2c-custom-rest-api-netfw.md) article.</span></span>
* <span data-ttu-id="04867-117">Get a valid certificate (a .pfx file with a private key).</span><span class="sxs-lookup"><span data-stu-id="04867-117">Get a valid certificate (a .pfx file with a private key).</span></span>

## <a name="step-1-configure-a-web-app-for-client-certificate-authentication"></a><span data-ttu-id="04867-118">Step 1: Configure a web app for client certificate authentication</span><span class="sxs-lookup"><span data-stu-id="04867-118">Step 1: Configure a web app for client certificate authentication</span></span>
<span data-ttu-id="04867-119">To set up **Azure App Service** to require client certificates, set the web app `clientCertEnabled` site setting to *true*.</span><span class="sxs-lookup"><span data-stu-id="04867-119">To set up **Azure App Service** to require client certificates, set the web app `clientCertEnabled` site setting to *true*.</span></span> <span data-ttu-id="04867-120">To make this change, in the Azure portal, open your web app page.</span><span class="sxs-lookup"><span data-stu-id="04867-120">To make this change, in the Azure portal, open your web app page.</span></span> <span data-ttu-id="04867-121">In the left navigation, under **Settings** select **SSL Settings**.</span><span class="sxs-lookup"><span data-stu-id="04867-121">In the left navigation, under **Settings** select **SSL Settings**.</span></span> <span data-ttu-id="04867-122">In the **Client Certificates** section, turn on the **Incoming client certificate** option.</span><span class="sxs-lookup"><span data-stu-id="04867-122">In the **Client Certificates** section, turn on the **Incoming client certificate** option.</span></span>

>[!NOTE]
><span data-ttu-id="04867-123">Make sure that your Azure App Service plan is Standard or greater.</span><span class="sxs-lookup"><span data-stu-id="04867-123">Make sure that your Azure App Service plan is Standard or greater.</span></span> <span data-ttu-id="04867-124">For more information, see [Azure App Service plans in-depth overview](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span><span class="sxs-lookup"><span data-stu-id="04867-124">For more information, see [Azure App Service plans in-depth overview](https://docs.microsoft.com/azure/app-service/azure-web-sites-web-hosting-plans-in-depth-overview).</span></span>

>[!NOTE]
><span data-ttu-id="04867-125">For more information about setting the **clientCertEnabled** property, see [Configure TLS mutual authentication for web apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth).</span><span class="sxs-lookup"><span data-stu-id="04867-125">For more information about setting the **clientCertEnabled** property, see [Configure TLS mutual authentication for web apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth).</span></span>

## <a name="step-2-upload-your-certificate-to-azure-ad-b2c-policy-keys"></a><span data-ttu-id="04867-126">Step 2: Upload your certificate to Azure AD B2C policy keys</span><span class="sxs-lookup"><span data-stu-id="04867-126">Step 2: Upload your certificate to Azure AD B2C policy keys</span></span>
<span data-ttu-id="04867-127">After you set `clientCertEnabled` to *true*, the communication with your RESTful API requires a client certificate.</span><span class="sxs-lookup"><span data-stu-id="04867-127">After you set `clientCertEnabled` to *true*, the communication with your RESTful API requires a client certificate.</span></span> <span data-ttu-id="04867-128">To obtain, upload, and store the client certificate in your Azure AD B2C tenant, do the following:</span><span class="sxs-lookup"><span data-stu-id="04867-128">To obtain, upload, and store the client certificate in your Azure AD B2C tenant, do the following:</span></span> 
1. <span data-ttu-id="04867-129">In your Azure AD B2C tenant, select **B2C Settings** > **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="04867-129">In your Azure AD B2C tenant, select **B2C Settings** > **Identity Experience Framework**.</span></span>

2. <span data-ttu-id="04867-130">To view the keys that are available in your tenant, select **Policy Keys**.</span><span class="sxs-lookup"><span data-stu-id="04867-130">To view the keys that are available in your tenant, select **Policy Keys**.</span></span>

3. <span data-ttu-id="04867-131">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="04867-131">Select **Add**.</span></span>  
    <span data-ttu-id="04867-132">The **Create a key** window opens.</span><span class="sxs-lookup"><span data-stu-id="04867-132">The **Create a key** window opens.</span></span>

4. <span data-ttu-id="04867-133">In the **Options** box, select **Upload**.</span><span class="sxs-lookup"><span data-stu-id="04867-133">In the **Options** box, select **Upload**.</span></span>

5. <span data-ttu-id="04867-134">In the **Name** box, type **B2cRestClientCertificate**.</span><span class="sxs-lookup"><span data-stu-id="04867-134">In the **Name** box, type **B2cRestClientCertificate**.</span></span>  
    <span data-ttu-id="04867-135">The prefix *B2C_1A_* is added automatically.</span><span class="sxs-lookup"><span data-stu-id="04867-135">The prefix *B2C_1A_* is added automatically.</span></span>

6. <span data-ttu-id="04867-136">In the **File upload** box, select your certificate's .pfx file with a private key.</span><span class="sxs-lookup"><span data-stu-id="04867-136">In the **File upload** box, select your certificate's .pfx file with a private key.</span></span>

7. <span data-ttu-id="04867-137">In the **Password** box, type the certificate's password.</span><span class="sxs-lookup"><span data-stu-id="04867-137">In the **Password** box, type the certificate's password.</span></span>

    ![Upload policy key](media/aadb2c-ief-rest-api-netfw-secure-cert/rest-api-netfw-secure-client-cert-upload.png)

7. <span data-ttu-id="04867-139">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="04867-139">Select **Create**.</span></span>

8. <span data-ttu-id="04867-140">To view the keys that are available in your tenant and confirm that you've created the `B2C_1A_B2cRestClientCertificate` key, select **Policy Keys**.</span><span class="sxs-lookup"><span data-stu-id="04867-140">To view the keys that are available in your tenant and confirm that you've created the `B2C_1A_B2cRestClientCertificate` key, select **Policy Keys**.</span></span>

## <a name="step-3-change-the-technical-profile"></a><span data-ttu-id="04867-141">Step 3: Change the technical profile</span><span class="sxs-lookup"><span data-stu-id="04867-141">Step 3: Change the technical profile</span></span>
<span data-ttu-id="04867-142">To support client certificate authentication in your custom policy, change the technical profile by doing the following:</span><span class="sxs-lookup"><span data-stu-id="04867-142">To support client certificate authentication in your custom policy, change the technical profile by doing the following:</span></span>

1. <span data-ttu-id="04867-143">In your working directory, open the *TrustFrameworkExtensions.xml* extension policy file.</span><span class="sxs-lookup"><span data-stu-id="04867-143">In your working directory, open the *TrustFrameworkExtensions.xml* extension policy file.</span></span>

2. <span data-ttu-id="04867-144">Search for the `<TechnicalProfile>` node that includes `Id="REST-API-SignUp"`.</span><span class="sxs-lookup"><span data-stu-id="04867-144">Search for the `<TechnicalProfile>` node that includes `Id="REST-API-SignUp"`.</span></span>

3. <span data-ttu-id="04867-145">Locate the `<Metadata>` element.</span><span class="sxs-lookup"><span data-stu-id="04867-145">Locate the `<Metadata>` element.</span></span>

4. <span data-ttu-id="04867-146">Change the *AuthenticationType* to *ClientCertificate*, as follows:</span><span class="sxs-lookup"><span data-stu-id="04867-146">Change the *AuthenticationType* to *ClientCertificate*, as follows:</span></span>

    ```xml
    <Item Key="AuthenticationType">ClientCertificate</Item>
    ```

5. <span data-ttu-id="04867-147">Immediately after the closing `<Metadata>` element, add the following XML snippet:</span><span class="sxs-lookup"><span data-stu-id="04867-147">Immediately after the closing `<Metadata>` element, add the following XML snippet:</span></span> 

    ```xml
    <CryptographicKeys>
        <Key Id="ClientCertificate" StorageReferenceId="B2C_1A_B2cRestClientCertificate" />
    </CryptographicKeys>
    ```

    <span data-ttu-id="04867-148">After you add the snippet, your technical profile should look like the following XML code:</span><span class="sxs-lookup"><span data-stu-id="04867-148">After you add the snippet, your technical profile should look like the following XML code:</span></span>

    ![Set ClientCertificate authentication XML elements](media/aadb2c-ief-rest-api-netfw-secure-cert/rest-api-netfw-secure-client-cert-tech-profile.png)

## <a name="step-4-upload-the-policy-to-your-tenant"></a><span data-ttu-id="04867-150">Step 4: Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="04867-150">Step 4: Upload the policy to your tenant</span></span>

1. <span data-ttu-id="04867-151">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then select **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="04867-151">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then select **Azure AD B2C**.</span></span>

2. <span data-ttu-id="04867-152">Select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="04867-152">Select **Identity Experience Framework**.</span></span>

3. <span data-ttu-id="04867-153">Select **All Policies**.</span><span class="sxs-lookup"><span data-stu-id="04867-153">Select **All Policies**.</span></span>

4. <span data-ttu-id="04867-154">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="04867-154">Select **Upload Policy**.</span></span>

5. <span data-ttu-id="04867-155">Select the **Overwrite the policy if it exists** check box.</span><span class="sxs-lookup"><span data-stu-id="04867-155">Select the **Overwrite the policy if it exists** check box.</span></span>

6. <span data-ttu-id="04867-156">Upload the *TrustFrameworkExtensions.xml* file, and then ensure that it passes validation.</span><span class="sxs-lookup"><span data-stu-id="04867-156">Upload the *TrustFrameworkExtensions.xml* file, and then ensure that it passes validation.</span></span>

## <a name="step-5-test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="04867-157">Step 5: Test the custom policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="04867-157">Step 5: Test the custom policy by using Run Now</span></span>
1. <span data-ttu-id="04867-158">Open **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="04867-158">Open **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="04867-159">Run Now requires at least one application to be preregistered on the tenant.</span><span class="sxs-lookup"><span data-stu-id="04867-159">Run Now requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="04867-160">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span><span class="sxs-lookup"><span data-stu-id="04867-160">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>

2. <span data-ttu-id="04867-161">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="04867-161">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span></span>

3. <span data-ttu-id="04867-162">Test the process by typing **Test** in the **Given Name** box.</span><span class="sxs-lookup"><span data-stu-id="04867-162">Test the process by typing **Test** in the **Given Name** box.</span></span>  
    <span data-ttu-id="04867-163">Azure AD B2C displays an error message at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="04867-163">Azure AD B2C displays an error message at the top of the window.</span></span>    

    ![Test your identity API](media/aadb2c-ief-rest-api-netfw-secure-basic/rest-api-netfw-test.png)

4. <span data-ttu-id="04867-165">In the **Given Name** box, type a name (other than "Test").</span><span class="sxs-lookup"><span data-stu-id="04867-165">In the **Given Name** box, type a name (other than "Test").</span></span>  
    <span data-ttu-id="04867-166">Azure AD B2C signs up the user and then sends a loyalty number to your application.</span><span class="sxs-lookup"><span data-stu-id="04867-166">Azure AD B2C signs up the user and then sends a loyalty number to your application.</span></span> <span data-ttu-id="04867-167">Note the number in this JWT example:</span><span class="sxs-lookup"><span data-stu-id="04867-167">Note the number in this JWT example:</span></span>

   ```
   {
     "typ": "JWT",
     "alg": "RS256",
     "kid": "X5eXk4xyojNFum1kl2Ytv8dlNP4-c57dO6QGTVBwaNk"
   }.{
     "exp": 1507125903,
     "nbf": 1507122303,
     "ver": "1.0",
     "iss": "https://contoso.b2clogin.com/f06c2fe8-709f-4030-85dc-38a4bfd9e82d/v2.0/",
     "aud": "e1d2612f-c2bc-4599-8e7b-d874eaca1ee1",
     "acr": "b2c_1a_signup_signin",
     "nonce": "defaultNonce",
     "iat": 1507122303,
     "auth_time": 1507122303,
     "loyaltyNumber": "290",
     "given_name": "Emily",
     "emails": ["B2cdemo@outlook.com"]
   }
   ```

   >[!NOTE]
   ><span data-ttu-id="04867-168">If you receive the error message, *The name is not valid, please provide a valid name*, it means that Azure AD B2C successfully called your RESTful service while it presented the client certificate.</span><span class="sxs-lookup"><span data-stu-id="04867-168">If you receive the error message, *The name is not valid, please provide a valid name*, it means that Azure AD B2C successfully called your RESTful service while it presented the client certificate.</span></span> <span data-ttu-id="04867-169">The next step is to validate the certificate.</span><span class="sxs-lookup"><span data-stu-id="04867-169">The next step is to validate the certificate.</span></span>

## <a name="step-6-add-certificate-validation"></a><span data-ttu-id="04867-170">Step 6: Add certificate validation</span><span class="sxs-lookup"><span data-stu-id="04867-170">Step 6: Add certificate validation</span></span>
<span data-ttu-id="04867-171">The client certificate that Azure AD B2C sends to your RESTful service does not undergo validation by the Azure Web Apps platform, except to check whether the certificate exists.</span><span class="sxs-lookup"><span data-stu-id="04867-171">The client certificate that Azure AD B2C sends to your RESTful service does not undergo validation by the Azure Web Apps platform, except to check whether the certificate exists.</span></span> <span data-ttu-id="04867-172">Validating the certificate is the responsibility of the web app.</span><span class="sxs-lookup"><span data-stu-id="04867-172">Validating the certificate is the responsibility of the web app.</span></span> 

<span data-ttu-id="04867-173">In this section, you add sample ASP.NET code that validates the certificate properties for authentication purposes.</span><span class="sxs-lookup"><span data-stu-id="04867-173">In this section, you add sample ASP.NET code that validates the certificate properties for authentication purposes.</span></span>

> [!NOTE]
><span data-ttu-id="04867-174">For more information about configuring Azure App Service for client certificate authentication, see [Configure TLS mutual authentication for web apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth).</span><span class="sxs-lookup"><span data-stu-id="04867-174">For more information about configuring Azure App Service for client certificate authentication, see [Configure TLS mutual authentication for web apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-configure-tls-mutual-auth).</span></span>

### <a name="61-add-application-settings-to-your-projects-webconfig-file"></a><span data-ttu-id="04867-175">6.1 Add application settings to your project's web.config file</span><span class="sxs-lookup"><span data-stu-id="04867-175">6.1 Add application settings to your project's web.config file</span></span>
<span data-ttu-id="04867-176">In the Visual Studio project that you created earlier, add the following application settings to the *web.config* file after the `appSettings` element:</span><span class="sxs-lookup"><span data-stu-id="04867-176">In the Visual Studio project that you created earlier, add the following application settings to the *web.config* file after the `appSettings` element:</span></span>

```XML
<add key="ClientCertificate:Subject" value="CN=Subject name" />
<add key="ClientCertificate:Issuer" value="CN=Issuer name" />
<add key="ClientCertificate:Thumbprint" value="Certificate thumbprint" />
```

<span data-ttu-id="04867-177">Replace the certificate's **Subject name**, **Issuer name**, and **Certificate thumbprint** values with your certificate values.</span><span class="sxs-lookup"><span data-stu-id="04867-177">Replace the certificate's **Subject name**, **Issuer name**, and **Certificate thumbprint** values with your certificate values.</span></span>

### <a name="62-add-the-isvalidclientcertificate-function"></a><span data-ttu-id="04867-178">6.2 Add the IsValidClientCertificate function</span><span class="sxs-lookup"><span data-stu-id="04867-178">6.2 Add the IsValidClientCertificate function</span></span>
<span data-ttu-id="04867-179">Open the *Controllers\IdentityController.cs* file, and then add to the `Identity` controller class the following function:</span><span class="sxs-lookup"><span data-stu-id="04867-179">Open the *Controllers\IdentityController.cs* file, and then add to the `Identity` controller class the following function:</span></span> 

```csharp
private bool IsValidClientCertificate()
{
    string ClientCertificateSubject = ConfigurationManager.AppSettings["ClientCertificate:Subject"];
    string ClientCertificateIssuer = ConfigurationManager.AppSettings["ClientCertificate:Issuer"];
    string ClientCertificateThumbprint = ConfigurationManager.AppSettings["ClientCertificate:Thumbprint"];

    X509Certificate2 clientCertInRequest = RequestContext.ClientCertificate;
    if (clientCertInRequest == null)
    {
        Trace.WriteLine("Certificate is NULL");
        return false;
    }

    // Basic verification
    if (clientCertInRequest.Verify() == false)
    {
        Trace.TraceError("Basic verification failed");
        return false;
    }

    // 1. Check the time validity of the certificate
    if (DateTime.Compare(DateTime.Now, clientCertInRequest.NotBefore) < 0 ||
        DateTime.Compare(DateTime.Now, clientCertInRequest.NotAfter) > 0)
    {
        Trace.TraceError($"NotBefore '{clientCertInRequest.NotBefore}' or NotAfter '{clientCertInRequest.NotAfter}' not valid");
        return false;
    }

    // 2. Check the subject name of the certificate
    bool foundSubject = false;
    string[] certSubjectData = clientCertInRequest.Subject.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
    foreach (string s in certSubjectData)
    {
        if (String.Compare(s.Trim(), ClientCertificateSubject) == 0)
        {
            foundSubject = true;
            break;
        }
    }

    if (!foundSubject)
    {
        Trace.TraceError($"Subject name '{clientCertInRequest.Subject}' is not valid");
        return false;
    }
    
    // 3. Check the issuer name of the certificate
    bool foundIssuerCN = false;
    string[] certIssuerData = clientCertInRequest.Issuer.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries);
    foreach (string s in certIssuerData)
    {
        if (String.Compare(s.Trim(), ClientCertificateIssuer) == 0)
        {
            foundIssuerCN = true;
            break;
        }
    }

    if (!foundIssuerCN)
    {
        Trace.TraceError($"Issuer '{clientCertInRequest.Issuer}' is not valid");
        return false;
    }

    // 4. Check the thumbprint of the certificate
    if (String.Compare(clientCertInRequest.Thumbprint.Trim().ToUpper(), ClientCertificateThumbprint) != 0)
    {
        Trace.TraceError($"Thumbprint '{clientCertInRequest.Thumbprint.Trim().ToUpper()}' is not valid");
        return false;
    }

    // 5. If you also want to test whether the certificate chains to a trusted root authority, you can uncomment the following code:
    //
    //X509Chain certChain = new X509Chain();
    //certChain.Build(certificate);
    //bool isValidCertChain = true;
    //foreach (X509ChainElement chElement in certChain.ChainElements)
    //{
    //    if (!chElement.Certificate.Verify())
    //    {
    //        isValidCertChain = false;
    //        break;
    //    }
    //}
    //if (!isValidCertChain) return false;
    return true;
}
```

<span data-ttu-id="04867-180">In the preceding sample code, we accept the certificate as valid only if all the following conditions are met:</span><span class="sxs-lookup"><span data-stu-id="04867-180">In the preceding sample code, we accept the certificate as valid only if all the following conditions are met:</span></span>
* <span data-ttu-id="04867-181">The certificate is not expired and is active for the current time on server.</span><span class="sxs-lookup"><span data-stu-id="04867-181">The certificate is not expired and is active for the current time on server.</span></span>
* <span data-ttu-id="04867-182">The `Subject` name of the certificate is equal to the `ClientCertificate:Subject` application setting value.</span><span class="sxs-lookup"><span data-stu-id="04867-182">The `Subject` name of the certificate is equal to the `ClientCertificate:Subject` application setting value.</span></span>
* <span data-ttu-id="04867-183">The `Issuer` name of the certificate is equal to the `ClientCertificate:Issuer` application setting value.</span><span class="sxs-lookup"><span data-stu-id="04867-183">The `Issuer` name of the certificate is equal to the `ClientCertificate:Issuer` application setting value.</span></span>
* <span data-ttu-id="04867-184">The `thumbprint` of the certificate is equal to the `ClientCertificate:Thumbprint` application setting value.</span><span class="sxs-lookup"><span data-stu-id="04867-184">The `thumbprint` of the certificate is equal to the `ClientCertificate:Thumbprint` application setting value.</span></span>

>[!IMPORTANT]
><span data-ttu-id="04867-185">Depending on the sensitivity of your service, you might need to add more validations.</span><span class="sxs-lookup"><span data-stu-id="04867-185">Depending on the sensitivity of your service, you might need to add more validations.</span></span> <span data-ttu-id="04867-186">For example, you might need to test whether the certificate chains to a trusted root authority, issuer organization name validation, and so on.</span><span class="sxs-lookup"><span data-stu-id="04867-186">For example, you might need to test whether the certificate chains to a trusted root authority, issuer organization name validation, and so on.</span></span>

### <a name="63-call-the-isvalidclientcertificate-function"></a><span data-ttu-id="04867-187">6.3 Call the IsValidClientCertificate function</span><span class="sxs-lookup"><span data-stu-id="04867-187">6.3 Call the IsValidClientCertificate function</span></span>
<span data-ttu-id="04867-188">Open the *Controllers\IdentityController.cs* file and then, at the beginning of the `SignUp()` function, add the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="04867-188">Open the *Controllers\IdentityController.cs* file and then, at the beginning of the `SignUp()` function, add the following code snippet:</span></span> 

```csharp
if (IsValidClientCertificate() == false)
{
    return Content(HttpStatusCode.Conflict, new B2CResponseContent("Your client certificate is not valid", HttpStatusCode.Conflict));
}
```

<span data-ttu-id="04867-189">After you add the snippet, your `Identity` controller should look like the following code:</span><span class="sxs-lookup"><span data-stu-id="04867-189">After you add the snippet, your `Identity` controller should look like the following code:</span></span>

![Add certificate validation code](media/aadb2c-ief-rest-api-netfw-secure-cert/rest-api-netfw-secure-client-code.png)

## <a name="step-7-publish-your-project-to-azure-and-test-it"></a><span data-ttu-id="04867-191">Step 7: Publish your project to Azure and test it</span><span class="sxs-lookup"><span data-stu-id="04867-191">Step 7: Publish your project to Azure and test it</span></span>
1. <span data-ttu-id="04867-192">In **Solution Explorer**, right-click the **Contoso.AADB2C.API** project, and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="04867-192">In **Solution Explorer**, right-click the **Contoso.AADB2C.API** project, and then select **Publish**.</span></span>

2. <span data-ttu-id="04867-193">Repeat "Step 6," and re-test your custom policy with the certificate validation.</span><span class="sxs-lookup"><span data-stu-id="04867-193">Repeat "Step 6," and re-test your custom policy with the certificate validation.</span></span> <span data-ttu-id="04867-194">Try to run the policy, and make sure that everything works after you add the validation.</span><span class="sxs-lookup"><span data-stu-id="04867-194">Try to run the policy, and make sure that everything works after you add the validation.</span></span>

3. <span data-ttu-id="04867-195">In your *web.config* file, change the value of `ClientCertificate:Subject` to **invalid**.</span><span class="sxs-lookup"><span data-stu-id="04867-195">In your *web.config* file, change the value of `ClientCertificate:Subject` to **invalid**.</span></span> <span data-ttu-id="04867-196">Run the policy again and you should see an error message.</span><span class="sxs-lookup"><span data-stu-id="04867-196">Run the policy again and you should see an error message.</span></span>

4. <span data-ttu-id="04867-197">Change the value back to **valid**, and make sure that the policy can call your REST API.</span><span class="sxs-lookup"><span data-stu-id="04867-197">Change the value back to **valid**, and make sure that the policy can call your REST API.</span></span>

<span data-ttu-id="04867-198">If you need to troubleshoot this step, see [Collecting logs by using Application Insights](active-directory-b2c-troubleshoot-custom.md).</span><span class="sxs-lookup"><span data-stu-id="04867-198">If you need to troubleshoot this step, see [Collecting logs by using Application Insights](active-directory-b2c-troubleshoot-custom.md).</span></span>

## <a name="optional-download-the-complete-policy-files-and-code"></a><span data-ttu-id="04867-199">(Optional) Download the complete policy files and code</span><span class="sxs-lookup"><span data-stu-id="04867-199">(Optional) Download the complete policy files and code</span></span>
* <span data-ttu-id="04867-200">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span><span class="sxs-lookup"><span data-stu-id="04867-200">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span></span> <span data-ttu-id="04867-201">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw-secure-cert).</span><span class="sxs-lookup"><span data-stu-id="04867-201">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw-secure-cert).</span></span>
* <span data-ttu-id="04867-202">You can download the complete code from [Sample Visual Studio solution for reference](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw/Contoso.AADB2C.API).</span><span class="sxs-lookup"><span data-stu-id="04867-202">You can download the complete code from [Sample Visual Studio solution for reference](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw/Contoso.AADB2C.API).</span></span> 
