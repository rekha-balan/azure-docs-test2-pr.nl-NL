---
title: Use Azure AD authentication to access Azure Media Services API with .NET | Microsoft Docs
description: This topic shows how to use Azure Active Directory (Azure AD) authentication to access Azure Media Services (AMS) API with .NET.
services: media-services
documentationcenter: ''
author: Juliako
manager: cfowler
editor: ''
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/27/2018
ms.author: juliako
ms.openlocfilehash: b8f58f4010590dc40d5e8dc7ac1b634f161a807d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965452"
---
# <a name="use-azure-ad-authentication-to-access-azure-media-services-api-with-net"></a><span data-ttu-id="f96ca-103">Use Azure AD authentication to access Azure Media Services API with .NET</span><span class="sxs-lookup"><span data-stu-id="f96ca-103">Use Azure AD authentication to access Azure Media Services API with .NET</span></span>

<span data-ttu-id="f96ca-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="f96ca-104">Starting with windowsazure.mediaservices 4.0.0.4, Azure Media Services supports authentication based on Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="f96ca-105">This topic shows you how to use Azure AD  authentication to access Azure Media Services API with Microsoft .NET.</span><span class="sxs-lookup"><span data-stu-id="f96ca-105">This topic shows you how to use Azure AD  authentication to access Azure Media Services API with Microsoft .NET.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f96ca-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f96ca-106">Prerequisites</span></span>

