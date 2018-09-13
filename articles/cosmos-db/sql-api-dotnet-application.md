---
title: 'ASP.NET MVC tutorial for Azure Cosmos DB: Web Application Development | Microsoft Docs'
description: ASP.NET MVC tutorial to create an MVC web application using Azure Cosmos DB. You'll store JSON and access data from a todo app hosted on Azure Websites - ASP NET MVC tutorial step by step.
keywords: asp.net mvc tutorial, web application development, mvc web application, asp net mvc tutorial step by step
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.workload: azure-vs
ms.devlang: dotnet
ms.topic: tutorial
ms.date: 08/03/2017
ms.author: sngun
ms.custom: devcenter, vs-azure
ms.openlocfilehash: 6fbe043e0232701d2aabcbc09606864b5cc27450
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864641"
---
# <a name="_Toc395809351"></a><span data-ttu-id="c75e3-105">ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c75e3-105">ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB</span></span>

> [!div class="op_single_selector"]
> * [.NET](sql-api-dotnet-application.md)
> * [Java](sql-api-java-application.md)
> * [Node.js](sql-api-nodejs-application.md)
> * [Node.js- v2](sql-api-nodejs-application-preview.md)
> * [Python](sql-api-python-application.md)
> * [Xamarin](mobile-apps-with-xamarin.md)
> 

<span data-ttu-id="c75e3-112">To highlight how you can efficiently leverage Azure Cosmos DB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c75e3-112">To highlight how you can efficiently leverage Azure Cosmos DB to store and query JSON documents, this article provides an end-to-end walk-through showing you how to build a todo app using Azure Cosmos DB.</span></span> <span data-ttu-id="c75e3-113">The tasks will be stored as JSON documents in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c75e3-113">The tasks will be stored as JSON documents in Azure Cosmos DB.</span></span>

![Screen shot of the todo list MVC web application created by this tutorial - ASP NET MVC tutorial step by step](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-image01.png)

