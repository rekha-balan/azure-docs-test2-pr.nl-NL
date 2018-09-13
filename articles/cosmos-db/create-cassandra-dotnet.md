---
title: 'Quickstart: Cassandra API with .NET - Azure Cosmos DB | Microsoft Docs'
description: This quickstart shows how to use the Azure Cosmos DB Cassandra API to create a profile application with the Azure portal and .NET
services: cosmos-db
author: SnehaGunda
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-cassandra
ms.custom: quick start connect, mvc
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 11/15/2017
ms.author: sngun
ms.openlocfilehash: 6ab7c0fa5f7e4d10b38ecee8f75372dda3b11a1c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857991"
---
# <a name="quickstart-build-a-cassandra-app-with-net-and-azure-cosmos-db"></a><span data-ttu-id="6c23b-103">Quickstart: Build a Cassandra app with .NET and Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="6c23b-103">Quickstart: Build a Cassandra app with .NET and Azure Cosmos DB</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-cassandra-dotnet.md)
> * [Java](create-cassandra-java.md)
> * [Node.js](create-cassandra-nodejs.md)
> * [Python](create-cassandra-python.md)
>  

<span data-ttu-id="6c23b-108">This quickstart shows how to use .NET and the Azure Cosmos DB [Cassandra API](cassandra-introduction.md) to build a profile app by cloning an example from GitHub.</span><span class="sxs-lookup"><span data-stu-id="6c23b-108">This quickstart shows how to use .NET and the Azure Cosmos DB [Cassandra API](cassandra-introduction.md) to build a profile app by cloning an example from GitHub.</span></span> <span data-ttu-id="6c23b-109">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span><span class="sxs-lookup"><span data-stu-id="6c23b-109">This quickstart also walks you through the creation of an Azure Cosmos DB account by using the web-based Azure portal.</span></span>   

<span data-ttu-id="6c23b-110">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="6c23b-110">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="6c23b-111">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="6c23b-111">You can quickly create and query document, table, key-value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6c23b-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c23b-112">Prerequisites</span></span>

