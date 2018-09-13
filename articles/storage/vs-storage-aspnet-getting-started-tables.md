---
title: Get started with Azure table storage and Visual Studio Connected Services (ASP.NET) | Microsoft Docs
description: How to get started using Azure table storage in an ASP.NET project in Visual Studio after connecting to a storage account using Visual Studio Connected Services
services: storage
documentationcenter: ''
author: TomArcher
manager: douge
editor: ''
ms.assetid: af81a326-18f4-4449-bc0d-e96fba27c1f8
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/21/2016
ms.author: tarcher
ms.openlocfilehash: d2f7ceffda2cbee821472b9fb30eb70083b3d440
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549666"
---
# <a name="get-started-with-azure-table-storage-and-visual-studio-connected-services-aspnet"></a><span data-ttu-id="f4087-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f4087-103">Get started with Azure table storage and Visual Studio Connected Services (ASP.NET)</span></span>
[!INCLUDE [storage-try-azure-tools-tables](../../includes/storage-try-azure-tools-tables.md)]

## <a name="overview"></a><span data-ttu-id="f4087-104">Overview</span><span class="sxs-lookup"><span data-stu-id="f4087-104">Overview</span></span>

<span data-ttu-id="f4087-105">Azure Table storage enables you to store large amounts of structured data.</span><span class="sxs-lookup"><span data-stu-id="f4087-105">Azure Table storage enables you to store large amounts of structured data.</span></span> <span data-ttu-id="f4087-106">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="f4087-106">The service is a NoSQL datastore that accepts authenticated calls from inside and outside the Azure cloud.</span></span> <span data-ttu-id="f4087-107">Azure tables are ideal for storing structured, non-relational data.</span><span class="sxs-lookup"><span data-stu-id="f4087-107">Azure tables are ideal for storing structured, non-relational data.</span></span>

<span data-ttu-id="f4087-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure table storage entities.</span><span class="sxs-lookup"><span data-stu-id="f4087-108">This tutorial shows how to write ASP.NET code for some common scenarios using Azure table storage entities.</span></span> <span data-ttu-id="f4087-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span><span class="sxs-lookup"><span data-stu-id="f4087-109">These scenarios include creating a table, and adding, querying, and deleting table entities.</span></span> 

##<a name="prerequisites"></a><span data-ttu-id="f4087-110">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f4087-110">Prerequisites</span></span>

* [<span data-ttu-id="f4087-111">Microsoft Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f4087-111">Microsoft Visual Studio</span></span>](https://www.visualstudio.com/visual-studio-homepage-vs.aspx)
* [<span data-ttu-id="f4087-112">Azure storage account</span><span class="sxs-lookup"><span data-stu-id="f4087-112">Azure storage account</span></span>](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/vs-storage-aspnet-getting-started-create-azure-account.md)]

[!INCLUDE [storage-development-environment-include](../../includes/vs-storage-aspnet-getting-started-setup-dev-env.md)]

### <a name="create-an-mvc-controller"></a><span data-ttu-id="f4087-113">Create an MVC controller</span><span class="sxs-lookup"><span data-stu-id="f4087-113">Create an MVC controller</span></span> 

1. <span data-ttu-id="f4087-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span><span class="sxs-lookup"><span data-stu-id="f4087-114">In the **Solution Explorer**, right-click **Controllers**, and, from the context menu, select **Add->Controller**.</span></span>

    ![Add a controller to an ASP.NET MVC app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-tables/add-controller-menu.png)

1. <span data-ttu-id="f4087-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4087-116">On the **Add Scaffold** dialog, select **MVC 5 Controller - Empty**, and select **Add**.</span></span>

    ![Specify MVC controller type](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-tables/add-controller.png)

1. <span data-ttu-id="f4087-118">On the **Add Controller** dialog, name the controller *TablesController*, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4087-118">On the **Add Controller** dialog, name the controller *TablesController*, and select **Add**.</span></span>

    ![Name the MVC controller](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-tables/add-controller-name.png)

1. <span data-ttu-id="f4087-120">Add the following *using* directives to the `TablesController.cs` file:</span><span class="sxs-lookup"><span data-stu-id="f4087-120">Add the following *using* directives to the `TablesController.cs` file:</span></span>

    ```csharp
    using Microsoft.Azure;
    using Microsoft.WindowsAzure.Storage;
    using Microsoft.WindowsAzure.Storage.Auth;
    using Microsoft.WindowsAzure.Storage.Table;
    ```

### <a name="create-a-model-class"></a><span data-ttu-id="f4087-121">Create a model class</span><span class="sxs-lookup"><span data-stu-id="f4087-121">Create a model class</span></span>

