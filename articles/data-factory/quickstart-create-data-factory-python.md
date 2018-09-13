---
title: Create an Azure data factory using Python | Microsoft Docs
description: Create an Azure data factory to copy data from one location in Azure Blob storage to another location.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.reviewer: douglasl
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: ''
ms.devlang: python
ms.topic: quickstart
ms.date: 01/22/2018
ms.author: shlo
ms.openlocfilehash: 5b8e1d894a0f2b7868433cb25a097a4cfcdc1796
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968086"
---
# <a name="create-a-data-factory-and-pipeline-using-python"></a><span data-ttu-id="0b119-103">Create a data factory and pipeline using Python</span><span class="sxs-lookup"><span data-stu-id="0b119-103">Create a data factory and pipeline using Python</span></span>
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Version 1](v1/data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Current version](quickstart-create-data-factory-python.md)

<span data-ttu-id="0b119-106">Azure Data Factory is a cloud-based data integration service that allows you to create data-driven workflows in the cloud for orchestrating and automating data movement and data transformation.</span><span class="sxs-lookup"><span data-stu-id="0b119-106">Azure Data Factory is a cloud-based data integration service that allows you to create data-driven workflows in the cloud for orchestrating and automating data movement and data transformation.</span></span> <span data-ttu-id="0b119-107">Using Azure Data Factory, you can create and schedule data-driven workflows (called pipelines) that can ingest data from disparate data stores, process/transform the data by using compute services such as Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics, and Azure Machine Learning, and publish output data to data stores such as Azure SQL Data Warehouse for business intelligence (BI) applications to consume.</span><span class="sxs-lookup"><span data-stu-id="0b119-107">Using Azure Data Factory, you can create and schedule data-driven workflows (called pipelines) that can ingest data from disparate data stores, process/transform the data by using compute services such as Azure HDInsight Hadoop, Spark, Azure Data Lake Analytics, and Azure Machine Learning, and publish output data to data stores such as Azure SQL Data Warehouse for business intelligence (BI) applications to consume.</span></span>

<span data-ttu-id="0b119-108">This quickstart describes how to use Python to create an Azure data factory.</span><span class="sxs-lookup"><span data-stu-id="0b119-108">This quickstart describes how to use Python to create an Azure data factory.</span></span> <span data-ttu-id="0b119-109">The pipeline in this data factory copies data from one folder to another folder in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="0b119-109">The pipeline in this data factory copies data from one folder to another folder in an Azure blob storage.</span></span>

<span data-ttu-id="0b119-110">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span><span class="sxs-lookup"><span data-stu-id="0b119-110">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0b119-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0b119-111">Prerequisites</span></span>

