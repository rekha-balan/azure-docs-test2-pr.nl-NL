---
title: Secure your RESTful services by using HTTP basic authentication in Azure Active Directory B2C | Microsoft Docs
description: Secure your custom REST API claims exchanges in your Azure AD B2C by using HTTP basic authentication.
services: active-directory-b2c
author: davidmu1
manager: mtillman
ms.service: active-directory
ms.workload: identity
ms.topic: conceptual
ms.date: 09/25/2017
ms.author: davidmu
ms.component: B2C
ms.openlocfilehash: f157602ce3a9c5b6f15a03ad816d8aece4e22805
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870919"
---
# <a name="secure-your-restful-services-by-using-http-basic-authentication"></a><span data-ttu-id="5eed1-103">Secure your RESTful services by using HTTP basic authentication</span><span class="sxs-lookup"><span data-stu-id="5eed1-103">Secure your RESTful services by using HTTP basic authentication</span></span>

[!INCLUDE [active-directory-b2c-advanced-audience-warning](../../includes/active-directory-b2c-advanced-audience-warning.md)]

<span data-ttu-id="5eed1-104">In a [related Azure AD B2C article](active-directory-b2c-custom-rest-api-netfw.md), you create a RESTful service (web API) that integrates with Azure Active Directory B2C (Azure AD B2C) user journeys without authentication.</span><span class="sxs-lookup"><span data-stu-id="5eed1-104">In a [related Azure AD B2C article](active-directory-b2c-custom-rest-api-netfw.md), you create a RESTful service (web API) that integrates with Azure Active Directory B2C (Azure AD B2C) user journeys without authentication.</span></span> 

<span data-ttu-id="5eed1-105">In this article, you add HTTP basic authentication to your RESTful service so that only verified users, including B2C, can access your API.</span><span class="sxs-lookup"><span data-stu-id="5eed1-105">In this article, you add HTTP basic authentication to your RESTful service so that only verified users, including B2C, can access your API.</span></span> <span data-ttu-id="5eed1-106">With HTTP basic authentication, you set the user credentials (app ID and app secret) in your custom policy.</span><span class="sxs-lookup"><span data-stu-id="5eed1-106">With HTTP basic authentication, you set the user credentials (app ID and app secret) in your custom policy.</span></span> 

