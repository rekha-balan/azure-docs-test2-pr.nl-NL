---
title: 'Azure Cosmos DB: Build a MongoDB API console app with Golang and the Azure portal | Microsoft Docs'
description: Presents a Golang code sample you can use to connect to and query Azure Cosmos DB
services: cosmos-db
author: slyons
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.devlang: na
ms.topic: quickstart
ms.date: 07/21/2017
ms.author: sclyon
ms.custom: mvc
ms.openlocfilehash: 7bfcbf2c72dbe33727097841f34f3f6869e9d2d8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967249"
---
# <a name="azure-cosmos-db-build-a-mongodb-api-console-app-with-golang-and-the-azure-portal"></a><span data-ttu-id="c8103-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c8103-103">Azure Cosmos DB: Build a MongoDB API console app with Golang and the Azure portal</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-mongodb-dotnet.md)
> * [Java](create-mongodb-java.md)
> * [Node.js](create-mongodb-nodejs.md)
> * [Python](create-mongodb-flask.md)
> * [Xamarin](create-mongodb-xamarin.md)
> * [Golang](create-mongodb-golang.md)
>  

<span data-ttu-id="c8103-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="c8103-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="c8103-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8103-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="c8103-112">This quick-start demonstrates how to use an existing MongoDB app written in [Golang](https://golang.org/) and connect it to your Azure Cosmos DB database, which supports MongoDB client connections by using the [MongoDB API](mongodb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c8103-112">This quick-start demonstrates how to use an existing MongoDB app written in [Golang](https://golang.org/) and connect it to your Azure Cosmos DB database, which supports MongoDB client connections by using the [MongoDB API](mongodb-introduction.md).</span></span>

<span data-ttu-id="c8103-113">In other words, your Golang application only knows that it's connecting to a database using MongoDB APIs.</span><span class="sxs-lookup"><span data-stu-id="c8103-113">In other words, your Golang application only knows that it's connecting to a database using MongoDB APIs.</span></span> <span data-ttu-id="c8103-114">It is transparent to the application that the data is stored in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c8103-114">It is transparent to the application that the data is stored in Azure Cosmos DB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c8103-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c8103-115">Prerequisites</span></span>

- <span data-ttu-id="c8103-116">An Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="c8103-116">An Azure subscription.</span></span> <span data-ttu-id="c8103-117">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span><span class="sxs-lookup"><span data-stu-id="c8103-117">If you don’t have an Azure subscription, create a [free account](https://azure.microsoft.com/free) before you begin.</span></span> 

  [!INCLUDE [cosmos-db-emulator-mongodb](../../includes/cosmos-db-emulator-mongodb.md)]

- <span data-ttu-id="c8103-118">[Go](https://golang.org/dl/) and a basic knowledge of the [Go](https://golang.org/) language.</span><span class="sxs-lookup"><span data-stu-id="c8103-118">[Go](https://golang.org/dl/) and a basic knowledge of the [Go](https://golang.org/) language.</span></span>
- <span data-ttu-id="c8103-119">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span><span class="sxs-lookup"><span data-stu-id="c8103-119">An IDE — [Gogland](https://www.jetbrains.com/go/) by Jetbrains, [Visual Studio Code](https://code.visualstudio.com/) by Microsoft, or [Atom](https://atom.io/).</span></span> <span data-ttu-id="c8103-120">In this tutorial, I'm using Goglang.</span><span class="sxs-lookup"><span data-stu-id="c8103-120">In this tutorial, I'm using Goglang.</span></span>

<a id="create-account"></a>
## <a name="create-a-database-account"></a><span data-ttu-id="c8103-121">Create a database account</span><span class="sxs-lookup"><span data-stu-id="c8103-121">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="clone-the-sample-application"></a><span data-ttu-id="c8103-122">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="c8103-122">Clone the sample application</span></span>

<span data-ttu-id="c8103-123">Clone the sample application and install the required packages.</span><span class="sxs-lookup"><span data-stu-id="c8103-123">Clone the sample application and install the required packages.</span></span>

1. <span data-ttu-id="c8103-124">Create a folder named CosmosDBSample inside the GOROOT\src folder, which is C:\Go\ by default.</span><span class="sxs-lookup"><span data-stu-id="c8103-124">Create a folder named CosmosDBSample inside the GOROOT\src folder, which is C:\Go\ by default.</span></span>
2. <span data-ttu-id="c8103-125">Run the following command using a git terminal window such as git bash to clone the sample repository into the CosmosDBSample folder.</span><span class="sxs-lookup"><span data-stu-id="c8103-125">Run the following command using a git terminal window such as git bash to clone the sample repository into the CosmosDBSample folder.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-mongodb-golang-getting-started.git
    ```
3.  <span data-ttu-id="c8103-126">Run the following command to get the mgo package.</span><span class="sxs-lookup"><span data-stu-id="c8103-126">Run the following command to get the mgo package.</span></span> 

    ```
    go get gopkg.in/mgo.v2
    ```

<span data-ttu-id="c8103-127">The [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for the [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span><span class="sxs-lookup"><span data-stu-id="c8103-127">The [mgo](http://labix.org/mgo) driver (pronounced as *mango*) is a [MongoDB](http://www.mongodb.org/) driver for the [Go language](http://golang.org/) that implements a rich and well tested selection of features under a very simple API following standard Go idioms.</span></span>

<a id="connection-string"></a>

## <a name="update-your-connection-string"></a><span data-ttu-id="c8103-128">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="c8103-128">Update your connection string</span></span>

<span data-ttu-id="c8103-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="c8103-129">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="c8103-130">Click **Quick start** in the left navigation menu, and then click **Other** to view the connection string information required by the Go application.</span><span class="sxs-lookup"><span data-stu-id="c8103-130">Click **Quick start** in the left navigation menu, and then click **Other** to view the connection string information required by the Go application.</span></span>

2. <span data-ttu-id="c8103-131">In Goglang, open the main.go file in the GOROOT\CosmosDBSample directory and update the following lines of code using the connection string information from the Azure portal as shown in the following screenshot.</span><span class="sxs-lookup"><span data-stu-id="c8103-131">In Goglang, open the main.go file in the GOROOT\CosmosDBSample directory and update the following lines of code using the connection string information from the Azure portal as shown in the following screenshot.</span></span> 

    <span data-ttu-id="c8103-132">The Database name is the prefix of the **Host** value in the Azure portal connection string pane.</span><span class="sxs-lookup"><span data-stu-id="c8103-132">The Database name is the prefix of the **Host** value in the Azure portal connection string pane.</span></span> <span data-ttu-id="c8103-133">For the account shown in the image below, the Database name is golang-coach.</span><span class="sxs-lookup"><span data-stu-id="c8103-133">For the account shown in the image below, the Database name is golang-coach.</span></span>

    ```go
    Database: "The prefix of the Host value in the Azure portal",
    Username: "The Username in the Azure portal",
    Password: "The Password in the Azure portal",
    ```

    ![Quick start pane, Other tab in the Azure portal showing the connection string information](./media/create-mongodb-golang/cosmos-db-golang-connection-string.png)

3. <span data-ttu-id="c8103-135">Save the main.go file.</span><span class="sxs-lookup"><span data-stu-id="c8103-135">Save the main.go file.</span></span>

## <a name="review-the-code"></a><span data-ttu-id="c8103-136">Review the code</span><span class="sxs-lookup"><span data-stu-id="c8103-136">Review the code</span></span>

<span data-ttu-id="c8103-137">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="c8103-137">This step is optional.</span></span> <span data-ttu-id="c8103-138">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="c8103-138">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="c8103-139">Otherwise, you can skip ahead to [Run the app](#run-the-app).</span><span class="sxs-lookup"><span data-stu-id="c8103-139">Otherwise, you can skip ahead to [Run the app](#run-the-app).</span></span> 

<span data-ttu-id="c8103-140">The following snippets are all taken from the main.go file.</span><span class="sxs-lookup"><span data-stu-id="c8103-140">The following snippets are all taken from the main.go file.</span></span>

### <a name="connecting-the-go-app-to-azure-cosmos-db"></a><span data-ttu-id="c8103-141">Connecting the Go app to Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c8103-141">Connecting the Go app to Azure Cosmos DB</span></span>

<span data-ttu-id="c8103-142">Azure Cosmos DB supports the SSL-enabled MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c8103-142">Azure Cosmos DB supports the SSL-enabled MongoDB.</span></span> <span data-ttu-id="c8103-143">To connect to an SSL-enabled MongoDB, you need to define the **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of the [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function to perform the connection.</span><span class="sxs-lookup"><span data-stu-id="c8103-143">To connect to an SSL-enabled MongoDB, you need to define the **DialServer** function in [mgo.DialInfo](http://gopkg.in/mgo.v2#DialInfo), and make use of the [tls.*Dial*](http://golang.org/pkg/crypto/tls#Dial) function to perform the connection.</span></span>

<span data-ttu-id="c8103-144">The following Golang code snippet connects the Go app with Azure Cosmos DB MongoDB API.</span><span class="sxs-lookup"><span data-stu-id="c8103-144">The following Golang code snippet connects the Go app with Azure Cosmos DB MongoDB API.</span></span> <span data-ttu-id="c8103-145">The *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span><span class="sxs-lookup"><span data-stu-id="c8103-145">The *DialInfo* class holds options for establishing a session with a MongoDB cluster.</span></span>

```go
// DialInfo holds options for establishing a session with a MongoDB cluster.
dialInfo := &mgo.DialInfo{
    Addrs:    []string{"golang-couch.documents.azure.com:10255"}, // Get HOST + PORT
    Timeout:  60 * time.Second,
    Database: "database", // It can be anything
    Username: "username", // Username
    Password: "Azure database connect password from Azure Portal", // PASSWORD
    DialServer: func(addr *mgo.ServerAddr) (net.Conn, error) {
        return tls.Dial("tcp", addr.String(), &tls.Config{})
    },
}

// Create a session which maintains a pool of socket connections
// to our Azure Cosmos DB MongoDB database.
session, err := mgo.DialWithInfo(dialInfo)

if err != nil {
    fmt.Printf("Can't connect to mongo, go error %v\n", err)
    os.Exit(1)
}

defer session.Close()

// SetSafe changes the session safety mode.
// If the safe parameter is nil, the session is put in unsafe mode, 
// and writes become fire-and-forget,
// without error checking. The unsafe mode is faster since operations won't hold on waiting for a confirmation.
// 
session.SetSafe(&mgo.Safe{})
```

<span data-ttu-id="c8103-146">The **mgo.Dial()** method is used when there is no SSL connection.</span><span class="sxs-lookup"><span data-stu-id="c8103-146">The **mgo.Dial()** method is used when there is no SSL connection.</span></span> <span data-ttu-id="c8103-147">For an SSL connection, the **mgo.DialWithInfo()** method is required.</span><span class="sxs-lookup"><span data-stu-id="c8103-147">For an SSL connection, the **mgo.DialWithInfo()** method is required.</span></span>

<span data-ttu-id="c8103-148">An instance of the **DialWIthInfo{}** object is used to create the session object.</span><span class="sxs-lookup"><span data-stu-id="c8103-148">An instance of the **DialWIthInfo{}** object is used to create the session object.</span></span> <span data-ttu-id="c8103-149">Once the session is established, you can access the collection by using the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="c8103-149">Once the session is established, you can access the collection by using the following code snippet:</span></span>

```go
collection := session.DB("database").C("package")
```

<a id="create-document"></a>

### <a name="create-a-document"></a><span data-ttu-id="c8103-150">Create a document</span><span class="sxs-lookup"><span data-stu-id="c8103-150">Create a document</span></span>

```go
// Model
type Package struct {
    Id bson.ObjectId  `bson:"_id,omitempty"`
    FullName      string
    Description   string
    StarsCount    int
    ForksCount    int
    LastUpdatedBy string
}

// insert Document in collection
err = collection.Insert(&Package{
    FullName:"react",
    Description:"A framework for building native apps with React.",
    ForksCount: 11392,
    StarsCount:48794,
    LastUpdatedBy:"shergin",

})

if err != nil {
    log.Fatal("Problem inserting data: ", err)
    return
}
```

### <a name="query-or-read-a-document"></a><span data-ttu-id="c8103-151">Query or read a document</span><span class="sxs-lookup"><span data-stu-id="c8103-151">Query or read a document</span></span>

<span data-ttu-id="c8103-152">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span><span class="sxs-lookup"><span data-stu-id="c8103-152">Azure Cosmos DB supports rich queries against JSON documents stored in each collection.</span></span> <span data-ttu-id="c8103-153">The following sample code shows a query that you can run against the documents in your collection.</span><span class="sxs-lookup"><span data-stu-id="c8103-153">The following sample code shows a query that you can run against the documents in your collection.</span></span>

```go
// Get a Document from the collection
result := Package{}
err = collection.Find(bson.M{"fullname": "react"}).One(&result)
if err != nil {
    log.Fatal("Error finding record: ", err)
    return
}

fmt.Println("Description:", result.Description)
```


### <a name="update-a-document"></a><span data-ttu-id="c8103-154">Update a document</span><span class="sxs-lookup"><span data-stu-id="c8103-154">Update a document</span></span>

```go
// Update a document
updateQuery := bson.M{"_id": result.Id}
change := bson.M{"$set": bson.M{"fullname": "react-native"}}
err = collection.Update(updateQuery, change)
if err != nil {
    log.Fatal("Error updating record: ", err)
    return
}
```

### <a name="delete-a-document"></a><span data-ttu-id="c8103-155">Delete a document</span><span class="sxs-lookup"><span data-stu-id="c8103-155">Delete a document</span></span>

<span data-ttu-id="c8103-156">Azure Cosmos DB supports deleting JSON documents.</span><span class="sxs-lookup"><span data-stu-id="c8103-156">Azure Cosmos DB supports deleting JSON documents.</span></span>

```go
// Delete a document
query := bson.M{"_id": result.Id}
err = collection.Remove(query)
if err != nil {
   log.Fatal("Error deleting record: ", err)
   return
}
```
    
## <a name="run-the-app"></a><span data-ttu-id="c8103-157">Run the app</span><span class="sxs-lookup"><span data-stu-id="c8103-157">Run the app</span></span>

1. <span data-ttu-id="c8103-158">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include the location in which the gopkg was installed, which is USERPROFILE\go by default.</span><span class="sxs-lookup"><span data-stu-id="c8103-158">In Goglang, ensure that your GOPATH (available under **File**, **Settings**, **Go**, **GOPATH**) include the location in which the gopkg was installed, which is USERPROFILE\go by default.</span></span> 
2. <span data-ttu-id="c8103-159">Comment out the lines that delete the document, lines 103-107, so that you can see the document after running the app.</span><span class="sxs-lookup"><span data-stu-id="c8103-159">Comment out the lines that delete the document, lines 103-107, so that you can see the document after running the app.</span></span>
3. <span data-ttu-id="c8103-160">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span><span class="sxs-lookup"><span data-stu-id="c8103-160">In Goglang, click **Run**, and then click **Run 'Build main.go and run'**.</span></span>

    <span data-ttu-id="c8103-161">The app finishes and displays the description of the document created in [Create a document](#create-document).</span><span class="sxs-lookup"><span data-stu-id="c8103-161">The app finishes and displays the description of the document created in [Create a document](#create-document).</span></span>
    
    ```
    Description: A framework for building native apps with React.
    
    Process finished with exit code 0
    ```

    ![Goglang showing the output of the app](./media/create-mongodb-golang/goglang-cosmos-db.png)
    
## <a name="review-your-document-in-data-explorer"></a><span data-ttu-id="c8103-163">Review your document in Data Explorer</span><span class="sxs-lookup"><span data-stu-id="c8103-163">Review your document in Data Explorer</span></span>

<span data-ttu-id="c8103-164">Go back to the Azure portal to see your document in Data Explorer.</span><span class="sxs-lookup"><span data-stu-id="c8103-164">Go back to the Azure portal to see your document in Data Explorer.</span></span>

1. <span data-ttu-id="c8103-165">Click **Data Explorer (Preview)** in the left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span><span class="sxs-lookup"><span data-stu-id="c8103-165">Click **Data Explorer (Preview)** in the left navigation menu, expand **golang-coach**, **package**, and then click **Documents**.</span></span> <span data-ttu-id="c8103-166">In the **Documents** tab, click the \_id to display the document in the right pane.</span><span class="sxs-lookup"><span data-stu-id="c8103-166">In the **Documents** tab, click the \_id to display the document in the right pane.</span></span> 

    ![Data Explorer showing the newly created document](./media/create-mongodb-golang/golang-cosmos-db-data-explorer.png)
    
2. <span data-ttu-id="c8103-168">You can then work with the document inline and click **Update** to save it.</span><span class="sxs-lookup"><span data-stu-id="c8103-168">You can then work with the document inline and click **Update** to save it.</span></span> <span data-ttu-id="c8103-169">You can also delete the document, or create new documents or queries.</span><span class="sxs-lookup"><span data-stu-id="c8103-169">You can also delete the document, or create new documents or queries.</span></span>

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="c8103-170">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="c8103-170">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="c8103-171">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="c8103-171">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="c8103-172">Next steps</span><span class="sxs-lookup"><span data-stu-id="c8103-172">Next steps</span></span>

<span data-ttu-id="c8103-173">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a Golang app using the API for MongoDB.</span><span class="sxs-lookup"><span data-stu-id="c8103-173">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a Golang app using the API for MongoDB.</span></span> <span data-ttu-id="c8103-174">You can now import additional data to your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="c8103-174">You can now import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB for the MongoDB API](mongodb-migrate.md)
