---
title: How to Set Up Computer for Media Services Development with .NET
description: Learn about the prerequisites for Media Services using the Media Services SDK for .NET. Also learn how to create a Visual Studio app.
services: media-services
documentationcenter: ''
author: juliako
manager: erikre
editor: ''
ms.assetid: ec2804c7-c656-4fbf-b3e4-3f0f78599a7f
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/07/2017
ms.author: juliako
ms.openlocfilehash: 612b58db48e160cb1b4cfef1f8f4c2b203061064
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552222"
---
# <a name="media-services-development-with-net"></a><span data-ttu-id="d503b-104">Media Services development with .NET</span><span class="sxs-lookup"><span data-stu-id="d503b-104">Media Services development with .NET</span></span>
[!INCLUDE [media-services-selector-setup](../../includes/media-services-selector-setup.md)]

<span data-ttu-id="d503b-105">This topic discusses how to start developing Media Services applications using .NET.</span><span class="sxs-lookup"><span data-stu-id="d503b-105">This topic discusses how to start developing Media Services applications using .NET.</span></span>

<span data-ttu-id="d503b-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span><span class="sxs-lookup"><span data-stu-id="d503b-106">The **Azure Media Services .NET SDK** library enables you to program against Media Services using .NET.</span></span> <span data-ttu-id="d503b-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span><span class="sxs-lookup"><span data-stu-id="d503b-107">To make it even easier to develop with .NET, the **Azure Media Services .NET SDK Extensions** library is provided.</span></span> <span data-ttu-id="d503b-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span><span class="sxs-lookup"><span data-stu-id="d503b-108">This library contains a set of extension methods and helper functions that simplify your .NET code.</span></span> <span data-ttu-id="d503b-109">Both libraries are available through **NuGet** and **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="d503b-109">Both libraries are available through **NuGet** and **GitHub**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d503b-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d503b-110">Prerequisites</span></span>
* <span data-ttu-id="d503b-111">A Media Services account in a new or existing Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="d503b-111">A Media Services account in a new or existing Azure subscription.</span></span> <span data-ttu-id="d503b-112">See the topic [How to Create a Media Services Account](media-services-portal-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="d503b-112">See the topic [How to Create a Media Services Account](media-services-portal-create-account.md).</span></span>
* <span data-ttu-id="d503b-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span><span class="sxs-lookup"><span data-stu-id="d503b-113">Operating Systems: Windows 10, Windows 7, Windows 2008 R2, or Windows 8.</span></span>
* <span data-ttu-id="d503b-114">.NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="d503b-114">.NET Framework 4.5.</span></span>
* <span data-ttu-id="d503b-115">Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d503b-115">Visual Studio.</span></span>

## <a name="create-and-configure-a-visual-studio-project"></a><span data-ttu-id="d503b-116">Create and configure a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="d503b-116">Create and configure a Visual Studio project</span></span>
<span data-ttu-id="d503b-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span><span class="sxs-lookup"><span data-stu-id="d503b-117">This section shows you how to create a project in Visual Studio and set it up for Media Services development.</span></span>  <span data-ttu-id="d503b-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span><span class="sxs-lookup"><span data-stu-id="d503b-118">In this case, the project is a C# Windows console application, but the same setup steps shown here apply to other types of projects you can create for Media Services applications (for example, a Windows Forms application or an ASP.NET Web application).</span></span>

<span data-ttu-id="d503b-119">This section shows how to use **NuGet** to add Media Services .NET SDK and other dependent libraries.</span><span class="sxs-lookup"><span data-stu-id="d503b-119">This section shows how to use **NuGet** to add Media Services .NET SDK and other dependent libraries.</span></span>

<span data-ttu-id="d503b-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span><span class="sxs-lookup"><span data-stu-id="d503b-120">Alternatively, you can get the latest Media Services .NET SDK bits from GitHub ([github.com/Azure/azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services) or [github.com/Azure/azure-sdk-for-media-services-extensions](https://github.com/Azure/azure-sdk-for-media-services-extensions)), build the solution, and add the references to the client project.</span></span> <span data-ttu-id="d503b-121">All the necessary dependencies get downloaded and extracted automatically.</span><span class="sxs-lookup"><span data-stu-id="d503b-121">All the necessary dependencies get downloaded and extracted automatically.</span></span>

1. <span data-ttu-id="d503b-122">Create a new C# Console Application in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="d503b-122">Create a new C# Console Application in Visual Studio.</span></span> <span data-ttu-id="d503b-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span><span class="sxs-lookup"><span data-stu-id="d503b-123">Enter the **Name**, **Location**, and **Solution name**, and then click OK.</span></span>
2. <span data-ttu-id="d503b-124">Build the solution.</span><span class="sxs-lookup"><span data-stu-id="d503b-124">Build the solution.</span></span>
3. <span data-ttu-id="d503b-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions**.</span><span class="sxs-lookup"><span data-stu-id="d503b-125">Use **NuGet** to install and add **Azure Media Services .NET SDK Extensions**.</span></span> <span data-ttu-id="d503b-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span><span class="sxs-lookup"><span data-stu-id="d503b-126">Installing this package, also installs **Media Services .NET SDK** and adds all other required dependencies.</span></span>
   
    <span data-ttu-id="d503b-127">Ensure that you have the newest version of NuGet installed.</span><span class="sxs-lookup"><span data-stu-id="d503b-127">Ensure that you have the newest version of NuGet installed.</span></span> <span data-ttu-id="d503b-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="d503b-128">For more information and installation instructions, see [NuGet](http://nuget.codeplex.com/).</span></span>
4. <span data-ttu-id="d503b-129">In Solution Explorer, right-click the name of the project and choose Manage NuGet packages.</span><span class="sxs-lookup"><span data-stu-id="d503b-129">In Solution Explorer, right-click the name of the project and choose Manage NuGet packages.</span></span>
   
    <span data-ttu-id="d503b-130">The Manage NuGet Packages dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="d503b-130">The Manage NuGet Packages dialog box appears.</span></span>
5. <span data-ttu-id="d503b-131">In the Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click the Install button.</span><span class="sxs-lookup"><span data-stu-id="d503b-131">In the Online gallery, search for Azure MediaServices Extensions, choose Azure Media Services .NET SDK Extensions, and then click the Install button.</span></span>
   
    <span data-ttu-id="d503b-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span><span class="sxs-lookup"><span data-stu-id="d503b-132">The project is modified and references to the Media Services .NET SDK Extensions,  Media Services .NET SDK, and other dependent assemblies are added.</span></span>
6. <span data-ttu-id="d503b-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span><span class="sxs-lookup"><span data-stu-id="d503b-133">To promote a cleaner development environment, consider enabling NuGet Package Restore.</span></span> <span data-ttu-id="d503b-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span><span class="sxs-lookup"><span data-stu-id="d503b-134">For more information, see [NuGet Package Restore"](http://docs.nuget.org/consume/package-restore).</span></span>
7. <span data-ttu-id="d503b-135">Add a reference to **System.Configuration** assembly.</span><span class="sxs-lookup"><span data-stu-id="d503b-135">Add a reference to **System.Configuration** assembly.</span></span> <span data-ttu-id="d503b-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span><span class="sxs-lookup"><span data-stu-id="d503b-136">This assembly contains the System.Configuration.**ConfigurationManager** class that is used to access configuration files (for example, App.config).</span></span>
   
    <span data-ttu-id="d503b-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="d503b-137">To add references using the Manage References dialog, right-click the project name in the Solution Explorer.</span></span> <span data-ttu-id="d503b-138">Then, select Add and References.</span><span class="sxs-lookup"><span data-stu-id="d503b-138">Then, select Add and References.</span></span>
   
    <span data-ttu-id="d503b-139">The Manage References dialog appears.</span><span class="sxs-lookup"><span data-stu-id="d503b-139">The Manage References dialog appears.</span></span>
8. <span data-ttu-id="d503b-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press OK.</span><span class="sxs-lookup"><span data-stu-id="d503b-140">Under .NET framework assemblies, find and select the System.Configuration assembly and press OK.</span></span>
9. <span data-ttu-id="d503b-141">Open the App.config file (add the file to your project if it was not added by default) and add an *appSettings* section to the file.</span><span class="sxs-lookup"><span data-stu-id="d503b-141">Open the App.config file (add the file to your project if it was not added by default) and add an *appSettings* section to the file.</span></span>     
   <span data-ttu-id="d503b-142">Set the values for your Azure Media Services account name and account key, as shown in the following example.</span><span class="sxs-lookup"><span data-stu-id="d503b-142">Set the values for your Azure Media Services account name and account key, as shown in the following example.</span></span>
   
    <span data-ttu-id="d503b-143">To find the Name and Key values, go to the Azure portal and select your account.</span><span class="sxs-lookup"><span data-stu-id="d503b-143">To find the Name and Key values, go to the Azure portal and select your account.</span></span> <span data-ttu-id="d503b-144">The Settings window appears on the right.</span><span class="sxs-lookup"><span data-stu-id="d503b-144">The Settings window appears on the right.</span></span> <span data-ttu-id="d503b-145">In the Settings window, select Keys.</span><span class="sxs-lookup"><span data-stu-id="d503b-145">In the Settings window, select Keys.</span></span> <span data-ttu-id="d503b-146">Clicking the icon next to each text box copies the value to the system clipboard.</span><span class="sxs-lookup"><span data-stu-id="d503b-146">Clicking the icon next to each text box copies the value to the system clipboard.</span></span>

        <configuration>
        ...
            <appSettings>
              <add key="MediaServicesAccountName" value="Media-Services-Account-Name" />
              <add key="MediaServicesAccountKey" value="Media-Services-Account-Key" />
            </appSettings>

        </configuration>

1. <span data-ttu-id="d503b-147">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span><span class="sxs-lookup"><span data-stu-id="d503b-147">Overwrite the existing **using** statements at the beginning of the Program.cs file with the following code.</span></span>
   
        using System;
        using System.Collections.Generic;
        using System.Linq;
        using System.Text;
        using System.Threading.Tasks;
        using System.Configuration;
        using System.Threading;
        using System.IO;
        using Microsoft.WindowsAzure.MediaServices.Client;

<span data-ttu-id="d503b-148">At this point, you are ready to start developing a Media Services application.</span><span class="sxs-lookup"><span data-stu-id="d503b-148">At this point, you are ready to start developing a Media Services application.</span></span>    

## <a name="media-services-learning-paths"></a><span data-ttu-id="d503b-149">Media Services learning paths</span><span class="sxs-lookup"><span data-stu-id="d503b-149">Media Services learning paths</span></span>
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a><span data-ttu-id="d503b-150">Provide feedback</span><span class="sxs-lookup"><span data-stu-id="d503b-150">Provide feedback</span></span>
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