<span data-ttu-id="f4087-122">Many of the examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="f4087-122">Many of the examples in this article use a **TableEntity**-derived class called **CustomerEntity**.</span></span> <span data-ttu-id="f4087-123">The following steps guide you through declaring this class as a model class:</span><span class="sxs-lookup"><span data-stu-id="f4087-123">The following steps guide you through declaring this class as a model class:</span></span>

1. <span data-ttu-id="f4087-124">In the **Solution Explorer**, right-click **Models**, and, from the context menu, select **Add->Class**.</span><span class="sxs-lookup"><span data-stu-id="f4087-124">In the **Solution Explorer**, right-click **Models**, and, from the context menu, select **Add->Class**.</span></span>

1. <span data-ttu-id="f4087-125">On the **Add New Item** dialog, name the class, **CustomerEntity**.</span><span class="sxs-lookup"><span data-stu-id="f4087-125">On the **Add New Item** dialog, name the class, **CustomerEntity**.</span></span>

1. <span data-ttu-id="f4087-126">Open the `CustomerEntity.cs` file, and add the following **using** directive:</span><span class="sxs-lookup"><span data-stu-id="f4087-126">Open the `CustomerEntity.cs` file, and add the following **using** directive:</span></span>

    ```csharp
    using Microsoft.WindowsAzure.Storage.Table;
    ```

1. <span data-ttu-id="f4087-127">Modify the class so that, when finished, the class is declared as in the following code.</span><span class="sxs-lookup"><span data-stu-id="f4087-127">Modify the class so that, when finished, the class is declared as in the following code.</span></span> <span data-ttu-id="f4087-128">The class declares an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span><span class="sxs-lookup"><span data-stu-id="f4087-128">The class declares an entity class called **CustomerEntity** that uses the customer's first name as the row key and last name as the partition key.</span></span>

    ```csharp
    public class CustomerEntity : TableEntity
    {
        public CustomerEntity(string lastName, string firstName)
        {
            this.PartitionKey = lastName;
            this.RowKey = firstName;
        }

        public CustomerEntity() { }

        public string Email { get; set; }
    }
    ```

## <a name="create-a-table"></a><span data-ttu-id="f4087-129">Create a table</span><span class="sxs-lookup"><span data-stu-id="f4087-129">Create a table</span></span>

<span data-ttu-id="f4087-130">The following steps illustrate how to create a table:</span><span class="sxs-lookup"><span data-stu-id="f4087-130">The following steps illustrate how to create a table:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="f4087-131">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="f4087-131">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span> 

1. <span data-ttu-id="f4087-132">Open the `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="f4087-132">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="f4087-133">Add a method called **CreateTable** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f4087-133">Add a method called **CreateTable** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult CreateTable()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="f4087-134">Within the **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="f4087-134">Within the **CreateTable** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f4087-135">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="f4087-135">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="f4087-136">Get a **CloudTableClient** object represents a table service client.</span><span class="sxs-lookup"><span data-stu-id="f4087-136">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="f4087-137">Get a **CloudTable** object that represents a reference to the desired table name.</span><span class="sxs-lookup"><span data-stu-id="f4087-137">Get a **CloudTable** object that represents a reference to the desired table name.</span></span> <span data-ttu-id="f4087-138">The **CloudTableClient.GetTableReference** method does not make a request against table storage.</span><span class="sxs-lookup"><span data-stu-id="f4087-138">The **CloudTableClient.GetTableReference** method does not make a request against table storage.</span></span> <span data-ttu-id="f4087-139">The reference is returned whether or not the table exists.</span><span class="sxs-lookup"><span data-stu-id="f4087-139">The reference is returned whether or not the table exists.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="f4087-140">Call the **CloudTable.CreateIfNotExists** method to create the table if it does not yet exist.</span><span class="sxs-lookup"><span data-stu-id="f4087-140">Call the **CloudTable.CreateIfNotExists** method to create the table if it does not yet exist.</span></span> <span data-ttu-id="f4087-141">The **CloudTable.CreateIfNotExists** method returns **true** if the table does not exist, and is successfully created.</span><span class="sxs-lookup"><span data-stu-id="f4087-141">The **CloudTable.CreateIfNotExists** method returns **true** if the table does not exist, and is successfully created.</span></span> <span data-ttu-id="f4087-142">Otherwise, **false** is returned.</span><span class="sxs-lookup"><span data-stu-id="f4087-142">Otherwise, **false** is returned.</span></span>    

    ```csharp
    ViewBag.Success = table.CreateIfNotExists();
    ```

1. <span data-ttu-id="f4087-143">Update the **ViewBag** with the name of the table.</span><span class="sxs-lookup"><span data-stu-id="f4087-143">Update the **ViewBag** with the name of the table.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ```