<span data-ttu-id="6c23b-113">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span><span class="sxs-lookup"><span data-stu-id="6c23b-113">[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)] Alternatively, you can [Try Azure Cosmos DB for free](https://azure.microsoft.com/try/cosmosdb/) without an Azure subscription, free of charge and commitments.</span></span>

<span data-ttu-id="6c23b-114">Access to the Azure Cosmos DB Cassandra API preview program.</span><span class="sxs-lookup"><span data-stu-id="6c23b-114">Access to the Azure Cosmos DB Cassandra API preview program.</span></span> <span data-ttu-id="6c23b-115">If you haven't applied for access yet, [sign up now](cassandra-introduction.md#sign-up-now).</span><span class="sxs-lookup"><span data-stu-id="6c23b-115">If you haven't applied for access yet, [sign up now](cassandra-introduction.md#sign-up-now).</span></span>

<span data-ttu-id="6c23b-116">In addition:</span><span class="sxs-lookup"><span data-stu-id="6c23b-116">In addition:</span></span> 
* <span data-ttu-id="6c23b-117">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="6c23b-117">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="6c23b-118">Make sure that you enable **Azure development** during the Visual Studio setup.</span><span class="sxs-lookup"><span data-stu-id="6c23b-118">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>
* <span data-ttu-id="6c23b-119">Install [Git](https://www.git-scm.com/) to clone the example.</span><span class="sxs-lookup"><span data-stu-id="6c23b-119">Install [Git](https://www.git-scm.com/) to clone the example.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="6c23b-120">Create a database account</span><span class="sxs-lookup"><span data-stu-id="6c23b-120">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount-cassandra](../../includes/cosmos-db-create-dbaccount-cassandra.md)]


## <a name="clone-the-sample-application"></a><span data-ttu-id="6c23b-121">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="6c23b-121">Clone the sample application</span></span>

<span data-ttu-id="6c23b-122">Now let's switch to working with code.</span><span class="sxs-lookup"><span data-stu-id="6c23b-122">Now let's switch to working with code.</span></span> <span data-ttu-id="6c23b-123">Let's clone a Cassandra API app from GitHub, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="6c23b-123">Let's clone a Cassandra API app from GitHub, set the connection string, and run it.</span></span> <span data-ttu-id="6c23b-124">You'll see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="6c23b-124">You'll see how easy it is to work with data programmatically.</span></span> 

1. <span data-ttu-id="6c23b-125">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="6c23b-125">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="6c23b-126">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="6c23b-126">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="6c23b-127">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="6c23b-127">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="6c23b-128">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="6c23b-128">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-cassandra-dotnet-getting-started.git
    ```

3. <span data-ttu-id="6c23b-129">Then open the CassandraQuickStartSample solution file in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6c23b-129">Then open the CassandraQuickStartSample solution file in Visual Studio.</span></span> 

## <a name="review-the-code"></a><span data-ttu-id="6c23b-130">Review the code</span><span class="sxs-lookup"><span data-stu-id="6c23b-130">Review the code</span></span>

<span data-ttu-id="6c23b-131">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="6c23b-131">This step is optional.</span></span> <span data-ttu-id="6c23b-132">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="6c23b-132">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="6c23b-133">The snippets are all taken from the Program.cs file installed in the C:\git-samples\azure-cosmos-db-cassandra-dotnet-getting-started\CassandraQuickStartSample folder.</span><span class="sxs-lookup"><span data-stu-id="6c23b-133">The snippets are all taken from the Program.cs file installed in the C:\git-samples\azure-cosmos-db-cassandra-dotnet-getting-started\CassandraQuickStartSample folder.</span></span> <span data-ttu-id="6c23b-134">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span><span class="sxs-lookup"><span data-stu-id="6c23b-134">Otherwise, you can skip ahead to [Update your connection string](#update-your-connection-string).</span></span>

* <span data-ttu-id="6c23b-135">Initialize the session by connecting to a Cassandra cluster endpoint.</span><span class="sxs-lookup"><span data-stu-id="6c23b-135">Initialize the session by connecting to a Cassandra cluster endpoint.</span></span> <span data-ttu-id="6c23b-136">The Cassandra API on Azure Cosmos DB supports only TLSv1.2.</span><span class="sxs-lookup"><span data-stu-id="6c23b-136">The Cassandra API on Azure Cosmos DB supports only TLSv1.2.</span></span> 

  ```csharp
   var options = new Cassandra.SSLOptions(SslProtocols.Tls12, true, ValidateServerCertificate);
   options.SetHostNameResolver((ipAddress) => CassandraContactPoint);
   Cluster cluster = Cluster.Builder().WithCredentials(UserName, Password).WithPort(CassandraPort).AddContactPoint(CassandraContactPoint).WithSSL(options).Build();
   ISession session = cluster.Connect();
   ```

* <span data-ttu-id="6c23b-137">Create a new keyspace.</span><span class="sxs-lookup"><span data-stu-id="6c23b-137">Create a new keyspace.</span></span>

    ```csharp
    session.Execute("CREATE KEYSPACE uprofile WITH REPLICATION = { 'class' : 'NetworkTopologyStrategy', 'datacenter1' : 1 };"); 
    ```

* <span data-ttu-id="6c23b-138">Create a new table.</span><span class="sxs-lookup"><span data-stu-id="6c23b-138">Create a new table.</span></span>

   ```csharp
  session.Execute("CREATE TABLE IF NOT EXISTS uprofile.user (user_id int PRIMARY KEY, user_name text, user_bcity text)");
   ```

* <span data-ttu-id="6c23b-139">Insert user entities by using the IMapper object with a new session that connects to the uprofile keyspace.</span><span class="sxs-lookup"><span data-stu-id="6c23b-139">Insert user entities by using the IMapper object with a new session that connects to the uprofile keyspace.</span></span>

    ```csharp
    mapper.Insert<User>(new User(1, "LyubovK", "Dubai"));
    ```
    
* <span data-ttu-id="6c23b-140">Query to get all user's information.</span><span class="sxs-lookup"><span data-stu-id="6c23b-140">Query to get all user's information.</span></span>

    ```csharp
   foreach (User user in mapper.Fetch<User>("Select * from user"))
   {
      Console.WriteLine(user);
   }
    ```
    
* <span data-ttu-id="6c23b-141">Query to get a single user's information.</span><span class="sxs-lookup"><span data-stu-id="6c23b-141">Query to get a single user's information.</span></span>

    ```csharp
    mapper.FirstOrDefault<User>("Select * from user where user_id = ?", 3);
    ```

## <a name="update-your-connection-string"></a><span data-ttu-id="6c23b-142">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="6c23b-142">Update your connection string</span></span>

<span data-ttu-id="6c23b-143">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="6c23b-143">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span> <span data-ttu-id="6c23b-144">The connection string information enables your app to communicate with your hosted database.</span><span class="sxs-lookup"><span data-stu-id="6c23b-144">The connection string information enables your app to communicate with your hosted database.</span></span>

1. <span data-ttu-id="6c23b-145">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span><span class="sxs-lookup"><span data-stu-id="6c23b-145">In the [Azure portal](http://portal.azure.com/), click **Connection String**.</span></span> 

    <span data-ttu-id="6c23b-146">Use the</span><span class="sxs-lookup"><span data-stu-id="6c23b-146">Use the</span></span> ![Copy button](./media/create-cassandra-dotnet/copy.png) <span data-ttu-id="6c23b-148">button on the right side of the screen to copy the USERNAME value.</span><span class="sxs-lookup"><span data-stu-id="6c23b-148">button on the right side of the screen to copy the USERNAME value.</span></span>

    ![View and copy an access key in the Azure portal, Connection String page](./media/create-cassandra-dotnet/keys.png)

2. <span data-ttu-id="6c23b-150">In Visual Studio 2017, open the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="6c23b-150">In Visual Studio 2017, open the Program.cs file.</span></span> 

3. <span data-ttu-id="6c23b-151">Paste the USERNAME value from the portal over `<FILLME>` on line 13.</span><span class="sxs-lookup"><span data-stu-id="6c23b-151">Paste the USERNAME value from the portal over `<FILLME>` on line 13.</span></span>

    <span data-ttu-id="6c23b-152">Line 13 of Program.cs should now look similar to</span><span class="sxs-lookup"><span data-stu-id="6c23b-152">Line 13 of Program.cs should now look similar to</span></span> 

    `private const string UserName = "cosmos-db-quickstart";`

3. <span data-ttu-id="6c23b-153">Go back to portal and copy the PASSWORD value.</span><span class="sxs-lookup"><span data-stu-id="6c23b-153">Go back to portal and copy the PASSWORD value.</span></span> <span data-ttu-id="6c23b-154">Paste the PASSWORD value from the portal over `<FILLME>` on line 14.</span><span class="sxs-lookup"><span data-stu-id="6c23b-154">Paste the PASSWORD value from the portal over `<FILLME>` on line 14.</span></span>

    <span data-ttu-id="6c23b-155">Line 14 of Program.cs should now look similar to</span><span class="sxs-lookup"><span data-stu-id="6c23b-155">Line 14 of Program.cs should now look similar to</span></span> 

    `private const string Password = "2Ggkr662ifxz2Mg...==";`

4. Go back to portal and copy the CONTACT POINT value. <span data-ttu-id="6c23b-157">Paste the CONTACT POINT value from the portal over `<FILLME>` on line 15.</span><span class="sxs-lookup"><span data-stu-id="6c23b-157">Paste the CONTACT POINT value from the portal over `<FILLME>` on line 15.</span></span>

    <span data-ttu-id="6c23b-158">Line 15 of Program.cs should now look similar to</span><span class="sxs-lookup"><span data-stu-id="6c23b-158">Line 15 of Program.cs should now look similar to</span></span> 

    `private const string CassandraContactPoint = "cosmos-db-quickstarts.cassandra.cosmosdb.azure.com"; //  DnsName`

5. <span data-ttu-id="6c23b-159">Save the Program.cs file.</span><span class="sxs-lookup"><span data-stu-id="6c23b-159">Save the Program.cs file.</span></span>
    
## <a name="run-the-app"></a><span data-ttu-id="6c23b-160">Run the app</span><span class="sxs-lookup"><span data-stu-id="6c23b-160">Run the app</span></span>

1. <span data-ttu-id="6c23b-161">In Visual Studio, click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="6c23b-161">In Visual Studio, click **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>

2. <span data-ttu-id="6c23b-162">At the command prompt, use the following command to install the .NET Driver's NuGet package.</span><span class="sxs-lookup"><span data-stu-id="6c23b-162">At the command prompt, use the following command to install the .NET Driver's NuGet package.</span></span> 

    ```cmd
    Install-Package CassandraCSharpDriver
    ```
3. <span data-ttu-id="6c23b-163">Click CTRL + F5 to run the application.</span><span class="sxs-lookup"><span data-stu-id="6c23b-163">Click CTRL + F5 to run the application.</span></span> <span data-ttu-id="6c23b-164">Your app displays in your console window.</span><span class="sxs-lookup"><span data-stu-id="6c23b-164">Your app displays in your console window.</span></span> 

    ![View and verify the output](./media/create-cassandra-dotnet/output.png)

    <span data-ttu-id="6c23b-166">Press CTRL + C to stop exection of the program and close the console window.</span><span class="sxs-lookup"><span data-stu-id="6c23b-166">Press CTRL + C to stop exection of the program and close the console window.</span></span> 
    
    <span data-ttu-id="6c23b-167">You can now open Data Explorer in the Azure portal to see query, modify, and work with this new data.</span><span class="sxs-lookup"><span data-stu-id="6c23b-167">You can now open Data Explorer in the Azure portal to see query, modify, and work with this new data.</span></span> 

    ![View the data in Data Explorer](./media/create-cassandra-dotnet/data-explorer.png)

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="6c23b-169">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="6c23b-169">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="6c23b-170">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="6c23b-170">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="6c23b-171">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c23b-171">Next steps</span></span>

<span data-ttu-id="6c23b-172">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a container using the Data Explorer, and run a web app.</span><span class="sxs-lookup"><span data-stu-id="6c23b-172">In this quickstart, you've learned how to create an Azure Cosmos DB account, create a container using the Data Explorer, and run a web app.</span></span> <span data-ttu-id="6c23b-173">You can now import additional data to your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="6c23b-173">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [Import Cassandra data into Azure Cosmos DB](cassandra-import-data.md)
