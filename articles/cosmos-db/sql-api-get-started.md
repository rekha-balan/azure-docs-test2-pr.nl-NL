---
title: 'Azure Cosmos DB: SQL API getting started tutorial | Microsoft Docs'
description: A tutorial that creates an online database and C# console application using the SQL API.
keywords: nosql tutorial, online database, c# console application
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-sql
ms.devlang: dotnet
ms.topic: tutorial
ms.date: 08/16/2017
ms.author: sngun
ms.openlocfilehash: a02d723d01eca5ea4d4312146bbb938179331fd3
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867102"
---
# <a name="azure-cosmos-db-sql-api-getting-started-tutorial"></a><span data-ttu-id="9804e-104">Azure Cosmos DB: SQL API getting started tutorial</span><span class="sxs-lookup"><span data-stu-id="9804e-104">Azure Cosmos DB: SQL API getting started tutorial</span></span>

> [!div class="op_single_selector"]
> * [.NET](sql-api-get-started.md)
> * [.NET Core](sql-api-dotnetcore-get-started.md)
> * [Java](sql-api-java-get-started.md)
> * [Async Java](sql-api-async-java-get-started.md)
> * [Node.js](sql-api-nodejs-get-started.md)
> * [Node.js- v2](sql-api-nodejs-get-started-preview.md) 
> 

<span data-ttu-id="9804e-111">Welcome to the Azure Cosmos DB SQL API getting started tutorial!</span><span class="sxs-lookup"><span data-stu-id="9804e-111">Welcome to the Azure Cosmos DB SQL API getting started tutorial!</span></span> <span data-ttu-id="9804e-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="9804e-112">After following this tutorial, you'll have a console application that creates and queries Azure Cosmos DB resources.</span></span>

<span data-ttu-id="9804e-113">This tutorial covers:</span><span class="sxs-lookup"><span data-stu-id="9804e-113">This tutorial covers:</span></span>

* <span data-ttu-id="9804e-114">Creating and connecting to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="9804e-114">Creating and connecting to an Azure Cosmos DB account</span></span>
* <span data-ttu-id="9804e-115">Configuring your Visual Studio Solution</span><span class="sxs-lookup"><span data-stu-id="9804e-115">Configuring your Visual Studio Solution</span></span>
* <span data-ttu-id="9804e-116">Creating an online database</span><span class="sxs-lookup"><span data-stu-id="9804e-116">Creating an online database</span></span>
* <span data-ttu-id="9804e-117">Creating a collection</span><span class="sxs-lookup"><span data-stu-id="9804e-117">Creating a collection</span></span>
* <span data-ttu-id="9804e-118">Creating JSON documents</span><span class="sxs-lookup"><span data-stu-id="9804e-118">Creating JSON documents</span></span>
* <span data-ttu-id="9804e-119">Querying the collection</span><span class="sxs-lookup"><span data-stu-id="9804e-119">Querying the collection</span></span>
* <span data-ttu-id="9804e-120">Replacing a document</span><span class="sxs-lookup"><span data-stu-id="9804e-120">Replacing a document</span></span>
* <span data-ttu-id="9804e-121">Deleting a document</span><span class="sxs-lookup"><span data-stu-id="9804e-121">Deleting a document</span></span>
* <span data-ttu-id="9804e-122">Deleting the database</span><span class="sxs-lookup"><span data-stu-id="9804e-122">Deleting the database</span></span>

