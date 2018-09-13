---
title: Tutorial - Use the Azure Batch client library for Node.js | Microsoft Docs
description: Learn the basic concepts of Azure Batch and build a simple solution using Node.js.
services: batch
author: shwetams
manager: jeconnoc
ms.assetid: ''
ms.service: batch
ms.devlang: nodejs
ms.topic: hero-article
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: shwetams
ms.openlocfilehash: 807fd49a54c82b0930134beb8413e14c1c28b278
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867726"
---
# <a name="get-started-with-batch-sdk-for-nodejs"></a><span data-ttu-id="50ea0-103">Get started with Batch SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="50ea0-103">Get started with Batch SDK for Node.js</span></span>

<span data-ttu-id="50ea0-104">Learn the basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](/javascript/api/overview/azure/batch).</span><span class="sxs-lookup"><span data-stu-id="50ea0-104">Learn the basics of building a Batch client in Node.js using [Azure Batch Node.js SDK](/javascript/api/overview/azure/batch).</span></span> <span data-ttu-id="50ea0-105">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span><span class="sxs-lookup"><span data-stu-id="50ea0-105">We take a step by step approach of understanding a scenario for a batch application and then setting it up using a Node.js client.</span></span>  

## <a name="prerequisites"></a><span data-ttu-id="50ea0-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="50ea0-106">Prerequisites</span></span>
<span data-ttu-id="50ea0-107">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span><span class="sxs-lookup"><span data-stu-id="50ea0-107">This article assumes that you have a working knowledge of Node.js and familiarity with Linux.</span></span> <span data-ttu-id="50ea0-108">It also assumes that you have an Azure account setup with access rights to create Batch and Storage services.</span><span class="sxs-lookup"><span data-stu-id="50ea0-108">It also assumes that you have an Azure account setup with access rights to create Batch and Storage services.</span></span>

<span data-ttu-id="50ea0-109">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through the steps outlined this article.</span><span class="sxs-lookup"><span data-stu-id="50ea0-109">We recommend reading [Azure Batch Technical Overview](batch-technical-overview.md) before you go through the steps outlined this article.</span></span>

## <a name="the-tutorial-scenario"></a><span data-ttu-id="50ea0-110">The tutorial scenario</span><span class="sxs-lookup"><span data-stu-id="50ea0-110">The tutorial scenario</span></span>
<span data-ttu-id="50ea0-111">Let us understand the batch workflow scenario.</span><span class="sxs-lookup"><span data-stu-id="50ea0-111">Let us understand the batch workflow scenario.</span></span> <span data-ttu-id="50ea0-112">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them to JSON.</span><span class="sxs-lookup"><span data-stu-id="50ea0-112">We have a simple script written in Python that downloads all csv files from an Azure Blob storage container and converts them to JSON.</span></span> <span data-ttu-id="50ea0-113">To process multiple storage account containers in parallel, we can deploy the script as an Azure Batch job.</span><span class="sxs-lookup"><span data-stu-id="50ea0-113">To process multiple storage account containers in parallel, we can deploy the script as an Azure Batch job.</span></span>

## <a name="azure-batch-architecture"></a><span data-ttu-id="50ea0-114">Azure Batch Architecture</span><span class="sxs-lookup"><span data-stu-id="50ea0-114">Azure Batch Architecture</span></span>
<span data-ttu-id="50ea0-115">The following diagram depicts how we can scale the Python script using Azure Batch and a Node.js client.</span><span class="sxs-lookup"><span data-stu-id="50ea0-115">The following diagram depicts how we can scale the Python script using Azure Batch and a Node.js client.</span></span>

![Azure Batch Scenario](./media/batch-nodejs-get-started/BatchScenario.png)

<span data-ttu-id="50ea0-117">The node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on the number of containers in the storage account.</span><span class="sxs-lookup"><span data-stu-id="50ea0-117">The node.js client deploys a batch job with a preparation task (explained in detail later) and a set of tasks depending on the number of containers in the storage account.</span></span> <span data-ttu-id="50ea0-118">You can download the scripts from the github repository.</span><span class="sxs-lookup"><span data-stu-id="50ea0-118">You can download the scripts from the github repository.</span></span>

