---
title: 'End-user authentication: Data Lake Store with Azure Active Directory | Microsoft Docs'
description: Learn how to achieve end-user authentication with Data Lake Store using Azure Active Directory
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: 7280cd971e9857c494dfd1cb77d528e4737ed9d2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44775196"
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="0bd4d-103">End-user authentication with Data Lake Store using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0bd4d-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md)
> * [Service-to-service authentication](data-lake-store-service-to-service-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="0bd4d-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="0bd4d-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must decide how to authenticate your application with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="0bd4d-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must decide how to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="0bd4d-108">The two main options available are:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-108">The two main options available are:</span></span>

* <span data-ttu-id="0bd4d-109">End-user authentication (this article)</span><span class="sxs-lookup"><span data-stu-id="0bd4d-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="0bd4d-110">Service-to-service authentication (pick this option from the drop-down above)</span><span class="sxs-lookup"><span data-stu-id="0bd4d-110">Service-to-service authentication (pick this option from the drop-down above)</span></span>

<span data-ttu-id="0bd4d-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="0bd4d-112">This article talks about how to create an **Azure AD native application for end-user authentication**.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-112">This article talks about how to create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="0bd4d-113">For instructions on Azure AD application configuration for service-to-service authentication, see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="0bd4d-113">For instructions on Azure AD application configuration for service-to-service authentication, see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0bd4d-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0bd4d-114">Prerequisites</span></span>
* <span data-ttu-id="0bd4d-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-115">An Azure subscription.</span></span> <span data-ttu-id="0bd4d-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0bd4d-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="0bd4d-117">Your subscription ID.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-117">Your subscription ID.</span></span> <span data-ttu-id="0bd4d-118">You can retrieve it from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-118">You can retrieve it from the Azure portal.</span></span> <span data-ttu-id="0bd4d-119">For example, it is available from the Data Lake Store account blade.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-119">For example, it is available from the Data Lake Store account blade.</span></span>
  
    ![Get subscription ID](./media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="0bd4d-121">Your Azure AD domain name.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-121">Your Azure AD domain name.</span></span> <span data-ttu-id="0bd4d-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure portal.</span></span> <span data-ttu-id="0bd4d-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span></span> 
  
    ![Get AAD domain](./media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

* <span data-ttu-id="0bd4d-125">Your Azure tenant ID.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-125">Your Azure tenant ID.</span></span> <span data-ttu-id="0bd4d-126">For instructions on how to retrieve the tenant ID, see [Get the tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="0bd4d-126">For instructions on how to retrieve the tenant ID, see [Get the tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>

## <a name="end-user-authentication"></a><span data-ttu-id="0bd4d-127">End-user authentication</span><span class="sxs-lookup"><span data-stu-id="0bd4d-127">End-user authentication</span></span>
<span data-ttu-id="0bd4d-128">This authentication mechanism is the recommended approach if you want an end user to log in to your application via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-128">This authentication mechanism is the recommended approach if you want an end user to log in to your application via Azure AD.</span></span> <span data-ttu-id="0bd4d-129">Your application is then able to access Azure resources with the same level of access as the end user that logged in.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-129">Your application is then able to access Azure resources with the same level of access as the end user that logged in.</span></span> <span data-ttu-id="0bd4d-130">Your end user needs to provide their credentials periodically in order for your application to maintain access.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-130">Your end user needs to provide their credentials periodically in order for your application to maintain access.</span></span>

<span data-ttu-id="0bd4d-131">The result of having the end-user login is that your application is given an access token and a refresh token.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-131">The result of having the end-user login is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="0bd4d-132">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-132">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="0bd4d-133">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-133">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default.</span></span> <span data-ttu-id="0bd4d-134">You can use two different approaches for end-user login.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-134">You can use two different approaches for end-user login.</span></span>

### <a name="using-the-oauth-20-pop-up"></a><span data-ttu-id="0bd4d-135">Using the OAuth 2.0 pop-up</span><span class="sxs-lookup"><span data-stu-id="0bd4d-135">Using the OAuth 2.0 pop-up</span></span>
<span data-ttu-id="0bd4d-136">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end user can enter their credentials.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-136">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end user can enter their credentials.</span></span> <span data-ttu-id="0bd4d-137">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if necessary.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-137">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if necessary.</span></span> 

> [!NOTE]
> This method is not yet supported in the Azure AD Authentication Library (ADAL) for Python or Java.
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="0bd4d-139">Directly passing in user credentials</span><span class="sxs-lookup"><span data-stu-id="0bd4d-139">Directly passing in user credentials</span></span>
<span data-ttu-id="0bd4d-140">Your application can directly provide user credentials to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-140">Your application can directly provide user credentials to Azure AD.</span></span> <span data-ttu-id="0bd4d-141">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including the accounts ending in @outlook.com or @live.com.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-141">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including the accounts ending in @outlook.com or @live.com.</span></span> <span data-ttu-id="0bd4d-142">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span><span class="sxs-lookup"><span data-stu-id="0bd4d-142">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-for-this-approach"></a><span data-ttu-id="0bd4d-143">What do I need for this approach?</span><span class="sxs-lookup"><span data-stu-id="0bd4d-143">What do I need for this approach?</span></span>
* <span data-ttu-id="0bd4d-144">Azure AD domain name.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-144">Azure AD domain name.</span></span> <span data-ttu-id="0bd4d-145">This requirement is already listed in the prerequisite of this article.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-145">This requirement is already listed in the prerequisite of this article.</span></span>
* <span data-ttu-id="0bd4d-146">Azure AD tenant ID.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-146">Azure AD tenant ID.</span></span> <span data-ttu-id="0bd4d-147">This requirement is already listed in the prerequisite of this article.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-147">This requirement is already listed in the prerequisite of this article.</span></span>
* <span data-ttu-id="0bd4d-148">Azure AD **native application**</span><span class="sxs-lookup"><span data-stu-id="0bd4d-148">Azure AD **native application**</span></span>
* <span data-ttu-id="0bd4d-149">Application ID for the Azure AD native application</span><span class="sxs-lookup"><span data-stu-id="0bd4d-149">Application ID for the Azure AD native application</span></span>
* <span data-ttu-id="0bd4d-150">Redirect URI for the Azure AD native application</span><span class="sxs-lookup"><span data-stu-id="0bd4d-150">Redirect URI for the Azure AD native application</span></span>
* <span data-ttu-id="0bd4d-151">Set delegated permissions</span><span class="sxs-lookup"><span data-stu-id="0bd4d-151">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-native-application"></a><span data-ttu-id="0bd4d-152">Step 1: Create an Active Directory native application</span><span class="sxs-lookup"><span data-stu-id="0bd4d-152">Step 1: Create an Active Directory native application</span></span>

<span data-ttu-id="0bd4d-153">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-153">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="0bd4d-154">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0bd4d-154">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="0bd4d-155">While following the instructions in the link, make sure you select **Native** for application type, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="0bd4d-155">While following the instructions in the link, make sure you select **Native** for application type, as shown in the following screenshot:</span></span>

<span data-ttu-id="0bd4d-156">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span><span class="sxs-lookup"><span data-stu-id="0bd4d-156">![Create web app](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-application-id-and-redirect-uri"></a><span data-ttu-id="0bd4d-157">Step 2: Get application ID and redirect URI</span><span class="sxs-lookup"><span data-stu-id="0bd4d-157">Step 2: Get application ID and redirect URI</span></span>

<span data-ttu-id="0bd4d-158">See [Get the application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the application ID.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-158">See [Get the application ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the application ID.</span></span>

<span data-ttu-id="0bd4d-159">To retrieve the redirect URI, do the following steps.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-159">To retrieve the redirect URI, do the following steps.</span></span>

1. <span data-ttu-id="0bd4d-160">From the Azure portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you created.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-160">From the Azure portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you created.</span></span>

2. <span data-ttu-id="0bd4d-161">From the **Settings** blade for the application, click **Redirect URIs**.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-161">From the **Settings** blade for the application, click **Redirect URIs**.</span></span>

    ![Get Redirect URI](./media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="0bd4d-163">Copy the value displayed.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-163">Copy the value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="0bd4d-164">Step 3: Set permissions</span><span class="sxs-lookup"><span data-stu-id="0bd4d-164">Step 3: Set permissions</span></span>

1. <span data-ttu-id="0bd4d-165">From the Azure portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you created.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-165">From the Azure portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you created.</span></span>

2. <span data-ttu-id="0bd4d-166">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-166">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span></span>

    ![client ID](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="0bd4d-168">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-168">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![client ID](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="0bd4d-170">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-170">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span></span>

    ![client ID](./media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="0bd4d-172">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-172">Click **Done**.</span></span>

5. <span data-ttu-id="0bd4d-173">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-173">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="0bd4d-174">Next steps</span><span class="sxs-lookup"><span data-stu-id="0bd4d-174">Next steps</span></span>
<span data-ttu-id="0bd4d-175">In this article, you created an Azure AD native application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span><span class="sxs-lookup"><span data-stu-id="0bd4d-175">In this article, you created an Azure AD native application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="0bd4d-176">End-user-authentication with Data Lake Store using Java SDK</span><span class="sxs-lookup"><span data-stu-id="0bd4d-176">End-user-authentication with Data Lake Store using Java SDK</span></span>](data-lake-store-end-user-authenticate-java-sdk.md)
* [<span data-ttu-id="0bd4d-177">End-user authentication with Data Lake Store using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="0bd4d-177">End-user authentication with Data Lake Store using .NET SDK</span></span>](data-lake-store-end-user-authenticate-net-sdk.md)
* [<span data-ttu-id="0bd4d-178">End-user authentication with Data Lake Store using Python</span><span class="sxs-lookup"><span data-stu-id="0bd4d-178">End-user authentication with Data Lake Store using Python</span></span>](data-lake-store-end-user-authenticate-python.md)
* [<span data-ttu-id="0bd4d-179">End-user authentication with Data Lake Store using REST API</span><span class="sxs-lookup"><span data-stu-id="0bd4d-179">End-user authentication with Data Lake Store using REST API</span></span>](data-lake-store-end-user-authenticate-rest-api.md)

