---
title: 'Azure Cosmos DB: Build a Flask web app with Python and the Azure Cosmos DB MongoDB API | Microsoft Docs'
description: Presents a Python Flask code sample you can use to connect to and query the Azure Cosmos DB MongoDB API
services: cosmos-db
author: slyons
manager: kfile
ms.service: cosmos-db
ms.component: cosmosdb-mongo
ms.custom: quick start connect, mvc
ms.devlang: python
ms.topic: quickstart
ms.date: 10/2/2017
ms.author: sclyon
ms.openlocfilehash: faba9b2999445152f700ddfa1a7e56983cbb03f4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965857"
---
# <a name="azure-cosmos-db-build-a-flask-app-with-the-mongodb-api"></a><span data-ttu-id="ff538-103">Azure Cosmos DB: Build a Flask app with the MongoDB API</span><span class="sxs-lookup"><span data-stu-id="ff538-103">Azure Cosmos DB: Build a Flask app with the MongoDB API</span></span>

> [!div class="op_single_selector"]
> * [.NET](create-mongodb-dotnet.md)
> * [Java](create-mongodb-java.md)
> * [Node.js](create-mongodb-nodejs.md)
> * [Python](create-mongodb-flask.md)
> * [Xamarin](create-mongodb-xamarin.md)
> * [Golang](create-mongodb-golang.md)
>  

<span data-ttu-id="ff538-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span><span class="sxs-lookup"><span data-stu-id="ff538-110">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="ff538-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ff538-111">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="ff538-112">This quick start guide, uses the following [Flask example](https://github.com/Azure-Samples/CosmosDB-Flask-Mongo-Sample) and demonstrates how to build a simple To-Do Flask app with the [Azure Cosmos DB Emulator](local-emulator.md) and the Azure Cosmos DB [MongoDB API](mongodb-introduction.md) instead of MongoDB.</span><span class="sxs-lookup"><span data-stu-id="ff538-112">This quick start guide, uses the following [Flask example](https://github.com/Azure-Samples/CosmosDB-Flask-Mongo-Sample) and demonstrates how to build a simple To-Do Flask app with the [Azure Cosmos DB Emulator](local-emulator.md) and the Azure Cosmos DB [MongoDB API](mongodb-introduction.md) instead of MongoDB.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ff538-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ff538-113">Prerequisites</span></span>