1. <span data-ttu-id="f4087-144">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="f4087-144">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f4087-145">On the **Add View** dialog, enter **CreateTable** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4087-145">On the **Add View** dialog, enter **CreateTable** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="f4087-146">Open `CreateTable.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="f4087-146">Open `CreateTable.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Create Table";
    }
    
    <h2>Create Table results</h2>

    Creation of @ViewBag.TableName @(ViewBag.Success == true ? "succeeded" : "failed")
    ```

1. <span data-ttu-id="f4087-147">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f4087-147">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f4087-148">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f4087-148">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Create table", "CreateTable", "Tables")</li>
    ```

1. <span data-ttu-id="f4087-149">Run the application, and select **Create table** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="f4087-149">Run the application, and select **Create table** to see results similar to the following screen shot:</span></span>
  
    ![Create table](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-tables/create-table-results.png)

    <span data-ttu-id="f4087-151">As mentioned previously, the **CloudTable.CreateIfNotExists** method returns **true** only when the table doesn't exist and is created.</span><span class="sxs-lookup"><span data-stu-id="f4087-151">As mentioned previously, the **CloudTable.CreateIfNotExists** method returns **true** only when the table doesn't exist and is created.</span></span> <span data-ttu-id="f4087-152">Therefore, if you run the app when the table exists, the method returns **false**.</span><span class="sxs-lookup"><span data-stu-id="f4087-152">Therefore, if you run the app when the table exists, the method returns **false**.</span></span> <span data-ttu-id="f4087-153">To run the app multiple times, you must delete the table before running the app again.</span><span class="sxs-lookup"><span data-stu-id="f4087-153">To run the app multiple times, you must delete the table before running the app again.</span></span> <span data-ttu-id="f4087-154">Deleting the table can be done via the **CloudTable.Delete** method.</span><span class="sxs-lookup"><span data-stu-id="f4087-154">Deleting the table can be done via the **CloudTable.Delete** method.</span></span> <span data-ttu-id="f4087-155">You can also delete the table using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span><span class="sxs-lookup"><span data-stu-id="f4087-155">You can also delete the table using the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040) or the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).</span></span>  

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="f4087-156">Add an entity to a table</span><span class="sxs-lookup"><span data-stu-id="f4087-156">Add an entity to a table</span></span>

<span data-ttu-id="f4087-157">*Entities* map to C\# objects by using a custom class derived from **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="f4087-157">*Entities* map to C\# objects by using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="f4087-158">To add an entity to a table, create a class that defines the properties of your entity.</span><span class="sxs-lookup"><span data-stu-id="f4087-158">To add an entity to a table, create a class that defines the properties of your entity.</span></span> <span data-ttu-id="f4087-159">In this section, you'll see how to define an entity class that uses the customer's first name as the row key and last name as the partition key.</span><span class="sxs-lookup"><span data-stu-id="f4087-159">In this section, you'll see how to define an entity class that uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="f4087-160">Together, an entity's partition and row key uniquely identify the entity in the table.</span><span class="sxs-lookup"><span data-stu-id="f4087-160">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="f4087-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span><span class="sxs-lookup"><span data-stu-id="f4087-161">Entities with the same partition key can be queried faster than entities with different partition keys, but using diverse partition keys allows for greater scalability of parallel operations.</span></span> <span data-ttu-id="f4087-162">For any property that should be stored in the table service, the property must be a public property of a supported type that exposes both setting and retrieving values.</span><span class="sxs-lookup"><span data-stu-id="f4087-162">For any property that should be stored in the table service, the property must be a public property of a supported type that exposes both setting and retrieving values.</span></span>
<span data-ttu-id="f4087-163">The entity class *must* declare a public parameter-less constructor.</span><span class="sxs-lookup"><span data-stu-id="f4087-163">The entity class *must* declare a public parameter-less constructor.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="f4087-164">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="f4087-164">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="f4087-165">Open the `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="f4087-165">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="f4087-166">Add the following directive so that the code in the `TablesController.cs` file can access the **CustomerEntity** class:</span><span class="sxs-lookup"><span data-stu-id="f4087-166">Add the following directive so that the code in the `TablesController.cs` file can access the **CustomerEntity** class:</span></span>

    ```csharp
    using StorageAspnet.Models;
    ```

1. <span data-ttu-id="f4087-167">Add a method called **AddEntity** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f4087-167">Add a method called **AddEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="f4087-168">Within the **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="f4087-168">Within the **AddEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f4087-169">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="f4087-169">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="f4087-170">Get a **CloudTableClient** object represents a table service client.</span><span class="sxs-lookup"><span data-stu-id="f4087-170">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="f4087-171">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entity.</span><span class="sxs-lookup"><span data-stu-id="f4087-171">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="f4087-172">Instantiate and initialize the **CustomerEntity** class.</span><span class="sxs-lookup"><span data-stu-id="f4087-172">Instantiate and initialize the **CustomerEntity** class.</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
    customer1.Email = "Walter@contoso.com";
    ```

