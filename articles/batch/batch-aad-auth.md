---
title: Use Azure Active Directory to authenticate from Azure Batch | Microsoft Docs
description: Batch supports Azure AD for authentication from the Batch service and Batch resource provider.
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 03/16/2017
ms.author: tamram
ms.openlocfilehash: ea90a1c251128d9b4ad357c2430eb5f6a2572cbf
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552946"
---
# <a name="authenticate-from-batch-solutions-with-active-directory"></a><span data-ttu-id="9b768-103">Authenticate from Batch solutions with Active Directory</span><span class="sxs-lookup"><span data-stu-id="9b768-103">Authenticate from Batch solutions with Active Directory</span></span>

<span data-ttu-id="9b768-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD) for the Batch service and the Batch management service.</span><span class="sxs-lookup"><span data-stu-id="9b768-104">Azure Batch supports authentication with [Azure Active Directory][aad_about] (Azure AD) for the Batch service and the Batch management service.</span></span> <span data-ttu-id="9b768-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span><span class="sxs-lookup"><span data-stu-id="9b768-105">Azure AD is Microsoft’s multi-tenant cloud based directory and identity management service.</span></span> <span data-ttu-id="9b768-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span><span class="sxs-lookup"><span data-stu-id="9b768-106">Azure itself uses Azure AD for the authentication of its customers, service administrators, and organizational users.</span></span>

<span data-ttu-id="9b768-107">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library or the Batch .NET library.</span><span class="sxs-lookup"><span data-stu-id="9b768-107">In this article, we explore using Azure AD to authenticate from applications that use the Batch Management .NET library or the Batch .NET library.</span></span> <span data-ttu-id="9b768-108">In the context of the Batch .NET APIs, we show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span><span class="sxs-lookup"><span data-stu-id="9b768-108">In the context of the Batch .NET APIs, we show how to use Azure AD to authenticate a subscription administrator or co-administrator, using integrated authentication.</span></span> <span data-ttu-id="9b768-109">The authenticated user can then issue requests to Azure Batch.</span><span class="sxs-lookup"><span data-stu-id="9b768-109">The authenticated user can then issue requests to Azure Batch.</span></span>

<span data-ttu-id="9b768-110">It's also possible to use Azure AD to authenticate access to an application running unattended.</span><span class="sxs-lookup"><span data-stu-id="9b768-110">It's also possible to use Azure AD to authenticate access to an application running unattended.</span></span> <span data-ttu-id="9b768-111">Here we focus on using Azure AD integrated authentication, and refer you to other resources to learn about authenticating unattended applications.</span><span class="sxs-lookup"><span data-stu-id="9b768-111">Here we focus on using Azure AD integrated authentication, and refer you to other resources to learn about authenticating unattended applications.</span></span>

## <a name="use-azure-ad-with-batch-management-solutions"></a><span data-ttu-id="9b768-112">Use Azure AD with Batch management solutions</span><span class="sxs-lookup"><span data-stu-id="9b768-112">Use Azure AD with Batch management solutions</span></span>

<span data-ttu-id="9b768-113">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span><span class="sxs-lookup"><span data-stu-id="9b768-113">The Batch Management .NET library exposes types for working with Batch accounts, account keys, applications, and application packages.</span></span> <span data-ttu-id="9b768-114">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span><span class="sxs-lookup"><span data-stu-id="9b768-114">The Batch Management .NET library is an Azure resource provider client, and is used together with [Azure Resource Manager][resman_overview] to manage these resources programmatically.</span></span> 

<span data-ttu-id="9b768-115">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span><span class="sxs-lookup"><span data-stu-id="9b768-115">Azure AD is required to authenticate requests made through any Azure resource provider client, including the Batch Management .NET library, and through [Azure Resource Manager][resman_overview].</span></span>

