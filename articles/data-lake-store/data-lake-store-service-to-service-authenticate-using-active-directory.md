---
title: 'Service-to-service authentication: Data Lake Store with Azure Active Directory | Microsoft Docs'
description: Learn how to achieve service-to-service authentication with Data Lake Store using Azure Active Directory
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
ms.openlocfilehash: 1e59ed093417d8761135b946e2fa3f183bb085c9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869698"
---
# <a name="service-to-service-authentication-with-data-lake-store-using-azure-active-directory"></a><span data-ttu-id="9d1b5-103">Service-to-service authentication with Data Lake Store using Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="9d1b5-103">Service-to-service authentication with Data Lake Store using Azure Active Directory</span></span>
> [!div class="op_single_selector"]
> * [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md)
> * [Service-to-service authentication](data-lake-store-service-to-service-authenticate-using-active-directory.md)
> 
>  

<span data-ttu-id="9d1b5-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-106">Azure Data Lake Store uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="9d1b5-107">Before authoring an application that works with Azure Data Lake Store, you must decide how to authenticate your application with Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="9d1b5-107">Before authoring an application that works with Azure Data Lake Store, you must decide how to authenticate your application with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="9d1b5-108">The two main options available are:</span><span class="sxs-lookup"><span data-stu-id="9d1b5-108">The two main options available are:</span></span>

* <span data-ttu-id="9d1b5-109">End-user authentication</span><span class="sxs-lookup"><span data-stu-id="9d1b5-109">End-user authentication</span></span> 
* <span data-ttu-id="9d1b5-110">Service-to-service authentication (this article)</span><span class="sxs-lookup"><span data-stu-id="9d1b5-110">Service-to-service authentication (this article)</span></span> 

<span data-ttu-id="9d1b5-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-111">Both these options result in your application being provided with an OAuth 2.0 token, which gets attached to each request made to Azure Data Lake Store.</span></span>

<span data-ttu-id="9d1b5-112">This article talks about how to create an **Azure AD web application for service-to-service authentication**.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-112">This article talks about how to create an **Azure AD web application for service-to-service authentication**.</span></span> <span data-ttu-id="9d1b5-113">For instructions on Azure AD application configuration for end-user authentication, see [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="9d1b5-113">For instructions on Azure AD application configuration for end-user authentication, see [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d1b5-114">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9d1b5-114">Prerequisites</span></span>
* <span data-ttu-id="9d1b5-115">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-115">An Azure subscription.</span></span> <span data-ttu-id="9d1b5-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="9d1b5-116">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

## <a name="step-1-create-an-active-directory-web-application"></a><span data-ttu-id="9d1b5-117">Step 1: Create an Active Directory web application</span><span class="sxs-lookup"><span data-stu-id="9d1b5-117">Step 1: Create an Active Directory web application</span></span>

<span data-ttu-id="9d1b5-118">Create and configure an Azure AD web application for service-to-service authentication with Azure Data Lake Store using Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-118">Create and configure an Azure AD web application for service-to-service authentication with Azure Data Lake Store using Azure Active Directory.</span></span> <span data-ttu-id="9d1b5-119">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span><span class="sxs-lookup"><span data-stu-id="9d1b5-119">For instructions, see [Create an Azure AD application](../azure-resource-manager/resource-group-create-service-principal-portal.md).</span></span>

<span data-ttu-id="9d1b5-120">While following the instructions at the preceding link, make sure you select **Web App / API** for application type, as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="9d1b5-120">While following the instructions at the preceding link, make sure you select **Web App / API** for application type, as shown in the following screenshot:</span></span>

