---
title: Create an Azure data factory using REST API | Microsoft Docs
description: Create an Azure data factory to copy data from one location in Azure Blob storage to another location.
services: data-factory
documentationcenter: ''
author: linda33wj
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: ''
ms.devlang: rest-api
ms.topic: quickstart
ms.date: 01/22/2018
ms.author: jingwang
ms.openlocfilehash: cd529b63a4683f866a8a94379b6da12bee7eb775
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965804"
---
# <a name="create-an-azure-data-factory-and-pipeline-by-using-the-rest-api"></a><span data-ttu-id="f2d10-103">Create an Azure data factory and pipeline by using the REST API</span><span class="sxs-lookup"><span data-stu-id="f2d10-103">Create an Azure data factory and pipeline by using the REST API</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Current version](quickstart-create-data-factory-rest-api.md)

<span data-ttu-id="f2d10-106">Azure Data Factory is a cloud-based data integration service that allows you to create data-driven workflows in the cloud for orchestrating and automating data movement and data transformation.</span><span class="sxs-lookup"><span data-stu-id="f2d10-106">Azure Data Factory is a cloud-based data integration service that allows you to create data-driven workflows in the cloud for orchestrating and automating data movement and data transformation.</span></span> <span data-ttu-id="f2d10-107">Using Azure Data Factory, you can create and schedule data-driven workflows (called pipelines) that can ingest data from disparate data stores, process/transform the data by using compute services such as Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics, and Azure Machine Learning, and publish output data to data stores such as Azure SQL Data Warehouse for business intelligence (BI) applications to consume.</span><span class="sxs-lookup"><span data-stu-id="f2d10-107">Using Azure Data Factory, you can create and schedule data-driven workflows (called pipelines) that can ingest data from disparate data stores, process/transform the data by using compute services such as Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics, and Azure Machine Learning, and publish output data to data stores such as Azure SQL Data Warehouse for business intelligence (BI) applications to consume.</span></span> 

<span data-ttu-id="f2d10-108">This quickstart describes how to use REST API to create an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="f2d10-108">This quickstart describes how to use REST API to create an Azure data factory.</span></span> <span data-ttu-id="f2d10-109">The pipeline in this data factory copies data from one location to another location in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="f2d10-109">The pipeline in this data factory copies data from one location to another location in an Azure blob storage.</span></span>

<span data-ttu-id="f2d10-110">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="f2d10-110">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2d10-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="f2d10-111">Prerequisites</span></span>

