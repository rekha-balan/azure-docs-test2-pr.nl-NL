---
title: 'ASP.NET MVC tutorial for DocumentDB: Web Application Development | Microsoft Docs'
description: ASP.NET MVC tutorial to create an MVC web application using DocumentDB. You'll store JSON and access data from a todo app hosted on Azure Websites - ASP NET MVC tutorial step by step.
keywords: asp.net mvc tutorial, web application development, mvc web application, asp net mvc tutorial step by step
services: documentdb
documentationcenter: .net
author: syamkmsft
manager: jhubbard
editor: cgronlun
ms.assetid: 52532d89-a40e-4fdf-9b38-aadb3a4cccbc
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 12/25/2016
ms.author: syamk
ms.openlocfilehash: 3cf2d1d66f5b747858e771a03f7c32d4d43c0489
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563215"
---
# <a name="_Toc395809351"></a><span data-ttu-id="a1b82-105">ASP.NET MVC Tutorial: Web application development with DocumentDB</span><span class="sxs-lookup"><span data-stu-id="a1b82-105">ASP.NET MVC Tutorial: Web application development with DocumentDB</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-dotnet-application.md)
> * [.NET for MongoDB](documentdb-mongodb-application.md)
> * [Node.js](documentdb-nodejs-application.md)
> * [Java](documentdb-java-application.md)
> * [Python](documentdb-python-application.md)
> 
> 

<span data-ttu-id="a1b82-111">To highlight how you can efficiently leverage Azure DocumentDB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="a1b82-111">To highlight how you can efficiently leverage Azure DocumentDB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure DocumentDB.</span></span> <span data-ttu-id="a1b82-112">The tasks will be stored as JSON documents in Azure DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="a1b82-112">The tasks will be stored as JSON documents in Azure DocumentDB.</span></span>

![Screen shot of the todo list MVC web application created by this tutorial - ASP NET MVC tutorial step by step](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/asp-net-mvc-tutorial-image1.png)