<span data-ttu-id="9d1b5-121">![Create web app](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Create web app")</span><span class="sxs-lookup"><span data-stu-id="9d1b5-121">![Create web app](./media/data-lake-store-authenticate-using-active-directory/azure-active-directory-create-web-app.png "Create web app")</span></span>

## <a name="step-2-get-application-id-authentication-key-and-tenant-id"></a><span data-ttu-id="9d1b5-122">Step 2: Get application ID, authentication key, and tenant ID</span><span class="sxs-lookup"><span data-stu-id="9d1b5-122">Step 2: Get application ID, authentication key, and tenant ID</span></span>
<span data-ttu-id="9d1b5-123">When programmatically logging in, you need the ID for your application.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-123">When programmatically logging in, you need the ID for your application.</span></span> <span data-ttu-id="9d1b5-124">If the application runs under its own credentials, you also need an authentication key.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-124">If the application runs under its own credentials, you also need an authentication key.</span></span>

* <span data-ttu-id="9d1b5-125">For instructions on how to retrieve the application ID and authentication key (also called the client secret) for your application, see [Get application ID and authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span><span class="sxs-lookup"><span data-stu-id="9d1b5-125">For instructions on how to retrieve the application ID and authentication key (also called the client secret) for your application, see [Get application ID and authentication key](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-application-id-and-authentication-key).</span></span>

* <span data-ttu-id="9d1b5-126">For instructions on how to retrieve the tenant ID, see [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="9d1b5-126">For instructions on how to retrieve the tenant ID, see [Get tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>

## <a name="step-3-assign-the-azure-ad-application-to-the-azure-data-lake-store-account-file-or-folder"></a><span data-ttu-id="9d1b5-127">Step 3: Assign the Azure AD application to the Azure Data Lake Store account file or folder</span><span class="sxs-lookup"><span data-stu-id="9d1b5-127">Step 3: Assign the Azure AD application to the Azure Data Lake Store account file or folder</span></span>


1. <span data-ttu-id="9d1b5-128">Sign on to the [Azure portal](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="9d1b5-128">Sign on to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="9d1b5-129">Open the Azure Data Lake Store account that you want to associate with the Azure Active Directory application you created earlier.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-129">Open the Azure Data Lake Store account that you want to associate with the Azure Active Directory application you created earlier.</span></span>
2. <span data-ttu-id="9d1b5-130">In your Data Lake Store account blade, click **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-130">In your Data Lake Store account blade, click **Data Explorer**.</span></span>
   
    <span data-ttu-id="9d1b5-131">![Create directories in Data Lake Store account](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Create directories in Data Lake account")</span><span class="sxs-lookup"><span data-stu-id="9d1b5-131">![Create directories in Data Lake Store account](./media/data-lake-store-authenticate-using-active-directory/adl.start.data.explorer.png "Create directories in Data Lake account")</span></span>
3. <span data-ttu-id="9d1b5-132">In the **Data Explorer** blade, click the file or folder for which you want to provide access to the Azure AD application, and then click **Access**.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-132">In the **Data Explorer** blade, click the file or folder for which you want to provide access to the Azure AD application, and then click **Access**.</span></span> <span data-ttu-id="9d1b5-133">To configure access to a file, you must click **Access** from the **File Preview** blade.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-133">To configure access to a file, you must click **Access** from the **File Preview** blade.</span></span>
   
    <span data-ttu-id="9d1b5-134">![Set ACLs on Data Lake file system](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Set ACLs on Data Lake file system")</span><span class="sxs-lookup"><span data-stu-id="9d1b5-134">![Set ACLs on Data Lake file system](./media/data-lake-store-authenticate-using-active-directory/adl.acl.1.png "Set ACLs on Data Lake file system")</span></span>
4. <span data-ttu-id="9d1b5-135">The **Access** blade lists the standard access and custom access already assigned to the root.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-135">The **Access** blade lists the standard access and custom access already assigned to the root.</span></span> <span data-ttu-id="9d1b5-136">Click the **Add** icon to add custom-level ACLs.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-136">Click the **Add** icon to add custom-level ACLs.</span></span>
   
    <span data-ttu-id="9d1b5-137">![List standard and custom access](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "List standard and custom access")</span><span class="sxs-lookup"><span data-stu-id="9d1b5-137">![List standard and custom access](./media/data-lake-store-authenticate-using-active-directory/adl.acl.2.png "List standard and custom access")</span></span>
5. <span data-ttu-id="9d1b5-138">Click the **Add** icon to open the **Add Custom Access** blade.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-138">Click the **Add** icon to open the **Add Custom Access** blade.</span></span> <span data-ttu-id="9d1b5-139">In this blade, click **Select User or Group**, and then in **Select User or Group** blade, look for the Azure Active Directory application you created earlier.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-139">In this blade, click **Select User or Group**, and then in **Select User or Group** blade, look for the Azure Active Directory application you created earlier.</span></span> <span data-ttu-id="9d1b5-140">If you have many groups to search from, use the text box at the top to filter on the group name.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-140">If you have many groups to search from, use the text box at the top to filter on the group name.</span></span> <span data-ttu-id="9d1b5-141">Click the group you want to add and then click **Select**.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-141">Click the group you want to add and then click **Select**.</span></span>
   
    <span data-ttu-id="9d1b5-142">![Add a group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Add a group")</span><span class="sxs-lookup"><span data-stu-id="9d1b5-142">![Add a group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.3.png "Add a group")</span></span>
6. <span data-ttu-id="9d1b5-143">Click **Select Permissions**, select the permissions and whether you want to assign the permissions as a default ACL, access ACL, or both.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-143">Click **Select Permissions**, select the permissions and whether you want to assign the permissions as a default ACL, access ACL, or both.</span></span> <span data-ttu-id="9d1b5-144">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-144">Click **OK**.</span></span>
   
    <span data-ttu-id="9d1b5-145">![Assign permissions to group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "Assign permissions to group")</span><span class="sxs-lookup"><span data-stu-id="9d1b5-145">![Assign permissions to group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.4.png "Assign permissions to group")</span></span>
   
    <span data-ttu-id="9d1b5-146">For more information about permissions in Data Lake Store, and Default/Access ACLs, see [Access Control in Data Lake Store](data-lake-store-access-control.md).</span><span class="sxs-lookup"><span data-stu-id="9d1b5-146">For more information about permissions in Data Lake Store, and Default/Access ACLs, see [Access Control in Data Lake Store](data-lake-store-access-control.md).</span></span>
7. <span data-ttu-id="9d1b5-147">In the **Add Custom Access** blade, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-147">In the **Add Custom Access** blade, click **OK**.</span></span> <span data-ttu-id="9d1b5-148">The newly added group, with the associated permissions, are listed in the **Access** blade.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-148">The newly added group, with the associated permissions, are listed in the **Access** blade.</span></span>
   
    <span data-ttu-id="9d1b5-149">![Assign permissions to group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "Assign permissions to group")</span><span class="sxs-lookup"><span data-stu-id="9d1b5-149">![Assign permissions to group](./media/data-lake-store-authenticate-using-active-directory/adl.acl.5.png "Assign permissions to group")</span></span>

> [!NOTE]
> If you plan on restricting your Azure Active Directory application to a specific folder, you will also need to give that same Azure Active directory application **Execute** permission to the root to enable file creation access via the .NET SDK.

> [!NOTE]
> If you want to use the SDKs to create a Data Lake Store account, you must assign the Azure AD web application as a role to the Resource Group in which you create the Data Lake Store account.
> 
>

## <a name="step-4-get-the-oauth-20-token-endpoint-only-for-java-based-applications"></a><span data-ttu-id="9d1b5-152">Step 4: Get the OAuth 2.0 token endpoint (only for Java-based applications)</span><span class="sxs-lookup"><span data-stu-id="9d1b5-152">Step 4: Get the OAuth 2.0 token endpoint (only for Java-based applications)</span></span>

1. <span data-ttu-id="9d1b5-153">Sign on to the [Azure portal](https://portal.azure.com) and click Active Directory from the left pane.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-153">Sign on to the [Azure portal](https://portal.azure.com) and click Active Directory from the left pane.</span></span>

2. <span data-ttu-id="9d1b5-154">From the left pane, click **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-154">From the left pane, click **App registrations**.</span></span>

3. <span data-ttu-id="9d1b5-155">From the top of the App registrations blade, click **Endpoints**.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-155">From the top of the App registrations blade, click **Endpoints**.</span></span>

    <span data-ttu-id="9d1b5-156">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth token endpoint")</span><span class="sxs-lookup"><span data-stu-id="9d1b5-156">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint.png "OAuth token endpoint")</span></span>

4. <span data-ttu-id="9d1b5-157">From the list of endpoints, copy the OAuth 2.0 token endpoint.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-157">From the list of endpoints, copy the OAuth 2.0 token endpoint.</span></span>

    <span data-ttu-id="9d1b5-158">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth token endpoint")</span><span class="sxs-lookup"><span data-stu-id="9d1b5-158">![OAuth token endpoint](./media/data-lake-store-authenticate-using-active-directory/oauth-token-endpoint-1.png "OAuth token endpoint")</span></span>   

## <a name="next-steps"></a><span data-ttu-id="9d1b5-159">Next steps</span><span class="sxs-lookup"><span data-stu-id="9d1b5-159">Next steps</span></span>
<span data-ttu-id="9d1b5-160">In this article, you created an Azure AD web application and gathered the information you need in your client applications that you author using .NET SDK, Java, Python, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD native application to first authenticate with Data Lake Store and then perform other operations on the store.</span><span class="sxs-lookup"><span data-stu-id="9d1b5-160">In this article, you created an Azure AD web application and gathered the information you need in your client applications that you author using .NET SDK, Java, Python, REST API, etc. You can now proceed to the following articles that talk about how to use the Azure AD native application to first authenticate with Data Lake Store and then perform other operations on the store.</span></span>

* [<span data-ttu-id="9d1b5-161">Service-to-service authentication with Data Lake Store using Java</span><span class="sxs-lookup"><span data-stu-id="9d1b5-161">Service-to-service authentication with Data Lake Store using Java</span></span>](data-lake-store-service-to-service-authenticate-java.md)
* [<span data-ttu-id="9d1b5-162">Service-to-service authentication with Data Lake Store using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="9d1b5-162">Service-to-service authentication with Data Lake Store using .NET SDK</span></span>](data-lake-store-service-to-service-authenticate-net-sdk.md)
* [<span data-ttu-id="9d1b5-163">Service-to-service authentication with Data Lake Store using Python</span><span class="sxs-lookup"><span data-stu-id="9d1b5-163">Service-to-service authentication with Data Lake Store using Python</span></span>](data-lake-store-service-to-service-authenticate-python.md)
* [<span data-ttu-id="9d1b5-164">Service-to-service authentication with Data Lake Store using REST API</span><span class="sxs-lookup"><span data-stu-id="9d1b5-164">Service-to-service authentication with Data Lake Store using REST API</span></span>](data-lake-store-service-to-service-authenticate-rest-api.md)


