---
title: Branching in Azure Data Factory pipeline | Microsoft Docs
description: Learn how to control flow of data in Azure Data Factory by branching and chaining activities.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: shlo
ms.openlocfilehash: b492635da55ae08f92b18dcf9c030cb23d4fa48c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871340"
---
# <a name="branching-and-chaining-activities-in-a-data-factory-pipeline"></a><span data-ttu-id="98bf8-103">Branching and chaining activities in a Data Factory pipeline</span><span class="sxs-lookup"><span data-stu-id="98bf8-103">Branching and chaining activities in a Data Factory pipeline</span></span>
<span data-ttu-id="98bf8-104">In this tutorial, you create a Data Factory pipeline that showcases some of the control flow features.</span><span class="sxs-lookup"><span data-stu-id="98bf8-104">In this tutorial, you create a Data Factory pipeline that showcases some of the control flow features.</span></span> <span data-ttu-id="98bf8-105">This pipeline does a simple copy from a container in Azure Blob Storage to another container in the same storage account.</span><span class="sxs-lookup"><span data-stu-id="98bf8-105">This pipeline does a simple copy from a container in Azure Blob Storage to another container in the same storage account.</span></span> <span data-ttu-id="98bf8-106">If the copy activity succeeds, you want to send details of the successful copy operation (such as the amount of data written) in a success email.</span><span class="sxs-lookup"><span data-stu-id="98bf8-106">If the copy activity succeeds, you want to send details of the successful copy operation (such as the amount of data written) in a success email.</span></span> <span data-ttu-id="98bf8-107">If the copy activity fails, you want to send details of copy failure (such as the error message) in a failure email.</span><span class="sxs-lookup"><span data-stu-id="98bf8-107">If the copy activity fails, you want to send details of copy failure (such as the error message) in a failure email.</span></span> <span data-ttu-id="98bf8-108">Throughout the tutorial, you see how to pass parameters.</span><span class="sxs-lookup"><span data-stu-id="98bf8-108">Throughout the tutorial, you see how to pass parameters.</span></span>

<span data-ttu-id="98bf8-109">A high-level overview of the scenario: ![Overview](media/tutorial-control-flow/overview.png)</span><span class="sxs-lookup"><span data-stu-id="98bf8-109">A high-level overview of the scenario: ![Overview](media/tutorial-control-flow/overview.png)</span></span>

<span data-ttu-id="98bf8-110">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="98bf8-110">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="98bf8-111">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="98bf8-111">Create a data factory.</span></span>
> * <span data-ttu-id="98bf8-112">Create an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="98bf8-112">Create an Azure Storage linked service.</span></span>
> * <span data-ttu-id="98bf8-113">Create an Azure Blob dataset</span><span class="sxs-lookup"><span data-stu-id="98bf8-113">Create an Azure Blob dataset</span></span>
> * <span data-ttu-id="98bf8-114">Create a pipeline that contains a copy activity and a web activity</span><span class="sxs-lookup"><span data-stu-id="98bf8-114">Create a pipeline that contains a copy activity and a web activity</span></span>
> * <span data-ttu-id="98bf8-115">Send outputs of activities to subsequent activities</span><span class="sxs-lookup"><span data-stu-id="98bf8-115">Send outputs of activities to subsequent activities</span></span>
> * <span data-ttu-id="98bf8-116">Utilize parameter passing and system variables</span><span class="sxs-lookup"><span data-stu-id="98bf8-116">Utilize parameter passing and system variables</span></span>
> * <span data-ttu-id="98bf8-117">Start a pipeline run</span><span class="sxs-lookup"><span data-stu-id="98bf8-117">Start a pipeline run</span></span>
> * <span data-ttu-id="98bf8-118">Monitor the pipeline and activity runs</span><span class="sxs-lookup"><span data-stu-id="98bf8-118">Monitor the pipeline and activity runs</span></span>

<span data-ttu-id="98bf8-119">This tutorial uses .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="98bf8-119">This tutorial uses .NET SDK.</span></span> <span data-ttu-id="98bf8-120">You can use other mechanisms to interact with Azure Data Factory, refer to "Quickstarts" in the table of contents.</span><span class="sxs-lookup"><span data-stu-id="98bf8-120">You can use other mechanisms to interact with Azure Data Factory, refer to "Quickstarts" in the table of contents.</span></span>

<span data-ttu-id="98bf8-121">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="98bf8-121">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98bf8-122">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="98bf8-122">Prerequisites</span></span>

* <span data-ttu-id="98bf8-123">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-123">**Azure Storage account**.</span></span> <span data-ttu-id="98bf8-124">You use the blob storage as **source** data store.</span><span class="sxs-lookup"><span data-stu-id="98bf8-124">You use the blob storage as **source** data store.</span></span> <span data-ttu-id="98bf8-125">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="98bf8-125">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span></span>
* <span data-ttu-id="98bf8-126">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-126">**Azure SQL Database**.</span></span> <span data-ttu-id="98bf8-127">You use the database as **sink** data store.</span><span class="sxs-lookup"><span data-stu-id="98bf8-127">You use the database as **sink** data store.</span></span> <span data-ttu-id="98bf8-128">If you don't have an Azure SQL Database, see the [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="98bf8-128">If you don't have an Azure SQL Database, see the [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article for steps to create one.</span></span>
* <span data-ttu-id="98bf8-129">**Visual Studio** 2013, 2015, or 2017.</span><span class="sxs-lookup"><span data-stu-id="98bf8-129">**Visual Studio** 2013, 2015, or 2017.</span></span> <span data-ttu-id="98bf8-130">The walkthrough in this article uses Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="98bf8-130">The walkthrough in this article uses Visual Studio 2017.</span></span>
* <span data-ttu-id="98bf8-131">**Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-131">**Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)**.</span></span>
* <span data-ttu-id="98bf8-132">**Create an application in Azure Active Directory** following [these instructions](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application).</span><span class="sxs-lookup"><span data-stu-id="98bf8-132">**Create an application in Azure Active Directory** following [these instructions](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application).</span></span> <span data-ttu-id="98bf8-133">Make note of the following values that you use in later steps: **application ID**, **authentication key**, and **tenant ID**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-133">Make note of the following values that you use in later steps: **application ID**, **authentication key**, and **tenant ID**.</span></span> <span data-ttu-id="98bf8-134">Assign application to "**Contributor**" role by following instructions in the same article.</span><span class="sxs-lookup"><span data-stu-id="98bf8-134">Assign application to "**Contributor**" role by following instructions in the same article.</span></span>

### <a name="create-blob-table"></a><span data-ttu-id="98bf8-135">Create blob table</span><span class="sxs-lookup"><span data-stu-id="98bf8-135">Create blob table</span></span>

1. <span data-ttu-id="98bf8-136">Launch Notepad.</span><span class="sxs-lookup"><span data-stu-id="98bf8-136">Launch Notepad.</span></span> <span data-ttu-id="98bf8-137">Copy the following text and save it as **input.txt** file on your disk.</span><span class="sxs-lookup"><span data-stu-id="98bf8-137">Copy the following text and save it as **input.txt** file on your disk.</span></span>

    ```
    John|Doe
    Jane|Doe
    ```
