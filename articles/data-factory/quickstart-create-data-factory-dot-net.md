---
title: Create an Azure data factory using .NET | Microsoft Docs
description: Create an Azure data factory to copy data from one location in Azure Blob storage to another location.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: ''
ms.devlang: dotnet
ms.topic: quickstart
ms.date: 03/28/2018
ms.author: jingwang
ms.openlocfilehash: a7916a434552cbcb999f1e69c7a5bc2419f517fb
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864606"
---
# <a name="create-a-data-factory-and-pipeline-using-net-sdk"></a><span data-ttu-id="347f7-103">Create a data factory and pipeline using .NET SDK</span><span class="sxs-lookup"><span data-stu-id="347f7-103">Create a data factory and pipeline using .NET SDK</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Current version](quickstart-create-data-factory-dot-net.md)

<span data-ttu-id="347f7-106">This quickstart describes how to use .NET SDK to create an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="347f7-106">This quickstart describes how to use .NET SDK to create an Azure data factory.</span></span> <span data-ttu-id="347f7-107">The pipeline you create in this data factory **copies** data from one folder to another folder in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="347f7-107">The pipeline you create in this data factory **copies** data from one folder to another folder in an Azure blob storage.</span></span> <span data-ttu-id="347f7-108">For a tutorial on how to **transform** data using Azure Data Factory, see [Tutorial: Transform data using Spark](transform-data-using-spark.md).</span><span class="sxs-lookup"><span data-stu-id="347f7-108">For a tutorial on how to **transform** data using Azure Data Factory, see [Tutorial: Transform data using Spark](transform-data-using-spark.md).</span></span> 

> [!NOTE]
> This article does not provide a detailed introduction of the Data Factory service. For an introduction to the Azure Data Factory service, see [Introduction to Azure Data Factory](introduction.md).

<span data-ttu-id="347f7-111">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="347f7-111">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [data-factory-quickstart-prerequisites](../../includes/data-factory-quickstart-prerequisites.md)] 

### <a name="visual-studio"></a><span data-ttu-id="347f7-112">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="347f7-112">Visual Studio</span></span>
<span data-ttu-id="347f7-113">The walkthrough in this article uses Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="347f7-113">The walkthrough in this article uses Visual Studio 2017.</span></span> <span data-ttu-id="347f7-114">You can also use Visual Studio 2013 or 2015.</span><span class="sxs-lookup"><span data-stu-id="347f7-114">You can also use Visual Studio 2013 or 2015.</span></span>

### <a name="azure-net-sdk"></a><span data-ttu-id="347f7-115">Azure .NET SDK</span><span class="sxs-lookup"><span data-stu-id="347f7-115">Azure .NET SDK</span></span>
<span data-ttu-id="347f7-116">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/) on your machine.</span><span class="sxs-lookup"><span data-stu-id="347f7-116">Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/) on your machine.</span></span>

## <a name="create-an-application-in-azure-active-directory"></a><span data-ttu-id="347f7-117">Create an application in Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="347f7-117">Create an application in Azure Active Directory</span></span>
<span data-ttu-id="347f7-118">Following instructions from the sections in [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) to do the following tasks:</span><span class="sxs-lookup"><span data-stu-id="347f7-118">Following instructions from the sections in [this article](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application) to do the following tasks:</span></span> 

