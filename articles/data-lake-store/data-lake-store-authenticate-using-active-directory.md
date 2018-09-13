---
title: 'Service-to-service authentication: Data Lake Store with Azure Active Directory | Microsoft Docs'
description: Learn how to achieve service-to-service authentication with Data Lake Store using Azure Active Directory
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 820b7c5d-4863-4225-9bd1-df4d8f515537
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/30/2017
ms.author: nitinme
ms.openlocfilehash: 89b862e1fe5729e7d327db6fa3ad45437d023b14
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556773"
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="83f93-103">Service-to-service authentication with Data Lake Store using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="83f93-103">Service-to-service authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md)
> * [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md)
> 
> 

<span data-ttu-id="83f93-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span><span class="sxs-lookup"><span data-stu-id="83f93-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="83f93-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="83f93-107">Before authoring an application that works with Azure Data Lake Store or Azure Data Lake Analytics, you must first decide how you would like to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="83f93-108">The two main options available are:</span><span class="sxs-lookup"><span data-stu-id="83f93-108">The two main options available are:</span></span>

* <span data-ttu-id="83f93-109">End-user authentication</span><span class="sxs-lookup"><span data-stu-id="83f93-109">End-user authentication</span></span> 
* <span data-ttu-id="83f93-110">Service-to-service authentication (this article)</span><span class="sxs-lookup"><span data-stu-id="83f93-110">Service-to-service authentication (this article)</span></span> 

<span data-ttu-id="83f93-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="83f93-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store or Azure Data Lake Analytics.</span></span>