2. <span data-ttu-id="98bf8-138">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adfv2branch** container, and to upload the **input.txt** file to the container.</span><span class="sxs-lookup"><span data-stu-id="98bf8-138">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adfv2branch** container, and to upload the **input.txt** file to the container.</span></span>

## <a name="create-visual-studio-project"></a><span data-ttu-id="98bf8-139">Create Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="98bf8-139">Create Visual Studio project</span></span>

<span data-ttu-id="98bf8-140">Using Visual Studio 2015/2017, create a C# .NET console application.</span><span class="sxs-lookup"><span data-stu-id="98bf8-140">Using Visual Studio 2015/2017, create a C# .NET console application.</span></span>

1. <span data-ttu-id="98bf8-141">Launch **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-141">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="98bf8-142">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-142">Click **File**, point to **New**, and click **Project**.</span></span> <span data-ttu-id="98bf8-143">.NET version 4.5.2 or above is required.</span><span class="sxs-lookup"><span data-stu-id="98bf8-143">.NET version 4.5.2 or above is required.</span></span>
3. <span data-ttu-id="98bf8-144">Select **Visual C#** -> **Console App (.NET Framework)** from the list of project types on the right.</span><span class="sxs-lookup"><span data-stu-id="98bf8-144">Select **Visual C#** -> **Console App (.NET Framework)** from the list of project types on the right.</span></span>
4. <span data-ttu-id="98bf8-145">Enter **ADFv2BranchTutorial** for the Name.</span><span class="sxs-lookup"><span data-stu-id="98bf8-145">Enter **ADFv2BranchTutorial** for the Name.</span></span>
5. <span data-ttu-id="98bf8-146">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="98bf8-146">Click **OK** to create the project.</span></span>

## <a name="install-nuget-packages"></a><span data-ttu-id="98bf8-147">Install NuGet packages</span><span class="sxs-lookup"><span data-stu-id="98bf8-147">Install NuGet packages</span></span>

1. <span data-ttu-id="98bf8-148">Click **Tools** -> **NuGet Package Manager** -> **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-148">Click **Tools** -> **NuGet Package Manager** -> **Package Manager Console**.</span></span>
2. <span data-ttu-id="98bf8-149">In the **Package Manager Console**, run the following commands to install packages:</span><span class="sxs-lookup"><span data-stu-id="98bf8-149">In the **Package Manager Console**, run the following commands to install packages:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
    Install-Package Microsoft.Azure.Management.ResourceManager -Prerelease
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

## <a name="create-a-data-factory-client"></a><span data-ttu-id="98bf8-150">Create a data factory client</span><span class="sxs-lookup"><span data-stu-id="98bf8-150">Create a data factory client</span></span>

1. <span data-ttu-id="98bf8-151">Open **Program.cs**, include the following statements to add references to namespaces.</span><span class="sxs-lookup"><span data-stu-id="98bf8-151">Open **Program.cs**, include the following statements to add references to namespaces.</span></span>

    ```csharp
    using System;
    using System.Collections.Generic;
    using System.Linq;
    using Microsoft.Rest;
    using Microsoft.Azure.Management.ResourceManager;
    using Microsoft.Azure.Management.DataFactory;
    using Microsoft.Azure.Management.DataFactory.Models;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    ```

2. <span data-ttu-id="98bf8-152">Add these static variables to the **Program class**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-152">Add these static variables to the **Program class**.</span></span> <span data-ttu-id="98bf8-153">Replace place-holders with your own values.</span><span class="sxs-lookup"><span data-stu-id="98bf8-153">Replace place-holders with your own values.</span></span> <span data-ttu-id="98bf8-154">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="98bf8-154">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="98bf8-155">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="98bf8-155">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>

    ```csharp
        // Set variables
        static string tenantID = "<tenant ID>";
        static string applicationId = "<application ID>";
        static string authenticationKey = "<Authentication key for your application>";
        static string subscriptionId = "<Azure subscription ID>";
        static string resourceGroup = "<Azure resource group name>";

        static string region = "East US";
        static string dataFactoryName = "<Data factory name>";

        // Specify the source Azure Blob information
        static string storageAccount = "<Azure Storage account name>";
        static string storageKey = "<Azure Storage account key>";
        // confirm that you have the input.txt file placed in th input folder of the adfv2branch container. 
        static string inputBlobPath = "adfv2branch/input";
        static string inputBlobName = "input.txt";
        static string outputBlobPath = "adfv2branch/output";
        static string emailReceiver = "<specify email address of the receiver>";

        static string storageLinkedServiceName = "AzureStorageLinkedService";
        static string blobSourceDatasetName = "SourceStorageDataset";
        static string blobSinkDatasetName = "SinkStorageDataset";
        static string pipelineName = "Adfv2TutorialBranchCopy";

        static string copyBlobActivity = "CopyBlobtoBlob";
        static string sendFailEmailActivity = "SendFailEmailActivity";
        static string sendSuccessEmailActivity = "SendSuccessEmailActivity";
    
    ```

3. <span data-ttu-id="98bf8-156">Add the following code to the **Main** method that creates an instance of **DataFactoryManagementClient** class.</span><span class="sxs-lookup"><span data-stu-id="98bf8-156">Add the following code to the **Main** method that creates an instance of **DataFactoryManagementClient** class.</span></span> <span data-ttu-id="98bf8-157">You use this object to create data factory, linked service, datasets, and pipeline.</span><span class="sxs-lookup"><span data-stu-id="98bf8-157">You use this object to create data factory, linked service, datasets, and pipeline.</span></span> <span data-ttu-id="98bf8-158">You also use this object to monitor the pipeline run details.</span><span class="sxs-lookup"><span data-stu-id="98bf8-158">You also use this object to monitor the pipeline run details.</span></span>

    ```csharp
    // Authenticate and create a data factory management client
    var context = new AuthenticationContext("https://login.windows.net/" + tenantID);
    ClientCredential cc = new ClientCredential(applicationId, authenticationKey);
    AuthenticationResult result = context.AcquireTokenAsync("https://management.azure.com/", cc).Result;
    ServiceClientCredentials cred = new TokenCredentials(result.AccessToken);
    var client = new DataFactoryManagementClient(cred) { SubscriptionId = subscriptionId };
    ```

## <a name="create-a-data-factory"></a><span data-ttu-id="98bf8-159">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="98bf8-159">Create a data factory</span></span>
<span data-ttu-id="98bf8-160">Create a “CreateOrUpdateDataFactory” function in your Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="98bf8-160">Create a “CreateOrUpdateDataFactory” function in your Program.cs file:</span></span>

```csharp
static Factory CreateOrUpdateDataFactory(DataFactoryManagementClient client)
{
    Console.WriteLine("Creating data factory " + dataFactoryName + "...");
    Factory resource = new Factory
    {
        Location = region
    };
    Console.WriteLine(SafeJsonConvert.SerializeObject(resource, client.SerializationSettings));

    Factory response;
    {
        response = client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, resource);
    }

    while (client.Factories.Get(resourceGroup, dataFactoryName).ProvisioningState == "PendingCreation")
    {
        System.Threading.Thread.Sleep(1000);
    }
    return response;
}
```