1. <span data-ttu-id="347f7-119">**Create an Azure Active Directory application**.</span><span class="sxs-lookup"><span data-stu-id="347f7-119">**Create an Azure Active Directory application**.</span></span> <span data-ttu-id="347f7-120">Create an application in Azure Active Directory that represents the .NET application you are creating in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="347f7-120">Create an application in Azure Active Directory that represents the .NET application you are creating in this tutorial.</span></span> <span data-ttu-id="347f7-121">For the sign-on URL, you can provide a dummy URL as shown in the article (`https://contoso.org/exampleapp`).</span><span class="sxs-lookup"><span data-stu-id="347f7-121">For the sign-on URL, you can provide a dummy URL as shown in the article (`https://contoso.org/exampleapp`).</span></span>
2. <span data-ttu-id="347f7-122">Get the **application ID** and **authentication key**, and note down these values that you use later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="347f7-122">Get the **application ID** and **authentication key**, and note down these values that you use later in this tutorial.</span></span> 
3. <span data-ttu-id="347f7-123">Get the **tenant ID** and note down this value that you use later in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="347f7-123">Get the **tenant ID** and note down this value that you use later in this tutorial.</span></span>
4. <span data-ttu-id="347f7-124">Assign the application to the **Contributor** role at the subscription level so that the application can create data factories in the subscription.</span><span class="sxs-lookup"><span data-stu-id="347f7-124">Assign the application to the **Contributor** role at the subscription level so that the application can create data factories in the subscription.</span></span>

## <a name="create-a-visual-studio-project"></a><span data-ttu-id="347f7-125">Create a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="347f7-125">Create a Visual Studio project</span></span>

<span data-ttu-id="347f7-126">Using Visual Studio 2013/2015/2017, create a C# .NET console application.</span><span class="sxs-lookup"><span data-stu-id="347f7-126">Using Visual Studio 2013/2015/2017, create a C# .NET console application.</span></span>

1. <span data-ttu-id="347f7-127">Launch **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="347f7-127">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="347f7-128">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="347f7-128">Click **File**, point to **New**, and click **Project**.</span></span>
3. <span data-ttu-id="347f7-129">Select **Visual C#** -> **Console App (.NET Framework)** from the list of project types on the right.</span><span class="sxs-lookup"><span data-stu-id="347f7-129">Select **Visual C#** -> **Console App (.NET Framework)** from the list of project types on the right.</span></span> <span data-ttu-id="347f7-130">.NET version 4.5.2 or above is required.</span><span class="sxs-lookup"><span data-stu-id="347f7-130">.NET version 4.5.2 or above is required.</span></span>
4. <span data-ttu-id="347f7-131">Enter **ADFv2QuickStart** for the Name.</span><span class="sxs-lookup"><span data-stu-id="347f7-131">Enter **ADFv2QuickStart** for the Name.</span></span>
5. <span data-ttu-id="347f7-132">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="347f7-132">Click **OK** to create the project.</span></span>

## <a name="install-nuget-packages"></a><span data-ttu-id="347f7-133">Install NuGet packages</span><span class="sxs-lookup"><span data-stu-id="347f7-133">Install NuGet packages</span></span>

