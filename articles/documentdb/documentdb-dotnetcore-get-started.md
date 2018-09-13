---
title: 'NoSQL tutorial: DocumentDB .NET Core SDK | Microsoft Docs'
description: A NoSQL tutorial that creates an online database and C# console application using the DocumentDB .NET Core SDK. DocumentDB is a NoSQL database for JSON.
services: documentdb
documentationcenter: .net
author: arramac
manager: jhubbard
editor: ''
ms.assetid: 9f93e276-9936-4efb-a534-a9889fa7c7d2
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/28/2017
ms.author: arramac
ms.openlocfilehash: 03ab9dc3b1df6264f437a67683a4aed3d3cbaaff
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549464"
---
# <a name="nosql-tutorial-build-a-documentdb-c-console-application-on-net-core"></a><span data-ttu-id="36634-104">NoSQL tutorial: Build a DocumentDB C# console application on .NET Core</span><span class="sxs-lookup"><span data-stu-id="36634-104">NoSQL tutorial: Build a DocumentDB C# console application on .NET Core</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js for MongoDB](documentdb-mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="36634-111">Welcome to the NoSQL tutorial for the Azure DocumentDB .NET Core SDK!</span><span class="sxs-lookup"><span data-stu-id="36634-111">Welcome to the NoSQL tutorial for the Azure DocumentDB .NET Core SDK!</span></span> <span data-ttu-id="36634-112">After following this tutorial, you'll have a console application that creates and queries DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="36634-112">After following this tutorial, you'll have a console application that creates and queries DocumentDB resources.</span></span>

<span data-ttu-id="36634-113">We'll cover:</span><span class="sxs-lookup"><span data-stu-id="36634-113">We'll cover:</span></span>

* <span data-ttu-id="36634-114">Creating and connecting to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="36634-114">Creating and connecting to a DocumentDB account</span></span>
* <span data-ttu-id="36634-115">Configuring your Visual Studio Solution</span><span class="sxs-lookup"><span data-stu-id="36634-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="36634-116">Creating an online database</span><span class="sxs-lookup"><span data-stu-id="36634-116">Creating an online database</span></span>
* <span data-ttu-id="36634-117">Creating a collection</span><span class="sxs-lookup"><span data-stu-id="36634-117">Creating a collection</span></span>
* <span data-ttu-id="36634-118">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="36634-118">Creating JSON documents</span></span>
* <span data-ttu-id="36634-119">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="36634-119">Querying the collection</span></span>
* <span data-ttu-id="36634-120">Replacing a document</span><span class="sxs-lookup"><span data-stu-id="36634-120">Replacing a document</span></span>
* <span data-ttu-id="36634-121">Deleting a document</span><span class="sxs-lookup"><span data-stu-id="36634-121">Deleting a document</span></span>
* <span data-ttu-id="36634-122">Deleting the database</span><span class="sxs-lookup"><span data-stu-id="36634-122">Deleting the database</span></span>