<span data-ttu-id="9b768-116">In this section, we use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span><span class="sxs-lookup"><span data-stu-id="9b768-116">In this section, we use the [AccountManagment][acct_mgmt_sample] sample project, available on GitHub, to walk through using Azure AD with the Batch Management .NET library.</span></span> <span data-ttu-id="9b768-117">The AccountManagement sample is a console application that accesses a subscription programmatically, creates a resource group and a new Batch account, and performs some operations on the account.</span><span class="sxs-lookup"><span data-stu-id="9b768-117">The AccountManagement sample is a console application that accesses a subscription programmatically, creates a resource group and a new Batch account, and performs some operations on the account.</span></span> 

<span data-ttu-id="9b768-118">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9b768-118">To learn more about using the Batch Management .NET library and the AccountManagement sample, see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

### <a name="register-your-application-with-azure-ad"></a><span data-ttu-id="9b768-119">Register your application with Azure AD</span><span class="sxs-lookup"><span data-stu-id="9b768-119">Register your application with Azure AD</span></span>

<span data-ttu-id="9b768-120">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span><span class="sxs-lookup"><span data-stu-id="9b768-120">The Azure [Active Directory Authentication Library][aad_adal] (ADAL) provides a programmatic interface to Azure AD for use within your applications.</span></span> <span data-ttu-id="9b768-121">To call ADAL from your application, you must register your application in an Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="9b768-121">To call ADAL from your application, you must register your application in an Azure AD tenant.</span></span> <span data-ttu-id="9b768-122">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="9b768-122">When you register your application, you supply Azure AD with information about your application, including a name for it within the Azure AD tenant.</span></span> <span data-ttu-id="9b768-123">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span><span class="sxs-lookup"><span data-stu-id="9b768-123">Azure AD then provides an application ID that you use to associate your application with Azure AD at runtime.</span></span> <span data-ttu-id="9b768-124">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span><span class="sxs-lookup"><span data-stu-id="9b768-124">To learn more about the application ID, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md).</span></span>

<span data-ttu-id="9b768-125">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="9b768-125">To register the AccountManagement sample application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="9b768-126">Specify **Native Client Application** for the type of application.</span><span class="sxs-lookup"><span data-stu-id="9b768-126">Specify **Native Client Application** for the type of application.</span></span> <span data-ttu-id="9b768-127">For the **Redirect URI**, you can specify any valid URI (such as `http://myaccountmanagementsample`), as it does not need to be a real endpoint:</span><span class="sxs-lookup"><span data-stu-id="9b768-127">For the **Redirect URI**, you can specify any valid URI (such as `http://myaccountmanagementsample`), as it does not need to be a real endpoint:</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-aad-auth/app-registration-management-plane.png)

<span data-ttu-id="9b768-128">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span><span class="sxs-lookup"><span data-stu-id="9b768-128">Once you complete the registration process, you'll see the application ID and the object (service principal) ID listed for your application.</span></span>  

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-aad-auth/app-registration-client-id.png)

### <a name="update-your-code-to-reference-your-application-id"></a><span data-ttu-id="9b768-129">Update your code to reference your application ID</span><span class="sxs-lookup"><span data-stu-id="9b768-129">Update your code to reference your application ID</span></span> 

<span data-ttu-id="9b768-130">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span><span class="sxs-lookup"><span data-stu-id="9b768-130">Your client application uses the application ID (also referred to as the client ID) to access Azure AD at runtime.</span></span> <span data-ttu-id="9b768-131">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span><span class="sxs-lookup"><span data-stu-id="9b768-131">Once you've registered your application in the Azure portal, update your code to use the application ID provided by Azure AD for your registered application.</span></span> <span data-ttu-id="9b768-132">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span><span class="sxs-lookup"><span data-stu-id="9b768-132">In the AccountManagement sample application, copy your application ID from the Azure portal to the appropriate constant:</span></span>

```csharp
// Specify the unique identifier (the "Client ID") for your application. This is required so that your
// native client application (i.e. this sample) can access the Microsoft Azure AD Graph API. For information
// about registering an application in Azure Active Directory, please see "Adding an Application" here:
// https://azure.microsoft.com/documentation/articles/active-directory-integrating-applications/
private const string ClientId = "<application-id>";
```
<span data-ttu-id="9b768-133">Also copy the redirect URI that you specified during the registration process.</span><span class="sxs-lookup"><span data-stu-id="9b768-133">Also copy the redirect URI that you specified during the registration process.</span></span>

