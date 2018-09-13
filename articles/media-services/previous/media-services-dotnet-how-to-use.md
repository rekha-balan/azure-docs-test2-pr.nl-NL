---
title: How to Set Up Computer for Media Services Development with .NET
description: Learn about the prerequisites for Media Services using the Media Services SDK for .NET. Also learn how to create a Visual Studio app.
services: media-services
documentationcenter: ''
author: juliako
manager: cfowler
editor: ''
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 12/09/2017
ms.author: juliako
ms.openlocfilehash: 639d1d6af169a0bb459dd8d6c778503b60c48e2c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857829"
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="21cb7-104">Media Services development with .NET</span><span class="sxs-lookup"><span data-stu-id="21cb7-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../../includes/media-services-selector-setup.md)]

<span data-ttu-id="21cb7-105">This article discusses how to start developing Media Services applications using .NET.</span><span class="sxs-lookup"><span data-stu-id="21cb7-105">This article discusses how to start developing Media Services applications using .NET.</span></span>

<span data-ttu-id="21cb7-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span><span class="sxs-lookup"><span data-stu-id="21cb7-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="21cb7-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span><span class="sxs-lookup"><span data-stu-id="21cb7-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="21cb7-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span><span class="sxs-lookup"><span data-stu-id="21cb7-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="21cb7-109">Both libraries are available through **NuGet** and **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="21cb7-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21cb7-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="21cb7-110">Prerequisites</span></span>
* <span data-ttu-id="21cb7-111">A Media Services account in a new or existing Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="21cb7-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="21cb7-112">See the article [How to Create a Media Services Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="21cb7-112">See the article [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="21cb7-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span><span class="sxs-lookup"><span data-stu-id="21cb7-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="21cb7-114">.NET Framework 4.5 or later.</span><span class="sxs-lookup"><span data-stu-id="21cb7-114">.NET Framework 4.5 or later.</span></span>
* <span data-ttu-id="21cb7-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="21cb7-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="21cb7-116">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="21cb7-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="21cb7-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span><span class="sxs-lookup"><span data-stu-id="21cb7-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="21cb7-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span><span class="sxs-lookup"><span data-stu-id="21cb7-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="21cb7-119">This section shows how to use **NuGet** to add Media Services .NET SDK extensions and other dependent libraries.</span><span class="sxs-lookup"><span data-stu-id="21cb7-119">This section shows how to use **NuGet** to add Media Services .NET SDK extensions and other dependent libraries.</span></span>

<span data-ttu-id="21cb7-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span><span class="sxs-lookup"><span data-stu-id="21cb7-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span></span> <span data-ttu-id="21cb7-121">All the necessary dependencies get downloaded and extracted automatically.</span><span class="sxs-lookup"><span data-stu-id="21cb7-121">All the necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="21cb7-122">Create a new C# Console Application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="21cb7-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="21cb7-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span><span class="sxs-lookup"><span data-stu-id="21cb7-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="21cb7-124">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="21cb7-124">Build the solution.</span></span>
3. <span data-ttu-id="21cb7-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span><span class="sxs-lookup"><span data-stu-id="21cb7-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**).</span></span> <span data-ttu-id="21cb7-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span><span class="sxs-lookup"><span data-stu-id="21cb7-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="21cb7-127">Ensure that you have the newest version of NuGet installed.</span><span class="sxs-lookup"><span data-stu-id="21cb7-127">Ensure that you have the newest version of NuGet installed.</span></span> <span data-ttu-id="21cb7-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="21cb7-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>

    1. <span data-ttu-id="21cb7-129">In Solution Explorer, right-click the name of the project and choose **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="21cb7-129">In Solution Explorer, right-click the name of the project and choose **Manage NuGet Packages**.</span></span>

    2. <span data-ttu-id="21cb7-130">The Manage NuGet Packages dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="21cb7-130">The Manage NuGet Packages dialog box appears.</span></span>

    3. <span data-ttu-id="21cb7-131">In the Online gallery, search for Azure MediaServices Extensions, choose **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**), and then click the **Install** button.</span><span class="sxs-lookup"><span data-stu-id="21cb7-131">In the Online gallery, search for Azure MediaServices Extensions, choose **Azure Media Services .NET SDK Extensions** (**windowsazure.mediaservices.extensions**), and then click the **Install** button.</span></span>
   
    4. <span data-ttu-id="21cb7-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span><span class="sxs-lookup"><span data-stu-id="21cb7-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
4. <span data-ttu-id="21cb7-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span><span class="sxs-lookup"><span data-stu-id="21cb7-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="21cb7-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="21cb7-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
5. <span data-ttu-id="21cb7-135">Add a reference to **System.Configuration** assembly.</span><span class="sxs-lookup"><span data-stu-id="21cb7-135">Add a reference to **System.Configuration** assembly.</span></span> <span data-ttu-id="21cb7-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span><span class="sxs-lookup"><span data-stu-id="21cb7-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span></span>
   
    1. <span data-ttu-id="21cb7-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="21cb7-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span></span> <span data-ttu-id="21cb7-138">Then, click **Add**, then click **Reference...**.</span><span class="sxs-lookup"><span data-stu-id="21cb7-138">Then, click **Add**, then click **Reference...**.</span></span>
   
    2. <span data-ttu-id="21cb7-139">The Manage References dialog appears.</span><span class="sxs-lookup"><span data-stu-id="21cb7-139">The Manage References dialog appears.</span></span>
    3. <span data-ttu-id="21cb7-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press **OK**.</span><span class="sxs-lookup"><span data-stu-id="21cb7-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press **OK**.</span></span>