<span data-ttu-id="36634-123">Don't have time?</span><span class="sxs-lookup"><span data-stu-id="36634-123">Don't have time?</span></span> <span data-ttu-id="36634-124">Don't worry!</span><span class="sxs-lookup"><span data-stu-id="36634-124">Don't worry!</span></span> <span data-ttu-id="36634-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="36634-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span> <span data-ttu-id="36634-126">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span><span class="sxs-lookup"><span data-stu-id="36634-126">Jump to the [Get the complete solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="36634-127">Want to build a Xamarin iOS, Android, or Forms application using the DocumentDB .NET Core SDK?</span><span class="sxs-lookup"><span data-stu-id="36634-127">Want to build a Xamarin iOS, Android, or Forms application using the DocumentDB .NET Core SDK?</span></span> <span data-ttu-id="36634-128">See [Developing Xamarin mobile applications using DocumentDB](documentdb-mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="36634-128">See [Developing Xamarin mobile applications using DocumentDB](documentdb-mobile-apps-with-xamarin.md).</span></span>

<span data-ttu-id="36634-129">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span><span class="sxs-lookup"><span data-stu-id="36634-129">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span></span> <span data-ttu-id="36634-130">If you'd like us to contact you directly, feel free to include your email address in your comments.</span><span class="sxs-lookup"><span data-stu-id="36634-130">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

> [!NOTE]
> The DocumentDB .NET Core SDK used in this tutorial is not yet compatible with Universal Windows Platform (UWP) apps. For a preview version of the .NET Core SDK that does support UWP apps, send email to [askdocdb@microsoft.com](mailto:askdocdb@microsoft.com).

<span data-ttu-id="36634-133">Now let's get started!</span><span class="sxs-lookup"><span data-stu-id="36634-133">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="36634-134">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="36634-134">Prerequisites</span></span>
<span data-ttu-id="36634-135">Please make sure you have the following:</span><span class="sxs-lookup"><span data-stu-id="36634-135">Please make sure you have the following:</span></span>

* <span data-ttu-id="36634-136">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="36634-136">An active Azure account.</span></span> <span data-ttu-id="36634-137">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="36634-137">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="36634-138">Alternatively, you can use the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="36634-138">Alternatively, you can use the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) for this tutorial.</span></span>
* [<span data-ttu-id="36634-139">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="36634-139">Visual Studio 2017</span></span>](https://www.visualstudio.com/vs/) 
    * <span data-ttu-id="36634-140">If you're working on MacOS or Linux, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span><span class="sxs-lookup"><span data-stu-id="36634-140">If you're working on MacOS or Linux, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#macos) for the platform of your choice.</span></span> 
    * <span data-ttu-id="36634-141">If you're working on Windows, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span><span class="sxs-lookup"><span data-stu-id="36634-141">If you're working on Windows, you can develop .NET Core apps from the command-line by installing the [.NET Core SDK](https://www.microsoft.com/net/core#windows).</span></span> 
    * <span data-ttu-id="36634-142">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span><span class="sxs-lookup"><span data-stu-id="36634-142">You can use your own editor, or download [Visual Studio Code](https://code.visualstudio.com/) which is free and works on Windows, Linux, and MacOS.</span></span> 

## <a name="step-1-create-a-documentdb-account"></a><span data-ttu-id="36634-143">Step 1: Create a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="36634-143">Step 1: Create a DocumentDB account</span></span>
<span data-ttu-id="36634-144">Let's create a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="36634-144">Let's create a DocumentDB account.</span></span> <span data-ttu-id="36634-145">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="36634-145">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="36634-146">If you are using the DocumentDB Emulator, please follow the steps at [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="36634-146">If you are using the DocumentDB Emulator, please follow the steps at [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [documentdb-create-dbaccount](../../includes/documentdb-create-dbaccount.md)]

## <a id="SetupVS"></a><span data-ttu-id="36634-147">Step 2: Setup your Visual Studio solution</span><span class="sxs-lookup"><span data-stu-id="36634-147">Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="36634-148">Open **Visual Studio 2017** on your computer.</span><span class="sxs-lookup"><span data-stu-id="36634-148">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="36634-149">On the **File** menu, select **New**, and then choose **Project**.</span><span class="sxs-lookup"><span data-stu-id="36634-149">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="36634-150">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="36634-150">In the **New Project** dialog, select **Templates** / **Visual C#** / **.NET Core**/**Console Application (.NET Core)**, name your project **DocumentDBGettingStarted**, and then click **OK**.</span></span>

   ![Screen shot of the New Project window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnetcore-get-started/nosql-tutorial-new-project-2.png)
4. <span data-ttu-id="36634-152">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span><span class="sxs-lookup"><span data-stu-id="36634-152">In the **Solution Explorer**, right click on **DocumentDBGettingStarted**.</span></span>
5. <span data-ttu-id="36634-153">Then without leaving the menu, click on **Manage NuGet Packages...**.</span><span class="sxs-lookup"><span data-stu-id="36634-153">Then without leaving the menu, click on **Manage NuGet Packages...**.</span></span>

   ![Screen shot of the Right Clicked Menu for the Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnetcore-get-started/nosql-tutorial-manage-nuget-pacakges.png)
6. <span data-ttu-id="36634-155">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span><span class="sxs-lookup"><span data-stu-id="36634-155">In the **NuGet** tab, click **Browse** at the top of the window, and type **azure documentdb** in the search box.</span></span>
7. <span data-ttu-id="36634-156">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="36634-156">Within the results, find **Microsoft.Azure.DocumentDB.Core** and click **Install**.</span></span>
   <span data-ttu-id="36634-157">The package ID for the DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span><span class="sxs-lookup"><span data-stu-id="36634-157">The package ID for the DocumentDB Client Library for .NET Core is [Microsoft.Azure.DocumentDB.Core](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB.Core).</span></span> <span data-ttu-id="36634-158">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="36634-158">If you are targeting a .NET Framework version (like net461) that is not supported by this .NET Core NuGet package, then use [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB) that supports all .NET Framework versions starting .NET Framework 4.5.</span></span>
8. <span data-ttu-id="36634-159">At the prompts, accept the NuGet package installations and the license agreement.</span><span class="sxs-lookup"><span data-stu-id="36634-159">At the prompts, accept the NuGet package installations and the license agreement.</span></span>

<span data-ttu-id="36634-160">Great!</span><span class="sxs-lookup"><span data-stu-id="36634-160">Great!</span></span> <span data-ttu-id="36634-161">Now that we finished the setup, let's start writing some code.</span><span class="sxs-lookup"><span data-stu-id="36634-161">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="36634-162">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span><span class="sxs-lookup"><span data-stu-id="36634-162">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started).</span></span>

## <a id="Connect"></a><span data-ttu-id="36634-163">Step 3: Connect to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="36634-163">Step 3: Connect to a DocumentDB account</span></span>
<span data-ttu-id="36634-164">First, add these references to the beginning of your C# application, in the Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="36634-164">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

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
> In order to complete this NoSQL tutorial, make sure you add the dependencies above.

<span data-ttu-id="36634-166">Now, add these two constants and your *client* variable underneath your public class *Program*.</span><span class="sxs-lookup"><span data-stu-id="36634-166">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

```csharp
class Program
{
    // ADD THIS PART TO YOUR CODE
    private const string EndpointUri = "<your endpoint URI>";
    private const string PrimaryKey = "<your key>";
    private DocumentClient client;
```

<span data-ttu-id="36634-167">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span><span class="sxs-lookup"><span data-stu-id="36634-167">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span></span> <span data-ttu-id="36634-168">The DocumentDB URI and primary key are necessary for your application to understand where to connect to, and for DocumentDB to trust your application's connection.</span><span class="sxs-lookup"><span data-stu-id="36634-168">The DocumentDB URI and primary key are necessary for your application to understand where to connect to, and for DocumentDB to trust your application's connection.</span></span>

<span data-ttu-id="36634-169">In the Azure Portal, navigate to your DocumentDB account, and then click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="36634-169">In the Azure Portal, navigate to your DocumentDB account, and then click **Keys**.</span></span>

<span data-ttu-id="36634-170">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span><span class="sxs-lookup"><span data-stu-id="36634-170">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span></span> <span data-ttu-id="36634-171">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="36634-171">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span> <span data-ttu-id="36634-172">If you are using the Azure DocumentDB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the DocumentDB Emulator](documentdb-nosql-local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="36634-172">If you are using the Azure DocumentDB Emulator, use `https://localhost:8081` as the endpoint, and the well-defined authorization key from [How to develop using the DocumentDB Emulator](documentdb-nosql-local-emulator.md).</span></span> <span data-ttu-id="36634-173">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span><span class="sxs-lookup"><span data-stu-id="36634-173">Make sure to remove the < and > but leave the double quotes around your endpoint and key.</span></span>

![Screen shot of the Azure Portal used by the NoSQL tutorial to create a C# console application.][keys]

<span data-ttu-id="36634-176">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="36634-176">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="36634-177">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="36634-177">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

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

<span data-ttu-id="36634-178">Add the following code to run your asynchronous task from your **Main** method.</span><span class="sxs-lookup"><span data-stu-id="36634-178">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="36634-179">The **Main** method will catch exceptions and write them to the console.</span><span class="sxs-lookup"><span data-stu-id="36634-179">The **Main** method will catch exceptions and write them to the console.</span></span>

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

<span data-ttu-id="36634-180">Press the **DocumentDBGettingStarted** button to build and run the application.</span><span class="sxs-lookup"><span data-stu-id="36634-180">Press the **DocumentDBGettingStarted** button to build and run the application.</span></span>

<span data-ttu-id="36634-181">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="36634-181">Congratulations!</span></span> <span data-ttu-id="36634-182">You have successfully connected to a DocumentDB account, let's now take a look at working with DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="36634-182">You have successfully connected to a DocumentDB account, let's now take a look at working with DocumentDB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="36634-183">Step 4: Create a database</span><span class="sxs-lookup"><span data-stu-id="36634-183">Step 4: Create a database</span></span>
<span data-ttu-id="36634-184">Before you add the code for creating a database, add a helper method for writing to the console.</span><span class="sxs-lookup"><span data-stu-id="36634-184">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="36634-185">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span><span class="sxs-lookup"><span data-stu-id="36634-185">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
{
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
}
```

<span data-ttu-id="36634-186">Your DocumentDB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="36634-186">Your DocumentDB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="36634-187">A database is the logical container of JSON document storage partitioned across collections.</span><span class="sxs-lookup"><span data-stu-id="36634-187">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="36634-188">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span><span class="sxs-lookup"><span data-stu-id="36634-188">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span></span> <span data-ttu-id="36634-189">This will create a database named *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="36634-189">This will create a database named *FamilyDB*.</span></span>

```csharp
private async Task GetStartedDemo()
{
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB_oa" });
```

<span data-ttu-id="36634-190">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="36634-190">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="36634-191">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="36634-191">Congratulations!</span></span> <span data-ttu-id="36634-192">You have successfully created a DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="36634-192">You have successfully created a DocumentDB database.</span></span>  

## <a id="CreateColl"></a><span data-ttu-id="36634-193">Step 5: Create a collection</span><span class="sxs-lookup"><span data-stu-id="36634-193">Step 5: Create a collection</span></span>
> [!WARNING]
> **CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications. For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).

<span data-ttu-id="36634-196">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="36634-196">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="36634-197">A collection is a container of JSON documents and associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="36634-197">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="36634-198">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span><span class="sxs-lookup"><span data-stu-id="36634-198">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span></span> <span data-ttu-id="36634-199">This will create a document collection named *FamilyCollection_oa*.</span><span class="sxs-lookup"><span data-stu-id="36634-199">This will create a document collection named *FamilyCollection_oa*.</span></span>

```csharp
    this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

    await this.CreateDatabaseIfNotExists("FamilyDB_oa");

    // ADD THIS PART TO YOUR CODE
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"), new DocumentCollection { Id = "FamilyCollection_oa" });
```

<span data-ttu-id="36634-200">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="36634-200">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="36634-201">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="36634-201">Congratulations!</span></span> <span data-ttu-id="36634-202">You have successfully created a DocumentDB document collection.</span><span class="sxs-lookup"><span data-stu-id="36634-202">You have successfully created a DocumentDB document collection.</span></span>  

## <a id="CreateDoc"></a><span data-ttu-id="36634-203">Step 6: Create JSON documents</span><span class="sxs-lookup"><span data-stu-id="36634-203">Step 6: Create JSON documents</span></span>
<span data-ttu-id="36634-204">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="36634-204">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="36634-205">Documents are user defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="36634-205">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="36634-206">We can now insert one or more documents.</span><span class="sxs-lookup"><span data-stu-id="36634-206">We can now insert one or more documents.</span></span> <span data-ttu-id="36634-207">If you already have data you'd like to store in your database, you can use DocumentDB's [Data Migration tool](documentdb-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="36634-207">If you already have data you'd like to store in your database, you can use DocumentDB's [Data Migration tool](documentdb-import-data.md).</span></span>

<span data-ttu-id="36634-208">First, we need to create a **Family** class that will represent objects stored within DocumentDB in this sample.</span><span class="sxs-lookup"><span data-stu-id="36634-208">First, we need to create a **Family** class that will represent objects stored within DocumentDB in this sample.</span></span> <span data-ttu-id="36634-209">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span><span class="sxs-lookup"><span data-stu-id="36634-209">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="36634-210">Note that documents must have an **Id** property serialized as **id** in JSON.</span><span class="sxs-lookup"><span data-stu-id="36634-210">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="36634-211">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span><span class="sxs-lookup"><span data-stu-id="36634-211">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="36634-212">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span><span class="sxs-lookup"><span data-stu-id="36634-212">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="36634-213">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span><span class="sxs-lookup"><span data-stu-id="36634-213">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

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

<span data-ttu-id="36634-214">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span><span class="sxs-lookup"><span data-stu-id="36634-214">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="36634-215">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span><span class="sxs-lookup"><span data-stu-id="36634-215">Copy and paste the code that follows `// ADD THIS PART TO YOUR CODE` to your **GetStartedDemo** method underneath the document collection creation.</span></span>

```csharp
await this.CreateDatabaseIfNotExists("FamilyDB_oa");

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

<span data-ttu-id="36634-216">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="36634-216">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="36634-217">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="36634-217">Congratulations!</span></span> <span data-ttu-id="36634-218">You have successfully created two DocumentDB documents.</span><span class="sxs-lookup"><span data-stu-id="36634-218">You have successfully created two DocumentDB documents.</span></span>  

![Diagram illustrating the hierarchical relationship between the account, the online database, the collection, and the documents used by the NoSQL tutorial to create a C# console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnetcore-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a><span data-ttu-id="36634-220">Step 7: Query DocumentDB resources</span><span class="sxs-lookup"><span data-stu-id="36634-220">Step 7: Query DocumentDB resources</span></span>
<span data-ttu-id="36634-221">DocumentDB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="36634-221">DocumentDB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="36634-222">The following sample code shows various queries - using both DocumentDB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span><span class="sxs-lookup"><span data-stu-id="36634-222">The following sample code shows various queries - using both DocumentDB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="36634-223">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span><span class="sxs-lookup"><span data-stu-id="36634-223">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="36634-224">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span><span class="sxs-lookup"><span data-stu-id="36634-224">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

// ADD THIS PART TO YOUR CODE
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="36634-225">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="36634-225">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="36634-226">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="36634-226">Congratulations!</span></span> <span data-ttu-id="36634-227">You have successfully queried against a DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="36634-227">You have successfully queried against a DocumentDB collection.</span></span>

<span data-ttu-id="36634-228">The following diagram illustrates how the DocumentDB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span><span class="sxs-lookup"><span data-stu-id="36634-228">The following diagram illustrates how the DocumentDB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagram illustrating the scope and meaning of the query used by the NoSQL tutorial to create a C# console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnetcore-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="36634-230">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because DocumentDB queries are already scoped to a single collection.</span><span class="sxs-lookup"><span data-stu-id="36634-230">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because DocumentDB queries are already scoped to a single collection.</span></span> <span data-ttu-id="36634-231">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span><span class="sxs-lookup"><span data-stu-id="36634-231">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="36634-232">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span><span class="sxs-lookup"><span data-stu-id="36634-232">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <a id="ReplaceDocument"></a><span data-ttu-id="36634-233">Step 8: Replace JSON document</span><span class="sxs-lookup"><span data-stu-id="36634-233">Step 8: Replace JSON document</span></span>
<span data-ttu-id="36634-234">DocumentDB supports replacing JSON documents.</span><span class="sxs-lookup"><span data-stu-id="36634-234">DocumentDB supports replacing JSON documents.</span></span>  

<span data-ttu-id="36634-235">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span><span class="sxs-lookup"><span data-stu-id="36634-235">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
{
    try
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
        this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="36634-236">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span><span class="sxs-lookup"><span data-stu-id="36634-236">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span></span> <span data-ttu-id="36634-237">After replacing the document, this will run the same query again to view the changed document.</span><span class="sxs-lookup"><span data-stu-id="36634-237">After replacing the document, this will run the same query again to view the changed document.</span></span>

```csharp
await this.CreateFamilyDocumentIfNotExists("FamilyDB_oa", "FamilyCollection_oa", wakefieldFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO YOUR CODE
// Update the Grade of the Andersen Family child
andersenFamily.Children[0].Grade = 6;

await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");
```

<span data-ttu-id="36634-238">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="36634-238">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="36634-239">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="36634-239">Congratulations!</span></span> <span data-ttu-id="36634-240">You have successfully replaced a DocumentDB document.</span><span class="sxs-lookup"><span data-stu-id="36634-240">You have successfully replaced a DocumentDB document.</span></span>

## <a id="DeleteDocument"></a><span data-ttu-id="36634-241">Step 9: Delete JSON document</span><span class="sxs-lookup"><span data-stu-id="36634-241">Step 9: Delete JSON document</span></span>
<span data-ttu-id="36634-242">DocumentDB supports deleting JSON documents.</span><span class="sxs-lookup"><span data-stu-id="36634-242">DocumentDB supports deleting JSON documents.</span></span>  

<span data-ttu-id="36634-243">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span><span class="sxs-lookup"><span data-stu-id="36634-243">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

```csharp
// ADD THIS PART TO YOUR CODE
private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
{
    try
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
        Console.WriteLine("Deleted Family {0}", documentName);
    }
    catch (DocumentClientException de)
    {
        throw;
    }
}
```

<span data-ttu-id="36634-244">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span><span class="sxs-lookup"><span data-stu-id="36634-244">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span></span>

```cshrp
await this.ReplaceFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1", andersenFamily);

this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

// ADD THIS PART TO CODE
await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");
```

<span data-ttu-id="36634-245">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="36634-245">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="36634-246">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="36634-246">Congratulations!</span></span> <span data-ttu-id="36634-247">You have successfully deleted a DocumentDB document.</span><span class="sxs-lookup"><span data-stu-id="36634-247">You have successfully deleted a DocumentDB document.</span></span>

## <a id="DeleteDatabase"></a><span data-ttu-id="36634-248">Step 10: Delete the database</span><span class="sxs-lookup"><span data-stu-id="36634-248">Step 10: Delete the database</span></span>
<span data-ttu-id="36634-249">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="36634-249">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="36634-250">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span><span class="sxs-lookup"><span data-stu-id="36634-250">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span></span>

```csharp
this.ExecuteSimpleQuery("FamilyDB_oa", "FamilyCollection_oa");

await this.DeleteFamilyDocument("FamilyDB_oa", "FamilyCollection_oa", "Andersen.1");

// ADD THIS PART TO CODE
// Clean up/delete the database
await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_oa"));
```

<span data-ttu-id="36634-251">Press the **DocumentDBGettingStarted** button to run your application.</span><span class="sxs-lookup"><span data-stu-id="36634-251">Press the **DocumentDBGettingStarted** button to run your application.</span></span>

<span data-ttu-id="36634-252">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="36634-252">Congratulations!</span></span> <span data-ttu-id="36634-253">You have successfully deleted a DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="36634-253">You have successfully deleted a DocumentDB database.</span></span>

## <a id="Run"></a><span data-ttu-id="36634-254">Step 11: Run your C# console application all together!</span><span class="sxs-lookup"><span data-stu-id="36634-254">Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="36634-255">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span><span class="sxs-lookup"><span data-stu-id="36634-255">Press the **DocumentDBGettingStarted** button in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="36634-256">You should see the output of your get started app.</span><span class="sxs-lookup"><span data-stu-id="36634-256">You should see the output of your get started app.</span></span> <span data-ttu-id="36634-257">The output will show the results of the queries we added and should match the example text below.</span><span class="sxs-lookup"><span data-stu-id="36634-257">The output will show the results of the queries we added and should match the example text below.</span></span>

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

<span data-ttu-id="36634-258">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="36634-258">Congratulations!</span></span> <span data-ttu-id="36634-259">You've completed this NoSQL tutorial and have a working C# console application!</span><span class="sxs-lookup"><span data-stu-id="36634-259">You've completed this NoSQL tutorial and have a working C# console application!</span></span>

## <a id="GetSolution"></a> <span data-ttu-id="36634-260">Get the complete NoSQL tutorial solution</span><span class="sxs-lookup"><span data-stu-id="36634-260">Get the complete NoSQL tutorial solution</span></span>
<span data-ttu-id="36634-261">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="36634-261">To build the GetStarted solution that contains all the samples in this article, you will need the following:</span></span>

* <span data-ttu-id="36634-262">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="36634-262">An active Azure account.</span></span> <span data-ttu-id="36634-263">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="36634-263">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="36634-264">A [DocumentDB account][documentdb-create-account].</span><span class="sxs-lookup"><span data-stu-id="36634-264">A [DocumentDB account][documentdb-create-account].</span></span>
* <span data-ttu-id="36634-265">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="36634-265">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-core-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="36634-266">To restore the references to the DocumentDB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span><span class="sxs-lookup"><span data-stu-id="36634-266">To restore the references to the DocumentDB .NET Core SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="36634-267">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to a DocumentDB account](#Connect).</span><span class="sxs-lookup"><span data-stu-id="36634-267">Next, in the Program.cs file, update the EndpointUrl and AuthorizationKey values as described in [Connect to a DocumentDB account](#Connect).</span></span>

## <a name="next-steps"></a><span data-ttu-id="36634-268">Next steps</span><span class="sxs-lookup"><span data-stu-id="36634-268">Next steps</span></span>
* <span data-ttu-id="36634-269">Want a more complex ASP.NET MVC NoSQL tutorial?</span><span class="sxs-lookup"><span data-stu-id="36634-269">Want a more complex ASP.NET MVC NoSQL tutorial?</span></span> <span data-ttu-id="36634-270">See [Build a web application with ASP.NET MVC using DocumentDB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="36634-270">See [Build a web application with ASP.NET MVC using DocumentDB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="36634-271">Want to develop a Xamarin iOS, Android, or Forms application using the DocumentDB .NET Core SDK?</span><span class="sxs-lookup"><span data-stu-id="36634-271">Want to develop a Xamarin iOS, Android, or Forms application using the DocumentDB .NET Core SDK?</span></span> <span data-ttu-id="36634-272">See [Developing Xamarin mobile applications using DocumentDB](documentdb-mobile-apps-with-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="36634-272">See [Developing Xamarin mobile applications using DocumentDB](documentdb-mobile-apps-with-xamarin.md).</span></span>
* <span data-ttu-id="36634-273">Want to perform scale and performance testing with DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="36634-273">Want to perform scale and performance testing with DocumentDB?</span></span> <span data-ttu-id="36634-274">See [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="36634-274">See [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md)</span></span>
* <span data-ttu-id="36634-275">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="36634-275">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span></span>
* <span data-ttu-id="36634-276">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="36634-276">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="36634-277">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="36634-277">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[documentdb-create-account]: documentdb-create-account.md
[keys]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-dotnetcore-get-started/nosql-tutorial-keys.png