* [<span data-ttu-id="50ea0-119">Node.js client</span><span class="sxs-lookup"><span data-stu-id="50ea0-119">Node.js client</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/nodejs_batch_client_sample.js)
* [<span data-ttu-id="50ea0-120">Preparation task shell scripts</span><span class="sxs-lookup"><span data-stu-id="50ea0-120">Preparation task shell scripts</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/startup_prereq.sh)
* [<span data-ttu-id="50ea0-121">Python csv to JSON processor</span><span class="sxs-lookup"><span data-stu-id="50ea0-121">Python csv to JSON processor</span></span>](https://github.com/Azure/azure-batch-samples/blob/master/Node.js/GettingStarted/processcsv.py)

> [!TIP]
> <span data-ttu-id="50ea0-122">The Node.js client in the link specified does not contain specific code to be deployed as an Azure function app.</span><span class="sxs-lookup"><span data-stu-id="50ea0-122">The Node.js client in the link specified does not contain specific code to be deployed as an Azure function app.</span></span> <span data-ttu-id="50ea0-123">You can refer to the following links for instructions to create one.</span><span class="sxs-lookup"><span data-stu-id="50ea0-123">You can refer to the following links for instructions to create one.</span></span>
> - [<span data-ttu-id="50ea0-124">Create function app</span><span class="sxs-lookup"><span data-stu-id="50ea0-124">Create function app</span></span>](../azure-functions/functions-create-first-azure-function.md)
> - [<span data-ttu-id="50ea0-125">Create timer trigger function</span><span class="sxs-lookup"><span data-stu-id="50ea0-125">Create timer trigger function</span></span>](../azure-functions/functions-bindings-timer.md)
>
>

## <a name="build-the-application"></a><span data-ttu-id="50ea0-126">Build the application</span><span class="sxs-lookup"><span data-stu-id="50ea0-126">Build the application</span></span>

<span data-ttu-id="50ea0-127">Now, let us follow the process step by step into building the Node.js client:</span><span class="sxs-lookup"><span data-stu-id="50ea0-127">Now, let us follow the process step by step into building the Node.js client:</span></span>

### <a name="step-1-install-azure-batch-sdk"></a><span data-ttu-id="50ea0-128">Step 1: Install Azure Batch SDK</span><span class="sxs-lookup"><span data-stu-id="50ea0-128">Step 1: Install Azure Batch SDK</span></span>

<span data-ttu-id="50ea0-129">You can install Azure Batch SDK for Node.js using the npm install command.</span><span class="sxs-lookup"><span data-stu-id="50ea0-129">You can install Azure Batch SDK for Node.js using the npm install command.</span></span>

`npm install azure-batch`

<span data-ttu-id="50ea0-130">This command installs the latest version of azure-batch node SDK.</span><span class="sxs-lookup"><span data-stu-id="50ea0-130">This command installs the latest version of azure-batch node SDK.</span></span>

>[!Tip]
> <span data-ttu-id="50ea0-131">In an Azure Function app, you can go to "Kudu Console" in the Azure function's Settings tab to run the npm install commands.</span><span class="sxs-lookup"><span data-stu-id="50ea0-131">In an Azure Function app, you can go to "Kudu Console" in the Azure function's Settings tab to run the npm install commands.</span></span> <span data-ttu-id="50ea0-132">In this case to install Azure Batch SDK for Node.js.</span><span class="sxs-lookup"><span data-stu-id="50ea0-132">In this case to install Azure Batch SDK for Node.js.</span></span>
>
>

### <a name="step-2-create-an-azure-batch-account"></a><span data-ttu-id="50ea0-133">Step 2: Create an Azure Batch account</span><span class="sxs-lookup"><span data-stu-id="50ea0-133">Step 2: Create an Azure Batch account</span></span>

<span data-ttu-id="50ea0-134">You can create it from the [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](/cli/azure)).</span><span class="sxs-lookup"><span data-stu-id="50ea0-134">You can create it from the [Azure portal](batch-account-create-portal.md) or from command line ([Powershell](batch-powershell-cmdlets-get-started.md) /[Azure cli](/cli/azure)).</span></span>

<span data-ttu-id="50ea0-135">Following are the commands to create one through Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="50ea0-135">Following are the commands to create one through Azure CLI.</span></span>

