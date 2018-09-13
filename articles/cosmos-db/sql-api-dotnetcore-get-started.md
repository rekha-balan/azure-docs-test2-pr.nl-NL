---
title: 'Azure Cosmos DB: SQL API getting started with .NET Core tutorial | Microsoft Docs'
description: A tutorial that creates an online database and C# console application using the Azure Cosmos DB SQL API .NET Core SDK.
services: cosmos-db
author: SnehaGunda
manager: kfile
editor: ''
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: dotnet
ms.topic: tutorial
ms.date: 03/12/2018
ms.author: sngun
ms.custom: devcenter
ms.openlocfilehash: d433eeb7d63282868b8919ee8c53283080bf8b59
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868439"
---
# <a name="azure-cosmos-db-getting-started-with-the-sql-api-and-net-core"></a><span data-ttu-id="7a533-103">Azure Cosmos DB: Getting started with the SQL API and .NET Core</span><span class="sxs-lookup"><span data-stu-id="7a533-103">Azure Cosmos DB: Getting started with the SQL API and .NET Core</span></span>

> [!div class="op_single_selector"]
> * [.NET](sql-api-get-started.md)
> * [.NET Core](sql-api-dotnetcore-get-started.md)
> * [Java](sql-api-java-get-started.md)
> * [Async Java](sql-api-async-java-get-started.md)
> * [Node.js](sql-api-nodejs-get-started.md)
> * [Node.js- v2](sql-api-nodejs-get-started-preview.md) 
> 

<span data-ttu-id="7a533-110">Welcome to the SQL API for Azure Cosmos DB getting started with .NET Core tutorial!</span><span class="sxs-lookup"><span data-stu-id="7a533-110">Welcome to the SQL API for Azure Cosmos DB getting started with .NET Core tutorial!</span></span> <span data-ttu-id="7a533-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="7a533-111">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="7a533-112">This tutorial covers:</span><span class="sxs-lookup"><span data-stu-id="7a533-112">This tutorial covers:</span></span>

* <span data-ttu-id="7a533-113">Creating and connecting to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="7a533-113">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="7a533-114">Configuring your Visual Studio Solution</span><span class="sxs-lookup"><span data-stu-id="7a533-114">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="7a533-115">Creating an online database</span><span class="sxs-lookup"><span data-stu-id="7a533-115">Creating an online database</span></span>
* <span data-ttu-id="7a533-116">Creating a collection</span><span class="sxs-lookup"><span data-stu-id="7a533-116">Creating a collection</span></span>
* <span data-ttu-id="7a533-117">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="7a533-117">Creating JSON documents</span></span>
* <span data-ttu-id="7a533-118">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="7a533-118">Querying the collection</span></span>
* <span data-ttu-id="7a533-119">Replacing a document</span><span class="sxs-lookup"><span data-stu-id="7a533-119">Replacing a document</span></span>
* <span data-ttu-id="7a533-120">Deleting a document</span><span class="sxs-lookup"><span data-stu-id="7a533-120">Deleting a document</span></span>
* <span data-ttu-id="7a533-121">Deleting the database</span><span class="sxs-lookup"><span data-stu-id="7a533-121">Deleting the database</span></span>

<span data-ttu-id="7a533-122">Don't have time?</span><span class="sxs-lookup"><span data-stu-id="7a533-122">Don't have time?</span></span> <span data-ttu-id="7a533-123">Don't worry!</span><span class="sxs-lookup"><span data-stu-id="7a533-123">Don't worry!</span></span> <span data-ttu-id="7a533-124">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="7a533-124">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="7a533-125">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span><span class="sxs-lookup"><span data-stu-id="7a533-125">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="7a533-126">Want to build a Xamarin iOS, Android, or Forms application using the SQL API and .NET Core SDK?</span><span class="sxs-lookup"><span data-stu-id="7a533-126">Want to build a Xamarin iOS, Android, or Forms application using the SQL API and .NET Core SDK?</span></span> <span data-ttu-id="7a533-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="7a533-127">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>