1. <span data-ttu-id="347f7-134">Click **Tools** -> **NuGet Package Manager** -> **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="347f7-134">Click **Tools** -> **NuGet Package Manager** -> **Package Manager Console**.</span></span>
2. <span data-ttu-id="347f7-135">In the **Package Manager Console**, run the following commands to install packages:</span><span class="sxs-lookup"><span data-stu-id="347f7-135">In the **Package Manager Console**, run the following commands to install packages:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
    Install-Package Microsoft.Azure.Management.ResourceManager -Prerelease
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory

    ```

## <a name="create-a-data-factory-client"></a><span data-ttu-id="347f7-136">Create a data factory client</span><span class="sxs-lookup"><span data-stu-id="347f7-136">Create a data factory client</span></span>

1. <span data-ttu-id="347f7-137">Open **Program.cs**, include the following statements to add references to namespaces.</span><span class="sxs-lookup"><span data-stu-id="347f7-137">Open **Program.cs**, include the following statements to add references to namespaces.</span></span>

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

2. <span data-ttu-id="347f7-138">Add the following code to the **Main** method that sets the variables.</span><span class="sxs-lookup"><span data-stu-id="347f7-138">Add the following code to the **Main** method that sets the variables.</span></span> <span data-ttu-id="347f7-139">Replace the place-holders with your own values.</span><span class="sxs-lookup"><span data-stu-id="347f7-139">Replace the place-holders with your own values.</span></span> <span data-ttu-id="347f7-140">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="347f7-140">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="347f7-141">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="347f7-141">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>

    ```csharp
    // Set variables
    string tenantID = "<your tenant ID>";
    string applicationId = "<your application ID>";
    string authenticationKey = "<your authentication key for the application>";
    string subscriptionId = "<your subscription ID where the data factory resides>";
    string resourceGroup = "<your resource group where the data factory resides>";
    string region = "East US 2";
    string dataFactoryName = "<specify the name of data factory to create. It must be globally unique.>";
    string storageAccount = "<your storage account name to copy data>";
    string storageKey = "<your storage account key>";
    // specify the container and input folder from which all files need to be copied to the output folder. 
    string inputBlobPath = "<the path to existing blob(s) to copy data from, e.g. containername/foldername>";
    //specify the contains and output folder where the files are copied
    string outputBlobPath = "<the blob path to copy data to, e.g. containername/foldername>";

    string storageLinkedServiceName = "AzureStorageLinkedService";  // name of the Azure Storage linked service
    string blobDatasetName = "BlobDataset";             // name of the blob dataset
    string pipelineName = "Adfv2QuickStartPipeline";    // name of the pipeline
    ```

3. <span data-ttu-id="347f7-142">Add the following code to the **Main** method that creates an instance of **DataFactoryManagementClient** class.</span><span class="sxs-lookup"><span data-stu-id="347f7-142">Add the following code to the **Main** method that creates an instance of **DataFactoryManagementClient** class.</span></span> <span data-ttu-id="347f7-143">You use this object to create a data factory, a linked service, datasets, and a pipeline.</span><span class="sxs-lookup"><span data-stu-id="347f7-143">You use this object to create a data factory, a linked service, datasets, and a pipeline.</span></span> <span data-ttu-id="347f7-144">You also use this object to monitor the pipeline run details.</span><span class="sxs-lookup"><span data-stu-id="347f7-144">You also use this object to monitor the pipeline run details.</span></span>

    ```csharp
    // Authenticate and create a data factory management client
    var context = new AuthenticationContext("https://login.windows.net/" + tenantID);
    ClientCredential cc = new ClientCredential(applicationId, authenticationKey);
    AuthenticationResult result = context.AcquireTokenAsync("https://management.azure.com/", cc).Result;
    ServiceClientCredentials cred = new TokenCredentials(result.AccessToken);
    var client = new DataFactoryManagementClient(cred) { SubscriptionId = subscriptionId };
    ```

## <a name="create-a-data-factory"></a><span data-ttu-id="347f7-145">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="347f7-145">Create a data factory</span></span>

<span data-ttu-id="347f7-146">Add the following code to the **Main** method that creates a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="347f7-146">Add the following code to the **Main** method that creates a **data factory**.</span></span> 

```csharp
// Create a data factory
Console.WriteLine("Creating data factory " + dataFactoryName + "...");
Factory dataFactory = new Factory
{
    Location = region,
    Identity = new FactoryIdentity()
};
client.Factories.CreateOrUpdate(resourceGroup, dataFactoryName, dataFactory);
Console.WriteLine(SafeJsonConvert.SerializeObject(dataFactory, client.SerializationSettings));

while (client.Factories.Get(resourceGroup, dataFactoryName).ProvisioningState == "PendingCreation")
{
    System.Threading.Thread.Sleep(1000);
}
```

## <a name="create-a-linked-service"></a><span data-ttu-id="347f7-147">Create a linked service</span><span class="sxs-lookup"><span data-stu-id="347f7-147">Create a linked service</span></span>

<span data-ttu-id="347f7-148">Add the following code to the **Main** method that creates an **Azure Storage linked service**.</span><span class="sxs-lookup"><span data-stu-id="347f7-148">Add the following code to the **Main** method that creates an **Azure Storage linked service**.</span></span>

<span data-ttu-id="347f7-149">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="347f7-149">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="347f7-150">In this Quickstart, you only need to create one Azure Storage linked service for both the copy source and sink store, named "AzureStorageLinkedService" in the sample.</span><span class="sxs-lookup"><span data-stu-id="347f7-150">In this Quickstart, you only need to create one Azure Storage linked service for both the copy source and sink store, named "AzureStorageLinkedService" in the sample.</span></span>

```csharp
// Create an Azure Storage linked service
Console.WriteLine("Creating linked service " + storageLinkedServiceName + "...");

