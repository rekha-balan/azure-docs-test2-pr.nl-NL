---
redirect_url: https://azure.microsoft.com/services/documentdb/
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: f76efca8428f5198c4b0997189a59bf8880e2579
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44541004"
---
# <a name="nosql-tutorial-build-a-documentdb-c-console-application"></a><span data-ttu-id="24d37-101">NoSQL tutorial: Build a DocumentDB C# console application</span><span class="sxs-lookup"><span data-stu-id="24d37-101">NoSQL tutorial: Build a DocumentDB C# console application</span></span>
> [!div class="op_single_selector"]
> * [.NET](documentdb-get-started.md)
> * [Node.js](documentdb-nodejs-get-started.md)
> 
> 

<span data-ttu-id="24d37-104">Welcome to the NoSQL tutorial for the Azure DocumentDB .NET SDK!</span><span class="sxs-lookup"><span data-stu-id="24d37-104">Welcome to the NoSQL tutorial for the Azure DocumentDB .NET SDK!</span></span> <span data-ttu-id="24d37-105">After getting the QuickStart project or completing the tutorial, you'll have a console application that creates and queries DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="24d37-105">After getting the QuickStart project or completing the tutorial, you'll have a console application that creates and queries DocumentDB resources.</span></span>

* <span data-ttu-id="24d37-106">**[QuickStart](#quickstart)**: Download the sample project, add your connection information, and have a DocumentDB app running in less than 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="24d37-106">**[QuickStart](#quickstart)**: Download the sample project, add your connection information, and have a DocumentDB app running in less than 10 minutes.</span></span>
* <span data-ttu-id="24d37-107">**[Tutorial](#tutorial)**: Build the QuickStart app from scratch in 30 minutes.</span><span class="sxs-lookup"><span data-stu-id="24d37-107">**[Tutorial](#tutorial)**: Build the QuickStart app from scratch in 30 minutes.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24d37-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="24d37-108">Prerequisites</span></span>
* <span data-ttu-id="24d37-109">An active Azure account.</span><span class="sxs-lookup"><span data-stu-id="24d37-109">An active Azure account.</span></span> <span data-ttu-id="24d37-110">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="24d37-110">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span>
* <span data-ttu-id="24d37-111">[Visual Studio 2013 or Visual Studio 2015](http://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="24d37-111">[Visual Studio 2013 or Visual Studio 2015](http://www.visualstudio.com/).</span></span>
* <span data-ttu-id="24d37-112">.NET Framework 4.6</span><span class="sxs-lookup"><span data-stu-id="24d37-112">.NET Framework 4.6</span></span>

## <a name="quickstart"></a><span data-ttu-id="24d37-113">QuickStart</span><span class="sxs-lookup"><span data-stu-id="24d37-113">QuickStart</span></span>
1. <span data-ttu-id="24d37-114">Download the sample project .zip from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started-quickstart/archive/master.zip) or clone the [documentdb-dotnet-getting-started-quickstart](https://github.com/Azure-Samples/documentdb-dotnet-getting-started-quickstart) repo.</span><span class="sxs-lookup"><span data-stu-id="24d37-114">Download the sample project .zip from [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started-quickstart/archive/master.zip) or clone the [documentdb-dotnet-getting-started-quickstart](https://github.com/Azure-Samples/documentdb-dotnet-getting-started-quickstart) repo.</span></span>
2. <span data-ttu-id="24d37-115">Use the Azure portal to [create a DocumentDB account](documentdb-create-account.md).</span><span class="sxs-lookup"><span data-stu-id="24d37-115">Use the Azure portal to [create a DocumentDB account](documentdb-create-account.md).</span></span>
3. <span data-ttu-id="24d37-116">In the App.config file, replace the EndpointUri and PrimaryKey values with the values retrieved from the [Azure portal](https://portal.azure.com/), by navigating to **DocumentDB (NoSQL)** blade, then clicking the **Account name**,  and then clicking **Keys** on the resource menu.</span><span class="sxs-lookup"><span data-stu-id="24d37-116">In the App.config file, replace the EndpointUri and PrimaryKey values with the values retrieved from the [Azure portal](https://portal.azure.com/), by navigating to **DocumentDB (NoSQL)** blade, then clicking the **Account name**,  and then clicking **Keys** on the resource menu.</span></span>
    <span data-ttu-id="24d37-117">![Screen shot of the EndpointUri and PrimaryKey value to replace in App.config](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started-quickstart/nosql-tutorial-documentdb-keys.png)</span><span class="sxs-lookup"><span data-stu-id="24d37-117">![Screen shot of the EndpointUri and PrimaryKey value to replace in App.config](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started-quickstart/nosql-tutorial-documentdb-keys.png)</span></span>
4. <span data-ttu-id="24d37-118">Build the project.</span><span class="sxs-lookup"><span data-stu-id="24d37-118">Build the project.</span></span> <span data-ttu-id="24d37-119">The console window shows the new resources being created, queried, and then cleaned up.</span><span class="sxs-lookup"><span data-stu-id="24d37-119">The console window shows the new resources being created, queried, and then cleaned up.</span></span>
   
    ![Screen shot of the console output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started-quickstart/nosql-tutorial-documentdb-console-output.png)

## <a id="tutorial"></a><span data-ttu-id="24d37-121">Tutorial</span><span class="sxs-lookup"><span data-stu-id="24d37-121">Tutorial</span></span>
<span data-ttu-id="24d37-122">This tutorial walks you through the creation of a DocumentDB database, a DocumentDB collection, and JSON documents.</span><span class="sxs-lookup"><span data-stu-id="24d37-122">This tutorial walks you through the creation of a DocumentDB database, a DocumentDB collection, and JSON documents.</span></span> <span data-ttu-id="24d37-123">You'll then query the collection, and clean up and delete the database.</span><span class="sxs-lookup"><span data-stu-id="24d37-123">You'll then query the collection, and clean up and delete the database.</span></span> <span data-ttu-id="24d37-124">This tutorial builds the same project as the QuickStart project, but you'll build it incrementally and will receive explanation about the code you're adding to the project.</span><span class="sxs-lookup"><span data-stu-id="24d37-124">This tutorial builds the same project as the QuickStart project, but you'll build it incrementally and will receive explanation about the code you're adding to the project.</span></span>

## <a name="step-1-create-a-documentdb-account"></a><span data-ttu-id="24d37-125">Step 1: Create a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="24d37-125">Step 1: Create a DocumentDB account</span></span>
<span data-ttu-id="24d37-126">Let's create a DocumentDB account.</span><span class="sxs-lookup"><span data-stu-id="24d37-126">Let's create a DocumentDB account.</span></span> <span data-ttu-id="24d37-127">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="24d37-127">If you already have an account you want to use, you can skip ahead to [Setup your Visual Studio Solution](#SetupVS).</span></span>

[!INCLUDE [documentdb-create-dbaccount](../../includes/documentdb-create-dbaccount.md)]

## <a id="SetupVS"></a><span data-ttu-id="24d37-128">Step 2: Setup your Visual Studio solution</span><span class="sxs-lookup"><span data-stu-id="24d37-128">Step 2: Setup your Visual Studio solution</span></span>
1. <span data-ttu-id="24d37-129">Open **Visual Studio 2015** on your computer.</span><span class="sxs-lookup"><span data-stu-id="24d37-129">Open **Visual Studio 2015** on your computer.</span></span>
2. <span data-ttu-id="24d37-130">On the **File** menu, select **New**, and then choose **Project**.</span><span class="sxs-lookup"><span data-stu-id="24d37-130">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="24d37-131">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span><span class="sxs-lookup"><span data-stu-id="24d37-131">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console Application**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="24d37-132">![Screen shot of the New Project window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="24d37-132">![Screen shot of the New Project window](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-new-project-2.png)</span></span>
4. <span data-ttu-id="24d37-133">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution.</span><span class="sxs-lookup"><span data-stu-id="24d37-133">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution.</span></span>
5. <span data-ttu-id="24d37-134">Then without leaving the menu, click on **Manage NuGet Packages...**
   ![Screen shot of the Right Clicked Menu for the Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)</span><span class="sxs-lookup"><span data-stu-id="24d37-134">Then without leaving the menu, click on **Manage NuGet Packages...**
![Screen shot of the Right Clicked Menu for the Project](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges.png)</span></span>
6. <span data-ttu-id="24d37-135">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span><span class="sxs-lookup"><span data-stu-id="24d37-135">In the **Nuget** tab, click **Browse**, and type **azure documentdb** in the search box.</span></span>
7. <span data-ttu-id="24d37-136">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span><span class="sxs-lookup"><span data-stu-id="24d37-136">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="24d37-137">The package ID for the DocumentDB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)
   ![Screen shot of the Nuget Menu for finding DocumentDB Client SDK](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="24d37-137">The package ID for the DocumentDB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB)
![Screen shot of the Nuget Menu for finding DocumentDB Client SDK](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

<span data-ttu-id="24d37-138">Great!</span><span class="sxs-lookup"><span data-stu-id="24d37-138">Great!</span></span> <span data-ttu-id="24d37-139">Now that we finished the setup, let's start writing some code.</span><span class="sxs-lookup"><span data-stu-id="24d37-139">Now that we finished the setup, let's start writing some code.</span></span> <span data-ttu-id="24d37-140">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span><span class="sxs-lookup"><span data-stu-id="24d37-140">You can find a completed code project of this tutorial at [GitHub](https://github.com/Azure-Samples/documentdb-dotnet-getting-started/blob/master/src/Program.cs).</span></span>

## <a id="Connect"></a><span data-ttu-id="24d37-141">Step 3: Connect to a DocumentDB account</span><span class="sxs-lookup"><span data-stu-id="24d37-141">Step 3: Connect to a DocumentDB account</span></span>
<span data-ttu-id="24d37-142">First, add these references to the beginning of your C# application, in the Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="24d37-142">First, add these references to the beginning of your C# application, in the Program.cs file:</span></span>

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

<span data-ttu-id="24d37-144">Now, add these two constants and your *client* variable underneath your public class *Program*.</span><span class="sxs-lookup"><span data-stu-id="24d37-144">Now, add these two constants and your *client* variable underneath your public class *Program*.</span></span>

    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUri = "<your endpoint URI>";
        private const string PrimaryKey = "<your key>";
        private DocumentClient client;

<span data-ttu-id="24d37-145">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span><span class="sxs-lookup"><span data-stu-id="24d37-145">Next, head to the [Azure Portal](https://portal.azure.com) to retrieve your URI and primary key.</span></span> <span data-ttu-id="24d37-146">The DocumentDB URI and primary key are necessary for your application to understand where to connect to, and for DocumentDB to trust your application's connection.</span><span class="sxs-lookup"><span data-stu-id="24d37-146">The DocumentDB URI and primary key are necessary for your application to understand where to connect to, and for DocumentDB to trust your application's connection.</span></span>

<span data-ttu-id="24d37-147">In the Azure Portal, navigate to your DocumentDB account, and then click **Keys**.</span><span class="sxs-lookup"><span data-stu-id="24d37-147">In the Azure Portal, navigate to your DocumentDB account, and then click **Keys**.</span></span>

<span data-ttu-id="24d37-148">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span><span class="sxs-lookup"><span data-stu-id="24d37-148">Copy the URI from the portal and paste it into `<your endpoint URI>` in the program.cs file.</span></span> <span data-ttu-id="24d37-149">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span><span class="sxs-lookup"><span data-stu-id="24d37-149">Then copy the PRIMARY KEY from the portal and paste it into `<your key>`.</span></span>

![Screen shot of the Azure Portal used by the NoSQL tutorial to create a C# console application.][keys]

<span data-ttu-id="24d37-152">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="24d37-152">We'll start the getting started application by creating a new instance of the **DocumentClient**.</span></span>

<span data-ttu-id="24d37-153">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="24d37-153">Below the **Main** method, add this new asynchronous task called **GetStartedDemo**, which will instantiate our new **DocumentClient**.</span></span>

    static void Main(string[] args)
    {
    }

    // ADD THIS PART TO YOUR CODE
    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);
    }

<span data-ttu-id="24d37-154">Add the following code to run your asynchronous task from your **Main** method.</span><span class="sxs-lookup"><span data-stu-id="24d37-154">Add the following code to run your asynchronous task from your **Main** method.</span></span> <span data-ttu-id="24d37-155">The **Main** method will catch exceptions and write them to the console.</span><span class="sxs-lookup"><span data-stu-id="24d37-155">The **Main** method will catch exceptions and write them to the console.</span></span>

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

<span data-ttu-id="24d37-156">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="24d37-156">Press **F5** to run your application.</span></span>

<span data-ttu-id="24d37-157">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="24d37-157">Congratulations!</span></span> <span data-ttu-id="24d37-158">You have successfully connected to a DocumentDB account, let's now take a look at working with DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="24d37-158">You have successfully connected to a DocumentDB account, let's now take a look at working with DocumentDB resources.</span></span>  

## <a name="step-4-create-a-database"></a><span data-ttu-id="24d37-159">Step 4: Create a database</span><span class="sxs-lookup"><span data-stu-id="24d37-159">Step 4: Create a database</span></span>
<span data-ttu-id="24d37-160">Before you add the code for creating a database, add a helper method for writing to the console.</span><span class="sxs-lookup"><span data-stu-id="24d37-160">Before you add the code for creating a database, add a helper method for writing to the console.</span></span>

<span data-ttu-id="24d37-161">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span><span class="sxs-lookup"><span data-stu-id="24d37-161">Copy and paste the **WriteToConsoleAndPromptToContinue** method underneath the **GetStartedDemo** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
            Console.WriteLine(format, args);
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }

<span data-ttu-id="24d37-162">Your DocumentDB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="24d37-162">Your DocumentDB [database](documentdb-resources.md#databases) can be created by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="24d37-163">A database is the logical container of JSON document storage partitioned across collections.</span><span class="sxs-lookup"><span data-stu-id="24d37-163">A database is the logical container of JSON document storage partitioned across collections.</span></span>

<span data-ttu-id="24d37-164">Copy and paste the **CreateDatabaseIfNotExists** method underneath the **WriteToConsoleAndPromptToContinue** method.</span><span class="sxs-lookup"><span data-stu-id="24d37-164">Copy and paste the **CreateDatabaseIfNotExists** method underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task CreateDatabaseIfNotExists(string databaseName)
    {
            // Check to verify a database with the id=FamilyDB does not exist
            try
            {
                    await this.client.ReadDatabaseAsync(UriFactory.CreateDatabaseUri(databaseName));
                    this.WriteToConsoleAndPromptToContinue("Found {0}", databaseName);
            }
            catch (DocumentClientException de)
            {
                    // If the database does not exist, create a new database
                    if (de.StatusCode == HttpStatusCode.NotFound)
                    {
                            await this.client.CreateDatabaseAsync(new Database { Id = databaseName });
                            this.WriteToConsoleAndPromptToContinue("Created {0}", databaseName);
                    }
                    else
                    {
                            throw;
                    }
            }
    }

<span data-ttu-id="24d37-165">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span><span class="sxs-lookup"><span data-stu-id="24d37-165">Copy and paste the following code to your **GetStartedDemo** method underneath the client creation.</span></span> <span data-ttu-id="24d37-166">This will create a database named *FamilyDB*.</span><span class="sxs-lookup"><span data-stu-id="24d37-166">This will create a database named *FamilyDB*.</span></span>

    private async Task GetStartedDemo()
    {
        this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

        // ADD THIS PART TO YOUR CODE
        await this.CreateDatabaseIfNotExists("FamilyDB_va");

<span data-ttu-id="24d37-167">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="24d37-167">Press **F5** to run your application.</span></span>

<span data-ttu-id="24d37-168">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="24d37-168">Congratulations!</span></span> <span data-ttu-id="24d37-169">You have successfully created a DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="24d37-169">You have successfully created a DocumentDB database.</span></span>  

## <a id="CreateColl"></a><span data-ttu-id="24d37-170">Step 5: Create a collection</span><span class="sxs-lookup"><span data-stu-id="24d37-170">Step 5: Create a collection</span></span>
> [!WARNING]
> **CreateDocumentCollectionAsync** will create a new collection with reserved throughput, which has pricing implications. For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/documentdb/).
> 
> 

<span data-ttu-id="24d37-173">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="24d37-173">A [collection](documentdb-resources.md#collections) can be created by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="24d37-174">A collection is a container of JSON documents and associated JavaScript application logic.</span><span class="sxs-lookup"><span data-stu-id="24d37-174">A collection is a container of JSON documents and associated JavaScript application logic.</span></span>

<span data-ttu-id="24d37-175">Copy and paste the **CreateDocumentCollectionIfNotExists** method underneath your **CreateDatabaseIfNotExists** method.</span><span class="sxs-lookup"><span data-stu-id="24d37-175">Copy and paste the **CreateDocumentCollectionIfNotExists** method underneath your **CreateDatabaseIfNotExists** method.</span></span>

    // ADD THIS PART TO YOUR CODE
    private async Task CreateDocumentCollectionIfNotExists(string databaseName, string collectionName)
    {
        try
        {
            await this.client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName));
            this.WriteToConsoleAndPromptToContinue("Found {0}", collectionName);
        }
        catch (DocumentClientException de)
        {
            // If the document collection does not exist, create a new collection
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                DocumentCollection collectionInfo = new DocumentCollection();
                collectionInfo.Id = collectionName;

                // Configure collections for maximum query flexibility including string range queries.
                collectionInfo.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

                // Here we create a collection with 400 RU/s.
                await this.client.CreateDocumentCollectionAsync(
                    UriFactory.CreateDatabaseUri(databaseName),
                    collectionInfo,
                    new RequestOptions { OfferThroughput = 400 });

                this.WriteToConsoleAndPromptToContinue("Created {0}", collectionName);
            }
            else
            {
                throw;
            }
        }
    }

<span data-ttu-id="24d37-176">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span><span class="sxs-lookup"><span data-stu-id="24d37-176">Copy and paste the following code to your **GetStartedDemo** method underneath the database creation.</span></span> <span data-ttu-id="24d37-177">This will create a document collection named *FamilyCollection_va*.</span><span class="sxs-lookup"><span data-stu-id="24d37-177">This will create a document collection named *FamilyCollection_va*.</span></span>

        this.client = new DocumentClient(new Uri(EndpointUri), PrimaryKey);

        await this.CreateDatabaseIfNotExists("FamilyDB_oa");

        // ADD THIS PART TO YOUR CODE
        await this.CreateDocumentCollectionIfNotExists("FamilyDB_va", "FamilyCollection_va");

<span data-ttu-id="24d37-178">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="24d37-178">Press **F5** to run your application.</span></span>

<span data-ttu-id="24d37-179">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="24d37-179">Congratulations!</span></span> <span data-ttu-id="24d37-180">You have successfully created a DocumentDB document collection.</span><span class="sxs-lookup"><span data-stu-id="24d37-180">You have successfully created a DocumentDB document collection.</span></span>  

## <a id="CreateDoc"></a><span data-ttu-id="24d37-181">Step 6: Create JSON documents</span><span class="sxs-lookup"><span data-stu-id="24d37-181">Step 6: Create JSON documents</span></span>
<span data-ttu-id="24d37-182">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span><span class="sxs-lookup"><span data-stu-id="24d37-182">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="24d37-183">Documents are user defined (arbitrary) JSON content.</span><span class="sxs-lookup"><span data-stu-id="24d37-183">Documents are user defined (arbitrary) JSON content.</span></span> <span data-ttu-id="24d37-184">We can now insert one or more documents.</span><span class="sxs-lookup"><span data-stu-id="24d37-184">We can now insert one or more documents.</span></span> <span data-ttu-id="24d37-185">If you already have data you'd like to store in your database, you can use DocumentDB's [Data Migration tool](documentdb-import-data.md).</span><span class="sxs-lookup"><span data-stu-id="24d37-185">If you already have data you'd like to store in your database, you can use DocumentDB's [Data Migration tool](documentdb-import-data.md).</span></span>

<span data-ttu-id="24d37-186">First, we need to create a **Family** class that will represent objects stored within DocumentDB in this sample.</span><span class="sxs-lookup"><span data-stu-id="24d37-186">First, we need to create a **Family** class that will represent objects stored within DocumentDB in this sample.</span></span> <span data-ttu-id="24d37-187">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span><span class="sxs-lookup"><span data-stu-id="24d37-187">We will also create **Parent**, **Child**, **Pet**, **Address** subclasses that are used within **Family**.</span></span> <span data-ttu-id="24d37-188">Note that documents must have an **Id** property serialized as **id** in JSON.</span><span class="sxs-lookup"><span data-stu-id="24d37-188">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> <span data-ttu-id="24d37-189">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span><span class="sxs-lookup"><span data-stu-id="24d37-189">Create these classes by adding the following internal sub-classes after the **GetStartedDemo** method.</span></span>

<span data-ttu-id="24d37-190">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span><span class="sxs-lookup"><span data-stu-id="24d37-190">Copy and paste the **Family**, **Parent**, **Child**, **Pet**, and **Address** classes underneath the **WriteToConsoleAndPromptToContinue** method.</span></span>

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

<span data-ttu-id="24d37-191">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span><span class="sxs-lookup"><span data-stu-id="24d37-191">Copy and paste the **CreateFamilyDocumentIfNotExists** method underneath your **CreateDocumentCollectionIfNotExists** method.</span></span>

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

<span data-ttu-id="24d37-192">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span><span class="sxs-lookup"><span data-stu-id="24d37-192">And insert two documents, one each for the Andersen Family and the Wakefield Family.</span></span>

<span data-ttu-id="24d37-193">Copy and paste the following code to your **GetStartedDemo** method underneath the document collection creation.</span><span class="sxs-lookup"><span data-stu-id="24d37-193">Copy and paste the following code to your **GetStartedDemo** method underneath the document collection creation.</span></span>

    await this.CreateDatabaseIfNotExists("FamilyDB_va");

    await this.CreateDocumentCollectionIfNotExists("FamilyDB_va", "FamilyCollection_va");

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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB_va", "FamilyCollection_va", andersenFamily);

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

    await this.CreateFamilyDocumentIfNotExists("FamilyDB_va", "FamilyCollection_va", wakefieldFamily);

<span data-ttu-id="24d37-194">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="24d37-194">Press **F5** to run your application.</span></span>

<span data-ttu-id="24d37-195">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="24d37-195">Congratulations!</span></span> <span data-ttu-id="24d37-196">You have successfully created two DocumentDB documents.</span><span class="sxs-lookup"><span data-stu-id="24d37-196">You have successfully created two DocumentDB documents.</span></span>  

![Diagram illustrating the hierarchical relationship between the account, the online database, the collection, and the documents used by the NoSQL tutorial to create a C# console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-account-database.png)

## <a id="Query"></a><span data-ttu-id="24d37-198">Step 7: Query DocumentDB resources</span><span class="sxs-lookup"><span data-stu-id="24d37-198">Step 7: Query DocumentDB resources</span></span>
<span data-ttu-id="24d37-199">DocumentDB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="24d37-199">DocumentDB supports rich [queries](documentdb-sql-query.md) against JSON documents stored in each collection.</span></span>  <span data-ttu-id="24d37-200">The following sample code shows various queries - using both DocumentDB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span><span class="sxs-lookup"><span data-stu-id="24d37-200">The following sample code shows various queries - using both DocumentDB SQL syntax as well as LINQ - that we can run against the documents we inserted in the previous step.</span></span>

<span data-ttu-id="24d37-201">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span><span class="sxs-lookup"><span data-stu-id="24d37-201">Copy and paste the **ExecuteSimpleQuery** method underneath your **CreateFamilyDocumentIfNotExists** method.</span></span>

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

<span data-ttu-id="24d37-202">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span><span class="sxs-lookup"><span data-stu-id="24d37-202">Copy and paste the following code to your **GetStartedDemo** method underneath the second document creation.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB_va", "FamilyCollection_va", wakefieldFamily);

    // ADD THIS PART TO YOUR CODE
    this.ExecuteSimpleQuery("FamilyDB_va", "FamilyCollection_va");

<span data-ttu-id="24d37-203">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="24d37-203">Press **F5** to run your application.</span></span>

<span data-ttu-id="24d37-204">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="24d37-204">Congratulations!</span></span> <span data-ttu-id="24d37-205">You have successfully queried against a DocumentDB collection.</span><span class="sxs-lookup"><span data-stu-id="24d37-205">You have successfully queried against a DocumentDB collection.</span></span>

<span data-ttu-id="24d37-206">The following diagram illustrates how the DocumentDB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span><span class="sxs-lookup"><span data-stu-id="24d37-206">The following diagram illustrates how the DocumentDB SQL query syntax is called against the collection you created, and the same logic applies to the LINQ query as well.</span></span>

![Diagram illustrating the scope and meaning of the query used by the NoSQL tutorial to create a C# console application](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started/nosql-tutorial-collection-documents.png)

<span data-ttu-id="24d37-208">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because DocumentDB queries are already scoped to a single collection.</span><span class="sxs-lookup"><span data-stu-id="24d37-208">The [FROM](documentdb-sql-query.md#FromClause) keyword is optional in the query because DocumentDB queries are already scoped to a single collection.</span></span> <span data-ttu-id="24d37-209">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span><span class="sxs-lookup"><span data-stu-id="24d37-209">Therefore, "FROM Families f" can be swapped with "FROM root r", or any other variable name you choose.</span></span> <span data-ttu-id="24d37-210">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span><span class="sxs-lookup"><span data-stu-id="24d37-210">DocumentDB will infer that Families, root, or the variable name you chose, reference the current collection by default.</span></span>

## <a id="ReplaceDocument"></a><span data-ttu-id="24d37-211">Step 8: Replace JSON document</span><span class="sxs-lookup"><span data-stu-id="24d37-211">Step 8: Replace JSON document</span></span>
<span data-ttu-id="24d37-212">DocumentDB supports replacing JSON documents.</span><span class="sxs-lookup"><span data-stu-id="24d37-212">DocumentDB supports replacing JSON documents.</span></span>  

<span data-ttu-id="24d37-213">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span><span class="sxs-lookup"><span data-stu-id="24d37-213">Copy and paste the **ReplaceFamilyDocument** method underneath your **ExecuteSimpleQuery** method.</span></span>

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

<span data-ttu-id="24d37-214">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span><span class="sxs-lookup"><span data-stu-id="24d37-214">Copy and paste the following code to your **GetStartedDemo** method underneath the query execution.</span></span> <span data-ttu-id="24d37-215">After replacing the document, this will run the same query again to view the changed document.</span><span class="sxs-lookup"><span data-stu-id="24d37-215">After replacing the document, this will run the same query again to view the changed document.</span></span>

    await this.CreateFamilyDocumentIfNotExists("FamilyDB_va", "FamilyCollection_va", wakefieldFamily);

    this.ExecuteSimpleQuery("FamilyDB_va", "FamilyCollection_va");

    // ADD THIS PART TO YOUR CODE
    // Update the Grade of the Andersen Family child
    andersenFamily.Children[0].Grade = 6;

    await this.ReplaceFamilyDocument("FamilyDB_va", "FamilyCollection_va", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB_va", "FamilyCollection_va");

<span data-ttu-id="24d37-216">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="24d37-216">Press **F5** to run your application.</span></span>

<span data-ttu-id="24d37-217">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="24d37-217">Congratulations!</span></span> <span data-ttu-id="24d37-218">You have successfully replaced a DocumentDB document.</span><span class="sxs-lookup"><span data-stu-id="24d37-218">You have successfully replaced a DocumentDB document.</span></span>

## <a id="DeleteDocument"></a><span data-ttu-id="24d37-219">Step 9: Delete JSON document</span><span class="sxs-lookup"><span data-stu-id="24d37-219">Step 9: Delete JSON document</span></span>
<span data-ttu-id="24d37-220">DocumentDB supports deleting JSON documents.</span><span class="sxs-lookup"><span data-stu-id="24d37-220">DocumentDB supports deleting JSON documents.</span></span>  

<span data-ttu-id="24d37-221">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span><span class="sxs-lookup"><span data-stu-id="24d37-221">Copy and paste the **DeleteFamilyDocument** method underneath your **ReplaceFamilyDocument** method.</span></span>

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

<span data-ttu-id="24d37-222">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span><span class="sxs-lookup"><span data-stu-id="24d37-222">Copy and paste the following code to your **GetStartedDemo** method underneath the second query execution.</span></span>

    await this.ReplaceFamilyDocument("FamilyDB_va", "FamilyCollection_va", "Andersen.1", andersenFamily);

    this.ExecuteSimpleQuery("FamilyDB_va", "FamilyCollection_va");

    // ADD THIS PART TO CODE
    await this.DeleteFamilyDocument("FamilyDB_va", "FamilyCollection_va", "Andersen.1");

<span data-ttu-id="24d37-223">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="24d37-223">Press **F5** to run your application.</span></span>

<span data-ttu-id="24d37-224">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="24d37-224">Congratulations!</span></span> <span data-ttu-id="24d37-225">You have successfully deleted a DocumentDB document.</span><span class="sxs-lookup"><span data-stu-id="24d37-225">You have successfully deleted a DocumentDB document.</span></span>

## <a id="DeleteDatabase"></a><span data-ttu-id="24d37-226">Step 10: Delete the database</span><span class="sxs-lookup"><span data-stu-id="24d37-226">Step 10: Delete the database</span></span>
<span data-ttu-id="24d37-227">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span><span class="sxs-lookup"><span data-stu-id="24d37-227">Deleting the created database will remove the database and all children resources (collections, documents, etc.).</span></span>

<span data-ttu-id="24d37-228">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span><span class="sxs-lookup"><span data-stu-id="24d37-228">Copy and paste the following code to your **GetStartedDemo** method underneath the document delete to delete the entire database and all children resources.</span></span>

    this.ExecuteSimpleQuery("FamilyDB_va", "FamilyCollection_va");

    await this.DeleteFamilyDocument("FamilyDB_va", "FamilyCollection_va", "Andersen.1");

    // ADD THIS PART TO CODE
    // Clean up/delete the database
    await this.client.DeleteDatabaseAsync(UriFactory.CreateDatabaseUri("FamilyDB_va"));

<span data-ttu-id="24d37-229">Press **F5** to run your application.</span><span class="sxs-lookup"><span data-stu-id="24d37-229">Press **F5** to run your application.</span></span>

<span data-ttu-id="24d37-230">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="24d37-230">Congratulations!</span></span> <span data-ttu-id="24d37-231">You have successfully deleted a DocumentDB database.</span><span class="sxs-lookup"><span data-stu-id="24d37-231">You have successfully deleted a DocumentDB database.</span></span>

## <a id="Run"></a><span data-ttu-id="24d37-232">Step 11: Run your C# console application all together!</span><span class="sxs-lookup"><span data-stu-id="24d37-232">Step 11: Run your C# console application all together!</span></span>
<span data-ttu-id="24d37-233">Hit F5 in Visual Studio to build the application in debug mode.</span><span class="sxs-lookup"><span data-stu-id="24d37-233">Hit F5 in Visual Studio to build the application in debug mode.</span></span>

<span data-ttu-id="24d37-234">You should see the output of your get started app.</span><span class="sxs-lookup"><span data-stu-id="24d37-234">You should see the output of your get started app.</span></span> <span data-ttu-id="24d37-235">The output will show the results of the queries we added and should match the example text below.</span><span class="sxs-lookup"><span data-stu-id="24d37-235">The output will show the results of the queries we added and should match the example text below.</span></span>

    Created FamilyDB_va
    Press any key to continue ...
    Created FamilyCollection_va
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

<span data-ttu-id="24d37-236">Congratulations!</span><span class="sxs-lookup"><span data-stu-id="24d37-236">Congratulations!</span></span> <span data-ttu-id="24d37-237">You've completed this NoSQL tutorial and have a working C# console application!</span><span class="sxs-lookup"><span data-stu-id="24d37-237">You've completed this NoSQL tutorial and have a working C# console application!</span></span>

## <a name="next-steps"></a><span data-ttu-id="24d37-238">Next steps</span><span class="sxs-lookup"><span data-stu-id="24d37-238">Next steps</span></span>
* <span data-ttu-id="24d37-239">Want a more complex ASP.NET MVC NoSQL tutorial?</span><span class="sxs-lookup"><span data-stu-id="24d37-239">Want a more complex ASP.NET MVC NoSQL tutorial?</span></span> <span data-ttu-id="24d37-240">See [Build a web application with ASP.NET MVC using DocumentDB](documentdb-dotnet-application.md).</span><span class="sxs-lookup"><span data-stu-id="24d37-240">See [Build a web application with ASP.NET MVC using DocumentDB](documentdb-dotnet-application.md).</span></span>
* <span data-ttu-id="24d37-241">Want to perform scale and performance testing with DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="24d37-241">Want to perform scale and performance testing with DocumentDB?</span></span> <span data-ttu-id="24d37-242">See [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md)</span><span class="sxs-lookup"><span data-stu-id="24d37-242">See [Performance and Scale Testing with Azure DocumentDB](documentdb-performance-testing.md)</span></span>
* <span data-ttu-id="24d37-243">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span><span class="sxs-lookup"><span data-stu-id="24d37-243">Learn how to [monitor a DocumentDB account](documentdb-monitor-accounts.md).</span></span>
* <span data-ttu-id="24d37-244">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span><span class="sxs-lookup"><span data-stu-id="24d37-244">Run queries against our sample dataset in the [Query Playground](https://www.documentdb.com/sql/demo).</span></span>
* <span data-ttu-id="24d37-245">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="24d37-245">Learn more about the programming model in the Develop section of the [DocumentDB documentation page](https://azure.microsoft.com/documentation/services/documentdb/).</span></span>

[documentdb-create-account]: documentdb-create-account.md
[keys]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-get-started-quickstart/nosql-tutorial-keys.png