<span data-ttu-id="98bf8-161">Add the following code to **Main** method that creates a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-161">Add the following code to **Main** method that creates a **data factory**.</span></span> 

```csharp
Factory df = CreateOrUpdateDataFactory(client);
```

## <a name="create-an-azure-storage-linked-service"></a><span data-ttu-id="98bf8-162">Create an Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="98bf8-162">Create an Azure Storage linked service</span></span>
<span data-ttu-id="98bf8-163">Create a “StorageLinkedServiceDefinition” function in your Program.cs file:</span><span class="sxs-lookup"><span data-stu-id="98bf8-163">Create a “StorageLinkedServiceDefinition” function in your Program.cs file:</span></span>

```csharp
static LinkedServiceResource StorageLinkedServiceDefinition(DataFactoryManagementClient client)
{
    Console.WriteLine("Creating linked service " + storageLinkedServiceName + "...");
    AzureStorageLinkedService storageLinkedService = new AzureStorageLinkedService
    {
        ConnectionString = new SecureString("DefaultEndpointsProtocol=https;AccountName=" + storageAccount + ";AccountKey=" + storageKey)
    };
    Console.WriteLine(SafeJsonConvert.SerializeObject(storageLinkedService, client.SerializationSettings));
    LinkedServiceResource linkedService = new LinkedServiceResource(storageLinkedService, name:storageLinkedServiceName);
    return linkedService;
}
```
Add the following code to the **Main** method that creates an **Azure Storage linked service**. <span data-ttu-id="98bf8-165">Learn more from [Azure Blob linked service properties](connector-azure-blob-storage.md#linked-service-properties) on supported properties and details.</span><span class="sxs-lookup"><span data-stu-id="98bf8-165">Learn more from [Azure Blob linked service properties](connector-azure-blob-storage.md#linked-service-properties) on supported properties and details.</span></span>

```csharp
client.LinkedServices.CreateOrUpdate(resourceGroup, dataFactoryName, storageLinkedServiceName, StorageLinkedServiceDefinition(client));
```

## <a name="create-datasets"></a><span data-ttu-id="98bf8-166">Create datasets</span><span class="sxs-lookup"><span data-stu-id="98bf8-166">Create datasets</span></span>

<span data-ttu-id="98bf8-167">In this section, you create two datasets: one for the source and the other for the sink.</span><span class="sxs-lookup"><span data-stu-id="98bf8-167">In this section, you create two datasets: one for the source and the other for the sink.</span></span> 

### <a name="create-a-dataset-for-source-azure-blob"></a><span data-ttu-id="98bf8-168">Create a dataset for source Azure Blob</span><span class="sxs-lookup"><span data-stu-id="98bf8-168">Create a dataset for source Azure Blob</span></span>
<span data-ttu-id="98bf8-169">Add the following code to the **Main** method that creates an **Azure blob dataset**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-169">Add the following code to the **Main** method that creates an **Azure blob dataset**.</span></span> <span data-ttu-id="98bf8-170">Learn more from [Azure Blob dataset properties](connector-azure-blob-storage.md#dataset-properties) on supported properties and details.</span><span class="sxs-lookup"><span data-stu-id="98bf8-170">Learn more from [Azure Blob dataset properties](connector-azure-blob-storage.md#dataset-properties) on supported properties and details.</span></span>

<span data-ttu-id="98bf8-171">You define a dataset that represents the source data in Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="98bf8-171">You define a dataset that represents the source data in Azure Blob.</span></span> <span data-ttu-id="98bf8-172">This Blob dataset refers to the Azure Storage linked service you create in the previous step, and describes:</span><span class="sxs-lookup"><span data-stu-id="98bf8-172">This Blob dataset refers to the Azure Storage linked service you create in the previous step, and describes:</span></span>

- <span data-ttu-id="98bf8-173">The location of the blob to copy from: **FolderPath** and **FileName**;</span><span class="sxs-lookup"><span data-stu-id="98bf8-173">The location of the blob to copy from: **FolderPath** and **FileName**;</span></span>
- <span data-ttu-id="98bf8-174">Notice the use of parameters for the FolderPath.</span><span class="sxs-lookup"><span data-stu-id="98bf8-174">Notice the use of parameters for the FolderPath.</span></span> <span data-ttu-id="98bf8-175">“sourceBlobContainer” is the name of the parameter and the expression is replaced with the values passed in the pipeline run.</span><span class="sxs-lookup"><span data-stu-id="98bf8-175">“sourceBlobContainer” is the name of the parameter and the expression is replaced with the values passed in the pipeline run.</span></span> <span data-ttu-id="98bf8-176">The syntax to define parameters is `@pipeline().parameters.<parameterName>`</span><span class="sxs-lookup"><span data-stu-id="98bf8-176">The syntax to define parameters is `@pipeline().parameters.<parameterName>`</span></span>

<span data-ttu-id="98bf8-177">Create a “SourceBlobDatasetDefinition” function in your Program.cs file</span><span class="sxs-lookup"><span data-stu-id="98bf8-177">Create a “SourceBlobDatasetDefinition” function in your Program.cs file</span></span>

```csharp
static DatasetResource SourceBlobDatasetDefinition(DataFactoryManagementClient client)
{
    Console.WriteLine("Creating dataset " + blobSourceDatasetName + "...");
    AzureBlobDataset blobDataset = new AzureBlobDataset
    { 
        FolderPath = new Expression { Value = "@pipeline().parameters.sourceBlobContainer" },
        FileName = inputBlobName,
        LinkedServiceName = new LinkedServiceReference
        {
            ReferenceName = storageLinkedServiceName
        }
    };
    Console.WriteLine(SafeJsonConvert.SerializeObject(blobDataset, client.SerializationSettings));
    DatasetResource dataset = new DatasetResource(blobDataset, name:blobSourceDatasetName);
    return dataset;
}
```

### <a name="create-a-dataset-for-sink-azure-blob"></a><span data-ttu-id="98bf8-178">Create a dataset for sink Azure Blob</span><span class="sxs-lookup"><span data-stu-id="98bf8-178">Create a dataset for sink Azure Blob</span></span>

<span data-ttu-id="98bf8-179">Create a “SourceBlobDatasetDefinition” function in your Program.cs file</span><span class="sxs-lookup"><span data-stu-id="98bf8-179">Create a “SourceBlobDatasetDefinition” function in your Program.cs file</span></span>

```csharp
static DatasetResource SinkBlobDatasetDefinition(DataFactoryManagementClient client)
{
    Console.WriteLine("Creating dataset " + blobSinkDatasetName + "...");
    AzureBlobDataset blobDataset = new AzureBlobDataset
    {
        FolderPath = new Expression { Value = "@pipeline().parameters.sinkBlobContainer" },
        LinkedServiceName = new LinkedServiceReference
        {
            ReferenceName = storageLinkedServiceName
        }
    };
    Console.WriteLine(SafeJsonConvert.SerializeObject(blobDataset, client.SerializationSettings));
    DatasetResource dataset = new DatasetResource(blobDataset, name: blobSinkDatasetName);
    return dataset;
}
```

<span data-ttu-id="98bf8-180">Add the following code to the **Main** method that creates both Azure Blob source and sink datasets.</span><span class="sxs-lookup"><span data-stu-id="98bf8-180">Add the following code to the **Main** method that creates both Azure Blob source and sink datasets.</span></span> 

```csharp
client.Datasets.CreateOrUpdate(resourceGroup, dataFactoryName, blobSourceDatasetName, SourceBlobDatasetDefinition(client));

client.Datasets.CreateOrUpdate(resourceGroup, dataFactoryName, blobSinkDatasetName, SinkBlobDatasetDefinition(client));
```

## <a name="create-a-c-class-emailrequest"></a><span data-ttu-id="98bf8-181">Create a C# class: EmailRequest</span><span class="sxs-lookup"><span data-stu-id="98bf8-181">Create a C# class: EmailRequest</span></span>
<span data-ttu-id="98bf8-182">In your C# project, create a class named **EmailRequest**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-182">In your C# project, create a class named **EmailRequest**.</span></span> <span data-ttu-id="98bf8-183">This defines what properties the pipeline sends in the body request when sending an email.</span><span class="sxs-lookup"><span data-stu-id="98bf8-183">This defines what properties the pipeline sends in the body request when sending an email.</span></span> <span data-ttu-id="98bf8-184">In this tutorial, the pipeline sends four properties from the pipeline to the email:</span><span class="sxs-lookup"><span data-stu-id="98bf8-184">In this tutorial, the pipeline sends four properties from the pipeline to the email:</span></span>

- <span data-ttu-id="98bf8-185">**Message**: body of the email.</span><span class="sxs-lookup"><span data-stu-id="98bf8-185">**Message**: body of the email.</span></span> <span data-ttu-id="98bf8-186">In the case of a successful copy, this property contains details of the run (number of data written).</span><span class="sxs-lookup"><span data-stu-id="98bf8-186">In the case of a successful copy, this property contains details of the run (number of data written).</span></span> <span data-ttu-id="98bf8-187">In the case of a failed copy, this property contains details of the error.</span><span class="sxs-lookup"><span data-stu-id="98bf8-187">In the case of a failed copy, this property contains details of the error.</span></span>
- <span data-ttu-id="98bf8-188">**Data factory name**: name of the data factory</span><span class="sxs-lookup"><span data-stu-id="98bf8-188">**Data factory name**: name of the data factory</span></span>
- <span data-ttu-id="98bf8-189">**Pipeline name**: name of the pipeline</span><span class="sxs-lookup"><span data-stu-id="98bf8-189">**Pipeline name**: name of the pipeline</span></span>
- <span data-ttu-id="98bf8-190">**Receiver**: Parameter that is passed through.</span><span class="sxs-lookup"><span data-stu-id="98bf8-190">**Receiver**: Parameter that is passed through.</span></span> <span data-ttu-id="98bf8-191">This property specifies the receiver of the email.</span><span class="sxs-lookup"><span data-stu-id="98bf8-191">This property specifies the receiver of the email.</span></span>

```csharp
    class EmailRequest
    {
        [Newtonsoft.Json.JsonProperty(PropertyName = "message")]
        public string message;

        [Newtonsoft.Json.JsonProperty(PropertyName = "dataFactoryName")]
        public string dataFactoryName;

        [Newtonsoft.Json.JsonProperty(PropertyName = "pipelineName")]
        public string pipelineName;

        [Newtonsoft.Json.JsonProperty(PropertyName = "receiver")]
        public string receiver;

        public EmailRequest(string input, string df, string pipeline, string receiverName)
        {
            message = input;
            dataFactoryName = df;
            pipelineName = pipeline;
            receiver = receiverName;
        }
    }
```
## <a name="create-email-workflow-endpoints"></a><span data-ttu-id="98bf8-192">Create email workflow endpoints</span><span class="sxs-lookup"><span data-stu-id="98bf8-192">Create email workflow endpoints</span></span>
<span data-ttu-id="98bf8-193">To trigger sending an email, you use [Logic Apps](../logic-apps/logic-apps-overview.md) to define the workflow.</span><span class="sxs-lookup"><span data-stu-id="98bf8-193">To trigger sending an email, you use [Logic Apps](../logic-apps/logic-apps-overview.md) to define the workflow.</span></span> <span data-ttu-id="98bf8-194">For details on creating a Logic App workflow, see [How to create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span><span class="sxs-lookup"><span data-stu-id="98bf8-194">For details on creating a Logic App workflow, see [How to create a logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).</span></span> 

### <a name="success-email-workflow"></a><span data-ttu-id="98bf8-195">Success email workflow</span><span class="sxs-lookup"><span data-stu-id="98bf8-195">Success email workflow</span></span> 
<span data-ttu-id="98bf8-196">Create a Logic App workflow named `CopySuccessEmail`.</span><span class="sxs-lookup"><span data-stu-id="98bf8-196">Create a Logic App workflow named `CopySuccessEmail`.</span></span> <span data-ttu-id="98bf8-197">Define the workflow trigger as `When an HTTP request is received`, and add an action of `Office 365 Outlook – Send an email`.</span><span class="sxs-lookup"><span data-stu-id="98bf8-197">Define the workflow trigger as `When an HTTP request is received`, and add an action of `Office 365 Outlook – Send an email`.</span></span>

![Success email workflow](media/tutorial-control-flow/success-email-workflow.png)

<span data-ttu-id="98bf8-199">For your request trigger, fill in the `Request Body JSON Schema` with the following JSON:</span><span class="sxs-lookup"><span data-stu-id="98bf8-199">For your request trigger, fill in the `Request Body JSON Schema` with the following JSON:</span></span>

```json
{
    "properties": {
        "dataFactoryName": {
            "type": "string"
        },
        "message": {
            "type": "string"
        },
        "pipelineName": {
            "type": "string"
        },
        "receiver": {
            "type": "string"
        }
    },
    "type": "object"
}
```
<span data-ttu-id="98bf8-200">This aligns with the **EmailRequest** class you created in the previous section.</span><span class="sxs-lookup"><span data-stu-id="98bf8-200">This aligns with the **EmailRequest** class you created in the previous section.</span></span> 

<span data-ttu-id="98bf8-201">Your Request should look like this in the Logic App Designer:</span><span class="sxs-lookup"><span data-stu-id="98bf8-201">Your Request should look like this in the Logic App Designer:</span></span>

![Logic App designer - request](media/tutorial-control-flow/logic-app-designer-request.png)

<span data-ttu-id="98bf8-203">For the **Send Email** action, customize how you wish to format the email, utilizing the properties passed in the request Body JSON schema.</span><span class="sxs-lookup"><span data-stu-id="98bf8-203">For the **Send Email** action, customize how you wish to format the email, utilizing the properties passed in the request Body JSON schema.</span></span> <span data-ttu-id="98bf8-204">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="98bf8-204">Here is an example:</span></span>

![Logic App designer - send email action](media/tutorial-control-flow/send-email-action.png)

<span data-ttu-id="98bf8-206">Make a note of your HTTP Post request URL for your success email workflow:</span><span class="sxs-lookup"><span data-stu-id="98bf8-206">Make a note of your HTTP Post request URL for your success email workflow:</span></span>

```
//Success Request Url
https://prodxxx.eastus.logic.azure.com:443/workflows/000000/triggers/manual/paths/invoke?api-version=2016-10-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=000000
```

## <a name="fail-email-workflow"></a><span data-ttu-id="98bf8-207">Fail email workflow</span><span class="sxs-lookup"><span data-stu-id="98bf8-207">Fail email workflow</span></span> 
<span data-ttu-id="98bf8-208">Clone your **CopySuccessEmail** and create another Logic Apps workflow of **CopyFailEmail**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-208">Clone your **CopySuccessEmail** and create another Logic Apps workflow of **CopyFailEmail**.</span></span> <span data-ttu-id="98bf8-209">In the request trigger, the `Request Body JSON schema` is the same.</span><span class="sxs-lookup"><span data-stu-id="98bf8-209">In the request trigger, the `Request Body JSON schema` is the same.</span></span> <span data-ttu-id="98bf8-210">Simply change the format of your email like the `Subject` to tailor toward a failure email.</span><span class="sxs-lookup"><span data-stu-id="98bf8-210">Simply change the format of your email like the `Subject` to tailor toward a failure email.</span></span> <span data-ttu-id="98bf8-211">Here is an example:</span><span class="sxs-lookup"><span data-stu-id="98bf8-211">Here is an example:</span></span>

![Logic App designer - fail email workflow](media/tutorial-control-flow/fail-email-workflow.png)

<span data-ttu-id="98bf8-213">Make a note of your HTTP Post request URL for your failure email workflow:</span><span class="sxs-lookup"><span data-stu-id="98bf8-213">Make a note of your HTTP Post request URL for your failure email workflow:</span></span>

```
//Fail Request Url
https://prodxxx.eastus.logic.azure.com:443/workflows/000000/triggers/manual/paths/invoke?api-version=2016-10-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=000000
```

<span data-ttu-id="98bf8-214">You should now have two workflow URL’s:</span><span class="sxs-lookup"><span data-stu-id="98bf8-214">You should now have two workflow URL’s:</span></span>

```
//Success Request Url
https://prodxxx.eastus.logic.azure.com:443/workflows/000000/triggers/manual/paths/invoke?api-version=2016-10-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=000000

//Fail Request Url
https://prodxxx.eastus.logic.azure.com:443/workflows/000000/triggers/manual/paths/invoke?api-version=2016-10-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=000000
```
## <a name="create-a-pipeline"></a><span data-ttu-id="98bf8-215">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="98bf8-215">Create a pipeline</span></span>
<span data-ttu-id="98bf8-216">Add the following code to the Main method that creates a pipeline with a copy activity and dependsOn property.</span><span class="sxs-lookup"><span data-stu-id="98bf8-216">Add the following code to the Main method that creates a pipeline with a copy activity and dependsOn property.</span></span> <span data-ttu-id="98bf8-217">In this tutorial, the pipeline contains one activity: copy activity, which takes in the Blob dataset as a source and another Blob dataset as a sink.</span><span class="sxs-lookup"><span data-stu-id="98bf8-217">In this tutorial, the pipeline contains one activity: copy activity, which takes in the Blob dataset as a source and another Blob dataset as a sink.</span></span> <span data-ttu-id="98bf8-218">Upon the copy activity succeeding and failing, it calls different email tasks.</span><span class="sxs-lookup"><span data-stu-id="98bf8-218">Upon the copy activity succeeding and failing, it calls different email tasks.</span></span>

<span data-ttu-id="98bf8-219">In this pipeline, you use the following features:</span><span class="sxs-lookup"><span data-stu-id="98bf8-219">In this pipeline, you use the following features:</span></span>

- <span data-ttu-id="98bf8-220">Parameters</span><span class="sxs-lookup"><span data-stu-id="98bf8-220">Parameters</span></span>
- <span data-ttu-id="98bf8-221">Web Activity</span><span class="sxs-lookup"><span data-stu-id="98bf8-221">Web Activity</span></span>
- <span data-ttu-id="98bf8-222">Activity dependency</span><span class="sxs-lookup"><span data-stu-id="98bf8-222">Activity dependency</span></span>
- <span data-ttu-id="98bf8-223">Using output from an activity as an input to the subsequent activity</span><span class="sxs-lookup"><span data-stu-id="98bf8-223">Using output from an activity as an input to the subsequent activity</span></span>

<span data-ttu-id="98bf8-224">Let’s break down the following pipeline section by section:</span><span class="sxs-lookup"><span data-stu-id="98bf8-224">Let’s break down the following pipeline section by section:</span></span>

```csharp

static PipelineResource PipelineDefinition(DataFactoryManagementClient client)
        {
            Console.WriteLine("Creating pipeline " + pipelineName + "...");
            PipelineResource resource = new PipelineResource
            {
                Parameters = new Dictionary<string, ParameterSpecification>
                {
                    { "sourceBlobContainer", new ParameterSpecification { Type = ParameterType.String } },
                    { "sinkBlobContainer", new ParameterSpecification { Type = ParameterType.String } },
                    { "receiver", new ParameterSpecification { Type = ParameterType.String } }

                },
                Activities = new List<Activity>
                {
                    new CopyActivity
                    {
                        Name = copyBlobActivity,
                        Inputs = new List<DatasetReference>
                        {
                            new DatasetReference
                            {
                                ReferenceName = blobSourceDatasetName
                            }
                        },
                        Outputs = new List<DatasetReference>
                        {
                            new DatasetReference
                            {
                                ReferenceName = blobSinkDatasetName
                            }
                        },
                        Source = new BlobSource { },
                        Sink = new BlobSink { }
                    },
                    new WebActivity
                    {
                        Name = sendSuccessEmailActivity,
                        Method = WebActivityMethod.POST,
                        Url = "https://prodxxx.eastus.logic.azure.com:443/workflows/00000000000000000000000000000000000/triggers/manual/paths/invoke?api-version=2016-10-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=0000000000000000000000000000000000000000000000",
                        Body = new EmailRequest("@{activity('CopyBlobtoBlob').output.dataWritten}", "@{pipeline().DataFactory}", "@{pipeline().Pipeline}", "@pipeline().parameters.receiver"),
                        DependsOn = new List<ActivityDependency>
                        {
                            new ActivityDependency
                            {
                                Activity = copyBlobActivity,
                                DependencyConditions = new List<String> { "Succeeded" }
                            }
                        }
                    },
                    new WebActivity
                    {
                        Name = sendFailEmailActivity,
                        Method =WebActivityMethod.POST,
                        Url = "https://prodxxx.eastus.logic.azure.com:443/workflows/000000000000000000000000000000000/triggers/manual/paths/invoke?api-version=2016-10-01&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=0000000000000000000000000000000000000000000",
                        Body = new EmailRequest("@{activity('CopyBlobtoBlob').error.message}", "@{pipeline().DataFactory}", "@{pipeline().Pipeline}", "@pipeline().parameters.receiver"),
                        DependsOn = new List<ActivityDependency>
                        {
                            new ActivityDependency
                            {
                                Activity = copyBlobActivity,
                                DependencyConditions = new List<String> { "Failed" }
                            }
                        }
                    }
                }
            };
            Console.WriteLine(SafeJsonConvert.SerializeObject(resource, client.SerializationSettings));
            return resource;
        }
```
<span data-ttu-id="98bf8-225">Add the following code to the **Main** method that creates the pipeline:</span><span class="sxs-lookup"><span data-stu-id="98bf8-225">Add the following code to the **Main** method that creates the pipeline:</span></span>

```
client.Pipelines.CreateOrUpdate(resourceGroup, dataFactoryName, pipelineName, PipelineDefinition(client));
```
### <a name="parameters"></a><span data-ttu-id="98bf8-226">Parameters</span><span class="sxs-lookup"><span data-stu-id="98bf8-226">Parameters</span></span>
<span data-ttu-id="98bf8-227">The first section of our pipeline defines parameters.</span><span class="sxs-lookup"><span data-stu-id="98bf8-227">The first section of our pipeline defines parameters.</span></span> 

- <span data-ttu-id="98bf8-228">sourceBlobContainer - parameter in the pipeline consumed by the source blob dataset.</span><span class="sxs-lookup"><span data-stu-id="98bf8-228">sourceBlobContainer - parameter in the pipeline consumed by the source blob dataset.</span></span>
- <span data-ttu-id="98bf8-229">sinkBlobContainer – parameter in the pipeline consumed by the sink blob dataset</span><span class="sxs-lookup"><span data-stu-id="98bf8-229">sinkBlobContainer – parameter in the pipeline consumed by the sink blob dataset</span></span>
- <span data-ttu-id="98bf8-230">receiver – this parameter is used by the two Web activities in the pipeline that send success or failure emails to the receiver whose email address is specified by this parameter.</span><span class="sxs-lookup"><span data-stu-id="98bf8-230">receiver – this parameter is used by the two Web activities in the pipeline that send success or failure emails to the receiver whose email address is specified by this parameter.</span></span>


```csharp
Parameters = new Dictionary<string, ParameterSpecification>
    {
        { "sourceBlobContainer", new ParameterSpecification { Type = ParameterType.String } },
        { "sinkBlobContainer", new ParameterSpecification { Type = ParameterType.String } },
        { "receiver", new ParameterSpecification { Type = ParameterType.String } }
    },
```
### <a name="web-activity"></a><span data-ttu-id="98bf8-231">Web Activity</span><span class="sxs-lookup"><span data-stu-id="98bf8-231">Web Activity</span></span>
<span data-ttu-id="98bf8-232">The Web Activity allows a call to any REST endpoint.</span><span class="sxs-lookup"><span data-stu-id="98bf8-232">The Web Activity allows a call to any REST endpoint.</span></span> <span data-ttu-id="98bf8-233">For more information about the activity, see [Web Activity](control-flow-web-activity.md).</span><span class="sxs-lookup"><span data-stu-id="98bf8-233">For more information about the activity, see [Web Activity](control-flow-web-activity.md).</span></span> <span data-ttu-id="98bf8-234">This pipeline uses a Web Activity to call the Logic Apps email workflow.</span><span class="sxs-lookup"><span data-stu-id="98bf8-234">This pipeline uses a Web Activity to call the Logic Apps email workflow.</span></span> <span data-ttu-id="98bf8-235">You create two web activities: one that calls to the **CopySuccessEmail** workflow and one that calls the **CopyFailWorkFlow**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-235">You create two web activities: one that calls to the **CopySuccessEmail** workflow and one that calls the **CopyFailWorkFlow**.</span></span>

```csharp
        new WebActivity
        {
            Name = sendCopyEmailActivity,
            Method = WebActivityMethod.POST,
            Url = "https://prodxxx.eastus.logic.azure.com:443/workflows/12345",
            Body = new EmailRequest("@{activity('CopyBlobtoBlob').output.dataWritten}", "@{pipeline().DataFactory}", "@{pipeline().Pipeline}", "@pipeline().parameters.receiver"),
            DependsOn = new List<ActivityDependency>
            {
                new ActivityDependency
                {
                    Activity = copyBlobActivity,
                    DependencyConditions = new List<String> { "Succeeded" }
                }
            }
        }
```
<span data-ttu-id="98bf8-236">In the “Url” property, paste the Request URL endpoints from your Logic Apps workflow accordingly.</span><span class="sxs-lookup"><span data-stu-id="98bf8-236">In the “Url” property, paste the Request URL endpoints from your Logic Apps workflow accordingly.</span></span> <span data-ttu-id="98bf8-237">In the “Body” property, pass an instance of the “EmailRequest” class.</span><span class="sxs-lookup"><span data-stu-id="98bf8-237">In the “Body” property, pass an instance of the “EmailRequest” class.</span></span> <span data-ttu-id="98bf8-238">The email request contains the following properties:</span><span class="sxs-lookup"><span data-stu-id="98bf8-238">The email request contains the following properties:</span></span>

- <span data-ttu-id="98bf8-239">Message – Passing value of `@{activity('CopyBlobtoBlob').output.dataWritten`.</span><span class="sxs-lookup"><span data-stu-id="98bf8-239">Message – Passing value of `@{activity('CopyBlobtoBlob').output.dataWritten`.</span></span> <span data-ttu-id="98bf8-240">Accesses a property of the previous copy activity and passes the value of dataWritten.</span><span class="sxs-lookup"><span data-stu-id="98bf8-240">Accesses a property of the previous copy activity and passes the value of dataWritten.</span></span> <span data-ttu-id="98bf8-241">For the failure case, pass the error output instead of `@{activity('CopyBlobtoBlob').error.message`.</span><span class="sxs-lookup"><span data-stu-id="98bf8-241">For the failure case, pass the error output instead of `@{activity('CopyBlobtoBlob').error.message`.</span></span>
- <span data-ttu-id="98bf8-242">Data Factory Name – Passing value of `@{pipeline().DataFactory}` This is a system variable, allowing you to access the corresponding data factory name.</span><span class="sxs-lookup"><span data-stu-id="98bf8-242">Data Factory Name – Passing value of `@{pipeline().DataFactory}` This is a system variable, allowing you to access the corresponding data factory name.</span></span> <span data-ttu-id="98bf8-243">For a list of system variables, see [System Variables](control-flow-system-variables.md) article.</span><span class="sxs-lookup"><span data-stu-id="98bf8-243">For a list of system variables, see [System Variables](control-flow-system-variables.md) article.</span></span>
- <span data-ttu-id="98bf8-244">Pipeline Name – Passing value of `@{pipeline().Pipeline}`.</span><span class="sxs-lookup"><span data-stu-id="98bf8-244">Pipeline Name – Passing value of `@{pipeline().Pipeline}`.</span></span> <span data-ttu-id="98bf8-245">This is also a system variable, allowing you to access the corresponding pipeline name.</span><span class="sxs-lookup"><span data-stu-id="98bf8-245">This is also a system variable, allowing you to access the corresponding pipeline name.</span></span> 
- <span data-ttu-id="98bf8-246">Receiver – Passing value of "\@pipeline().parameters.receiver").</span><span class="sxs-lookup"><span data-stu-id="98bf8-246">Receiver – Passing value of "\@pipeline().parameters.receiver").</span></span> <span data-ttu-id="98bf8-247">Accessing the pipeline parameters.</span><span class="sxs-lookup"><span data-stu-id="98bf8-247">Accessing the pipeline parameters.</span></span>
 
