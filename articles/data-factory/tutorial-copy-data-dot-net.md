---
title: Copy data from Azure Blob Storage to SQL Database | Microsoft Docs
description: This tutorial provides step-by-step instructions for copying  data from Azure Blob Storage to Azure SQL Database.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: tutorial
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: 780a9323c07af4754f5afd0ab758b882444a2154
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869277"
---
# <a name="copy-data-from-azure-blob-to-azure-sql-database-using-azure-data-factory"></a><span data-ttu-id="57e26-103">Copy data from Azure Blob to Azure SQL Database using Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="57e26-103">Copy data from Azure Blob to Azure SQL Database using Azure Data Factory</span></span>
<span data-ttu-id="57e26-104">In this tutorial, you create a Data Factory pipeline that copies data from Azure Blob Storage to Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="57e26-104">In this tutorial, you create a Data Factory pipeline that copies data from Azure Blob Storage to Azure SQL Database.</span></span> <span data-ttu-id="57e26-105">The configuration pattern in this tutorial applies to copying from a file-based data store to a relational data store.</span><span class="sxs-lookup"><span data-stu-id="57e26-105">The configuration pattern in this tutorial applies to copying from a file-based data store to a relational data store.</span></span> <span data-ttu-id="57e26-106">For a list of data stores supported as sources and sinks, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span><span class="sxs-lookup"><span data-stu-id="57e26-106">For a list of data stores supported as sources and sinks, see [supported data stores](copy-activity-overview.md#supported-data-stores-and-formats) table.</span></span>

<span data-ttu-id="57e26-107">You perform the following steps in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="57e26-107">You perform the following steps in this tutorial:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="57e26-108">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="57e26-108">Create a data factory.</span></span>
> * <span data-ttu-id="57e26-109">Create Azure Storage and Azure SQL Database linked services.</span><span class="sxs-lookup"><span data-stu-id="57e26-109">Create Azure Storage and Azure SQL Database linked services.</span></span>
> * <span data-ttu-id="57e26-110">Create Azure BLob and Azure SQL Database datasets.</span><span class="sxs-lookup"><span data-stu-id="57e26-110">Create Azure BLob and Azure SQL Database datasets.</span></span>
> * <span data-ttu-id="57e26-111">Create a pipeline contains a Copy activity.</span><span class="sxs-lookup"><span data-stu-id="57e26-111">Create a pipeline contains a Copy activity.</span></span>
> * <span data-ttu-id="57e26-112">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="57e26-112">Start a pipeline run.</span></span>
> * <span data-ttu-id="57e26-113">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="57e26-113">Monitor the pipeline and activity runs.</span></span>

<span data-ttu-id="57e26-114">This tutorial uses .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="57e26-114">This tutorial uses .NET SDK.</span></span> <span data-ttu-id="57e26-115">You can use other mechanisms to interact with Azure Data Factory, refer to samples under "Quickstarts".</span><span class="sxs-lookup"><span data-stu-id="57e26-115">You can use other mechanisms to interact with Azure Data Factory, refer to samples under "Quickstarts".</span></span>

<span data-ttu-id="57e26-116">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="57e26-116">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="57e26-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="57e26-117">Prerequisites</span></span>

* <span data-ttu-id="57e26-118">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="57e26-118">**Azure Storage account**.</span></span> <span data-ttu-id="57e26-119">You use the blob storage as **source** data store.</span><span class="sxs-lookup"><span data-stu-id="57e26-119">You use the blob storage as **source** data store.</span></span> <span data-ttu-id="57e26-120">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="57e26-120">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span></span>
* <span data-ttu-id="57e26-121">**Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="57e26-121">**Azure SQL Database**.</span></span> <span data-ttu-id="57e26-122">You use the database as **sink** data store.</span><span class="sxs-lookup"><span data-stu-id="57e26-122">You use the database as **sink** data store.</span></span> <span data-ttu-id="57e26-123">If you don't have an Azure SQL Database, see the [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="57e26-123">If you don't have an Azure SQL Database, see the [Create an Azure SQL database](../sql-database/sql-database-get-started-portal.md) article for steps to create one.</span></span>
* <span data-ttu-id="57e26-124">**Visual Studio** 2015, or 2017.</span><span class="sxs-lookup"><span data-stu-id="57e26-124">**Visual Studio** 2015, or 2017.</span></span> <span data-ttu-id="57e26-125">The walkthrough in this article uses Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="57e26-125">The walkthrough in this article uses Visual Studio 2017.</span></span>
* <span data-ttu-id="57e26-126">**Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)**.</span><span class="sxs-lookup"><span data-stu-id="57e26-126">**Download and install [Azure .NET SDK](http://azure.microsoft.com/downloads/)**.</span></span>
* <span data-ttu-id="57e26-127">**Create an application in Azure Active Directory** following [this instruction](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application).</span><span class="sxs-lookup"><span data-stu-id="57e26-127">**Create an application in Azure Active Directory** following [this instruction](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application).</span></span> <span data-ttu-id="57e26-128">Make note of the following values that you use in later steps: **application ID**, **authentication key**, and **tenant ID**.</span><span class="sxs-lookup"><span data-stu-id="57e26-128">Make note of the following values that you use in later steps: **application ID**, **authentication key**, and **tenant ID**.</span></span> <span data-ttu-id="57e26-129">Assign application to "**Contributor**" role by following instructions in the same article.</span><span class="sxs-lookup"><span data-stu-id="57e26-129">Assign application to "**Contributor**" role by following instructions in the same article.</span></span>

### <a name="create-a-blob-and-a-sql-table"></a><span data-ttu-id="57e26-130">Create a blob and a SQL table</span><span class="sxs-lookup"><span data-stu-id="57e26-130">Create a blob and a SQL table</span></span>

<span data-ttu-id="57e26-131">Now, prepare your Azure Blob and Azure SQL Database for the tutorial by performing the following steps:</span><span class="sxs-lookup"><span data-stu-id="57e26-131">Now, prepare your Azure Blob and Azure SQL Database for the tutorial by performing the following steps:</span></span>

#### <a name="create-a-source-blob"></a><span data-ttu-id="57e26-132">Create a source blob</span><span class="sxs-lookup"><span data-stu-id="57e26-132">Create a source blob</span></span>

1. <span data-ttu-id="57e26-133">Launch Notepad.</span><span class="sxs-lookup"><span data-stu-id="57e26-133">Launch Notepad.</span></span> <span data-ttu-id="57e26-134">Copy the following text and save it as **inputEmp.txt** file on your disk.</span><span class="sxs-lookup"><span data-stu-id="57e26-134">Copy the following text and save it as **inputEmp.txt** file on your disk.</span></span>

    ```
    John|Doe
    Jane|Doe
    ```

2. <span data-ttu-id="57e26-135">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adfv2tutorial** container, and to upload the **inputEmp.txt** file to the container.</span><span class="sxs-lookup"><span data-stu-id="57e26-135">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adfv2tutorial** container, and to upload the **inputEmp.txt** file to the container.</span></span>

#### <a name="create-a-sink-sql-table"></a><span data-ttu-id="57e26-136">Create a sink SQL table</span><span class="sxs-lookup"><span data-stu-id="57e26-136">Create a sink SQL table</span></span>

1. <span data-ttu-id="57e26-137">Use the following SQL script to create the **dbo.emp** table in your Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="57e26-137">Use the following SQL script to create the **dbo.emp** table in your Azure SQL Database.</span></span>

    ```sql
    CREATE TABLE dbo.emp
    (
        ID int IDENTITY(1,1) NOT NULL,
        FirstName varchar(50),
        LastName varchar(50)
    )
    GO

    CREATE CLUSTERED INDEX IX_emp_ID ON dbo.emp (ID);
    ```

2. <span data-ttu-id="57e26-138">Allow Azure services to access SQL server.</span><span class="sxs-lookup"><span data-stu-id="57e26-138">Allow Azure services to access SQL server.</span></span> <span data-ttu-id="57e26-139">Ensure that **Allow access to Azure services** setting is turned **ON** for your Azure SQL server so that the Data Factory service can write data to your Azure SQL server.</span><span class="sxs-lookup"><span data-stu-id="57e26-139">Ensure that **Allow access to Azure services** setting is turned **ON** for your Azure SQL server so that the Data Factory service can write data to your Azure SQL server.</span></span> <span data-ttu-id="57e26-140">To verify and turn on this setting, do the following steps:</span><span class="sxs-lookup"><span data-stu-id="57e26-140">To verify and turn on this setting, do the following steps:</span></span>

    1. <span data-ttu-id="57e26-141">Click **More services** hub on the left and click **SQL servers**.</span><span class="sxs-lookup"><span data-stu-id="57e26-141">Click **More services** hub on the left and click **SQL servers**.</span></span>
    2. <span data-ttu-id="57e26-142">Select your server, and click **Firewall** under **SETTINGS**.</span><span class="sxs-lookup"><span data-stu-id="57e26-142">Select your server, and click **Firewall** under **SETTINGS**.</span></span>
    3. <span data-ttu-id="57e26-143">In the **Firewall settings** page, click **ON** for **Allow access to Azure services**.</span><span class="sxs-lookup"><span data-stu-id="57e26-143">In the **Firewall settings** page, click **ON** for **Allow access to Azure services**.</span></span>


## <a name="create-a-visual-studio-project"></a><span data-ttu-id="57e26-144">Create a Visual Studio project</span><span class="sxs-lookup"><span data-stu-id="57e26-144">Create a Visual Studio project</span></span>

<span data-ttu-id="57e26-145">Using Visual Studio 2015/2017, create a C# .NET console application.</span><span class="sxs-lookup"><span data-stu-id="57e26-145">Using Visual Studio 2015/2017, create a C# .NET console application.</span></span>

1. <span data-ttu-id="57e26-146">Launch **Visual Studio**.</span><span class="sxs-lookup"><span data-stu-id="57e26-146">Launch **Visual Studio**.</span></span>
2. <span data-ttu-id="57e26-147">Click **File**, point to **New**, and click **Project**.</span><span class="sxs-lookup"><span data-stu-id="57e26-147">Click **File**, point to **New**, and click **Project**.</span></span>
3. <span data-ttu-id="57e26-148">Select **Visual C#** -> **Console App (.NET Framework)** from the list of project types on the right.</span><span class="sxs-lookup"><span data-stu-id="57e26-148">Select **Visual C#** -> **Console App (.NET Framework)** from the list of project types on the right.</span></span> <span data-ttu-id="57e26-149">.NET version 4.5.2 or above is required.</span><span class="sxs-lookup"><span data-stu-id="57e26-149">.NET version 4.5.2 or above is required.</span></span>
4. <span data-ttu-id="57e26-150">Enter **ADFv2Tutorial** for the Name.</span><span class="sxs-lookup"><span data-stu-id="57e26-150">Enter **ADFv2Tutorial** for the Name.</span></span>
5. <span data-ttu-id="57e26-151">Click **OK** to create the project.</span><span class="sxs-lookup"><span data-stu-id="57e26-151">Click **OK** to create the project.</span></span>

## <a name="install-nuget-packages"></a><span data-ttu-id="57e26-152">Install NuGet packages</span><span class="sxs-lookup"><span data-stu-id="57e26-152">Install NuGet packages</span></span>

1. <span data-ttu-id="57e26-153">Click **Tools** -> **NuGet Package Manager** -> **Package Manager Console**.</span><span class="sxs-lookup"><span data-stu-id="57e26-153">Click **Tools** -> **NuGet Package Manager** -> **Package Manager Console**.</span></span>
2. <span data-ttu-id="57e26-154">In the **Package Manager Console**, run the following commands to install packages:</span><span class="sxs-lookup"><span data-stu-id="57e26-154">In the **Package Manager Console**, run the following commands to install packages:</span></span>

    ```
    Install-Package Microsoft.Azure.Management.DataFactory -Prerelease
    Install-Package Microsoft.Azure.Management.ResourceManager -Prerelease
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
    ```

## <a name="create-a-data-factory-client"></a><span data-ttu-id="57e26-155">Create a data factory client</span><span class="sxs-lookup"><span data-stu-id="57e26-155">Create a data factory client</span></span>

1. <span data-ttu-id="57e26-156">Open **Program.cs**, include the following statements to add references to namespaces.</span><span class="sxs-lookup"><span data-stu-id="57e26-156">Open **Program.cs**, include the following statements to add references to namespaces.</span></span>

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
    
2. <span data-ttu-id="57e26-157">Add the following code to the **Main** method that sets variables.</span><span class="sxs-lookup"><span data-stu-id="57e26-157">Add the following code to the **Main** method that sets variables.</span></span> <span data-ttu-id="57e26-158">Replace place-holders with your own values.</span><span class="sxs-lookup"><span data-stu-id="57e26-158">Replace place-holders with your own values.</span></span> <span data-ttu-id="57e26-159">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="57e26-159">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="57e26-160">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="57e26-160">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>

    ```csharp
    // Set variables
    string tenantID = "<your tenant ID>";
    string applicationId = "<your application ID>";
    string authenticationKey = "<your authentication key for the application>";
    string subscriptionId = "<your subscription ID to create the factory>";
    string resourceGroup = "<your resource group to create the factory>";

    string region = "East US";
    string dataFactoryName = "<specify the name of a data factory to create. It must be globally unique.>";

    // Specify the source Azure Blob information
    string storageAccount = "<your storage account name to copy data>";
    string storageKey = "<your storage account key>";
    string inputBlobPath = "adfv2tutorial/";
    string inputBlobName = "inputEmp.txt";

    // Specify the sink Azure SQL Database information
    string azureSqlConnString = "Server=tcp:<your server name>.database.windows.net,1433;Database=<your database name>;User ID=<your username>@<your server name>;Password=<your password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30";
    string azureSqlTableName = "dbo.emp";

    string storageLinkedServiceName = "AzureStorageLinkedService";
    string sqlDbLinkedServiceName = "AzureSqlDbLinkedService";
    string blobDatasetName = "BlobDataset";
    string sqlDatasetName = "SqlDataset";
    string pipelineName = "Adfv2TutorialBlobToSqlCopy";
    ```

3. <span data-ttu-id="57e26-161">Add the following code to the **Main** method that creates an instance of **DataFactoryManagementClient** class.</span><span class="sxs-lookup"><span data-stu-id="57e26-161">Add the following code to the **Main** method that creates an instance of **DataFactoryManagementClient** class.</span></span> <span data-ttu-id="57e26-162">You use this object to create a data factory, linked service, datasets, and pipeline.</span><span class="sxs-lookup"><span data-stu-id="57e26-162">You use this object to create a data factory, linked service, datasets, and pipeline.</span></span> <span data-ttu-id="57e26-163">You also use this object to monitor the pipeline run details.</span><span class="sxs-lookup"><span data-stu-id="57e26-163">You also use this object to monitor the pipeline run details.</span></span>

    ```csharp
    // Authenticate and create a data factory management client
    var context = new AuthenticationContext("https://login.windows.net/" + tenantID);
    ClientCredential cc = new ClientCredential(applicationId, authenticationKey);
    AuthenticationResult result = context.AcquireTokenAsync("https://management.azure.com/", cc).Result;
    ServiceClientCredentials cred = new TokenCredentials(result.AccessToken);
    var client = new DataFactoryManagementClient(cred) { SubscriptionId = subscriptionId };
    ```

## <a name="create-a-data-factory"></a><span data-ttu-id="57e26-164">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="57e26-164">Create a data factory</span></span>

<span data-ttu-id="57e26-165">Add the following code to the **Main** method that creates a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="57e26-165">Add the following code to the **Main** method that creates a **data factory**.</span></span>

```csharp
// Create a data factory
Console.WriteLine("Creating a data factory " + dataFactoryName + "...");
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

## <a name="create-linked-services"></a><span data-ttu-id="57e26-166">Create linked services</span><span class="sxs-lookup"><span data-stu-id="57e26-166">Create linked services</span></span>

<span data-ttu-id="57e26-167">In this tutorial, you create two linked services for source and sink respectively:</span><span class="sxs-lookup"><span data-stu-id="57e26-167">In this tutorial, you create two linked services for source and sink respectively:</span></span>

### <a name="create-an-azure-storage-linked-service"></a><span data-ttu-id="57e26-168">Create an Azure Storage linked service</span><span class="sxs-lookup"><span data-stu-id="57e26-168">Create an Azure Storage linked service</span></span>

<span data-ttu-id="57e26-169">Add the following code to the **Main** method that creates an **Azure Storage linked service**.</span><span class="sxs-lookup"><span data-stu-id="57e26-169">Add the following code to the **Main** method that creates an **Azure Storage linked service**.</span></span> <span data-ttu-id="57e26-170">Learn more from [Azure Blob linked service properties](connector-azure-blob-storage.md#linked-service-properties) on supported properties and details.</span><span class="sxs-lookup"><span data-stu-id="57e26-170">Learn more from [Azure Blob linked service properties](connector-azure-blob-storage.md#linked-service-properties) on supported properties and details.</span></span>

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

### <a name="create-an-azure-sql-database-linked-service"></a><span data-ttu-id="57e26-171">Create an Azure SQL Database linked service</span><span class="sxs-lookup"><span data-stu-id="57e26-171">Create an Azure SQL Database linked service</span></span>

<span data-ttu-id="57e26-172">Add the following code to the **Main** method that creates an **Azure SQL Database linked service**.</span><span class="sxs-lookup"><span data-stu-id="57e26-172">Add the following code to the **Main** method that creates an **Azure SQL Database linked service**.</span></span> <span data-ttu-id="57e26-173">Learn more from [Azure SQL Database linked service properties](connector-azure-sql-database.md#linked-service-properties) on supported properties and details.</span><span class="sxs-lookup"><span data-stu-id="57e26-173">Learn more from [Azure SQL Database linked service properties](connector-azure-sql-database.md#linked-service-properties) on supported properties and details.</span></span>

```csharp
// Create an Azure SQL Database linked service
Console.WriteLine("Creating linked service " + sqlDbLinkedServiceName + "...");

LinkedServiceResource sqlDbLinkedService = new LinkedServiceResource(
    new AzureSqlDatabaseLinkedService
    {
        ConnectionString = new SecureString(azureSqlConnString)
    }
);
client.LinkedServices.CreateOrUpdate(resourceGroup, dataFactoryName, sqlDbLinkedServiceName, sqlDbLinkedService);
Console.WriteLine(SafeJsonConvert.SerializeObject(sqlDbLinkedService, client.SerializationSettings));
```

## <a name="create-datasets"></a><span data-ttu-id="57e26-174">Create datasets</span><span class="sxs-lookup"><span data-stu-id="57e26-174">Create datasets</span></span>

<span data-ttu-id="57e26-175">In this section, you create two datasets: one for the source and the other for the sink.</span><span class="sxs-lookup"><span data-stu-id="57e26-175">In this section, you create two datasets: one for the source and the other for the sink.</span></span> 

### <a name="create-a-dataset-for-source-azure-blob"></a><span data-ttu-id="57e26-176">Create a dataset for source Azure Blob</span><span class="sxs-lookup"><span data-stu-id="57e26-176">Create a dataset for source Azure Blob</span></span>

<span data-ttu-id="57e26-177">Add the following code to the **Main** method that creates an **Azure blob dataset**.</span><span class="sxs-lookup"><span data-stu-id="57e26-177">Add the following code to the **Main** method that creates an **Azure blob dataset**.</span></span> <span data-ttu-id="57e26-178">Learn more from [Azure Blob dataset properties](connector-azure-blob-storage.md#dataset-properties) on supported properties and details.</span><span class="sxs-lookup"><span data-stu-id="57e26-178">Learn more from [Azure Blob dataset properties](connector-azure-blob-storage.md#dataset-properties) on supported properties and details.</span></span>

<span data-ttu-id="57e26-179">You define a dataset that represents the source data in Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="57e26-179">You define a dataset that represents the source data in Azure Blob.</span></span> <span data-ttu-id="57e26-180">This Blob dataset refers to the Azure Storage linked service you create in the previous step, and describes:</span><span class="sxs-lookup"><span data-stu-id="57e26-180">This Blob dataset refers to the Azure Storage linked service you create in the previous step, and describes:</span></span>

- <span data-ttu-id="57e26-181">The location of the blob to copy from: **FolderPath** and **FileName**;</span><span class="sxs-lookup"><span data-stu-id="57e26-181">The location of the blob to copy from: **FolderPath** and **FileName**;</span></span>
- <span data-ttu-id="57e26-182">The blob format indicating how to parse the content: **TextFormat** and its settings (for example, column delimiter).</span><span class="sxs-lookup"><span data-stu-id="57e26-182">The blob format indicating how to parse the content: **TextFormat** and its settings (for example, column delimiter).</span></span>
- <span data-ttu-id="57e26-183">The data structure, including column names and data types which in this case map to the sink SQL table.</span><span class="sxs-lookup"><span data-stu-id="57e26-183">The data structure, including column names and data types which in this case map to the sink SQL table.</span></span>

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
        FolderPath = inputBlobPath,
        FileName = inputBlobName,
        Format = new TextFormat { ColumnDelimiter = "|" },
        Structure = new List<DatasetDataElement>
        {
            new DatasetDataElement
            {
                Name = "FirstName",
                Type = "String"
            },
            new DatasetDataElement
            {
                Name = "LastName",
                Type = "String"
            }
        }
    }
);
client.Datasets.CreateOrUpdate(resourceGroup, dataFactoryName, blobDatasetName, blobDataset);
Console.WriteLine(SafeJsonConvert.SerializeObject(blobDataset, client.SerializationSettings));
```

### <a name="create-a-dataset-for-sink-azure-sql-database"></a><span data-ttu-id="57e26-184">Create a dataset for sink Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="57e26-184">Create a dataset for sink Azure SQL Database</span></span>

<span data-ttu-id="57e26-185">Add the following code to the **Main** method that creates an **Azure SQL Database dataset**.</span><span class="sxs-lookup"><span data-stu-id="57e26-185">Add the following code to the **Main** method that creates an **Azure SQL Database dataset**.</span></span> <span data-ttu-id="57e26-186">Learn more from [Azure SQL Database dataset properties](connector-azure-sql-database.md#dataset-properties) on supported properties and details.</span><span class="sxs-lookup"><span data-stu-id="57e26-186">Learn more from [Azure SQL Database dataset properties](connector-azure-sql-database.md#dataset-properties) on supported properties and details.</span></span>

<span data-ttu-id="57e26-187">You define a dataset that represents the sink data in Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="57e26-187">You define a dataset that represents the sink data in Azure SQL Database.</span></span> <span data-ttu-id="57e26-188">This dataset refers to the Azure SQL Database linked service you create in the previous step.</span><span class="sxs-lookup"><span data-stu-id="57e26-188">This dataset refers to the Azure SQL Database linked service you create in the previous step.</span></span> <span data-ttu-id="57e26-189">It also specifies the SQL table that holds the copied data.</span><span class="sxs-lookup"><span data-stu-id="57e26-189">It also specifies the SQL table that holds the copied data.</span></span> 

```csharp
// Create a Azure SQL Database dataset
Console.WriteLine("Creating dataset " + sqlDatasetName + "...");
DatasetResource sqlDataset = new DatasetResource(
    new AzureSqlTableDataset
    {
        LinkedServiceName = new LinkedServiceReference
        {
            ReferenceName = sqlDbLinkedServiceName
        },
        TableName = azureSqlTableName
    }
);
client.Datasets.CreateOrUpdate(resourceGroup, dataFactoryName, sqlDatasetName, sqlDataset);
Console.WriteLine(SafeJsonConvert.SerializeObject(sqlDataset, client.SerializationSettings));
```

## <a name="create-a-pipeline"></a><span data-ttu-id="57e26-190">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="57e26-190">Create a pipeline</span></span>

<span data-ttu-id="57e26-191">Add the following code to the **Main** method that creates a **pipeline with a copy activity**.</span><span class="sxs-lookup"><span data-stu-id="57e26-191">Add the following code to the **Main** method that creates a **pipeline with a copy activity**.</span></span> <span data-ttu-id="57e26-192">In this tutorial, this pipeline contains one activity: copy activity, which takes in the Blob dataset as source and the SQL dataset as sink.</span><span class="sxs-lookup"><span data-stu-id="57e26-192">In this tutorial, this pipeline contains one activity: copy activity, which takes in the Blob dataset as source and the SQL dataset as sink.</span></span> <span data-ttu-id="57e26-193">Learn more from [Copy Activity Overview](copy-activity-overview.md) on copy activity details.</span><span class="sxs-lookup"><span data-stu-id="57e26-193">Learn more from [Copy Activity Overview](copy-activity-overview.md) on copy activity details.</span></span>

```csharp
// Create a pipeline with copy activity
Console.WriteLine("Creating pipeline " + pipelineName + "...");
PipelineResource pipeline = new PipelineResource
{
    Activities = new List<Activity>
    {
        new CopyActivity
        {
            Name = "CopyFromBlobToSQL",
            Inputs = new List<DatasetReference>
            {
                new DatasetReference()
                {
                    ReferenceName = blobDatasetName
                }
            },
            Outputs = new List<DatasetReference>
            {
                new DatasetReference
                {
                    ReferenceName = sqlDatasetName
                }
            },
            Source = new BlobSource { },
            Sink = new SqlSink { }
        }
    }
};
client.Pipelines.CreateOrUpdate(resourceGroup, dataFactoryName, pipelineName, pipeline);
Console.WriteLine(SafeJsonConvert.SerializeObject(pipeline, client.SerializationSettings));
```

## <a name="create-a-pipeline-run"></a><span data-ttu-id="57e26-194">Create a pipeline run</span><span class="sxs-lookup"><span data-stu-id="57e26-194">Create a pipeline run</span></span>

<span data-ttu-id="57e26-195">Add the following code to the **Main** method that **triggers a pipeline run**.</span><span class="sxs-lookup"><span data-stu-id="57e26-195">Add the following code to the **Main** method that **triggers a pipeline run**.</span></span>

```csharp
// Create a pipeline run
Console.WriteLine("Creating pipeline run...");
CreateRunResponse runResponse = client.Pipelines.CreateRunWithHttpMessagesAsync(resourceGroup, dataFactoryName, pipelineName).Result.Body;
Console.WriteLine("Pipeline run ID: " + runResponse.RunId);
```

## <a name="monitor-a-pipeline-run"></a><span data-ttu-id="57e26-196">Monitor a pipeline run</span><span class="sxs-lookup"><span data-stu-id="57e26-196">Monitor a pipeline run</span></span>

1. <span data-ttu-id="57e26-197">Add the following code to the **Main** method to continuously check the status of the pipeline run until it finishes copying the data.</span><span class="sxs-lookup"><span data-stu-id="57e26-197">Add the following code to the **Main** method to continuously check the status of the pipeline run until it finishes copying the data.</span></span>

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

2. <span data-ttu-id="57e26-198">Add the following code to the **Main** method that retrieves copy activity run details, for example, size of the data read/written.</span><span class="sxs-lookup"><span data-stu-id="57e26-198">Add the following code to the **Main** method that retrieves copy activity run details, for example, size of the data read/written.</span></span>

    ```csharp
    // Check the copy activity run details
    Console.WriteLine("Checking copy activity run details...");

    List<ActivityRun> activityRuns = client.ActivityRuns.ListByPipelineRun(
    resourceGroup, dataFactoryName, runResponse.RunId, DateTime.UtcNow.AddMinutes(-10), DateTime.UtcNow.AddMinutes(10)).ToList(); 
 
    if (pipelineRun.Status == "Succeeded")
    {
        Console.WriteLine(activityRuns.First().Output);
    }
    else
        Console.WriteLine(activityRuns.First().Error);
    
    Console.WriteLine("\nPress any key to exit...");
    Console.ReadKey();
    ```

## <a name="run-the-code"></a><span data-ttu-id="57e26-199">Run the code</span><span class="sxs-lookup"><span data-stu-id="57e26-199">Run the code</span></span>

<span data-ttu-id="57e26-200">Build and start the application, then verify the pipeline execution.</span><span class="sxs-lookup"><span data-stu-id="57e26-200">Build and start the application, then verify the pipeline execution.</span></span>

<span data-ttu-id="57e26-201">The console prints the progress of creating a data factory, linked service, datasets, pipeline, and pipeline run.</span><span class="sxs-lookup"><span data-stu-id="57e26-201">The console prints the progress of creating a data factory, linked service, datasets, pipeline, and pipeline run.</span></span> <span data-ttu-id="57e26-202">It then checks the pipeline run status.</span><span class="sxs-lookup"><span data-stu-id="57e26-202">It then checks the pipeline run status.</span></span> <span data-ttu-id="57e26-203">Wait until you see the copy activity run details with data read/written size.</span><span class="sxs-lookup"><span data-stu-id="57e26-203">Wait until you see the copy activity run details with data read/written size.</span></span> <span data-ttu-id="57e26-204">Then, use tools such as SSMS (SQL Server Management Studio) or Visual Studio to connect to your destination Azure SQL Database and check if the data is copied into the table you specified.</span><span class="sxs-lookup"><span data-stu-id="57e26-204">Then, use tools such as SSMS (SQL Server Management Studio) or Visual Studio to connect to your destination Azure SQL Database and check if the data is copied into the table you specified.</span></span>

### <a name="sample-output"></a><span data-ttu-id="57e26-205">Sample output</span><span class="sxs-lookup"><span data-stu-id="57e26-205">Sample output</span></span>

```json
Creating a data factory AdfV2Tutorial...
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
        "type": "SecureString",
        "value": "DefaultEndpointsProtocol=https;AccountName=<accountName>;AccountKey=<accountKey>"
      }
    }
  }
}
Creating linked service AzureSqlDbLinkedService...
{
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": {
        "type": "SecureString",
        "value": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
      }
    }
  }
}
Creating dataset BlobDataset...
{
  "properties": {
    "type": "AzureBlob",
    "typeProperties": {
      "folderPath": "adfv2tutorial/",
      "fileName": "inputEmp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "|"
      }
    },
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "linkedServiceName": {
      "type": "LinkedServiceReference",
      "referenceName": "AzureStorageLinkedService"
    }
  }
}
Creating dataset SqlDataset...
{
  "properties": {
    "type": "AzureSqlTable",
    "typeProperties": {
      "tableName": "dbo.emp"
    },
    "linkedServiceName": {
      "type": "LinkedServiceReference",
      "referenceName": "AzureSqlDbLinkedService"
    }
  }
}
Creating pipeline Adfv2TutorialBlobToSqlCopy...
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
            "type": "SqlSink"
          }
        },
        "inputs": [
          {
            "type": "DatasetReference",
            "referenceName": "BlobDataset"
          }
        ],
        "outputs": [
          {
            "type": "DatasetReference",
            "referenceName": "SqlDataset"
          }
        ],
        "name": "CopyFromBlobToSQL"
      }
    ]
  }
}
Creating pipeline run...
Pipeline run ID: 1cd03653-88a0-4c90-aabc-ae12d843e252
Checking pipeline run status...
Status: InProgress
Status: InProgress
Status: Succeeded
Checking copy activity run details...
{
  "dataRead": 18,
  "dataWritten": 28,
  "rowsCopied": 2,
  "copyDuration": 2,
  "throughput": 0.01,
  "errors": [],
  "effectiveIntegrationRuntime": "DefaultIntegrationRuntime (East US)",
  "usedDataIntegrationUnits": 2,
  "billedDuration": 2
}

Press any key to exit...
```


## <a name="next-steps"></a><span data-ttu-id="57e26-206">Next steps</span><span class="sxs-lookup"><span data-stu-id="57e26-206">Next steps</span></span>
<span data-ttu-id="57e26-207">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="57e26-207">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span></span> <span data-ttu-id="57e26-208">You learned how to:</span><span class="sxs-lookup"><span data-stu-id="57e26-208">You learned how to:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="57e26-209">Create a data factory.</span><span class="sxs-lookup"><span data-stu-id="57e26-209">Create a data factory.</span></span>
> * <span data-ttu-id="57e26-210">Create Azure Storage and Azure SQL Database linked services.</span><span class="sxs-lookup"><span data-stu-id="57e26-210">Create Azure Storage and Azure SQL Database linked services.</span></span>
> * <span data-ttu-id="57e26-211">Create Azure Blob and Azure SQL Database datasets.</span><span class="sxs-lookup"><span data-stu-id="57e26-211">Create Azure Blob and Azure SQL Database datasets.</span></span>
> * <span data-ttu-id="57e26-212">Create a pipeline contains a Copy activity.</span><span class="sxs-lookup"><span data-stu-id="57e26-212">Create a pipeline contains a Copy activity.</span></span>
> * <span data-ttu-id="57e26-213">Start a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="57e26-213">Start a pipeline run.</span></span>
> * <span data-ttu-id="57e26-214">Monitor the pipeline and activity runs.</span><span class="sxs-lookup"><span data-stu-id="57e26-214">Monitor the pipeline and activity runs.</span></span>


<span data-ttu-id="57e26-215">Advance to the following tutorial to learn about copying data from on-premises to cloud:</span><span class="sxs-lookup"><span data-stu-id="57e26-215">Advance to the following tutorial to learn about copying data from on-premises to cloud:</span></span> 

> [!div class="nextstepaction"]
>[<span data-ttu-id="57e26-216">Copy data from on-premises to cloud</span><span class="sxs-lookup"><span data-stu-id="57e26-216">Copy data from on-premises to cloud</span></span>](tutorial-hybrid-copy-powershell.md)
