---
title: Use Azure Active Directory to authenticate Batch Management solutions | Microsoft Docs
description: Applications built with Azure resource manager and the Batch resource provider authenticate with Azure AD.
services: batch
documentationcenter: .net
author: dlepow
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: ''
ms.workload: big-compute
ms.date: 04/27/2017
ms.author: danlep
ms.openlocfilehash: 698212ce1f4e88cda741a78030023f3acdeee9f0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866851"
---
# <a name="authenticate-batch-management-solutions-with-active-directory"></a><span data-ttu-id="c900c-103">Authenticate Batch Management solutions with Active Directory</span><span class="sxs-lookup"><span data-stu-id="c900c-103">Authenticate Batch Management solutions with Active Directory</span></span>

<span data-ttu-id="c900c-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="c900c-104">Applications that call the Azure Batch Management service authenticate with [Azure Active Directory][aad_about] (Azure AD).</span></span> <span data-ttu-id="c900c-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span><span class="sxs-lookup"><span data-stu-id="c900c-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="c900c-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span><span class="sxs-lookup"><span data-stu-id="c900c-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="c900c-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span><span class="sxs-lookup"><span data-stu-id="c900c-107">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="c900c-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span><span class="sxs-lookup"><span data-stu-id="c900c-108">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> <span data-ttu-id="c900c-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="c900c-109">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="c900c-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span><span class="sxs-lookup"><span data-stu-id="c900c-110">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library.</span></span> <span data-ttu-id="c900c-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span><span class="sxs-lookup"><span data-stu-id="c900c-111">We show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="c900c-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span><span class="sxs-lookup"><span data-stu-id="c900c-112">We use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span>

<span data-ttu-id="c900c-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c900c-113">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

## <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="c900c-114">Register your application with Azure AD</span><span class="sxs-lookup"><span data-stu-id="c900c-114">Register your application with Azure AD</span></span>

<span data-ttu-id="c900c-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span><span class="sxs-lookup"><span data-stu-id="c900c-115">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="c900c-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="c900c-116">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="c900c-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="c900c-117">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="c900c-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span><span class="sxs-lookup"><span data-stu-id="c900c-118">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="c900c-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/app-objects-and-service-principals.md).</span><span class="sxs-lookup"><span data-stu-id="c900c-119">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/app-objects-and-service-principals.md).</span></span>

<span data-ttu-id="c900c-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="c900c-120">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/quickstart-v1-integrate-apps-with-azure-ad.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="c900c-121">Specify **Native Client Application** for the type of application.</span><span class="sxs-lookup"><span data-stu-id="c900c-121">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="c900c-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span><span class="sxs-lookup"><span data-stu-id="c900c-122">The industry standard OAuth 2.0 URI for the **Redirect URI** is `urn:ietf:wg:oauth:2.0:oob`.</span></span> <span data-ttu-id="c900c-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span><span class="sxs-lookup"><span data-stu-id="c900c-123">However, you can specify any valid URI (such as `http://myaccountmanagementsample`) for the **Redirect URI**, as it does not need to be a real endpoint:</span></span>

![](./media/batch-aad-auth-management/app-registration-management-plane.png)

<span data-ttu-id="c900c-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span><span class="sxs-lookup"><span data-stu-id="c900c-124">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](./media/batch-aad-auth-management/app-registration-client-id.png)

## <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="c900c-125">Grant the Azure Resource Manager API access to your application</span><span class="sxs-lookup"><span data-stu-id="c900c-125">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="c900c-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="c900c-126">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="c900c-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span><span class="sxs-lookup"><span data-stu-id="c900c-127">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="c900c-128">Follow these steps in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="c900c-128">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="c900c-129">In the left-hand navigation pane of the Azure portal, choose **All services**, click **App Registrations**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c900c-129">In the left-hand navigation pane of the Azure portal, choose **All services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="c900c-130">Search for the name of your application in the list of app registrations:</span><span class="sxs-lookup"><span data-stu-id="c900c-130">Search for the name of your application in the list of app registrations:</span></span>

    ![Search for your application name](./media/batch-aad-auth-management/search-app-registration.png)

3. <span data-ttu-id="c900c-132">Display the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="c900c-132">Display the **Settings** blade.</span></span> <span data-ttu-id="c900c-133">In the **API Access** section, select **Required permissions**.</span><span class="sxs-lookup"><span data-stu-id="c900c-133">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="c900c-134">Click **Add** to add a new required permission.</span><span class="sxs-lookup"><span data-stu-id="c900c-134">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="c900c-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="c900c-135">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="c900c-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="c900c-136">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="c900c-137">Click the **Done** button.</span><span class="sxs-lookup"><span data-stu-id="c900c-137">Click the **Done** button.</span></span>