1. <span data-ttu-id="f4087-173">Create a **TableOperation** object that inserts the customer entity.</span><span class="sxs-lookup"><span data-stu-id="f4087-173">Create a **TableOperation** object that inserts the customer entity.</span></span>

    ```csharp
    TableOperation insertOperation = TableOperation.Insert(customer1);
    ```

1. <span data-ttu-id="f4087-174">Execute the insert operation by calling the **CloudTable.Execute** method.</span><span class="sxs-lookup"><span data-stu-id="f4087-174">Execute the insert operation by calling the **CloudTable.Execute** method.</span></span> <span data-ttu-id="f4087-175">You can verify the result of the operation by inspecting the **TableResult.HttpStatusCode** property.</span><span class="sxs-lookup"><span data-stu-id="f4087-175">You can verify the result of the operation by inspecting the **TableResult.HttpStatusCode** property.</span></span> <span data-ttu-id="f4087-176">A status code of 2xx indicates the action requested by the client was processed successfully.</span><span class="sxs-lookup"><span data-stu-id="f4087-176">A status code of 2xx indicates the action requested by the client was processed successfully.</span></span> <span data-ttu-id="f4087-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that the operation was successfully processed and the server did not return any content.</span><span class="sxs-lookup"><span data-stu-id="f4087-177">For example, successful insertions of new entities results in an HTTP status code of 204, meaning that the operation was successfully processed and the server did not return any content.</span></span>

    ```csharp
    TableResult result = table.Execute(insertOperation);
    ```

1. <span data-ttu-id="f4087-178">Update the **ViewBag** with the table name, and the results of the insert operation.</span><span class="sxs-lookup"><span data-stu-id="f4087-178">Update the **ViewBag** with the table name, and the results of the insert operation.</span></span>

    ```csharp
    ViewBag.TableName = table.Name;
    ViewBag.Result = result.HttpStatusCode;
    ```

1. <span data-ttu-id="f4087-179">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="f4087-179">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f4087-180">On the **Add View** dialog, enter **AddEntity** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4087-180">On the **Add View** dialog, enter **AddEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="f4087-181">Open `AddEntity.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="f4087-181">Open `AddEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @{
        ViewBag.Title = "Add entity";
    }
    
    <h2>Add entity results</h2>

    Insert of entity into @ViewBag.TableName @(ViewBag.Result == 204 ? "succeeded" : "failed")
    ```
1. <span data-ttu-id="f4087-182">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f4087-182">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f4087-183">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f4087-183">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entity", "AddEntity", "Tables")</li>
    ```

1. <span data-ttu-id="f4087-184">Run the application, and select **Add entity** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="f4087-184">Run the application, and select **Add entity** to see results similar to the following screen shot:</span></span>
  
    ![Add entity](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-tables/add-entity-results.png)

    <span data-ttu-id="f4087-186">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="f4087-186">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="f4087-187">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span><span class="sxs-lookup"><span data-stu-id="f4087-187">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="add-a-batch-of-entities-to-a-table"></a><span data-ttu-id="f4087-188">Add a batch of entities to a table</span><span class="sxs-lookup"><span data-stu-id="f4087-188">Add a batch of entities to a table</span></span>