<span data-ttu-id="7a533-128">Now let's get started!</span><span class="sxs-lookup"><span data-stu-id="7a533-128">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a533-129">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7a533-129">Prerequisites</span></span>

* <span data-ttu-id="7a533-130">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="7a533-130">An active Azure account.</span></span> <span data-ttu-id="7a533-131">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7a533-131">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* <span data-ttu-id="7a533-132">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="7a533-132">If you don’t already have Visual Studio 2017 installed, you can download and use the free [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="7a533-133">If you are developing a Universal Windows Platform (UWP) app, you should use **Visual Studio 2017 with version 15.4** or higher.</span><span class="sxs-lookup"><span data-stu-id="7a533-133">If you are developing a Universal Windows Platform (UWP) app, you should use **Visual Studio 2017 with version 15.4** or higher.</span></span> <span data-ttu-id="7a533-134">Make sure that you enable **Azure development** during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="7a533-134">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>
    * <span data-ttu-id="7a533-135">If you're working on MacOS or Linux, you can develop .NET Core apps from the command line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span><span class="sxs-lookup"><span data-stu-id="7a533-135">If you're working on MacOS or Linux, you can develop .NET Core apps from the command line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span></span> 
    * <span data-ttu-id="7a533-136">If you're working on Windows, you can develop .NET Core apps from the command line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="7a533-136">If you're working on Windows, you can develop .NET Core apps from the command line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="7a533-137">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/), which is free and works on Windows, Linux, and MacOS.</span><span class="sxs-lookup"><span data-stu-id="7a533-137">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/), which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="7a533-138">Step 1: Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="7a533-138">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="7a533-139">Let's create an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="7a533-139">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="7a533-140">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="7a533-140">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="7a533-141">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="7a533-141">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a><span data-ttu-id="7a533-142">Step 2: Setup your Visual Studio solution</span><span class="sxs-lookup"><span data-stu-id="7a533-142">Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="7a533-143">Open **Visual Studio 2017** on your computer.</span><span class="sxs-lookup"><span data-stu-id="7a533-143">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="7a533-144">On the **File** menu, select **New**, and then choose **Project**.</span><span class="sxs-lookup"><span data-stu-id="7a533-144">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="7a533-145">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a533-145">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Screen shot of the New Project window](./media/sql-api-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="7a533-147">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="7a533-147">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="7a533-148">Then without leaving the menu, click on **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="7a533-148">Then without leaving the menu, click on **Manage NuGet Packages...**.</span></span>

   ![Screen shot of the Right Clicked Menu for the Project](./media/sql-api-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="7a533-150">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span><span class="sxs-lookup"><span data-stu-id="7a533-150">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span></span>
7. <span data-ttu-id="7a533-151">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="7a533-151">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="7a533-152">The package ID for the library is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="7a533-152">The package ID for the library is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="7a533-153">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="7a533-153">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="7a533-154">At the prompts, accept the NuGet package installations and the license agreement.</span><span class="sxs-lookup"><span data-stu-id="7a533-154">At the prompts, accept the NuGet package installations and the license agreement.</span></span>

<span data-ttu-id="7a533-155">Great!</span><span class="sxs-lookup"><span data-stu-id="7a533-155">Great!</span></span> <span data-ttu-id="7a533-156">Now that setup is complete, let's start writing some code.</span><span class="sxs-lookup"><span data-stu-id="7a533-156">Now that setup is complete, let's start writing some code.</span></span> <span data-ttu-id="7a533-157">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="7a533-157">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <a id="Connect"></a><span data-ttu-id="7a533-158">Step 3: Connect to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="7a533-158">Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="7a533-159">First, add these references to the beginning of your C# application, in the Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="7a533-159">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

```csharp
using System;

// ADD THIS PART TO YOUR CODE
using System.Linq;
using System.Threading.Tasks;
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

> [!IMPORTANT]
> In order to complete this tutorial, make sure you add the dependencies above.

<span data-ttu-id="7a533-161">Now, add these two constants and your *client* variable underneath your public class *Program*.</span><span class="sxs-lookup"><span data-stu-id="7a533-161">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="7a533-162">Next, head to the [Azure portal](https://portal.azure.com) to retrieve your URI and primary key.</span><span class="sxs-lookup"><span data-stu-id="7a533-162">Next, head to the [Azure portal](https://portal.azure.com) to retrieve your URI and primary key.</span></span> <span data-ttu-id="7a533-163">The Azure Cosmos DB URI and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span><span class="sxs-lookup"><span data-stu-id="7a533-163">The Azure Cosmos DB URI and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="7a533-164">In the Azure portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="7a533-164">In the Azure portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="7a533-165">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span><span class="sxs-lookup"><span data-stu-id="7a533-165">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span></span> <span data-ttu-id="7a533-166">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="7a533-166">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span> <span data-ttu-id="7a533-167">If you are using the Azure Cosmos DB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the Azure Cosmos DB Emulator](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="7a533-167">If you are using the Azure Cosmos DB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="7a533-168">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span><span class="sxs-lookup"><span data-stu-id="7a533-168">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span></span>

![Screen shot of the Azure portal used by the NoSQL tutorial to create a C# console application.][keys]

<span data-ttu-id="7a533-171">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="7a533-171">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="7a533-172">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="7a533-172">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

```csharp
static void Main(string[] args)
{
}

// ADD THIS PART TO YOUR CODE
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
}
```

<span data-ttu-id="7a533-173">Add the following code to run your asynchronous task from your **Main** method.</span><span class="sxs-lookup"><span data-stu-id="7a533-173">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="7a533-174">The **Main** method catches exceptions and write them to the console.</span><span class="sxs-lookup"><span data-stu-id="7a533-174">The **Main** method catches exceptions and write them to the console.</span></span>

```csharp
static void Main(string[] args)
{
        // ADD THIS PART TO YOUR CODE
        try
        {
                Program p = new Program();
                p.GetStartedDemo().Wait();
        }
        catch (DocumentClientException de)
        {
                Exception baseException = de.GetBaseException();
                Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
        }
        catch (Exception e)
        {
                Exception baseException = e.GetBaseException();
                Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
        }
        finally
        {
                Console.WriteLine("End of demo, press any key to exit.");
                Console.ReadKey();
        }
```

<span data-ttu-id="7a533-175">Press the **DocumentDBGettingStarted** button to build and run the application.</span><span class="sxs-lookup"><span data-stu-id="7a533-175">Press the **DocumentDBGettingStarted** button to build and run the application.</span></span>

<span data-ttu-id="7a533-176">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="7a533-176">Congratulations!</span></span> <span data-ttu-id="7a533-177">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="7a533-177">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="7a533-178">Step 4: Create a database</span><span class="sxs-lookup"><span data-stu-id="7a533-178">Step 4: Create a database</span></span>
<span data-ttu-id="7a533-179">Before you add the code for creating a database, add a helper method for writing to the console.</span><span class="sxs-lookup"><span data-stu-id="7a533-179">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="7a533-180">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span><span class="sxs-lookup"><span data-stu-id="7a533-180">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="7a533-181">Your Azure Cosmos DB [database](sql-api-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="7a533-181">Your Azure Cosmos DB [database](sql-api-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="7a533-182">A database is the logical container of JSON document storage partitioned across collections.</span><span class="sxs-lookup"><span data-stu-id="7a533-182">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="7a533-183">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span><span class="sxs-lookup"><span data-stu-id="7a533-183">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span></span> <span data-ttu-id="7a533-184">This creates a database named *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="7a533-184">This creates a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="7a533-185">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="7a533-185">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a533-186">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="7a533-186">Congratulations!</span></span> <span data-ttu-id="7a533-187">You have successfully created an Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="7a533-187">You have successfully created an Azure Cosmos DB database.</span></span>  

## <a id="CreateColl"></a><span data-ttu-id="7a533-188">Step 5: Create a collection</span><span class="sxs-lookup"><span data-stu-id="7a533-188">Step 5: Create a collection</span></span>
> [!WARNING]
> **CreateDocumentCollectionAsync** creates a new collection with reserved throughput, which has pricing implications. For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).

<span data-ttu-id="7a533-191">A [collection](sql-api-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="7a533-191">A [collection](sql-api-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="7a533-192">A collection is a container of JSON documents and associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="7a533-192">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="7a533-193">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span><span class="sxs-lookup"><span data-stu-id="7a533-193">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span></span> <span data-ttu-id="7a533-194">This creates a document collection named *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="7a533-194">This creates a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.client.CreateDatabaseIfNotExistsAsync("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="7a533-195">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="7a533-195">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a533-196">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="7a533-196">Congratulations!</span></span> <span data-ttu-id="7a533-197">You have successfully created an Azure Cosmos DB document collection.</span><span class="sxs-lookup"><span data-stu-id="7a533-197">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <a id="CreateDoc"></a><span data-ttu-id="7a533-198">Step 6: Create JSON documents</span><span class="sxs-lookup"><span data-stu-id="7a533-198">Step 6: Create JSON documents</span></span>
<span data-ttu-id="7a533-199">A [document](sql-api-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="7a533-199">A [document](sql-api-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="7a533-200">Documents are user-defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="7a533-200">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="7a533-201">We can now insert one or more documents.</span><span class="sxs-lookup"><span data-stu-id="7a533-201">We can now insert one or more documents.</span></span> <span data-ttu-id="7a533-202">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span><span class="sxs-lookup"><span data-stu-id="7a533-202">If you already have data you'd like to store in your database, you can use Azure Cosmos DB's [Data Migration tool](import-data.md).</span></span>

<span data-ttu-id="7a533-203">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span><span class="sxs-lookup"><span data-stu-id="7a533-203">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="7a533-204">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span><span class="sxs-lookup"><span data-stu-id="7a533-204">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="7a533-205">Note that documents must have an **Id** property serialized as **id** in JSON.</span><span class="sxs-lookup"><span data-stu-id="7a533-205">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="7a533-206">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span><span class="sxs-lookup"><span data-stu-id="7a533-206">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="7a533-207">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span><span class="sxs-lookup"><span data-stu-id="7a533-207">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

```csharp
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
    Console.WriteLine(format, args);
    Console.WriteLine("Press any key to continue ...");
    Console.ReadKey();
}

