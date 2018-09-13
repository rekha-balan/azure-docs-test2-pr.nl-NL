---
title: Develop with Storage API in Azure Government  | Microsoft Docs
description: This provides a guide for getting started with Storage in Azure Government
services: azure-government
cloud: gov
documentationcenter: ''
author: yujhongmicrosoft
manager: zakramer
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 08/10/2018
ms.author: yujhong
ms.openlocfilehash: 5b577a9b7cfc8a19158b563b6d89f03c8bc8287f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855933"
---
# <a name="develop-with-storage-api-on-azure-government"></a><span data-ttu-id="f07cf-103">Develop with Storage API on Azure Government</span><span class="sxs-lookup"><span data-stu-id="f07cf-103">Develop with Storage API on Azure Government</span></span>

<span data-ttu-id="f07cf-104">Azure Government uses the same underlying technologies as commercial Azure, enabling you to use the development tools you’re already familiar with.</span><span class="sxs-lookup"><span data-stu-id="f07cf-104">Azure Government uses the same underlying technologies as commercial Azure, enabling you to use the development tools you’re already familiar with.</span></span>
<span data-ttu-id="f07cf-105">In order to use these services in Azure Government, you must define different endpoint mappings, as shown below for the Storage service.</span><span class="sxs-lookup"><span data-stu-id="f07cf-105">In order to use these services in Azure Government, you must define different endpoint mappings, as shown below for the Storage service.</span></span> 

<span data-ttu-id="f07cf-106">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/global-infrastructure/government/request/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f07cf-106">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/global-infrastructure/government/request/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f07cf-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f07cf-107">Prerequisites</span></span>