<span data-ttu-id="a1b82-114">This walk-through shows you how to use the DocumentDB service provided by Azure to store and access data from an ASP.NET MVC web application hosted on Azure.</span><span class="sxs-lookup"><span data-stu-id="a1b82-114">This walk-through shows you how to use the DocumentDB service provided by Azure to store and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="a1b82-115">If you're looking for a tutorial that focuses only on DocumentDB, and not the ASP.NET MVC components, see [Build a DocumentDB C# console application](documentdb-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="a1b82-115">If you're looking for a tutorial that focuses only on DocumentDB, and not the ASP.NET MVC components, see [Build a DocumentDB C# console application](documentdb-get-started.md).</span></span>

> [!TIP]
> This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites. If you are new to ASP.NET or the [prerequisite tools](#_Toc395637760), we recommend downloading the complete sample project from [GitHub][GitHub] and following the instructions in this sample. Once you have it built, you can review this article to gain insight on the code in the context of the project.
> 
> 

## <a name="_Toc395637760"></a><span data-ttu-id="a1b82-119">Prerequisites for this database tutorial</span><span class="sxs-lookup"><span data-stu-id="a1b82-119">Prerequisites for this database tutorial</span></span>
<span data-ttu-id="a1b82-120">Before following the instructions in this article, you should ensure that you have the following:</span><span class="sxs-lookup"><span data-stu-id="a1b82-120">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="a1b82-121">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="a1b82-121">An active Azure account.</span></span> <span data-ttu-id="a1b82-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span><span class="sxs-lookup"><span data-stu-id="a1b82-122">If you don't have an account, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="a1b82-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span><span class="sxs-lookup"><span data-stu-id="a1b82-123">For details, see [Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/)</span></span> 

    <span data-ttu-id="a1b82-124">OR</span><span class="sxs-lookup"><span data-stu-id="a1b82-124">OR</span></span>

    <span data-ttu-id="a1b82-125">A local installation of the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="a1b82-125">A local installation of the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md).</span></span>
* <span data-ttu-id="a1b82-126">[Visual Studio 2015](http://www.visualstudio.com/) or Visual Studio 2013 Update 4 or higher.</span><span class="sxs-lookup"><span data-stu-id="a1b82-126">[Visual Studio 2015](http://www.visualstudio.com/) or Visual Studio 2013 Update 4 or higher.</span></span> <span data-ttu-id="a1b82-127">If using Visual Studio 2013, you will need to install the [Microsoft.Net.Compilers nuget package](https://www.nuget.org/packages/Microsoft.Net.Compilers/) to add support for C# 6.0.</span><span class="sxs-lookup"><span data-stu-id="a1b82-127">If using Visual Studio 2013, you will need to install the [Microsoft.Net.Compilers nuget package](https://www.nuget.org/packages/Microsoft.Net.Compilers/) to add support for C# 6.0.</span></span> 
* <span data-ttu-id="a1b82-128">Azure SDK for .NET version 2.5.1 or higher, available through the [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span><span class="sxs-lookup"><span data-stu-id="a1b82-128">Azure SDK for .NET version 2.5.1 or higher, available through the [Microsoft Web Platform Installer][Microsoft Web Platform Installer].</span></span>

<span data-ttu-id="a1b82-129">All the screen shots in this article have been taken using Visual Studio 2013 with Update 4 applied and the Azure SDK for .NET version 2.5.1.</span><span class="sxs-lookup"><span data-stu-id="a1b82-129">All the screen shots in this article have been taken using Visual Studio 2013 with Update 4 applied and the Azure SDK for .NET version 2.5.1.</span></span> <span data-ttu-id="a1b82-130">If your system is configured with different versions it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span><span class="sxs-lookup"><span data-stu-id="a1b82-130">If your system is configured with different versions it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span></span>

## <a name="_Toc395637761"></a><span data-ttu-id="a1b82-131">Step 1: Create a DocumentDB database account</span><span class="sxs-lookup"><span data-stu-id="a1b82-131">Step 1: Create a DocumentDB database account</span></span>
<span data-ttu-id="a1b82-132">Let's start by creating a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="a1b82-132">Let's start by creating a DocumentDB account.</span></span> <span data-ttu-id="a1b82-133">If you already have an account or if you are using the DocumentDB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="a1b82-133">If you already have an account or if you are using the DocumentDB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [documentdb-create-dbaccount](../../includes/documentdb-create-dbaccount.md)]

[!INCLUDE [documentdb-keys](../../includes/documentdb-keys.md)]

<br/>
<span data-ttu-id="a1b82-134">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span><span class="sxs-lookup"><span data-stu-id="a1b82-134">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span></span> 

## <a name="_Toc395637762"></a><span data-ttu-id="a1b82-135">Step 2: Create a new ASP.NET MVC application</span><span class="sxs-lookup"><span data-stu-id="a1b82-135">Step 2: Create a new ASP.NET MVC application</span></span>
<span data-ttu-id="a1b82-136">Now that you have an account, let's create our new ASP.NET project.</span><span class="sxs-lookup"><span data-stu-id="a1b82-136">Now that you have an account, let's create our new ASP.NET project.</span></span>

1. <span data-ttu-id="a1b82-137">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-137">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span>
   
       The **New Project** dialog box appears.
2. <span data-ttu-id="a1b82-138">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-138">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>
   
      ![Screen shot of the New Project dialog box with the ASP.NET Web Application project type highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/asp-net-mvc-tutorial-image10.png)
3. <span data-ttu-id="a1b82-140">In the **Name** box, type the name of the project.</span><span class="sxs-lookup"><span data-stu-id="a1b82-140">In the **Name** box, type the name of the project.</span></span> <span data-ttu-id="a1b82-141">This tutorial uses the name "todo".</span><span class="sxs-lookup"><span data-stu-id="a1b82-141">This tutorial uses the name "todo".</span></span> <span data-ttu-id="a1b82-142">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span><span class="sxs-lookup"><span data-stu-id="a1b82-142">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span></span> 
4. <span data-ttu-id="a1b82-143">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-143">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span></span>
   
      <span data-ttu-id="a1b82-144">The **New ASP.NET Project** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="a1b82-144">The **New ASP.NET Project** dialog box appears.</span></span>
   
      ![Screen shot of the New ASP.NET Project dialog box with the MVC application template highlighted and the Host in the cloud box checked](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/asp-net-mvc-tutorial-image11.png)
5. <span data-ttu-id="a1b82-146">In the templates pane, select **MVC**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-146">In the templates pane, select **MVC**.</span></span>
6. <span data-ttu-id="a1b82-147">If you plan on hosting your application in Azure then select **Host in the cloud** on the lower right to have Azure host the application.</span><span class="sxs-lookup"><span data-stu-id="a1b82-147">If you plan on hosting your application in Azure then select **Host in the cloud** on the lower right to have Azure host the application.</span></span> <span data-ttu-id="a1b82-148">We've selected to host in the cloud, and to run the application hosted in an Azure Website.</span><span class="sxs-lookup"><span data-stu-id="a1b82-148">We've selected to host in the cloud, and to run the application hosted in an Azure Website.</span></span> <span data-ttu-id="a1b82-149">Selecting this option will preprovision an Azure Website for you and make life a lot easier when it comes time to deploy the final working application.</span><span class="sxs-lookup"><span data-stu-id="a1b82-149">Selecting this option will preprovision an Azure Website for you and make life a lot easier when it comes time to deploy the final working application.</span></span> <span data-ttu-id="a1b82-150">If you want to host this elsewhere or don't want to configure Azure upfront, then just clear **Host in the Cloud**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-150">If you want to host this elsewhere or don't want to configure Azure upfront, then just clear **Host in the Cloud**.</span></span>
7. <span data-ttu-id="a1b82-151">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span><span class="sxs-lookup"><span data-stu-id="a1b82-151">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span></span> 

    <span data-ttu-id="a1b82-152">If you receive the error "An error occurred while processing your request" see the [Troubleshooting](#troubleshooting) section.</span><span class="sxs-lookup"><span data-stu-id="a1b82-152">If you receive the error "An error occurred while processing your request" see the [Troubleshooting](#troubleshooting) section.</span></span>

8. <span data-ttu-id="a1b82-153">If you chose to host this in the cloud you will see at least one additional screen asking you to login to your Azure account and provide some values for your new website.</span><span class="sxs-lookup"><span data-stu-id="a1b82-153">If you chose to host this in the cloud you will see at least one additional screen asking you to login to your Azure account and provide some values for your new website.</span></span> <span data-ttu-id="a1b82-154">Supply all the additional values and continue.</span><span class="sxs-lookup"><span data-stu-id="a1b82-154">Supply all the additional values and continue.</span></span> 
   
      <span data-ttu-id="a1b82-155">I haven't chosen a "Database server" here because we're not using an Azure SQL Database Server here, we're going to be creating a new Azure DocumentDB account later on in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a1b82-155">I haven't chosen a "Database server" here because we're not using an Azure SQL Database Server here, we're going to be creating a new Azure DocumentDB account later on in the Azure Portal.</span></span>
   
    <span data-ttu-id="a1b82-156">For more information about choosing an **App Service plan** and **Resource group**, see [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1b82-156">For more information about choosing an **App Service plan** and **Resource group**, see [Azure App Service plans in-depth overview](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md).</span></span>
   
      ![Screen shot of the Configure Microsoft Azure Website dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image11_1.png)
9. <span data-ttu-id="a1b82-158">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span><span class="sxs-lookup"><span data-stu-id="a1b82-158">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="a1b82-159">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span><span class="sxs-lookup"><span data-stu-id="a1b82-159">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span></span> <span data-ttu-id="a1b82-160">Let's go straight to adding DocumentDB to this project and building our application.</span><span class="sxs-lookup"><span data-stu-id="a1b82-160">Let's go straight to adding DocumentDB to this project and building our application.</span></span>

## <a name="_Toc395637767"></a><span data-ttu-id="a1b82-161">Step 3: Add DocumentDB to your MVC web application project</span><span class="sxs-lookup"><span data-stu-id="a1b82-161">Step 3: Add DocumentDB to your MVC web application project</span></span>
<span data-ttu-id="a1b82-162">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure DocumentDB to our MVC web application.</span><span class="sxs-lookup"><span data-stu-id="a1b82-162">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure DocumentDB to our MVC web application.</span></span>

1. <span data-ttu-id="a1b82-163">The DocumentDB .NET SDK is packaged and distributed as a NuGet package.</span><span class="sxs-lookup"><span data-stu-id="a1b82-163">The DocumentDB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="a1b82-164">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-164">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
      ![Sreen shot of the right-click options for the web application project in Solution Explorer, with Manage NuGet Packages highlighted.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image21.png)
   
    <span data-ttu-id="a1b82-166">The **Manage NuGet Packages** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="a1b82-166">The **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="a1b82-167">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-167">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span></span>
   
    <span data-ttu-id="a1b82-168">From the results, install the **Microsoft Azure DocumentDB Client Library** package.</span><span class="sxs-lookup"><span data-stu-id="a1b82-168">From the results, install the **Microsoft Azure DocumentDB Client Library** package.</span></span> <span data-ttu-id="a1b82-169">This will download and install the DocumentDB package as well as all dependencies, like Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="a1b82-169">This will download and install the DocumentDB package as well as all dependencies, like Newtonsoft.Json.</span></span> <span data-ttu-id="a1b82-170">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span><span class="sxs-lookup"><span data-stu-id="a1b82-170">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span></span>
   
      ![Sreen shot of the Manage NuGet Packages window, with the Microsoft Azure DocumentDB Client Library highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/nuget.png)
   
      <span data-ttu-id="a1b82-172">Alternatively you can use the Package Manager Console to install the package.</span><span class="sxs-lookup"><span data-stu-id="a1b82-172">Alternatively you can use the Package Manager Console to install the package.</span></span> <span data-ttu-id="a1b82-173">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-173">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="a1b82-174">At the prompt, type the following.</span><span class="sxs-lookup"><span data-stu-id="a1b82-174">At the prompt, type the following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
3. <span data-ttu-id="a1b82-175">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="a1b82-175">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
      ![Sreen shot of the two references added to the JSON data project in Solution Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image22.png)

## <a name="_Toc395637763"></a><span data-ttu-id="a1b82-177">Step 4: Set up the ASP.NET MVC application</span><span class="sxs-lookup"><span data-stu-id="a1b82-177">Step 4: Set up the ASP.NET MVC application</span></span>
<span data-ttu-id="a1b82-178">Now let's add the models, views, and controllers to this MVC application:</span><span class="sxs-lookup"><span data-stu-id="a1b82-178">Now let's add the models, views, and controllers to this MVC application:</span></span>

* <span data-ttu-id="a1b82-179">[Add a model](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="a1b82-179">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="a1b82-180">[Add a controller](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="a1b82-180">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="a1b82-181">[Add views](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="a1b82-181">[Add views](#_Toc395637766).</span></span>

### <a name="_Toc395637764"></a><span data-ttu-id="a1b82-182">Add a JSON data model</span><span class="sxs-lookup"><span data-stu-id="a1b82-182">Add a JSON data model</span></span>
<span data-ttu-id="a1b82-183">Let's begin by creating the **M** in MVC, the model.</span><span class="sxs-lookup"><span data-stu-id="a1b82-183">Let's begin by creating the **M** in MVC, the model.</span></span> 

1. <span data-ttu-id="a1b82-184">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-184">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="a1b82-185">The **Add New Item** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="a1b82-185">The **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="a1b82-186">Name your new class **Item.cs** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-186">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="a1b82-187">In this new **Item.cs** file, add the following after the last *using statement*.</span><span class="sxs-lookup"><span data-stu-id="a1b82-187">In this new **Item.cs** file, add the following after the last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="a1b82-188">Now replace this code</span><span class="sxs-lookup"><span data-stu-id="a1b82-188">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="a1b82-189">with the following code.</span><span class="sxs-lookup"><span data-stu-id="a1b82-189">with the following code.</span></span>
   
        public class Item
        {
            [JsonProperty(PropertyName = "id")]
            public string Id { get; set; }
   
            [JsonProperty(PropertyName = "name")]
            public string Name { get; set; }
   
            [JsonProperty(PropertyName = "description")]
            public string Description { get; set; }
   
            [JsonProperty(PropertyName = "isComplete")]
            public bool Completed { get; set; }
        }
   
    <span data-ttu-id="a1b82-190">All data in DocumentDB is passed over the wire and stored as JSON.</span><span class="sxs-lookup"><span data-stu-id="a1b82-190">All data in DocumentDB is passed over the wire and stored as JSON.</span></span> <span data-ttu-id="a1b82-191">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span><span class="sxs-lookup"><span data-stu-id="a1b82-191">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span></span> <span data-ttu-id="a1b82-192">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span><span class="sxs-lookup"><span data-stu-id="a1b82-192">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="a1b82-193">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span><span class="sxs-lookup"><span data-stu-id="a1b82-193">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span></span> 

### <a name="_Toc395637765"></a><span data-ttu-id="a1b82-194">Add a controller</span><span class="sxs-lookup"><span data-stu-id="a1b82-194">Add a controller</span></span>
<span data-ttu-id="a1b82-195">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span><span class="sxs-lookup"><span data-stu-id="a1b82-195">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="a1b82-196">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-196">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="a1b82-197">The **Add Scaffold** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="a1b82-197">The **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="a1b82-198">Select **MVC 5 Controller - Empty** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-198">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Screen shot of the Add Scaffold dialog box with the MVC 5 Controller - Empty option highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image14.png)
3. <span data-ttu-id="a1b82-200">Name your new Controller, **ItemController.**</span><span class="sxs-lookup"><span data-stu-id="a1b82-200">Name your new Controller, **ItemController.**</span></span>
   
    ![Screen shot of the Add Controller dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image15.png)
   
    <span data-ttu-id="a1b82-202">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-202">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="a1b82-203">The new Item.cs file created earlier is also shown.</span><span class="sxs-lookup"><span data-stu-id="a1b82-203">The new Item.cs file created earlier is also shown.</span></span>
   
    ![Screen shot of the Visual Studio solution - Solution Explorer with the new ItemController.cs file and Item.cs file highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image16.png)
   
    <span data-ttu-id="a1b82-205">You can close ItemController.cs, we'll come back to it later.</span><span class="sxs-lookup"><span data-stu-id="a1b82-205">You can close ItemController.cs, we'll come back to it later.</span></span> 

### <a name="_Toc395637766"></a><span data-ttu-id="a1b82-206">Add views</span><span class="sxs-lookup"><span data-stu-id="a1b82-206">Add views</span></span>
<span data-ttu-id="a1b82-207">Now, let's create the **V** in MVC, the views:</span><span class="sxs-lookup"><span data-stu-id="a1b82-207">Now, let's create the **V** in MVC, the views:</span></span>

* <span data-ttu-id="a1b82-208">[Add an Item Index view](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="a1b82-208">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="a1b82-209">[Add a New Item view](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="a1b82-209">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="a1b82-210">[Add an Edit Item view](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="a1b82-210">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <a name="AddItemIndexView"></a><span data-ttu-id="a1b82-211">Add an Item Index view</span><span class="sxs-lookup"><span data-stu-id="a1b82-211">Add an Item Index view</span></span>
1. <span data-ttu-id="a1b82-212">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-212">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Screen shot of Solution Explorer showing the Item folder that Visual Studio created with the Add View commands highlighted](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image17.png)
2. <span data-ttu-id="a1b82-214">In the **Add View** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="a1b82-214">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="a1b82-215">In the **View name** box, type ***Index***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-215">In the **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="a1b82-216">In the **Template** box, select ***List***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-216">In the **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="a1b82-217">In the **Model class** box, select ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-217">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="a1b82-218">Leave the **Data context class** box empty.</span><span class="sxs-lookup"><span data-stu-id="a1b82-218">Leave the **Data context class** box empty.</span></span> 
   * <span data-ttu-id="a1b82-219">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-219">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
     ![Screen shot showing the Add View dialog box](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image18.png)
3. <span data-ttu-id="a1b82-221">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span><span class="sxs-lookup"><span data-stu-id="a1b82-221">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="a1b82-222">Once it is done, it will open the cshtml file  that was created.</span><span class="sxs-lookup"><span data-stu-id="a1b82-222">Once it is done, it will open the cshtml file  that was created.</span></span> <span data-ttu-id="a1b82-223">We can close that file in Visual Studio as we will come back to it later.</span><span class="sxs-lookup"><span data-stu-id="a1b82-223">We can close that file in Visual Studio as we will come back to it later.</span></span>

#### <a name="AddNewIndexView"></a><span data-ttu-id="a1b82-224">Add a New Item view</span><span class="sxs-lookup"><span data-stu-id="a1b82-224">Add a New Item view</span></span>
<span data-ttu-id="a1b82-225">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-225">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="a1b82-226">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-226">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="a1b82-227">In the **Add View** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="a1b82-227">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="a1b82-228">In the **View name** box, type ***Create***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-228">In the **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="a1b82-229">In the **Template** box, select ***Create***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-229">In the **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="a1b82-230">In the **Model class** box, select ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-230">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="a1b82-231">Leave the **Data context class** box empty.</span><span class="sxs-lookup"><span data-stu-id="a1b82-231">Leave the **Data context class** box empty.</span></span>
   * <span data-ttu-id="a1b82-232">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-232">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="a1b82-233">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-233">Click **Add**.</span></span>

#### <a name="_Toc395888515"></a><span data-ttu-id="a1b82-234">Add an Edit Item view</span><span class="sxs-lookup"><span data-stu-id="a1b82-234">Add an Edit Item view</span></span>
<span data-ttu-id="a1b82-235">And finally, add one last view for editing an **Item** in the same way as before.</span><span class="sxs-lookup"><span data-stu-id="a1b82-235">And finally, add one last view for editing an **Item** in the same way as before.</span></span>

1. <span data-ttu-id="a1b82-236">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-236">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="a1b82-237">In the **Add View** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="a1b82-237">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="a1b82-238">In the **View name** box, type ***Edit***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-238">In the **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="a1b82-239">In the **Template** box, select ***Edit***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-239">In the **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="a1b82-240">In the **Model class** box, select ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-240">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="a1b82-241">Leave the **Data context class** box empty.</span><span class="sxs-lookup"><span data-stu-id="a1b82-241">Leave the **Data context class** box empty.</span></span> 
   * <span data-ttu-id="a1b82-242">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="a1b82-242">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="a1b82-243">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-243">Click **Add**.</span></span>

<span data-ttu-id="a1b82-244">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span><span class="sxs-lookup"><span data-stu-id="a1b82-244">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span></span>

## <a name="_Toc395637769"></a><span data-ttu-id="a1b82-245">Step 5: Wiring up DocumentDB</span><span class="sxs-lookup"><span data-stu-id="a1b82-245">Step 5: Wiring up DocumentDB</span></span>
<span data-ttu-id="a1b82-246">Now that the standard MVC stuff is taken care of, let's turn to adding the code for DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="a1b82-246">Now that the standard MVC stuff is taken care of, let's turn to adding the code for DocumentDB.</span></span> 

<span data-ttu-id="a1b82-247">In this section, we'll add code to handle the following:</span><span class="sxs-lookup"><span data-stu-id="a1b82-247">In this section, we'll add code to handle the following:</span></span>

* <span data-ttu-id="a1b82-248">[Listing incomplete Items](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="a1b82-248">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="a1b82-249">[Adding Items](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="a1b82-249">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="a1b82-250">[Editing Items](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="a1b82-250">[Editing Items](#_Toc395637772).</span></span>

### <a name="_Toc395637770"></a><span data-ttu-id="a1b82-251">Listing incomplete Items in your MVC web application</span><span class="sxs-lookup"><span data-stu-id="a1b82-251">Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="a1b82-252">The first thing to do here is add a class that contains all the logic to connect to and use DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="a1b82-252">The first thing to do here is add a class that contains all the logic to connect to and use DocumentDB.</span></span> <span data-ttu-id="a1b82-253">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="a1b82-253">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="a1b82-254">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-254">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="a1b82-255">Name the new class **DocumentDBRepository** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-255">Name the new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="a1b82-256">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span><span class="sxs-lookup"><span data-stu-id="a1b82-256">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
   
    <span data-ttu-id="a1b82-257">Now replace this code</span><span class="sxs-lookup"><span data-stu-id="a1b82-257">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="a1b82-258">with the following code.</span><span class="sxs-lookup"><span data-stu-id="a1b82-258">with the following code.</span></span>
   
        public static class DocumentDBRepository<T> where T : class
        {
            private static readonly string DatabaseId = ConfigurationManager.AppSettings["database"];
            private static readonly string CollectionId = ConfigurationManager.AppSettings["collection"];
            private static DocumentClient client;
   
            public static void Initialize()
            {
                client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpoint"]), ConfigurationManager.AppSettings["authKey"]);
                CreateDatabaseIfNotExistsAsync().Wait();
                CreateCollectionIfNotExistsAsync().Wait();
            }
   
            private static async Task CreateDatabaseIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(DatabaseId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDatabaseAsync(new Database { Id = DatabaseId });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
   
            private static async Task CreateCollectionIfNotExistsAsync()
            {
                try
                {
                    await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId));
                }
                catch (DocumentClientException e)
                {
                    if (e.StatusCode == System.Net.HttpStatusCode.NotFound)
                    {
                        await client.CreateDocumentCollectionAsync(
                            UriFactory.CreateDatabaseUri(DatabaseId),
                            new DocumentCollection { Id = CollectionId },
                            new RequestOptions { OfferThroughput = 1000 });
                    }
                    else
                    {
                        throw;
                    }
                }
            }
        }
   
   > [!TIP]
   > When creating a new DocumentCollection you can supply an optional RequestOptions parameter of OfferType, which allows you to specify the performance level of the new collection. If this parameter is not passed the default offer type will be used. For more on DocumentDB offer types please refer to [DocumentDB Performance Levels](documentdb-performance-levels.md)
   > 
   > 
3. <span data-ttu-id="a1b82-262">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="a1b82-262">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="a1b82-263">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a1b82-263">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span></span> <span data-ttu-id="a1b82-264">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span><span class="sxs-lookup"><span data-stu-id="a1b82-264">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span></span>

    <span data-ttu-id="a1b82-265">That takes care of wiring up the DocumentDB repository, now let's add our application logic.</span><span class="sxs-lookup"><span data-stu-id="a1b82-265">That takes care of wiring up the DocumentDB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="a1b82-266">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span><span class="sxs-lookup"><span data-stu-id="a1b82-266">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span></span>  <span data-ttu-id="a1b82-267">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span><span class="sxs-lookup"><span data-stu-id="a1b82-267">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span></span>
   
        public static async Task<IEnumerable<T>> GetItemsAsync(Expression<Func<T, bool>> predicate)
        {
            IDocumentQuery<T> query = client.CreateDocumentQuery<T>(
                UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId))
                .Where(predicate)
                .AsDocumentQuery();
   
            List<T> results = new List<T>();
            while (query.HasMoreResults)
            {
                results.AddRange(await query.ExecuteNextAsync<T>());
            }
   
            return results;
        }
2. <span data-ttu-id="a1b82-268">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span><span class="sxs-lookup"><span data-stu-id="a1b82-268">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="a1b82-269">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span><span class="sxs-lookup"><span data-stu-id="a1b82-269">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span></span>
   
    <span data-ttu-id="a1b82-270">Now replace this code</span><span class="sxs-lookup"><span data-stu-id="a1b82-270">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="a1b82-271">with the following code.</span><span class="sxs-lookup"><span data-stu-id="a1b82-271">with the following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="a1b82-272">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span><span class="sxs-lookup"><span data-stu-id="a1b82-272">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="a1b82-273">At this point your solution should be able to build without any errors.</span><span class="sxs-lookup"><span data-stu-id="a1b82-273">At this point your solution should be able to build without any errors.</span></span>

<span data-ttu-id="a1b82-274">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span><span class="sxs-lookup"><span data-stu-id="a1b82-274">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span></span> <span data-ttu-id="a1b82-275">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span><span class="sxs-lookup"><span data-stu-id="a1b82-275">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span></span> <span data-ttu-id="a1b82-276">Let's change the routing on this MVC application to alter this behavior.</span><span class="sxs-lookup"><span data-stu-id="a1b82-276">Let's change the routing on this MVC application to alter this behavior.</span></span>

<span data-ttu-id="a1b82-277">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span><span class="sxs-lookup"><span data-stu-id="a1b82-277">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="a1b82-278">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span><span class="sxs-lookup"><span data-stu-id="a1b82-278">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span></span>

<span data-ttu-id="a1b82-279">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span><span class="sxs-lookup"><span data-stu-id="a1b82-279">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="a1b82-280">If you build and run this project now, you should now see something that looks this.</span><span class="sxs-lookup"><span data-stu-id="a1b82-280">If you build and run this project now, you should now see something that looks this.</span></span>    

![Screen shot of the todo list web application created by this database tutorial](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image23.png)

### <a name="_Toc395637771"></a><span data-ttu-id="a1b82-282">Adding Items</span><span class="sxs-lookup"><span data-stu-id="a1b82-282">Adding Items</span></span>
<span data-ttu-id="a1b82-283">Let's put some items into our database so we have something more than an empty grid to look at.</span><span class="sxs-lookup"><span data-stu-id="a1b82-283">Let's put some items into our database so we have something more than an empty grid to look at.</span></span>

<span data-ttu-id="a1b82-284">Let's add some code to  DocumentDBRepository and ItemController to persist the record in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="a1b82-284">Let's add some code to  DocumentDBRepository and ItemController to persist the record in DocumentDB.</span></span>

1. <span data-ttu-id="a1b82-285">Add the following method to your **DocumentDBRepository** class.</span><span class="sxs-lookup"><span data-stu-id="a1b82-285">Add the following method to your **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="a1b82-286">This method simply takes an object passed to it and persists it in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="a1b82-286">This method simply takes an object passed to it and persists it in DocumentDB.</span></span>
2. <span data-ttu-id="a1b82-287">Open the ItemController.cs file and add the following code snippet within the class.</span><span class="sxs-lookup"><span data-stu-id="a1b82-287">Open the ItemController.cs file and add the following code snippet within the class.</span></span> <span data-ttu-id="a1b82-288">This is how ASP.NET MVC knows what to do for the **Create** action.</span><span class="sxs-lookup"><span data-stu-id="a1b82-288">This is how ASP.NET MVC knows what to do for the **Create** action.</span></span> <span data-ttu-id="a1b82-289">In this case just render the associated Create.cshtml view created earlier.</span><span class="sxs-lookup"><span data-stu-id="a1b82-289">In this case just render the associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="a1b82-290">We now need some more code in this controller that will accept the submission from the **Create** view.</span><span class="sxs-lookup"><span data-stu-id="a1b82-290">We now need some more code in this controller that will accept the submission from the **Create** view.</span></span>
3. <span data-ttu-id="a1b82-291">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span><span class="sxs-lookup"><span data-stu-id="a1b82-291">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span></span>
   
        [HttpPost]
        [ActionName("Create")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> CreateAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.CreateItemAsync(item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
    <span data-ttu-id="a1b82-292">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span><span class="sxs-lookup"><span data-stu-id="a1b82-292">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span></span> 
   
    <span data-ttu-id="a1b82-293">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span><span class="sxs-lookup"><span data-stu-id="a1b82-293">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="a1b82-294">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span><span class="sxs-lookup"><span data-stu-id="a1b82-294">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span></span> <span data-ttu-id="a1b82-295">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="a1b82-295">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="a1b82-296">The source code provided on [GitHub][GitHub] has the full implementation in place.</span><span class="sxs-lookup"><span data-stu-id="a1b82-296">The source code provided on [GitHub][GitHub] has the full implementation in place.</span></span>
   
    <span data-ttu-id="a1b82-297">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span><span class="sxs-lookup"><span data-stu-id="a1b82-297">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span></span> <span data-ttu-id="a1b82-298">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="a1b82-298">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="a1b82-299">This concludes the code required to add new Items to our database.</span><span class="sxs-lookup"><span data-stu-id="a1b82-299">This concludes the code required to add new Items to our database.</span></span>

### <a name="_Toc395637772"></a><span data-ttu-id="a1b82-300">Editing Items</span><span class="sxs-lookup"><span data-stu-id="a1b82-300">Editing Items</span></span>
<span data-ttu-id="a1b82-301">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span><span class="sxs-lookup"><span data-stu-id="a1b82-301">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span></span> <span data-ttu-id="a1b82-302">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span><span class="sxs-lookup"><span data-stu-id="a1b82-302">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="a1b82-303">Add the following to the **DocumentDBRepository** class.</span><span class="sxs-lookup"><span data-stu-id="a1b82-303">Add the following to the **DocumentDBRepository** class.</span></span>
   
        public static async Task<Document> UpdateItemAsync(string id, T item)
        {
            return await client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id), item);
        }
   
        public static async Task<T> GetItemAsync(string id)
        {
            try
            {
                Document document = await client.ReadDocumentAsync(UriFactory.CreateDocumentUri(DatabaseId, CollectionId, id));
                return (T)(dynamic)document;
            }
            catch (DocumentClientException e)
            {
                if (e.StatusCode == HttpStatusCode.NotFound)
                {
                    return null;
                }
                else
                {
                    throw;
                }
            }
        }
   
    <span data-ttu-id="a1b82-304">The first of these methods, **GetItem** fetches an Item from DocumentDB which is passed back to the **ItemController** and then on to the **Edit** view.</span><span class="sxs-lookup"><span data-stu-id="a1b82-304">The first of these methods, **GetItem** fetches an Item from DocumentDB which is passed back to the **ItemController** and then on to the **Edit** view.</span></span>
   
    <span data-ttu-id="a1b82-305">The second of the methods we just added replaces the **Document** in DocumentDB with the version of the **Document** passed in from the **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-305">The second of the methods we just added replaces the **Document** in DocumentDB with the version of the **Document** passed in from the **ItemController**.</span></span>
2. <span data-ttu-id="a1b82-306">Add the following to the **ItemController** class.</span><span class="sxs-lookup"><span data-stu-id="a1b82-306">Add the following to the **ItemController** class.</span></span>
   
        [HttpPost]
        [ActionName("Edit")]
        [ValidateAntiForgeryToken]
        public async Task<ActionResult> EditAsync([Bind(Include = "Id,Name,Description,Completed")] Item item)
        {
            if (ModelState.IsValid)
            {
                await DocumentDBRepository<Item>.UpdateItemAsync(item.Id, item);
                return RedirectToAction("Index");
            }
   
            return View(item);
        }
   
        [ActionName("Edit")]
        public async Task<ActionResult> EditAsync(string id)
        {
            if (id == null)
            {
                return new HttpStatusCodeResult(HttpStatusCode.BadRequest);
            }
   
            Item item = await DocumentDBRepository<Item>.GetItemAsync(id);
            if (item == null)
            {
                return HttpNotFound();
            }
   
            return View(item);
        }
   
    <span data-ttu-id="a1b82-307">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span><span class="sxs-lookup"><span data-stu-id="a1b82-307">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span></span> <span data-ttu-id="a1b82-308">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from DocumentDB and passes it to the **Edit** view.</span><span class="sxs-lookup"><span data-stu-id="a1b82-308">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from DocumentDB and passes it to the **Edit** view.</span></span>
   
    <span data-ttu-id="a1b82-309">The **Edit** view will then do an Http POST to the **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-309">The **Edit** view will then do an Http POST to the **IndexController**.</span></span> 
   
    <span data-ttu-id="a1b82-310">The second method we added handles passing the updated object to DocumentDB to be persisted in the database.</span><span class="sxs-lookup"><span data-stu-id="a1b82-310">The second method we added handles passing the updated object to DocumentDB to be persisted in the database.</span></span>

<span data-ttu-id="a1b82-311">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-311">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <a name="_Toc395637773"></a><span data-ttu-id="a1b82-312">Step 6: Run the application locally</span><span class="sxs-lookup"><span data-stu-id="a1b82-312">Step 6: Run the application locally</span></span>
<span data-ttu-id="a1b82-313">To test the application on your local machine, do the following:</span><span class="sxs-lookup"><span data-stu-id="a1b82-313">To test the application on your local machine, do the following:</span></span>

1. <span data-ttu-id="a1b82-314">Hit F5 in Visual Studio to build the application in debug mode.</span><span class="sxs-lookup"><span data-stu-id="a1b82-314">Hit F5 in Visual Studio to build the application in debug mode.</span></span> <span data-ttu-id="a1b82-315">It should build the application and launch a browser with the empty grid page we saw before:</span><span class="sxs-lookup"><span data-stu-id="a1b82-315">It should build the application and launch a browser with the empty grid page we saw before:</span></span>
   
    ![Screen shot of the todo list web application created by this database tutorial](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image24.png)
   
    <span data-ttu-id="a1b82-317">If you are using Visual Studio 2013 and receive the error "Cannot await in the body of a catch clause."</span><span class="sxs-lookup"><span data-stu-id="a1b82-317">If you are using Visual Studio 2013 and receive the error "Cannot await in the body of a catch clause."</span></span> <span data-ttu-id="a1b82-318">you need to install the [Microsoft.Net.Compilers nuget package](https://www.nuget.org/packages/Microsoft.Net.Compilers/).</span><span class="sxs-lookup"><span data-stu-id="a1b82-318">you need to install the [Microsoft.Net.Compilers nuget package](https://www.nuget.org/packages/Microsoft.Net.Compilers/).</span></span> <span data-ttu-id="a1b82-319">You can also compare your code against the sample project on [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="a1b82-319">You can also compare your code against the sample project on [GitHub][GitHub].</span></span> 
2. <span data-ttu-id="a1b82-320">Click the **Create New** link and add values to the **Name** and **Description** fields.</span><span class="sxs-lookup"><span data-stu-id="a1b82-320">Click the **Create New** link and add values to the **Name** and **Description** fields.</span></span> <span data-ttu-id="a1b82-321">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span><span class="sxs-lookup"><span data-stu-id="a1b82-321">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span></span>
   
    ![Screen shot of the Create view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image25.png)
3. <span data-ttu-id="a1b82-323">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span><span class="sxs-lookup"><span data-stu-id="a1b82-323">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span></span>
   
    ![Screen shot of the Index view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image26.png)
   
    <span data-ttu-id="a1b82-325">Feel free to add a few more **Items** to your todo list.</span><span class="sxs-lookup"><span data-stu-id="a1b82-325">Feel free to add a few more **Items** to your todo list.</span></span>
4. <span data-ttu-id="a1b82-326">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span><span class="sxs-lookup"><span data-stu-id="a1b82-326">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span></span> <span data-ttu-id="a1b82-327">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span><span class="sxs-lookup"><span data-stu-id="a1b82-327">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span></span>
   
    ![Screen shot of the Index view with the Completed box checked](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image27.png)
5. <span data-ttu-id="a1b82-329">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span><span class="sxs-lookup"><span data-stu-id="a1b82-329">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span></span> <span data-ttu-id="a1b82-330">You're ready to deploy!</span><span class="sxs-lookup"><span data-stu-id="a1b82-330">You're ready to deploy!</span></span>

## <a name="_Toc395637774"></a><span data-ttu-id="a1b82-331">Step 7: Deploy the application to Azure Websites</span><span class="sxs-lookup"><span data-stu-id="a1b82-331">Step 7: Deploy the application to Azure Websites</span></span>
<span data-ttu-id="a1b82-332">Now that you have the complete application working correctly with DocumentDB we're going to deploy this web app to Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="a1b82-332">Now that you have the complete application working correctly with DocumentDB we're going to deploy this web app to Azure Websites.</span></span> <span data-ttu-id="a1b82-333">If you selected **Host in the cloud** when you created the empty ASP.NET MVC project then Visual Studio makes this really easy and does most of the work for you.</span><span class="sxs-lookup"><span data-stu-id="a1b82-333">If you selected **Host in the cloud** when you created the empty ASP.NET MVC project then Visual Studio makes this really easy and does most of the work for you.</span></span> 

1. <span data-ttu-id="a1b82-334">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-334">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Screen shot of the Publish option in Solution Explorer](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image28.png)
2. <span data-ttu-id="a1b82-336">Everything should already be configured according to your credentials; in fact the website has already been created in Azure for you at the **Destination URL** shown, all you need to do is click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-336">Everything should already be configured according to your credentials; in fact the website has already been created in Azure for you at the **Destination URL** shown, all you need to do is click **Publish**.</span></span>
   
    ![Screen shot of the Publish Web dialog box in Visual Studio - ASP NET MVC tutorial step by step](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnet-application/image29.png)

<span data-ttu-id="a1b82-338">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handy work running in Azure!</span><span class="sxs-lookup"><span data-stu-id="a1b82-338">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handy work running in Azure!</span></span>

## <a name="Troubleshooting"></a><span data-ttu-id="a1b82-339">Troubleshooting</span><span class="sxs-lookup"><span data-stu-id="a1b82-339">Troubleshooting</span></span>

<span data-ttu-id="a1b82-340">If you receive the "An error occurred while processing your request" while trying to deploy the web app, do the following:</span><span class="sxs-lookup"><span data-stu-id="a1b82-340">If you receive the "An error occurred while processing your request" while trying to deploy the web app, do the following:</span></span> 

1. <span data-ttu-id="a1b82-341">Cancel out of the error message and then select **Microsoft Azure Web Apps** again.</span><span class="sxs-lookup"><span data-stu-id="a1b82-341">Cancel out of the error message and then select **Microsoft Azure Web Apps** again.</span></span> 
2. <span data-ttu-id="a1b82-342">Login and then select **New** to create a new web app.</span><span class="sxs-lookup"><span data-stu-id="a1b82-342">Login and then select **New** to create a new web app.</span></span> 
3. <span data-ttu-id="a1b82-343">On the **Create a Web App on Microsoft Azure** screen, do the following:</span><span class="sxs-lookup"><span data-stu-id="a1b82-343">On the **Create a Web App on Microsoft Azure** screen, do the following:</span></span> 
    
    - <span data-ttu-id="a1b82-344">Web App name: "todo-net-app"</span><span class="sxs-lookup"><span data-stu-id="a1b82-344">Web App name: "todo-net-app"</span></span>
    - <span data-ttu-id="a1b82-345">App Service plan: Create new, named "todo-net-app"</span><span class="sxs-lookup"><span data-stu-id="a1b82-345">App Service plan: Create new, named "todo-net-app"</span></span>
    - <span data-ttu-id="a1b82-346">Resource group: Create new, named "todo-net-app"</span><span class="sxs-lookup"><span data-stu-id="a1b82-346">Resource group: Create new, named "todo-net-app"</span></span>
    - <span data-ttu-id="a1b82-347">Region: Select the region closest to your app users</span><span class="sxs-lookup"><span data-stu-id="a1b82-347">Region: Select the region closest to your app users</span></span>
    - <span data-ttu-id="a1b82-348">Database server: Click no database, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-348">Database server: Click no database, then click **Create**.</span></span> 

4. <span data-ttu-id="a1b82-349">In the "todo-net-app \* screen", click **Validate Connection**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-349">In the "todo-net-app \* screen", click **Validate Connection**.</span></span> <span data-ttu-id="a1b82-350">After the connection is verified, **Publish**.</span><span class="sxs-lookup"><span data-stu-id="a1b82-350">After the connection is verified, **Publish**.</span></span> 
    
    <span data-ttu-id="a1b82-351">The app then gets displayed on your browser.</span><span class="sxs-lookup"><span data-stu-id="a1b82-351">The app then gets displayed on your browser.</span></span>


## <a name="_Toc395637775"></a><span data-ttu-id="a1b82-352">Next steps</span><span class="sxs-lookup"><span data-stu-id="a1b82-352">Next steps</span></span>
<span data-ttu-id="a1b82-353">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="a1b82-353">Congratulations!</span></span> <span data-ttu-id="a1b82-354">You just built your first ASP.NET MVC web application using Azure DocumentDB and published it to Azure Websites.</span><span class="sxs-lookup"><span data-stu-id="a1b82-354">You just built your first ASP.NET MVC web application using Azure DocumentDB and published it to Azure Websites.</span></span> <span data-ttu-id="a1b82-355">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="a1b82-355">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="a1b82-356">So if you're interested in adding that to your app, grab the code and add it to this app.</span><span class="sxs-lookup"><span data-stu-id="a1b82-356">So if you're interested in adding that to your app, grab the code and add it to this app.</span></span>

<span data-ttu-id="a1b82-357">To add additional functionality to your application, review the APIs available in the [DocumentDB .NET Library](https://msdn.microsoft.com/library/azure/dn948556.aspx) and feel free to contribute to the DocumentDB .NET Library on [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="a1b82-357">To add additional functionality to your application, review the APIs available in the [DocumentDB .NET Library](https://msdn.microsoft.com/library/azure/dn948556.aspx) and feel free to contribute to the DocumentDB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app



















