---
title: 'End-user authentication: .NET SDK with Data Lake Store using Azure Active Directory | Microsoft Docs'
description: Learn how to achieve end-user authentication with Data Lake Store using Azure Active Directory with .NET SDK
services: data-lake-store
documentationcenter: ''
author: nitinme
manager: cgronlun
editor: cgronlun
ms.service: data-lake-store
ms.devlang: na
ms.topic: conceptual
ms.date: 05/29/2018
ms.author: nitinme
ms.openlocfilehash: cbb0f703f61b6c15b3a827dc75821286b7914c21
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857687"
---
# <a name="end-user-authentication-with-data-lake-store-using-net-sdk"></a><span data-ttu-id="8fcf4-103">End-user authentication with Data Lake Store using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8fcf4-103">End-user authentication with Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [Using Java](data-lake-store-end-user-authenticate-java-sdk.md)
> * [Using .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md)
> * [Using Python](data-lake-store-end-user-authenticate-python.md)
> * [Using REST API](data-lake-store-end-user-authenticate-rest-api.md)
> 
>  

<span data-ttu-id="8fcf4-108">In this article, you learn about how to use the .NET SDK to do end-user authentication with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-108">In this article, you learn about how to use the .NET SDK to do end-user authentication with Azure Data Lake Store.</span></span> <span data-ttu-id="8fcf4-109">For service-to-service authentication with Data Lake Store using .NET SDK, see [Service-to-service authentication with Data Lake Store using .NET SDK](data-lake-store-service-to-service-authenticate-net-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="8fcf4-109">For service-to-service authentication with Data Lake Store using .NET SDK, see [Service-to-service authentication with Data Lake Store using .NET SDK](data-lake-store-service-to-service-authenticate-net-sdk.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8fcf4-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="8fcf4-110">Prerequisites</span></span>
* <span data-ttu-id="8fcf4-111">**Visual Studio 2013, 2015, or 2017**.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-111">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="8fcf4-112">The instructions below use Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-112">The instructions below use Visual Studio 2017.</span></span>