// ADD THIS PART TO YOUR CODE
public class Family
{
    [JsonProperty(PropertyName = "id")]
    public string Id { get; set; }
    public string LastName { get; set; }
    public Parent[] Parents { get; set; }
    public Child[] Children { get; set; }
    public Address Address { get; set; }
    public bool IsRegistered { get; set; }
    public override string ToString()
    {
            return JsonConvert.SerializeObject(this);
    }
}

public class Parent
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
}

public class Child
{
    public string FamilyName { get; set; }
    public string FirstName { get; set; }
    public string Gender { get; set; }
    public int Grade { get; set; }
    public Pet[] Pets { get; set; }
}

public class Pet
{
    public string GivenName { get; set; }
}

public class Address
{
    public string State { get; set; }
    public string County { get; set; }
    public string City { get; set; }
}
```

<span data-ttu-id="7a533-208">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span><span class="sxs-lookup"><span data-stu-id="7a533-208">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task CreateFamilyDocumentIfNotExists(string databaseName, string collectionName, Family family)
{
    try
    {
        await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, family.Id));
        this.WriteToConsoleAndPromptToContinue("Found {0}", family.Id);
    }
    catch (DocumentClientException de)
    {
        if (de.StatusCode == HttpStatusCode.NotFound)
        {
            await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), family);
            this.WriteToConsoleAndPromptToContinue("Created Family {0}", family.Id);
        }
        else
        {
            throw;
        }
    }
}
```