<span data-ttu-id="c75e3-115">This walk-through shows you how to use the Azure Cosmos DB service to store and access data from an ASP.NET MVC web application hosted on Azure.</span><span class="sxs-lookup"><span data-stu-id="c75e3-115">This walk-through shows you how to use the Azure Cosmos DB service to store and access data from an ASP.NET MVC web application hosted on Azure.</span></span> <span data-ttu-id="c75e3-116">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not the ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](sql-api-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c75e3-116">If you're looking for a tutorial that focuses only on Azure Cosmos DB, and not the ASP.NET MVC components, see [Build an Azure Cosmos DB C# console application](sql-api-get-started.md).</span></span>

> [!TIP]
> This tutorial assumes that you have prior experience using ASP.NET MVC and Azure Websites. If you are new to ASP.NET or the [prerequisite tools](#_Toc395637760), we recommend downloading the complete sample project from [GitHub][GitHub] and following the instructions in this sample. Once you have it built, you can review this article to gain insight on the code in the context of the project.
> 
> 

## <a name="_Toc395637760"></a><span data-ttu-id="c75e3-120">Prerequisites for this database tutorial</span><span class="sxs-lookup"><span data-stu-id="c75e3-120">Prerequisites for this database tutorial</span></span>
<span data-ttu-id="c75e3-121">Before following the instructions in this article, you should ensure that you have the following:</span><span class="sxs-lookup"><span data-stu-id="c75e3-121">Before following the instructions in this article, you should ensure that you have the following:</span></span>

* <span data-ttu-id="c75e3-122">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="c75e3-122">An active Azure account.</span></span>  <span data-ttu-id="c75e3-123">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="c75e3-123">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span> 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* [!INCLUDE [cosmos-db-emulator-vs](../../includes/cosmos-db-emulator-vs.md)]  
* <span data-ttu-id="c75e3-124">Microsoft Azure SDK for .NET for Visual Studio 2017, available through the Visual Studio Installer.</span><span class="sxs-lookup"><span data-stu-id="c75e3-124">Microsoft Azure SDK for .NET for Visual Studio 2017, available through the Visual Studio Installer.</span></span>

<span data-ttu-id="c75e3-125">All the screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span><span class="sxs-lookup"><span data-stu-id="c75e3-125">All the screen shots in this article have been taken using Microsoft Visual Studio Community 2017.</span></span> <span data-ttu-id="c75e3-126">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span><span class="sxs-lookup"><span data-stu-id="c75e3-126">If your system is configured with a different version it is possible that your screens and options won't match entirely, but if you meet the above prerequisites this solution should work.</span></span>

## <a name="_Toc395637761"></a><span data-ttu-id="c75e3-127">Step 1: Create an Azure Cosmos DB database account</span><span class="sxs-lookup"><span data-stu-id="c75e3-127">Step 1: Create an Azure Cosmos DB database account</span></span>
<span data-ttu-id="c75e3-128">Let's start by creating an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="c75e3-128">Let's start by creating an Azure Cosmos DB account.</span></span> <span data-ttu-id="c75e3-129">If you already have a SQL account for Azure Cosmos DB or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span><span class="sxs-lookup"><span data-stu-id="c75e3-129">If you already have a SQL account for Azure Cosmos DB or if you are using the Azure Cosmos DB Emulator for this tutorial, you can skip to [Create a new ASP.NET MVC application](#_Toc395637762).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

[!INCLUDE [keys](../../includes/cosmos-db-keys.md)]

<br/>
<span data-ttu-id="c75e3-130">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span><span class="sxs-lookup"><span data-stu-id="c75e3-130">We will now walk through how to create a new ASP.NET MVC application from the ground-up.</span></span> 

## <a name="_Toc395637762"></a><span data-ttu-id="c75e3-131">Step 2: Create a new ASP.NET MVC application</span><span class="sxs-lookup"><span data-stu-id="c75e3-131">Step 2: Create a new ASP.NET MVC application</span></span>

1. <span data-ttu-id="c75e3-132">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-132">In Visual Studio, on the **File** menu, point to **New**, and then click **Project**.</span></span> <span data-ttu-id="c75e3-133">The **New Project** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="c75e3-133">The **New Project** dialog box appears.</span></span>

2. <span data-ttu-id="c75e3-134">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-134">In the **Project types** pane, expand **Templates**, **Visual C#**, **Web**, and then select **ASP.NET Web Application**.</span></span>

      ![Screen shot of the New Project dialog box with the ASP.NET Web Application project type highlighted](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-new-project-dialog.png)

3. <span data-ttu-id="c75e3-136">In the **Name** box, type the name of the project.</span><span class="sxs-lookup"><span data-stu-id="c75e3-136">In the **Name** box, type the name of the project.</span></span> <span data-ttu-id="c75e3-137">This tutorial uses the name "todo".</span><span class="sxs-lookup"><span data-stu-id="c75e3-137">This tutorial uses the name "todo".</span></span> <span data-ttu-id="c75e3-138">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span><span class="sxs-lookup"><span data-stu-id="c75e3-138">If you choose to use something other than this, then wherever this tutorial talks about the todo namespace, you need to adjust the provided code samples to use whatever you named your application.</span></span> 
4. <span data-ttu-id="c75e3-139">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-139">Click **Browse** to navigate to the folder where you would like to create the project, and then click **OK**.</span></span>
   
      <span data-ttu-id="c75e3-140">The **New ASP.NET Web Application** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="c75e3-140">The **New ASP.NET Web Application** dialog box appears.</span></span>
   
    ![Screen shot of the New ASP.NET Web Application dialog box with the MVC application template highlighted](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-MVC.png)
5. <span data-ttu-id="c75e3-142">In the templates pane, select **MVC**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-142">In the templates pane, select **MVC**.</span></span>

6. <span data-ttu-id="c75e3-143">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span><span class="sxs-lookup"><span data-stu-id="c75e3-143">Click **OK** and let Visual Studio do its thing around scaffolding the empty ASP.NET MVC template.</span></span> 

          
7. <span data-ttu-id="c75e3-144">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span><span class="sxs-lookup"><span data-stu-id="c75e3-144">Once Visual Studio has finished creating the boilerplate MVC application you have an empty ASP.NET application that you can run locally.</span></span>
   
    <span data-ttu-id="c75e3-145">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span><span class="sxs-lookup"><span data-stu-id="c75e3-145">We'll skip running the project locally because I'm sure we've all seen the ASP.NET "Hello World" application.</span></span> <span data-ttu-id="c75e3-146">Let's go straight to adding Azure Cosmos DB to this project and building our application.</span><span class="sxs-lookup"><span data-stu-id="c75e3-146">Let's go straight to adding Azure Cosmos DB to this project and building our application.</span></span>

## <a name="_Toc395637767"></a><span data-ttu-id="c75e3-147">Step 3: Add Azure Cosmos DB to your MVC web application project</span><span class="sxs-lookup"><span data-stu-id="c75e3-147">Step 3: Add Azure Cosmos DB to your MVC web application project</span></span>
<span data-ttu-id="c75e3-148">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure Cosmos DB to our MVC web application.</span><span class="sxs-lookup"><span data-stu-id="c75e3-148">Now that we have most of the ASP.NET MVC plumbing that we need for this solution, let's get to the real purpose of this tutorial, adding Azure Cosmos DB to our MVC web application.</span></span>

1. <span data-ttu-id="c75e3-149">The Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span><span class="sxs-lookup"><span data-stu-id="c75e3-149">The Azure Cosmos DB .NET SDK is packaged and distributed as a NuGet package.</span></span> <span data-ttu-id="c75e3-150">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-150">To get the NuGet package in Visual Studio, use the NuGet package manager in Visual Studio by right-clicking on the project in **Solution Explorer** and then clicking **Manage NuGet Packages**.</span></span>
   
    ![Screen shot of the right-click options for the web application project in Solution Explorer, with Manage NuGet Packages highlighted.](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-manage-nuget.png)
   
    <span data-ttu-id="c75e3-152">The **Manage NuGet Packages** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="c75e3-152">The **Manage NuGet Packages** dialog box appears.</span></span>
2. <span data-ttu-id="c75e3-153">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-153">In the NuGet **Browse** box, type ***Azure DocumentDB***.</span></span> <span data-ttu-id="c75e3-154">(The package name has not been updated to Azure Cosmos DB.)</span><span class="sxs-lookup"><span data-stu-id="c75e3-154">(The package name has not been updated to Azure Cosmos DB.)</span></span>
   
    <span data-ttu-id="c75e3-155">From the results, install the **Microsoft.Azure.DocumentDB by Microsoft** package.</span><span class="sxs-lookup"><span data-stu-id="c75e3-155">From the results, install the **Microsoft.Azure.DocumentDB by Microsoft** package.</span></span> <span data-ttu-id="c75e3-156">This will download and install the Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="c75e3-156">This will download and install the Azure Cosmos DB package as well as all dependencies, such as Newtonsoft.Json.</span></span> <span data-ttu-id="c75e3-157">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span><span class="sxs-lookup"><span data-stu-id="c75e3-157">Click **OK** in the **Preview** window, and **I Accept** in the **License Acceptance** window to complete the install.</span></span>
   
    ![Sreen shot of the Manage NuGet Packages window, with the Microsoft Azure Cosmos DB Client Library highlighted](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-install-nuget.png)
   
      <span data-ttu-id="c75e3-159">Alternatively you can use the Package Manager Console to install the package.</span><span class="sxs-lookup"><span data-stu-id="c75e3-159">Alternatively you can use the Package Manager Console to install the package.</span></span> <span data-ttu-id="c75e3-160">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-160">To do so, on the **Tools** menu, click **NuGet Package Manager**, and then click **Package Manager Console**.</span></span> <span data-ttu-id="c75e3-161">At the prompt, type the following.</span><span class="sxs-lookup"><span data-stu-id="c75e3-161">At the prompt, type the following.</span></span>
   
        Install-Package Microsoft.Azure.DocumentDB
        
3. <span data-ttu-id="c75e3-162">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span><span class="sxs-lookup"><span data-stu-id="c75e3-162">Once the package is installed, your Visual Studio solution should resemble the following with two new references added, Microsoft.Azure.Documents.Client and Newtonsoft.Json.</span></span>
   
    ![Sreen shot of the two references added to the JSON data project in Solution Explorer](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-added-references.png)

## <a name="_Toc395637763"></a><span data-ttu-id="c75e3-164">Step 4: Set up the ASP.NET MVC application</span><span class="sxs-lookup"><span data-stu-id="c75e3-164">Step 4: Set up the ASP.NET MVC application</span></span>
<span data-ttu-id="c75e3-165">Now let's add the models, views, and controllers to this MVC application:</span><span class="sxs-lookup"><span data-stu-id="c75e3-165">Now let's add the models, views, and controllers to this MVC application:</span></span>

* <span data-ttu-id="c75e3-166">[Add a model](#_Toc395637764).</span><span class="sxs-lookup"><span data-stu-id="c75e3-166">[Add a model](#_Toc395637764).</span></span>
* <span data-ttu-id="c75e3-167">[Add a controller](#_Toc395637765).</span><span class="sxs-lookup"><span data-stu-id="c75e3-167">[Add a controller](#_Toc395637765).</span></span>
* <span data-ttu-id="c75e3-168">[Add views](#_Toc395637766).</span><span class="sxs-lookup"><span data-stu-id="c75e3-168">[Add views](#_Toc395637766).</span></span>

### <a name="_Toc395637764"></a><span data-ttu-id="c75e3-169">Add a JSON data model</span><span class="sxs-lookup"><span data-stu-id="c75e3-169">Add a JSON data model</span></span>
<span data-ttu-id="c75e3-170">Let's begin by creating the **M** in MVC, the model.</span><span class="sxs-lookup"><span data-stu-id="c75e3-170">Let's begin by creating the **M** in MVC, the model.</span></span> 

1. <span data-ttu-id="c75e3-171">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-171">In **Solution Explorer**, right-click the **Models** folder, click **Add**, and then click **Class**.</span></span>
   
      <span data-ttu-id="c75e3-172">The **Add New Item** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="c75e3-172">The **Add New Item** dialog box appears.</span></span>
2. <span data-ttu-id="c75e3-173">Name your new class **Item.cs** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-173">Name your new class **Item.cs** and click **Add**.</span></span> 
3. <span data-ttu-id="c75e3-174">In this new **Item.cs** file, add the following after the last *using statement*.</span><span class="sxs-lookup"><span data-stu-id="c75e3-174">In this new **Item.cs** file, add the following after the last *using statement*.</span></span>
   
        using Newtonsoft.Json;
4. <span data-ttu-id="c75e3-175">Now replace this code</span><span class="sxs-lookup"><span data-stu-id="c75e3-175">Now replace this code</span></span> 
   
        public class Item
        {
        }
   
    <span data-ttu-id="c75e3-176">with the following code.</span><span class="sxs-lookup"><span data-stu-id="c75e3-176">with the following code.</span></span>
   
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
   
    <span data-ttu-id="c75e3-177">All data in Azure Cosmos DB is passed over the wire and stored as JSON.</span><span class="sxs-lookup"><span data-stu-id="c75e3-177">All data in Azure Cosmos DB is passed over the wire and stored as JSON.</span></span> <span data-ttu-id="c75e3-178">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span><span class="sxs-lookup"><span data-stu-id="c75e3-178">To control the way your objects are serialized/deserialized by JSON.NET you can use the **JsonProperty** attribute as demonstrated in the **Item** class we just created.</span></span> <span data-ttu-id="c75e3-179">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span><span class="sxs-lookup"><span data-stu-id="c75e3-179">You don't **have** to do this but I want to ensure that my properties follow the JSON camelCase naming conventions.</span></span> 
   
    <span data-ttu-id="c75e3-180">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span><span class="sxs-lookup"><span data-stu-id="c75e3-180">Not only can you control the format of the property name when it goes into JSON, but you can entirely rename your .NET properties like I did with the **Description** property.</span></span> 

### <a name="_Toc395637765"></a><span data-ttu-id="c75e3-181">Add a controller</span><span class="sxs-lookup"><span data-stu-id="c75e3-181">Add a controller</span></span>
<span data-ttu-id="c75e3-182">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span><span class="sxs-lookup"><span data-stu-id="c75e3-182">That takes care of the **M**, now let's create the **C** in MVC, a controller class.</span></span>

1. <span data-ttu-id="c75e3-183">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-183">In **Solution Explorer**, right-click the **Controllers** folder, click **Add**, and then click **Controller**.</span></span>
   
    <span data-ttu-id="c75e3-184">The **Add Scaffold** dialog box appears.</span><span class="sxs-lookup"><span data-stu-id="c75e3-184">The **Add Scaffold** dialog box appears.</span></span>
2. <span data-ttu-id="c75e3-185">Select **MVC 5 Controller - Empty** and then click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-185">Select **MVC 5 Controller - Empty** and then click **Add**.</span></span>
   
    ![Screen shot of the Add Scaffold dialog box with the MVC 5 Controller - Empty option highlighted](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-controller-add-scaffold.png)
3. <span data-ttu-id="c75e3-187">Name your new Controller, **ItemController.**</span><span class="sxs-lookup"><span data-stu-id="c75e3-187">Name your new Controller, **ItemController.**</span></span>
   
    ![Screen shot of the Add Controller dialog box](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-add-controller.png)
   
    <span data-ttu-id="c75e3-189">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-189">Once the file is created, your Visual Studio solution should resemble the following with the new ItemController.cs file in **Solution Explorer**.</span></span> <span data-ttu-id="c75e3-190">The new Item.cs file created earlier is also shown.</span><span class="sxs-lookup"><span data-stu-id="c75e3-190">The new Item.cs file created earlier is also shown.</span></span>
   
    ![Screen shot of the Visual Studio solution - Solution Explorer with the new ItemController.cs file and Item.cs file highlighted](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-new-item-solution-explorer.png)
   
    <span data-ttu-id="c75e3-192">You can close ItemController.cs, we'll come back to it later.</span><span class="sxs-lookup"><span data-stu-id="c75e3-192">You can close ItemController.cs, we'll come back to it later.</span></span> 

### <a name="_Toc395637766"></a><span data-ttu-id="c75e3-193">Add views</span><span class="sxs-lookup"><span data-stu-id="c75e3-193">Add views</span></span>
<span data-ttu-id="c75e3-194">Now, let's create the **V** in MVC, the views:</span><span class="sxs-lookup"><span data-stu-id="c75e3-194">Now, let's create the **V** in MVC, the views:</span></span>

* <span data-ttu-id="c75e3-195">[Add an Item Index view](#AddItemIndexView).</span><span class="sxs-lookup"><span data-stu-id="c75e3-195">[Add an Item Index view](#AddItemIndexView).</span></span>
* <span data-ttu-id="c75e3-196">[Add a New Item view](#AddNewIndexView).</span><span class="sxs-lookup"><span data-stu-id="c75e3-196">[Add a New Item view](#AddNewIndexView).</span></span>
* <span data-ttu-id="c75e3-197">[Add an Edit Item view](#_Toc395888515).</span><span class="sxs-lookup"><span data-stu-id="c75e3-197">[Add an Edit Item view](#_Toc395888515).</span></span>

#### <a name="AddItemIndexView"></a><span data-ttu-id="c75e3-198">Add an Item Index view</span><span class="sxs-lookup"><span data-stu-id="c75e3-198">Add an Item Index view</span></span>
1. <span data-ttu-id="c75e3-199">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-199">In **Solution Explorer**, expand the **Views**  folder, right-click the empty **Item** folder that Visual Studio created for you when you added the **ItemController** earlier, click **Add**, and then click **View**.</span></span>
   
    ![Screen shot of Solution Explorer showing the Item folder that Visual Studio created with the Add View commands highlighted](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-add-view.png)
2. <span data-ttu-id="c75e3-201">In the **Add View** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="c75e3-201">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="c75e3-202">In the **View name** box, type ***Index***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-202">In the **View name** box, type ***Index***.</span></span>
   * <span data-ttu-id="c75e3-203">In the **Template** box, select ***List***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-203">In the **Template** box, select ***List***.</span></span>
   * <span data-ttu-id="c75e3-204">In the **Model class** box, select ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-204">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="c75e3-205">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-205">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
     
   ![Screen shot showing the Add View dialog box](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-add-view-dialog.png)
3. <span data-ttu-id="c75e3-207">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span><span class="sxs-lookup"><span data-stu-id="c75e3-207">Once all these values are set, click **Add** and let Visual Studio create a new template view.</span></span> <span data-ttu-id="c75e3-208">Once it is done, it will open the cshtml file  that was created.</span><span class="sxs-lookup"><span data-stu-id="c75e3-208">Once it is done, it will open the cshtml file  that was created.</span></span> <span data-ttu-id="c75e3-209">We can close that file in Visual Studio as we will come back to it later.</span><span class="sxs-lookup"><span data-stu-id="c75e3-209">We can close that file in Visual Studio as we will come back to it later.</span></span>

#### <a name="AddNewIndexView"></a><span data-ttu-id="c75e3-210">Add a New Item view</span><span class="sxs-lookup"><span data-stu-id="c75e3-210">Add a New Item view</span></span>
<span data-ttu-id="c75e3-211">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-211">Similar to how we created an **Item Index** view, we will now create a new view for creating new **Items**.</span></span>

1. <span data-ttu-id="c75e3-212">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-212">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="c75e3-213">In the **Add View** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="c75e3-213">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="c75e3-214">In the **View name** box, type ***Create***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-214">In the **View name** box, type ***Create***.</span></span>
   * <span data-ttu-id="c75e3-215">In the **Template** box, select ***Create***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-215">In the **Template** box, select ***Create***.</span></span>
   * <span data-ttu-id="c75e3-216">In the **Model class** box, select ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-216">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="c75e3-217">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-217">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="c75e3-218">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-218">Click **Add**.</span></span>
   
#### <a name="_Toc395888515"></a><span data-ttu-id="c75e3-219">Add an Edit Item view</span><span class="sxs-lookup"><span data-stu-id="c75e3-219">Add an Edit Item view</span></span>
<span data-ttu-id="c75e3-220">And finally, add one last view for editing an **Item** in the same way as before.</span><span class="sxs-lookup"><span data-stu-id="c75e3-220">And finally, add one last view for editing an **Item** in the same way as before.</span></span>

1. <span data-ttu-id="c75e3-221">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-221">In **Solution Explorer**, right-click the **Item** folder again, click **Add**, and then click **View**.</span></span>
2. <span data-ttu-id="c75e3-222">In the **Add View** dialog box, do the following:</span><span class="sxs-lookup"><span data-stu-id="c75e3-222">In the **Add View** dialog box, do the following:</span></span>
   
   * <span data-ttu-id="c75e3-223">In the **View name** box, type ***Edit***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-223">In the **View name** box, type ***Edit***.</span></span>
   * <span data-ttu-id="c75e3-224">In the **Template** box, select ***Edit***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-224">In the **Template** box, select ***Edit***.</span></span>
   * <span data-ttu-id="c75e3-225">In the **Model class** box, select ***Item (todo.Models)***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-225">In the **Model class** box, select ***Item (todo.Models)***.</span></span>
   * <span data-ttu-id="c75e3-226">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span><span class="sxs-lookup"><span data-stu-id="c75e3-226">In the layout page box, type ***~/Views/Shared/_Layout.cshtml***.</span></span>
   * <span data-ttu-id="c75e3-227">Click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-227">Click **Add**.</span></span>

<span data-ttu-id="c75e3-228">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span><span class="sxs-lookup"><span data-stu-id="c75e3-228">Once this is done, close all the cshtml documents in Visual Studio as we will return to these views later.</span></span>

## <a name="_Toc395637769"></a><span data-ttu-id="c75e3-229">Step 5: Wiring up Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c75e3-229">Step 5: Wiring up Azure Cosmos DB</span></span>
<span data-ttu-id="c75e3-230">Now that the standard MVC stuff is taken care of, let's turn to adding the code for Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c75e3-230">Now that the standard MVC stuff is taken care of, let's turn to adding the code for Azure Cosmos DB.</span></span> 

<span data-ttu-id="c75e3-231">In this section, we'll add code to handle the following:</span><span class="sxs-lookup"><span data-stu-id="c75e3-231">In this section, we'll add code to handle the following:</span></span>

* <span data-ttu-id="c75e3-232">[Listing incomplete Items](#_Toc395637770).</span><span class="sxs-lookup"><span data-stu-id="c75e3-232">[Listing incomplete Items](#_Toc395637770).</span></span>
* <span data-ttu-id="c75e3-233">[Adding Items](#_Toc395637771).</span><span class="sxs-lookup"><span data-stu-id="c75e3-233">[Adding Items](#_Toc395637771).</span></span>
* <span data-ttu-id="c75e3-234">[Editing Items](#_Toc395637772).</span><span class="sxs-lookup"><span data-stu-id="c75e3-234">[Editing Items](#_Toc395637772).</span></span>

### <a name="_Toc395637770"></a><span data-ttu-id="c75e3-235">Listing incomplete Items in your MVC web application</span><span class="sxs-lookup"><span data-stu-id="c75e3-235">Listing incomplete Items in your MVC web application</span></span>
<span data-ttu-id="c75e3-236">The first thing to do here is add a class that contains all the logic to connect to and use Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c75e3-236">The first thing to do here is add a class that contains all the logic to connect to and use Azure Cosmos DB.</span></span> <span data-ttu-id="c75e3-237">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span><span class="sxs-lookup"><span data-stu-id="c75e3-237">For this tutorial we'll encapsulate all this logic in to a repository class called DocumentDBRepository.</span></span> 

1. <span data-ttu-id="c75e3-238">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-238">In **Solution Explorer**, right-click on the project, click **Add**, and then click **Class**.</span></span> <span data-ttu-id="c75e3-239">Name the new class **DocumentDBRepository** and click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-239">Name the new class **DocumentDBRepository** and click **Add**.</span></span>
2. <span data-ttu-id="c75e3-240">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span><span class="sxs-lookup"><span data-stu-id="c75e3-240">In the newly created **DocumentDBRepository** class and add the following *using statements* above the *namespace* declaration</span></span>
   
        using Microsoft.Azure.Documents; 
        using Microsoft.Azure.Documents.Client; 
        using Microsoft.Azure.Documents.Linq; 
        using System.Configuration;
        using System.Linq.Expressions;
        using System.Threading.Tasks;
        using System.Net;
        
    <span data-ttu-id="c75e3-241">Now replace this code</span><span class="sxs-lookup"><span data-stu-id="c75e3-241">Now replace this code</span></span> 
   
        public class DocumentDBRepository
        {
        }
   
    <span data-ttu-id="c75e3-242">with the following code.</span><span class="sxs-lookup"><span data-stu-id="c75e3-242">with the following code.</span></span>
   
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
   
    
3. <span data-ttu-id="c75e3-243">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span><span class="sxs-lookup"><span data-stu-id="c75e3-243">We're reading some values from configuration, so open the **Web.config** file of your application and add the following lines under the `<AppSettings>` section.</span></span>
   
        <add key="endpoint" value="enter the URI from the Keys blade of the Azure Portal"/>
        <add key="authKey" value="enter the PRIMARY KEY, or the SECONDARY KEY, from the Keys blade of the Azure  Portal"/>
        <add key="database" value="ToDoList"/>
        <add key="collection" value="Items"/>
4. <span data-ttu-id="c75e3-244">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="c75e3-244">Now, update the values for *endpoint* and *authKey* using the Keys blade of the Azure Portal.</span></span> <span data-ttu-id="c75e3-245">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span><span class="sxs-lookup"><span data-stu-id="c75e3-245">Use the **URI** from the Keys blade as the value of the endpoint setting, and use the **PRIMARY KEY**, or **SECONDARY KEY** from the Keys blade as the value of the authKey setting.</span></span>

    <span data-ttu-id="c75e3-246">That takes care of wiring up the Azure Cosmos DB repository, now let's add our application logic.</span><span class="sxs-lookup"><span data-stu-id="c75e3-246">That takes care of wiring up the Azure Cosmos DB repository, now let's add our application logic.</span></span>

1. <span data-ttu-id="c75e3-247">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span><span class="sxs-lookup"><span data-stu-id="c75e3-247">The first thing we want to be able to do with a todo list application is to display the incomplete items.</span></span>  <span data-ttu-id="c75e3-248">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span><span class="sxs-lookup"><span data-stu-id="c75e3-248">Copy and paste the following code snippet anywhere within the **DocumentDBRepository** class.</span></span>
   
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
2. <span data-ttu-id="c75e3-249">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span><span class="sxs-lookup"><span data-stu-id="c75e3-249">Open the **ItemController** we added earlier and add the following *using statements* above the namespace declaration.</span></span>
   
        using System.Net;
        using System.Threading.Tasks;
        using todo.Models;
   
    <span data-ttu-id="c75e3-250">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span><span class="sxs-lookup"><span data-stu-id="c75e3-250">If your project is not named "todo", then you need to update using "todo.Models"; to reflect the name of your project.</span></span>
   
    <span data-ttu-id="c75e3-251">Now replace this code</span><span class="sxs-lookup"><span data-stu-id="c75e3-251">Now replace this code</span></span>
   
        //GET: Item
        public ActionResult Index()
        {
            return View();
        }
   
    <span data-ttu-id="c75e3-252">with the following code.</span><span class="sxs-lookup"><span data-stu-id="c75e3-252">with the following code.</span></span>
   
        [ActionName("Index")]
        public async Task<ActionResult> IndexAsync()
        {
            var items = await DocumentDBRepository<Item>.GetItemsAsync(d => !d.Completed);
            return View(items);
        }
3. <span data-ttu-id="c75e3-253">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span><span class="sxs-lookup"><span data-stu-id="c75e3-253">Open **Global.asax.cs** and add the following line to the **Application_Start** method</span></span> 
   
        DocumentDBRepository<todo.Models.Item>.Initialize();

<span data-ttu-id="c75e3-254">At this point your solution should be able to build without any errors.</span><span class="sxs-lookup"><span data-stu-id="c75e3-254">At this point your solution should be able to build without any errors.</span></span>

<span data-ttu-id="c75e3-255">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span><span class="sxs-lookup"><span data-stu-id="c75e3-255">If you ran the application now, you would go to the **HomeController** and the **Index** view of that controller.</span></span> <span data-ttu-id="c75e3-256">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span><span class="sxs-lookup"><span data-stu-id="c75e3-256">This is the default behavior for the MVC template project we chose at the start but we don't want that!</span></span> <span data-ttu-id="c75e3-257">Let's change the routing on this MVC application to alter this behavior.</span><span class="sxs-lookup"><span data-stu-id="c75e3-257">Let's change the routing on this MVC application to alter this behavior.</span></span>

<span data-ttu-id="c75e3-258">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span><span class="sxs-lookup"><span data-stu-id="c75e3-258">Open ***App\_Start\RouteConfig.cs*** and locate the line starting with "defaults:" and change it to resemble the following.</span></span>

        defaults: new { controller = "Item", action = "Index", id = UrlParameter.Optional }

<span data-ttu-id="c75e3-259">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span><span class="sxs-lookup"><span data-stu-id="c75e3-259">This now tells ASP.NET MVC that if you have not specified a value in the URL to control the routing behavior that instead of **Home**, use **Item** as the controller and user **Index** as the view.</span></span>

<span data-ttu-id="c75e3-260">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span><span class="sxs-lookup"><span data-stu-id="c75e3-260">Now if you run the application, it will call into your **ItemController** which will call in to the repository class and use the GetItems method to return all the incomplete items to the **Views**\\**Item**\\**Index** view.</span></span> 

<span data-ttu-id="c75e3-261">If you build and run this project now, you should now see something that looks this.</span><span class="sxs-lookup"><span data-stu-id="c75e3-261">If you build and run this project now, you should now see something that looks this.</span></span>    

![Screen shot of the todo list web application created by this database tutorial](./media/sql-api-dotnet-application/build-and-run-the-project-now.png)

### <a name="_Toc395637771"></a><span data-ttu-id="c75e3-263">Adding Items</span><span class="sxs-lookup"><span data-stu-id="c75e3-263">Adding Items</span></span>
<span data-ttu-id="c75e3-264">Let's put some items into our database so we have something more than an empty grid to look at.</span><span class="sxs-lookup"><span data-stu-id="c75e3-264">Let's put some items into our database so we have something more than an empty grid to look at.</span></span>

<span data-ttu-id="c75e3-265">Let's add some code to  Azure Cosmos DBRepository and ItemController to persist the record in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c75e3-265">Let's add some code to  Azure Cosmos DBRepository and ItemController to persist the record in Azure Cosmos DB.</span></span>

1. <span data-ttu-id="c75e3-266">Add the following method to your **DocumentDBRepository** class.</span><span class="sxs-lookup"><span data-stu-id="c75e3-266">Add the following method to your **DocumentDBRepository** class.</span></span>
   
       public static async Task<Document> CreateItemAsync(T item)
       {
           return await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(DatabaseId, CollectionId), item);
       }
   
   <span data-ttu-id="c75e3-267">This method simply takes an object passed to it and persists it in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c75e3-267">This method simply takes an object passed to it and persists it in Azure Cosmos DB.</span></span>
2. <span data-ttu-id="c75e3-268">Open the ItemController.cs file and add the following code snippet within the class.</span><span class="sxs-lookup"><span data-stu-id="c75e3-268">Open the ItemController.cs file and add the following code snippet within the class.</span></span> <span data-ttu-id="c75e3-269">This is how ASP.NET MVC knows what to do for the **Create** action.</span><span class="sxs-lookup"><span data-stu-id="c75e3-269">This is how ASP.NET MVC knows what to do for the **Create** action.</span></span> <span data-ttu-id="c75e3-270">In this case just render the associated Create.cshtml view created earlier.</span><span class="sxs-lookup"><span data-stu-id="c75e3-270">In this case just render the associated Create.cshtml view created earlier.</span></span>
   
        [ActionName("Create")]
        public async Task<ActionResult> CreateAsync()
        {
            return View();
        }
   
    <span data-ttu-id="c75e3-271">We now need some more code in this controller that will accept the submission from the **Create** view.</span><span class="sxs-lookup"><span data-stu-id="c75e3-271">We now need some more code in this controller that will accept the submission from the **Create** view.</span></span>
3. <span data-ttu-id="c75e3-272">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span><span class="sxs-lookup"><span data-stu-id="c75e3-272">Add the next block of code to the ItemController.cs class that tells ASP.NET MVC what to do with a form POST for this controller.</span></span>
   
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
   
    <span data-ttu-id="c75e3-273">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span><span class="sxs-lookup"><span data-stu-id="c75e3-273">This code calls in to the DocumentDBRepository and uses the CreateItemAsync method to persist the new todo item to the database.</span></span> 
   
    <span data-ttu-id="c75e3-274">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span><span class="sxs-lookup"><span data-stu-id="c75e3-274">**Security Note**: The **ValidateAntiForgeryToken** attribute is used here to help protect this application against cross-site request forgery attacks.</span></span> <span data-ttu-id="c75e3-275">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span><span class="sxs-lookup"><span data-stu-id="c75e3-275">There is more to it than just adding this attribute, your views need to work with this anti-forgery token as well.</span></span> <span data-ttu-id="c75e3-276">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span><span class="sxs-lookup"><span data-stu-id="c75e3-276">For more on the subject, and examples of how to implement this correctly, please see [Preventing Cross-Site Request Forgery][Preventing Cross-Site Request Forgery].</span></span> <span data-ttu-id="c75e3-277">The source code provided on [GitHub][GitHub] has the full implementation in place.</span><span class="sxs-lookup"><span data-stu-id="c75e3-277">The source code provided on [GitHub][GitHub] has the full implementation in place.</span></span>
   
    <span data-ttu-id="c75e3-278">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span><span class="sxs-lookup"><span data-stu-id="c75e3-278">**Security Note**: We also use the **Bind** attribute on the method parameter to help protect against over-posting attacks.</span></span> <span data-ttu-id="c75e3-279">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span><span class="sxs-lookup"><span data-stu-id="c75e3-279">For more details please see [Basic CRUD Operations in ASP.NET MVC][Basic CRUD Operations in ASP.NET MVC].</span></span>

<span data-ttu-id="c75e3-280">This concludes the code required to add new Items to our database.</span><span class="sxs-lookup"><span data-stu-id="c75e3-280">This concludes the code required to add new Items to our database.</span></span>

### <a name="_Toc395637772"></a><span data-ttu-id="c75e3-281">Editing Items</span><span class="sxs-lookup"><span data-stu-id="c75e3-281">Editing Items</span></span>
<span data-ttu-id="c75e3-282">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span><span class="sxs-lookup"><span data-stu-id="c75e3-282">There is one last thing for us to do, and that is to add the ability to edit **Items** in the database and to mark them as complete.</span></span> <span data-ttu-id="c75e3-283">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span><span class="sxs-lookup"><span data-stu-id="c75e3-283">The view for editing was already added to the project, so we just need to add some code to our controller and to the **DocumentDBRepository** class again.</span></span>

1. <span data-ttu-id="c75e3-284">Add the following to the **DocumentDBRepository** class.</span><span class="sxs-lookup"><span data-stu-id="c75e3-284">Add the following to the **DocumentDBRepository** class.</span></span>
   
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
   
    <span data-ttu-id="c75e3-285">The first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back to the **ItemController** and then on to the **Edit** view.</span><span class="sxs-lookup"><span data-stu-id="c75e3-285">The first of these methods, **GetItem** fetches an Item from Azure Cosmos DB which is passed back to the **ItemController** and then on to the **Edit** view.</span></span>
   
    <span data-ttu-id="c75e3-286">The second of the methods we just added replaces the **Document** in Azure Cosmos DB with the version of the **Document** passed in from the **ItemController**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-286">The second of the methods we just added replaces the **Document** in Azure Cosmos DB with the version of the **Document** passed in from the **ItemController**.</span></span>
2. <span data-ttu-id="c75e3-287">Add the following to the **ItemController** class.</span><span class="sxs-lookup"><span data-stu-id="c75e3-287">Add the following to the **ItemController** class.</span></span>
   
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
   
    <span data-ttu-id="c75e3-288">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span><span class="sxs-lookup"><span data-stu-id="c75e3-288">The first method handles the Http GET that happens when the user clicks on the **Edit** link from the **Index** view.</span></span> <span data-ttu-id="c75e3-289">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it to the **Edit** view.</span><span class="sxs-lookup"><span data-stu-id="c75e3-289">This method fetches a [**Document**](http://msdn.microsoft.com/library/azure/microsoft.azure.documents.document.aspx) from Azure Cosmos DB and passes it to the **Edit** view.</span></span>
   
    <span data-ttu-id="c75e3-290">The **Edit** view will then do an Http POST to the **IndexController**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-290">The **Edit** view will then do an Http POST to the **IndexController**.</span></span> 
   
    <span data-ttu-id="c75e3-291">The second method we added handles passing the updated object to Azure Cosmos DB to be persisted in the database.</span><span class="sxs-lookup"><span data-stu-id="c75e3-291">The second method we added handles passing the updated object to Azure Cosmos DB to be persisted in the database.</span></span>

<span data-ttu-id="c75e3-292">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-292">That's it, that is everything we need to run our application, list incomplete **Items**, add new **Items**, and edit **Items**.</span></span>

## <a name="_Toc395637773"></a><span data-ttu-id="c75e3-293">Step 6: Run the application locally</span><span class="sxs-lookup"><span data-stu-id="c75e3-293">Step 6: Run the application locally</span></span>
<span data-ttu-id="c75e3-294">To test the application on your local machine, do the following:</span><span class="sxs-lookup"><span data-stu-id="c75e3-294">To test the application on your local machine, do the following:</span></span>

1. <span data-ttu-id="c75e3-295">Hit F5 in Visual Studio to build the application in debug mode.</span><span class="sxs-lookup"><span data-stu-id="c75e3-295">Hit F5 in Visual Studio to build the application in debug mode.</span></span> <span data-ttu-id="c75e3-296">It should build the application and launch a browser with the empty grid page we saw before:</span><span class="sxs-lookup"><span data-stu-id="c75e3-296">It should build the application and launch a browser with the empty grid page we saw before:</span></span>
   
    ![Screen shot of the todo list web application created by this database tutorial](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-create-an-item-a.png)
   
     
2. <span data-ttu-id="c75e3-298">Click the **Create New** link and add values to the **Name** and **Description** fields.</span><span class="sxs-lookup"><span data-stu-id="c75e3-298">Click the **Create New** link and add values to the **Name** and **Description** fields.</span></span> <span data-ttu-id="c75e3-299">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span><span class="sxs-lookup"><span data-stu-id="c75e3-299">Leave the **Completed** check box unselected otherwise the new **Item** will be added in a completed state and will not appear on the initial list.</span></span>
   
    ![Screen shot of the Create view](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-create-new-item.png)
3. <span data-ttu-id="c75e3-301">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span><span class="sxs-lookup"><span data-stu-id="c75e3-301">Click **Create** and you are redirected back to the **Index** view and your **Item** appears in the list.</span></span>
   
    ![Screen shot of the Index view](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-create-an-item.png)
   
    <span data-ttu-id="c75e3-303">Feel free to add a few more **Items** to your todo list.</span><span class="sxs-lookup"><span data-stu-id="c75e3-303">Feel free to add a few more **Items** to your todo list.</span></span>
    
4. <span data-ttu-id="c75e3-304">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span><span class="sxs-lookup"><span data-stu-id="c75e3-304">Click **Edit** next to an **Item** on the list and you are taken to the **Edit** view where you can update any property of your object, including the **Completed** flag.</span></span> <span data-ttu-id="c75e3-305">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span><span class="sxs-lookup"><span data-stu-id="c75e3-305">If you mark the **Complete** flag and click **Save**, the **Item** is removed from the list of incomplete tasks.</span></span>
   
    ![Screen shot of the Index view with the Completed box checked](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-completed-item.png)
5. <span data-ttu-id="c75e3-307">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span><span class="sxs-lookup"><span data-stu-id="c75e3-307">Once you've tested the app, press Ctrl+F5 to stop debugging the app.</span></span> <span data-ttu-id="c75e3-308">You're ready to deploy!</span><span class="sxs-lookup"><span data-stu-id="c75e3-308">You're ready to deploy!</span></span>

## <a name="_Toc395637774"></a><span data-ttu-id="c75e3-309">Step 7: Deploy the application to Azure App Service</span><span class="sxs-lookup"><span data-stu-id="c75e3-309">Step 7: Deploy the application to Azure App Service</span></span> 
<span data-ttu-id="c75e3-310">Now that you have the complete application working correctly with Azure Cosmos DB we're going to deploy this web app to Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c75e3-310">Now that you have the complete application working correctly with Azure Cosmos DB we're going to deploy this web app to Azure App Service.</span></span>  

1. <span data-ttu-id="c75e3-311">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-311">To publish this application all you need to do is right-click on the project in **Solution Explorer** and click **Publish**.</span></span>
   
    ![Screen shot of the Publish option in Solution Explorer](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-publish.png)

2. <span data-ttu-id="c75e3-313">In the **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** to create an App Service profile, or click **Select Existing** to use an existing profile.</span><span class="sxs-lookup"><span data-stu-id="c75e3-313">In the **Publish** dialog box, click **Microsoft Azure App Service**, then select **Create New** to create an App Service profile, or click **Select Existing** to use an existing profile.</span></span>

    ![Publish dialog box in Visual Studio](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-publish-to-existing.png)

3. <span data-ttu-id="c75e3-315">If you have an existing Azure App Service profile, enter your subscription name.</span><span class="sxs-lookup"><span data-stu-id="c75e3-315">If you have an existing Azure App Service profile, enter your subscription name.</span></span> <span data-ttu-id="c75e3-316">Use the **View** filter to sort by resource group or resource type, then select your Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c75e3-316">Use the **View** filter to sort by resource group or resource type, then select your Azure App Service.</span></span> 
   
    ![App Service dialog box in Visual Studio](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-app-service.png)

4. <span data-ttu-id="c75e3-318">To create a new Azure App Service profile, click **Create New** in the **Publish** dialog box.</span><span class="sxs-lookup"><span data-stu-id="c75e3-318">To create a new Azure App Service profile, click **Create New** in the **Publish** dialog box.</span></span> <span data-ttu-id="c75e3-319">In the **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span><span class="sxs-lookup"><span data-stu-id="c75e3-319">In the **Create App Service** dialog, enter your Web App name and appropriate subscription, resource group, and App Service plan, then click **Create**.</span></span>

    ![Create App Service dialog box in Visual Studio](./media/sql-api-dotnet-application/asp-net-mvc-tutorial-create-app-service.png)

<span data-ttu-id="c75e3-321">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span><span class="sxs-lookup"><span data-stu-id="c75e3-321">In a few seconds, Visual Studio will finish publishing your web application and launch a browser where you can see your handiwork running in Azure!</span></span>



## <a name="_Toc395637775"></a><span data-ttu-id="c75e3-322">Next steps</span><span class="sxs-lookup"><span data-stu-id="c75e3-322">Next steps</span></span>
<span data-ttu-id="c75e3-323">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="c75e3-323">Congratulations!</span></span> <span data-ttu-id="c75e3-324">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it to Azure.</span><span class="sxs-lookup"><span data-stu-id="c75e3-324">You just built your first ASP.NET MVC web application using Azure Cosmos DB and published it to Azure.</span></span> <span data-ttu-id="c75e3-325">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="c75e3-325">The source code for the complete application, including the detail and delete functionality that were not included in this tutorial can be downloaded or cloned from [GitHub][GitHub].</span></span> <span data-ttu-id="c75e3-326">So if you're interested in adding that to your app, grab the code and add it to this app.</span><span class="sxs-lookup"><span data-stu-id="c75e3-326">So if you're interested in adding that to your app, grab the code and add it to this app.</span></span>

<span data-ttu-id="c75e3-327">To add additional functionality to your application, review the APIs available in the [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free to contribute to the Azure Cosmos DB .NET Library on [GitHub][GitHub].</span><span class="sxs-lookup"><span data-stu-id="c75e3-327">To add additional functionality to your application, review the APIs available in the [Azure Cosmos DB .NET Library](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet) and feel free to contribute to the Azure Cosmos DB .NET Library on [GitHub][GitHub].</span></span> 

[\*]: https://microsoft.sharepoint.com/teams/DocDB/Shared%20Documents/Documentation/Docs.LatestVersions/PicExportError
[Visual Studio Express]: http://www.visualstudio.com/products/visual-studio-express-vs.aspx
[Microsoft Web Platform Installer]: http://www.microsoft.com/web/downloads/platform.aspx
[Preventing Cross-Site Request Forgery]: http://go.microsoft.com/fwlink/?LinkID=517254
[Basic CRUD Operations in ASP.NET MVC]: http://go.microsoft.com/fwlink/?LinkId=317598
[GitHub]: https://github.com/Azure-Samples/documentdb-net-todo-app