<span data-ttu-id="98bf8-248">This code creates a new Activity Dependency, depending on the previous copy activity that it succeeds.</span><span class="sxs-lookup"><span data-stu-id="98bf8-248">This code creates a new Activity Dependency, depending on the previous copy activity that it succeeds.</span></span>

## <a name="create-a-pipeline-run"></a><span data-ttu-id="98bf8-249">Create a pipeline run</span><span class="sxs-lookup"><span data-stu-id="98bf8-249">Create a pipeline run</span></span>
<span data-ttu-id="98bf8-250">Add the following code to the **Main** method that **triggers a pipeline run**.</span><span class="sxs-lookup"><span data-stu-id="98bf8-250">Add the following code to the **Main** method that **triggers a pipeline run**.</span></span>

```csharp
// Create a pipeline run
Console.WriteLine("Creating pipeline run...");
Dictionary<string, object> arguments = new Dictionary<string, object>
{
    { "sourceBlobContainer", inputBlobPath },
    { "sinkBlobContainer", outputBlobPath },
    { "receiver", emailReceiver }
};
 
CreateRunResponse runResponse = client.Pipelines.CreateRunWithHttpMessagesAsync(resourceGroup, dataFactoryName, pipelineName, arguments).Result.Body;
Console.WriteLine("Pipeline run ID: " + runResponse.RunId);
```