LinkedServiceResource storageLinkedService = new LinkedServiceResource(
    new AzureStorageLinkedService
    {
        ConnectionString = new SecureString("DefaultEndpointsProtocol=https;AccountName=" + storageAccount + ";AccountKey=" + storageKey)
    }
);
client.LinkedServices.CreateOrUpdate(resourceGroup, dataFactoryName, storageLinkedServiceName, storageLinkedService);
Console.WriteLine(SafeJsonConvert.SerializeObject(storageLinkedService, client.SerializationSettings));
```

## <a name="create-a-dataset"></a><span data-ttu-id="347f7-151">Create a dataset</span><span class="sxs-lookup"><span data-stu-id="347f7-151">Create a dataset</span></span>

<span data-ttu-id="347f7-152">Add the following code to the **Main** method that creates an **Azure blob dataset**.</span><span class="sxs-lookup"><span data-stu-id="347f7-152">Add the following code to the **Main** method that creates an **Azure blob dataset**.</span></span>

<span data-ttu-id="347f7-153">You define a dataset that represents the data to copy from a source to a sink.</span><span class="sxs-lookup"><span data-stu-id="347f7-153">You define a dataset that represents the data to copy from a source to a sink.</span></span> <span data-ttu-id="347f7-154">In this example, this Blob dataset references to the Azure Storage linked service you created in the previous step.</span><span class="sxs-lookup"><span data-stu-id="347f7-154">In this example, this Blob dataset references to the Azure Storage linked service you created in the previous step.</span></span> <span data-ttu-id="347f7-155">The dataset takes a parameter whose value is set in an activity that consumes the dataset.</span><span class="sxs-lookup"><span data-stu-id="347f7-155">The dataset takes a parameter whose value is set in an activity that consumes the dataset.</span></span> <span data-ttu-id="347f7-156">The parameter is used to construct the "folderPath" pointing to where the data resides/stored.</span><span class="sxs-lookup"><span data-stu-id="347f7-156">The parameter is used to construct the "folderPath" pointing to where the data resides/stored.</span></span>

```csharp
// Create a Azure Blob dataset
Console.WriteLine("Creating dataset " + blobDatasetName + "...");
DatasetResource blobDataset = new DatasetResource(
    new AzureBlobDataset
    {
        LinkedServiceName = new LinkedServiceReference
        {
            ReferenceName = storageLinkedServiceName
        },
        FolderPath = new Expression { Value = "@{dataset().path}" },
        Parameters = new Dictionary<string, ParameterSpecification>
        {
            { "path", new ParameterSpecification { Type = ParameterType.String } }

        }
    }
);
client.Datasets.CreateOrUpdate(resourceGroup, dataFactoryName, blobDatasetName, blobDataset);
Console.WriteLine(SafeJsonConvert.SerializeObject(blobDataset, client.SerializationSettings));
```

## <a name="create-a-pipeline"></a><span data-ttu-id="347f7-157">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="347f7-157">Create a pipeline</span></span>

<span data-ttu-id="347f7-158">Add the following code to the **Main** method that creates a **pipeline with a copy activity**.</span><span class="sxs-lookup"><span data-stu-id="347f7-158">Add the following code to the **Main** method that creates a **pipeline with a copy activity**.</span></span>

<span data-ttu-id="347f7-159">In this example, this pipeline contains one activity and takes two parameters - input blob path and output blob path.</span><span class="sxs-lookup"><span data-stu-id="347f7-159">In this example, this pipeline contains one activity and takes two parameters - input blob path and output blob path.</span></span> <span data-ttu-id="347f7-160">The values for these parameters are set when the pipeline is triggered/run.</span><span class="sxs-lookup"><span data-stu-id="347f7-160">The values for these parameters are set when the pipeline is triggered/run.</span></span> <span data-ttu-id="347f7-161">The copy activity refers to the same blob dataset created in the previous step as input and output.</span><span class="sxs-lookup"><span data-stu-id="347f7-161">The copy activity refers to the same blob dataset created in the previous step as input and output.</span></span> <span data-ttu-id="347f7-162">When the dataset is used as an input dataset, input path is specified.</span><span class="sxs-lookup"><span data-stu-id="347f7-162">When the dataset is used as an input dataset, input path is specified.</span></span> <span data-ttu-id="347f7-163">And, when the dataset is used as an output dataset, the output path is specified.</span><span class="sxs-lookup"><span data-stu-id="347f7-163">And, when the dataset is used as an output dataset, the output path is specified.</span></span> 

```csharp
// Create a pipeline with a copy activity
Console.WriteLine("Creating pipeline " + pipelineName + "...");
PipelineResource pipeline = new PipelineResource
{
    Parameters = new Dictionary<string, ParameterSpecification>
    {
        { "inputPath", new ParameterSpecification { Type = ParameterType.String } },
        { "outputPath", new ParameterSpecification { Type = ParameterType.String } }
    },
    Activities = new List<Activity>
    {
        new CopyActivity
        {
            Name = "CopyFromBlobToBlob",
            Inputs = new List<DatasetReference>
            {
                new DatasetReference()
                {
                    ReferenceName = blobDatasetName,
                    Parameters = new Dictionary<string, object>
                    {
                        { "path", "@pipeline().parameters.inputPath" }
                    }
                }
            },
            Outputs = new List<DatasetReference>
            {
                new DatasetReference
                {
                    ReferenceName = blobDatasetName,
                    Parameters = new Dictionary<string, object>
                    {
                        { "path", "@pipeline().parameters.outputPath" }
                    }
                }
            },
            Source = new BlobSource { },
            Sink = new BlobSink { }
        }
    }
};
client.Pipelines.CreateOrUpdate(resourceGroup, dataFactoryName, pipelineName, pipeline);
Console.WriteLine(SafeJsonConvert.SerializeObject(pipeline, client.SerializationSettings));
```

## <a name="create-a-pipeline-run"></a><span data-ttu-id="347f7-164">Create a pipeline run</span><span class="sxs-lookup"><span data-stu-id="347f7-164">Create a pipeline run</span></span>

<span data-ttu-id="347f7-165">Add the following code to the **Main** method that **triggers a pipeline run**.</span><span class="sxs-lookup"><span data-stu-id="347f7-165">Add the following code to the **Main** method that **triggers a pipeline run**.</span></span>

<span data-ttu-id="347f7-166">This code also sets values of **inputPath** and **outputPath** parameters specified in pipeline with the actual values of source and sink blob paths.</span><span class="sxs-lookup"><span data-stu-id="347f7-166">This code also sets values of **inputPath** and **outputPath** parameters specified in pipeline with the actual values of source and sink blob paths.</span></span>

```csharp
// Create a pipeline run
Console.WriteLine("Creating pipeline run...");
Dictionary<string, object> parameters = new Dictionary<string, object>
{
    { "inputPath", inputBlobPath },
    { "outputPath", outputBlobPath }
};
CreateRunResponse runResponse = client.Pipelines.CreateRunWithHttpMessagesAsync(resourceGroup, dataFactoryName, pipelineName, parameters: parameters).Result.Body;
Console.WriteLine("Pipeline run ID: " + runResponse.RunId);
```

## <a name="monitor-a-pipeline-run"></a><span data-ttu-id="347f7-167">Monitor a pipeline run</span><span class="sxs-lookup"><span data-stu-id="347f7-167">Monitor a pipeline run</span></span>

1. <span data-ttu-id="347f7-168">Add the following code to the **Main** method to continuously check the status until it finishes copying the data.</span><span class="sxs-lookup"><span data-stu-id="347f7-168">Add the following code to the **Main** method to continuously check the status until it finishes copying the data.</span></span>

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

2. <span data-ttu-id="347f7-169">Add the following code to the **Main** method that retrieves copy activity run details, for example, size of the data read/written.</span><span class="sxs-lookup"><span data-stu-id="347f7-169">Add the following code to the **Main** method that retrieves copy activity run details, for example, size of the data read/written.</span></span>

    ```csharp
    // Check the copy activity run details
    Console.WriteLine("Checking copy activity run details...");
   
    List<ActivityRun> activityRuns = client.ActivityRuns.ListByPipelineRun(
    resourceGroup, dataFactoryName, runResponse.RunId, DateTime.UtcNow.AddMinutes(-10), DateTime.UtcNow.AddMinutes(10)).ToList(); 
    if (pipelineRun.Status == "Succeeded")
        Console.WriteLine(activityRuns.First().Output);
    else
        Console.WriteLine(activityRuns.First().Error);
    Console.WriteLine("\nPress any key to exit...");
    Console.ReadKey();
    ```

## <a name="run-the-code"></a><span data-ttu-id="347f7-170">Run the code</span><span class="sxs-lookup"><span data-stu-id="347f7-170">Run the code</span></span>

<span data-ttu-id="347f7-171">Build and start the application, then verify the pipeline execution.</span><span class="sxs-lookup"><span data-stu-id="347f7-171">Build and start the application, then verify the pipeline execution.</span></span>

<span data-ttu-id="347f7-172">The console prints the progress of creating data factory, linked service, datasets, pipeline, and pipeline run.</span><span class="sxs-lookup"><span data-stu-id="347f7-172">The console prints the progress of creating data factory, linked service, datasets, pipeline, and pipeline run.</span></span> <span data-ttu-id="347f7-173">It then checks the pipeline run status.</span><span class="sxs-lookup"><span data-stu-id="347f7-173">It then checks the pipeline run status.</span></span> <span data-ttu-id="347f7-174">Wait until you see the copy activity run details with data read/written size.</span><span class="sxs-lookup"><span data-stu-id="347f7-174">Wait until you see the copy activity run details with data read/written size.</span></span> <span data-ttu-id="347f7-175">Then, use tools such as [Azure Storage explorer](https://azure.microsoft.com/features/storage-explorer/) to check the blob(s) is copied to "outputBlobPath" from "inputBlobPath" as you specified in variables.</span><span class="sxs-lookup"><span data-stu-id="347f7-175">Then, use tools such as [Azure Storage explorer](https://azure.microsoft.com/features/storage-explorer/) to check the blob(s) is copied to "outputBlobPath" from "inputBlobPath" as you specified in variables.</span></span>

### <a name="sample-output"></a><span data-ttu-id="347f7-176">Sample output:</span><span class="sxs-lookup"><span data-stu-id="347f7-176">Sample output:</span></span> 
```json
Creating data factory SPv2Factory0907...
{
  "identity": {
    "type": "SystemAssigned"
  },
  "location": "East US"
}
Creating linked service AzureStorageLinkedService...
{
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": {
        "value": "DefaultEndpointsProtocol=https;AccountName=<storageAccountName>;AccountKey=<storageAccountKey>",
        "type": "SecureString"
      }
    }
  }
}
Creating dataset BlobDataset...
{
  "properties": {
    "type": "AzureBlob",
    "typeProperties": {
      "folderPath": {
        "value": "@{dataset().path}",
        "type": "Expression"
      }
    },
    "linkedServiceName": {
      "referenceName": "AzureStorageLinkedService",
      "type": "LinkedServiceReference"
    },
    "parameters": {
      "path": {
        "type": "String"
      }
    }
  }
}
Creating pipeline Adfv2QuickStartPipeline...
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
            "referenceName": "BlobDataset",
            "parameters": {
              "path": "@pipeline().parameters.inputPath"
            },
            "type": "DatasetReference"
          }
        ],
        "outputs": [
          {
            "referenceName": "BlobDataset",
            "parameters": {
              "path": "@pipeline().parameters.outputPath"
            },
            "type": "DatasetReference"
          }
        ],
        "name": "CopyFromBlobToBlob"
      }
    ],
    "parameters": {
      "inputPath": {
        "type": "String"
      },
      "outputPath": {
        "type": "String"
      }
    }
  }
}
Creating pipeline run...
Pipeline run ID: 308d222d-3858-48b1-9e66-acd921feaa09
Checking pipeline run status...
Status: InProgress
Status: InProgress
Checking copy activity run details...
{
    "dataRead": 331452208,
    "dataWritten": 331452208,
    "copyDuration": 23,
    "throughput": 14073.209,
    "errors": [],
    "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (West US)",
    "usedDataIntegrationUnits": 2,
    "billedDuration": 23
}