<span data-ttu-id="5eed1-107">For more information, see [Basic authentication in ASP.NET web API](https://docs.microsoft.com/aspnet/web-api/overview/security/basic-authentication).</span><span class="sxs-lookup"><span data-stu-id="5eed1-107">For more information, see [Basic authentication in ASP.NET web API](https://docs.microsoft.com/aspnet/web-api/overview/security/basic-authentication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5eed1-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5eed1-108">Prerequisites</span></span>
<span data-ttu-id="5eed1-109">Complete the steps in the [Integrate REST API claims exchanges in your Azure AD B2C user journey](active-directory-b2c-custom-rest-api-netfw.md) article.</span><span class="sxs-lookup"><span data-stu-id="5eed1-109">Complete the steps in the [Integrate REST API claims exchanges in your Azure AD B2C user journey](active-directory-b2c-custom-rest-api-netfw.md) article.</span></span>

## <a name="step-1-add-authentication-support"></a><span data-ttu-id="5eed1-110">Step 1: Add authentication support</span><span class="sxs-lookup"><span data-stu-id="5eed1-110">Step 1: Add authentication support</span></span>

### <a name="step-11-add-application-settings-to-your-projects-webconfig-file"></a><span data-ttu-id="5eed1-111">Step 1.1: Add application settings to your project's web.config file</span><span class="sxs-lookup"><span data-stu-id="5eed1-111">Step 1.1: Add application settings to your project's web.config file</span></span>
1. <span data-ttu-id="5eed1-112">Open the Visual Studio project that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="5eed1-112">Open the Visual Studio project that you created earlier.</span></span> 

2. <span data-ttu-id="5eed1-113">Add the following application settings to the web.config file under the `appSettings` element:</span><span class="sxs-lookup"><span data-stu-id="5eed1-113">Add the following application settings to the web.config file under the `appSettings` element:</span></span>

    ```XML
    <add key="WebApp:ClientId" value="B2CServiceUserAccount" />
    <add key="WebApp:ClientSecret" value="your secret" />
    ```

3. <span data-ttu-id="5eed1-114">Create a password, and then set the `WebApp:ClientSecret` value.</span><span class="sxs-lookup"><span data-stu-id="5eed1-114">Create a password, and then set the `WebApp:ClientSecret` value.</span></span>

    <span data-ttu-id="5eed1-115">To generate a complex password, run the following PowerShell code.</span><span class="sxs-lookup"><span data-stu-id="5eed1-115">To generate a complex password, run the following PowerShell code.</span></span> <span data-ttu-id="5eed1-116">You can use any arbitrary value.</span><span class="sxs-lookup"><span data-stu-id="5eed1-116">You can use any arbitrary value.</span></span>

    ```PowerShell
    $bytes = New-Object Byte[] 32
    $rand = [System.Security.Cryptography.RandomNumberGenerator]::Create()
    $rand.GetBytes($bytes)
    $rand.Dispose()
    [System.Convert]::ToBase64String($bytes)
    ```

### <a name="step-12-install-owin-libraries"></a><span data-ttu-id="5eed1-117">Step 1.2: Install OWIN libraries</span><span class="sxs-lookup"><span data-stu-id="5eed1-117">Step 1.2: Install OWIN libraries</span></span>
<span data-ttu-id="5eed1-118">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console:</span><span class="sxs-lookup"><span data-stu-id="5eed1-118">To begin, add the OWIN middleware NuGet packages to the project by using the Visual Studio Package Manager Console:</span></span>

```
PM> Install-Package Microsoft.Owin
PM> Install-Package Owin
PM> Install-Package Microsoft.Owin.Host.SystemWeb
```

### <a name="step-13-add-an-authentication-middleware-class"></a><span data-ttu-id="5eed1-119">Step 1.3: Add an authentication middleware class</span><span class="sxs-lookup"><span data-stu-id="5eed1-119">Step 1.3: Add an authentication middleware class</span></span>
<span data-ttu-id="5eed1-120">Add the `ClientAuthMiddleware.cs` class under the *App_Start* folder.</span><span class="sxs-lookup"><span data-stu-id="5eed1-120">Add the `ClientAuthMiddleware.cs` class under the *App_Start* folder.</span></span> <span data-ttu-id="5eed1-121">To do so:</span><span class="sxs-lookup"><span data-stu-id="5eed1-121">To do so:</span></span>

1. <span data-ttu-id="5eed1-122">Right-click the *App_Start* folder, select **Add**, and then select **Class**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-122">Right-click the *App_Start* folder, select **Add**, and then select **Class**.</span></span>

   ![Add ClientAuthMiddleware.cs class in the App_Start folder](media/aadb2c-ief-rest-api-netfw-secure-basic/rest-api-netfw-secure-basic-OWIN-startup-auth1.png)

2. <span data-ttu-id="5eed1-124">In the **Name** box, type **ClientAuthMiddleware.cs**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-124">In the **Name** box, type **ClientAuthMiddleware.cs**.</span></span>

   ![Create new C# class](media/aadb2c-ief-rest-api-netfw-secure-basic/rest-api-netfw-secure-basic-OWIN-startup-auth2.png)

3. <span data-ttu-id="5eed1-126">Open the *App_Start\ClientAuthMiddleware.cs* file, and replace the file content with following code:</span><span class="sxs-lookup"><span data-stu-id="5eed1-126">Open the *App_Start\ClientAuthMiddleware.cs* file, and replace the file content with following code:</span></span>

    ```csharp
    
    using Microsoft.Owin;
    using System;
    using System.Collections.Generic;
    using System.Configuration;
    using System.Linq;
    using System.Security.Principal;
    using System.Text;
    using System.Threading.Tasks;
    using System.Web;
    
    namespace Contoso.AADB2C.API
    {
        /// <summary>
        /// Class to create a custom owin middleware to check for client authentication
        /// </summary>
        public class ClientAuthMiddleware
        {
            private static readonly string ClientID = ConfigurationManager.AppSettings["WebApp:ClientId"];
            private static readonly string ClientSecret = ConfigurationManager.AppSettings["WebApp:ClientSecret"];
    
            /// <summary>
            /// Gets or sets the next owin middleware
            /// </summary>
            private Func<IDictionary<string, object>, Task> Next { get; set; }
    
            /// <summary>
            /// Initializes a new instance of the <see cref="ClientAuthMiddleware"/> class.
            /// </summary>
            /// <param name="next"></param>
            public ClientAuthMiddleware(Func<IDictionary<string, object>, Task> next)
            {
                this.Next = next;
            }
    
            /// <summary>
            /// Invoke client authentication middleware during each request.
            /// </summary>
            /// <param name="environment">Owin environment</param>
            /// <returns></returns>
            public Task Invoke(IDictionary<string, object> environment)
            {
                // Get wrapper class for the environment
                var context = new OwinContext(environment);
    
                // Check whether the authorization header is available. This contains the credentials.
                var authzValue = context.Request.Headers.Get("Authorization");
                if (string.IsNullOrEmpty(authzValue) || !authzValue.StartsWith("Basic ", StringComparison.OrdinalIgnoreCase))
                {
                    // Process next middleware
                    return Next(environment);
                }
    
                // Get credentials
                var creds = authzValue.Substring("Basic ".Length).Trim();
                string clientId;
                string clientSecret;
    
                if (RetrieveCreds(creds, out clientId, out clientSecret))
                {
                    // Set transaction authenticated as client
                    context.Request.User = new GenericPrincipal(new GenericIdentity(clientId, "client"), new string[] { "client" });
                }
    
                return Next(environment);
            }
    
            /// <summary>
            /// Retrieve credentials from header
            /// </summary>
            /// <param name="credentials">Authorization header</param>
            /// <param name="clientId">Client identifier</param>
            /// <param name="clientSecret">Client secret</param>
            /// <returns>True if valid credentials were presented</returns>
            private bool RetrieveCreds(string credentials, out string clientId, out string clientSecret)
            {
                string pair;
                clientId = clientSecret = string.Empty;
    
                try
                {
                    pair = Encoding.UTF8.GetString(Convert.FromBase64String(credentials));
                }
                catch (FormatException)
                {
                    return false;
                }
                catch (ArgumentException)
                {
                    return false;
                }
    
                var ix = pair.IndexOf(':');
                if (ix == -1)
                {
                    return false;
                }
    
                clientId = pair.Substring(0, ix);
                clientSecret = pair.Substring(ix + 1);
    
                // Return whether credentials are valid
                return (string.Compare(clientId, ClientAuthMiddleware.ClientID) == 0 &&
                    string.Compare(clientSecret, ClientAuthMiddleware.ClientSecret) == 0);
            }
        }
    }
    ```

### <a name="step-14-add-an-owin-startup-class"></a><span data-ttu-id="5eed1-127">Step 1.4: Add an OWIN startup class</span><span class="sxs-lookup"><span data-stu-id="5eed1-127">Step 1.4: Add an OWIN startup class</span></span>
<span data-ttu-id="5eed1-128">Add an OWIN startup class named `Startup.cs` to the API.</span><span class="sxs-lookup"><span data-stu-id="5eed1-128">Add an OWIN startup class named `Startup.cs` to the API.</span></span> <span data-ttu-id="5eed1-129">To do so:</span><span class="sxs-lookup"><span data-stu-id="5eed1-129">To do so:</span></span>
1. <span data-ttu-id="5eed1-130">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-130">Right-click the project, select **Add** > **New Item**, and then search for **OWIN**.</span></span>

   ![Add an OWIN startup class](media/aadb2c-ief-rest-api-netfw-secure-basic/rest-api-netfw-secure-basic-OWIN-startup.png)

2. <span data-ttu-id="5eed1-132">Open the *Startup.cs* file, and replace the file content with following code:</span><span class="sxs-lookup"><span data-stu-id="5eed1-132">Open the *Startup.cs* file, and replace the file content with following code:</span></span>

    ```csharp
    using Microsoft.Owin;
    using Owin;
    
    [assembly: OwinStartup(typeof(Contoso.AADB2C.API.Startup))]
    namespace Contoso.AADB2C.API
    {
        public class Startup
        {
            public void Configuration(IAppBuilder app)
            {
                    app.Use<ClientAuthMiddleware>();
            }
        }
    }
    ```

### <a name="step-15-protect-the-identity-api-class"></a><span data-ttu-id="5eed1-133">Step 1.5: Protect the Identity API class</span><span class="sxs-lookup"><span data-stu-id="5eed1-133">Step 1.5: Protect the Identity API class</span></span>
<span data-ttu-id="5eed1-134">Open Controllers\IdentityController.cs, and add the `[Authorize]` tag to the controller class.</span><span class="sxs-lookup"><span data-stu-id="5eed1-134">Open Controllers\IdentityController.cs, and add the `[Authorize]` tag to the controller class.</span></span> <span data-ttu-id="5eed1-135">This tag restricts access to the controller to users who meet the authorization requirement.</span><span class="sxs-lookup"><span data-stu-id="5eed1-135">This tag restricts access to the controller to users who meet the authorization requirement.</span></span>

![Add the Authorize tag to the controller](media/aadb2c-ief-rest-api-netfw-secure-basic/rest-api-netfw-secure-basic-authorize.png)

## <a name="step-2-publish-to-azure"></a><span data-ttu-id="5eed1-137">Step 2: Publish to Azure</span><span class="sxs-lookup"><span data-stu-id="5eed1-137">Step 2: Publish to Azure</span></span>
<span data-ttu-id="5eed1-138">To publish your project, in Solution Explorer, right-click the **Contoso.AADB2C.API** project, and then select **Publish**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-138">To publish your project, in Solution Explorer, right-click the **Contoso.AADB2C.API** project, and then select **Publish**.</span></span>

## <a name="step-3-add-the-restful-services-app-id-and-app-secret-to-azure-ad-b2c"></a><span data-ttu-id="5eed1-139">Step 3: Add the RESTful services app ID and app secret to Azure AD B2C</span><span class="sxs-lookup"><span data-stu-id="5eed1-139">Step 3: Add the RESTful services app ID and app secret to Azure AD B2C</span></span>
<span data-ttu-id="5eed1-140">After your RESTful service is protected by the client ID (username) and secret, you must store the credentials in your Azure AD B2C tenant.</span><span class="sxs-lookup"><span data-stu-id="5eed1-140">After your RESTful service is protected by the client ID (username) and secret, you must store the credentials in your Azure AD B2C tenant.</span></span> <span data-ttu-id="5eed1-141">Your custom policy provides the credentials when it invokes your RESTful services.</span><span class="sxs-lookup"><span data-stu-id="5eed1-141">Your custom policy provides the credentials when it invokes your RESTful services.</span></span> 

### <a name="step-31-add-a-restful-services-client-id"></a><span data-ttu-id="5eed1-142">Step 3.1: Add a RESTful services client ID</span><span class="sxs-lookup"><span data-stu-id="5eed1-142">Step 3.1: Add a RESTful services client ID</span></span>
1. <span data-ttu-id="5eed1-143">In your Azure AD B2C tenant, select **B2C Settings** > **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-143">In your Azure AD B2C tenant, select **B2C Settings** > **Identity Experience Framework**.</span></span>


2. <span data-ttu-id="5eed1-144">Select **Policy Keys** to view the keys that are available in your tenant.</span><span class="sxs-lookup"><span data-stu-id="5eed1-144">Select **Policy Keys** to view the keys that are available in your tenant.</span></span>

3. <span data-ttu-id="5eed1-145">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-145">Select **Add**.</span></span>

4. <span data-ttu-id="5eed1-146">For **Options**, select **Manual**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-146">For **Options**, select **Manual**.</span></span>

5. <span data-ttu-id="5eed1-147">For **Name**, type **B2cRestClientId**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-147">For **Name**, type **B2cRestClientId**.</span></span>  
    <span data-ttu-id="5eed1-148">The prefix *B2C_1A_* might be added automatically.</span><span class="sxs-lookup"><span data-stu-id="5eed1-148">The prefix *B2C_1A_* might be added automatically.</span></span>

6. <span data-ttu-id="5eed1-149">In the **Secret** box, enter the app ID that you defined earlier.</span><span class="sxs-lookup"><span data-stu-id="5eed1-149">In the **Secret** box, enter the app ID that you defined earlier.</span></span>

7. <span data-ttu-id="5eed1-150">For **Key usage**, select **Secret**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-150">For **Key usage**, select **Secret**.</span></span>

8. <span data-ttu-id="5eed1-151">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-151">Select **Create**.</span></span>

9. <span data-ttu-id="5eed1-152">Confirm that you've created the `B2C_1A_B2cRestClientId` key.</span><span class="sxs-lookup"><span data-stu-id="5eed1-152">Confirm that you've created the `B2C_1A_B2cRestClientId` key.</span></span>

### <a name="step-32-add-a-restful-services-client-secret"></a><span data-ttu-id="5eed1-153">Step 3.2: Add a RESTful services client secret</span><span class="sxs-lookup"><span data-stu-id="5eed1-153">Step 3.2: Add a RESTful services client secret</span></span>
1. <span data-ttu-id="5eed1-154">In your Azure AD B2C tenant, select **B2C Settings** > **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-154">In your Azure AD B2C tenant, select **B2C Settings** > **Identity Experience Framework**.</span></span>

2. <span data-ttu-id="5eed1-155">Select **Policy Keys** to view the keys available in your tenant.</span><span class="sxs-lookup"><span data-stu-id="5eed1-155">Select **Policy Keys** to view the keys available in your tenant.</span></span>

3. <span data-ttu-id="5eed1-156">Select **Add**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-156">Select **Add**.</span></span>

4. <span data-ttu-id="5eed1-157">For **Options**, select **Manual**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-157">For **Options**, select **Manual**.</span></span>

5. <span data-ttu-id="5eed1-158">For **Name**, type **B2cRestClientSecret**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-158">For **Name**, type **B2cRestClientSecret**.</span></span>  
    <span data-ttu-id="5eed1-159">The prefix *B2C_1A_* might be added automatically.</span><span class="sxs-lookup"><span data-stu-id="5eed1-159">The prefix *B2C_1A_* might be added automatically.</span></span>

6. <span data-ttu-id="5eed1-160">In the **Secret** box, enter the app secret that you defined earlier.</span><span class="sxs-lookup"><span data-stu-id="5eed1-160">In the **Secret** box, enter the app secret that you defined earlier.</span></span>

7. <span data-ttu-id="5eed1-161">For **Key usage**, select **Secret**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-161">For **Key usage**, select **Secret**.</span></span>

8. <span data-ttu-id="5eed1-162">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-162">Select **Create**.</span></span>

9. <span data-ttu-id="5eed1-163">Confirm that you've created the `B2C_1A_B2cRestClientSecret` key.</span><span class="sxs-lookup"><span data-stu-id="5eed1-163">Confirm that you've created the `B2C_1A_B2cRestClientSecret` key.</span></span>

## <a name="step-4-change-the-technical-profile-to-support-basic-authentication-in-your-extension-policy"></a><span data-ttu-id="5eed1-164">Step 4: Change the technical profile to support basic authentication in your extension policy</span><span class="sxs-lookup"><span data-stu-id="5eed1-164">Step 4: Change the technical profile to support basic authentication in your extension policy</span></span>
1. <span data-ttu-id="5eed1-165">In your working directory, open the extension policy file (TrustFrameworkExtensions.xml).</span><span class="sxs-lookup"><span data-stu-id="5eed1-165">In your working directory, open the extension policy file (TrustFrameworkExtensions.xml).</span></span>

2. <span data-ttu-id="5eed1-166">Search for the `<TechnicalProfile>` node that includes `Id="REST-API-SignUp"`.</span><span class="sxs-lookup"><span data-stu-id="5eed1-166">Search for the `<TechnicalProfile>` node that includes `Id="REST-API-SignUp"`.</span></span>

3. <span data-ttu-id="5eed1-167">Locate the `<Metadata>` element.</span><span class="sxs-lookup"><span data-stu-id="5eed1-167">Locate the `<Metadata>` element.</span></span>

4. <span data-ttu-id="5eed1-168">Change the *AuthenticationType* to *Basic*, as follows:</span><span class="sxs-lookup"><span data-stu-id="5eed1-168">Change the *AuthenticationType* to *Basic*, as follows:</span></span>
    ```xml
    <Item Key="AuthenticationType">Basic</Item>
    ```

5. <span data-ttu-id="5eed1-169">Immediately after the closing `<Metadata>` element, add the following XML snippet:</span><span class="sxs-lookup"><span data-stu-id="5eed1-169">Immediately after the closing `<Metadata>` element, add the following XML snippet:</span></span> 

    ```xml
    <CryptographicKeys>
        <Key Id="BasicAuthenticationUsername" StorageReferenceId="B2C_1A_B2cRestClientId" />
        <Key Id="BasicAuthenticationPassword" StorageReferenceId="B2C_1A_B2cRestClientSecret" />
    </CryptographicKeys>
    ```
    <span data-ttu-id="5eed1-170">After you add the snippet, your technical profile should look like the following XML code:</span><span class="sxs-lookup"><span data-stu-id="5eed1-170">After you add the snippet, your technical profile should look like the following XML code:</span></span>
    
    ![Add basic authentication XML elements](media/aadb2c-ief-rest-api-netfw-secure-basic/rest-api-netfw-secure-basic-add-1.png)

## <a name="step-5-upload-the-policy-to-your-tenant"></a><span data-ttu-id="5eed1-172">Step 5: Upload the policy to your tenant</span><span class="sxs-lookup"><span data-stu-id="5eed1-172">Step 5: Upload the policy to your tenant</span></span>

1. <span data-ttu-id="5eed1-173">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open **Azure AD B2C**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-173">In the [Azure portal](https://portal.azure.com), switch to the [context of your Azure AD B2C tenant](active-directory-b2c-navigate-to-b2c-context.md), and then open **Azure AD B2C**.</span></span>

2. <span data-ttu-id="5eed1-174">Select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-174">Select **Identity Experience Framework**.</span></span>

3. <span data-ttu-id="5eed1-175">Open **All Policies**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-175">Open **All Policies**.</span></span>

4. <span data-ttu-id="5eed1-176">Select **Upload Policy**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-176">Select **Upload Policy**.</span></span>

5. <span data-ttu-id="5eed1-177">Select the **Overwrite the policy if it exists** check box.</span><span class="sxs-lookup"><span data-stu-id="5eed1-177">Select the **Overwrite the policy if it exists** check box.</span></span>

6. <span data-ttu-id="5eed1-178">Upload the *TrustFrameworkExtensions.xml* file, and then ensure that it passes validation.</span><span class="sxs-lookup"><span data-stu-id="5eed1-178">Upload the *TrustFrameworkExtensions.xml* file, and then ensure that it passes validation.</span></span>

## <a name="step-6-test-the-custom-policy-by-using-run-now"></a><span data-ttu-id="5eed1-179">Step 6: Test the custom policy by using Run Now</span><span class="sxs-lookup"><span data-stu-id="5eed1-179">Step 6: Test the custom policy by using Run Now</span></span>
1. <span data-ttu-id="5eed1-180">Open **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-180">Open **Azure AD B2C Settings**, and then select **Identity Experience Framework**.</span></span>

    >[!NOTE]
    ><span data-ttu-id="5eed1-181">Run Now requires at least one application to be preregistered on the tenant.</span><span class="sxs-lookup"><span data-stu-id="5eed1-181">Run Now requires at least one application to be preregistered on the tenant.</span></span> <span data-ttu-id="5eed1-182">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span><span class="sxs-lookup"><span data-stu-id="5eed1-182">To learn how to register applications, see the Azure AD B2C [Get started](active-directory-b2c-get-started.md) article or the [Application registration](active-directory-b2c-app-registration.md) article.</span></span>

2. <span data-ttu-id="5eed1-183">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span><span class="sxs-lookup"><span data-stu-id="5eed1-183">Open **B2C_1A_signup_signin**, the relying party (RP) custom policy that you uploaded, and then select **Run now**.</span></span>

3. <span data-ttu-id="5eed1-184">Test the process by typing **Test** in the **Given Name** box.</span><span class="sxs-lookup"><span data-stu-id="5eed1-184">Test the process by typing **Test** in the **Given Name** box.</span></span>  
    <span data-ttu-id="5eed1-185">Azure AD B2C displays an error message at the top of the window.</span><span class="sxs-lookup"><span data-stu-id="5eed1-185">Azure AD B2C displays an error message at the top of the window.</span></span>

    ![Test your identity API](media/aadb2c-ief-rest-api-netfw-secure-basic/rest-api-netfw-test.png)

4. <span data-ttu-id="5eed1-187">In the **Given Name** box, type a name (other than "Test").</span><span class="sxs-lookup"><span data-stu-id="5eed1-187">In the **Given Name** box, type a name (other than "Test").</span></span>  
    <span data-ttu-id="5eed1-188">Azure AD B2C signs up the user and then sends a loyalty number to your application.</span><span class="sxs-lookup"><span data-stu-id="5eed1-188">Azure AD B2C signs up the user and then sends a loyalty number to your application.</span></span> <span data-ttu-id="5eed1-189">Note the number in this example:</span><span class="sxs-lookup"><span data-stu-id="5eed1-189">Note the number in this example:</span></span>

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

## <a name="optional-download-the-complete-policy-files-and-code"></a><span data-ttu-id="5eed1-190">(Optional) Download the complete policy files and code</span><span class="sxs-lookup"><span data-stu-id="5eed1-190">(Optional) Download the complete policy files and code</span></span>
* <span data-ttu-id="5eed1-191">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span><span class="sxs-lookup"><span data-stu-id="5eed1-191">After you complete the [Get started with custom policies](active-directory-b2c-get-started-custom.md) walkthrough, we recommend that you build your scenario by using your own custom policy files.</span></span> <span data-ttu-id="5eed1-192">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw-secure-basic).</span><span class="sxs-lookup"><span data-stu-id="5eed1-192">For your reference, we have provided [Sample policy files](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw-secure-basic).</span></span>
* <span data-ttu-id="5eed1-193">You can download the complete code from [Sample Visual Studio solution for reference](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw/Contoso.AADB2C.API).</span><span class="sxs-lookup"><span data-stu-id="5eed1-193">You can download the complete code from [Sample Visual Studio solution for reference](https://github.com/Azure-Samples/active-directory-b2c-custom-policy-starterpack/tree/master/scenarios/aadb2c-ief-rest-api-netfw/Contoso.AADB2C.API).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5eed1-194">Next steps</span><span class="sxs-lookup"><span data-stu-id="5eed1-194">Next steps</span></span>
* [<span data-ttu-id="5eed1-195">Use client certificates to secure your RESTful API</span><span class="sxs-lookup"><span data-stu-id="5eed1-195">Use client certificates to secure your RESTful API</span></span>](active-directory-b2c-custom-rest-api-netfw-secure-cert.md)