<span data-ttu-id="9804e-123">Don't have time?</span><span class="sxs-lookup"><span data-stu-id="9804e-123">Don't have time?</span></span> <span data-ttu-id="9804e-124">Don't worry!</span><span class="sxs-lookup"><span data-stu-id="9804e-124">Don't worry!</span></span> <span data-ttu-id="9804e-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9804e-125">The complete solution is available on [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> <span data-ttu-id="9804e-126">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span><span class="sxs-lookup"><span data-stu-id="9804e-126">Jump to the [Get the complete NoSQL tutorial solution section](#GetSolution) for quick instructions.</span></span>

<span data-ttu-id="9804e-127">Now let's get started!</span><span class="sxs-lookup"><span data-stu-id="9804e-127">Now let's get started!</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9804e-128">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9804e-128">Prerequisites</span></span>

* <span data-ttu-id="9804e-129">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="9804e-129">An active Azure account.</span></span> <span data-ttu-id="9804e-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9804e-130">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 

  [!INCLUDE [cosmos-db-emulator-docdb-api](../../includes/cosmos-db-emulator-docdb-api.md)]

* [!INCLUDE [cosmos-db-emulator-vs](../../includes/cosmos-db-emulator-vs.md)]

## <a name="step-1-create-an-azure-cosmos-db-account"></a><span data-ttu-id="9804e-131">Step 1: Create an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="9804e-131">Step 1: Create an Azure Cosmos DB account</span></span>
<span data-ttu-id="9804e-132">Let's create an Azure Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="9804e-132">Let's create an Azure Cosmos DB account.</span></span> <span data-ttu-id="9804e-133">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="9804e-133">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span> <span data-ttu-id="9804e-134">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="9804e-134">If you are using the Azure Cosmos DB Emulator, follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <a id="SetupVS"></a><span data-ttu-id="9804e-135">Step 2: Setup your Visual Studio solution</span><span class="sxs-lookup"><span data-stu-id="9804e-135">Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="9804e-136">Open **Visual Studio 2017** on your computer.</span><span class="sxs-lookup"><span data-stu-id="9804e-136">Open **Visual Studio 2017** on your computer.</span></span>
2. <span data-ttu-id="9804e-137">On the **File** menu, select **New**, and then choose **Project**.</span><span class="sxs-lookup"><span data-stu-id="9804e-137">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="9804e-138">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9804e-138">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="9804e-139">![Screen shot of the New Project window](./media/sql-api-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="9804e-139">![Screen shot of the New Project window](./media/sql-api-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="9804e-140">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span><span class="sxs-lookup"><span data-stu-id="9804e-140">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Screen shot of the Right Clicked Menu for the Project](./media/sql-api-get-started/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="9804e-142">In the **NuGet** tab, click **Browse**, and type **azure documentdb** in the search box.</span><span class="sxs-lookup"><span data-stu-id="9804e-142">In the **NuGet** tab, click **Browse**, and type **azure documentdb** in the search box.</span></span>
6. <span data-ttu-id="9804e-143">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="9804e-143">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="9804e-144">The package ID for the Azure Cosmos DB SQL API Client Library is [Microsoft Azure Cosmos DB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span><span class="sxs-lookup"><span data-stu-id="9804e-144">The package ID for the Azure Cosmos DB SQL API Client Library is [Microsoft Azure Cosmos DB Client Library](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/).</span></span>
   <span data-ttu-id="9804e-145">![Screen shot of the NuGet Menu for finding Azure Cosmos DB Client SDK](./media/sql-api-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="9804e-145">![Screen shot of the NuGet Menu for finding Azure Cosmos DB Client SDK](./media/sql-api-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="9804e-146">If you get a message about reviewing changes to the solution, click **OK**.</span><span class="sxs-lookup"><span data-stu-id="9804e-146">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="9804e-147">If you get a message about license acceptance, click **I accept**.</span><span class="sxs-lookup"><span data-stu-id="9804e-147">If you get a message about license acceptance, click **I accept**.</span></span>

<span data-ttu-id="9804e-148">Great!</span><span class="sxs-lookup"><span data-stu-id="9804e-148">Great!</span></span> <span data-ttu-id="9804e-149">Now that we finished the setup, let's start writing some code.</span><span class="sxs-lookup"><span data-stu-id="9804e-149">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="9804e-150">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="9804e-150">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <a id="Connect"></a><span data-ttu-id="9804e-151">Step 3: Connect to an Azure Cosmos DB account</span><span class="sxs-lookup"><span data-stu-id="9804e-151">Step 3: Connect to an Azure Cosmos DB account</span></span>
<span data-ttu-id="9804e-152">First, add these references to the beginning of your C# application, in the Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="9804e-152">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

    using System;
    using System.Linq;
    using System.Threading.Tasks;

    // ADD THIS PART TO YOUR CODE
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;

> [!IMPORTANT]
> In order to complete the tutorial, make sure you add the dependencies above.
> 
> 

<span data-ttu-id="9804e-154">Now, add these two constants and your *client* variable underneath your public class *Program*.</span><span class="sxs-lookup"><span data-stu-id="9804e-154">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;

<span data-ttu-id="9804e-155">Next, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span><span class="sxs-lookup"><span data-stu-id="9804e-155">Next, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="9804e-156">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span><span class="sxs-lookup"><span data-stu-id="9804e-156">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="9804e-157">In the Azure portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="9804e-157">In the Azure portal, navigate to your Azure Cosmos DB account, and then click **Keys**.</span></span>

<span data-ttu-id="9804e-158">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span><span class="sxs-lookup"><span data-stu-id="9804e-158">Copy the URI from the portal and paste it into `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="9804e-159">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="9804e-159">Then copy the PRIMARY KEY from the portal and paste it into `<your primary key>`.</span></span>

![Screen shot of the Azure portal used by the NoSQL tutorial to create a C# console application.][keys]

<span data-ttu-id="9804e-162">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="9804e-162">Next, we'll start the application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="9804e-163">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="9804e-163">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);
    }

<span data-ttu-id="9804e-164">Add the following code to run your asynchronous task from your **Main** method.</span><span class="sxs-lookup"><span data-stu-id="9804e-164">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="9804e-165">The **Main** method will catch exceptions and write them to the console.</span><span class="sxs-lookup"><span data-stu-id="9804e-165">The **Main** method will catch exceptions and write them to the console.</span></span>

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

<span data-ttu-id="9804e-166">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="9804e-166">Press **F5** to run your application.</span></span> <span data-ttu-id="9804e-167">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span><span class="sxs-lookup"><span data-stu-id="9804e-167">The console window output displays the message `End of demo, press any key to exit.` confirming that the connection was made.</span></span>  <span data-ttu-id="9804e-168">You can then close the console window.</span><span class="sxs-lookup"><span data-stu-id="9804e-168">You can then close the console window.</span></span> 

<span data-ttu-id="9804e-169">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9804e-169">Congratulations!</span></span> <span data-ttu-id="9804e-170">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span><span class="sxs-lookup"><span data-stu-id="9804e-170">You have successfully connected to an Azure Cosmos DB account, let's now take a look at working with Azure Cosmos DB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="9804e-171">Step 4: Create a database</span><span class="sxs-lookup"><span data-stu-id="9804e-171">Step 4: Create a database</span></span>
<span data-ttu-id="9804e-172">Before you add the code for creating a database, add a helper method for writing to the console.</span><span class="sxs-lookup"><span data-stu-id="9804e-172">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="9804e-173">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span><span class="sxs-lookup"><span data-stu-id="9804e-173">Copy and paste the **WriteToConsoleAndPromptToContinue** method after the **GetStartedDemo** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="9804e-174">Your Azure Cosmos DB [database](sql-api-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="9804e-174">Your Azure Cosmos DB [database](sql-api-resources.md#databases) can be created by using the [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="9804e-175">A database is the logical container of JSON document storage partitioned across collections.</span><span class="sxs-lookup"><span data-stu-id="9804e-175">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="9804e-176">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span><span class="sxs-lookup"><span data-stu-id="9804e-176">Copy and paste the following code to your **GetStartedDemo** method after the client creation.</span></span> <span data-ttu-id="9804e-177">This will create a database named *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="9804e-177">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

<span data-ttu-id="9804e-178">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="9804e-178">Press **F5** to run your application.</span></span>

<span data-ttu-id="9804e-179">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9804e-179">Congratulations!</span></span> <span data-ttu-id="9804e-180">You have successfully created an Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="9804e-180">You have successfully created an Azure Cosmos DB database.</span></span>  

## <a id="CreateColl"></a><span data-ttu-id="9804e-181">Step 5: Create a collection</span><span class="sxs-lookup"><span data-stu-id="9804e-181">Step 5: Create a collection</span></span>
> [!WARNING]
> **CreateDocumentCollectionIfNotExistsAsync** will create a new collection with reserved throughput, which has pricing implications. For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).
> 
> 

<span data-ttu-id="9804e-184">A [collection](sql-api-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="9804e-184">A [collection](sql-api-resources.md#collections) can be created by using the [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="9804e-185">A collection is a container of JSON documents and associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="9804e-185">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="9804e-186">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span><span class="sxs-lookup"><span data-stu-id="9804e-186">Copy and paste the following code to your **GetStartedDemo** method after the database creation.</span></span> <span data-ttu-id="9804e-187">This will create a document collection named *FamilyCollection*.</span><span class="sxs-lookup"><span data-stu-id="9804e-187">This will create a document collection named *FamilyCollection*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "FamilyDB" });

        // ADD THIS PART TO YOUR CODE
         await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("FamilyDB"), new DocumentCollection { Id = "FamilyCollection" });

<span data-ttu-id="9804e-188">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="9804e-188">Press **F5** to run your application.</span></span>

<span data-ttu-id="9804e-189">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9804e-189">Congratulations!</span></span> <span data-ttu-id="9804e-190">You have successfully created an Azure Cosmos DB document collection.</span><span class="sxs-lookup"><span data-stu-id="9804e-190">You have successfully created an Azure Cosmos DB document collection.</span></span>  

## <a id="CreateDoc"></a><span data-ttu-id="9804e-191">Step 6: Create JSON documents</span><span class="sxs-lookup"><span data-stu-id="9804e-191">Step 6: Create JSON documents</span></span>
<span data-ttu-id="9804e-192">A [document](sql-api-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="9804e-192">A [document](sql-api-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="9804e-193">Documents are user defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="9804e-193">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="9804e-194">We can now insert one or more documents.</span><span class="sxs-lookup"><span data-stu-id="9804e-194">We can now insert one or more documents.</span></span> <span data-ttu-id="9804e-195">If you already have data you'd like to store in your database, you can use the Azure Cosmos DB [Data Migration tool](import-data.md) to import the data into a database.</span><span class="sxs-lookup"><span data-stu-id="9804e-195">If you already have data you'd like to store in your database, you can use the Azure Cosmos DB [Data Migration tool](import-data.md) to import the data into a database.</span></span>

<span data-ttu-id="9804e-196">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span><span class="sxs-lookup"><span data-stu-id="9804e-196">First, we need to create a **Family** class that will represent objects stored within Azure Cosmos DB in this sample.</span></span> <span data-ttu-id="9804e-197">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span><span class="sxs-lookup"><span data-stu-id="9804e-197">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="9804e-198">Note that documents must have an **Id** property serialized as **id** in JSON.</span><span class="sxs-lookup"><span data-stu-id="9804e-198">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="9804e-199">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span><span class="sxs-lookup"><span data-stu-id="9804e-199">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="9804e-200">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span><span class="sxs-lookup"><span data-stu-id="9804e-200">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes after the **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="9804e-201">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span><span class="sxs-lookup"><span data-stu-id="9804e-201">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **Address** class.</span></span>

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

<span data-ttu-id="9804e-202">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span><span class="sxs-lookup"><span data-stu-id="9804e-202">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="9804e-203">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span><span class="sxs-lookup"><span data-stu-id="9804e-203">Copy and paste the following code to your **GetStartedDemo** method after the document collection creation.</span></span>

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

<span data-ttu-id="9804e-204">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="9804e-204">Press **F5** to run your application.</span></span>

<span data-ttu-id="9804e-205">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9804e-205">Congratulations!</span></span> <span data-ttu-id="9804e-206">You have successfully created two Azure Cosmos DB documents.</span><span class="sxs-lookup"><span data-stu-id="9804e-206">You have successfully created two Azure Cosmos DB documents.</span></span>  

![Diagram illustrating the hierarchical relationship between the account, the online database, the collection, and the documents used by the NoSQL tutorial to create a C# console application](./media/sql-api-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a><span data-ttu-id="9804e-208">Step 7: Query Azure Cosmos DB resources</span><span class="sxs-lookup"><span data-stu-id="9804e-208">Step 7: Query Azure Cosmos DB resources</span></span>
<span data-ttu-id="9804e-209">Azure Cosmos DB supports rich [queries](sql-api-sql-query.md) against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="9804e-209">Azure Cosmos DB supports rich [queries](sql-api-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="9804e-210">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span><span class="sxs-lookup"><span data-stu-id="9804e-210">The following sample code shows various queries - using both Azure Cosmos DB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="9804e-211">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span><span class="sxs-lookup"><span data-stu-id="9804e-211">Copy and paste the **ExecuteSimpleQuery** method after your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="9804e-212">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span><span class="sxs-lookup"><span data-stu-id="9804e-212">Copy and paste the following code to your **GetStartedDemo** method after the second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="9804e-213">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="9804e-213">Press **F5** to run your application.</span></span>

<span data-ttu-id="9804e-214">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9804e-214">Congratulations!</span></span> <span data-ttu-id="9804e-215">You have successfully queried against an Azure Cosmos DB collection.</span><span class="sxs-lookup"><span data-stu-id="9804e-215">You have successfully queried against an Azure Cosmos DB collection.</span></span>

<span data-ttu-id="9804e-216">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span><span class="sxs-lookup"><span data-stu-id="9804e-216">The following diagram illustrates how the Azure Cosmos DB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagram illustrating the scope and meaning of the query used by the NoSQL tutorial to create a C# console application](./media/sql-api-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="9804e-218">The [FROM](sql-api-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span><span class="sxs-lookup"><span data-stu-id="9804e-218">The [FROM](sql-api-sql-query.md#FromClause) keyword is optional in the query because Azure Cosmos DB queries are already scoped to a single collection.</span></span> <span data-ttu-id="9804e-219">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span><span class="sxs-lookup"><span data-stu-id="9804e-219">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="9804e-220">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span><span class="sxs-lookup"><span data-stu-id="9804e-220">Azure Cosmos DB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <a id="ReplaceDocument"></a><span data-ttu-id="9804e-221">Step 8: Replace JSON document</span><span class="sxs-lookup"><span data-stu-id="9804e-221">Step 8: Replace JSON document</span></span>
<span data-ttu-id="9804e-222">Azure Cosmos DB supports replacing JSON documents.</span><span class="sxs-lookup"><span data-stu-id="9804e-222">Azure Cosmos DB supports replacing JSON documents.</span></span>  

<span data-ttu-id="9804e-223">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span><span class="sxs-lookup"><span data-stu-id="9804e-223">Copy and paste the **ReplaceFamilyDocument** method after your **ExecuteSimpleQuery** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task ReplaceFamilyDocument(string databaseName, string collectionName, string familyName, Family updatedFamily)
    {
         await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, familyName), updatedFamily);
         this.WriteToConsoleAndPromptToContinue("Replaced Family {0}", familyName);
    }

<span data-ttu-id="9804e-224">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span><span class="sxs-lookup"><span data-stu-id="9804e-224">Copy and paste the following code to your **GetStartedDemo** method after the query execution, at the end of the method.</span></span> <span data-ttu-id="9804e-225">After replacing the document, this will run the same query again to view the changed document.</span><span class="sxs-lookup"><span data-stu-id="9804e-225">After replacing the document, this will run the same query again to view the changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB", "FamilyCollection", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

<span data-ttu-id="9804e-226">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="9804e-226">Press **F5** to run your application.</span></span>

<span data-ttu-id="9804e-227">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9804e-227">Congratulations!</span></span> <span data-ttu-id="9804e-228">You have successfully replaced an Azure Cosmos DB document.</span><span class="sxs-lookup"><span data-stu-id="9804e-228">You have successfully replaced an Azure Cosmos DB document.</span></span>

## <a id="DeleteDocument"></a><span data-ttu-id="9804e-229">Step 9: Delete JSON document</span><span class="sxs-lookup"><span data-stu-id="9804e-229">Step 9: Delete JSON document</span></span>
<span data-ttu-id="9804e-230">Azure Cosmos DB supports deleting JSON documents.</span><span class="sxs-lookup"><span data-stu-id="9804e-230">Azure Cosmos DB supports deleting JSON documents.</span></span>  

<span data-ttu-id="9804e-231">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span><span class="sxs-lookup"><span data-stu-id="9804e-231">Copy and paste the **DeleteFamilyDocument** method after your **ReplaceFamilyDocument** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task DeleteFamilyDocument(string databaseName, string collectionName, string documentName)
    {
         await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName));
         Console.WriteLine("Deleted Family {0}", documentName);
    }

<span data-ttu-id="9804e-232">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span><span class="sxs-lookup"><span data-stu-id="9804e-232">Copy and paste the following code to your **GetStartedDemo** method after the second query execution, at the end of the method.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1", andersenFamily);
    
    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");
    
    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

<span data-ttu-id="9804e-233">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="9804e-233">Press **F5** to run your application.</span></span>

<span data-ttu-id="9804e-234">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9804e-234">Congratulations!</span></span> <span data-ttu-id="9804e-235">You have successfully deleted an Azure Cosmos DB document.</span><span class="sxs-lookup"><span data-stu-id="9804e-235">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <a id="DeleteDatabase"></a><span data-ttu-id="9804e-236">Step 10: Delete the database</span><span class="sxs-lookup"><span data-stu-id="9804e-236">Step 10: Delete the database</span></span>
<span data-ttu-id="9804e-237">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="9804e-237">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="9804e-238">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span><span class="sxs-lookup"><span data-stu-id="9804e-238">Copy and paste the following code to your **GetStartedDemo** method after the document delete to delete the entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB", "FamilyCollection");

    await this.DeleteFamilyDocument("FamilyDB", "FamilyCollection", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB"));

<span data-ttu-id="9804e-239">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="9804e-239">Press **F5** to run your application.</span></span>

<span data-ttu-id="9804e-240">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9804e-240">Congratulations!</span></span> <span data-ttu-id="9804e-241">You have successfully deleted an Azure Cosmos DB database.</span><span class="sxs-lookup"><span data-stu-id="9804e-241">You have successfully deleted an Azure Cosmos DB database.</span></span>

## <a id="Run"></a><span data-ttu-id="9804e-242">Step 11: Run your C# console application all together!</span><span class="sxs-lookup"><span data-stu-id="9804e-242">Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="9804e-243">Hit F5 in Visual Studio to build the application in debug mode.</span><span class="sxs-lookup"><span data-stu-id="9804e-243">Hit F5 in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="9804e-244">You should see the output of your get started app in a console window.</span><span class="sxs-lookup"><span data-stu-id="9804e-244">You should see the output of your get started app in a console window.</span></span> <span data-ttu-id="9804e-245">The output will show the results of the queries we added and should match the example text below.</span><span class="sxs-lookup"><span data-stu-id="9804e-245">The output will show the results of the queries we added and should match the example text below.</span></span>

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

<span data-ttu-id="9804e-246">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="9804e-246">Congratulations!</span></span> <span data-ttu-id="9804e-247">You've completed the tutorial and have a working C# console application!</span><span class="sxs-lookup"><span data-stu-id="9804e-247">You've completed the tutorial and have a working C# console application!</span></span>

## <a id="GetSolution"></a> <span data-ttu-id="9804e-248">Get the complete tutorial solution</span><span class="sxs-lookup"><span data-stu-id="9804e-248">Get the complete tutorial solution</span></span>
<span data-ttu-id="9804e-249">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span><span class="sxs-lookup"><span data-stu-id="9804e-249">If you didn't have time to complete the steps in this tutorial, or just want to download the code samples, you can get it from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started).</span></span> 

<span data-ttu-id="9804e-250">To build the GetStarted solution, you will need the following:</span><span class="sxs-lookup"><span data-stu-id="9804e-250">To build the GetStarted solution, you will need the following:</span></span>

* <span data-ttu-id="9804e-251">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="9804e-251">An active Azure account.</span></span> <span data-ttu-id="9804e-252">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="9804e-252">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="9804e-253">An [Azure Cosmos DB account][cosmos-db-create-account].</span><span class="sxs-lookup"><span data-stu-id="9804e-253">An [Azure Cosmos DB account][cosmos-db-create-account].</span></span>
* <span data-ttu-id="9804e-254">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span><span class="sxs-lookup"><span data-stu-id="9804e-254">The [GetStarted](https://github.com/Azure-Samples/documentdb-dotnet-getting-started) solution available on GitHub.</span></span>

<span data-ttu-id="9804e-255">To restore the references to the Azure Cosmos DB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span><span class="sxs-lookup"><span data-stu-id="9804e-255">To restore the references to the Azure Cosmos DB .NET SDK in Visual Studio, right-click the **GetStarted** solution in Solution Explorer, and then click **Enable NuGet Package Restore**.</span></span> <span data-ttu-id="9804e-256">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span><span class="sxs-lookup"><span data-stu-id="9804e-256">Next, in the App.config file, update the EndpointUrl and AuthorizationKey values as described in [Connect to an Azure Cosmos DB account](#Connect).</span></span>

<span data-ttu-id="9804e-257">That's it, build it and you're on your way!</span><span class="sxs-lookup"><span data-stu-id="9804e-257">That's it, build it and you're on your way!</span></span>


## <a name="next-steps"></a><span data-ttu-id="9804e-258">Next steps</span><span class="sxs-lookup"><span data-stu-id="9804e-258">Next steps</span></span>
* <span data-ttu-id="9804e-259">Want a more complex ASP.NET MVC tutorial?</span><span class="sxs-lookup"><span data-stu-id="9804e-259">Want a more complex ASP.NET MVC tutorial?</span></span> <span data-ttu-id="9804e-260">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](sql-api-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="9804e-260">See [ASP.NET MVC Tutorial: Web application development with Azure Cosmos DB](sql-api-dotnet-application.md).</span></span>
* <span data-ttu-id="9804e-261">Want to perform scale and performance testing with Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="9804e-261">Want to perform scale and performance testing with Azure Cosmos DB?</span></span> <span data-ttu-id="9804e-262">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="9804e-262">See [Performance and scale testing with Azure Cosmos DB](performance-testing.md)</span></span>
* <span data-ttu-id="9804e-263">Learn how to [monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="9804e-263">Learn how to [monitor Azure Cosmos DB requests, usage, and storage](monitor-accounts.md).</span></span>
* <span data-ttu-id="9804e-264">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="9804e-264">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="9804e-265">To learn more about Azure Cosmos DB, see [Welcome to Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span><span class="sxs-lookup"><span data-stu-id="9804e-265">To learn more about Azure Cosmos DB, see [Welcome to Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

[keys]: media/sql-api-get-started/nosql-tutorial-keys.png
[cosmos-db-create-account]: create-sql-api-dotnet.md#create-account