<span data-ttu-id="c900c-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span><span class="sxs-lookup"><span data-stu-id="c900c-138">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="c900c-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c900c-139">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![Delegate permissions to the Azure Resource Manager API](./media/batch-aad-auth-management/required-permissions-management-plane.png)

## <a name="azure-ad-endpoints"></a><span data-ttu-id="c900c-141">Azure AD endpoints</span><span class="sxs-lookup"><span data-stu-id="c900c-141">Azure AD endpoints</span></span>

<span data-ttu-id="c900c-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span><span class="sxs-lookup"><span data-stu-id="c900c-142">To authenticate your Batch Management solutions with Azure AD, you'll need two well-known endpoints.</span></span>

- <span data-ttu-id="c900c-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span><span class="sxs-lookup"><span data-stu-id="c900c-143">The **Azure AD common endpoint** provides a generic credential gathering interface when a specific tenant is not provided, as in the case of integrated authentication:</span></span>

    `https://login.microsoftonline.com/common`

- <span data-ttu-id="c900c-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span><span class="sxs-lookup"><span data-stu-id="c900c-144">The **Azure Resource Manager endpoint** is used to acquire a token for authenticating requests to the Batch management service:</span></span>

    `https://management.core.windows.net/`

<span data-ttu-id="c900c-145">The AccountManagement sample application defines constants for these endpoints.</span><span class="sxs-lookup"><span data-stu-id="c900c-145">The AccountManagement sample application defines constants for these endpoints.</span></span> <span data-ttu-id="c900c-146">Leave these constants unchanged:</span><span class="sxs-lookup"><span data-stu-id="c900c-146">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure Resource Manager endpoint 
private const string ResourceUri = "https://management.core.windows.net/";
```

## <a name="reference-your-application-id"></a><span data-ttu-id="c900c-147">Reference your application ID</span><span class="sxs-lookup"><span data-stu-id="c900c-147">Reference your application ID</span></span> 

<span data-ttu-id="c900c-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span><span class="sxs-lookup"><span data-stu-id="c900c-148">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="c900c-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span><span class="sxs-lookup"><span data-stu-id="c900c-149">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="c900c-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span><span class="sxs-lookup"><span data-stu-id="c900c-150">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="c900c-151">Also copy the redirect URI that you specified during the registration process.</span><span class="sxs-lookup"><span data-stu-id="c900c-151">Also copy the redirect URI that you specified during the registration process.</span></span> <span data-ttu-id="c900c-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span><span class="sxs-lookup"><span data-stu-id="c900c-152">The redirect URI specified in your code must match the redirect URI that you provided when you registered the application.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

## <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="c900c-153">Acquire an Azure AD authentication token</span><span class="sxs-lookup"><span data-stu-id="c900c-153">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="c900c-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c900c-154">After you register the AccountManagement sample in the Azure AD tenant and update the sample source code with your values, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="c900c-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span><span class="sxs-lookup"><span data-stu-id="c900c-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="c900c-156">At this step, it prompts you for your Microsoft credentials:</span><span class="sxs-lookup"><span data-stu-id="c900c-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

```csharp
// Obtain an access token using the "common" AAD resource. This allows the application
// to query AAD for information that lies outside the application's tenant (such as for
// querying subscription information in your Azure account).
AuthenticationContext authContext = new AuthenticationContext(AuthorityUri);
AuthenticationResult authResult = authContext.AcquireToken(ResourceUri,
                                                        ClientId,
                                                        new Uri(RedirectUri),
                                                        PromptBehavior.Auto);
```

<span data-ttu-id="c900c-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span><span class="sxs-lookup"><span data-stu-id="c900c-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c900c-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="c900c-158">Next steps</span></span>

<span data-ttu-id="c900c-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="c900c-159">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="c900c-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="c900c-160">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="c900c-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span><span class="sxs-lookup"><span data-stu-id="c900c-161">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>

<span data-ttu-id="c900c-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span><span class="sxs-lookup"><span data-stu-id="c900c-162">To authenticate Batch service applications using Azure AD, see [Authenticate Batch service solutions with Active Directory](batch-aad-auth.md).</span></span> 


[aad_about]:../active-directory/fundamentals/active-directory-whatis.md "What is Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]:../active-directory/develop/authentication-scenarios.md "Authentication Scenarios for Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md