* <span data-ttu-id="0b119-112">**Azure Storage account**.</span><span class="sxs-lookup"><span data-stu-id="0b119-112">**Azure Storage account**.</span></span> <span data-ttu-id="0b119-113">You use the blob storage as **source** and **sink** data store.</span><span class="sxs-lookup"><span data-stu-id="0b119-113">You use the blob storage as **source** and **sink** data store.</span></span> <span data-ttu-id="0b119-114">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span><span class="sxs-lookup"><span data-stu-id="0b119-114">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-quickstart-create-account.md) article for steps to create one.</span></span>
* <span data-ttu-id="0b119-115">**Create an application in Azure Active Directory** following [this instruction](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application).</span><span class="sxs-lookup"><span data-stu-id="0b119-115">**Create an application in Azure Active Directory** following [this instruction](../azure-resource-manager/resource-group-create-service-principal-portal.md#create-an-azure-active-directory-application).</span></span> <span data-ttu-id="0b119-116">Make note of the following values that you use in later steps: **application ID**, **authentication key**, and **tenant ID**.</span><span class="sxs-lookup"><span data-stu-id="0b119-116">Make note of the following values that you use in later steps: **application ID**, **authentication key**, and **tenant ID**.</span></span> <span data-ttu-id="0b119-117">Assign application to "**Contributor**" role by following instructions in the same article.</span><span class="sxs-lookup"><span data-stu-id="0b119-117">Assign application to "**Contributor**" role by following instructions in the same article.</span></span>

### <a name="create-and-upload-an-input-file"></a><span data-ttu-id="0b119-118">Create and upload an input file</span><span class="sxs-lookup"><span data-stu-id="0b119-118">Create and upload an input file</span></span>

1. <span data-ttu-id="0b119-119">Launch Notepad.</span><span class="sxs-lookup"><span data-stu-id="0b119-119">Launch Notepad.</span></span> <span data-ttu-id="0b119-120">Copy the following text and save it as **input.txt** file on your disk.</span><span class="sxs-lookup"><span data-stu-id="0b119-120">Copy the following text and save it as **input.txt** file on your disk.</span></span>

    ```
    John|Doe
    Jane|Doe
    ```
2.  <span data-ttu-id="0b119-121">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adfv2tutorial** container, and **input** folder in the container.</span><span class="sxs-lookup"><span data-stu-id="0b119-121">Use tools such as [Azure Storage Explorer](http://storageexplorer.com/) to create the **adfv2tutorial** container, and **input** folder in the container.</span></span> <span data-ttu-id="0b119-122">Then, upload the **input.txt** file to the **input** folder.</span><span class="sxs-lookup"><span data-stu-id="0b119-122">Then, upload the **input.txt** file to the **input** folder.</span></span>

## <a name="install-the-python-package"></a><span data-ttu-id="0b119-123">Install the Python package</span><span class="sxs-lookup"><span data-stu-id="0b119-123">Install the Python package</span></span>
1. <span data-ttu-id="0b119-124">Open a terminal or command prompt with administrator privileges.</span><span class="sxs-lookup"><span data-stu-id="0b119-124">Open a terminal or command prompt with administrator privileges.</span></span> 
2. <span data-ttu-id="0b119-125">First, install the Python package for Azure management resources:</span><span class="sxs-lookup"><span data-stu-id="0b119-125">First, install the Python package for Azure management resources:</span></span>

    ```
    pip install azure-mgmt-resource
    ```
3. <span data-ttu-id="0b119-126">To install the Python package for Data Factory, run the following command:</span><span class="sxs-lookup"><span data-stu-id="0b119-126">To install the Python package for Data Factory, run the following command:</span></span>

    ```
    pip install azure-mgmt-datafactory
    ```

    <span data-ttu-id="0b119-127">The [Python SDK for Data Factory](https://github.com/Azure/azure-sdk-for-python) supports Python 2.7, 3.3, 3.4, 3.5 and 3.6.</span><span class="sxs-lookup"><span data-stu-id="0b119-127">The [Python SDK for Data Factory](https://github.com/Azure/azure-sdk-for-python) supports Python 2.7, 3.3, 3.4, 3.5 and 3.6.</span></span>

## <a name="create-a-data-factory-client"></a><span data-ttu-id="0b119-128">Create a data factory client</span><span class="sxs-lookup"><span data-stu-id="0b119-128">Create a data factory client</span></span>

1. <span data-ttu-id="0b119-129">Create a file named **datafactory.py**.</span><span class="sxs-lookup"><span data-stu-id="0b119-129">Create a file named **datafactory.py**.</span></span> <span data-ttu-id="0b119-130">Add the following statements to add references to namespaces.</span><span class="sxs-lookup"><span data-stu-id="0b119-130">Add the following statements to add references to namespaces.</span></span>

    ```python
    from azure.common.credentials import ServicePrincipalCredentials
    from azure.mgmt.resource import ResourceManagementClient
    from azure.mgmt.datafactory import DataFactoryManagementClient
    from azure.mgmt.datafactory.models import *
    from datetime import datetime, timedelta
    import time
    ```
2. <span data-ttu-id="0b119-131">Add the following functions that print information.</span><span class="sxs-lookup"><span data-stu-id="0b119-131">Add the following functions that print information.</span></span>

    ```python
    def print_item(group):
        """Print an Azure object instance."""
        print("\tName: {}".format(group.name))
        print("\tId: {}".format(group.id))
        if hasattr(group, 'location'):
            print("\tLocation: {}".format(group.location))
        if hasattr(group, 'tags'):
            print("\tTags: {}".format(group.tags))
        if hasattr(group, 'properties'):
            print_properties(group.properties)

    def print_properties(props):
        """Print a ResourceGroup properties instance."""
        if props and hasattr(props, 'provisioning_state') and props.provisioning_state:
            print("\tProperties:")
            print("\t\tProvisioning State: {}".format(props.provisioning_state))
        print("\n\n")

    def print_activity_run_details(activity_run):
        """Print activity run details."""
        print("\n\tActivity run details\n")
        print("\tActivity run status: {}".format(activity_run.status))    
        if activity_run.status == 'Succeeded':
            print("\tNumber of bytes read: {}".format(activity_run.output['dataRead']))       
            print("\tNumber of bytes written: {}".format(activity_run.output['dataWritten']))           
            print("\tCopy duration: {}".format(activity_run.output['copyDuration']))           
        else:
            print("\tErrors: {}".format(activity_run.error['message']))

    ```
3. <span data-ttu-id="0b119-132">Add the following code to the **Main** method that creates an instance of DataFactoryManagementClient class.</span><span class="sxs-lookup"><span data-stu-id="0b119-132">Add the following code to the **Main** method that creates an instance of DataFactoryManagementClient class.</span></span> <span data-ttu-id="0b119-133">You use this object to create the data factory, linked service, datasets, and pipeline.</span><span class="sxs-lookup"><span data-stu-id="0b119-133">You use this object to create the data factory, linked service, datasets, and pipeline.</span></span> <span data-ttu-id="0b119-134">You also use this object to monitor the pipeline run details.</span><span class="sxs-lookup"><span data-stu-id="0b119-134">You also use this object to monitor the pipeline run details.</span></span> <span data-ttu-id="0b119-135">Set **subscription_id** variable to the ID of your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="0b119-135">Set **subscription_id** variable to the ID of your Azure subscription.</span></span> <span data-ttu-id="0b119-136">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="0b119-136">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span> <span data-ttu-id="0b119-137">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span><span class="sxs-lookup"><span data-stu-id="0b119-137">The data stores (Azure Storage, Azure SQL Database, etc.) and computes (HDInsight, etc.) used by data factory can be in other regions.</span></span>

    ```python   
    def main():

        # Azure subscription ID
        subscription_id = '<Specify your Azure Subscription ID>'

        # This program creates this resource group. If it's an existing resource group, comment out the code that creates the resource group
        rg_name = 'ADFTutorialResourceGroup'

        # The data factory name. It must be globally unique.
        df_name = '<Specify a name for the data factory. It must be globally unique>'

        # Specify your Active Directory client ID, client secret, and tenant ID
        credentials = ServicePrincipalCredentials(client_id='<Active Directory application/client ID>', secret='<client secret>', tenant='<Active Directory tenant ID>')
        resource_client = ResourceManagementClient(credentials, subscription_id)
        adf_client = DataFactoryManagementClient(credentials, subscription_id)

        rg_params = {'location':'eastus'}
        df_params = {'location':'eastus'}    
    ```

## <a name="create-a-data-factory"></a><span data-ttu-id="0b119-138">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="0b119-138">Create a data factory</span></span>

<span data-ttu-id="0b119-139">Add the following code to the **Main** method that creates a **data factory**.</span><span class="sxs-lookup"><span data-stu-id="0b119-139">Add the following code to the **Main** method that creates a **data factory**.</span></span> <span data-ttu-id="0b119-140">If your resource group already exists, comment out the first `create_or_update` statement.</span><span class="sxs-lookup"><span data-stu-id="0b119-140">If your resource group already exists, comment out the first `create_or_update` statement.</span></span>

```python
    # create the resource group
    # comment out if the resource group already exits
    resource_client.resource_groups.create_or_update(rg_name, rg_params)

    #Create a data factory
    df_resource = Factory(location='eastus')
    df = adf_client.factories.create_or_update(rg_name, df_name, df_resource)
    print_item(df)
    while df.provisioning_state != 'Succeeded':
        df = adf_client.factories.get(rg_name, df_name)
        time.sleep(1)
```

## <a name="create-a-linked-service"></a><span data-ttu-id="0b119-141">Create a linked service</span><span class="sxs-lookup"><span data-stu-id="0b119-141">Create a linked service</span></span>

<span data-ttu-id="0b119-142">Add the following code to the **Main** method that creates an **Azure Storage linked service**.</span><span class="sxs-lookup"><span data-stu-id="0b119-142">Add the following code to the **Main** method that creates an **Azure Storage linked service**.</span></span>

<span data-ttu-id="0b119-143">You create linked services in a data factory to link your data stores and compute services to the data factory.</span><span class="sxs-lookup"><span data-stu-id="0b119-143">You create linked services in a data factory to link your data stores and compute services to the data factory.</span></span> <span data-ttu-id="0b119-144">In this quickstart, you only need create one Azure Storage linked service as both copy source and sink store, named "AzureStorageLinkedService" in the sample.</span><span class="sxs-lookup"><span data-stu-id="0b119-144">In this quickstart, you only need create one Azure Storage linked service as both copy source and sink store, named "AzureStorageLinkedService" in the sample.</span></span> <span data-ttu-id="0b119-145">Replace `<storageaccountname>` and `<storageaccountkey>` with name and key of your Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="0b119-145">Replace `<storageaccountname>` and `<storageaccountkey>` with name and key of your Azure Storage account.</span></span>

```python
    # Create an Azure Storage linked service
    ls_name = 'storageLinkedService'

    # IMPORTANT: specify the name and key of your Azure Storage account.
    storage_string = SecureString('DefaultEndpointsProtocol=https;AccountName=<storageaccountname>;AccountKey=<storageaccountkey>')

    ls_azure_storage = AzureStorageLinkedService(connection_string=storage_string)
    ls = adf_client.linked_services.create_or_update(rg_name, df_name, ls_name, ls_azure_storage)
    print_item(ls)
```
## <a name="create-datasets"></a><span data-ttu-id="0b119-146">Create datasets</span><span class="sxs-lookup"><span data-stu-id="0b119-146">Create datasets</span></span>
<span data-ttu-id="0b119-147">In this section, you create two datasets: one for the source and the other for the sink.</span><span class="sxs-lookup"><span data-stu-id="0b119-147">In this section, you create two datasets: one for the source and the other for the sink.</span></span>

### <a name="create-a-dataset-for-source-azure-blob"></a><span data-ttu-id="0b119-148">Create a dataset for source Azure Blob</span><span class="sxs-lookup"><span data-stu-id="0b119-148">Create a dataset for source Azure Blob</span></span>
<span data-ttu-id="0b119-149">Add the following code to the Main method that creates an Azure blob dataset.</span><span class="sxs-lookup"><span data-stu-id="0b119-149">Add the following code to the Main method that creates an Azure blob dataset.</span></span> <span data-ttu-id="0b119-150">For information about properties of Azure Blob dataset, see [Azure blob connector](connector-azure-blob-storage.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="0b119-150">For information about properties of Azure Blob dataset, see [Azure blob connector](connector-azure-blob-storage.md#dataset-properties) article.</span></span>

<span data-ttu-id="0b119-151">You define a dataset that represents the source data in Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="0b119-151">You define a dataset that represents the source data in Azure Blob.</span></span> <span data-ttu-id="0b119-152">This Blob dataset refers to the Azure Storage linked service you create in the previous step.</span><span class="sxs-lookup"><span data-stu-id="0b119-152">This Blob dataset refers to the Azure Storage linked service you create in the previous step.</span></span>

```python
    # Create an Azure blob dataset (input)
    ds_name = 'ds_in'
    ds_ls = LinkedServiceReference(ls_name)
    blob_path= 'adfv2tutorial/input'
    blob_filename = 'input.txt'
    ds_azure_blob= AzureBlobDataset(ds_ls, folder_path=blob_path, file_name = blob_filename)
    ds = adf_client.datasets.create_or_update(rg_name, df_name, ds_name, ds_azure_blob)
    print_item(ds)
```

### <a name="create-a-dataset-for-sink-azure-blob"></a><span data-ttu-id="0b119-153">Create a dataset for sink Azure Blob</span><span class="sxs-lookup"><span data-stu-id="0b119-153">Create a dataset for sink Azure Blob</span></span>
<span data-ttu-id="0b119-154">Add the following code to the Main method that creates an Azure blob dataset.</span><span class="sxs-lookup"><span data-stu-id="0b119-154">Add the following code to the Main method that creates an Azure blob dataset.</span></span> <span data-ttu-id="0b119-155">For information about properties of Azure Blob dataset, see [Azure blob connector](connector-azure-blob-storage.md#dataset-properties) article.</span><span class="sxs-lookup"><span data-stu-id="0b119-155">For information about properties of Azure Blob dataset, see [Azure blob connector](connector-azure-blob-storage.md#dataset-properties) article.</span></span>

<span data-ttu-id="0b119-156">You define a dataset that represents the source data in Azure Blob.</span><span class="sxs-lookup"><span data-stu-id="0b119-156">You define a dataset that represents the source data in Azure Blob.</span></span> <span data-ttu-id="0b119-157">This Blob dataset refers to the Azure Storage linked service you create in the previous step.</span><span class="sxs-lookup"><span data-stu-id="0b119-157">This Blob dataset refers to the Azure Storage linked service you create in the previous step.</span></span>

```python
    # Create an Azure blob dataset (output)
    dsOut_name = 'ds_out'
    output_blobpath = 'adfv2tutorial/output'
    dsOut_azure_blob = AzureBlobDataset(ds_ls, folder_path=output_blobpath)
    dsOut = adf_client.datasets.create_or_update(rg_name, df_name, dsOut_name, dsOut_azure_blob)
    print_item(dsOut)
```

## <a name="create-a-pipeline"></a><span data-ttu-id="0b119-158">Create a pipeline</span><span class="sxs-lookup"><span data-stu-id="0b119-158">Create a pipeline</span></span>

<span data-ttu-id="0b119-159">Add the following code to the **Main** method that creates a **pipeline with a copy activity**.</span><span class="sxs-lookup"><span data-stu-id="0b119-159">Add the following code to the **Main** method that creates a **pipeline with a copy activity**.</span></span>

```python
    # Create a copy activity
    act_name =  'copyBlobtoBlob'
    blob_source = BlobSource()
    blob_sink = BlobSink()
    dsin_ref = DatasetReference(ds_name)
    dsOut_ref = DatasetReference(dsOut_name)
    copy_activity = CopyActivity(act_name,inputs=[dsin_ref], outputs=[dsOut_ref], source=blob_source, sink=blob_sink)

    #Create a pipeline with the copy activity
    p_name =  'copyPipeline'
    params_for_pipeline = {}
    p_obj = PipelineResource(activities=[copy_activity], parameters=params_for_pipeline)
    p = adf_client.pipelines.create_or_update(rg_name, df_name, p_name, p_obj)
    print_item(p)
```


## <a name="create-a-pipeline-run"></a><span data-ttu-id="0b119-160">Create a pipeline run</span><span class="sxs-lookup"><span data-stu-id="0b119-160">Create a pipeline run</span></span>

<span data-ttu-id="0b119-161">Add the following code to the **Main** method that **triggers a pipeline run**.</span><span class="sxs-lookup"><span data-stu-id="0b119-161">Add the following code to the **Main** method that **triggers a pipeline run**.</span></span>

```python
    #Create a pipeline run.
    run_response = adf_client.pipelines.create_run(rg_name, df_name, p_name,
        {
        }
    )
```

## <a name="monitor-a-pipeline-run"></a><span data-ttu-id="0b119-162">Monitor a pipeline run</span><span class="sxs-lookup"><span data-stu-id="0b119-162">Monitor a pipeline run</span></span>
<span data-ttu-id="0b119-163">To monitor the pipeline run, add the following code the **Main** method:</span><span class="sxs-lookup"><span data-stu-id="0b119-163">To monitor the pipeline run, add the following code the **Main** method:</span></span>

```python
    #Monitor the pipeline run
    time.sleep(30)
    pipeline_run = adf_client.pipeline_runs.get(rg_name, df_name, run_response.run_id)
    print("\n\tPipeline run status: {}".format(pipeline_run.status))
    activity_runs_paged = list(adf_client.activity_runs.list_by_pipeline_run(rg_name, df_name, pipeline_run.run_id, datetime.now() - timedelta(1),  datetime.now() + timedelta(1)))
    print_activity_run_details(activity_runs_paged[0])
```

<span data-ttu-id="0b119-164">Now, add the following statement to invoke the **main** method when the program is run:</span><span class="sxs-lookup"><span data-stu-id="0b119-164">Now, add the following statement to invoke the **main** method when the program is run:</span></span>

```python
# Start the main method
main()
```

## <a name="full-script"></a><span data-ttu-id="0b119-165">Full script</span><span class="sxs-lookup"><span data-stu-id="0b119-165">Full script</span></span>
<span data-ttu-id="0b119-166">Here is the full Python code:</span><span class="sxs-lookup"><span data-stu-id="0b119-166">Here is the full Python code:</span></span>

```python
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.datafactory import DataFactoryManagementClient
from azure.mgmt.datafactory.models import *
from datetime import datetime, timedelta
import time

def print_item(group):
    """Print an Azure object instance."""
    print("\tName: {}".format(group.name))
    print("\tId: {}".format(group.id))
    if hasattr(group, 'location'):
        print("\tLocation: {}".format(group.location))
    if hasattr(group, 'tags'):
        print("\tTags: {}".format(group.tags))
    if hasattr(group, 'properties'):
        print_properties(group.properties)
    print("\n")        

def print_properties(props):
    """Print a ResourceGroup properties instance."""
    if props and hasattr(props, 'provisioning_state') and props.provisioning_state:
        print("\tProperties:")
        print("\t\tProvisioning State: {}".format(props.provisioning_state))
    print("\n")

def print_activity_run_details(activity_run):
    """Print activity run details."""
    print("\n\tActivity run details\n")
    print("\tActivity run status: {}".format(activity_run.status))    
    if activity_run.status == 'Succeeded':
        print("\tNumber of bytes read: {}".format(activity_run.output['dataRead']))       
        print("\tNumber of bytes written: {}".format(activity_run.output['dataWritten']))           
        print("\tCopy duration: {}".format(activity_run.output['copyDuration']))           
    else:
        print("\tErrors: {}".format(activity_run.error['message']))

def main():

    # Azure subscription ID
    subscription_id = '<your Azure subscription ID>'

    # This program creates this resource group. If it's an existing resource group, comment out the code that creates the resource group
    rg_name = '<Azure resource group name>'

    # The data factory name. It must be globally unique.
    df_name = '<Your data factory name>'        

    # Specify your Active Directory client ID, client secret, and tenant ID
    credentials = ServicePrincipalCredentials(client_id='<Active Directory client ID>', secret='<client secret>', tenant='<tenant ID>')
    resource_client = ResourceManagementClient(credentials, subscription_id)
    adf_client = DataFactoryManagementClient(credentials, subscription_id)

    rg_params = {'location':'eastus'}
    df_params = {'location':'eastus'}

    # create the resource group
    # comment out if the resource group already exits
    resource_client.resource_groups.create_or_update(rg_name, rg_params)

    # Create a data factory
    df_resource = Factory(location='eastus')
    df = adf_client.factories.create_or_update(rg_name, df_name, df_resource)
    print_item(df)
    while df.provisioning_state != 'Succeeded':
        df = adf_client.factories.get(rg_name, df_name)
        time.sleep(1)

    # Create an Azure Storage linked service
    ls_name = 'storageLinkedService'

    # Specify the name and key of your Azure Storage account
    storage_string = SecureString('DefaultEndpointsProtocol=https;AccountName=<storage account name>;AccountKey=<storage account key>')

    ls_azure_storage = AzureStorageLinkedService(connection_string=storage_string)
    ls = adf_client.linked_services.create_or_update(rg_name, df_name, ls_name, ls_azure_storage)
    print_item(ls)

    # Create an Azure blob dataset (input)
    ds_name = 'ds_in'
    ds_ls = LinkedServiceReference(ls_name)
    blob_path= 'adfv2tutorial/input'
    blob_filename = 'input.txt'
    ds_azure_blob= AzureBlobDataset(ds_ls, folder_path=blob_path, file_name = blob_filename)
    ds = adf_client.datasets.create_or_update(rg_name, df_name, ds_name, ds_azure_blob)
    print_item(ds)

    # Create an Azure blob dataset (output)
    dsOut_name = 'ds_out'
    output_blobpath = 'adfv2tutorial/output'
    dsOut_azure_blob = AzureBlobDataset(ds_ls, folder_path=output_blobpath)
    dsOut = adf_client.datasets.create_or_update(rg_name, df_name, dsOut_name, dsOut_azure_blob)
    print_item(dsOut)

    # Create a copy activity
    act_name =  'copyBlobtoBlob'
    blob_source = BlobSource()
    blob_sink = BlobSink()
    dsin_ref = DatasetReference(ds_name)
    dsOut_ref = DatasetReference(dsOut_name)
    copy_activity = CopyActivity(act_name,inputs=[dsin_ref], outputs=[dsOut_ref], source=blob_source, sink=blob_sink)

    # Create a pipeline with the copy activity
    p_name =  'copyPipeline'
    params_for_pipeline = {}
    p_obj = PipelineResource(activities=[copy_activity], parameters=params_for_pipeline)
    p = adf_client.pipelines.create_or_update(rg_name, df_name, p_name, p_obj)
    print_item(p)

    # Create a pipeline run
    run_response = adf_client.pipelines.create_run(rg_name, df_name, p_name,
        {
        }
    )

    # Monitor the pipeilne run
    time.sleep(30)
    pipeline_run = adf_client.pipeline_runs.get(rg_name, df_name, run_response.run_id)
    print("\n\tPipeline run status: {}".format(pipeline_run.status))
    activity_runs_paged = list(adf_client.activity_runs.list_by_pipeline_run(rg_name, df_name, pipeline_run.run_id, datetime.now() - timedelta(1),  datetime.now() + timedelta(1)))
    print_activity_run_details(activity_runs_paged[0])

# Start the main method
main()
```

## <a name="run-the-code"></a><span data-ttu-id="0b119-167">Run the code</span><span class="sxs-lookup"><span data-stu-id="0b119-167">Run the code</span></span>
<span data-ttu-id="0b119-168">Build and start the application, then verify the pipeline execution.</span><span class="sxs-lookup"><span data-stu-id="0b119-168">Build and start the application, then verify the pipeline execution.</span></span>

<span data-ttu-id="0b119-169">The console prints the progress of creating data factory, linked service, datasets, pipeline, and pipeline run.</span><span class="sxs-lookup"><span data-stu-id="0b119-169">The console prints the progress of creating data factory, linked service, datasets, pipeline, and pipeline run.</span></span> <span data-ttu-id="0b119-170">Wait until you see the copy activity run details with data read/written size.</span><span class="sxs-lookup"><span data-stu-id="0b119-170">Wait until you see the copy activity run details with data read/written size.</span></span> <span data-ttu-id="0b119-171">Then, use tools such as [Azure Storage explorer](https://azure.microsoft.com/features/storage-explorer/) to check the blob(s) is copied to "outputBlobPath" from "inputBlobPath" as you specified in variables.</span><span class="sxs-lookup"><span data-stu-id="0b119-171">Then, use tools such as [Azure Storage explorer](https://azure.microsoft.com/features/storage-explorer/) to check the blob(s) is copied to "outputBlobPath" from "inputBlobPath" as you specified in variables.</span></span>

<span data-ttu-id="0b119-172">Here is the sample output:</span><span class="sxs-lookup"><span data-stu-id="0b119-172">Here is the sample output:</span></span>

```json
Name: <data factory name>
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.DataFactory/factories/<data factory name>
Location: eastus
Tags: {}

Name: storageLinkedService
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.DataFactory/factories/<data factory name>/linkedservices/storageLinkedService

Name: ds_in
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.DataFactory/factories/<data factory name>/datasets/ds_in

Name: ds_out
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.DataFactory/factories/<data factory name>/datasets/ds_out

Name: copyPipeline
Id: /subscriptions/<subscription ID>/resourceGroups/<resource group name>/providers/Microsoft.DataFactory/factories/<data factory name>/pipelines/copyPipeline

Pipeline run status: Succeeded
Datetime with no tzinfo will be considered UTC.
Datetime with no tzinfo will be considered UTC.

Activity run details

Activity run status: Succeeded
Number of bytes read: 18
Number of bytes written: 18
Copy duration: 4
```


## <a name="clean-up-resources"></a><span data-ttu-id="0b119-173">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="0b119-173">Clean up resources</span></span>
<span data-ttu-id="0b119-174">To delete the data factory, add the following code to the program:</span><span class="sxs-lookup"><span data-stu-id="0b119-174">To delete the data factory, add the following code to the program:</span></span>

```python
adf_client.factories.delete(rg_name,df_name)
```

## <a name="next-steps"></a><span data-ttu-id="0b119-175">Next steps</span><span class="sxs-lookup"><span data-stu-id="0b119-175">Next steps</span></span>
<span data-ttu-id="0b119-176">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span><span class="sxs-lookup"><span data-stu-id="0b119-176">The pipeline in this sample copies data from one location to another location in an Azure blob storage.</span></span> <span data-ttu-id="0b119-177">Go through the [tutorials](tutorial-copy-data-dot-net.md) to learn about using Data Factory in more scenarios.</span><span class="sxs-lookup"><span data-stu-id="0b119-177">Go through the [tutorials](tutorial-copy-data-dot-net.md) to learn about using Data Factory in more scenarios.</span></span>