<span data-ttu-id="7a533-209">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span><span class="sxs-lookup"><span data-stu-id="7a533-209">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="7a533-210">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span><span class="sxs-lookup"><span data-stu-id="7a533-210">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExistsAsync("FamilyDB_oa");

await this.CreateDocumentCollectionIfNotExists("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
Family andersenFamily = new Family
{
        Id = "Andersen.1",
        LastName = "Andersen",
        Parents = new Parent[]
        {
                new Parent { FirstName = "Thomas" },
                new Parent { FirstName = "Mary Kay" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FirstName = "Henriette Thaulow",
                        Gender = "female",
                        Grade = 5,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Fluffy" }
                        }
                }
        },
        Address = new Address { State = "WA", County = "King", City = "Seattle" },
        IsRegistered = true
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", andersenFamily);

Family wakefieldFamily = new Family
{
        Id = "Wakefield.7",
        LastName = "Wakefield",
        Parents = new Parent[]
        {
                new Parent { FamilyName = "Wakefield", FirstName = "Robin" },
                new Parent { FamilyName = "Miller", FirstName = "Ben" }
        },
        Children = new Child[]
        {
                new Child
                {
                        FamilyName = "Merriam",
                        FirstName = "Jesse",
                        Gender = "female",
                        Grade = 8,
                        Pets = new Pet[]
                        {
                                new Pet { GivenName = "Goofy" },
                                new Pet { GivenName = "Shadow" }
                        }
                },
                new Child
                {
                        FamilyName = "Miller",
                        FirstName = "Lisa",
                        Gender = "female",
                        Grade = 1
                }
        },
        Address = new Address { State = "NY", County = "Manhattan", City = "NY" },
        IsRegistered = false
};

await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);
```

<span data-ttu-id="7a533-211">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="7a533-211">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a533-212">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="7a533-212">Congratulations!</span></span> <span data-ttu-id="7a533-213">You have successfully created two Azure Cosmos DB documents.</span><span class="sxs-lookup"><span data-stu-id="7a533-213">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagram illustrating the hierarchical relationship between the account, the online database, the collection, and the documents used by the NoSQL tutorial to create a C# console application](./media/sql-api-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a><span data-ttu-id="7a533-215">Step 7: Query Azure Cosmos DB resources</span><span class="sxs-lookup"><span data-stu-id="7a533-215">Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="7a533-216">Azure Cosmos DB supports rich [queries](sql-api-sql-query.md) against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="7a533-216">Azure Cosmos DB supports rich [queries](sql-api-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="7a533-217">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span><span class="sxs-lookup"><span data-stu-id="7a533-217">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="7a533-218">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span><span class="sxs-lookup"><span data-stu-id="7a533-218">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void ExecuteSimpleQuery(string databaseName, string collectionName)
{
    // Set some common query options
    FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1 };

        // Here we find the Andersen family via its LastName
        IQueryable<Family> familyQuery = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                .Where(f => f.LastName == "Andersen");

        // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
        Console.WriteLine("Running LINQ query...");
        foreach (Family family in familyQuery)
        {
            Console.WriteLine("\tRead {0}", family);
        }

        // Now execute the same query via direct SQL
        IQueryable<Family> familyQueryInSql = this.client.CreateDocumentQuery<Family>(
                UriFactory.CreateDocumentCollectionUri(databaseName, collectionName),
                "SELECT * FROM Family WHERE Family.LastName = 'Andersen'",
                queryOptions);

        Console.WriteLine("Running direct SQL query...");
        foreach (Family family in familyQueryInSql)
        {
                Console.WriteLine("\tRead {0}", family);
        }

        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="7a533-219">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span><span class="sxs-lookup"><span data-stu-id="7a533-219">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="7a533-220">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="7a533-220">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a533-221">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="7a533-221">Congratulations!</span></span> <span data-ttu-id="7a533-222">You have successfully queried against an Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="7a533-222">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="7a533-223">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span><span class="sxs-lookup"><span data-stu-id="7a533-223">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagram illustrating the scope and meaning of the query used by the NoSQL tutorial to create a C# console application](./media/sql-api-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="7a533-225">The [FROM](sql-api-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span><span class="sxs-lookup"><span data-stu-id="7a533-225">The [FROM](sql-api-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="7a533-226">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span><span class="sxs-lookup"><span data-stu-id="7a533-226">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="7a533-227">Azure Cosmos DB infers the Families, root, or the variable name you chose, reference the current collection by default.</span><span class="sxs-lookup"><span data-stu-id="7a533-227">Azure Cosmos DB infers the Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <a id="ReplaceDocument"></a><span data-ttu-id="7a533-228">Step 8: Replace JSON document</span><span class="sxs-lookup"><span data-stu-id="7a533-228">Step 8: Replace JSON document</span></span>
<span data-ttu-id="7a533-229">Azure Cosmos DB supports replacing JSON documents.</span><span class="sxs-lookup"><span data-stu-id="7a533-229">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="7a533-230">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span><span class="sxs-lookup"><span data-stu-id="7a533-230">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
    this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
}
```