```csharp
// The URI to which Azure AD will redirect in response to an OAuth 2.0 request. This value is
// specified by you when you register an application with AAD (see ClientId comment). It does not
// need to be a real endpoint, but must be a valid URI (e.g. https://accountmgmtsampleapp).
private const string RedirectUri = "http://myaccountmanagementsample";
```

### <a name="grant-the-azure-resource-manager-api-access-to-your-application"></a><span data-ttu-id="9b768-134">Grant the Azure Resource Manager API access to your application</span><span class="sxs-lookup"><span data-stu-id="9b768-134">Grant the Azure Resource Manager API access to your application</span></span>

<span data-ttu-id="9b768-135">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span><span class="sxs-lookup"><span data-stu-id="9b768-135">Next, you'll need to delegate access to your application to the Azure Resource Manager API.</span></span> <span data-ttu-id="9b768-136">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span><span class="sxs-lookup"><span data-stu-id="9b768-136">The Azure AD identifier for the Resource Manager API is **Windows Azure Service Management API**.</span></span>

<span data-ttu-id="9b768-137">Follow these steps in the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="9b768-137">Follow these steps in the Azure portal:</span></span>

1. <span data-ttu-id="9b768-138">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="9b768-138">In the left-hand navigation pane of the Azure portal, choose **More Services**, click **App Registrations**, and click **Add**.</span></span>
2. <span data-ttu-id="9b768-139">Search for the name of your application in the list of app registrations:</span><span class="sxs-lookup"><span data-stu-id="9b768-139">Search for the name of your application in the list of app registrations:</span></span>

    ![Search for your application name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-aad-auth/search-app-registration.png)

3. <span data-ttu-id="9b768-141">Display the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="9b768-141">Display the **Settings** blade.</span></span> <span data-ttu-id="9b768-142">In the **API Access** section, select **Required permissions**.</span><span class="sxs-lookup"><span data-stu-id="9b768-142">In the **API Access** section, select **Required permissions**.</span></span>
4. <span data-ttu-id="9b768-143">Click **Add** to add a new required permission.</span><span class="sxs-lookup"><span data-stu-id="9b768-143">Click **Add** to add a new required permission.</span></span> 
5. <span data-ttu-id="9b768-144">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="9b768-144">In step 1, enter **Windows Azure Service Management API**, select that API from the list of results, and click the **Select** button.</span></span>
6. <span data-ttu-id="9b768-145">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="9b768-145">In step 2, select the check box next to **Access Azure classic deployment model as organization users**, and click the **Select** button.</span></span>
7. <span data-ttu-id="9b768-146">Click the **Done** button.</span><span class="sxs-lookup"><span data-stu-id="9b768-146">Click the **Done** button.</span></span>

<span data-ttu-id="9b768-147">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span><span class="sxs-lookup"><span data-stu-id="9b768-147">The **Required Permissions** blade now shows that permissions to your application are granted to both the ADAL and Resource Manager APIs.</span></span> <span data-ttu-id="9b768-148">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b768-148">Permissions are granted to ADAL by default when you first register your app with Azure AD.</span></span>

![Delegate permissions to the Azure Resource Manager API](https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-aad-auth/required-permissions-management-plane.png)


### <a name="acquire-an-azure-ad-authentication-token"></a><span data-ttu-id="9b768-150">Acquire an Azure AD authentication token</span><span class="sxs-lookup"><span data-stu-id="9b768-150">Acquire an Azure AD authentication token</span></span>

<span data-ttu-id="9b768-151">The AccountManagement sample application defines constants that provide the endpoint for Azure AD and for Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="9b768-151">The AccountManagement sample application defines constants that provide the endpoint for Azure AD and for Azure Resource Manager.</span></span> <span data-ttu-id="9b768-152">The sample application uses these constants to query Azure AD for subscription information.</span><span class="sxs-lookup"><span data-stu-id="9b768-152">The sample application uses these constants to query Azure AD for subscription information.</span></span> <span data-ttu-id="9b768-153">Leave these constants unchanged:</span><span class="sxs-lookup"><span data-stu-id="9b768-153">Leave these constants unchanged:</span></span>