* <span data-ttu-id="f07cf-108">Review [Guidance for developers](documentation-government-developer-guide.md).</span><span class="sxs-lookup"><span data-stu-id="f07cf-108">Review [Guidance for developers](documentation-government-developer-guide.md).</span></span><br/> <span data-ttu-id="f07cf-109">This article discusses Azure Government's unique URLs and endpoints for managing your environment.</span><span class="sxs-lookup"><span data-stu-id="f07cf-109">This article discusses Azure Government's unique URLs and endpoints for managing your environment.</span></span> <span data-ttu-id="f07cf-110">You must know about these endpoints in order to connect to Azure Government.</span><span class="sxs-lookup"><span data-stu-id="f07cf-110">You must know about these endpoints in order to connect to Azure Government.</span></span> 
* <span data-ttu-id="f07cf-111">Review [Compare Azure Government and global Azure](compare-azure-government-global-azure.md) and click on a service of interest to see variations between Azure Government and global Azure.</span><span class="sxs-lookup"><span data-stu-id="f07cf-111">Review [Compare Azure Government and global Azure](compare-azure-government-global-azure.md) and click on a service of interest to see variations between Azure Government and global Azure.</span></span>
* <span data-ttu-id="f07cf-112">Download and install the latest version of Azure Storage Explorer [here](https://azure.microsoft.com/features/storage-explorer/).</span><span class="sxs-lookup"><span data-stu-id="f07cf-112">Download and install the latest version of Azure Storage Explorer [here](https://azure.microsoft.com/features/storage-explorer/).</span></span> 

## <a name="connecting-storage-explorer-to-azure-government"></a><span data-ttu-id="f07cf-113">Connecting Storage Explorer to Azure Government</span><span class="sxs-lookup"><span data-stu-id="f07cf-113">Connecting Storage Explorer to Azure Government</span></span>
<span data-ttu-id="f07cf-114">[The Microsoft Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) is a cross-platform tool for working with Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="f07cf-114">[The Microsoft Azure Storage Explorer](https://azure.microsoft.com/features/storage-explorer/) is a cross-platform tool for working with Azure Storage.</span></span> <span data-ttu-id="f07cf-115">Government customers will now be able to take advantage of all the latest features of the Azure Storage Explorer such as being able to create and manage blobs, queues, tables, and file shares.</span><span class="sxs-lookup"><span data-stu-id="f07cf-115">Government customers will now be able to take advantage of all the latest features of the Azure Storage Explorer such as being able to create and manage blobs, queues, tables, and file shares.</span></span>

### <a name="getting-started-with-storage-explorer"></a><span data-ttu-id="f07cf-116">Getting Started with Storage Explorer</span><span class="sxs-lookup"><span data-stu-id="f07cf-116">Getting Started with Storage Explorer</span></span>
1. <span data-ttu-id="f07cf-117">Open the Azure Storage Explorer desktop application.</span><span class="sxs-lookup"><span data-stu-id="f07cf-117">Open the Azure Storage Explorer desktop application.</span></span>

2. <span data-ttu-id="f07cf-118">You will be prompted to add an Azure account; in the dropdown choose the “Azure US Government” option:</span><span class="sxs-lookup"><span data-stu-id="f07cf-118">You will be prompted to add an Azure account; in the dropdown choose the “Azure US Government” option:</span></span>

    ![storage1](./media/documentation-government-get-started-connect-with-storage-img1.png)
3. <span data-ttu-id="f07cf-120">Log in to your Azure Government account and you will be able to see all of your resources.</span><span class="sxs-lookup"><span data-stu-id="f07cf-120">Log in to your Azure Government account and you will be able to see all of your resources.</span></span> <span data-ttu-id="f07cf-121">The Storage Explorer should look similar to the screenshot below.</span><span class="sxs-lookup"><span data-stu-id="f07cf-121">The Storage Explorer should look similar to the screenshot below.</span></span> <span data-ttu-id="f07cf-122">Click on your Storage Account to see the blob containers, file shares, Queues, and Tables.</span><span class="sxs-lookup"><span data-stu-id="f07cf-122">Click on your Storage Account to see the blob containers, file shares, Queues, and Tables.</span></span> 

    ![storage2](./media/documentation-government-get-started-connect-with-storage-img2.png)

<span data-ttu-id="f07cf-124">For more information on Azure Storage Explorer, click [here](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f07cf-124">For more information on Azure Storage Explorer, click [here](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="connecting-to-the-storage-api"></a><span data-ttu-id="f07cf-125">Connecting to the Storage API</span><span class="sxs-lookup"><span data-stu-id="f07cf-125">Connecting to the Storage API</span></span> 

### <a name="prerequisites"></a><span data-ttu-id="f07cf-126">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f07cf-126">Prerequisites</span></span>
* <span data-ttu-id="f07cf-127">Have an active Azure Government subscription.</span><span class="sxs-lookup"><span data-stu-id="f07cf-127">Have an active Azure Government subscription.</span></span>
<span data-ttu-id="f07cf-128">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/overview/clouds/government/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="f07cf-128">If you don't have an Azure Government subscription, create a [free account](https://azure.microsoft.com/overview/clouds/government/) before you begin.</span></span>
* <span data-ttu-id="f07cf-129">Download Visual Studio 2017 and [Connect to Azure Government](documentation-government-get-started-connect-with-vs.md).</span><span class="sxs-lookup"><span data-stu-id="f07cf-129">Download Visual Studio 2017 and [Connect to Azure Government](documentation-government-get-started-connect-with-vs.md).</span></span>

### <a name="getting-started-with-storage-api"></a><span data-ttu-id="f07cf-130">Getting Started with Storage API</span><span class="sxs-lookup"><span data-stu-id="f07cf-130">Getting Started with Storage API</span></span>
<span data-ttu-id="f07cf-131">One important difference to note when connecting with the Storage API is that the URL for storage is different than the URL for storage in commercial Azure – specifically, the domain ends with “core.usgovcloudapi.net”, rather than “core.windows.net”.</span><span class="sxs-lookup"><span data-stu-id="f07cf-131">One important difference to note when connecting with the Storage API is that the URL for storage is different than the URL for storage in commercial Azure – specifically, the domain ends with “core.usgovcloudapi.net”, rather than “core.windows.net”.</span></span>

<span data-ttu-id="f07cf-132">These endpoint differences must be taken into account when you connect to storage in Azure Government with C#.</span><span class="sxs-lookup"><span data-stu-id="f07cf-132">These endpoint differences must be taken into account when you connect to storage in Azure Government with C#.</span></span>
1. <span data-ttu-id="f07cf-133">Go to the [Azure Government portal](https://portal.azure.us) and select your storage account and then click the “Access Keys” tab:</span><span class="sxs-lookup"><span data-stu-id="f07cf-133">Go to the [Azure Government portal](https://portal.azure.us) and select your storage account and then click the “Access Keys” tab:</span></span>

    ![storage4](./media/documentation-government-get-started-connect-with-storage-img4.png)
2. <span data-ttu-id="f07cf-135">Copy/paste the storage account connection string.</span><span class="sxs-lookup"><span data-stu-id="f07cf-135">Copy/paste the storage account connection string.</span></span>

#### <a name="c"></a><span data-ttu-id="f07cf-136">C#</span><span class="sxs-lookup"><span data-stu-id="f07cf-136">C#</span></span> 
1. <span data-ttu-id="f07cf-137">Open up Visual Studio and create a new project.</span><span class="sxs-lookup"><span data-stu-id="f07cf-137">Open up Visual Studio and create a new project.</span></span> <span data-ttu-id="f07cf-138">Add a reference to the [WindowsAzure.Storage NuGet package](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="f07cf-138">Add a reference to the [WindowsAzure.Storage NuGet package](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span> <span data-ttu-id="f07cf-139">This NuGet package contains classes we will need to connect to your storage account.</span><span class="sxs-lookup"><span data-stu-id="f07cf-139">This NuGet package contains classes we will need to connect to your storage account.</span></span>

2. <span data-ttu-id="f07cf-140">Add these two lines of C# code to connect:</span><span class="sxs-lookup"><span data-stu-id="f07cf-140">Add these two lines of C# code to connect:</span></span>
    ```cs
    var credentials = new StorageCredentials(storageAccountName, storageAccountKey);

    var storageAccount = new CloudStorageAccount(credentials, "core.usgovcloudapi.net", useHttps: true);   
    ```

    -   <span data-ttu-id="f07cf-141">Notice on the second line we had to use a [particular constructor for the CloudStorageAccount](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount.-ctor?view=azure-dotnet) – enabling us to explicitly pass in the endpoint suffix of “core.usgovcloudapi.net”.</span><span class="sxs-lookup"><span data-stu-id="f07cf-141">Notice on the second line we had to use a [particular constructor for the CloudStorageAccount](https://docs.microsoft.com/dotnet/api/microsoft.windowsazure.storage.cloudstorageaccount.-ctor?view=azure-dotnet) – enabling us to explicitly pass in the endpoint suffix of “core.usgovcloudapi.net”.</span></span> <span data-ttu-id="f07cf-142">This constructor is the **only difference** your code requires to connect to storage in Azure Government as compared with commercial Azure.</span><span class="sxs-lookup"><span data-stu-id="f07cf-142">This constructor is the **only difference** your code requires to connect to storage in Azure Government as compared with commercial Azure.</span></span>

3. <span data-ttu-id="f07cf-143">At this point, we can interact with storage as we normally would.</span><span class="sxs-lookup"><span data-stu-id="f07cf-143">At this point, we can interact with storage as we normally would.</span></span> <span data-ttu-id="f07cf-144">For example, if we want to retrieve a specific record from our table storage we could do it like this:</span><span class="sxs-lookup"><span data-stu-id="f07cf-144">For example, if we want to retrieve a specific record from our table storage we could do it like this:</span></span>

   ```cs
    var tableClient = storageAccount.CreateCloudTableClient();

    var table = tableClient.GetTableReference("Contacts");
    var retrieveOperation = TableOperation.Retrieve<ContactEntity>("gov-partition1", "0fb52a6c-3784-4dc5-aa6d-ecda4426dbda");
    var result = await table.ExecuteAsync(retrieveOperation);
    var contact = result.Result as ContactEntity;
    Console.WriteLine($"Contact: {contact.FirstName} {contact.LastName}");
    ```

#### <a name="java"></a><span data-ttu-id="f07cf-145">Java</span><span class="sxs-lookup"><span data-stu-id="f07cf-145">Java</span></span>
1. <span data-ttu-id="f07cf-146">Download the [Azure Storage SDK for Java](https://github.com/azure/azure-storage-java) and configure your project accordingly.</span><span class="sxs-lookup"><span data-stu-id="f07cf-146">Download the [Azure Storage SDK for Java](https://github.com/azure/azure-storage-java) and configure your project accordingly.</span></span>
2. <span data-ttu-id="f07cf-147">Create a `CustomerEntity` class in your project and paste the code below:</span><span class="sxs-lookup"><span data-stu-id="f07cf-147">Create a `CustomerEntity` class in your project and paste the code below:</span></span>

    ```java
    import com.microsoft.azure.storage.table.TableServiceEntity;
    
    public class CustomerEntity extends TableServiceEntity {
            public CustomerEntity(String lastName, String firstName) {
                this.partitionKey = lastName;
                this.rowKey = firstName;
            }
    
            public CustomerEntity() { }
    
            String email;
            
            public String getEmail() {
                return this.email;
            }
    
            public void setEmail(String email) {
                this.email = email;
            }
    
        }
    ``` 
3. <span data-ttu-id="f07cf-148">Create a "test" class where we will access Azure Table Storage using the Azure Storage API.</span><span class="sxs-lookup"><span data-stu-id="f07cf-148">Create a "test" class where we will access Azure Table Storage using the Azure Storage API.</span></span> 
 <span data-ttu-id="f07cf-149">Copy and paste the code below, and **paste** your Storage Account connection string into the storageConnectionString variable.</span><span class="sxs-lookup"><span data-stu-id="f07cf-149">Copy and paste the code below, and **paste** your Storage Account connection string into the storageConnectionString variable.</span></span> 

    ```java
    import com.microsoft.azure.storage.*;
    import com.microsoft.azure.storage.table.*;
    
    public class test {

        public static final String storageConnectionString = //Paste in your Storage Account connection string

        public static void main(String[] args) {

        try
        {
            // Retrieve storage account from connection-string.
            CloudStorageAccount storageAccount =
            CloudStorageAccount.parse(storageConnectionString);

            // Create the table client.
            CloudTableClient tableClient = storageAccount.createCloudTableClient();

            // Create the table if it doesn't exist.
            String tableName = "Contacts";
            CloudTable cloudTable = tableClient.getTableReference(tableName);
            cloudTable.createIfNotExists();
            // Create a new customer entity.
            CustomerEntity customer1 = new CustomerEntity("Brown", "Walter");
            customer1.setEmail("Walter@contoso.com");

            // Create an operation to add the new customer to the people table.
            TableOperation insertCustomer1 = TableOperation.insertOrReplace(customer1);

            // Submit the operation to the table service.
            cloudTable.execute(insertCustomer1);
        }
        catch (Exception e)
        {
            // Output the stack trace.
            e.printStackTrace();
        }
      } 
    }   
    ```

#### <a name="nodejs"></a><span data-ttu-id="f07cf-150">Node.js</span><span class="sxs-lookup"><span data-stu-id="f07cf-150">Node.js</span></span>
1. <span data-ttu-id="f07cf-151">Download the [Azure Storage SDK for Node.js](../storage/blobs/storage-quickstart-blobs-nodejs.md#configure-your-storage-connection-string) and configure your application accordingly.</span><span class="sxs-lookup"><span data-stu-id="f07cf-151">Download the [Azure Storage SDK for Node.js](../storage/blobs/storage-quickstart-blobs-nodejs.md#configure-your-storage-connection-string) and configure your application accordingly.</span></span>
2. <span data-ttu-id="f07cf-152">The following code below connects to Azure Blob Storage and creates a Container using the Azure Storage API.</span><span class="sxs-lookup"><span data-stu-id="f07cf-152">The following code below connects to Azure Blob Storage and creates a Container using the Azure Storage API.</span></span> 
    <span data-ttu-id="f07cf-153">**Paste** your Azure Storage account connection string into the storageConnectionString variable below.</span><span class="sxs-lookup"><span data-stu-id="f07cf-153">**Paste** your Azure Storage account connection string into the storageConnectionString variable below.</span></span> 

    ```nodejs
    var azure = require('azure-storage');
    var storageConnectionString = //Paste Azure Storage connection string here
    var blobSvc = azure.createBlobService(storageConnectionString);
    blobSvc.createContainerIfNotExists('testing', function(error, result, response){
    if(!error){
    // Container exists and is private
    }
    });
    ```

#### <a name="python"></a><span data-ttu-id="f07cf-154">Python</span><span class="sxs-lookup"><span data-stu-id="f07cf-154">Python</span></span>
1. <span data-ttu-id="f07cf-155">Download the [Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span><span class="sxs-lookup"><span data-stu-id="f07cf-155">Download the [Azure Storage SDK for Python](https://github.com/Azure/azure-storage-python).</span></span>
2. <span data-ttu-id="f07cf-156">When using the Storage SDK for Python to connect to Azure Government, you **must separately define an "endpoint_suffix" parameter**.</span><span class="sxs-lookup"><span data-stu-id="f07cf-156">When using the Storage SDK for Python to connect to Azure Government, you **must separately define an "endpoint_suffix" parameter**.</span></span> 
    <span data-ttu-id="f07cf-157">**Paste** in your Azure storage account name and key in the placeholders below.</span><span class="sxs-lookup"><span data-stu-id="f07cf-157">**Paste** in your Azure storage account name and key in the placeholders below.</span></span>
    
    ```python
    # Create the BlockBlockService that is used to call the Blob service for the storage account
    block_blob_service = BlockBlobService(account_name='#your account name', account_key='#your account key', endpoint_suffix="core.usgovcloudapi.net") 
    container_name ='ml-gov-demo'
    generator = block_blob_service.list_blobs(container_name)
    for blob in generator:
        print(blob.name)
    ```

#### <a name="php"></a><span data-ttu-id="f07cf-158">PHP</span><span class="sxs-lookup"><span data-stu-id="f07cf-158">PHP</span></span>
1. <span data-ttu-id="f07cf-159">Download the [Azure Storage SDK for PHP](../php-download-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="f07cf-159">Download the [Azure Storage SDK for PHP](../php-download-sdk.md).</span></span>
2. <span data-ttu-id="f07cf-160">The code below accesses Azure Table Storage using the Azure Storage API.</span><span class="sxs-lookup"><span data-stu-id="f07cf-160">The code below accesses Azure Table Storage using the Azure Storage API.</span></span>
   <span data-ttu-id="f07cf-161">In the `connectionString` variable, you will notice that there is a `TableEndpoint` parameter.</span><span class="sxs-lookup"><span data-stu-id="f07cf-161">In the `connectionString` variable, you will notice that there is a `TableEndpoint` parameter.</span></span> 
   <span data-ttu-id="f07cf-162">Depending on which service you are using, you must define the parameter and set it to the endpoint for that service:</span><span class="sxs-lookup"><span data-stu-id="f07cf-162">Depending on which service you are using, you must define the parameter and set it to the endpoint for that service:</span></span>
   
    - <span data-ttu-id="f07cf-163">BlobEndpoint= //ends with 'blob.core.usgovcloudapi.net'</span><span class="sxs-lookup"><span data-stu-id="f07cf-163">BlobEndpoint= //ends with 'blob.core.usgovcloudapi.net'</span></span>
    - <span data-ttu-id="f07cf-164">QueueEndpoint= //ends with 'queue.core.usgovcloudapi.net'</span><span class="sxs-lookup"><span data-stu-id="f07cf-164">QueueEndpoint= //ends with 'queue.core.usgovcloudapi.net'</span></span>
    - <span data-ttu-id="f07cf-165">TableEndpoint= //ends with 'table.core.usgovcloudapi.net'</span><span class="sxs-lookup"><span data-stu-id="f07cf-165">TableEndpoint= //ends with 'table.core.usgovcloudapi.net'</span></span>
    >[!Note]
    > <span data-ttu-id="f07cf-166">You can find these endpoints by navigating to your Storage Account from the [portal](https://portal.azure.us).</span><span class="sxs-lookup"><span data-stu-id="f07cf-166">You can find these endpoints by navigating to your Storage Account from the [portal](https://portal.azure.us).</span></span> 
    > <span data-ttu-id="f07cf-167">**Paste** in your storage account name, key, and service endpoint in the `connectionString` variable.</span><span class="sxs-lookup"><span data-stu-id="f07cf-167">**Paste** in your storage account name, key, and service endpoint in the `connectionString` variable.</span></span> 
    >
    
    ```php
    <?php
    require_once "vendor/autoload.php";
    use WindowsAzure\Common\ServicesBuilder;
    use MicrosoftAzure\Storage\Common\ServiceException; 
    $connectionString = 'DefaultEndpointsProtocol=http;AccountName=<accountname>;AccountKey=<accountkey>;TableEndpoint=http://<storageaccountname>.table.core.usgovcloudapi.net/';

    $tableRestProxy = ServicesBuilder::getInstance()->createTableService($connectionString);
    try {
    // Create table.
    $tableRestProxy->createTable("test");
    }
    catch(ServiceException $e){
    $code = $e->getCode();
    $error_message = $e->getMessage();
    }
    ?>
    ```

## <a name="get-help-and-provide-feedback"></a><span data-ttu-id="f07cf-168">Get help and provide feedback</span><span class="sxs-lookup"><span data-stu-id="f07cf-168">Get help and provide feedback</span></span>

* <span data-ttu-id="f07cf-169">Read more about [Azure Storage](https://docs.microsoft.com/azure/storage/).</span><span class="sxs-lookup"><span data-stu-id="f07cf-169">Read more about [Azure Storage](https://docs.microsoft.com/azure/storage/).</span></span> 
* <span data-ttu-id="f07cf-170">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span><span class="sxs-lookup"><span data-stu-id="f07cf-170">Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)</span></span>
* <span data-ttu-id="f07cf-171">Get help on Stack Overflow by using the "[azure-gov](https://stackoverflow.com/questions/tagged/azure-gov)" tag</span><span class="sxs-lookup"><span data-stu-id="f07cf-171">Get help on Stack Overflow by using the "[azure-gov](https://stackoverflow.com/questions/tagged/azure-gov)" tag</span></span>
* <span data-ttu-id="f07cf-172">Give us feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span><span class="sxs-lookup"><span data-stu-id="f07cf-172">Give us feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f07cf-173">Next steps</span><span class="sxs-lookup"><span data-stu-id="f07cf-173">Next steps</span></span>

[<span data-ttu-id="f07cf-174">Develop with Visual Studio</span><span class="sxs-lookup"><span data-stu-id="f07cf-174">Develop with Visual Studio</span></span>](documentation-government-get-started-connect-with-vs.md)