* <span data-ttu-id="8fcf4-113">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-113">**An Azure subscription**.</span></span> <span data-ttu-id="8fcf4-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="8fcf4-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="8fcf4-115">**Create an Azure Active Directory "Native" Application**.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-115">**Create an Azure Active Directory "Native" Application**.</span></span> <span data-ttu-id="8fcf4-116">You must have completed the steps in [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="8fcf4-116">You must have completed the steps in [End-user authentication with Data Lake Store using Azure Active Directory](data-lake-store-end-user-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="8fcf4-117">Create a .NET application</span><span class="sxs-lookup"><span data-stu-id="8fcf4-117">Create a .NET application</span></span>
1. <span data-ttu-id="8fcf4-118">Open Visual Studio and create a console application.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-118">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="8fcf4-119">From the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-119">From the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="8fcf4-120">From **New Project**, type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="8fcf4-120">From **New Project**, type or select the following values:</span></span>

   | <span data-ttu-id="8fcf4-121">Property</span><span class="sxs-lookup"><span data-stu-id="8fcf4-121">Property</span></span> | <span data-ttu-id="8fcf4-122">Value</span><span class="sxs-lookup"><span data-stu-id="8fcf4-122">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="8fcf4-123">Category</span><span class="sxs-lookup"><span data-stu-id="8fcf4-123">Category</span></span> |<span data-ttu-id="8fcf4-124">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="8fcf4-124">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="8fcf4-125">Template</span><span class="sxs-lookup"><span data-stu-id="8fcf4-125">Template</span></span> |<span data-ttu-id="8fcf4-126">Console Application</span><span class="sxs-lookup"><span data-stu-id="8fcf4-126">Console Application</span></span> |
   | <span data-ttu-id="8fcf4-127">Name</span><span class="sxs-lookup"><span data-stu-id="8fcf4-127">Name</span></span> |<span data-ttu-id="8fcf4-128">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="8fcf4-128">CreateADLApplication</span></span> |

4. <span data-ttu-id="8fcf4-129">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-129">Click **OK** to create the project.</span></span>

5. <span data-ttu-id="8fcf4-130">Add the NuGet packages to your project.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-130">Add the NuGet packages to your project.</span></span>

   1. <span data-ttu-id="8fcf4-131">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-131">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="8fcf4-132">In the **NuGet Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-132">In the **NuGet Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="8fcf4-133">Search for and install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="8fcf4-133">Search for and install the following NuGet packages:</span></span>

      * <span data-ttu-id="8fcf4-134">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-134">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="8fcf4-135">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-135">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="8fcf4-136">![Add a NuGet source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span><span class="sxs-lookup"><span data-stu-id="8fcf4-136">![Add a NuGet source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="8fcf4-137">Close the **NuGet Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-137">Close the **NuGet Package Manager**.</span></span>

6. <span data-ttu-id="8fcf4-138">Open **Program.cs**</span><span class="sxs-lookup"><span data-stu-id="8fcf4-138">Open **Program.cs**</span></span>
7. <span data-ttu-id="8fcf4-139">Replace the using statements with the following lines:</span><span class="sxs-lookup"><span data-stu-id="8fcf4-139">Replace the using statements with the following lines:</span></span>

    ```csharp
    using System;
    using System.IO;
    using System.Linq;
    using System.Text;
    using System.Threading;
    using System.Collections.Generic;
            
    using Microsoft.Rest;
    using Microsoft.Rest.Azure.Authentication;
    using Microsoft.Azure.Management.DataLake.Store;
    using Microsoft.Azure.Management.DataLake.Store.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    ```     

## <a name="end-user-authentication"></a><span data-ttu-id="8fcf4-140">End-user authentication</span><span class="sxs-lookup"><span data-stu-id="8fcf4-140">End-user authentication</span></span>
<span data-ttu-id="8fcf4-141">Add this snippet in your .NET client application.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-141">Add this snippet in your .NET client application.</span></span> <span data-ttu-id="8fcf4-142">Replace the placeholder values with the values retrieved from an Azure AD native application (listed as prerequisite).</span><span class="sxs-lookup"><span data-stu-id="8fcf4-142">Replace the placeholder values with the values retrieved from an Azure AD native application (listed as prerequisite).</span></span> <span data-ttu-id="8fcf4-143">This snippet lets you authenticate your application **interactively** with Data Lake Store, which means you are prompted to enter your Azure credentials.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-143">This snippet lets you authenticate your application **interactively** with Data Lake Store, which means you are prompted to enter your Azure credentials.</span></span>

<span data-ttu-id="8fcf4-144">For ease of use, the following snippet uses default values for client ID and redirect URI that are valid for any Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-144">For ease of use, the following snippet uses default values for client ID and redirect URI that are valid for any Azure subscription.</span></span> <span data-ttu-id="8fcf4-145">In the following snippet, you only need to provide the value for your tenant ID.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-145">In the following snippet, you only need to provide the value for your tenant ID.</span></span> <span data-ttu-id="8fcf4-146">You can retrieve the Tenant ID using the instructions provided at [Get the tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="8fcf4-146">You can retrieve the Tenant ID using the instructions provided at [Get the tenant ID](../azure-resource-manager/resource-group-create-service-principal-portal.md#get-tenant-id).</span></span>
    
- <span data-ttu-id="8fcf4-147">Replace the Main() function with the following code:</span><span class="sxs-lookup"><span data-stu-id="8fcf4-147">Replace the Main() function with the following code:</span></span>

    ```csharp
    private static void Main(string[] args)
    {
        //User login via interactive popup
        string TENANT = "<AAD-directory-domain>";
        string CLIENTID = "1950a258-227b-4e31-a9cf-717495945fc2";
        System.Uri ARM_TOKEN_AUDIENCE = new System.Uri(@"https://management.core.windows.net/");
        System.Uri ADL_TOKEN_AUDIENCE = new System.Uri(@"https://datalake.azure.net/");
        string MY_DOCUMENTS = System.Environment.GetFolderPath(System.Environment.SpecialFolder.MyDocuments);
        string TOKEN_CACHE_PATH = System.IO.Path.Combine(MY_DOCUMENTS, "my.tokencache");
        var tokenCache = GetTokenCache(TOKEN_CACHE_PATH);
        var armCreds = GetCreds_User_Popup(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, tokenCache);
        var adlCreds = GetCreds_User_Popup(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, tokenCache);
    }
    ```

<span data-ttu-id="8fcf4-148">A couple of things to know about the preceding snippet:</span><span class="sxs-lookup"><span data-stu-id="8fcf4-148">A couple of things to know about the preceding snippet:</span></span>

* <span data-ttu-id="8fcf4-149">The preceeding snippet uses a helper functions `GetTokenCache` and `GetCreds_User_Popup`.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-149">The preceeding snippet uses a helper functions `GetTokenCache` and `GetCreds_User_Popup`.</span></span> <span data-ttu-id="8fcf4-150">The code for these helper functions is available [here on Github](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options#gettokencache).</span><span class="sxs-lookup"><span data-stu-id="8fcf4-150">The code for these helper functions is available [here on Github](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options#gettokencache).</span></span>
* <span data-ttu-id="8fcf4-151">To help you complete the tutorial faster, the snippet uses a native application client ID that is available by default for all Azure subscriptions.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-151">To help you complete the tutorial faster, the snippet uses a native application client ID that is available by default for all Azure subscriptions.</span></span> <span data-ttu-id="8fcf4-152">So, you can **use this snippet as-is in your application**.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-152">So, you can **use this snippet as-is in your application**.</span></span>
* <span data-ttu-id="8fcf4-153">However, if you do want to use your own Azure AD domain and application client ID, you must create an Azure AD native application and then use the Azure AD tenant ID, client ID, and redirect URI for the application you created.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-153">However, if you do want to use your own Azure AD domain and application client ID, you must create an Azure AD native application and then use the Azure AD tenant ID, client ID, and redirect URI for the application you created.</span></span> <span data-ttu-id="8fcf4-154">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-154">See [Create an Active Directory Application for end-user authentication with Data Lake Store](data-lake-store-end-user-authenticate-using-active-directory.md) for instructions.</span></span>

  
## <a name="next-steps"></a><span data-ttu-id="8fcf4-155">Next steps</span><span class="sxs-lookup"><span data-stu-id="8fcf4-155">Next steps</span></span>
<span data-ttu-id="8fcf4-156">In this article, you learned how to use end-user authentication to authenticate with Azure Data Lake Store using .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-156">In this article, you learned how to use end-user authentication to authenticate with Azure Data Lake Store using .NET SDK.</span></span> <span data-ttu-id="8fcf4-157">You can now look at the following articles that talk about how to use the .NET SDK to work with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8fcf4-157">You can now look at the following articles that talk about how to use the .NET SDK to work with Azure Data Lake Store.</span></span>

* [<span data-ttu-id="8fcf4-158">Account management operations on Data Lake Store using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8fcf4-158">Account management operations on Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="8fcf4-159">Data operations on Data Lake Store using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="8fcf4-159">Data operations on Data Lake Store using .NET SDK</span></span>](data-lake-store-data-operations-net-sdk.md)

