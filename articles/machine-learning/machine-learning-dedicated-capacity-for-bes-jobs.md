---
title: Dedicated Capacity for Machine Learning Batch Execution Service Jobs | Microsoft Docs
description: Overview of Azure Batch services for Machine Learning jobs.
services: machine-learning
documentationcenter: ''
author: vDonGlover
manager: raymondl
editor: ''
ms.service: machine-learning
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/19/2017
ms.author: v-donglo
ms.openlocfilehash: 1cacc792070e8dcd191e1f6cd86e803f9b57f553
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660702"
---
# <a name="azure-batch-service-for-machine-learning-jobs"></a><span data-ttu-id="3d60d-103">Azure Batch service for Machine Learning jobs</span><span class="sxs-lookup"><span data-stu-id="3d60d-103">Azure Batch service for Machine Learning jobs</span></span>

<span data-ttu-id="3d60d-104">Machine Learning Batch Pool processing provides customer-managed scale for the Azure Machine Learning Batch Execution Service.</span><span class="sxs-lookup"><span data-stu-id="3d60d-104">Machine Learning Batch Pool processing provides customer-managed scale for the Azure Machine Learning Batch Execution Service.</span></span> <span data-ttu-id="3d60d-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits the number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span><span class="sxs-lookup"><span data-stu-id="3d60d-105">Classic batch processing for machine learning takes place in a multi-tenant environment, which limits the number of concurrent jobs you can submit, and jobs are queued on a first-in-first-out basis.</span></span> <span data-ttu-id="3d60d-106">This uncertainty means that you can't accurately predict when your job will run.</span><span class="sxs-lookup"><span data-stu-id="3d60d-106">This uncertainty means that you can't accurately predict when your job will run.</span></span>

<span data-ttu-id="3d60d-107">Batch Pool processing allows you to create pools on which you can submit batch jobs.</span><span class="sxs-lookup"><span data-stu-id="3d60d-107">Batch Pool processing allows you to create pools on which you can submit batch jobs.</span></span> <span data-ttu-id="3d60d-108">You control the size of the pool, and to which pool the job is submitted.</span><span class="sxs-lookup"><span data-stu-id="3d60d-108">You control the size of the pool, and to which pool the job is submitted.</span></span> <span data-ttu-id="3d60d-109">Your BES job runs in its own processing space providing predictable processing performance and the ability to create resource pools that correspond to the processing load that you submit.</span><span class="sxs-lookup"><span data-stu-id="3d60d-109">Your BES job runs in its own processing space providing predictable processing performance and the ability to create resource pools that correspond to the processing load that you submit.</span></span>

## <a name="how-to-use-batch-pool-processing"></a><span data-ttu-id="3d60d-110">How to use Batch Pool processing</span><span class="sxs-lookup"><span data-stu-id="3d60d-110">How to use Batch Pool processing</span></span>

<span data-ttu-id="3d60d-111">Configuration of Batch Pool Processing is not currently available through the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="3d60d-111">Configuration of Batch Pool Processing is not currently available through the Azure portal.</span></span> <span data-ttu-id="3d60d-112">To use Batch Pool processing, you must:</span><span class="sxs-lookup"><span data-stu-id="3d60d-112">To use Batch Pool processing, you must:</span></span>

-   <span data-ttu-id="3d60d-113">Call CSS to create a Batch Pool Account and obtain a Pool Service URL and an authorization key</span><span class="sxs-lookup"><span data-stu-id="3d60d-113">Call CSS to create a Batch Pool Account and obtain a Pool Service URL and an authorization key</span></span>
-   <span data-ttu-id="3d60d-114">Create a New Resource Manager based web service and billing plan</span><span class="sxs-lookup"><span data-stu-id="3d60d-114">Create a New Resource Manager based web service and billing plan</span></span>