<span data-ttu-id="50ea0-136">Create a Resource Group, skip this step if you already have one where you want to create the Batch Account:</span><span class="sxs-lookup"><span data-stu-id="50ea0-136">Create a Resource Group, skip this step if you already have one where you want to create the Batch Account:</span></span>

`az group create -n "<resource-group-name>" -l "<location>"`

<span data-ttu-id="50ea0-137">Next, create an Azure Batch account.</span><span class="sxs-lookup"><span data-stu-id="50ea0-137">Next, create an Azure Batch account.</span></span>

`az batch account create -l "<location>"  -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="50ea0-138">Each Batch account has its corresponding access keys.</span><span class="sxs-lookup"><span data-stu-id="50ea0-138">Each Batch account has its corresponding access keys.</span></span> <span data-ttu-id="50ea0-139">These keys are needed to create further resources in Azure batch account.</span><span class="sxs-lookup"><span data-stu-id="50ea0-139">These keys are needed to create further resources in Azure batch account.</span></span> <span data-ttu-id="50ea0-140">A good practice for production environment is to use Azure Key Vault to store these keys.</span><span class="sxs-lookup"><span data-stu-id="50ea0-140">A good practice for production environment is to use Azure Key Vault to store these keys.</span></span> <span data-ttu-id="50ea0-141">You can then create a Service principal for the application.</span><span class="sxs-lookup"><span data-stu-id="50ea0-141">You can then create a Service principal for the application.</span></span> <span data-ttu-id="50ea0-142">Using this service principal the application can create an OAuth token to access keys from the key vault.</span><span class="sxs-lookup"><span data-stu-id="50ea0-142">Using this service principal the application can create an OAuth token to access keys from the key vault.</span></span>

`az batch account keys list -g "<resource-group-name>" -n "<batch-account-name>"`

<span data-ttu-id="50ea0-143">Copy and store the key to be used in the subsequent steps.</span><span class="sxs-lookup"><span data-stu-id="50ea0-143">Copy and store the key to be used in the subsequent steps.</span></span>

### <a name="step-3-create-an-azure-batch-service-client"></a><span data-ttu-id="50ea0-144">Step 3: Create an Azure Batch service client</span><span class="sxs-lookup"><span data-stu-id="50ea0-144">Step 3: Create an Azure Batch service client</span></span>
<span data-ttu-id="50ea0-145">Following code snippet first imports the azure-batch Node.js module and then creates a Batch Service client.</span><span class="sxs-lookup"><span data-stu-id="50ea0-145">Following code snippet first imports the azure-batch Node.js module and then creates a Batch Service client.</span></span> <span data-ttu-id="50ea0-146">You need to first create a SharedKeyCredentials object with the Batch account key copied from the previous step.</span><span class="sxs-lookup"><span data-stu-id="50ea0-146">You need to first create a SharedKeyCredentials object with the Batch account key copied from the previous step.</span></span>

```nodejs
// Initializing Azure Batch variables

var batch = require('azure-batch');

var accountName = '<azure-batch-account-name>';

var accountKey = '<account-key-downloaded>';

var accountUrl = '<account-url>'

// Create Batch credentials object using account name and account key

var credentials = new batch.SharedKeyCredentials(accountName,accountKey);

// Create Batch service client

var batch_client = new batch.ServiceClient(credentials,accountUrl);

```

<span data-ttu-id="50ea0-147">The Azure Batch URI can be found in the Overview tab of the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="50ea0-147">The Azure Batch URI can be found in the Overview tab of the Azure portal.</span></span> <span data-ttu-id="50ea0-148">It is of the format:</span><span class="sxs-lookup"><span data-stu-id="50ea0-148">It is of the format:</span></span>

`https://accountname.location.batch.azure.com`

<span data-ttu-id="50ea0-149">Refer to the screenshot:</span><span class="sxs-lookup"><span data-stu-id="50ea0-149">Refer to the screenshot:</span></span>

![Azure batch uri](./media/batch-nodejs-get-started/azurebatchuri.png)