<span data-ttu-id="83f93-112">This article talks about how create an **Azure AD web application for service-to-service authentication**.</span><span class="sxs-lookup"><span data-stu-id="83f93-112">This article talks about how create an **Azure AD web application for service-to-service authentication**.</span></span> <span data-ttu-id="83f93-113">For instructions on Azure AD application configuration for end-user authentication see [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="83f93-113">For instructions on Azure AD application configuration for end-user authentication see [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83f93-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="83f93-114">Prerequisites</span></span>
* <span data-ttu-id="83f93-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="83f93-115">An Azure subscription.</span></span> <span data-ttu-id="83f93-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="83f93-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="step-1-create-an-active-directory-web-application"></a><span data-ttu-id="83f93-117">Step 1: Create an Active Directory web application</span><span class="sxs-lookup"><span data-stu-id="83f93-117">Step 1: Create an Active Directory web application</span></span>

<span data-ttu-id="83f93-118">Create and configure an Azure AD web application for service-to-service authentication with Azure Data Lake Store using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="83f93-118">Create and configure an Azure AD web application for service-to-service authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="83f93-119">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="83f93-119">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="83f93-120">While following the instructions at the above link, make sure you select **Web App / API** for application type, as shown in the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="83f93-120">While following the instructions at the above link, make sure you select **Web App / API** for application type, as shown in the screenshot below.</span></span>

<span data-ttu-id="83f93-121">![Create web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Create web app")</span><span class="sxs-lookup"><span data-stu-id="83f93-121">![Create web app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Create web app")</span></span>

## <a name="step-2-get-client-id-client-secret-and-tenant-id"></a><span data-ttu-id="83f93-122">Step 2: Get client id, client secret, and tenant id</span><span class="sxs-lookup"><span data-stu-id="83f93-122">Step 2: Get client id, client secret, and tenant id</span></span>
<span data-ttu-id="83f93-123">When programmatically logging in, you need the id for your application.</span><span class="sxs-lookup"><span data-stu-id="83f93-123">When programmatically logging in, you need the id for your application.</span></span> <span data-ttu-id="83f93-124">If the application runs under its own credentials, you will also need an authentication key.</span><span class="sxs-lookup"><span data-stu-id="83f93-124">If the application runs under its own credentials, you will also need an authentication key.</span></span>

* <span data-ttu-id="83f93-125">For instructions on how to retrieve the client ID and client secret for your application, see [Get application ID and authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span><span class="sxs-lookup"><span data-stu-id="83f93-125">For instructions on how to retrieve the client ID and client secret for your application, see [Get application ID and authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span></span>

* <span data-ttu-id="83f93-126">For instructions on how to retrieve the tenant ID, see [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="83f93-126">For instructions on how to retrieve the tenant ID, see [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>

## <a name="step-3-assign-the-azure-ad-application-to-the-azure-data-lake-store-account-file-or-folder-only-for-service-to-service-authentication"></a><span data-ttu-id="83f93-127">Step 3: Assign the Azure AD application to the Azure Data Lake Store account file or folder (only for service-to-service authentication)</span><span class="sxs-lookup"><span data-stu-id="83f93-127">Step 3: Assign the Azure AD application to the Azure Data Lake Store account file or folder (only for service-to-service authentication)</span></span>
1. <span data-ttu-id="83f93-128">Sign on to the new [Azure portal](https://portal.azure.com) and open the Azure Data Lake Store account that you want to associate with the Azure Active Directory application you created earlier.</span><span class="sxs-lookup"><span data-stu-id="83f93-128">Sign on to the new [Azure portal](https://portal.azure.com) and open the Azure Data Lake Store account that you want to associate with the Azure Active Directory application you created earlier.</span></span>
2. <span data-ttu-id="83f93-129">In your Data Lake Store account blade, click **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="83f93-129">In your Data Lake Store account blade, click **Data Explorer**.</span></span>
   
    <span data-ttu-id="83f93-130">![Create directories in Data Lake Store account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Create directories in Data Lake account")</span><span class="sxs-lookup"><span data-stu-id="83f93-130">![Create directories in Data Lake Store account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Create directories in Data Lake account")</span></span>
3. <span data-ttu-id="83f93-131">In the **Data Explorer** blade, click the file or folder for which you want to provide access to the Azure AD application, and then click **Access**.</span><span class="sxs-lookup"><span data-stu-id="83f93-131">In the **Data Explorer** blade, click the file or folder for which you want to provide access to the Azure AD application, and then click **Access**.</span></span> <span data-ttu-id="83f93-132">To configure access to a file, you must click **Access** from the **File Preview** blade.</span><span class="sxs-lookup"><span data-stu-id="83f93-132">To configure access to a file, you must click **Access** from the **File Preview** blade.</span></span>
   
    <span data-ttu-id="83f93-133">![Set ACLs on Data Lake file system](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Set ACLs on Data Lake file system")</span><span class="sxs-lookup"><span data-stu-id="83f93-133">![Set ACLs on Data Lake file system](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Set ACLs on Data Lake file system")</span></span>
4. <span data-ttu-id="83f93-134">The **Access** blade lists the standard access and custom access already assigned to the root.</span><span class="sxs-lookup"><span data-stu-id="83f93-134">The **Access** blade lists the standard access and custom access already assigned to the root.</span></span> <span data-ttu-id="83f93-135">Click the **Add** icon to add custom-level ACLs.</span><span class="sxs-lookup"><span data-stu-id="83f93-135">Click the **Add** icon to add custom-level ACLs.</span></span>
   
    <span data-ttu-id="83f93-136">![List standard and custom access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "List standard and custom access")</span><span class="sxs-lookup"><span data-stu-id="83f93-136">![List standard and custom access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "List standard and custom access")</span></span>
5. <span data-ttu-id="83f93-137">Click the **Add** icon to open the **Add Custom Access** blade.</span><span class="sxs-lookup"><span data-stu-id="83f93-137">Click the **Add** icon to open the **Add Custom Access** blade.</span></span> <span data-ttu-id="83f93-138">In this blade, click **Select User or Group**, and then in **Select User or Group** blade, look for the Azure Active Directory application you created earlier.</span><span class="sxs-lookup"><span data-stu-id="83f93-138">In this blade, click **Select User or Group**, and then in **Select User or Group** blade, look for the Azure Active Directory application you created earlier.</span></span> <span data-ttu-id="83f93-139">If you have a lot of groups to search from, use the text box at the top to filter on the group name.</span><span class="sxs-lookup"><span data-stu-id="83f93-139">If you have a lot of groups to search from, use the text box at the top to filter on the group name.</span></span> <span data-ttu-id="83f93-140">Click the group you want to add and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="83f93-140">Click the group you want to add and then click **Select**.</span></span>
   
    <span data-ttu-id="83f93-141">![Add a group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Add a group")</span><span class="sxs-lookup"><span data-stu-id="83f93-141">![Add a group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Add a group")</span></span>
6. <span data-ttu-id="83f93-142">Click **Select Permissions**, select the permissions and whether you want to assign the permissions as a default ACL, access ACL, or both.</span><span class="sxs-lookup"><span data-stu-id="83f93-142">Click **Select Permissions**, select the permissions and whether you want to assign the permissions as a default ACL, access ACL, or both.</span></span> <span data-ttu-id="83f93-143">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="83f93-143">Click **OK**.</span></span>
   
    <span data-ttu-id="83f93-144">![Assign permissions to group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "Assign permissions to group")</span><span class="sxs-lookup"><span data-stu-id="83f93-144">![Assign permissions to group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "Assign permissions to group")</span></span>
   
    <span data-ttu-id="83f93-145">For more information about permissions in Data Lake Store, and Default/Access ACLs, see [Access Control in Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="83f93-145">For more information about permissions in Data Lake Store, and Default/Access ACLs, see [Access Control in Data Lake Store](data-lake-store-access-control.md).</span></span>
7. <span data-ttu-id="83f93-146">In the **Add Custom Access** blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="83f93-146">In the **Add Custom Access** blade, click **OK**.</span></span> <span data-ttu-id="83f93-147">The newly added group, with the associated permissions, will now be listed in the **Access** blade.</span><span class="sxs-lookup"><span data-stu-id="83f93-147">The newly added group, with the associated permissions, will now be listed in the **Access** blade.</span></span>
   
    <span data-ttu-id="83f93-148">![Assign permissions to group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "Assign permissions to group")</span><span class="sxs-lookup"><span data-stu-id="83f93-148">![Assign permissions to group](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "Assign permissions to group")</span></span>

## <a name="step-4-get-the-oauth-20-token-endpoint-only-for-java-based-applications"></a><span data-ttu-id="83f93-149">Step 4: Get the OAuth 2.0 token endpoint (only for Java-based applications)</span><span class="sxs-lookup"><span data-stu-id="83f93-149">Step 4: Get the OAuth 2.0 token endpoint (only for Java-based applications)</span></span>

1. <span data-ttu-id="83f93-150">Sign on to the new [Azure portal](https://portal.azure.com) and click Active Directory from the left pane.</span><span class="sxs-lookup"><span data-stu-id="83f93-150">Sign on to the new [Azure portal](https://portal.azure.com) and click Active Directory from the left pane.</span></span>

2. <span data-ttu-id="83f93-151">From the left pane, click **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="83f93-151">From the left pane, click **App registrations**.</span></span>

3. <span data-ttu-id="83f93-152">From the top of the App registrations blade, click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="83f93-152">From the top of the App registrations blade, click **Endpoints**.</span></span>

    <span data-ttu-id="83f93-153">![OAuth token endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth token endpoint")</span><span class="sxs-lookup"><span data-stu-id="83f93-153">![OAuth token endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth token endpoint")</span></span>

4. <span data-ttu-id="83f93-154">From the list of endpoints, copy the OAuth 2.0 token endpoint.</span><span class="sxs-lookup"><span data-stu-id="83f93-154">From the list of endpoints, copy the OAuth 2.0 token endpoint.</span></span>


     <span data-ttu-id="83f93-155">![OAuth token endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth token endpoint")</span><span class="sxs-lookup"><span data-stu-id="83f93-155">![OAuth token endpoint](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-store/media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth token endpoint")</span></span>   

## <a name="next-steps"></a><span data-ttu-id="83f93-156">Next steps</span><span class="sxs-lookup"><span data-stu-id="83f93-156">Next steps</span></span>
<span data-ttu-id="83f93-157">In this article you created an Azure AD web application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span><span class="sxs-lookup"><span data-stu-id="83f93-157">In this article you created an Azure AD web application and gathered the information you need in your client applications that you author using .NET SDK, Java SDK, etc. You can now proceed to the following articles that talk about how to use the Azure AD web application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="83f93-158">Get started with Azure Data Lake Store using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="83f93-158">Get started with Azure Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="83f93-159">Get started with Azure Data Lake Store using Java SDK</span><span class="sxs-lookup"><span data-stu-id="83f93-159">Get started with Azure Data Lake Store using Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)

<span data-ttu-id="83f93-160">This article walked you through the basic steps needed to get a user principal up and running for your application.</span><span class="sxs-lookup"><span data-stu-id="83f93-160">This article walked you through the basic steps needed to get a user principal up and running for your application.</span></span> <span data-ttu-id="83f93-161">You can look at the following articles to get further information:</span><span class="sxs-lookup"><span data-stu-id="83f93-161">You can look at the following articles to get further information:</span></span>
* [<span data-ttu-id="83f93-162">Use PowerShell to create service principal</span><span class="sxs-lookup"><span data-stu-id="83f93-162">Use PowerShell to create service principal</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal)
* [<span data-ttu-id="83f93-163">Use certificate authentication for service principal authentication</span><span class="sxs-lookup"><span data-stu-id="83f93-163">Use certificate authentication for service principal authentication</span></span>](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-authenticate-service-principal#create-service-principal-with-certificate)
* [<span data-ttu-id="83f93-164">Other methods to authenticate to Azure AD</span><span class="sxs-lookup"><span data-stu-id="83f93-164">Other methods to authenticate to Azure AD</span></span>](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-authentication-scenarios)