6. <span data-ttu-id="21cb7-141">Open the App.config file and add an **appSettings** section to the file.</span><span class="sxs-lookup"><span data-stu-id="21cb7-141">Open the App.config file and add an **appSettings** section to the file.</span></span> <span data-ttu-id="21cb7-142">Set the values that are needed to connect to the Media Services API.</span><span class="sxs-lookup"><span data-stu-id="21cb7-142">Set the values that are needed to connect to the Media Services API.</span></span> <span data-ttu-id="21cb7-143">For more information, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span><span class="sxs-lookup"><span data-stu-id="21cb7-143">For more information, see [Access the Azure Media Services API with Azure AD authentication](media-services-use-aad-auth-to-access-ams-api.md).</span></span> 

    <span data-ttu-id="21cb7-144">Set the values that are needed to connect using the **Service principal** authentication method.</span><span class="sxs-lookup"><span data-stu-id="21cb7-144">Set the values that are needed to connect using the **Service principal** authentication method.</span></span>

        ```csharp
                <configuration>
                ...
                    <appSettings>
                        <add key="AMSAADTenantDomain" value="tenant"/>
                        <add key="AMSRESTAPIEndpoint" value="endpoint"/>
                        <add key="AMSClientId" value="id"/>
                        <add key="AMSClientSecret" value="secret"/>
                    </appSettings>
                </configuration>
        ```

7. <span data-ttu-id="21cb7-145">Add the **System.Configuration** reference to your project.</span><span class="sxs-lookup"><span data-stu-id="21cb7-145">Add the **System.Configuration** reference to your project.</span></span>
8. <span data-ttu-id="21cb7-146">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code:</span><span class="sxs-lookup"><span data-stu-id="21cb7-146">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code:</span></span>

    ```csharp      
            using System;
            using System.Configuration;
            using System.IO;
            using Microsoft.WindowsAzure.MediaServices.Client;
            using System.Threading;
            using System.Collections.Generic;
            using System.Linq;
    ```

    <span data-ttu-id="21cb7-147">At this point, you are ready to start developing a Media Services application.</span><span class="sxs-lookup"><span data-stu-id="21cb7-147">At this point, you are ready to start developing a Media Services application.</span></span>    

## <a name="example"></a><span data-ttu-id="21cb7-148">Example</span><span class="sxs-lookup"><span data-stu-id="21cb7-148">Example</span></span>

<span data-ttu-id="21cb7-149">Here is a small example that connects to the AMS API and lists all available Media Processors.</span><span class="sxs-lookup"><span data-stu-id="21cb7-149">Here is a small example that connects to the AMS API and lists all available Media Processors.</span></span>

```csharp
        class Program
        {
            // Read values from the App.config file.

            private static readonly string _AADTenantDomain =
                ConfigurationManager.AppSettings["AMSAADTenantDomain"];
            private static readonly string _RESTAPIEndpoint =
                ConfigurationManager.AppSettings["AMSRESTAPIEndpoint"];
            private static readonly string _AMSClientId =
                ConfigurationManager.AppSettings["AMSClientId"];
            private static readonly string _AMSClientSecret =
                ConfigurationManager.AppSettings["AMSClientSecret"];
        
            private static CloudMediaContext _context = null;
            static void Main(string[] args)
            {
                AzureAdTokenCredentials tokenCredentials = 
                    new AzureAdTokenCredentials(_AADTenantDomain,
                        new AzureAdClientSymmetricKey(_AMSClientId, _AMSClientSecret),
                        AzureEnvironments.AzureCloudEnvironment);

                var tokenProvider = new AzureAdTokenProvider(tokenCredentials);

                _context = new CloudMediaContext(new Uri(_RESTAPIEndpoint), tokenProvider);
        
                // List all available Media Processors
                foreach (var mp in _context.MediaProcessors)
                {
                    Console.WriteLine(mp.Name);
                }
        
            }
 ```

## <a name="next-steps"></a><span data-ttu-id="21cb7-150">Next steps</span><span class="sxs-lookup"><span data-stu-id="21cb7-150">Next steps</span></span>

<span data-ttu-id="21cb7-151">Now [you can connect to the AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="21cb7-151">Now [you can connect to the AMS API](media-services-use-aad-auth-to-access-ams-api.md) and start [developing](media-services-dotnet-get-started.md).</span></span>


## <a name="media-services-learning-paths"></a><span data-ttu-id="21cb7-152">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="21cb7-152">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="21cb7-153">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="21cb7-153">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

