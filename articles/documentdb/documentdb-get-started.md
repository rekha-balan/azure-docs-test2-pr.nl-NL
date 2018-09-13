---
title: 'NoSQL tutorial: DocumentDB .NET SDK | Microsoft Docs'
description: A NoSQL tutorial that creates an online database and C# console application using the DocumentDB .NET SDK. DocumentDB is a NoSQL database for JSON.
keywords: nosql tutorial, online database, c# console application
services: documentdb
documentationcenter: .net
author: AndrewHoh
manager: jhubbard
editor: monicar
ms.assetid: bf08e031-718a-4a2a-89d6-91e12ff8797d
ms.service: documentdb
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/19/2017
ms.author: anhoh
ms.openlocfilehash: d272541b2d5d7ddc645e2d0f1b6d927a8c1cc766
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549282"
---
# <a name="nosql-tutorial-build-a-documentdb-c-console-application"></a><span data-ttu-id="4df73-105">NoSQL tutorial: Build a DocumentDB C# console application</span><span class="sxs-lookup"><span data-stu-id="4df73-105">NoSQL tutorial: Build a DocumentDB C# console application</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [.NET Core](documentdb-dotnetcore-get-started.md)
> * [Node.js for MongoDB](documentdb-mongodb-samples.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> * [Java](documentdb-java-get-started.md)
> * [C++](documentdb-cpp-get-started.md)
>  
> 

<span data-ttu-id="4df73-112">Welcome to the NoSQL tutorial for the Azure DocumentDB .NET SDK!</span><span class="sxs-lookup"><span data-stu-id="4df73-112">Welcome to the NoSQL tutorial for the Azure DocumentDB .NET SDK!</span></span> <span data-ttu-id="4df73-113">After following this tutorial, you'll have a console application that creates and queries DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="4df73-113">After following this tutorial, you'll have a console application that creates and queries DocumentDB resources.</span></span>

<span data-ttu-id="4df73-114">We'll cover:</span><span class="sxs-lookup"><span data-stu-id="4df73-114">We'll cover:</span></span>

* <span data-ttu-id="4df73-115">Creating and connecting to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="4df73-115">Creating and connecting to a DocumentDB account</span></span>
* <span data-ttu-id="4df73-116">Configuring your Visual Studio Solution</span><span class="sxs-lookup"><span data-stu-id="4df73-116">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="4df73-117">Creating an online database</span><span class="sxs-lookup"><span data-stu-id="4df73-117">Creating an online database</span></span>
* <span data-ttu-id="4df73-118">Creating a collection</span><span class="sxs-lookup"><span data-stu-id="4df73-118">Creating a collection</span></span>
* <span data-ttu-id="4df73-119">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="4df73-119">Creating JSON documents</span></span>
* <span data-ttu-id="4df73-120">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="4df73-120">Querying the collection</span></span>
* <span data-ttu-id="4df73-121">Replacing a document</span><span class="sxs-lookup"><span data-stu-id="4df73-121">Replacing a document</span></span>
* <span data-ttu-id="4df73-122">Deleting a document</span><span class="sxs-lookup"><span data-stu-id="4df73-122">Deleting a document</span></span>
* <span data-ttu-id="4df73-123">Deleting the database</span><span class="sxs-lookup"><span data-stu-id="4df73-123">Deleting the database</span></span>

<span data-ttu-id="4df73-124">Don't have time?</span><span class="sxs-lookup"><span data-stu-id="4df73-124">Don't have time?</span></span> <span data-ttu-id="4df73-125">Don't worry!</span><span class="sxs-lookup"><span data-stu-id="4df73-125">Don't worry!</span></span> <span data-ttu-id="4df73-126">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="4df73-126">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="4df73-127">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span><span class="sxs-lookup"><span data-stu-id="4df73-127">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="4df73-128">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span><span class="sxs-lookup"><span data-stu-id="4df73-128">Afterwards, please use the voting buttons at the top or bottom of this page to give us feedback.</span></span> <span data-ttu-id="4df73-129">If you'd like us to contact you directly, feel free to include your email address in your comments.</span><span class="sxs-lookup"><span data-stu-id="4df73-129">If you'd like us to contact you directly, feel free to include your email address in your comments.</span></span>

<span data-ttu-id="4df73-130">Now let's get started!</span><span class="sxs-lookup"><span data-stu-id="4df73-130">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4df73-131">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="4df73-131">Prerequisites</span></span>
<span data-ttu-id="4df73-132">Please make sure you have the following:</span><span class="sxs-lookup"><span data-stu-id="4df73-132">Please make sure you have the following:</span></span>

* <span data-ttu-id="4df73-133">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="4df73-133">An active Azure account.</span></span> <span data-ttu-id="4df73-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4df73-134">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="4df73-135">Alternatively, you can use the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) for this tutorial.</span><span class="sxs-lookup"><span data-stu-id="4df73-135">Alternatively, you can use the [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="4df73-136">[Visual Studio 2013 / Visual Studio 2015](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="4df73-136">[Visual Studio 2013 / Visual Studio 2015](http://www.visualstudio.com/).</span></span>

## <a name="step-1-create-a-documentdb-account"></a><span data-ttu-id="4df73-137">Step 1: Create a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="4df73-137">Step 1: Create a DocumentDB account</span></span>
<span data-ttu-id="4df73-138">Let's create a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="4df73-138">Let's create a DocumentDB account.</span></span> <span data-ttu-id="4df73-139">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="4df73-139">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="4df73-140">If you are using the DocumentDB Emulator, please follow the steps at [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="4df73-140">If you are using the DocumentDB Emulator, please follow the steps at [Azure DocumentDB Emulator](documentdb-nosql-local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [documentdb-create-dbaccount](../../includes/documentdb-create-dbaccount.md)]

## <a id="SetupVS"></a><span data-ttu-id="4df73-141">Step 2: Setup your Visual Studio solution</span><span class="sxs-lookup"><span data-stu-id="4df73-141">Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="4df73-142">Open **Visual Studio 2015** on your computer.</span><span class="sxs-lookup"><span data-stu-id="4df73-142">Open **Visual Studio 2015** on your computer.</span></span>
2. <span data-ttu-id="4df73-143">On the **File** menu, select **New**, and then choose **Project**.</span><span class="sxs-lookup"><span data-stu-id="4df73-143">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="4df73-144">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4df73-144">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="4df73-145">![Screen shot of the New Project window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="4df73-145">![Screen shot of the New Project window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="4df73-146">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span><span class="sxs-lookup"><span data-stu-id="4df73-146">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Screen shot of the Right Clicked Menu for the Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="4df73-148">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span><span class="sxs-lookup"><span data-stu-id="4df73-148">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span></span>
6. <span data-ttu-id="4df73-149">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="4df73-149">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="4df73-150">The package ID for the DocumentDB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="4df73-150">The package ID for the DocumentDB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="4df73-151">![Screen shot of the Nuget Menu for finding DocumentDB Client SDK](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="4df73-151">![Screen shot of the Nuget Menu for finding DocumentDB Client SDK](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="4df73-152">If you get a messages about reviewing changes to the solution, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="4df73-152">If you get a messages about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="4df73-153">If you get a message about license acceptance, click **I accept**.</span><span class="sxs-lookup"><span data-stu-id="4df73-153">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="4df73-154">Great!</span><span class="sxs-lookup"><span data-stu-id="4df73-154">Great!</span></span> <span data-ttu-id="4df73-155">Now that we finished the setup, let's start writing some code.</span><span class="sxs-lookup"><span data-stu-id="4df73-155">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="4df73-156">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="4df73-156">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <a id="Connect"></a><span data-ttu-id="4df73-157">Step 3: Connect to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="4df73-157">Step 3: Connect to a DocumentDB account</span></span>
<span data-ttu-id="4df73-158">First, add these references to the beginning of your C# application, in the Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="4df73-158">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART TO YOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> In order to complete this NoSQL tutorial, make sure you add the dependencies above.
> 
> 

<span data-ttu-id="4df73-160">Now, add these two constants and your *client* variable underneath your public class *Program*.</span><span class="sxs-lookup"><span data-stu-id="4df73-160">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="4df73-161">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span><span class="sxs-lookup"><span data-stu-id="4df73-161">Next, head back to the [Azure Portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="4df73-162">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for DocumentDB to trust your application's connection.</span><span class="sxs-lookup"><span data-stu-id="4df73-162">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for DocumentDB to trust your application's connection.</span></span>

<span data-ttu-id="4df73-163">In the Azure Portal, navigate to your DocumentDB account, and then click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="4df73-163">In the Azure Portal, navigate to your DocumentDB account, and then click **Keys**.</span></span>

<span data-ttu-id="4df73-164">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span><span class="sxs-lookup"><span data-stu-id="4df73-164">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="4df73-165">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="4df73-165">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span></span>

![Screen shot of the Azure Portal used by the NoSQL tutorial to create a C# console application.][keys]

<span data-ttu-id="4df73-168">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="4df73-168">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="4df73-169">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="4df73-169">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="4df73-170">Add the following code to run your asynchronous task from your **Main** method.</span><span class="sxs-lookup"><span data-stu-id="4df73-170">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="4df73-171">The **Main** method will catch exceptions and write them to the console.</span><span class="sxs-lookup"><span data-stu-id="4df73-171">The **Main** method will catch exceptions and write them to the console.</span></span>

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

<span data-ttu-id="4df73-172">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="4df73-172">Press **F5** to run your application.</span></span> <span data-ttu-id="4df73-173">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span><span class="sxs-lookup"><span data-stu-id="4df73-173">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span></span>  <span data-ttu-id="4df73-174">You can then close the console window.</span><span class="sxs-lookup"><span data-stu-id="4df73-174">You can then close the console window.</span></span> 

<span data-ttu-id="4df73-175">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="4df73-175">Congratulations!</span></span> <span data-ttu-id="4df73-176">You have successfully connected to a DocumentDB account, let's now take a look at working with DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="4df73-176">You have successfully connected to a DocumentDB account, let's now take a look at working with DocumentDB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="4df73-177">Step 4: Create a database</span><span class="sxs-lookup"><span data-stu-id="4df73-177">Step 4: Create a database</span></span>
<span data-ttu-id="4df73-178">Before you add the code for creating a database, add a helper method for writing to the console.</span><span class="sxs-lookup"><span data-stu-id="4df73-178">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="4df73-179">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span><span class="sxs-lookup"><span data-stu-id="4df73-179">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="4df73-180">Your DocumentDB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="4df73-180">Your DocumentDB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="4df73-181">A database is the logical container of JSON document storage partitioned across collections.</span><span class="sxs-lookup"><span data-stu-id="4df73-181">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="4df73-182">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span><span class="sxs-lookup"><span data-stu-id="4df73-182">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span></span> <span data-ttu-id="4df73-183">This will create a database named *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="4df73-183">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="4df73-184">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="4df73-184">Press **F5** to run your application.</span></span>

<span data-ttu-id="4df73-185">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="4df73-185">Congratulations!</span></span> <span data-ttu-id="4df73-186">You have successfully created a DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="4df73-186">You have successfully created a DocumentDB database.</span></span>  

## <a id="CreateColl"></a><span data-ttu-id="4df73-187">Step 5: Create a collection</span><span class="sxs-lookup"><span data-stu-id="4df73-187">Step 5: Create a collection</span></span>
> [!WARNING]
> **CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications. For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).
> 
> 

<span data-ttu-id="4df73-190">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="4df73-190">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="4df73-191">A collection is a container of JSON documents and associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="4df73-191">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="4df73-192">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span><span class="sxs-lookup"><span data-stu-id="4df73-192">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span></span> <span data-ttu-id="4df73-193">This will create a document collection named *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="4df73-193">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART TO YOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="4df73-194">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="4df73-194">Press **F5** to run your application.</span></span>

<span data-ttu-id="4df73-195">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="4df73-195">Congratulations!</span></span> <span data-ttu-id="4df73-196">You have successfully created a DocumentDB document collection.</span><span class="sxs-lookup"><span data-stu-id="4df73-196">You have successfully created a DocumentDB document collection.</span></span>  

## <a id="CreateDoc"></a><span data-ttu-id="4df73-197">Step 6: Create JSON documents</span><span class="sxs-lookup"><span data-stu-id="4df73-197">Step 6: Create JSON documents</span></span>
<span data-ttu-id="4df73-198">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="4df73-198">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="4df73-199">Documents are user defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="4df73-199">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="4df73-200">We can now insert one or more documents.</span><span class="sxs-lookup"><span data-stu-id="4df73-200">We can now insert one or more documents.</span></span> <span data-ttu-id="4df73-201">If you already have data you'd like to store in your database, you can use DocumentDB's [Data Migration tool](documentdb-import-data.md) to import the data into a database.</span><span class="sxs-lookup"><span data-stu-id="4df73-201">If you already have data you'd like to store in your database, you can use DocumentDB's [Data Migration tool](documentdb-import-data.md) to import the data into a database.</span></span>

<span data-ttu-id="4df73-202">First, we need to create a **Family** class that will represent objects stored within DocumentDB in this sample.</span><span class="sxs-lookup"><span data-stu-id="4df73-202">First, we need to create a **Family** class that will represent objects stored within DocumentDB in this sample.</span></span> <span data-ttu-id="4df73-203">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span><span class="sxs-lookup"><span data-stu-id="4df73-203">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="4df73-204">Note that documents must have an **Id** property serialized as **id** in JSON.</span><span class="sxs-lookup"><span data-stu-id="4df73-204">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="4df73-205">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span><span class="sxs-lookup"><span data-stu-id="4df73-205">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="4df73-206">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span><span class="sxs-lookup"><span data-stu-id="4df73-206">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="4df73-207">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span><span class="sxs-lookup"><span data-stu-id="4df73-207">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

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

<span data-ttu-id="4df73-208">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span><span class="sxs-lookup"><span data-stu-id="4df73-208">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="4df73-209">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span><span class="sxs-lookup"><span data-stu-id="4df73-209">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span></span>

    await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });
    
    await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });


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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", andersenFamily);

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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

<span data-ttu-id="4df73-210">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="4df73-210">Press **F5** to run your application.</span></span>

<span data-ttu-id="4df73-211">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="4df73-211">Congratulations!</span></span> <span data-ttu-id="4df73-212">You have successfully created two DocumentDB documents.</span><span class="sxs-lookup"><span data-stu-id="4df73-212">You have successfully created two DocumentDB documents.</span></span>  

![Diagram illustrating the hierarchical relationship between the account, the online database, the collection, and the documents used by the NoSQL tutorial to create a C# console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a><span data-ttu-id="4df73-214">Step 7: Query DocumentDB resources</span><span class="sxs-lookup"><span data-stu-id="4df73-214">Step 7: Query DocumentDB resources</span></span>
<span data-ttu-id="4df73-215">DocumentDB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="4df73-215">DocumentDB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="4df73-216">The following sample code shows various queries - using both DocumentDB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span><span class="sxs-lookup"><span data-stu-id="4df73-216">The following sample code shows various queries - using both DocumentDB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="4df73-217">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span><span class="sxs-lookup"><span data-stu-id="4df73-217">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="4df73-218">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span><span class="sxs-lookup"><span data-stu-id="4df73-218">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="4df73-219">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="4df73-219">Press **F5** to run your application.</span></span>

<span data-ttu-id="4df73-220">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="4df73-220">Congratulations!</span></span> <span data-ttu-id="4df73-221">You have successfully queried against a DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="4df73-221">You have successfully queried against a DocumentDB collection.</span></span>

<span data-ttu-id="4df73-222">The following diagram illustrates how the DocumentDB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span><span class="sxs-lookup"><span data-stu-id="4df73-222">The following diagram illustrates how the DocumentDB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagram illustrating the scope and meaning of the query used by the NoSQL tutorial to create a C# console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="4df73-224">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because DocumentDB queries are already scoped to a single collection.</span><span class="sxs-lookup"><span data-stu-id="4df73-224">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because DocumentDB queries are already scoped to a single collection.</span></span> <span data-ttu-id="4df73-225">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span><span class="sxs-lookup"><span data-stu-id="4df73-225">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="4df73-226">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span><span class="sxs-lookup"><span data-stu-id="4df73-226">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <a id="ReplaceDocument"></a><span data-ttu-id="4df73-227">Step 8: Replace JSON document</span><span class="sxs-lookup"><span data-stu-id="4df73-227">Step 8: Replace JSON document</span></span>
<span data-ttu-id="4df73-228">DocumentDB supports replacing JSON documents.</span><span class="sxs-lookup"><span data-stu-id="4df73-228">DocumentDB supports replacing JSON documents.</span></span>  

<span data-ttu-id="4df73-229">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span><span class="sxs-lookup"><span data-stu-id="4df73-229">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="4df73-230">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span><span class="sxs-lookup"><span data-stu-id="4df73-230">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span></span> <span data-ttu-id="4df73-231">After replacing the document, this will run the same query again to view the changed document.</span><span class="sxs-lookup"><span data-stu-id="4df73-231">After replacing the document, this will run the same query again to view the changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="4df73-232">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="4df73-232">Press **F5** to run your application.</span></span>

<span data-ttu-id="4df73-233">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="4df73-233">Congratulations!</span></span> <span data-ttu-id="4df73-234">You have successfully replaced a DocumentDB document.</span><span class="sxs-lookup"><span data-stu-id="4df73-234">You have successfully replaced a DocumentDB document.</span></span>

## <a id="DeleteDocument"></a><span data-ttu-id="4df73-235">Step 9: Delete JSON document</span><span class="sxs-lookup"><span data-stu-id="4df73-235">Step 9: Delete JSON document</span></span>
<span data-ttu-id="4df73-236">DocumentDB supports deleting JSON documents.</span><span class="sxs-lookup"><span data-stu-id="4df73-236">DocumentDB supports deleting JSON documents.</span></span>  

<span data-ttu-id="4df73-237">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span><span class="sxs-lookup"><span data-stu-id="4df73-237">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="4df73-238">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span><span class="sxs-lookup"><span data-stu-id="4df73-238">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="4df73-239">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="4df73-239">Press **F5** to run your application.</span></span>

<span data-ttu-id="4df73-240">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="4df73-240">Congratulations!</span></span> <span data-ttu-id="4df73-241">You have successfully deleted a DocumentDB document.</span><span class="sxs-lookup"><span data-stu-id="4df73-241">You have successfully deleted a DocumentDB document.</span></span>

## <a id="DeleteDatabase"></a><span data-ttu-id="4df73-242">Step 10: Delete the database</span><span class="sxs-lookup"><span data-stu-id="4df73-242">Step 10: Delete the database</span></span>
<span data-ttu-id="4df73-243">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="4df73-243">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="4df73-244">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span><span class="sxs-lookup"><span data-stu-id="4df73-244">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="4df73-245">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="4df73-245">Press **F5** to run your application.</span></span>

<span data-ttu-id="4df73-246">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="4df73-246">Congratulations!</span></span> <span data-ttu-id="4df73-247">You have successfully deleted a DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="4df73-247">You have successfully deleted a DocumentDB database.</span></span>

## <a id="Run"></a><span data-ttu-id="4df73-248">Step 11: Run your C# console application all together!</span><span class="sxs-lookup"><span data-stu-id="4df73-248">Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="4df73-249">Hit F5 in Visual Studio to build the application in debug mode.</span><span class="sxs-lookup"><span data-stu-id="4df73-249">Hit F5 in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="4df73-250">You should see the output of your get started app.</span><span class="sxs-lookup"><span data-stu-id="4df73-250">You should see the output of your get started app.</span></span> <span data-ttu-id="4df73-251">The output will show the results of the queries we added and should match the example text below.</span><span class="sxs-lookup"><span data-stu-id="4df73-251">The output will show the results of the queries we added and should match the example text below.</span></span>

    Created FamilyDB
    Press any key to continue ...
    Created FamilyCollection
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

<span data-ttu-id="4df73-252">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="4df73-252">Congratulations!</span></span> <span data-ttu-id="4df73-253">You've completed this NoSQL tutorial and have a working C# console application!</span><span class="sxs-lookup"><span data-stu-id="4df73-253">You've completed this NoSQL tutorial and have a working C# console application!</span></span>

## <a id="GetSolution"></a> <span data-ttu-id="4df73-254">Get the complete NoSQL tutorial solution</span><span class="sxs-lookup"><span data-stu-id="4df73-254">Get the complete NoSQL tutorial solution</span></span>
<span data-ttu-id="4df73-255">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="4df73-255">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="4df73-256">To build the GetStarted solution, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="4df73-256">To build the GetStarted solution, you will need the following:</span></span>

* <span data-ttu-id="4df73-257">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="4df73-257">An active Azure account.</span></span> <span data-ttu-id="4df73-258">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4df73-258">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="4df73-259">A [DocumentDB account][documentdb-create-account].</span><span class="sxs-lookup"><span data-stu-id="4df73-259">A [DocumentDB account][documentdb-create-account].</span></span>
* <span data-ttu-id="4df73-260">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="4df73-260">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="4df73-261">To restore the references to the DocumentDB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span><span class="sxs-lookup"><span data-stu-id="4df73-261">To restore the references to the DocumentDB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="4df73-262">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to a DocumentDB account](#Connect).</span><span class="sxs-lookup"><span data-stu-id="4df73-262">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to a DocumentDB account](#Connect).</span></span>

<span data-ttu-id="4df73-263">That's it, build it and you're on your way!</span><span class="sxs-lookup"><span data-stu-id="4df73-263">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="4df73-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="4df73-264">Next steps</span></span>
* <span data-ttu-id="4df73-265">Want a more complex ASP.NET MVC NoSQL tutorial?</span><span class="sxs-lookup"><span data-stu-id="4df73-265">Want a more complex ASP.NET MVC NoSQL tutorial?</span></span> <span data-ttu-id="4df73-266">See [Build a web application with ASP.NET MVC using DocumentDB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="4df73-266">See [Build a web application with ASP.NET MVC using DocumentDB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="4df73-267">Want to perform scale and performance testing with DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="4df73-267">Want to perform scale and performance testing with DocumentDB?</span></span> <span data-ttu-id="4df73-268">See [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="4df73-268">See [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md)</span></span>
* <span data-ttu-id="4df73-269">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="4df73-269">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span></span>
* <span data-ttu-id="4df73-270">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="4df73-270">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="4df73-271">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="4df73-271">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[documentdb-create-account]: documentdb-create-account.md
[keys]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-keys.png