Press any key to exit...
```

## <a name="verify-the-output"></a><span data-ttu-id="347f7-177">Verify the output</span><span class="sxs-lookup"><span data-stu-id="347f7-177">Verify the output</span></span>
<span data-ttu-id="347f7-178">The pipeline automatically creates the output folder in the adftutorial blob container.</span><span class="sxs-lookup"><span data-stu-id="347f7-178">The pipeline automatically creates the output folder in the adftutorial blob container.</span></span> <span data-ttu-id="347f7-179">Then, it copies the emp.txt file from the input folder to the output folder.</span><span class="sxs-lookup"><span data-stu-id="347f7-179">Then, it copies the emp.txt file from the input folder to the output folder.</span></span> 

1. <span data-ttu-id="347f7-180">In the Azure portal, on the **adftutorial** container page, click **Refresh** to see the output folder.</span><span class="sxs-lookup"><span data-stu-id="347f7-180">In the Azure portal, on the **adftutorial** container page, click **Refresh** to see the output folder.</span></span> 
    
    ![Refresh](media/quickstart-create-data-factory-dot-net/output-refresh.png)
2. <span data-ttu-id="347f7-182">Click **output** in the folder list.</span><span class="sxs-lookup"><span data-stu-id="347f7-182">Click **output** in the folder list.</span></span> 
2. <span data-ttu-id="347f7-183">Confirm that the **emp.txt** is copied to the output folder.</span><span class="sxs-lookup"><span data-stu-id="347f7-183">Confirm that the **emp.txt** is copied to the output folder.</span></span> 

    ![Refresh](media/quickstart-create-data-factory-dot-net/output-file.png)

## <a name="clean-up-resources"></a><span data-ttu-id="347f7-185">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="347f7-185">Clean up resources</span></span>
<span data-ttu-id="347f7-186">To programmatically, delete the data factory, add the following lines of code to the program:</span><span class="sxs-lookup"><span data-stu-id="347f7-186">To programmatically, delete the data factory, add the following lines of code to the program:</span></span> 

```csharp
            Console.WriteLine("Deleting the data factory");
            client.Factories.Delete(resourceGroup, dataFactoryName);
```

## <a name="next-steps"></a><span data-ttu-id="347f7-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="347f7-187">Next steps</span></span>
<span data-ttu-id="347f7-188">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="347f7-188">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span></span> <span data-ttu-id="347f7-189">Go through the [tutorials](tutorial-copy-data-dot-net.md) to learn about using Data Factory in more scenarios.</span><span class="sxs-lookup"><span data-stu-id="347f7-189">Go through the [tutorials](tutorial-copy-data-dot-net.md) to learn about using Data Factory in more scenarios.</span></span> 