```csharp
// Azure Active Directory "common" endpoint.
private const string AuthorityUri = "https://login.microsoftonline.com/common";
// Azure service management resource 
private const string ResourceUri = "https://management.core.windows.net/";
```

<span data-ttu-id="9b768-154">After you register the AccountManagement sample in the Azure AD tenant and provide the necessary values within the sample source code, the sample is ready to authenticate using Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b768-154">After you register the AccountManagement sample in the Azure AD tenant and provide the necessary values within the sample source code, the sample is ready to authenticate using Azure AD.</span></span> <span data-ttu-id="9b768-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span><span class="sxs-lookup"><span data-stu-id="9b768-155">When you run the sample, the ADAL attempts to acquire an authentication token.</span></span> <span data-ttu-id="9b768-156">At this step, it prompts you for your Microsoft credentials:</span><span class="sxs-lookup"><span data-stu-id="9b768-156">At this step, it prompts you for your Microsoft credentials:</span></span> 

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

<span data-ttu-id="9b768-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span><span class="sxs-lookup"><span data-stu-id="9b768-157">After you provide your credentials, the sample application can proceed to issue authenticated requests to the Batch management service.</span></span> 

## <a name="use-azure-ad-with-batch-service-solutions"></a><span data-ttu-id="9b768-158">Use Azure AD with Batch service solutions</span><span class="sxs-lookup"><span data-stu-id="9b768-158">Use Azure AD with Batch service solutions</span></span>

<span data-ttu-id="9b768-159">The Batch .NET library provides types for building parallel processing workflows with the Batch service.</span><span class="sxs-lookup"><span data-stu-id="9b768-159">The Batch .NET library provides types for building parallel processing workflows with the Batch service.</span></span> <span data-ttu-id="9b768-160">The Batch service supports both [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) authentication and authentication through Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b768-160">The Batch service supports both [Shared Key](https://docs.microsoft.com/rest/api/batchservice/authenticate-requests-to-the-azure-batch-service) authentication and authentication through Azure AD.</span></span> <span data-ttu-id="9b768-161">In this section, we discuss authentication via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b768-161">In this section, we discuss authentication via Azure AD.</span></span>

>[!NOTE]
><span data-ttu-id="9b768-162">When you create a Batch account, you can specify whether pools are to be allocated in a subscription managed by Batch, or in a user subscription.</span><span class="sxs-lookup"><span data-stu-id="9b768-162">When you create a Batch account, you can specify whether pools are to be allocated in a subscription managed by Batch, or in a user subscription.</span></span> <span data-ttu-id="9b768-163">If your account allocates pools in a user subscription, then you must use Azure AD to authenticate requests to resources in that account.</span><span class="sxs-lookup"><span data-stu-id="9b768-163">If your account allocates pools in a user subscription, then you must use Azure AD to authenticate requests to resources in that account.</span></span>
>
>

<span data-ttu-id="9b768-164">Authenticating Batch .NET applications via Azure AD is similar to authenticating Batch Management .NET applications.</span><span class="sxs-lookup"><span data-stu-id="9b768-164">Authenticating Batch .NET applications via Azure AD is similar to authenticating Batch Management .NET applications.</span></span> <span data-ttu-id="9b768-165">There are a few differences, described in this section.</span><span class="sxs-lookup"><span data-stu-id="9b768-165">There are a few differences, described in this section.</span></span>

### <a name="batch-service-endpoints"></a><span data-ttu-id="9b768-166">Batch service endpoints</span><span class="sxs-lookup"><span data-stu-id="9b768-166">Batch service endpoints</span></span>

<span data-ttu-id="9b768-167">The Batch service endpoints differ from those that you use with Batch Management .NET.</span><span class="sxs-lookup"><span data-stu-id="9b768-167">The Batch service endpoints differ from those that you use with Batch Management .NET.</span></span>