## <a name="main-class"></a><span data-ttu-id="98bf8-251">Main class</span><span class="sxs-lookup"><span data-stu-id="98bf8-251">Main class</span></span> 
<span data-ttu-id="98bf8-252">Your final Main method should look like this.</span><span class="sxs-lookup"><span data-stu-id="98bf8-252">Your final Main method should look like this.</span></span> <span data-ttu-id="98bf8-253">Build and run your program to trigger a pipeline run!</span><span class="sxs-lookup"><span data-stu-id="98bf8-253">Build and run your program to trigger a pipeline run!</span></span>

```csharp
// Authenticate and create a data factory management client
var context = new AuthenticationContext("https://login.windows.net/" + tenantID);
ClientCredential cc = new ClientCredential(applicationId, authenticationKey);
AuthenticationResult result = context.AcquireTokenAsync("https://management.azure.com/", cc).Result;
ServiceClientCredentials cred = new TokenCredentials(result.AccessToken);
var client = new DataFactoryManagementClient(cred) { SubscriptionId = subscriptionId };

Factory df = CreateOrUpdateDataFactory(client);

client.LinkedServices.CreateOrUpdate(resourceGroup, dataFactoryName, storageLinkedServiceName, StorageLinkedServiceDefinition(client));
client.Datasets.CreateOrUpdate(resourceGroup, dataFactoryName, blobSourceDatasetName, SourceBlobDatasetDefinition(client));
client.Datasets.CreateOrUpdate(resourceGroup, dataFactoryName, blobSinkDatasetName, SinkBlobDatasetDefinition(client));

client.Pipelines.CreateOrUpdate(resourceGroup, dataFactoryName, pipelineName, PipelineDefinition(client));

Console.WriteLine("Creating pipeline run...");
Dictionary<string, object> arguments = new Dictionary<string, object>
{
    { "sourceBlobContainer", inputBlobPath },
    { "sinkBlobContainer", outputBlobPath },
    { "receiver", emailReceiver }
};

CreateRunResponse runResponse = client.Pipelines.CreateRunWithHttpMessagesAsync(resourceGroup, dataFactoryName, pipelineName, arguments).Result.Body;
Console.WriteLine("Pipeline run ID: " + runResponse.RunId);
```