<span data-ttu-id="f4087-189">In addition to being able to [add an entity to a table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span><span class="sxs-lookup"><span data-stu-id="f4087-189">In addition to being able to [add an entity to a table one at a time](#add-an-entity-to-a-table), you can also add entities in batch.</span></span> <span data-ttu-id="f4087-190">Adding entities in batch reduces the number of round-trips between your code and the Azure table service.</span><span class="sxs-lookup"><span data-stu-id="f4087-190">Adding entities in batch reduces the number of round-trips between your code and the Azure table service.</span></span> <span data-ttu-id="f4087-191">The following steps illustrate how to add multiple entities to a table with a single insert operation:</span><span class="sxs-lookup"><span data-stu-id="f4087-191">The following steps illustrate how to add multiple entities to a table with a single insert operation:</span></span>

> [!NOTE]
> 
> <span data-ttu-id="f4087-192">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span><span class="sxs-lookup"><span data-stu-id="f4087-192">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment).</span></span>

1. <span data-ttu-id="f4087-193">Open the `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="f4087-193">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="f4087-194">Add a method called **AddEntities** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f4087-194">Add a method called **AddEntities** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult AddEntities()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="f4087-195">Within the **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="f4087-195">Within the **AddEntities** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f4087-196">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="f4087-196">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="f4087-197">Get a **CloudTableClient** object represents a table service client.</span><span class="sxs-lookup"><span data-stu-id="f4087-197">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="f4087-198">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entities.</span><span class="sxs-lookup"><span data-stu-id="f4087-198">Get a **CloudTable** object that represents a reference to the table to which you are going to add the new entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="f4087-199">Instantiate some customer objects based on the **CustomerEntity** model class presented in the section, [Add an entity to a table](#add-an-entity-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="f4087-199">Instantiate some customer objects based on the **CustomerEntity** model class presented in the section, [Add an entity to a table](#add-an-entity-to-a-table).</span></span>

    ```csharp
    CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
    customer1.Email = "Jeff@contoso.com";

    CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
    customer2.Email = "Ben@contoso.com";
    ```

1. <span data-ttu-id="f4087-200">Get a **TableBatchOperation** object.</span><span class="sxs-lookup"><span data-stu-id="f4087-200">Get a **TableBatchOperation** object.</span></span>

    ```csharp
    TableBatchOperation batchOperation = new TableBatchOperation();
    ```

1. <span data-ttu-id="f4087-201">Add entities to the batch insert operation object.</span><span class="sxs-lookup"><span data-stu-id="f4087-201">Add entities to the batch insert operation object.</span></span>

    ```csharp
    batchOperation.Insert(customer1);
    batchOperation.Insert(customer2);
    ```

1. <span data-ttu-id="f4087-202">Execute the batch insert operation by calling the **CloudTable.ExecuteBatch** method.</span><span class="sxs-lookup"><span data-stu-id="f4087-202">Execute the batch insert operation by calling the **CloudTable.ExecuteBatch** method.</span></span>   

    ```csharp
    IList<TableResult> results = table.ExecuteBatch(batchOperation);
    ```

1. <span data-ttu-id="f4087-203">The **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined to determine the success or failure of each individual operation.</span><span class="sxs-lookup"><span data-stu-id="f4087-203">The **CloudTable.ExecuteBatch** method returns a list of **TableResult** objects where each **TableResult** object can be examined to determine the success or failure of each individual operation.</span></span> <span data-ttu-id="f4087-204">For this example, pass the list to a view and let the view display the results of each operation.</span><span class="sxs-lookup"><span data-stu-id="f4087-204">For this example, pass the list to a view and let the view display the results of each operation.</span></span> 
 
    ```csharp
    return View(results);
    ```

1. <span data-ttu-id="f4087-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="f4087-205">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f4087-206">On the **Add View** dialog, enter **AddEntities** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4087-206">On the **Add View** dialog, enter **AddEntities** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="f4087-207">Open `AddEntities.cshtml`, and modify it so that it looks like the following.</span><span class="sxs-lookup"><span data-stu-id="f4087-207">Open `AddEntities.cshtml`, and modify it so that it looks like the following.</span></span>

    ```csharp
    @model IEnumerable<Microsoft.WindowsAzure.Storage.Table.TableResult>
    @{
        ViewBag.Title = "AddEntities";
    }
    
    <h2>Add-entities results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        @foreach (var result in Model)
        {
        <tr>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((result.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@result.HttpStatusCode</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="f4087-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f4087-208">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f4087-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f4087-209">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Add entities", "AddEntities", "Tables")</li>
    ```

1. <span data-ttu-id="f4087-210">Run the application, and select **Add entities** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="f4087-210">Run the application, and select **Add entities** to see results similar to the following screen shot:</span></span>
  
    ![Add entities](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-tables/add-entities-results.png)

    <span data-ttu-id="f4087-212">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span><span class="sxs-lookup"><span data-stu-id="f4087-212">You can verify that the entity was added by following the steps in the section, [Get a single entity](#get-a-single-entity).</span></span> <span data-ttu-id="f4087-213">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span><span class="sxs-lookup"><span data-stu-id="f4087-213">You can also use the [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) to view all the entities for your tables.</span></span>

## <a name="get-a-single-entity"></a><span data-ttu-id="f4087-214">Get a single entity</span><span class="sxs-lookup"><span data-stu-id="f4087-214">Get a single entity</span></span>

<span data-ttu-id="f4087-215">This section illustrates how to get a single entity from a table using the entity's row key and partition key.</span><span class="sxs-lookup"><span data-stu-id="f4087-215">This section illustrates how to get a single entity from a table using the entity's row key and partition key.</span></span> 

> [!NOTE]
> 
> <span data-ttu-id="f4087-216">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="f4087-216">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="f4087-217">Open the `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="f4087-217">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="f4087-218">Add a method called **GetSingle** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f4087-218">Add a method called **GetSingle** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetSingle()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="f4087-219">Within the **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="f4087-219">Within the **GetSingle** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f4087-220">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="f4087-220">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="f4087-221">Get a **CloudTableClient** object represents a table service client.</span><span class="sxs-lookup"><span data-stu-id="f4087-221">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="f4087-222">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entity.</span><span class="sxs-lookup"><span data-stu-id="f4087-222">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="f4087-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="f4087-223">Create a retrieve operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="f4087-224">The first parameter is the *partitionKey*, and the second parameter is the *rowKey*.</span><span class="sxs-lookup"><span data-stu-id="f4087-224">The first parameter is the *partitionKey*, and the second parameter is the *rowKey*.</span></span> <span data-ttu-id="f4087-225">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span><span class="sxs-lookup"><span data-stu-id="f4087-225">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a **CustomerEntity** entity with a *partitionKey* value of "Smith" and a *rowKey* value of "Ben":</span></span>

    ```csharp
    TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");
    ```

1. <span data-ttu-id="f4087-226">Execute the retrieve operation.</span><span class="sxs-lookup"><span data-stu-id="f4087-226">Execute the retrieve operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(retrieveOperation);
    ```

1. <span data-ttu-id="f4087-227">Pass the result to the view for display.</span><span class="sxs-lookup"><span data-stu-id="f4087-227">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="f4087-228">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="f4087-228">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f4087-229">On the **Add View** dialog, enter **GetSingle** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4087-229">On the **Add View** dialog, enter **GetSingle** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="f4087-230">Open `GetSingle.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="f4087-230">Open `GetSingle.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "GetSingle";
    }
    
    <h2>Get Single results</h2>
    
    <table border="1">
        <tr>
            <th>HTTP result</th>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        <tr>
            <td>@Model.HttpStatusCode</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).Email)</td>
        </tr>
    </table>
    ```

1. <span data-ttu-id="f4087-231">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f4087-231">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f4087-232">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f4087-232">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get single", "GetSingle", "Tables")</li>
    ```

1. <span data-ttu-id="f4087-233">Run the application, and select **Get Single** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="f4087-233">Run the application, and select **Get Single** to see results similar to the following screen shot:</span></span>
  
    ![Get single](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-tables/get-single-results.png)

## <a name="get-all-entities-in-a-partition"></a><span data-ttu-id="f4087-235">Get all entities in a partition</span><span class="sxs-lookup"><span data-stu-id="f4087-235">Get all entities in a partition</span></span>

<span data-ttu-id="f4087-236">As mentioned in the section, [Add an entity to a table](#add-an-entity-to-a-table), the combination of a partition and a row key uniquely identify an entity in a table.</span><span class="sxs-lookup"><span data-stu-id="f4087-236">As mentioned in the section, [Add an entity to a table](#add-an-entity-to-a-table), the combination of a partition and a row key uniquely identify an entity in a table.</span></span> <span data-ttu-id="f4087-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span><span class="sxs-lookup"><span data-stu-id="f4087-237">Entities with the same partition key can be queried faster than entities with different partition keys.</span></span> <span data-ttu-id="f4087-238">This section illustrates how to query a table for all the entities from a specified partition.</span><span class="sxs-lookup"><span data-stu-id="f4087-238">This section illustrates how to query a table for all the entities from a specified partition.</span></span>  

> [!NOTE]
> 
> <span data-ttu-id="f4087-239">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="f4087-239">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="f4087-240">Open the `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="f4087-240">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="f4087-241">Add a method called **GetPartition** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f4087-241">Add a method called **GetPartition** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult GetPartition()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="f4087-242">Within the **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="f4087-242">Within the **GetPartition** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f4087-243">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="f4087-243">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="f4087-244">Get a **CloudTableClient** object represents a table service client.</span><span class="sxs-lookup"><span data-stu-id="f4087-244">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="f4087-245">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entities.</span><span class="sxs-lookup"><span data-stu-id="f4087-245">Get a **CloudTable** object that represents a reference to the table from which you are retrieving the entities.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="f4087-246">Instantiate a **TableQuery** object specifying the query in the **Where** clause.</span><span class="sxs-lookup"><span data-stu-id="f4087-246">Instantiate a **TableQuery** object specifying the query in the **Where** clause.</span></span> <span data-ttu-id="f4087-247">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a all entities where the **PartitionKey** (customer's last name) has a value of "Smith":</span><span class="sxs-lookup"><span data-stu-id="f4087-247">Using the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table), the following code snippet queries the table for a all entities where the **PartitionKey** (customer's last name) has a value of "Smith":</span></span>

    ```csharp
    TableQuery<CustomerEntity> query = 
        new TableQuery<CustomerEntity>()
        .Where(TableQuery.GenerateFilterCondition("PartitionKey", QueryComparisons.Equal, "Smith"));
    ```

1. <span data-ttu-id="f4087-248">Within a loop, call the **CloudTable.ExecuteQuerySegmented** method passing the query object you instantiated in the previous step.</span><span class="sxs-lookup"><span data-stu-id="f4087-248">Within a loop, call the **CloudTable.ExecuteQuerySegmented** method passing the query object you instantiated in the previous step.</span></span>  <span data-ttu-id="f4087-249">The **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities to retrieve.</span><span class="sxs-lookup"><span data-stu-id="f4087-249">The **CloudTable.ExecuteQuerySegmented** method returns a **TableContinuationToken** object that - when **null** - indicates that there are no more entities to retrieve.</span></span> <span data-ttu-id="f4087-250">Within the loop, use another loop to iterate over the returned entities.</span><span class="sxs-lookup"><span data-stu-id="f4087-250">Within the loop, use another loop to iterate over the returned entities.</span></span> <span data-ttu-id="f4087-251">In the following code example, each returned entity is added to a list.</span><span class="sxs-lookup"><span data-stu-id="f4087-251">In the following code example, each returned entity is added to a list.</span></span> <span data-ttu-id="f4087-252">Once the loop ends, the list is passed to a view for display:</span><span class="sxs-lookup"><span data-stu-id="f4087-252">Once the loop ends, the list is passed to a view for display:</span></span> 

    ```csharp
    List<CustomerEntity> customers = new List<CustomerEntity>();
    TableContinuationToken token = null;
    do
    {
        TableQuerySegment<CustomerEntity> resultSegment = table.ExecuteQuerySegmented(query, token);
        token = resultSegment.ContinuationToken;

        foreach (CustomerEntity customer in resultSegment.Results)
        {
            customers.Add(customer);
        }
    } while (token != null);

    return View(customers);
    ```

1. <span data-ttu-id="f4087-253">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="f4087-253">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f4087-254">On the **Add View** dialog, enter **GetPartition** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4087-254">On the **Add View** dialog, enter **GetPartition** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="f4087-255">Open `GetPartition.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="f4087-255">Open `GetPartition.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @model IEnumerable<StorageAspnet.Models.CustomerEntity>
    @{
        ViewBag.Title = "GetPartition";
    }
    
    <h2>Get Partition results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>Email</th>
        </tr>
        @foreach (var customer in Model)
        {
        <tr>
            <td>@(customer.RowKey)</td>
            <td>@(customer.PartitionKey)</td>
            <td>@(customer.Email)</td>
        </tr>
        }
    </table>
    ```

1. <span data-ttu-id="f4087-256">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f4087-256">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f4087-257">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f4087-257">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Get partition", "GetPartition", "Tables")</li>
    ```

1. <span data-ttu-id="f4087-258">Run the application, and select **Get Partition** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="f4087-258">Run the application, and select **Get Partition** to see results similar to the following screen shot:</span></span>
  
    ![Get Partition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-tables/get-partition-results.png)

## <a name="delete-an-entity"></a><span data-ttu-id="f4087-260">Delete an entity</span><span class="sxs-lookup"><span data-stu-id="f4087-260">Delete an entity</span></span>

<span data-ttu-id="f4087-261">This section illustrates how to delete an entity from a table.</span><span class="sxs-lookup"><span data-stu-id="f4087-261">This section illustrates how to delete an entity from a table.</span></span>

> [!NOTE]
> 
> <span data-ttu-id="f4087-262">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="f4087-262">This section assumes you have completed the steps in [Set up the development environment](#set-up-the-development-environment), and uses data from [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> 

1. <span data-ttu-id="f4087-263">Open the `TablesController.cs` file.</span><span class="sxs-lookup"><span data-stu-id="f4087-263">Open the `TablesController.cs` file.</span></span>

1. <span data-ttu-id="f4087-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span><span class="sxs-lookup"><span data-stu-id="f4087-264">Add a method called **DeleteEntity** that returns an **ActionResult**.</span></span>

    ```csharp
    public ActionResult DeleteEntity()
    {
        // The code in this section goes here.

        return View();
    }
    ```

1. <span data-ttu-id="f4087-265">Within the **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span><span class="sxs-lookup"><span data-stu-id="f4087-265">Within the **DeleteEntity** method, get a **CloudStorageAccount** object that represents your storage account information.</span></span> <span data-ttu-id="f4087-266">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span><span class="sxs-lookup"><span data-stu-id="f4087-266">Use the following code to get the storage connection string and storage account information from the Azure service configuration: (Change *&lt;storage-account-name>* to the name of the Azure storage account you're accessing.)</span></span>
   
    ```csharp
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
       CloudConfigurationManager.GetSetting("<storage-account-name>_AzureStorageConnectionString"));
    ```

1. <span data-ttu-id="f4087-267">Get a **CloudTableClient** object represents a table service client.</span><span class="sxs-lookup"><span data-stu-id="f4087-267">Get a **CloudTableClient** object represents a table service client.</span></span>
   
    ```csharp
    CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
    ```

1. <span data-ttu-id="f4087-268">Get a **CloudTable** object that represents a reference to the table from which you are deleting the entity.</span><span class="sxs-lookup"><span data-stu-id="f4087-268">Get a **CloudTable** object that represents a reference to the table from which you are deleting the entity.</span></span> 
   
    ```csharp
    CloudTable table = tableClient.GetTableReference("TestTable");
    ```

1. <span data-ttu-id="f4087-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="f4087-269">Create a delete operation object that takes an entity object derived from **TableEntity**.</span></span> <span data-ttu-id="f4087-270">In this case, we use the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span><span class="sxs-lookup"><span data-stu-id="f4087-270">In this case, we use the **CustomerEntity** class and data presented in the section [Add a batch of entities to a table](#add-a-batch-of-entities-to-a-table).</span></span> <span data-ttu-id="f4087-271">The entity's **ETag** must be set to a valid value.</span><span class="sxs-lookup"><span data-stu-id="f4087-271">The entity's **ETag** must be set to a valid value.</span></span>  

    ```csharp
    TableOperation deleteOperation = 
        TableOperation.Delete(new CustomerEntity("Smith", "Ben") { ETag = "*" } );
    ```

1. <span data-ttu-id="f4087-272">Execute the delete operation.</span><span class="sxs-lookup"><span data-stu-id="f4087-272">Execute the delete operation.</span></span>   

    ```csharp
    TableResult result = table.Execute(deleteOperation);
    ```

1. <span data-ttu-id="f4087-273">Pass the result to the view for display.</span><span class="sxs-lookup"><span data-stu-id="f4087-273">Pass the result to the view for display.</span></span>

    ```csharp
    return View(result);
    ```

1. <span data-ttu-id="f4087-274">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span><span class="sxs-lookup"><span data-stu-id="f4087-274">In the **Solution Explorer**, expand the **Views** folder, right-click **Tables**, and from the context menu, select **Add->View**.</span></span>

1. <span data-ttu-id="f4087-275">On the **Add View** dialog, enter **DeleteEntity** for the view name, and select **Add**.</span><span class="sxs-lookup"><span data-stu-id="f4087-275">On the **Add View** dialog, enter **DeleteEntity** for the view name, and select **Add**.</span></span>

1. <span data-ttu-id="f4087-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like the following code snippet:</span><span class="sxs-lookup"><span data-stu-id="f4087-276">Open `DeleteEntity.cshtml`, and modify it so that it looks like the following code snippet:</span></span>

    ```csharp
    @model Microsoft.WindowsAzure.Storage.Table.TableResult
    @{
        ViewBag.Title = "DeleteEntity";
    }
    
    <h2>Delete Entity results</h2>
    
    <table border="1">
        <tr>
            <th>First name</th>
            <th>Last name</th>
            <th>HTTP result</th>
        </tr>
        <tr>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).RowKey)</td>
            <td>@((Model.Result as StorageAspnet.Models.CustomerEntity).PartitionKey)</td>
            <td>@Model.HttpStatusCode</td>
        </tr>
    </table>

    ```

1. <span data-ttu-id="f4087-277">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span><span class="sxs-lookup"><span data-stu-id="f4087-277">In the **Solution Explorer**, expand the **Views->Shared** folder, and open `_Layout.cshtml`.</span></span>

1. <span data-ttu-id="f4087-278">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span><span class="sxs-lookup"><span data-stu-id="f4087-278">After the last **Html.ActionLink**, add the following **Html.ActionLink**:</span></span>

    ```html
    <li>@Html.ActionLink("Delete entity", "DeleteEntity", "Tables")</li>
    ```

1. <span data-ttu-id="f4087-279">Run the application, and select **Delete entity** to see results similar to the following screen shot:</span><span class="sxs-lookup"><span data-stu-id="f4087-279">Run the application, and select **Delete entity** to see results similar to the following screen shot:</span></span>
  
    ![Get single](https://docstestmedia1.blob.core.windows.net/azure-media/articles/storage/media/vs-storage-aspnet-getting-started-tables/delete-entity-results.png)

## <a name="next-steps"></a><span data-ttu-id="f4087-281">Next steps</span><span class="sxs-lookup"><span data-stu-id="f4087-281">Next steps</span></span>
<span data-ttu-id="f4087-282">View more feature guides to learn about additional options for storing data in Azure.</span><span class="sxs-lookup"><span data-stu-id="f4087-282">View more feature guides to learn about additional options for storing data in Azure.</span></span>

  * [<span data-ttu-id="f4087-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f4087-283">Get started with Azure blob storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-blobs.md)
  * [<span data-ttu-id="f4087-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span><span class="sxs-lookup"><span data-stu-id="f4087-284">Get started with Azure queue storage and Visual Studio Connected Services (ASP.NET)</span></span>](./vs-storage-aspnet-getting-started-queues.md)