<span data-ttu-id="9b768-168">The Azure AD endpoint for the Batch service is:</span><span class="sxs-lookup"><span data-stu-id="9b768-168">The Azure AD endpoint for the Batch service is:</span></span>

`https://login.microsoftonline.com/common`

<span data-ttu-id="9b768-169">The resource endpoint for the Batch service is:</span><span class="sxs-lookup"><span data-stu-id="9b768-169">The resource endpoint for the Batch service is:</span></span>

`https://batch.core.windows.net/`

### <a name="grant-the-batch-service-api-access-to-your-application"></a><span data-ttu-id="9b768-170">Grant the Batch service API access to your application</span><span class="sxs-lookup"><span data-stu-id="9b768-170">Grant the Batch service API access to your application</span></span>

<span data-ttu-id="9b768-171">Before you can authenticate via Azure AD from your Batch application, you need to register your application with Azure AD and grant access to the Batch service API.</span><span class="sxs-lookup"><span data-stu-id="9b768-171">Before you can authenticate via Azure AD from your Batch application, you need to register your application with Azure AD and grant access to the Batch service API.</span></span> <span data-ttu-id="9b768-172">The Azure AD identifier for the Batch service API is **Microsoft Azure Batch (MicrosoftAzureBatch)**.</span><span class="sxs-lookup"><span data-stu-id="9b768-172">The Azure AD identifier for the Batch service API is **Microsoft Azure Batch (MicrosoftAzureBatch)**.</span></span>