## <a name="monitor-a-pipeline-run"></a><span data-ttu-id="98bf8-254">Monitor a pipeline run</span><span class="sxs-lookup"><span data-stu-id="98bf8-254">Monitor a pipeline run</span></span>
1. <span data-ttu-id="98bf8-255">Add the following code to the **Main** method to continuously check the status of the pipeline run until it finishes copying the data.</span><span class="sxs-lookup"><span data-stu-id="98bf8-255">Add the following code to the **Main** method to continuously check the status of the pipeline run until it finishes copying the data.</span></span>

    ```csharp
    // Monitor the pipeline run
    Console.WriteLine("Checking pipeline run status...");
    PipelineRun pipelineRun;
    while (true)
    {
        pipelineRun = client.PipelineRuns.Get(resourceGroup, dataFactoryName, runResponse.RunId);
        Console.WriteLine("Status: " + pipelineRun.Status);
        if (pipelineRun.Status == "InProgress")
            System.Threading.Thread.Sleep(15000);
        else
            break;
    }
    ```

2. <span data-ttu-id="98bf8-256">Add the following code to the **Main** method that retrieves copy activity run details, for example, size of the data read/written.</span><span class="sxs-lookup"><span data-stu-id="98bf8-256">Add the following code to the **Main** method that retrieves copy activity run details, for example, size of the data read/written.</span></span>

    ```csharp
    // Check the copy activity run details
    Console.WriteLine("Checking copy activity run details...");

    List<ActivityRun> activityRuns = client.ActivityRuns.ListByPipelineRun(
    resourceGroup, dataFactoryName, runResponse.RunId, DateTime.UtcNow.AddMinutes(-10), DateTime.UtcNow.AddMinutes(10)).ToList(); 
 
    if (pipelineRun.Status == "Succeeded")
    {
        Console.WriteLine(activityRuns.First().Output);
        //SaveToJson(SafeJsonConvert.SerializeObject(activityRuns.First().Output, client.SerializationSettings), "ActivityRunResult.json", folderForJsons);
    }
    else
        Console.WriteLine(activityRuns.First().Error);

    Console.WriteLine("\nPress any key to exit...");
    Console.ReadKey();
    ```