### <a name="step-4-create-an-azure-batch-pool"></a><span data-ttu-id="50ea0-151">Step 4: Create an Azure Batch pool</span><span class="sxs-lookup"><span data-stu-id="50ea0-151">Step 4: Create an Azure Batch pool</span></span>
<span data-ttu-id="50ea0-152">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span><span class="sxs-lookup"><span data-stu-id="50ea0-152">An Azure Batch pool consists of multiple VMs (also known as Batch Nodes).</span></span> <span data-ttu-id="50ea0-153">Azure Batch service deploys the tasks on these nodes and manages them.</span><span class="sxs-lookup"><span data-stu-id="50ea0-153">Azure Batch service deploys the tasks on these nodes and manages them.</span></span> <span data-ttu-id="50ea0-154">You can define the following configuration parameters for your pool.</span><span class="sxs-lookup"><span data-stu-id="50ea0-154">You can define the following configuration parameters for your pool.</span></span>

* <span data-ttu-id="50ea0-155">Type of Virtual Machine image</span><span class="sxs-lookup"><span data-stu-id="50ea0-155">Type of Virtual Machine image</span></span>
* <span data-ttu-id="50ea0-156">Size of Virtual Machine nodes</span><span class="sxs-lookup"><span data-stu-id="50ea0-156">Size of Virtual Machine nodes</span></span>
* <span data-ttu-id="50ea0-157">Number of Virtual Machine nodes</span><span class="sxs-lookup"><span data-stu-id="50ea0-157">Number of Virtual Machine nodes</span></span>

> [!Tip]
> <span data-ttu-id="50ea0-158">The size and number of Virtual Machine nodes largely depend on the number of tasks you want to run in parallel and also the task itself.</span><span class="sxs-lookup"><span data-stu-id="50ea0-158">The size and number of Virtual Machine nodes largely depend on the number of tasks you want to run in parallel and also the task itself.</span></span> <span data-ttu-id="50ea0-159">We recommend testing to determine the ideal number and size.</span><span class="sxs-lookup"><span data-stu-id="50ea0-159">We recommend testing to determine the ideal number and size.</span></span>
>
>

<span data-ttu-id="50ea0-160">The following code snippet creates the configuration parameter objects.</span><span class="sxs-lookup"><span data-stu-id="50ea0-160">The following code snippet creates the configuration parameter objects.</span></span>

```nodejs
// Creating Image reference configuration for Ubuntu Linux VM
var imgRef = {publisher:"Canonical",offer:"UbuntuServer",sku:"14.04.2-LTS",version:"latest"}

// Creating the VM configuration object with the SKUID
var vmconfig = {imageReference:imgRef,nodeAgentSKUId:"batch.node.ubuntu 14.04"}

// Setting the VM size to Standard F4
var vmSize = "STANDARD_F4"

//Setting number of VMs in the pool to 4
var numVMs = 4
```

> [!Tip]
> <span data-ttu-id="50ea0-161">For the list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span><span class="sxs-lookup"><span data-stu-id="50ea0-161">For the list of Linux VM images available for Azure Batch and their SKU IDs, see [List of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images).</span></span>
>
>

<span data-ttu-id="50ea0-162">Once the pool configuration is defined, you can create the Azure Batch pool.</span><span class="sxs-lookup"><span data-stu-id="50ea0-162">Once the pool configuration is defined, you can create the Azure Batch pool.</span></span> <span data-ttu-id="50ea0-163">The Batch pool command creates Azure Virtual Machine nodes and prepares them to be ready to receive tasks to execute.</span><span class="sxs-lookup"><span data-stu-id="50ea0-163">The Batch pool command creates Azure Virtual Machine nodes and prepares them to be ready to receive tasks to execute.</span></span> <span data-ttu-id="50ea0-164">Each pool should have a unique ID for reference in subsequent steps.</span><span class="sxs-lookup"><span data-stu-id="50ea0-164">Each pool should have a unique ID for reference in subsequent steps.</span></span>

<span data-ttu-id="50ea0-165">The following code snippet creates an Azure Batch pool.</span><span class="sxs-lookup"><span data-stu-id="50ea0-165">The following code snippet creates an Azure Batch pool.</span></span>