* <span data-ttu-id="f2d10-112">**Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="f2d10-112">**Azure subscription**.</span></span> <span data-ttu-id="f2d10-113">If you don't have a subscription, you can create a [free trial](http://azure.microsoft.com/pricing/free-trial/) account.</span><span class="sxs-lookup"><span data-stu-id="f2d10-113">If you don't have a subscription, you can create a [free trial](http://azure.microsoft.com/pricing/free-trial/) account.</span></span>
* <span data-ttu-id="f2d10-114">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="f2d10-114">**Azure Storage account**.</span></span> <span data-ttu-id="f2d10-115">You use the blob storage as **source** and **sink** data store.</span><span class="sxs-lookup"><span data-stu-id="f2d10-115">You use the blob storage as **source** and **sink** data store.</span></span> <span data-ttu-id="f2d10-116">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="f2d10-116">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span></span>
* <span data-ttu-id="f2d10-117">Create a **blob container** in Blob Storage, create an input **folder** in the container, and upload some files to the folder.</span><span class="sxs-lookup"><span data-stu-id="f2d10-117">Create a **blob container** in Blob Storage, create an input **folder** in the container, and upload some files to the folder.</span></span> <span data-ttu-id="f2d10-118">You can use tools such as [Azure Storage explorer](https://azure.microsoft.com/features/storage-explorer/) to connect to Azure Blob storage, create a blob container, upload input file, and verify the output file.</span><span class="sxs-lookup"><span data-stu-id="f2d10-118">You can use tools such as [Azure Storage explorer](https://azure.microsoft.com/features/storage-explorer/) to connect to Azure Blob storage, create a blob container, upload input file, and verify the output file.</span></span>
* <span data-ttu-id="f2d10-119">Install **Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f2d10-119">Install **Azure PowerShell**.</span></span> <span data-ttu-id="f2d10-120">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="f2d10-120">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps).</span></span> <span data-ttu-id="f2d10-121">This quickstart uses PowerShell to invoke REST API calls.</span><span class="sxs-lookup"><span data-stu-id="f2d10-121">This quickstart uses PowerShell to invoke REST API calls.</span></span>
* <span data-ttu-id="f2d10-122">**Create an application in Azure Active Directory** following [this instruction](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application).</span><span class="sxs-lookup"><span data-stu-id="f2d10-122">**Create an application in Azure Active Directory** following [this instruction](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application).</span></span> <span data-ttu-id="f2d10-123">Make note of the following values that you use in later steps: **application ID**, **authentication key**, and **tenant ID**.</span><span class="sxs-lookup"><span data-stu-id="f2d10-123">Make note of the following values that you use in later steps: **application ID**, **authentication key**, and **tenant ID**.</span></span> <span data-ttu-id="f2d10-124">Assign application to "**Contributor**" role.</span><span class="sxs-lookup"><span data-stu-id="f2d10-124">Assign application to "**Contributor**" role.</span></span>

## <a name="set-global-variables"></a><span data-ttu-id="f2d10-125">Set global variables</span><span class="sxs-lookup"><span data-stu-id="f2d10-125">Set global variables</span></span>

1. <span data-ttu-id="f2d10-126">Launch **PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="f2d10-126">Launch **PowerShell**.</span></span> <span data-ttu-id="f2d10-127">Keep Azure PowerShell open until the end of this quickstart.</span><span class="sxs-lookup"><span data-stu-id="f2d10-127">Keep Azure PowerShell open until the end of this quickstart.</span></span> <span data-ttu-id="f2d10-128">If you close and reopen, you need to run the commands again.</span><span class="sxs-lookup"><span data-stu-id="f2d10-128">If you close and reopen, you need to run the commands again.</span></span>

    <span data-ttu-id="f2d10-129">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span><span class="sxs-lookup"><span data-stu-id="f2d10-129">Run the following command, and enter the user name and password that you use to sign in to the Azure portal:</span></span>
        
    ```powershell
    Connect-AzureRmAccount
    ```        
    <span data-ttu-id="f2d10-130">Run the following command to view all the subscriptions for this account:</span><span class="sxs-lookup"><span data-stu-id="f2d10-130">Run the following command to view all the subscriptions for this account:</span></span>

    ```powershell
    Get-AzureRmSubscription
    ```
    <span data-ttu-id="f2d10-131">Run the following command to select the subscription that you want to work with.</span><span class="sxs-lookup"><span data-stu-id="f2d10-131">Run the following command to select the subscription that you want to work with.</span></span> <span data-ttu-id="f2d10-132">Replace **SubscriptionId** with the ID of your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="f2d10-132">Replace **SubscriptionId** with the ID of your Azure subscription:</span></span>

    ```powershell
    Select-AzureRmSubscription -SubscriptionId "<SubscriptionId>"       
    ```
2. <span data-ttu-id="f2d10-133">Run the following commands after replacing the places-holders with your own values, to set global variables to be used in later steps.</span><span class="sxs-lookup"><span data-stu-id="f2d10-133">Run the following commands after replacing the places-holders with your own values, to set global variables to be used in later steps.</span></span>

    ```powershell
    $tenantID = "<your tenant ID>"
    $appId = "<your application ID>"
    $authKey = "<your authentication key for the application>"
    $subsId = "<your subscription ID to create the factory>"
    $resourceGroup = "<your resource group to create the factory>"
    $dataFactoryName = "<specify the name of data factory to create. It must be globally unique.>"
    $apiVersion = "2017-09-01-preview"
    ```

## <a name="authenticate-with-azure-ad"></a><span data-ttu-id="f2d10-134">Authenticate with Azure AD</span><span class="sxs-lookup"><span data-stu-id="f2d10-134">Authenticate with Azure AD</span></span>

<span data-ttu-id="f2d10-135">Run the following commands to authenticate with Azure Active Directory (AAD):</span><span class="sxs-lookup"><span data-stu-id="f2d10-135">Run the following commands to authenticate with Azure Active Directory (AAD):</span></span>

```powershell
$AuthContext = [Microsoft.IdentityModel.Clients.ActiveDirectory.AuthenticationContext]"https://login.microsoftonline.com/${tenantId}"
$cred = New-Object -TypeName Microsoft.IdentityModel.Clients.ActiveDirectory.ClientCredential -ArgumentList ($appId, $authKey)
$result = $AuthContext.AcquireToken("https://management.core.windows.net/", $cred)
$authHeader = @{
'Content-Type'='application/json'
'Accept'='application/json'
'Authorization'=$result.CreateAuthorizationHeader()
} 
```

## <a name="create-a-data-factory"></a><span data-ttu-id="f2d10-136">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="f2d10-136">Create a data factory</span></span>

<span data-ttu-id="f2d10-137">Run the following commands to create a data factory:</span><span class="sxs-lookup"><span data-stu-id="f2d10-137">Run the following commands to create a data factory:</span></span>

```powershell
$request = "https://management.azure.com/subscriptions/${subsId}/resourceGroups/${resourceGroup}/providers/Microsoft.DataFactory/factories/${dataFactoryName}?api-version=${apiVersion}"
$body = @"
{
    "name": "$dataFactoryName",
    "location": "East US",
    "properties": {},
    "identity": {
        "type": "SystemAssigned"
    }
}
"@
$response = Invoke-RestMethod -Method PUT -Uri $request -Header $authHeader -Body $body
$response | ConvertTo-Json
```

<span data-ttu-id="f2d10-138">Note the following points:</span><span class="sxs-lookup"><span data-stu-id="f2d10-138">Note the following points:</span></span>

* <span data-ttu-id="f2d10-139">The name of the Azure data factory must be globally unique.</span><span class="sxs-lookup"><span data-stu-id="f2d10-139">The name of the Azure data factory must be globally unique.</span></span> <span data-ttu-id="f2d10-140">If you receive the following error, change the name and try again.</span><span class="sxs-lookup"><span data-stu-id="f2d10-140">If you receive the following error, change the name and try again.</span></span>

    ```
    Data factory name "ADFv2QuickStartDataFactory" is not available.
    ```
* <span data-ttu-id="f2d10-141">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="f2d10-141">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="f2d10-142">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="f2d10-142">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>

<span data-ttu-id="f2d10-143">Here is the sample response:</span><span class="sxs-lookup"><span data-stu-id="f2d10-143">Here is the sample response:</span></span>

```json

{
    "name":  "<dataFactoryName>",
    "tags": {

            },
    "properties":  {
        "provisioningState":  "Succeeded",
        "loggingStorageAccountKey":  "**********",
        "createTime":  "2017-09-14T06:22:59.9106216Z",
        "version":  "2017-09-01-preview"
    },
    "identity":  {
        "type":  "SystemAssigned",
        "principalId":  "<service principal ID>",
        "tenantId":  "<tenant ID>"
    },
    "id":  "dataFactoryName",
    "type":  "Microsoft.DataFactory/factories",
    "location":  "East US"
} 

```

## <a name="create-linked-services"></a><span data-ttu-id="f2d10-144">Create linked services</span><span class="sxs-lookup"><span data-stu-id="f2d10-144">Create linked services</span></span>

<span data-ttu-id="f2d10-145">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="f2d10-145">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="f2d10-146">In this quickstart, you only need create one Azure Storage linked service as both copy source and sink store, named "AzureStorageLinkedService" in the sample.</span><span class="sxs-lookup"><span data-stu-id="f2d10-146">In this quickstart, you only need create one Azure Storage linked service as both copy source and sink store, named "AzureStorageLinkedService" in the sample.</span></span>

<span data-ttu-id="f2d10-147">Run the following commands to create a linked service named **AzureStorageLinkedService**:</span><span class="sxs-lookup"><span data-stu-id="f2d10-147">Run the following commands to create a linked service named **AzureStorageLinkedService**:</span></span>

<span data-ttu-id="f2d10-148">Replace &lt;accountName&gt; and &lt;accountKey&gt; with name and key of your Azure storage account before executing the commands.</span><span class="sxs-lookup"><span data-stu-id="f2d10-148">Replace &lt;accountName&gt; and &lt;accountKey&gt; with name and key of your Azure storage account before executing the commands.</span></span>

```powershell
$request = "https://management.azure.com/subscriptions/${subsId}/resourceGroups/${resourceGroup}/providers/Microsoft.DataFactory/factories/${dataFactoryName}/linkedservices/AzureStorageLinkedService?api-version=${apiVersion}"
$body = @"
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": {
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountName>;AccountKey=<accountKey>",
                "type": "SecureString"
            }
        }
    }
}
"@
$response = Invoke-RestMethod -Method PUT -Uri $request -Header $authHeader -Body $body
$response | ConvertTo-Json
```

<span data-ttu-id="f2d10-149">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="f2d10-149">Here is the sample output:</span></span>

```json
{
    "id":  "/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.DataFactory/factories/<dataFactoryName>/linkedservices/AzureStorageLinkedService",
    "name":  "AzureStorageLinkedService",
    "properties":  {
                       "type":  "AzureStorage",
                       "typeProperties":  {
                                              "connectionString":  "@{value=**********; type=SecureString}"
                                          }
                   },
    "etag":  "0000c552-0000-0000-0000-59b1459c0000"
}
```

## <a name="create-datasets"></a><span data-ttu-id="f2d10-150">Create datasets</span><span class="sxs-lookup"><span data-stu-id="f2d10-150">Create datasets</span></span>

<span data-ttu-id="f2d10-151">You define a dataset that represents the data to copy from a source to a sink.</span><span class="sxs-lookup"><span data-stu-id="f2d10-151">You define a dataset that represents the data to copy from a source to a sink.</span></span> <span data-ttu-id="f2d10-152">In this example, this Blob dataset refers to the Azure Storage linked service you create in the previous step.</span><span class="sxs-lookup"><span data-stu-id="f2d10-152">In this example, this Blob dataset refers to the Azure Storage linked service you create in the previous step.</span></span> <span data-ttu-id="f2d10-153">The dataset takes a parameter whose value is set in an activity that consumes the dataset.</span><span class="sxs-lookup"><span data-stu-id="f2d10-153">The dataset takes a parameter whose value is set in an activity that consumes the dataset.</span></span> <span data-ttu-id="f2d10-154">The parameter is used to construct the "folderPath" pointing to where the data resides/stored.</span><span class="sxs-lookup"><span data-stu-id="f2d10-154">The parameter is used to construct the "folderPath" pointing to where the data resides/stored.</span></span>

```powershell
$request = "https://management.azure.com/subscriptions/${subsId}/resourceGroups/${resourceGroup}/providers/Microsoft.DataFactory/factories/${dataFactoryName}/datasets/BlobDataset?api-version=${apiVersion}"
$body = @"
{
    "name": "BlobDataset",
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
"@
$response = Invoke-RestMethod -Method PUT -Uri $request -Header $authHeader -Body $body
$response | ConvertTo-Json
```

<span data-ttu-id="f2d10-155">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="f2d10-155">Here is the sample output:</span></span>

```json
{
    "id":  "/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.DataFactory/factories/<dataFactoryName>/datasets/BlobDataset",
    "name":  "BlobDataset",
    "properties":  {
                       "type":  "AzureBlob",
                       "typeProperties":  {
                                              "folderPath":  "@{value=@{dataset().path}; type=Expression}"
                                          },
                       "linkedServiceName":  {
                                                 "referenceName":  "AzureStorageLinkedService",
                                                 "type":  "LinkedServiceReference"
                                             },
                       "parameters":  {
                                          "path":  "@{type=String}"
                                      }
                   },
    "etag":  "0000c752-0000-0000-0000-59b1459d0000"
}
```

## <a name="create-pipeline"></a><span data-ttu-id="f2d10-156">Create pipeline</span><span class="sxs-lookup"><span data-stu-id="f2d10-156">Create pipeline</span></span>

<span data-ttu-id="f2d10-157">In this example, this pipeline contains one activity and takes two parameters - input blob path and output blob path.</span><span class="sxs-lookup"><span data-stu-id="f2d10-157">In this example, this pipeline contains one activity and takes two parameters - input blob path and output blob path.</span></span> <span data-ttu-id="f2d10-158">The values for these parameters are set when the pipeline is triggered/run.</span><span class="sxs-lookup"><span data-stu-id="f2d10-158">The values for these parameters are set when the pipeline is triggered/run.</span></span> <span data-ttu-id="f2d10-159">The copy activity refers to the same blob dataset created in the previous step as input and output.</span><span class="sxs-lookup"><span data-stu-id="f2d10-159">The copy activity refers to the same blob dataset created in the previous step as input and output.</span></span> <span data-ttu-id="f2d10-160">When the dataset is used as an input dataset, input path is specified.</span><span class="sxs-lookup"><span data-stu-id="f2d10-160">When the dataset is used as an input dataset, input path is specified.</span></span> <span data-ttu-id="f2d10-161">And, when the dataset is used as an output dataset, the output path is specified.</span><span class="sxs-lookup"><span data-stu-id="f2d10-161">And, when the dataset is used as an output dataset, the output path is specified.</span></span> 

```powershell
$request = "https://management.azure.com/subscriptions/${subsId}/resourceGroups/${resourceGroup}/providers/Microsoft.DataFactory/factories/${dataFactoryName}/pipelines/Adfv2QuickStartPipeline?api-version=${apiVersion}"
$body = @"
{
    "name": "Adfv2QuickStartPipeline",
    "properties": {
        "activities": [
            {
                "name": "CopyFromBlobToBlob",
                "type": "Copy",
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
                "typeProperties": {
                    "source": {
                        "type": "BlobSource"
                    },
                    "sink": {
                        "type": "BlobSink"
                    }
                }
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
"@
$response = Invoke-RestMethod -Method PUT -Uri $request -Header $authHeader -Body $body
$response | ConvertTo-Json
```

<span data-ttu-id="f2d10-162">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="f2d10-162">Here is the sample output:</span></span>

```json
{
    "id":  "/subscriptions/<subscriptionId>/resourceGroups/<resourceGroupName>/providers/Microsoft.DataFactory/factories/<dataFactoryName>/pipelines/Adfv2QuickStartPipeline",
    "name":  "Adfv2QuickStartPipeline",
    "properties":  {
                       "activities":  [
                                          "@{name=CopyFromBlobToBlob; type=Copy; inputs=System.Object[]; outputs=System.Object[]; typeProperties=}"
                                      ],
                       "parameters":  {
                                          "inputPath":  "@{type=String}",
                                          "outputPath":  "@{type=String}"
                                      }
                   },
    "etag":  "0000c852-0000-0000-0000-59b1459e0000"
}
```

## <a name="create-pipeline-run"></a><span data-ttu-id="f2d10-163">Create pipeline run</span><span class="sxs-lookup"><span data-stu-id="f2d10-163">Create pipeline run</span></span>

<span data-ttu-id="f2d10-164">In this step, you set values of **inputPath** and **outputPath** parameters specified in pipeline with the actual values of source and sink blob paths, and trigger a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="f2d10-164">In this step, you set values of **inputPath** and **outputPath** parameters specified in pipeline with the actual values of source and sink blob paths, and trigger a pipeline run.</span></span> <span data-ttu-id="f2d10-165">The pipeline run ID returned in the response body is used in later monitoring API.</span><span class="sxs-lookup"><span data-stu-id="f2d10-165">The pipeline run ID returned in the response body is used in later monitoring API.</span></span>

<span data-ttu-id="f2d10-166">Replace value of **inputPath** and **outputPath** with your source and sink blob path to copy data from and to before saving the file.</span><span class="sxs-lookup"><span data-stu-id="f2d10-166">Replace value of **inputPath** and **outputPath** with your source and sink blob path to copy data from and to before saving the file.</span></span>


```powershell
$request = "https://management.azure.com/subscriptions/${subsId}/resourceGroups/${resourceGroup}/providers/Microsoft.DataFactory/factories/${dataFactoryName}/pipelines/Adfv2QuickStartPipeline/createRun?api-version=${apiVersion}"
$body = @"
{
    "inputPath": "<the path to existing blob(s) to copy data from, e.g. containername/path>",
    "outputPath": "<the blob path to copy data to, e.g. containername/path>"
}
"@
$response = Invoke-RestMethod -Method POST -Uri $request -Header $authHeader -Body $body
$response | ConvertTo-Json
$runId = $response.runId
```

<span data-ttu-id="f2d10-167">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="f2d10-167">Here is the sample output:</span></span>

```json
{
    "runId":  "2f26be35-c112-43fa-9eaa-8ba93ea57881"
}
```

## <a name="monitor-pipeline"></a><span data-ttu-id="f2d10-168">Monitor pipeline</span><span class="sxs-lookup"><span data-stu-id="f2d10-168">Monitor pipeline</span></span>

1. <span data-ttu-id="f2d10-169">Run the following script to continuously check the pipeline run status until it finishes copying the data.</span><span class="sxs-lookup"><span data-stu-id="f2d10-169">Run the following script to continuously check the pipeline run status until it finishes copying the data.</span></span>

    ```powershell
    $request = "https://management.azure.com/subscriptions/${subsId}/resourceGroups/${resourceGroup}/providers/Microsoft.DataFactory/factories/${dataFactoryName}/pipelineruns/${runId}?api-version=${apiVersion}"
    while ($True) {
        $response = Invoke-RestMethod -Method GET -Uri $request -Header $authHeader
        Write-Host  "Pipeline run status: " $response.Status -foregroundcolor "Yellow"

        if ($response.Status -eq "InProgress") {
            Start-Sleep -Seconds 15
        }
        else {
            $response | ConvertTo-Json
            break
        }
    }
    ```

    <span data-ttu-id="f2d10-170">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="f2d10-170">Here is the sample output:</span></span>

    ```json
    {
        "key":  "000000000-0000-0000-0000-00000000000",
        "timestamp":  "2017-09-07T13:12:39.5561795Z",
        "runId":  "000000000-0000-0000-0000-000000000000",
        "dataFactoryName":  "<dataFactoryName>",
        "pipelineName":  "Adfv2QuickStartPipeline",
        "parameters":  [
                        "inputPath: <inputBlobPath>",
                        "outputPath: <outputBlobPath>"
                    ],
        "parametersCount":  2,
        "parameterNames":  [
                            "inputPath",
                            "outputPath"
                        ],
        "parameterNamesCount":  2,
        "parameterValues":  [
                                "<inputBlobPath>",
                                "<outputBlobPath>"
                            ],
        "parameterValuesCount":  2,
        "runStart":  "2017-09-07T13:12:00.3710792Z",
        "runEnd":  "2017-09-07T13:12:39.5561795Z",
        "durationInMs":  39185,
        "status":  "Succeeded",
        "message":  ""
    }
    ```

2. <span data-ttu-id="f2d10-171">Run the following script to retrieve copy activity run details, for example, size of the data read/written.</span><span class="sxs-lookup"><span data-stu-id="f2d10-171">Run the following script to retrieve copy activity run details, for example, size of the data read/written.</span></span>

    ```PowerShell
    $request = "https://management.azure.com/subscriptions/${subsId}/resourceGroups/${resourceGroup}/providers/Microsoft.DataFactory/factories/${dataFactoryName}/pipelineruns/${runId}/activityruns?api-version=${apiVersion}&startTime="+(Get-Date).ToString('yyyy-MM-dd')+"&endTime="+(Get-Date).AddDays(1).ToString('yyyy-MM-dd')+"&pipelineName=Adfv2QuickStartPipeline"
    $response = Invoke-RestMethod -Method GET -Uri $request -Header $authHeader
    $response | ConvertTo-Json
    ```

    <span data-ttu-id="f2d10-172">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="f2d10-172">Here is the sample output:</span></span>

    ```json
    {
        "value":  [
                    {
                        "id":  "000000000-0000-0000-0000-00000000000",
                        "timestamp":  "2017-09-07T13:12:38.4780542Z",
                        "pipelineRunId":  "000000000-0000-00000-0000-0000000000000",
                        "pipelineName":  "Adfv2QuickStartPipeline",
                        "status":  "Succeeded",
                        "failureType":  "",
                        "linkedServiceName":  "",
                        "activityName":  "CopyFromBlobToBlob",
                        "activityType":  "Copy",
                        "activityStart":  "2017-09-07T13:12:02.3299261Z",
                        "activityEnd":  "2017-09-07T13:12:38.4780542Z",
                        "duration":  36148,
                        "input":  "@{source=; sink=}",
                        "output":  "@{dataRead=331452208; dataWritten=331452208; copyDuration=22; throughput=14712.9; errors=System.Object[]; effectiveIntegrationRuntime=DefaultIntegrationRuntime (West US); usedDataIntegrationUnits=2; billedDuration=22}",
                        "error":  "@{errorCode=; message=; failureType=; target=CopyFromBlobToBlob}"
                    }
                ]
    }
    ```

## <a name="verify-the-output"></a><span data-ttu-id="f2d10-173">Verify the output</span><span class="sxs-lookup"><span data-stu-id="f2d10-173">Verify the output</span></span>

<span data-ttu-id="f2d10-174">Use Azure Storage explorer to check the blob(s) is copied to "outputBlobPath" from "inputBlobPath" as you specified when creating a pipeline run.</span><span class="sxs-lookup"><span data-stu-id="f2d10-174">Use Azure Storage explorer to check the blob(s) is copied to "outputBlobPath" from "inputBlobPath" as you specified when creating a pipeline run.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="f2d10-175">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="f2d10-175">Clean up resources</span></span>
<span data-ttu-id="f2d10-176">You can clean up the resources that you created in the Quickstart in two ways.</span><span class="sxs-lookup"><span data-stu-id="f2d10-176">You can clean up the resources that you created in the Quickstart in two ways.</span></span> <span data-ttu-id="f2d10-177">You can delete the [Azure resource group](../azure-resource-manager/resource-group-overview.md), which includes all the resources in the resource group.</span><span class="sxs-lookup"><span data-stu-id="f2d10-177">You can delete the [Azure resource group](../azure-resource-manager/resource-group-overview.md), which includes all the resources in the resource group.</span></span> <span data-ttu-id="f2d10-178">If you want to keep the other resources intact, delete only the data factory you created in this tutorial.</span><span class="sxs-lookup"><span data-stu-id="f2d10-178">If you want to keep the other resources intact, delete only the data factory you created in this tutorial.</span></span>

<span data-ttu-id="f2d10-179">Run the following command to delete the entire resource group:</span><span class="sxs-lookup"><span data-stu-id="f2d10-179">Run the following command to delete the entire resource group:</span></span> 
```powershell
Remove-AzureRmResourceGroup -ResourceGroupName $resourcegroupname
```

<span data-ttu-id="f2d10-180">Run the following command to delete only the data factory:</span><span class="sxs-lookup"><span data-stu-id="f2d10-180">Run the following command to delete only the data factory:</span></span> 

```powershell
Remove-AzureRmDataFactoryV2 -Name "<NameOfYourDataFactory>" -ResourceGroupName "<NameOfResourceGroup>"
```

## <a name="next-steps"></a><span data-ttu-id="f2d10-181">Next steps</span><span class="sxs-lookup"><span data-stu-id="f2d10-181">Next steps</span></span>
<span data-ttu-id="f2d10-182">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="f2d10-182">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span></span> <span data-ttu-id="f2d10-183">Go through the [tutorials](tutorial-copy-data-dot-net.md) to learn about using Data Factory in more scenarios.</span><span class="sxs-lookup"><span data-stu-id="f2d10-183">Go through the [tutorials](tutorial-copy-data-dot-net.md) to learn about using Data Factory in more scenarios.</span></span> 