<span data-ttu-id="7a533-231">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span><span class="sxs-lookup"><span data-stu-id="7a533-231">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span></span> <span data-ttu-id="7a533-232">After replacing the document, this will run the same query again to view the changed document.</span><span class="sxs-lookup"><span data-stu-id="7a533-232">After replacing the document, this will run the same query again to view the changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="7a533-233">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="7a533-233">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a533-234">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="7a533-234">Congratulations!</span></span> <span data-ttu-id="7a533-235">You have successfully replaced an Azure Cosmos DB document.</span><span class="sxs-lookup"><span data-stu-id="7a533-235">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <a id="DeleteDocument"></a><span data-ttu-id="7a533-236">Step 9: Delete JSON document</span><span class="sxs-lookup"><span data-stu-id="7a533-236">Step 9: Delete JSON document</span></span>
<span data-ttu-id="7a533-237">Azure Cosmos DB supports deleting JSON documents.</span><span class="sxs-lookup"><span data-stu-id="7a533-237">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="7a533-238">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span><span class="sxs-lookup"><span data-stu-id="7a533-238">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
    Console.WriteLine("Deleted Family {0}", documentName);
}
```

<span data-ttu-id="7a533-239">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span><span class="sxs-lookup"><span data-stu-id="7a533-239">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span></span>

```csharp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="7a533-240">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="7a533-240">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a533-241">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="7a533-241">Congratulations!</span></span> <span data-ttu-id="7a533-242">You have successfully deleted an Azure Cosmos DB document.</span><span class="sxs-lookup"><span data-stu-id="7a533-242">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <a id="DeleteDatabase"></a><span data-ttu-id="7a533-243">Step 10: Delete the database</span><span class="sxs-lookup"><span data-stu-id="7a533-243">Step 10: Delete the database</span></span>
<span data-ttu-id="7a533-244">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="7a533-244">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="7a533-245">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span><span class="sxs-lookup"><span data-stu-id="7a533-245">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="7a533-246">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="7a533-246">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="7a533-247">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="7a533-247">Congratulations!</span></span> <span data-ttu-id="7a533-248">You have successfully deleted an Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="7a533-248">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <a id="Run"></a><span data-ttu-id="7a533-249">Step 11: Run your C# console application all together!</span><span class="sxs-lookup"><span data-stu-id="7a533-249">Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="7a533-250">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span><span class="sxs-lookup"><span data-stu-id="7a533-250">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="7a533-251">You should see the output of your get started app in the console window.</span><span class="sxs-lookup"><span data-stu-id="7a533-251">You should see the output of your get started app in the console window.</span></span> <span data-ttu-id="7a533-252">The output will show the results of the queries we added and should match the example text below.</span><span class="sxs-lookup"><span data-stu-id="7a533-252">The output will show the results of the queries we added and should match the example text below.</span></span>