```nodejs
// Create a unique Azure Batch pool ID
var poolid = "pool" + customerDetails.customerid;
var poolConfig = {id:poolid, displayName:poolid,vmSize:vmSize,virtualMachineConfiguration:vmconfig,targetDedicatedComputeNodes:numVms,enableAutoScale:false };
// Creating the Pool for the specific customer
var pool = batch_client.pool.add(poolConfig,function(error,result){
    if(error!=null){console.log(error.response)};
});
```

<span data-ttu-id="50ea0-166">You can check the status of the pool created and ensure that the state is in "active" before going ahead with submission of a Job to that pool.</span><span class="sxs-lookup"><span data-stu-id="50ea0-166">You can check the status of the pool created and ensure that the state is in "active" before going ahead with submission of a Job to that pool.</span></span>

```nodejs
var cloudPool = batch_client.pool.get(poolid,function(error,result,request,response){
        if(error == null)
        {

            if(result.state == "active")
            {
                console.log("Pool is active");
            }
        }
        else
        {
            if(error.statusCode==404)
            {
                console.log("Pool not found yet returned 404...");    

            }
            else
            {
                console.log("Error occurred while retrieving pool data");
            }
        }
        });
```

<span data-ttu-id="50ea0-167">Following is a sample result object returned by the pool.get function.</span><span class="sxs-lookup"><span data-stu-id="50ea0-167">Following is a sample result object returned by the pool.get function.</span></span>

```
{ id: 'processcsv_201721152',
  displayName: 'processcsv_201721152',
  url: 'https://<batch-account-name>.centralus.batch.azure.com/pools/processcsv_201721152',
  eTag: '<eTag>',
  lastModified: 2017-03-27T10:28:02.398Z,
  creationTime: 2017-03-27T10:28:02.398Z,
  state: 'active',
  stateTransitionTime: 2017-03-27T10:28:02.398Z,
  allocationState: 'resizing',
  allocationStateTransitionTime: 2017-03-27T10:28:02.398Z,
  vmSize: 'standard_a1',
  virtualMachineConfiguration:
   { imageReference:
      { publisher: 'Canonical',
        offer: 'UbuntuServer',
        sku: '14.04.2-LTS',
        version: 'latest' },
     nodeAgentSKUId: 'batch.node.ubuntu 14.04' },
  resizeTimeout:
   { [Number: 900000]
     _milliseconds: 900000,
     _days: 0,
     _months: 0,
     _data:
      { milliseconds: 0,
        seconds: 0,
        minutes: 15,
        hours: 0,
        days: 0,
        months: 0,
        years: 0 },
     _locale:
      Locale {
        _calendar: [Object],
        _longDateFormat: [Object],
        _invalidDate: 'Invalid date',
        ordinal: [Function: ordinal],
        _ordinalParse: /\d{1,2}(th|st|nd|rd)/,
        _relativeTime: [Object],
        _months: [Object],
        _monthsShort: [Object],
        _week: [Object],
        _weekdays: [Object],
        _weekdaysMin: [Object],
        _weekdaysShort: [Object],
        _meridiemParse: /[ap]\.?m?\.?/i,
        _abbr: 'en',
        _config: [Object],
        _ordinalParseLenient: /\d{1,2}(th|st|nd|rd)|\d{1,2}/ } },
  currentDedicated: 0,
  targetDedicated: 4,
  enableAutoScale: false,
  enableInterNodeCommunication: false,
  maxTasksPerNode: 1,
  taskSchedulingPolicy: { nodeFillType: 'Spread' } }
```


### <a name="step-4-submit-an-azure-batch-job"></a><span data-ttu-id="50ea0-168">Step 4: Submit an Azure Batch job</span><span class="sxs-lookup"><span data-stu-id="50ea0-168">Step 4: Submit an Azure Batch job</span></span>
<span data-ttu-id="50ea0-169">An Azure Batch job is a logical group of similar tasks.</span><span class="sxs-lookup"><span data-stu-id="50ea0-169">An Azure Batch job is a logical group of similar tasks.</span></span> <span data-ttu-id="50ea0-170">In our scenario, it is "Process csv to JSON."</span><span class="sxs-lookup"><span data-stu-id="50ea0-170">In our scenario, it is "Process csv to JSON."</span></span> <span data-ttu-id="50ea0-171">Each task here could be processing csv files present in each Azure Storage container.</span><span class="sxs-lookup"><span data-stu-id="50ea0-171">Each task here could be processing csv files present in each Azure Storage container.</span></span>