- <span data-ttu-id="f96ca-107">An Azure account.</span><span class="sxs-lookup"><span data-stu-id="f96ca-107">An Azure account.</span></span> <span data-ttu-id="f96ca-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f96ca-108">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="f96ca-109">A Media Services account.</span><span class="sxs-lookup"><span data-stu-id="f96ca-109">A Media Services account.</span></span> <span data-ttu-id="f96ca-110">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="f96ca-110">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>
- <span data-ttu-id="f96ca-111">The latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span><span class="sxs-lookup"><span data-stu-id="f96ca-111">The latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span>
- <span data-ttu-id="f96ca-112">Familiarity with the topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="f96ca-112">Familiarity with the topic [Accessing Azure Media Services API with AAD authentication overview](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

<span data-ttu-id="f96ca-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span><span class="sxs-lookup"><span data-stu-id="f96ca-113">When you're using Azure AD authentication with Azure Media Services, you can authenticate in one of two ways:</span></span>

- <span data-ttu-id="f96ca-114">**User authentication** authenticates a person who is using the app to interact with Azure Media Services resources.</span><span class="sxs-lookup"><span data-stu-id="f96ca-114">**User authentication** authenticates a person who is using the app to interact with Azure Media Services resources.</span></span> <span data-ttu-id="f96ca-115">The interactive application should first prompt the user for credentials.</span><span class="sxs-lookup"><span data-stu-id="f96ca-115">The interactive application should first prompt the user for credentials.</span></span> <span data-ttu-id="f96ca-116">An example is a management console app that's used by authorized users to monitor encoding jobs or live streaming.</span><span class="sxs-lookup"><span data-stu-id="f96ca-116">An example is a management console app that's used by authorized users to monitor encoding jobs or live streaming.</span></span> 
- <span data-ttu-id="f96ca-117">**Service principal authentication** authenticates a service.</span><span class="sxs-lookup"><span data-stu-id="f96ca-117">**Service principal authentication** authenticates a service.</span></span> <span data-ttu-id="f96ca-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span><span class="sxs-lookup"><span data-stu-id="f96ca-118">Applications that commonly use this authentication method are apps that run daemon services, middle-tier services, or scheduled jobs, such as web apps, function apps, logic apps, APIs, or microservices.</span></span>

>[!IMPORTANT]
><span data-ttu-id="f96ca-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span><span class="sxs-lookup"><span data-stu-id="f96ca-119">Azure Media Service currently supports an Azure Access Control Service  authentication model.</span></span> <span data-ttu-id="f96ca-120">However, Access Control authorization is going to be deprecated on June 22, 2018.</span><span class="sxs-lookup"><span data-stu-id="f96ca-120">However, Access Control authorization is going to be deprecated on June 22, 2018.</span></span> <span data-ttu-id="f96ca-121">We recommend that you migrate to an Azure Active Directory authentication model as soon as possible.</span><span class="sxs-lookup"><span data-stu-id="f96ca-121">We recommend that you migrate to an Azure Active Directory authentication model as soon as possible.</span></span>

## <a name="get-an-azure-ad-access-token"></a><span data-ttu-id="f96ca-122">Get an Azure AD access token</span><span class="sxs-lookup"><span data-stu-id="f96ca-122">Get an Azure AD access token</span></span>

<span data-ttu-id="f96ca-123">To connect to the Azure Media Services API with Azure AD authentication, the client app needs to request an Azure AD access token.</span><span class="sxs-lookup"><span data-stu-id="f96ca-123">To connect to the Azure Media Services API with Azure AD authentication, the client app needs to request an Azure AD access token.</span></span> <span data-ttu-id="f96ca-124">When you use the Media Services .NET client SDK, many of the details about how to acquire an Azure AD access token are wrapped and simplified for you in the [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span><span class="sxs-lookup"><span data-stu-id="f96ca-124">When you use the Media Services .NET client SDK, many of the details about how to acquire an Azure AD access token are wrapped and simplified for you in the [AzureAdTokenProvider](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenProvider.cs) and [AzureAdTokenCredentials](https://github.com/Azure/azure-sdk-for-media-services/blob/dev/src/net/Client/Common/Common.Authentication/AzureAdTokenCredentials.cs) classes.</span></span> 

<span data-ttu-id="f96ca-125">For example, you don't need to provide the Azure AD authority, Media Services resource URI, or native Azure AD application details.</span><span class="sxs-lookup"><span data-stu-id="f96ca-125">For example, you don't need to provide the Azure AD authority, Media Services resource URI, or native Azure AD application details.</span></span> <span data-ttu-id="f96ca-126">These are well-known values that are already configured by the Azure AD access token provider class.</span><span class="sxs-lookup"><span data-stu-id="f96ca-126">These are well-known values that are already configured by the Azure AD access token provider class.</span></span> 

<span data-ttu-id="f96ca-127">If you are not using Azure Media Service .NET SDK, we recommend that you use the [Azure AD Authentication Library](../../active-directory/develop/active-directory-authentication-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="f96ca-127">If you are not using Azure Media Service .NET SDK, we recommend that you use the [Azure AD Authentication Library](../../active-directory/develop/active-directory-authentication-libraries.md).</span></span> <span data-ttu-id="f96ca-128">To get values for the parameters that you need to use with Azure AD Authentication Library, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="f96ca-128">To get values for the parameters that you need to use with Azure AD Authentication Library, see [Use the Azure portal to access Azure AD authentication settings](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="f96ca-129">You also have the option of replacing the default implementation of the **AzureAdTokenProvider** with your own implementation.</span><span class="sxs-lookup"><span data-stu-id="f96ca-129">You also have the option of replacing the default implementation of the **AzureAdTokenProvider** with your own implementation.</span></span>

## <a name="install-and-configure-azure-media-services-net-sdk"></a><span data-ttu-id="f96ca-130">Install and configure Azure Media Services .NET SDK</span><span class="sxs-lookup"><span data-stu-id="f96ca-130">Install and configure Azure Media Services .NET SDK</span></span>

>[!NOTE] 
><span data-ttu-id="f96ca-131">To use Azure AD authentication with the Media Services .NET SDK, you need to have the latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span><span class="sxs-lookup"><span data-stu-id="f96ca-131">To use Azure AD authentication with the Media Services .NET SDK, you need to have the latest [NuGet](https://www.nuget.org/packages/windowsazure.mediaservices) package.</span></span> <span data-ttu-id="f96ca-132">Also, add a reference to the **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span><span class="sxs-lookup"><span data-stu-id="f96ca-132">Also, add a reference to the **Microsoft.IdentityModel.Clients.ActiveDirectory** assembly.</span></span> <span data-ttu-id="f96ca-133">If you are using an existing app, include the **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span><span class="sxs-lookup"><span data-stu-id="f96ca-133">If you are using an existing app, include the **Microsoft.WindowsAzure.MediaServices.Client.Common.Authentication.dll** assembly.</span></span> 

1. <span data-ttu-id="f96ca-134">Create a new C# console application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f96ca-134">Create a new C# console application in Visual Studio.</span></span>
2. <span data-ttu-id="f96ca-135">Use the [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package to install **Azure Media Services .NET SDK**.</span><span class="sxs-lookup"><span data-stu-id="f96ca-135">Use the [windowsazure.mediaservices](https://www.nuget.org/packages/windowsazure.mediaservices) NuGet package to install **Azure Media Services .NET SDK**.</span></span> 

    <span data-ttu-id="f96ca-136">To add references by using NuGet, take the following steps: in **Solution Explorer**, right-click the project name, and then select **Manage NuGet packages**.</span><span class="sxs-lookup"><span data-stu-id="f96ca-136">To add references by using NuGet, take the following steps: in **Solution Explorer**, right-click the project name, and then select **Manage NuGet packages**.</span></span> <span data-ttu-id="f96ca-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span><span class="sxs-lookup"><span data-stu-id="f96ca-137">Then, search for **windowsazure.mediaservices** and select **Install**.</span></span>
    
    <span data-ttu-id="f96ca-138">-or-</span><span class="sxs-lookup"><span data-stu-id="f96ca-138">-or-</span></span>

    <span data-ttu-id="f96ca-139">Run the following command in **Package Manager Console** in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="f96ca-139">Run the following command in **Package Manager Console** in Visual Studio.</span></span>

        Install-Package windowsazure.mediaservices -Version 4.0.0.4

3. <span data-ttu-id="f96ca-140">Add **using** to your source code.</span><span class="sxs-lookup"><span data-stu-id="f96ca-140">Add **using** to your source code.</span></span>

        using Microsoft.WindowsAzure.MediaServices.Client; 

## <a name="use-user-authentication"></a><span data-ttu-id="f96ca-141">Use user authentication</span><span class="sxs-lookup"><span data-stu-id="f96ca-141">Use user authentication</span></span>

<span data-ttu-id="f96ca-142">To connect to the Azure Media Service API with the user authentication option, the client app needs to request an Azure AD token by using the following parameters:</span><span class="sxs-lookup"><span data-stu-id="f96ca-142">To connect to the Azure Media Service API with the user authentication option, the client app needs to request an Azure AD token by using the following parameters:</span></span>  

- <span data-ttu-id="f96ca-143">Azure AD tenant endpoint.</span><span class="sxs-lookup"><span data-stu-id="f96ca-143">Azure AD tenant endpoint.</span></span> <span data-ttu-id="f96ca-144">The tenant information can be retrieved from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f96ca-144">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="f96ca-145">Hover over the signed-in user in the upper-right corner.</span><span class="sxs-lookup"><span data-stu-id="f96ca-145">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="f96ca-146">Media Services resource URI.</span><span class="sxs-lookup"><span data-stu-id="f96ca-146">Media Services resource URI.</span></span>
- <span data-ttu-id="f96ca-147">Media Services (native) application client ID.</span><span class="sxs-lookup"><span data-stu-id="f96ca-147">Media Services (native) application client ID.</span></span> 
- <span data-ttu-id="f96ca-148">Media Services (native) application redirect URI.</span><span class="sxs-lookup"><span data-stu-id="f96ca-148">Media Services (native) application redirect URI.</span></span> 

<span data-ttu-id="f96ca-149">The values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span><span class="sxs-lookup"><span data-stu-id="f96ca-149">The values for these parameters can be found in **AzureEnvironments.AzureCloudEnvironment**.</span></span> <span data-ttu-id="f96ca-150">The **AzureEnvironments.AzureCloudEnvironment** constant is a helper in the .NET SDK to get the right environment variable settings for a public Azure Data Center.</span><span class="sxs-lookup"><span data-stu-id="f96ca-150">The **AzureEnvironments.AzureCloudEnvironment** constant is a helper in the .NET SDK to get the right environment variable settings for a public Azure Data Center.</span></span> 

<span data-ttu-id="f96ca-151">It contains pre-defined environment settings for accessing Media Services in the public data centers only.</span><span class="sxs-lookup"><span data-stu-id="f96ca-151">It contains pre-defined environment settings for accessing Media Services in the public data centers only.</span></span> <span data-ttu-id="f96ca-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span><span class="sxs-lookup"><span data-stu-id="f96ca-152">For sovereign or government cloud regions, you can use **AzureChinaCloudEnvironment**, **AzureUsGovernmentEnvrionment**, or **AzureGermanCloudEnvironment** respectively.</span></span>

<span data-ttu-id="f96ca-153">The following code example creates a token:</span><span class="sxs-lookup"><span data-stu-id="f96ca-153">The following code example creates a token:</span></span>
    
    var tokenCredentials = new AzureAdTokenCredentials("microsoft.onmicrosoft.com", AzureEnvironments.AzureCloudEnvironment);
    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
  
<span data-ttu-id="f96ca-154">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span><span class="sxs-lookup"><span data-stu-id="f96ca-154">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="f96ca-155">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span><span class="sxs-lookup"><span data-stu-id="f96ca-155">The **CloudMediaContext** includes references to important collections including jobs, assets, files, access policies, and locators.</span></span> 

<span data-ttu-id="f96ca-156">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span><span class="sxs-lookup"><span data-stu-id="f96ca-156">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="f96ca-157">To get the resource URI for Media REST Services, sign in to the Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect to Azure Media Services with user authentication**.</span><span class="sxs-lookup"><span data-stu-id="f96ca-157">To get the resource URI for Media REST Services, sign in to the Azure portal, select your Azure Media Services account, select **API access**, and then select **Connect to Azure Media Services with user authentication**.</span></span> 

<span data-ttu-id="f96ca-158">The following code example creates a **CloudMediaContext** instance:</span><span class="sxs-lookup"><span data-stu-id="f96ca-158">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);

<span data-ttu-id="f96ca-159">The following example shows how to create the Azure AD token and the context:</span><span class="sxs-lookup"><span data-stu-id="f96ca-159">The following example shows how to create the Azure AD token and the context:</span></span>

    namespace AADAuthSample
    {
        class Program
        {
            static void Main(string[] args)
            {
                // Specify your Azure AD tenant domain, for example "microsoft.onmicrosoft.com".
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR AAD TENANT DOMAIN HERE}", AzureEnvironments.AzureCloudEnvironment);
    
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
            }
    
        }
    }

>[!NOTE]
><span data-ttu-id="f96ca-160">If you get an exception that says "The remote server returned an error: (401) Unauthorized," see the [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span><span class="sxs-lookup"><span data-stu-id="f96ca-160">If you get an exception that says "The remote server returned an error: (401) Unauthorized," see the [Access control](media-services-use-aad-auth-to-access-ams-api.md#access-control) section of Accessing Azure Media Services API with Azure AD authentication overview.</span></span>

## <a name="use-service-principal-authentication"></a><span data-ttu-id="f96ca-161">Use service principal authentication</span><span class="sxs-lookup"><span data-stu-id="f96ca-161">Use service principal authentication</span></span>
    
<span data-ttu-id="f96ca-162">To connect to the Azure Media Services API with the service principal option, your middle-tier app (web API or web application) needs to requests an Azure AD token with the following parameters:</span><span class="sxs-lookup"><span data-stu-id="f96ca-162">To connect to the Azure Media Services API with the service principal option, your middle-tier app (web API or web application) needs to requests an Azure AD token with the following parameters:</span></span>  

- <span data-ttu-id="f96ca-163">Azure AD tenant endpoint.</span><span class="sxs-lookup"><span data-stu-id="f96ca-163">Azure AD tenant endpoint.</span></span> <span data-ttu-id="f96ca-164">The tenant information can be retrieved from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f96ca-164">The tenant information can be retrieved from the Azure portal.</span></span> <span data-ttu-id="f96ca-165">Hover over the signed-in user in the upper-right corner.</span><span class="sxs-lookup"><span data-stu-id="f96ca-165">Hover over the signed-in user in the upper-right corner.</span></span>
- <span data-ttu-id="f96ca-166">Media Services resource URI.</span><span class="sxs-lookup"><span data-stu-id="f96ca-166">Media Services resource URI.</span></span>
- <span data-ttu-id="f96ca-167">Azure AD application values: the **Client ID** and **Client secret**.</span><span class="sxs-lookup"><span data-stu-id="f96ca-167">Azure AD application values: the **Client ID** and **Client secret**.</span></span>

<span data-ttu-id="f96ca-168">The values for the **Client ID** and **Client secret** parameters can be found in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="f96ca-168">The values for the **Client ID** and **Client secret** parameters can be found in the Azure portal.</span></span> <span data-ttu-id="f96ca-169">For more information, see [Getting started with Azure AD authentication using the Azure portal](media-services-portal-get-started-with-aad.md).</span><span class="sxs-lookup"><span data-stu-id="f96ca-169">For more information, see [Getting started with Azure AD authentication using the Azure portal](media-services-portal-get-started-with-aad.md).</span></span>

<span data-ttu-id="f96ca-170">The following code example creates a token by using the **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span><span class="sxs-lookup"><span data-stu-id="f96ca-170">The following code example creates a token by using the **AzureAdTokenCredentials** constructor that takes **AzureAdClientSymmetricKey** as a parameter:</span></span> 
    
    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                AzureEnvironments.AzureCloudEnvironment);

    var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

<span data-ttu-id="f96ca-171">You can also specify the **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span><span class="sxs-lookup"><span data-stu-id="f96ca-171">You can also specify the **AzureAdTokenCredentials** constructor that takes **AzureAdClientCertificate** as a parameter.</span></span> 

<span data-ttu-id="f96ca-172">For instructions about how to create and configure a certificate in a form that can be used by Azure AD, see [Authenticating to Azure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span><span class="sxs-lookup"><span data-stu-id="f96ca-172">For instructions about how to create and configure a certificate in a form that can be used by Azure AD, see [Authenticating to Azure AD in daemon apps with certificates - manual configuration steps](https://github.com/Azure-Samples/active-directory-dotnet-daemon-certificate-credential/blob/master/Manual-Configuration-Steps.md).</span></span>

    var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                new AzureAdClientCertificate("{YOUR CLIENT ID HERE}", "{YOUR CLIENT CERTIFICATE THUMBPRINT}"), 
                                AzureEnvironments.AzureCloudEnvironment);

<span data-ttu-id="f96ca-173">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span><span class="sxs-lookup"><span data-stu-id="f96ca-173">To start programming against Media Services, you need to create a **CloudMediaContext** instance that represents the server context.</span></span> <span data-ttu-id="f96ca-174">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span><span class="sxs-lookup"><span data-stu-id="f96ca-174">You also need to pass the **resource URI for Media REST Services** to the **CloudMediaContext** constructor.</span></span> <span data-ttu-id="f96ca-175">You can get the **resource URI for Media REST Services** value from the Azure portal as well.</span><span class="sxs-lookup"><span data-stu-id="f96ca-175">You can get the **resource URI for Media REST Services** value from the Azure portal as well.</span></span>

<span data-ttu-id="f96ca-176">The following code example creates a **CloudMediaContext** instance:</span><span class="sxs-lookup"><span data-stu-id="f96ca-176">The following code example creates a **CloudMediaContext** instance:</span></span>

    CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
<span data-ttu-id="f96ca-177">The following example shows how to create the Azure AD token and the context:</span><span class="sxs-lookup"><span data-stu-id="f96ca-177">The following example shows how to create the Azure AD token and the context:</span></span>

    namespace AADAuthSample
    {
    
        class Program
        {
            static void Main(string[] args)
            {
                var tokenCredentials = new AzureAdTokenCredentials("{YOUR Azure AD TENANT DOMAIN HERE}", 
                                            new AzureAdClientSymmetricKey("{YOUR CLIENT ID HERE}", "{YOUR CLIENT SECRET}"), 
                                            AzureEnvironments.AzureCloudEnvironment);
            
                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);
    
                // Specify your REST API endpoint, for example "https://accountname.restv2.westcentralus.media.azure.net/API".      
                CloudMediaContext context = new CloudMediaContext(new Uri("YOUR REST API ENDPOINT HERE"), tokenProvider);
    
                var assets = context.Assets;
                foreach (var a in assets)
                {
                    Console.WriteLine(a.Name);
                }
    
                Console.ReadLine();
            }
    
        }
    }

## <a name="next-steps"></a><span data-ttu-id="f96ca-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="f96ca-178">Next steps</span></span>

<span data-ttu-id="f96ca-179">Get started with [uploading files to your account](media-services-dotnet-upload-files.md).</span><span class="sxs-lookup"><span data-stu-id="f96ca-179">Get started with [uploading files to your account](media-services-dotnet-upload-files.md).</span></span>