<span data-ttu-id="3d60d-115">To create your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span><span class="sxs-lookup"><span data-stu-id="3d60d-115">To create your account, call Microsoft Customer Service and Support (CSS) and provide your Subscription ID.</span></span> <span data-ttu-id="3d60d-116">CSS will work with you to determine the appropriate capacity for your scenario.</span><span class="sxs-lookup"><span data-stu-id="3d60d-116">CSS will work with you to determine the appropriate capacity for your scenario.</span></span> <span data-ttu-id="3d60d-117">CSS then configures your account with the maximum number of pools you can create and the maximum number of virtual machines (VMs) that you can place in each pool.</span><span class="sxs-lookup"><span data-stu-id="3d60d-117">CSS then configures your account with the maximum number of pools you can create and the maximum number of virtual machines (VMs) that you can place in each pool.</span></span> <span data-ttu-id="3d60d-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span><span class="sxs-lookup"><span data-stu-id="3d60d-118">Once your account is configured, you are provided your Pool Service URL and an authorization key.</span></span>

<span data-ttu-id="3d60d-119">After your account is created, you use the Pool Service URL and authorization key to perform pool management operations on your Batch Pool.</span><span class="sxs-lookup"><span data-stu-id="3d60d-119">After your account is created, you use the Pool Service URL and authorization key to perform pool management operations on your Batch Pool.</span></span>

