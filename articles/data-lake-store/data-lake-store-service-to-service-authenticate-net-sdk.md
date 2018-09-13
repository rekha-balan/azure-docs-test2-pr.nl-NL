---
title: 'Service-to-service authentication: .NET SDK with Data Lake Store using Azure Active Directory | Microsoft Docs'
description: Learn how to achieve service-to-service authentication with Data Lake Store using Azure Active Directory using .NET SDK
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
ms.openlocfilehash: 388b84024a031a181625404ec1429087982dffbe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866652"
---
# <a name="service-to-service-authentication-with-data-lake-store-using-net-sdk"></a><span data-ttu-id="611d6-103">Service-to-service authentication with Data Lake Store using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="611d6-103">Service-to-service authentication with Data Lake Store using .NET SDK</span></span>
> [!div class="op_single_selector"]
> * [Using Java](data-lake-store-service-to-service-authenticate-java.md)
> * [Using .NET SDK](data-lake-store-service-to-service-authenticate-net-sdk.md)
> * [Using Python](data-lake-store-service-to-service-authenticate-python.md)
> * [Using REST API](data-lake-store-service-to-service-authenticate-rest-api.md)
> 
>  

<span data-ttu-id="611d6-108">In this article, you learn about how to use the .NET SDK to do service-to-service authentication with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="611d6-108">In this article, you learn about how to use the .NET SDK to do service-to-service authentication with Azure Data Lake Store.</span></span> <span data-ttu-id="611d6-109">For end-user authentication with Data Lake Store using .NET SDK, see [End-user authentication with Data Lake Store using .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="611d6-109">For end-user authentication with Data Lake Store using .NET SDK, see [End-user authentication with Data Lake Store using .NET SDK](data-lake-store-end-user-authenticate-net-sdk.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="611d6-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="611d6-110">Prerequisites</span></span>
* <span data-ttu-id="611d6-111">**Visual Studio 2013, 2015, or 2017**.</span><span class="sxs-lookup"><span data-stu-id="611d6-111">**Visual Studio 2013, 2015, or 2017**.</span></span> <span data-ttu-id="611d6-112">The instructions below use Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="611d6-112">The instructions below use Visual Studio 2017.</span></span>

* <span data-ttu-id="611d6-113">**An Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="611d6-113">**An Azure subscription**.</span></span> <span data-ttu-id="611d6-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="611d6-114">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="611d6-115">**Create an Azure Active Directory "Web" Application**.</span><span class="sxs-lookup"><span data-stu-id="611d6-115">**Create an Azure Active Directory "Web" Application**.</span></span> <span data-ttu-id="611d6-116">You must have completed the steps in [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-service-to-service-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="611d6-116">You must have completed the steps in [Service-to-service authentication with Data Lake Store using Azure Active Directory](data-lake-store-service-to-service-authenticate-using-active-directory.md).</span></span>

## <a name="create-a-net-application"></a><span data-ttu-id="611d6-117">Create a .NET application</span><span class="sxs-lookup"><span data-stu-id="611d6-117">Create a .NET application</span></span>
1. <span data-ttu-id="611d6-118">Open Visual Studio and create a console application.</span><span class="sxs-lookup"><span data-stu-id="611d6-118">Open Visual Studio and create a console application.</span></span>
2. <span data-ttu-id="611d6-119">From the **File** menu, click **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="611d6-119">From the **File** menu, click **New**, and then click **Project**.</span></span>
3. <span data-ttu-id="611d6-120">From **New Project**, type or select the following values:</span><span class="sxs-lookup"><span data-stu-id="611d6-120">From **New Project**, type or select the following values:</span></span>

   | <span data-ttu-id="611d6-121">Property</span><span class="sxs-lookup"><span data-stu-id="611d6-121">Property</span></span> | <span data-ttu-id="611d6-122">Value</span><span class="sxs-lookup"><span data-stu-id="611d6-122">Value</span></span> |
   | --- | --- |
   | <span data-ttu-id="611d6-123">Category</span><span class="sxs-lookup"><span data-stu-id="611d6-123">Category</span></span> |<span data-ttu-id="611d6-124">Templates/Visual C#/Windows</span><span class="sxs-lookup"><span data-stu-id="611d6-124">Templates/Visual C#/Windows</span></span> |
   | <span data-ttu-id="611d6-125">Template</span><span class="sxs-lookup"><span data-stu-id="611d6-125">Template</span></span> |<span data-ttu-id="611d6-126">Console Application</span><span class="sxs-lookup"><span data-stu-id="611d6-126">Console Application</span></span> |
   | <span data-ttu-id="611d6-127">Name</span><span class="sxs-lookup"><span data-stu-id="611d6-127">Name</span></span> |<span data-ttu-id="611d6-128">CreateADLApplication</span><span class="sxs-lookup"><span data-stu-id="611d6-128">CreateADLApplication</span></span> |
4. <span data-ttu-id="611d6-129">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="611d6-129">Click **OK** to create the project.</span></span>

5. <span data-ttu-id="611d6-130">Add the NuGet packages to your project.</span><span class="sxs-lookup"><span data-stu-id="611d6-130">Add the NuGet packages to your project.</span></span>

   1. <span data-ttu-id="611d6-131">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="611d6-131">Right-click the project name in the Solution Explorer and click **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="611d6-132">In the **NuGet Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span><span class="sxs-lookup"><span data-stu-id="611d6-132">In the **NuGet Package Manager** tab, make sure that **Package source** is set to **nuget.org** and that **Include prerelease** check box is selected.</span></span>
   3. <span data-ttu-id="611d6-133">Search for and install the following NuGet packages:</span><span class="sxs-lookup"><span data-stu-id="611d6-133">Search for and install the following NuGet packages:</span></span>

      * <span data-ttu-id="611d6-134">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span><span class="sxs-lookup"><span data-stu-id="611d6-134">`Microsoft.Azure.Management.DataLake.Store` - This tutorial uses v2.1.3-preview.</span></span>
      * <span data-ttu-id="611d6-135">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span><span class="sxs-lookup"><span data-stu-id="611d6-135">`Microsoft.Rest.ClientRuntime.Azure.Authentication` - This tutorial uses v2.2.12.</span></span>

        <span data-ttu-id="611d6-136">![Add a NuGet source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span><span class="sxs-lookup"><span data-stu-id="611d6-136">![Add a NuGet source](./media/data-lake-store-get-started-net-sdk/data-lake-store-install-nuget-package.png "Create a new Azure Data Lake account")</span></span>
   4. <span data-ttu-id="611d6-137">Close the **NuGet Package Manager**.</span><span class="sxs-lookup"><span data-stu-id="611d6-137">Close the **NuGet Package Manager**.</span></span>

6. <span data-ttu-id="611d6-138">Open **Program.cs**, delete the existing code, and then include the following statements to add references to namespaces.</span><span class="sxs-lookup"><span data-stu-id="611d6-138">Open **Program.cs**, delete the existing code, and then include the following statements to add references to namespaces.</span></span>

        using System;
        using System.IO;
        using System.Linq;
        using System.Text;
        using System.Threading;
        using System.Collections.Generic;
        using System.Security.Cryptography.X509Certificates; // Required only if you are using an Azure AD application created with certificates
                
        using Microsoft.Rest;
        using Microsoft.Rest.Azure.Authentication;
        using Microsoft.Azure.Management.DataLake.Store;
        using Microsoft.Azure.Management.DataLake.Store.Models;
        using Microsoft.IdentityModel.Clients.ActiveDirectory;

## <a name="service-to-service-authentication-with-client-secret"></a><span data-ttu-id="611d6-139">Service-to-service authentication with client secret</span><span class="sxs-lookup"><span data-stu-id="611d6-139">Service-to-service authentication with client secret</span></span>
<span data-ttu-id="611d6-140">Add this snippet in your .NET client application.</span><span class="sxs-lookup"><span data-stu-id="611d6-140">Add this snippet in your .NET client application.</span></span> <span data-ttu-id="611d6-141">Replace the placeholder values with the values retrieved from an Azure AD web application (listed as a prerequisite).</span><span class="sxs-lookup"><span data-stu-id="611d6-141">Replace the placeholder values with the values retrieved from an Azure AD web application (listed as a prerequisite).</span></span>  <span data-ttu-id="611d6-142">This snippet lets you authenticate your application **non-interactively** with Data Lake Store using the client secret/key for Azure AD web application.</span><span class="sxs-lookup"><span data-stu-id="611d6-142">This snippet lets you authenticate your application **non-interactively** with Data Lake Store using the client secret/key for Azure AD web application.</span></span> 

    private static void Main(string[] args)
    {    
        // Service principal / appplication authentication with client secret / key
        // Use the client ID of an existing AAD "Web App" application.
        string TENANT = "<AAD-directory-domain>";
        string CLIENTID = "<AAD_WEB_APP_CLIENT_ID>";
        System.Uri ARM_TOKEN_AUDIENCE = new System.Uri(@"https://management.core.windows.net/");
        System.Uri ADL_TOKEN_AUDIENCE = new System.Uri(@"https://datalake.azure.net/");
        string secret_key = "<AAD_WEB_APP_SECRET_KEY>";
        var armCreds = GetCreds_SPI_SecretKey(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, secret_key);
        var adlCreds = GetCreds_SPI_SecretKey(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, secret_key);
    }

<span data-ttu-id="611d6-143">The preceeding snippet uses a helper function `GetCreds_SPI_SecretKey`.</span><span class="sxs-lookup"><span data-stu-id="611d6-143">The preceeding snippet uses a helper function `GetCreds_SPI_SecretKey`.</span></span> <span data-ttu-id="611d6-144">The code for this helper function is available [here on Github](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options#getcreds_spi_secretkey).</span><span class="sxs-lookup"><span data-stu-id="611d6-144">The code for this helper function is available [here on Github](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options#getcreds_spi_secretkey).</span></span>

## <a name="service-to-service-authentication-with-certificate"></a><span data-ttu-id="611d6-145">Service-to-service authentication with certificate</span><span class="sxs-lookup"><span data-stu-id="611d6-145">Service-to-service authentication with certificate</span></span>

<span data-ttu-id="611d6-146">Add this snippet in your .NET client application.</span><span class="sxs-lookup"><span data-stu-id="611d6-146">Add this snippet in your .NET client application.</span></span> <span data-ttu-id="611d6-147">Replace the placeholder values with the values retrieved from an Azure AD web application (listed as a prerequisite).</span><span class="sxs-lookup"><span data-stu-id="611d6-147">Replace the placeholder values with the values retrieved from an Azure AD web application (listed as a prerequisite).</span></span> <span data-ttu-id="611d6-148">This snippet lets you authenticate your application **non-interactively** with Data Lake Store using the certificate for an Azure AD web application.</span><span class="sxs-lookup"><span data-stu-id="611d6-148">This snippet lets you authenticate your application **non-interactively** with Data Lake Store using the certificate for an Azure AD web application.</span></span> <span data-ttu-id="611d6-149">For instructions on how to create an Azure AD application, see [Create service principal with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="611d6-149">For instructions on how to create an Azure AD application, see [Create service principal with certificates](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

    
    private static void Main(string[] args)
    {
        // Service principal / application authentication with certificate
        // Use the client ID and certificate of an existing AAD "Web App" application.
        string TENANT = "<AAD-directory-domain>";
        string CLIENTID = "<AAD_WEB_APP_CLIENT_ID>";
        System.Uri ARM_TOKEN_AUDIENCE = new System.Uri(@"https://management.core.windows.net/");
        System.Uri ADL_TOKEN_AUDIENCE = new System.Uri(@"https://datalake.azure.net/");
        var cert = new X509Certificate2(@"d:\cert.pfx", "<certpassword>");
        var armCreds = GetCreds_SPI_Cert(TENANT, ARM_TOKEN_AUDIENCE, CLIENTID, cert);
        var adlCreds = GetCreds_SPI_Cert(TENANT, ADL_TOKEN_AUDIENCE, CLIENTID, cert);
    }

<span data-ttu-id="611d6-150">The preceeding snippet uses a helper function `GetCreds_SPI_Cert`.</span><span class="sxs-lookup"><span data-stu-id="611d6-150">The preceeding snippet uses a helper function `GetCreds_SPI_Cert`.</span></span> <span data-ttu-id="611d6-151">The code for this helper function is available [here on Github](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options#getcreds_spi_cert).</span><span class="sxs-lookup"><span data-stu-id="611d6-151">The code for this helper function is available [here on Github](https://github.com/Azure-Samples/data-lake-analytics-dotnet-auth-options#getcreds_spi_cert).</span></span>

## <a name="next-steps"></a><span data-ttu-id="611d6-152">Next steps</span><span class="sxs-lookup"><span data-stu-id="611d6-152">Next steps</span></span>
<span data-ttu-id="611d6-153">In this article, you learned how to use service-to-service authentication to authenticate with Azure Data Lake Store using .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="611d6-153">In this article, you learned how to use service-to-service authentication to authenticate with Azure Data Lake Store using .NET SDK.</span></span> <span data-ttu-id="611d6-154">You can now look at the following articles that talk about how to use the .NET SDK to work with Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="611d6-154">You can now look at the following articles that talk about how to use the .NET SDK to work with Azure Data Lake Store.</span></span>

* [<span data-ttu-id="611d6-155">Account management operations on Data Lake Store using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="611d6-155">Account management operations on Data Lake Store using .NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
* [<span data-ttu-id="611d6-156">Data operations on Data Lake Store using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="611d6-156">Data operations on Data Lake Store using .NET SDK</span></span>](data-lake-store-data-operations-net-sdk.md)


