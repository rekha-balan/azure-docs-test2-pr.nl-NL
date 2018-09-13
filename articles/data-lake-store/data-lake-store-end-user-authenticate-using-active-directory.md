---
title: 'End-user authentication: Data Lake Store with Azure Active Directory | Microsoft Docs'
description: Learn how to achieve end-user authentication with Data Lake Store using Azure Active Directory
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: ec586ecd-1b42-459e-b600-fadbb7b80a9b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/02/2017
ms.author: nitinme
ms.openlocfilehash: ba52550e580d294940177c350b5e50cd1199700a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553175"
---
# <a name="end-user-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="8c297-103">End-user authentication with Data Lake Store using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c297-103">End-user authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md)
> * [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="8c297-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span><span class="sxs-lookup"><span data-stu-id="8c297-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="8c297-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c297-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="8c297-108">The two main options available are:</span><span class="sxs-lookup"><span data-stu-id="8c297-108">The two main options available are:</span></span>

* <span data-ttu-id="8c297-109">End-user authentication (this article)</span><span class="sxs-lookup"><span data-stu-id="8c297-109">End-user authentication (this article)</span></span>
* <span data-ttu-id="8c297-110">Service-to-service authentication</span><span class="sxs-lookup"><span data-stu-id="8c297-110">Service-to-service authentication</span></span>

<span data-ttu-id="8c297-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="8c297-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="8c297-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span><span class="sxs-lookup"><span data-stu-id="8c297-112">This article talks about how create an **Azure AD native application for end-user authentication**.</span></span> <span data-ttu-id="8c297-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="8c297-113">For instructions on Azure AD application configuration for service-to-service authentication see [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c297-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8c297-114">Prerequisites</span></span>
* <span data-ttu-id="8c297-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8c297-115">An Azure subscription.</span></span> <span data-ttu-id="8c297-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8c297-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="8c297-117">Your subscription ID.</span><span class="sxs-lookup"><span data-stu-id="8c297-117">Your subscription ID.</span></span> <span data-ttu-id="8c297-118">You can retrieve it from the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8c297-118">You can retrieve it from the Azure Portal.</span></span> <span data-ttu-id="8c297-119">For example, it is available from the Data Lake Store account blade.</span><span class="sxs-lookup"><span data-stu-id="8c297-119">For example, it is available from the Data Lake Store account blade.</span></span>
  
    ![Get subscription ID](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-end-user-authenticate-using-active-directory/get-subscription-id.png)

* <span data-ttu-id="8c297-121">Your Azure AD domain name.</span><span class="sxs-lookup"><span data-stu-id="8c297-121">Your Azure AD domain name.</span></span> <span data-ttu-id="8c297-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="8c297-122">You can retrieve it by hovering the mouse in the top-right corner of the Azure Portal.</span></span> <span data-ttu-id="8c297-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span><span class="sxs-lookup"><span data-stu-id="8c297-123">From the screenshot below, the domain name is **contoso.onmicrosoft.com**, and the GUID within brackets is the tenant ID.</span></span> 
  
    ![Get AAD domain](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-end-user-authenticate-using-active-directory/get-aad-domain.png)

## <a name="end-user-authentication"></a><span data-ttu-id="8c297-125">End-user authentication</span><span class="sxs-lookup"><span data-stu-id="8c297-125">End-user authentication</span></span>
<span data-ttu-id="8c297-126">This is the recommended approach if you want an end-user to log in to your application via Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c297-126">This is the recommended approach if you want an end-user to log in to your application via Azure AD.</span></span> <span data-ttu-id="8c297-127">Your application will be able to access Azure resources with the same level of access as the end-user that logged in.</span><span class="sxs-lookup"><span data-stu-id="8c297-127">Your application will be able to access Azure resources with the same level of access as the end-user that logged in.</span></span> <span data-ttu-id="8c297-128">Your end-user will need to provide their credentials periodically in order for your application to maintain access.</span><span class="sxs-lookup"><span data-stu-id="8c297-128">Your end-user will need to provide their credentials periodically in order for your application to maintain access.</span></span>

<span data-ttu-id="8c297-129">The result of having the end-user log in is that your application is given an access token and a refresh token.</span><span class="sxs-lookup"><span data-stu-id="8c297-129">The result of having the end-user log in is that your application is given an access token and a refresh token.</span></span> <span data-ttu-id="8c297-130">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span><span class="sxs-lookup"><span data-stu-id="8c297-130">The access token gets attached to each request made to Data Lake Store or Data Lake Analytics, and it is valid for one hour by default.</span></span> <span data-ttu-id="8c297-131">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span><span class="sxs-lookup"><span data-stu-id="8c297-131">The refresh token can be used to obtain a new access token, and it is valid for up to two weeks by default, if used regularly.</span></span> <span data-ttu-id="8c297-132">You can use two different approaches for end-user log in.</span><span class="sxs-lookup"><span data-stu-id="8c297-132">You can use two different approaches for end-user log in.</span></span>

### <a name="using-the-oauth-20-pop-up"></a><span data-ttu-id="8c297-133">Using the OAuth 2.0 pop-up</span><span class="sxs-lookup"><span data-stu-id="8c297-133">Using the OAuth 2.0 pop-up</span></span>
<span data-ttu-id="8c297-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end-user can enter their credentials.</span><span class="sxs-lookup"><span data-stu-id="8c297-134">Your application can trigger an OAuth 2.0 authorization pop-up, in which the end-user can enter their credentials.</span></span> <span data-ttu-id="8c297-135">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if required.</span><span class="sxs-lookup"><span data-stu-id="8c297-135">This pop-up also works with the Azure AD Two-factor Authentication (2FA) process, if required.</span></span> 

> [!NOTE]
> This method is not yet supported in the Azure AD Authentication Library (ADAL) for Python or Java.
> 
> 

### <a name="directly-passing-in-user-credentials"></a><span data-ttu-id="8c297-137">Directly passing in user credentials</span><span class="sxs-lookup"><span data-stu-id="8c297-137">Directly passing in user credentials</span></span>
<span data-ttu-id="8c297-138">Your application can directly provide user credentials to Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c297-138">Your application can directly provide user credentials to Azure AD.</span></span> <span data-ttu-id="8c297-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com.</span><span class="sxs-lookup"><span data-stu-id="8c297-139">This method only works with organizational ID user accounts; it is not compatible with personal / “live ID” user accounts, including those ending in @outlook.com or @live.com.</span></span> <span data-ttu-id="8c297-140">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span><span class="sxs-lookup"><span data-stu-id="8c297-140">Furthermore, this method is not compatible with user accounts that require Azure AD Two-factor Authentication (2FA).</span></span>

### <a name="what-do-i-need-to-use-this-approach"></a><span data-ttu-id="8c297-141">What do I need to use this approach?</span><span class="sxs-lookup"><span data-stu-id="8c297-141">What do I need to use this approach?</span></span>
* <span data-ttu-id="8c297-142">Azure AD domain name.</span><span class="sxs-lookup"><span data-stu-id="8c297-142">Azure AD domain name.</span></span> <span data-ttu-id="8c297-143">This is already listed in the prerequisite of this article.</span><span class="sxs-lookup"><span data-stu-id="8c297-143">This is already listed in the prerequisite of this article.</span></span>
* <span data-ttu-id="8c297-144">Azure AD **native application**</span><span class="sxs-lookup"><span data-stu-id="8c297-144">Azure AD **native application**</span></span>
* <span data-ttu-id="8c297-145">Client ID for the Azure AD native application</span><span class="sxs-lookup"><span data-stu-id="8c297-145">Client ID for the Azure AD native application</span></span>
* <span data-ttu-id="8c297-146">Reply URI for the Azure AD native application</span><span class="sxs-lookup"><span data-stu-id="8c297-146">Reply URI for the Azure AD native application</span></span>
* <span data-ttu-id="8c297-147">Set delegated permissions</span><span class="sxs-lookup"><span data-stu-id="8c297-147">Set delegated permissions</span></span>


## <a name="step-1-create-an-active-directory-web-application"></a><span data-ttu-id="8c297-148">Step 1: Create an Active Directory web application</span><span class="sxs-lookup"><span data-stu-id="8c297-148">Step 1: Create an Active Directory web application</span></span>

<span data-ttu-id="8c297-149">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c297-149">Create and configure an Azure AD native application for end-user authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="8c297-150">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="8c297-150">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="8c297-151">While following the instructions at the above link, make sure you select **Native** for application type, as shown in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="8c297-151">While following the instructions at the above link, make sure you select **Native** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="8c297-152">![Create web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span><span class="sxs-lookup"><span data-stu-id="8c297-152">![Create web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-create-native-app.png "Create native app")</span></span>

## <a name="step-2-get-client-id-reply-uri-and-set-delegated-permissions"></a><span data-ttu-id="8c297-153">Step 2: Get client id, reply URI, and set delegated permissions</span><span class="sxs-lookup"><span data-stu-id="8c297-153">Step 2: Get client id, reply URI, and set delegated permissions</span></span>

<span data-ttu-id="8c297-154">See [Get the client add](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the client id (also called the application id) of the Azure AD native application.</span><span class="sxs-lookup"><span data-stu-id="8c297-154">See [Get the client add](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key) to retrieve the client id (also called the application id) of the Azure AD native application.</span></span>

<span data-ttu-id="8c297-155">To retrieve the redirect URI, follow the steps below.</span><span class="sxs-lookup"><span data-stu-id="8c297-155">To retrieve the redirect URI, follow the steps below.</span></span>

1. <span data-ttu-id="8c297-156">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span><span class="sxs-lookup"><span data-stu-id="8c297-156">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="8c297-157">From the **Settings** blade for the application, click **Redirect URIs**.</span><span class="sxs-lookup"><span data-stu-id="8c297-157">From the **Settings** blade for the application, click **Redirect URIs**.</span></span>

    ![Get Redirect URI](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-end-user-authenticate-using-active-directory/azure-active-directory-redirect-uri.png)

3. <span data-ttu-id="8c297-159">Copy the value displayed.</span><span class="sxs-lookup"><span data-stu-id="8c297-159">Copy the value displayed.</span></span>


## <a name="step-3-set-permissions"></a><span data-ttu-id="8c297-160">Step 3: Set permissions</span><span class="sxs-lookup"><span data-stu-id="8c297-160">Step 3: Set permissions</span></span>

1. <span data-ttu-id="8c297-161">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span><span class="sxs-lookup"><span data-stu-id="8c297-161">From the Azure Portal, select **Azure Active Directory**, click **App registrations**, and then find and click the Azure AD native application that you just created.</span></span>

2. <span data-ttu-id="8c297-162">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="8c297-162">From the **Settings** blade for the application, click **Required permissions**, and then click **Add**.</span></span>

    ![client id](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-1.png)

3. <span data-ttu-id="8c297-164">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="8c297-164">In the **Add API Access** blade, click **Select an API**, click **Azure Data Lake**, and then click **Select**.</span></span>

    ![client id](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-2.png)
 
4.  <span data-ttu-id="8c297-166">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="8c297-166">In the **Add API Access** blade, click **Select permissions**, select the check box to give **Full access to Data Lake Store**, and then click **Select**.</span></span>

    ![client id](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-end-user-authenticate-using-active-directory/aad-end-user-auth-set-permission-3.png)

    <span data-ttu-id="8c297-168">Click **Done**.</span><span class="sxs-lookup"><span data-stu-id="8c297-168">Click **Done**.</span></span>

5. <span data-ttu-id="8c297-169">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span><span class="sxs-lookup"><span data-stu-id="8c297-169">Repeat the last two steps to grant permissions for **Windows Azure Service Management API** as well.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="8c297-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="8c297-170">Next steps</span></span>
<span data-ttu-id="8c297-171">In this article you created an Azure AD web application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span><span class="sxs-lookup"><span data-stu-id="8c297-171">In this article you created an Azure AD web application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="8c297-172">Get started with Azure Data Lake Store using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8c297-172">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="8c297-173">Get started with Azure Data Lake Store using Java SDK</span><span class="sxs-lookup"><span data-stu-id="8c297-173">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)