1. <span data-ttu-id="9b768-173">To register your Batch application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span><span class="sxs-lookup"><span data-stu-id="9b768-173">To register your Batch application, follow the steps in the [Adding an Application](../active-directory/develop/active-directory-integrating-applications.md#adding-an-application) section in [Integrating applications with Azure Active Directory][aad_integrate].</span></span> <span data-ttu-id="9b768-174">For the **Redirect URI**, you can specify any valid URI.</span><span class="sxs-lookup"><span data-stu-id="9b768-174">For the **Redirect URI**, you can specify any valid URI.</span></span> <span data-ttu-id="9b768-175">It does not need to be a real endpoint.</span><span class="sxs-lookup"><span data-stu-id="9b768-175">It does not need to be a real endpoint.</span></span>

    <span data-ttu-id="9b768-176">After you've registered your application, you'll see the application ID and object ID:</span><span class="sxs-lookup"><span data-stu-id="9b768-176">After you've registered your application, you'll see the application ID and object ID:</span></span>

    ![Register your Batch application with Azure AD](https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-aad-auth/app-registration-data-plane.png)

2. <span data-ttu-id="9b768-178">Next, display the **Settings** blade.</span><span class="sxs-lookup"><span data-stu-id="9b768-178">Next, display the **Settings** blade.</span></span> <span data-ttu-id="9b768-179">In the **API Access** section, select **Required permissions**.</span><span class="sxs-lookup"><span data-stu-id="9b768-179">In the **API Access** section, select **Required permissions**.</span></span>
3. <span data-ttu-id="9b768-180">In the **Required permissions** blade, click the **Add** button.</span><span class="sxs-lookup"><span data-stu-id="9b768-180">In the **Required permissions** blade, click the **Add** button.</span></span>
4. <span data-ttu-id="9b768-181">In step 1, search for **MicrosoftAzureBatch**, select **Microsoft Azure Batch (MicrosoftAzureBatch)**, and click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="9b768-181">In step 1, search for **MicrosoftAzureBatch**, select **Microsoft Azure Batch (MicrosoftAzureBatch)**, and click the **Select** button.</span></span>
5. <span data-ttu-id="9b768-182">In step 2, select the check box next to **Access Azure Batch Service** and click the **Select** button.</span><span class="sxs-lookup"><span data-stu-id="9b768-182">In step 2, select the check box next to **Access Azure Batch Service** and click the **Select** button.</span></span>
6. <span data-ttu-id="9b768-183">Click the **Done** button.</span><span class="sxs-lookup"><span data-stu-id="9b768-183">Click the **Done** button.</span></span>

<span data-ttu-id="9b768-184">The **Required Permissions** blade now shows that your Azure AD application grants access to both the Azure AD and Azure Batch APIs.</span><span class="sxs-lookup"><span data-stu-id="9b768-184">The **Required Permissions** blade now shows that your Azure AD application grants access to both the Azure AD and Azure Batch APIs.</span></span> 

![API permissions](https://docstestmedia1.blob.core.windows.net/azure-media/articles/batch/media/batch-aad-auth/required-permissions-data-plane.png)

### <a name="authentication-for-batch-accounts-in-a-user-subscription"></a><span data-ttu-id="9b768-186">Authentication for Batch accounts in a user subscription</span><span class="sxs-lookup"><span data-stu-id="9b768-186">Authentication for Batch accounts in a user subscription</span></span>

<span data-ttu-id="9b768-187">When you create a new Batch account, you can choose the subscription in which pools are allocated.</span><span class="sxs-lookup"><span data-stu-id="9b768-187">When you create a new Batch account, you can choose the subscription in which pools are allocated.</span></span> <span data-ttu-id="9b768-188">Your choice affects how you authenticate requests made to resources in that account</span><span class="sxs-lookup"><span data-stu-id="9b768-188">Your choice affects how you authenticate requests made to resources in that account</span></span>

<span data-ttu-id="9b768-189">By default, Batch pools are allocated in a Batch service subscription.</span><span class="sxs-lookup"><span data-stu-id="9b768-189">By default, Batch pools are allocated in a Batch service subscription.</span></span> <span data-ttu-id="9b768-190">If you choose this option, you can authenticate requests to resources in that account with either Shared Key or with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b768-190">If you choose this option, you can authenticate requests to resources in that account with either Shared Key or with Azure AD.</span></span>

<span data-ttu-id="9b768-191">You can also specify that Batch pools are allocated in a specified user subscription.</span><span class="sxs-lookup"><span data-stu-id="9b768-191">You can also specify that Batch pools are allocated in a specified user subscription.</span></span> <span data-ttu-id="9b768-192">If you choose this option, you must authenticate with Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b768-192">If you choose this option, you must authenticate with Azure AD.</span></span>

### <a name="best-practices-for-using-azure-ad-with-batch"></a><span data-ttu-id="9b768-193">Best practices for using Azure AD with Batch</span><span class="sxs-lookup"><span data-stu-id="9b768-193">Best practices for using Azure AD with Batch</span></span>

<span data-ttu-id="9b768-194">An Azure AD authentication token expires after one hour.</span><span class="sxs-lookup"><span data-stu-id="9b768-194">An Azure AD authentication token expires after one hour.</span></span> <span data-ttu-id="9b768-195">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request to ensure you always have a valid token.</span><span class="sxs-lookup"><span data-stu-id="9b768-195">When using a long-lived **BatchClient** object, we recommend that you retrieve a token from ADAL on every request to ensure you always have a valid token.</span></span> 

<span data-ttu-id="9b768-196">To achieve this in .NET, write a method that retrieves the token from Azure AD and pass that method to a **BatchTokenCredentials** object as a delegate.</span><span class="sxs-lookup"><span data-stu-id="9b768-196">To achieve this in .NET, write a method that retrieves the token from Azure AD and pass that method to a **BatchTokenCredentials** object as a delegate.</span></span> <span data-ttu-id="9b768-197">The delegate method is called on every request to the Batch service to ensure that a valid token is provided.</span><span class="sxs-lookup"><span data-stu-id="9b768-197">The delegate method is called on every request to the Batch service to ensure that a valid token is provided.</span></span> <span data-ttu-id="9b768-198">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span><span class="sxs-lookup"><span data-stu-id="9b768-198">By default ADAL caches tokens, so a new token is retrieved from Azure AD only when necessary.</span></span> <span data-ttu-id="9b768-199">For an example, see [Code example: Using Azure AD with Batch .NET](#code-example-using-azure-ad-with-batch-net) in the next section.</span><span class="sxs-lookup"><span data-stu-id="9b768-199">For an example, see [Code example: Using Azure AD with Batch .NET](#code-example-using-azure-ad-with-batch-net) in the next section.</span></span> <span data-ttu-id="9b768-200">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span><span class="sxs-lookup"><span data-stu-id="9b768-200">For more information about tokens in Azure AD, see [Authentication Scenarios for Azure AD][aad_auth_scenarios].</span></span>

### <a name="code-example-using-azure-ad-with-batch-net"></a><span data-ttu-id="9b768-201">Code example: Using Azure AD with Batch .NET</span><span class="sxs-lookup"><span data-stu-id="9b768-201">Code example: Using Azure AD with Batch .NET</span></span>

<span data-ttu-id="9b768-202">To write Batch .NET code that authenticates with Azure AD, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span><span class="sxs-lookup"><span data-stu-id="9b768-202">To write Batch .NET code that authenticates with Azure AD, reference the [Azure Batch .NET](https://www.nuget.org/packages/Azure.Batch/) package and the [ADAL](https://www.nuget.org/packages/Microsoft.IdentityModel.Clients.ActiveDirectory/) package.</span></span>

<span data-ttu-id="9b768-203">Include the following `using` statements in your code:</span><span class="sxs-lookup"><span data-stu-id="9b768-203">Include the following `using` statements in your code:</span></span>

```csharp
using Microsoft.Azure.Batch;
using Microsoft.Azure.Batch.Auth;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

<span data-ttu-id="9b768-204">Reference the Azure AD common endpoint and the Azure AD endpoint for the Batch service in your code:</span><span class="sxs-lookup"><span data-stu-id="9b768-204">Reference the Azure AD common endpoint and the Azure AD endpoint for the Batch service in your code:</span></span>  

```csharp
private const string AuthorityUri = "https://login.microsoftonline.com/common";
private const string BatchResourceUri = "https://batch.core.windows.net/";
```

<span data-ttu-id="9b768-205">Reference your Batch account endpoint:</span><span class="sxs-lookup"><span data-stu-id="9b768-205">Reference your Batch account endpoint:</span></span>

```csharp
private const string BatchAccountEndpoint = "https://myaccount.westcentralus.batch.azure.com";
```

<span data-ttu-id="9b768-206">Specify the application ID (client ID) for your application.</span><span class="sxs-lookup"><span data-stu-id="9b768-206">Specify the application ID (client ID) for your application.</span></span> <span data-ttu-id="9b768-207">The application ID is available from your app registration in the Azure portal; see the section titled [Grant the Batch service API access to your application](#grant-the-batch-service-api-access-to-your-application) to retrieve it.</span><span class="sxs-lookup"><span data-stu-id="9b768-207">The application ID is available from your app registration in the Azure portal; see the section titled [Grant the Batch service API access to your application](#grant-the-batch-service-api-access-to-your-application) to retrieve it.</span></span> 

```csharp
private const string ClientId = "<application-id>";
```

<span data-ttu-id="9b768-208">Also specify a redirect URI, which can be any valid URI.</span><span class="sxs-lookup"><span data-stu-id="9b768-208">Also specify a redirect URI, which can be any valid URI.</span></span>

```csharp
private const string RedirectUri = "http://mybatchdatasample";
```

<span data-ttu-id="9b768-209">Write a callback method to acquire the authentication token from Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9b768-209">Write a callback method to acquire the authentication token from Azure AD.</span></span> <span data-ttu-id="9b768-210">The **AcquireTokenAsync** method prompts the user for their credentials and uses those credentials to acquire a new token.</span><span class="sxs-lookup"><span data-stu-id="9b768-210">The **AcquireTokenAsync** method prompts the user for their credentials and uses those credentials to acquire a new token.</span></span>

```csharp
public static async Task<string> GetAuthenticationTokenAsync()
{
    var authContext = new AuthenticationContext(AuthorityUri);

    // Acquire the authentication token from Azure AD.
    var authResult = await authContext.AcquireTokenAsync(BatchResourceUri, 
                                                        ClientId, 
                                                        new Uri(RedirectUri), 
                                                        new PlatformParameters(PromptBehavior.Auto));

    return authResult.AccessToken;
}
```

<span data-ttu-id="9b768-211">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span><span class="sxs-lookup"><span data-stu-id="9b768-211">Construct a **BatchTokenCredentials** object that takes the delegate as a parameter.</span></span> <span data-ttu-id="9b768-212">Use those credentials to open a **BatchClient** object.</span><span class="sxs-lookup"><span data-stu-id="9b768-212">Use those credentials to open a **BatchClient** object.</span></span> <span data-ttu-id="9b768-213">You can then use that **BatchClient** object for subsequent operations against the Batch service.</span><span class="sxs-lookup"><span data-stu-id="9b768-213">You can then use that **BatchClient** object for subsequent operations against the Batch service.</span></span>

```csharp
public static async Task PerformBatchOperations()
{
    Func<Task<string>> tokenProvider = () => GetAuthenticationTokenAsync();

    using (var client = await BatchClient.OpenAsync(new BatchTokenCredentials(BatchAccountEndpoint, tokenProvider)))
    {
        await client.JobOperations.ListJobs().ToListAsync();
    }
}
```

<span data-ttu-id="9b768-214">The **GetAuthenticationTokenAsync** callback method shown above uses Azure AD for integrated authentication of a user who is interacting with the application.</span><span class="sxs-lookup"><span data-stu-id="9b768-214">The **GetAuthenticationTokenAsync** callback method shown above uses Azure AD for integrated authentication of a user who is interacting with the application.</span></span> <span data-ttu-id="9b768-215">The call to the **AcquireTokenAsync** method prompts the user for their credentials, and the application proceeds once the user provides them.</span><span class="sxs-lookup"><span data-stu-id="9b768-215">The call to the **AcquireTokenAsync** method prompts the user for their credentials, and the application proceeds once the user provides them.</span></span> <span data-ttu-id="9b768-216">You can also use Azure AD to authenticate an unattended application by using an Azure AD service principal.</span><span class="sxs-lookup"><span data-stu-id="9b768-216">You can also use Azure AD to authenticate an unattended application by using an Azure AD service principal.</span></span> <span data-ttu-id="9b768-217">For more information, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md) and [Use portal to create Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9b768-217">For more information, see [Application and service principal objects in Azure Active Directory](../active-directory/develop/active-directory-application-objects.md) and [Use portal to create Active Directory application and service principal that can access resources](../resource-group-create-service-principal-portal.md).</span></span>  
 

## <a name="next-steps"></a><span data-ttu-id="9b768-218">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b768-218">Next steps</span></span>

<span data-ttu-id="9b768-219">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="9b768-219">For more information on running the [AccountManagement sample application][acct_mgmt_sample], see [Manage Batch accounts and quotas with the Batch Management client library for .NET](batch-management-dotnet.md).</span></span>

<span data-ttu-id="9b768-220">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span><span class="sxs-lookup"><span data-stu-id="9b768-220">To learn more about Azure AD, see the [Azure Active Directory Documentation](https://docs.microsoft.com/azure/active-directory/).</span></span> <span data-ttu-id="9b768-221">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span><span class="sxs-lookup"><span data-stu-id="9b768-221">In-depth examples showing how to use ADAL are available in the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=active-directory) library.</span></span>


[aad_about]: ../active-directory/active-directory-whatis.md "What is Azure Active Directory?"
[aad_adal]: ../active-directory/active-directory-authentication-libraries.md
[aad_auth_scenarios]: ../active-directory/active-directory-authentication-scenarios.md "Authentication Scenarios for Azure AD"
[aad_integrate]: ../active-directory/active-directory-integrating-applications.md "Integrating Applications with Azure Active Directory"
[acct_mgmt_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/AccountManagement
[azure_portal]: http://portal.azure.com
[resman_overview]: ../azure-resource-manager/resource-group-overview.md