<span data-ttu-id="50ea0-172">These tasks would run in parallel and deployed across multiple nodes, orchestrated by the Azure Batch service.</span><span class="sxs-lookup"><span data-stu-id="50ea0-172">These tasks would run in parallel and deployed across multiple nodes, orchestrated by the Azure Batch service.</span></span>

> [!Tip]
> <span data-ttu-id="50ea0-173">You can use the [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property to specify maximum number of tasks that can run concurrently on a single node.</span><span class="sxs-lookup"><span data-stu-id="50ea0-173">You can use the [maxTasksPerNode](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property to specify maximum number of tasks that can run concurrently on a single node.</span></span>
>
>

#### <a name="preparation-task"></a><span data-ttu-id="50ea0-174">Preparation task</span><span class="sxs-lookup"><span data-stu-id="50ea0-174">Preparation task</span></span>

<span data-ttu-id="50ea0-175">The VM nodes created are blank Ubuntu nodes.</span><span class="sxs-lookup"><span data-stu-id="50ea0-175">The VM nodes created are blank Ubuntu nodes.</span></span> <span data-ttu-id="50ea0-176">Often, you need to install a set of programs as prerequisites.</span><span class="sxs-lookup"><span data-stu-id="50ea0-176">Often, you need to install a set of programs as prerequisites.</span></span>
<span data-ttu-id="50ea0-177">Typically, for Linux nodes you can have a shell script that installs the prerequisites before the actual tasks run.</span><span class="sxs-lookup"><span data-stu-id="50ea0-177">Typically, for Linux nodes you can have a shell script that installs the prerequisites before the actual tasks run.</span></span> <span data-ttu-id="50ea0-178">However it could be any programmable executable.</span><span class="sxs-lookup"><span data-stu-id="50ea0-178">However it could be any programmable executable.</span></span>
<span data-ttu-id="50ea0-179">The [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and the Azure Storage SDK for Python.</span><span class="sxs-lookup"><span data-stu-id="50ea0-179">The [shell script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/startup_prereq.sh) in this example installs Python-pip and the Azure Storage SDK for Python.</span></span>

<span data-ttu-id="50ea0-180">You can upload the script on an Azure Storage Account and generate a SAS URI to access the script.</span><span class="sxs-lookup"><span data-stu-id="50ea0-180">You can upload the script on an Azure Storage Account and generate a SAS URI to access the script.</span></span> <span data-ttu-id="50ea0-181">This process can also be automated using the Azure Storage Node.js SDK.</span><span class="sxs-lookup"><span data-stu-id="50ea0-181">This process can also be automated using the Azure Storage Node.js SDK.</span></span>

> [!Tip]
> <span data-ttu-id="50ea0-182">A preparation task for a job runs only on the VM nodes where the specific task needs to run.</span><span class="sxs-lookup"><span data-stu-id="50ea0-182">A preparation task for a job runs only on the VM nodes where the specific task needs to run.</span></span> <span data-ttu-id="50ea0-183">If you want prerequisites to be installed on all nodes irrespective of the tasks that run on it, you can use the [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span><span class="sxs-lookup"><span data-stu-id="50ea0-183">If you want prerequisites to be installed on all nodes irrespective of the tasks that run on it, you can use the [startTask](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Pool.html#add) property while adding a pool.</span></span> <span data-ttu-id="50ea0-184">You can use the following preparation task definition for reference.</span><span class="sxs-lookup"><span data-stu-id="50ea0-184">You can use the following preparation task definition for reference.</span></span>
>
>

<span data-ttu-id="50ea0-185">A preparation task is specified during the submission of Azure Batch job.</span><span class="sxs-lookup"><span data-stu-id="50ea0-185">A preparation task is specified during the submission of Azure Batch job.</span></span> <span data-ttu-id="50ea0-186">Following are the preparation task configuration parameters:</span><span class="sxs-lookup"><span data-stu-id="50ea0-186">Following are the preparation task configuration parameters:</span></span>

* <span data-ttu-id="50ea0-187">**ID**: A unique identifier for the preparation task</span><span class="sxs-lookup"><span data-stu-id="50ea0-187">**ID**: A unique identifier for the preparation task</span></span>
* <span data-ttu-id="50ea0-188">**commandLine**: Command line to execute the task executable</span><span class="sxs-lookup"><span data-stu-id="50ea0-188">**commandLine**: Command line to execute the task executable</span></span>
* <span data-ttu-id="50ea0-189">**resourceFiles**: Array of objects that provide details of files needed to be downloaded for this task to run.</span><span class="sxs-lookup"><span data-stu-id="50ea0-189">**resourceFiles**: Array of objects that provide details of files needed to be downloaded for this task to run.</span></span>  <span data-ttu-id="50ea0-190">Following are its options</span><span class="sxs-lookup"><span data-stu-id="50ea0-190">Following are its options</span></span>
    - <span data-ttu-id="50ea0-191">blobSource: The SAS URI of the file</span><span class="sxs-lookup"><span data-stu-id="50ea0-191">blobSource: The SAS URI of the file</span></span>
    - <span data-ttu-id="50ea0-192">filePath: Local path to download and save the file</span><span class="sxs-lookup"><span data-stu-id="50ea0-192">filePath: Local path to download and save the file</span></span>
    - <span data-ttu-id="50ea0-193">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span><span class="sxs-lookup"><span data-stu-id="50ea0-193">fileMode: Only applicable for Linux nodes, fileMode is in octal format with a default value of 0770</span></span>
* <span data-ttu-id="50ea0-194">**waitForSuccess**: If set to true, the task does not run on preparation task failures</span><span class="sxs-lookup"><span data-stu-id="50ea0-194">**waitForSuccess**: If set to true, the task does not run on preparation task failures</span></span>
* <span data-ttu-id="50ea0-195">**runElevated**: Set it to true if elevated privileges are needed to run the task.</span><span class="sxs-lookup"><span data-stu-id="50ea0-195">**runElevated**: Set it to true if elevated privileges are needed to run the task.</span></span>

<span data-ttu-id="50ea0-196">Following code snippet shows the preparation task script configuration sample:</span><span class="sxs-lookup"><span data-stu-id="50ea0-196">Following code snippet shows the preparation task script configuration sample:</span></span>

```nodejs
var job_prep_task_config = {id:"installprereq",commandLine:"sudo sh startup_prereq.sh > startup.log",resourceFiles:[{'blobSource':'Blob SAS URI','filePath':'startup_prereq.sh'}],waitForSuccess:true,runElevated:true}
```

<span data-ttu-id="50ea0-197">If there are no prerequisites to be installed for your tasks to run, you can skip the preparation tasks.</span><span class="sxs-lookup"><span data-stu-id="50ea0-197">If there are no prerequisites to be installed for your tasks to run, you can skip the preparation tasks.</span></span> <span data-ttu-id="50ea0-198">Following code creates a job with display name "process csv files."</span><span class="sxs-lookup"><span data-stu-id="50ea0-198">Following code creates a job with display name "process csv files."</span></span>

 ```nodejs
 // Setting up Batch pool configuration
 var pool_config = {poolId:poolid}
 // Setting up Job configuration along with preparation task
 var jobId = "processcsvjob"
 var job_config = {id:jobId,displayName:"process csv files",jobPreparationTask:job_prep_task_config,poolInfo:pool_config}
 // Adding Azure batch job to the pool
 var job = batch_client.job.add(job_config,function(error,result){
     if(error != null)
     {
         console.log("Error submitting job : " + error.response);
     }});
```


### <a name="step-5-submit-azure-batch-tasks-for-a-job"></a><span data-ttu-id="50ea0-199">Step 5: Submit Azure Batch tasks for a job</span><span class="sxs-lookup"><span data-stu-id="50ea0-199">Step 5: Submit Azure Batch tasks for a job</span></span>

<span data-ttu-id="50ea0-200">Now that our process csv job is created, let us create tasks for that job.</span><span class="sxs-lookup"><span data-stu-id="50ea0-200">Now that our process csv job is created, let us create tasks for that job.</span></span> <span data-ttu-id="50ea0-201">Assuming we have four containers, we have to create four tasks, one for each container.</span><span class="sxs-lookup"><span data-stu-id="50ea0-201">Assuming we have four containers, we have to create four tasks, one for each container.</span></span>

<span data-ttu-id="50ea0-202">If we look at the [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span><span class="sxs-lookup"><span data-stu-id="50ea0-202">If we look at the [Python script](https://github.com/shwetams/azure-batchclient-sample-nodejs/blob/master/processcsv.py), it accepts two parameters:</span></span>

* <span data-ttu-id="50ea0-203">container name: The Storage container to download files from</span><span class="sxs-lookup"><span data-stu-id="50ea0-203">container name: The Storage container to download files from</span></span>
* <span data-ttu-id="50ea0-204">pattern: An optional parameter of file name pattern</span><span class="sxs-lookup"><span data-stu-id="50ea0-204">pattern: An optional parameter of file name pattern</span></span>

<span data-ttu-id="50ea0-205">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks to the Azure batch job "process csv" we created earlier.</span><span class="sxs-lookup"><span data-stu-id="50ea0-205">Assuming we have four containers "con1", "con2", "con3","con4" following code shows submitting for tasks to the Azure batch job "process csv" we created earlier.</span></span>

```nodejs
// storing container names in an array
var container_list = ["con1","con2","con3","con4"]
    container_list.forEach(function(val,index){           

           var container_name = val;
           var taskID = container_name + "_process";
           var task_config = {id:taskID,displayName:'process csv in ' + container_name,commandLine:'python processcsv.py --container ' + container_name,resourceFiles:[{'blobSource':'<blob SAS URI>','filePath':'processcsv.py'}]}
           var task = batch_client.task.add(poolid,task_config,function(error,result){
                if(error != null)
                {
                    console.log(error.response);     
                }
                else
                {
                    console.log("Task for container : " + container_name + "submitted successfully");
                }



           });

    });
```

<span data-ttu-id="50ea0-206">The code adds multiple tasks to the pool.</span><span class="sxs-lookup"><span data-stu-id="50ea0-206">The code adds multiple tasks to the pool.</span></span> <span data-ttu-id="50ea0-207">And each of the tasks is executed on a node in the pool of VMs created.</span><span class="sxs-lookup"><span data-stu-id="50ea0-207">And each of the tasks is executed on a node in the pool of VMs created.</span></span> <span data-ttu-id="50ea0-208">If the number of tasks exceeds the number of VMs in a pool or the maxTasksPerNode property, the tasks wait until a node is made available.</span><span class="sxs-lookup"><span data-stu-id="50ea0-208">If the number of tasks exceeds the number of VMs in a pool or the maxTasksPerNode property, the tasks wait until a node is made available.</span></span> <span data-ttu-id="50ea0-209">This orchestration is handled by Azure Batch automatically.</span><span class="sxs-lookup"><span data-stu-id="50ea0-209">This orchestration is handled by Azure Batch automatically.</span></span>

<span data-ttu-id="50ea0-210">The portal has detailed views on the tasks and job statuses.</span><span class="sxs-lookup"><span data-stu-id="50ea0-210">The portal has detailed views on the tasks and job statuses.</span></span> <span data-ttu-id="50ea0-211">You can also use the list and get functions in the Azure Node SDK.</span><span class="sxs-lookup"><span data-stu-id="50ea0-211">You can also use the list and get functions in the Azure Node SDK.</span></span> <span data-ttu-id="50ea0-212">Details are provided in the documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span><span class="sxs-lookup"><span data-stu-id="50ea0-212">Details are provided in the documentation [link](http://azure.github.io/azure-sdk-for-node/azure-batch/latest/Job.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="50ea0-213">Next steps</span><span class="sxs-lookup"><span data-stu-id="50ea0-213">Next steps</span></span>

- <span data-ttu-id="50ea0-214">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span><span class="sxs-lookup"><span data-stu-id="50ea0-214">Review the [Overview of Azure Batch features](batch-api-basics.md) article, which we recommend if you're new to the service.</span></span>
- <span data-ttu-id="50ea0-215">See the [Batch Node.js reference](/javascript/api/overview/azure/batch) to explore the Batch API.</span><span class="sxs-lookup"><span data-stu-id="50ea0-215">See the [Batch Node.js reference](/javascript/api/overview/azure/batch) to explore the Batch API.</span></span>