## <a name="run-the-code"></a><span data-ttu-id="98bf8-257">Run the code</span><span class="sxs-lookup"><span data-stu-id="98bf8-257">Run the code</span></span>
<span data-ttu-id="98bf8-258">Build and start the application, then verify the pipeline execution.</span><span class="sxs-lookup"><span data-stu-id="98bf8-258">Build and start the application, then verify the pipeline execution.</span></span>
<span data-ttu-id="98bf8-259">The console prints the progress of creating data factory, linked service, datasets, pipeline, and pipeline run.</span><span class="sxs-lookup"><span data-stu-id="98bf8-259">The console prints the progress of creating data factory, linked service, datasets, pipeline, and pipeline run.</span></span> <span data-ttu-id="98bf8-260">It then checks the pipeline run status.</span><span class="sxs-lookup"><span data-stu-id="98bf8-260">It then checks the pipeline run status.</span></span> <span data-ttu-id="98bf8-261">Wait until you see the copy activity run details with data read/written size.</span><span class="sxs-lookup"><span data-stu-id="98bf8-261">Wait until you see the copy activity run details with data read/written size.</span></span> <span data-ttu-id="98bf8-262">Then, use tools such as Azure Storage explorer to check the blob(s) is copied to "outputBlobPath" from "inputBlobPath" as you specified in variables.</span><span class="sxs-lookup"><span data-stu-id="98bf8-262">Then, use tools such as Azure Storage explorer to check the blob(s) is copied to "outputBlobPath" from "inputBlobPath" as you specified in variables.</span></span>