![Batch pool service architecture.](https://docstestmedia1.blob.core.windows.net/azure-media/articles/machine-learning/media/machine-learning-dedicated-capacity-for-bes-jobs/pool-architecture.png)

<span data-ttu-id="3d60d-121">You create pools by calling the Create Pool operation on the pool service URL that CSS provided to you.</span><span class="sxs-lookup"><span data-stu-id="3d60d-121">You create pools by calling the Create Pool operation on the pool service URL that CSS provided to you.</span></span> <span data-ttu-id="3d60d-122">When you create a pool, specify the number of VMs and the URL of the swagger.json of a New Resource Manager based Machine Learning web service.</span><span class="sxs-lookup"><span data-stu-id="3d60d-122">When you create a pool, specify the number of VMs and the URL of the swagger.json of a New Resource Manager based Machine Learning web service.</span></span> <span data-ttu-id="3d60d-123">This web service is provided to establish the billing association.</span><span class="sxs-lookup"><span data-stu-id="3d60d-123">This web service is provided to establish the billing association.</span></span> <span data-ttu-id="3d60d-124">The Batch Pool service uses the swagger.json to associate the pool with a billing plan.</span><span class="sxs-lookup"><span data-stu-id="3d60d-124">The Batch Pool service uses the swagger.json to associate the pool with a billing plan.</span></span> <span data-ttu-id="3d60d-125">You can run any BES web service, both New Resource Manager based and classic, you choose on the pool.</span><span class="sxs-lookup"><span data-stu-id="3d60d-125">You can run any BES web service, both New Resource Manager based and classic, you choose on the pool.</span></span>

<span data-ttu-id="3d60d-126">You can use any New Resource Manager based web service, but be aware that the billing for the jobs are charged against the billing plan associated with that service.</span><span class="sxs-lookup"><span data-stu-id="3d60d-126">You can use any New Resource Manager based web service, but be aware that the billing for the jobs are charged against the billing plan associated with that service.</span></span> <span data-ttu-id="3d60d-127">You may want to create a web service and new billing plan specifically for running Batch Pool jobs.</span><span class="sxs-lookup"><span data-stu-id="3d60d-127">You may want to create a web service and new billing plan specifically for running Batch Pool jobs.</span></span>

<span data-ttu-id="3d60d-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span><span class="sxs-lookup"><span data-stu-id="3d60d-128">For more information on creating web services, see [Deploy an Azure Machine Learning web service](machine-learning-publish-a-machine-learning-web-service.md).</span></span>

<span data-ttu-id="3d60d-129">Once you have created a pool, you submit the BES job using the Batch Requests URL for the web service.</span><span class="sxs-lookup"><span data-stu-id="3d60d-129">Once you have created a pool, you submit the BES job using the Batch Requests URL for the web service.</span></span> <span data-ttu-id="3d60d-130">You can choose to submit it to a pool or to classic batch processing.</span><span class="sxs-lookup"><span data-stu-id="3d60d-130">You can choose to submit it to a pool or to classic batch processing.</span></span> <span data-ttu-id="3d60d-131">To submit a job to Batch Pool processing, you add the following parameter to the job submission request body:</span><span class="sxs-lookup"><span data-stu-id="3d60d-131">To submit a job to Batch Pool processing, you add the following parameter to the job submission request body:</span></span>

<span data-ttu-id="3d60d-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span><span class="sxs-lookup"><span data-stu-id="3d60d-132">"AzureBatchPoolId":"&lt;pool ID&gt;"</span></span>

<span data-ttu-id="3d60d-133">If you do not add the parameter, the job is run in the classic batch process environment.</span><span class="sxs-lookup"><span data-stu-id="3d60d-133">If you do not add the parameter, the job is run in the classic batch process environment.</span></span> <span data-ttu-id="3d60d-134">If the pool has available resources, the job starts running immediately.</span><span class="sxs-lookup"><span data-stu-id="3d60d-134">If the pool has available resources, the job starts running immediately.</span></span> <span data-ttu-id="3d60d-135">If the pool does not have free resources, your job is queued until a resource is available.</span><span class="sxs-lookup"><span data-stu-id="3d60d-135">If the pool does not have free resources, your job is queued until a resource is available.</span></span>

<span data-ttu-id="3d60d-136">If you find that you regularly reach the capacity of your pools, and you need increased capacity, you can call CSS and work with a representative to increase your quotas.</span><span class="sxs-lookup"><span data-stu-id="3d60d-136">If you find that you regularly reach the capacity of your pools, and you need increased capacity, you can call CSS and work with a representative to increase your quotas.</span></span>

<span data-ttu-id="3d60d-137">Example Request:</span><span class="sxs-lookup"><span data-stu-id="3d60d-137">Example Request:</span></span>

https://ussouthcentral.services.azureml.net/subscriptions/80c77c7674ba4c8c82294c3b2957990c/services/9fe659022c9747e3b9b7b923c3830623/jobs?api-version=2.0

```json
{

    "Input":{
    
        "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpoint
        =https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://zhguim
        l.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;;",
        
        "BaseLocation":null,
        
        "RelativeLocation":"testint/AdultCensusIncomeBinaryClassificationDataset.csv",
        
        "SasBlobToken":null
    
    },
    
    "GlobalParameters":{ },
    
    "Outputs":{
    
        "output1":{
        
            "ConnectionString":"DefaultEndpointsProtocol=https;BlobEndpoint=https://sampleaccount.blob.core.windows.net/;TableEndpo
            int=https://sampleaccount.table.core.windows.net/;QueueEndpoint=https://sampleaccount.queue.core.windows.net/;FileEndpoint=https://sampleaccount.file.core.windows.net/;AccountName=sampleaccount;AccountKey=&lt;Key&gt;",
            "BaseLocation":null,
            "RelativeLocation":"testintoutput/testint\_results.csv",
            
            "SasBlobToken":null
        
        }
    
    },
    
    "AzureBatchPoolId":"8dfc151b0d3e446497b845f3b29ef53b"

}
```

## <a name="considerations-when-using-batch-pool-processing"></a><span data-ttu-id="3d60d-138">Considerations when using Batch Pool processing</span><span class="sxs-lookup"><span data-stu-id="3d60d-138">Considerations when using Batch Pool processing</span></span>

<span data-ttu-id="3d60d-139">Batch Pool Processing is an always-on billable service and that requires you to associate it with a Resource Manager based billing plan.</span><span class="sxs-lookup"><span data-stu-id="3d60d-139">Batch Pool Processing is an always-on billable service and that requires you to associate it with a Resource Manager based billing plan.</span></span> <span data-ttu-id="3d60d-140">You are only billed for the number of compute hours the pool is running; regardless of the number of jobs run during that time pool.</span><span class="sxs-lookup"><span data-stu-id="3d60d-140">You are only billed for the number of compute hours the pool is running; regardless of the number of jobs run during that time pool.</span></span> <span data-ttu-id="3d60d-141">If you create a pool, you are billed for the compute hours of each virtual machine in the pool until the pool is deleted, even if no batch jobs are running in the pool.</span><span class="sxs-lookup"><span data-stu-id="3d60d-141">If you create a pool, you are billed for the compute hours of each virtual machine in the pool until the pool is deleted, even if no batch jobs are running in the pool.</span></span> <span data-ttu-id="3d60d-142">Billing for the virtual machines starts when they have finished provisioning and stops when they have been deleted.</span><span class="sxs-lookup"><span data-stu-id="3d60d-142">Billing for the virtual machines starts when they have finished provisioning and stops when they have been deleted.</span></span> <span data-ttu-id="3d60d-143">You can use any of the plans found on the [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span><span class="sxs-lookup"><span data-stu-id="3d60d-143">You can use any of the plans found on the [Machine Learning Pricing page](https://azure.microsoft.com/pricing/details/machine-learning/).</span></span>

<span data-ttu-id="3d60d-144">Billing example:</span><span class="sxs-lookup"><span data-stu-id="3d60d-144">Billing example:</span></span>

<span data-ttu-id="3d60d-145">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span><span class="sxs-lookup"><span data-stu-id="3d60d-145">If you create a Batch Pool with 2 virtual machines and delete it after 24 hours your billing plan is debited 48 compute hours; regardless of how many jobs were run during that period.</span></span>

<span data-ttu-id="3d60d-146">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span><span class="sxs-lookup"><span data-stu-id="3d60d-146">If you create a Batch Pool with 4 virtual machines and delete it after 12 hours, your billing plan is also debited 48 compute hours.</span></span>

<span data-ttu-id="3d60d-147">We recommend that you poll the job status to determine when jobs complete.</span><span class="sxs-lookup"><span data-stu-id="3d60d-147">We recommend that you poll the job status to determine when jobs complete.</span></span> <span data-ttu-id="3d60d-148">When all your jobs have finished running, call the Resize Pool operation to set the number of virtual machines in the pool to zero.</span><span class="sxs-lookup"><span data-stu-id="3d60d-148">When all your jobs have finished running, call the Resize Pool operation to set the number of virtual machines in the pool to zero.</span></span> <span data-ttu-id="3d60d-149">If you are short on pool resources and you need to create a new pool, for example to bill against a different billing plan, you can delete the pool instead when all your jobs have finished running.</span><span class="sxs-lookup"><span data-stu-id="3d60d-149">If you are short on pool resources and you need to create a new pool, for example to bill against a different billing plan, you can delete the pool instead when all your jobs have finished running.</span></span>


| <span data-ttu-id="3d60d-150">**Use Batch Pool Processing when**</span><span class="sxs-lookup"><span data-stu-id="3d60d-150">**Use Batch Pool Processing when**</span></span>    | <span data-ttu-id="3d60d-151">**Use classic batch processing when**</span><span class="sxs-lookup"><span data-stu-id="3d60d-151">**Use classic batch processing when**</span></span>  |
|---|---|
|<span data-ttu-id="3d60d-152">You need to run a large number of jobs</span><span class="sxs-lookup"><span data-stu-id="3d60d-152">You need to run a large number of jobs</span></span><br><span data-ttu-id="3d60d-153">Or</span><span class="sxs-lookup"><span data-stu-id="3d60d-153">Or</span></span><br/><span data-ttu-id="3d60d-154">You need to know that your jobs will run immediately</span><span class="sxs-lookup"><span data-stu-id="3d60d-154">You need to know that your jobs will run immediately</span></span><br/><span data-ttu-id="3d60d-155">Or</span><span class="sxs-lookup"><span data-stu-id="3d60d-155">Or</span></span><br/><span data-ttu-id="3d60d-156">You need guaranteed throughput.</span><span class="sxs-lookup"><span data-stu-id="3d60d-156">You need guaranteed throughput.</span></span> <span data-ttu-id="3d60d-157">For example, you need to run a number of jobs in a given time frame, and want to scale out your compute resources to meet your needs.</span><span class="sxs-lookup"><span data-stu-id="3d60d-157">For example, you need to run a number of jobs in a given time frame, and want to scale out your compute resources to meet your needs.</span></span>    | <span data-ttu-id="3d60d-158">You are running just a few jobs</span><span class="sxs-lookup"><span data-stu-id="3d60d-158">You are running just a few jobs</span></span><br/><span data-ttu-id="3d60d-159">And</span><span class="sxs-lookup"><span data-stu-id="3d60d-159">And</span></span><br/> <span data-ttu-id="3d60d-160">You don’t need the jobs to run immediately</span><span class="sxs-lookup"><span data-stu-id="3d60d-160">You don’t need the jobs to run immediately</span></span> |