- <span data-ttu-id="ff538-114">Download the [Azure Cosmos DB Emulator](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="ff538-114">Download the [Azure Cosmos DB Emulator](local-emulator.md).</span></span> <span data-ttu-id="ff538-115">The emulator is currently only supported on Windows.</span><span class="sxs-lookup"><span data-stu-id="ff538-115">The emulator is currently only supported on Windows.</span></span> <span data-ttu-id="ff538-116">The sample shows how to use the sample with a production key from Azure, which can be done on any platform.</span><span class="sxs-lookup"><span data-stu-id="ff538-116">The sample shows how to use the sample with a production key from Azure, which can be done on any platform.</span></span>

- <span data-ttu-id="ff538-117">If you don’t already have Visual Studio Code installed, you can quickly install [VS Code](https://code.visualstudio.com/Download) for your platform (Windows, Mac, Linux).</span><span class="sxs-lookup"><span data-stu-id="ff538-117">If you don’t already have Visual Studio Code installed, you can quickly install [VS Code](https://code.visualstudio.com/Download) for your platform (Windows, Mac, Linux).</span></span>

- <span data-ttu-id="ff538-118">Be sure to add Python Language support by installing one of the popular Python extensions.</span><span class="sxs-lookup"><span data-stu-id="ff538-118">Be sure to add Python Language support by installing one of the popular Python extensions.</span></span>
    1. <span data-ttu-id="ff538-119">Select an extension.</span><span class="sxs-lookup"><span data-stu-id="ff538-119">Select an extension.</span></span>
    2. <span data-ttu-id="ff538-120">Install the extension by typing `ext install` into the Command Palette `Ctrl+Shift+P`.</span><span class="sxs-lookup"><span data-stu-id="ff538-120">Install the extension by typing `ext install` into the Command Palette `Ctrl+Shift+P`.</span></span>

    <span data-ttu-id="ff538-121">The examples in this document use Don Jayamanne's popular and full featured [Python Extension](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python).</span><span class="sxs-lookup"><span data-stu-id="ff538-121">The examples in this document use Don Jayamanne's popular and full featured [Python Extension](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python).</span></span>

## <a name="clone-the-sample-application"></a><span data-ttu-id="ff538-122">Clone the sample application</span><span class="sxs-lookup"><span data-stu-id="ff538-122">Clone the sample application</span></span>

<span data-ttu-id="ff538-123">Now let's clone a Flask-MongoDB API app from github, set the connection string, and run it.</span><span class="sxs-lookup"><span data-stu-id="ff538-123">Now let's clone a Flask-MongoDB API app from github, set the connection string, and run it.</span></span> <span data-ttu-id="ff538-124">You see how easy it is to work with data programmatically.</span><span class="sxs-lookup"><span data-stu-id="ff538-124">You see how easy it is to work with data programmatically.</span></span>

1. <span data-ttu-id="ff538-125">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span><span class="sxs-lookup"><span data-stu-id="ff538-125">Open a command prompt, create a new folder named git-samples, then close the command prompt.</span></span>

    ```bash
    md "C:\git-samples"
    ```

2. <span data-ttu-id="ff538-126">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span><span class="sxs-lookup"><span data-stu-id="ff538-126">Open a git terminal window, such as git bash, and use the `cd` command to change to the new folder to install the sample app.</span></span>

    ```bash
    cd "C:\git-samples"
    ```

3. <span data-ttu-id="ff538-127">Run the following command to clone the sample repository.</span><span class="sxs-lookup"><span data-stu-id="ff538-127">Run the following command to clone the sample repository.</span></span> <span data-ttu-id="ff538-128">This command creates a copy of the sample app on your computer.</span><span class="sxs-lookup"><span data-stu-id="ff538-128">This command creates a copy of the sample app on your computer.</span></span>

    ```bash
    git clone https://github.com/Azure-Samples/CosmosDB-Flask-Mongo-Sample.git
    ```
3. <span data-ttu-id="ff538-129">Run the following command to install the python modules.</span><span class="sxs-lookup"><span data-stu-id="ff538-129">Run the following command to install the python modules.</span></span>

    ```bash 
    pip install -r .\requirements.txt
    ```
4. <span data-ttu-id="ff538-130">Open the folder in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="ff538-130">Open the folder in Visual Studio Code.</span></span>

## <a name="review-the-code"></a><span data-ttu-id="ff538-131">Review the code</span><span class="sxs-lookup"><span data-stu-id="ff538-131">Review the code</span></span>

<span data-ttu-id="ff538-132">This step is optional.</span><span class="sxs-lookup"><span data-stu-id="ff538-132">This step is optional.</span></span> <span data-ttu-id="ff538-133">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span><span class="sxs-lookup"><span data-stu-id="ff538-133">If you're interested in learning how the database resources are created in the code, you can review the following snippets.</span></span> <span data-ttu-id="ff538-134">Otherwise, you can skip ahead to [Run the web app](#run-the-web-app).</span><span class="sxs-lookup"><span data-stu-id="ff538-134">Otherwise, you can skip ahead to [Run the web app](#run-the-web-app).</span></span> 

<span data-ttu-id="ff538-135">The following snippets are all taken from the app.py file and uses the connection string for the local Azure Cosmos DB Emulator.</span><span class="sxs-lookup"><span data-stu-id="ff538-135">The following snippets are all taken from the app.py file and uses the connection string for the local Azure Cosmos DB Emulator.</span></span> <span data-ttu-id="ff538-136">The password needs to be split up as seen below to accommodate for the forward slashes that cannot be parsed otherwise.</span><span class="sxs-lookup"><span data-stu-id="ff538-136">The password needs to be split up as seen below to accommodate for the forward slashes that cannot be parsed otherwise.</span></span>

* <span data-ttu-id="ff538-137">Initialize the MongoDB client, retrieve the database, and authenticate.</span><span class="sxs-lookup"><span data-stu-id="ff538-137">Initialize the MongoDB client, retrieve the database, and authenticate.</span></span>

    ```python
    client = MongoClient("mongodb://127.0.0.1:10250/?ssl=true") #host uri
    db = client.test    #Select the database
    db.authenticate(name="localhost",password='C2y6yDjf5' + r'/R' + '+ob0N8A7Cgv30VRDJIWEHLM+4QDU5DE2nQ9nDuVTqobD4b8mGGyPMbIZnqyMsEcaGQy67XIw' + r'/Jw==')
    ```

* <span data-ttu-id="ff538-138">Retrieve the collection or create it if it does not already exist.</span><span class="sxs-lookup"><span data-stu-id="ff538-138">Retrieve the collection or create it if it does not already exist.</span></span>

    ```python
    todos = db.todo #Select the collection
    ```

* <span data-ttu-id="ff538-139">Create the app</span><span class="sxs-lookup"><span data-stu-id="ff538-139">Create the app</span></span>

    ```Python
    app = Flask(__name__)
    title = "TODO with Flask"
    heading = "ToDo Reminder"
    ```
    
## <a name="run-the-web-app"></a><span data-ttu-id="ff538-140">Run the web app</span><span class="sxs-lookup"><span data-stu-id="ff538-140">Run the web app</span></span>

1. <span data-ttu-id="ff538-141">Make sure the Azure Cosmos DB Emulator is running.</span><span class="sxs-lookup"><span data-stu-id="ff538-141">Make sure the Azure Cosmos DB Emulator is running.</span></span>

2. <span data-ttu-id="ff538-142">Open a terminal window and `cd` to the directory that the app is saved in.</span><span class="sxs-lookup"><span data-stu-id="ff538-142">Open a terminal window and `cd` to the directory that the app is saved in.</span></span>

3. <span data-ttu-id="ff538-143">Then set the environment variable for the Flask app with `set FLASK_APP=app.py` or `export FLASK_APP=app.py` if you are using a Mac.</span><span class="sxs-lookup"><span data-stu-id="ff538-143">Then set the environment variable for the Flask app with `set FLASK_APP=app.py` or `export FLASK_APP=app.py` if you are using a Mac.</span></span>

4. <span data-ttu-id="ff538-144">Run the app with `flask run` and browse to [http://127.0.0.1:5000/](http://127.0.0.1:5000/).</span><span class="sxs-lookup"><span data-stu-id="ff538-144">Run the app with `flask run` and browse to [http://127.0.0.1:5000/](http://127.0.0.1:5000/).</span></span>

5. <span data-ttu-id="ff538-145">Add and remove tasks and see them added and changed in the collection.</span><span class="sxs-lookup"><span data-stu-id="ff538-145">Add and remove tasks and see them added and changed in the collection.</span></span>

## <a name="create-a-database-account"></a><span data-ttu-id="ff538-146">Create a database account</span><span class="sxs-lookup"><span data-stu-id="ff538-146">Create a database account</span></span>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount-mongodb.md)]

## <a name="update-your-connection-string"></a><span data-ttu-id="ff538-147">Update your connection string</span><span class="sxs-lookup"><span data-stu-id="ff538-147">Update your connection string</span></span>

<span data-ttu-id="ff538-148">If you want to test the code against a live Azure Cosmos DB Account, go to the Azure portal to create an account and get your connection string information.</span><span class="sxs-lookup"><span data-stu-id="ff538-148">If you want to test the code against a live Azure Cosmos DB Account, go to the Azure portal to create an account and get your connection string information.</span></span> <span data-ttu-id="ff538-149">Then copy it into the app.</span><span class="sxs-lookup"><span data-stu-id="ff538-149">Then copy it into the app.</span></span>

1. <span data-ttu-id="ff538-150">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span><span class="sxs-lookup"><span data-stu-id="ff538-150">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Connection String**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="ff538-151">You'll use the copy buttons on the right side of the screen to copy the Username, Password, and Host into the Dal.cs file in the next step.</span><span class="sxs-lookup"><span data-stu-id="ff538-151">You'll use the copy buttons on the right side of the screen to copy the Username, Password, and Host into the Dal.cs file in the next step.</span></span>

2. <span data-ttu-id="ff538-152">Open the **app.py** file in the root directory.</span><span class="sxs-lookup"><span data-stu-id="ff538-152">Open the **app.py** file in the root directory.</span></span>

3. <span data-ttu-id="ff538-153">Copy your **username** value from the portal (using the copy button) and make it the value of the **name** in your **app.py** file.</span><span class="sxs-lookup"><span data-stu-id="ff538-153">Copy your **username** value from the portal (using the copy button) and make it the value of the **name** in your **app.py** file.</span></span>

4. <span data-ttu-id="ff538-154">Then copy your **connection string** value from the portal and make it the value of the MongoClient in your **app.py** file.</span><span class="sxs-lookup"><span data-stu-id="ff538-154">Then copy your **connection string** value from the portal and make it the value of the MongoClient in your **app.py** file.</span></span>

5. <span data-ttu-id="ff538-155">Finally copy your **password** value from the portal and make it the value of the **password** in your **app.py** file.</span><span class="sxs-lookup"><span data-stu-id="ff538-155">Finally copy your **password** value from the portal and make it the value of the **password** in your **app.py** file.</span></span>

<span data-ttu-id="ff538-156">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="ff538-156">You've now updated your app with all the info it needs to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="ff538-157">You can run it the same way as before.</span><span class="sxs-lookup"><span data-stu-id="ff538-157">You can run it the same way as before.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="ff538-158">Deploy to Azure</span><span class="sxs-lookup"><span data-stu-id="ff538-158">Deploy to Azure</span></span>

<span data-ttu-id="ff538-159">To deploy this app, you can create a new web app in Azure and enable continuous deployment with a fork of this github repo.</span><span class="sxs-lookup"><span data-stu-id="ff538-159">To deploy this app, you can create a new web app in Azure and enable continuous deployment with a fork of this github repo.</span></span> <span data-ttu-id="ff538-160">Follow this [tutorial](https://docs.microsoft.com/azure/app-service-web/app-service-continuous-deployment) to set up continuous deployment with Github in Azure.</span><span class="sxs-lookup"><span data-stu-id="ff538-160">Follow this [tutorial](https://docs.microsoft.com/azure/app-service-web/app-service-continuous-deployment) to set up continuous deployment with Github in Azure.</span></span>

<span data-ttu-id="ff538-161">When deploying to Azure, you should remove your application keys and make sure the section below is not commented out:</span><span class="sxs-lookup"><span data-stu-id="ff538-161">When deploying to Azure, you should remove your application keys and make sure the section below is not commented out:</span></span>

```python
    client = MongoClient(os.getenv("MONGOURL"))
    db = client.test    #Select the database
    db.authenticate(name=os.getenv("MONGO_USERNAME"),password=os.getenv("MONGO_PASSWORD"))
```

<span data-ttu-id="ff538-162">You then need to add your MONGOURL, MONGO_PASSWORD, and MONGO_USERNAME to the application settings.</span><span class="sxs-lookup"><span data-stu-id="ff538-162">You then need to add your MONGOURL, MONGO_PASSWORD, and MONGO_USERNAME to the application settings.</span></span> <span data-ttu-id="ff538-163">You can follow this [tutorial](https://docs.microsoft.com/azure/app-service-web/web-sites-configure#application-settings) to learn more about Application Settings in Azure Web Apps.</span><span class="sxs-lookup"><span data-stu-id="ff538-163">You can follow this [tutorial](https://docs.microsoft.com/azure/app-service-web/web-sites-configure#application-settings) to learn more about Application Settings in Azure Web Apps.</span></span>

<span data-ttu-id="ff538-164">If you don't want to create a fork of this repo, you can also click the deploy to Azure button below.</span><span class="sxs-lookup"><span data-stu-id="ff538-164">If you don't want to create a fork of this repo, you can also click the deploy to Azure button below.</span></span> <span data-ttu-id="ff538-165">You should then go into Azure and set up the application settings with your Cosmos DB account info.</span><span class="sxs-lookup"><span data-stu-id="ff538-165">You should then go into Azure and set up the application settings with your Cosmos DB account info.</span></span>

<a href="https://deploy.azure.com/?repository=https://github.com/heatherbshapiro/To-Do-List---Flask-MongoDB-Example" target="_blank">
<img src="http://azuredeploy.net/deploybutton.png"/>
</a>

> [!NOTE]
> If you plan to store your code in Github or other source control options, please be sure to remove your connection strings from the code. They can be set with application settings for the web app instead.

## <a name="review-slas-in-the-azure-portal"></a><span data-ttu-id="ff538-168">Review SLAs in the Azure portal</span><span class="sxs-lookup"><span data-stu-id="ff538-168">Review SLAs in the Azure portal</span></span>

[!INCLUDE [cosmosdb-tutorial-review-slas](../../includes/cosmos-db-tutorial-review-slas.md)]

## <a name="clean-up-resources"></a><span data-ttu-id="ff538-169">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="ff538-169">Clean up resources</span></span>

[!INCLUDE [cosmosdb-delete-resource-group](../../includes/cosmos-db-delete-resource-group.md)]

## <a name="next-steps"></a><span data-ttu-id="ff538-170">Next steps</span><span class="sxs-lookup"><span data-stu-id="ff538-170">Next steps</span></span>

<span data-ttu-id="ff538-171">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a Flask app using the API for MongoDB.You can now import additional data to your Cosmos DB account.</span><span class="sxs-lookup"><span data-stu-id="ff538-171">In this quickstart, you've learned how to create an Azure Cosmos DB account and run a Flask app using the API for MongoDB.You can now import additional data to your Cosmos DB account.</span></span>

> [!div class="nextstepaction"]
> [Import data into Azure Cosmos DB for the MongoDB API](mongodb-migrate.md)