<span data-ttu-id="98bf8-263">**Sample output:**</span><span class="sxs-lookup"><span data-stu-id="98bf8-263">**Sample output:**</span></span>

```json
Creating data factory DFTutorialTest...
{
  "location": "East US"
}
Creating linked service AzureStorageLinkedService...
{
  "type": "AzureStorage",
  "typeProperties": {
    "connectionString": {
      "type": "SecureString",
      "value": "DefaultEndpointsProtocol=https;AccountName=***;AccountKey=***"
    }
  }
}
Creating dataset SourceStorageDataset...
{
  "type": "AzureBlob",
  "typeProperties": {
    "folderPath": {
      "type": "Expression",
      "value": "@pipeline().parameters.sourceBlobContainer"
    },
    "fileName": "input.txt"
  },
  "linkedServiceName": {
    "type": "LinkedServiceReference",
    "referenceName": "AzureStorageLinkedService"
  }
}
Creating dataset SinkStorageDataset...
{
  "type": "AzureBlob",
  "typeProperties": {
    "folderPath": {
      "type": "Expression",
      "value": "@pipeline().parameters.sinkBlobContainer"
    }
  },
  "linkedServiceName": {
    "type": "LinkedServiceReference",
    "referenceName": "AzureStorageLinkedService"
  }
}
Creating pipeline Adfv2TutorialBranchCopy...
{
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
        "inputs": [
          {
            "type": "DatasetReference",
            "referenceName": "SourceStorageDataset"
          }
        ],
        "outputs": [
          {
            "type": "DatasetReference",
            "referenceName": "SinkStorageDataset"
          }
        ],
        "name": "CopyBlobtoBlob"
      },
      {
        "type": "WebActivity",
        "typeProperties": {
          "method": "POST",
          "url": "https://xxxx.eastus.logic.azure.com:443/workflows/... ",
          "body": {
            "message": "@{activity('CopyBlobtoBlob').output.dataWritten}",
            "dataFactoryName": "@{pipeline().DataFactory}",
            "pipelineName": "@{pipeline().Pipeline}",
            "receiver": "@pipeline().parameters.receiver"
          }
        },
        "name": "SendSuccessEmailActivity",
        "dependsOn": [
          {
            "activity": "CopyBlobtoBlob",
            "dependencyConditions": [
              "Succeeded"
            ]
          }
        ]
      },
      {
        "type": "WebActivity",
        "typeProperties": {
          "method": "POST",
          "url": "https://xxx.eastus.logic.azure.com:443/workflows/... ",
          "body": {
            "message": "@{activity('CopyBlobtoBlob').error.message}",
            "dataFactoryName": "@{pipeline().DataFactory}",
            "pipelineName": "@{pipeline().Pipeline}",
            "receiver": "@pipeline().parameters.receiver"
          }
        },
        "name": "SendFailEmailActivity",
        "dependsOn": [
          {
            "activity": "CopyBlobtoBlob",
            "dependencyConditions": [
              "Failed"
            ]
          }
        ]
      }
    ],
    "parameters": {
      "sourceBlobContainer": {
        "type": "String"
      },
      "sinkBlobContainer": {
        "type": "String"
      },
      "receiver": {
        "type": "String"
      }
    }
  }
}
Creating pipeline run...
Pipeline run ID: 00000000-0000-0000-0000-0000000000000
Checking pipeline run status...
Status: InProgress
Status: InProgress
Status: Succeeded
Checking copy activity run details...
{
  "dataRead": 20,
  "dataWritten": 20,
  "copyDuration": 4,
  "throughput": 0.01,
  "errors": [],
  "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (East US)"
}
{}

Press any key to exit...
```

## <a name="next-steps"></a><span data-ttu-id="98bf8-264">Next steps</span><span class="sxs-lookup"><span data-stu-id="98bf8-264">Next steps</span></span>
<span data-ttu-id="98bf8-265">You performed the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="98bf8-265">You performed the following steps in this tutorial:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="98bf8-266">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="98bf8-266">Create a data factory.</span></span>
> * <span data-ttu-id="98bf8-267">Create an Azure Storage linked service.</span><span class="sxs-lookup"><span data-stu-id="98bf8-267">Create an Azure Storage linked service.</span></span>
> * <span data-ttu-id="98bf8-268">Create an Azure Blob dataset</span><span class="sxs-lookup"><span data-stu-id="98bf8-268">Create an Azure Blob dataset</span></span>
> * <span data-ttu-id="98bf8-269">Create a pipeline that contains a copy activity and a web activity</span><span class="sxs-lookup"><span data-stu-id="98bf8-269">Create a pipeline that contains a copy activity and a web activity</span></span>
> * <span data-ttu-id="98bf8-270">Send outputs of activities to subsequent activities</span><span class="sxs-lookup"><span data-stu-id="98bf8-270">Send outputs of activities to subsequent activities</span></span>
> * <span data-ttu-id="98bf8-271">Utilize parameter passing and system variables</span><span class="sxs-lookup"><span data-stu-id="98bf8-271">Utilize parameter passing and system variables</span></span>
> * <span data-ttu-id="98bf8-272">Start a pipeline run</span><span class="sxs-lookup"><span data-stu-id="98bf8-272">Start a pipeline run</span></span>
> * <span data-ttu-id="98bf8-273">Monitor the pipeline and activity runs</span><span class="sxs-lookup"><span data-stu-id="98bf8-273">Monitor the pipeline and activity runs</span></span>

<span data-ttu-id="98bf8-274">You can now proceed to the Concepts section for more information about Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="98bf8-274">You can now proceed to the Concepts section for more information about Azure Data Factory.</span></span>
> [!div class="nextstepaction"]
>[<span data-ttu-id="98bf8-275">Pipelines and activities</span><span class="sxs-lookup"><span data-stu-id="98bf8-275">Pipelines and activities</span></span>](concepts-pipelines-activities.md)