```
Created FamilyDB_oa
Press any key to continue ...
Created FamilyCollection_oa
Press any key to continue ...
Created Family Andersen.1
Press any key to continue ...
Created Family Wakefield.7
Press any key to continue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":5,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Replaced Family Andersen.1
Press any key to continue ...
Running LINQ query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Running direct SQL query...
    Read {"id":"Andersen.1","LastName":"Andersen","District":"WA5","Parents":[{"FamilyName":null,"FirstName":"Thomas"},{"FamilyName":null,"FirstName":"Mary Kay"}],"Children":[{"FamilyName":null,"FirstName":"Henriette Thaulow","Gender":"female","Grade":6,"Pets":[{"GivenName":"Fluffy"}]}],"Address":{"State":"WA","County":"King","City":"Seattle"},"IsRegistered":true}
Deleted Family Andersen.1
End of demo, press any key to exit.
```

<span data-ttu-id="7a533-253">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="7a533-253">Congratulations!</span></span> <span data-ttu-id="7a533-254">You've completed the tutorial and have a working C# console application!</span><span class="sxs-lookup"><span data-stu-id="7a533-254">You've completed the tutorial and have a working C# console application!</span></span>

## <a id="GetSolution"></a> <span data-ttu-id="7a533-255">Get the complete tutorial solution</span><span class="sxs-lookup"><span data-stu-id="7a533-255">Get the complete tutorial solution</span></span>
<span data-ttu-id="7a533-256">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="7a533-256">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="7a533-257">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="7a533-257">An active Azure account.</span></span> <span data-ttu-id="7a533-258">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="7a533-258">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="7a533-259">An [Azure Cosmos DB account][create-sql-api-dotnet.md#create-account].</span><span class="sxs-lookup"><span data-stu-id="7a533-259">An [Azure Cosmos DB account][create-sql-api-dotnet.md#create-account].</span></span>
* <span data-ttu-id="7a533-260">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="7a533-260">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="7a533-261">To restore the references to the SQL API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span><span class="sxs-lookup"><span data-stu-id="7a533-261">To restore the references to the SQL API for Azure Cosmos DB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="7a533-262">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span><span class="sxs-lookup"><span data-stu-id="7a533-262">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7a533-263">Next steps</span><span class="sxs-lookup"><span data-stu-id="7a533-263">Next steps</span></span>
* <span data-ttu-id="7a533-264">Want a more complex ASP.NET MVC tutorial?</span><span class="sxs-lookup"><span data-stu-id="7a533-264">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="7a533-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](sql-api-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="7a533-265">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](sql-api-dotnet-application.md).</span></span>
* <span data-ttu-id="7a533-266">Want to develop a Xamarin iOS, Android, or Forms application using the SQL API for Azure Cosmos DB .NET Core SDK?</span><span class="sxs-lookup"><span data-stu-id="7a533-266">Want to develop a Xamarin iOS, Android, or Forms application using the SQL API for Azure Cosmos DB .NET Core SDK?</span></span> <span data-ttu-id="7a533-267">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="7a533-267">See [Build mobile applications with Xamarin and Azure Cosmos DB](mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="7a533-268">Want to perform scale and performance testing with Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="7a533-268">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="7a533-269">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="7a533-269">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="7a533-270">Learn how to [Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="7a533-270">Learn how to [Monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="7a533-271">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="7a533-271">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="7a533-272">To learn more about the programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="7a533-272">To learn more about the programming model, see [Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/).</span></span>

[create-sql-api-dotnet.md#create-account]: create-sql-api-dotnet.md#create-account
[keys]: media/sql-api-dotnetcore-get-started/nosql-tutorial-keys.png
