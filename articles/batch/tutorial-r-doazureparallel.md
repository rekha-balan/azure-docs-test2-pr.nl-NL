---
title: Parallel R simulation with Azure Batch
description: Tutorial - Step by step instructions to run a Monte Carlo financial simulation in Azure Batch using the R doAzureParallel package
services: batch
author: dlepow
manager: jeconnoc
ms.assetid: ''
ms.service: batch
ms.devlang: r
ms.topic: tutorial
ms.date: 01/23/2018
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: fb616dc95cc7dd7dbb25f2deb832b517d0747ae4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871727"
---
# <a name="tutorial-run-a-parallel-r-simulation-with-azure-batch"></a><span data-ttu-id="105dc-103">Tutorial: Run a parallel R simulation with Azure Batch</span><span class="sxs-lookup"><span data-stu-id="105dc-103">Tutorial: Run a parallel R simulation with Azure Batch</span></span> 

<span data-ttu-id="105dc-104">Run your parallel R workloads at scale using [doAzureParallel](http://www.github.com/Azure/doAzureParallel), a lightweight R package that allows you to use Azure Batch directly from your R session.</span><span class="sxs-lookup"><span data-stu-id="105dc-104">Run your parallel R workloads at scale using [doAzureParallel](http://www.github.com/Azure/doAzureParallel), a lightweight R package that allows you to use Azure Batch directly from your R session.</span></span> <span data-ttu-id="105dc-105">The doAzureParallel package is built on top of the popular [foreach](http://cran.r-project.org/web/packages/foreach/index.html) R package.</span><span class="sxs-lookup"><span data-stu-id="105dc-105">The doAzureParallel package is built on top of the popular [foreach](http://cran.r-project.org/web/packages/foreach/index.html) R package.</span></span> <span data-ttu-id="105dc-106">doAzureParallel takes each iteration of the foreach loop and submits it as an Azure Batch task.</span><span class="sxs-lookup"><span data-stu-id="105dc-106">doAzureParallel takes each iteration of the foreach loop and submits it as an Azure Batch task.</span></span>

<span data-ttu-id="105dc-107">This tutorial shows you how to deploy a Batch pool and run a parallel R job in Azure Batch directly within RStudio.</span><span class="sxs-lookup"><span data-stu-id="105dc-107">This tutorial shows you how to deploy a Batch pool and run a parallel R job in Azure Batch directly within RStudio.</span></span> <span data-ttu-id="105dc-108">You learn how to:</span><span class="sxs-lookup"><span data-stu-id="105dc-108">You learn how to:</span></span>
 

> [!div class="checklist"]
> * <span data-ttu-id="105dc-109">Install doAzureParallel and configure it to access your Batch and storage accounts</span><span class="sxs-lookup"><span data-stu-id="105dc-109">Install doAzureParallel and configure it to access your Batch and storage accounts</span></span>
> * <span data-ttu-id="105dc-110">Create a Batch pool as a parallel backend for your R session</span><span class="sxs-lookup"><span data-stu-id="105dc-110">Create a Batch pool as a parallel backend for your R session</span></span>
> * <span data-ttu-id="105dc-111">Run a sample parallel simulation on the pool</span><span class="sxs-lookup"><span data-stu-id="105dc-111">Run a sample parallel simulation on the pool</span></span>

## <a name="prerequisites"></a><span data-ttu-id="105dc-112">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="105dc-112">Prerequisites</span></span>

* <span data-ttu-id="105dc-113">An installed [R](https://www.r-project.org/) distribution, such as [Microsoft R Open](https://mran.microsoft.com/open).</span><span class="sxs-lookup"><span data-stu-id="105dc-113">An installed [R](https://www.r-project.org/) distribution, such as [Microsoft R Open](https://mran.microsoft.com/open).</span></span> <span data-ttu-id="105dc-114">Use R version 3.3.1 or later.</span><span class="sxs-lookup"><span data-stu-id="105dc-114">Use R version 3.3.1 or later.</span></span>

* <span data-ttu-id="105dc-115">[RStudio](https://www.rstudio.com/), either the commercial edition or the open-source [RStudio Desktop](https://www.rstudio.com/products/rstudio/#Desktop).</span><span class="sxs-lookup"><span data-stu-id="105dc-115">[RStudio](https://www.rstudio.com/), either the commercial edition or the open-source [RStudio Desktop](https://www.rstudio.com/products/rstudio/#Desktop).</span></span> 

* <span data-ttu-id="105dc-116">An Azure Batch account and an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="105dc-116">An Azure Batch account and an Azure Storage account.</span></span> <span data-ttu-id="105dc-117">To create these accounts, see the Batch quickstarts using the [Azure portal](quick-create-portal.md) or [Azure CLI](quick-create-cli.md).</span><span class="sxs-lookup"><span data-stu-id="105dc-117">To create these accounts, see the Batch quickstarts using the [Azure portal](quick-create-portal.md) or [Azure CLI](quick-create-cli.md).</span></span> 

## <a name="sign-in-to-azure"></a><span data-ttu-id="105dc-118">Sign in to Azure</span><span class="sxs-lookup"><span data-stu-id="105dc-118">Sign in to Azure</span></span>

<span data-ttu-id="105dc-119">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="105dc-119">Sign in to the Azure portal at [https://portal.azure.com](https://portal.azure.com).</span></span>

[!INCLUDE [batch-common-credentials](../../includes/batch-common-credentials.md)] 
## <a name="install-doazureparallel"></a><span data-ttu-id="105dc-120">Install doAzureParallel</span><span class="sxs-lookup"><span data-stu-id="105dc-120">Install doAzureParallel</span></span>

<span data-ttu-id="105dc-121">In the RStudio console, install the [doAzureParallel Github package](http://www.github.com/Azure/doAzureParallel).</span><span class="sxs-lookup"><span data-stu-id="105dc-121">In the RStudio console, install the [doAzureParallel Github package](http://www.github.com/Azure/doAzureParallel).</span></span> <span data-ttu-id="105dc-122">The following commands download and install the package and its dependencies in your current R session:</span><span class="sxs-lookup"><span data-stu-id="105dc-122">The following commands download and install the package and its dependencies in your current R session:</span></span> 

```R
# Install the devtools package  
install.packages("devtools") 

# Install rAzureBatch package
devtools::install_github("Azure/rAzureBatch") 

# Install the doAzureParallel package 
devtools::install_github("Azure/doAzureParallel") 
 
# Load the doAzureParallel library 
library(doAzureParallel) 
```
<span data-ttu-id="105dc-123">Installation can take several minutes.</span><span class="sxs-lookup"><span data-stu-id="105dc-123">Installation can take several minutes.</span></span>

<span data-ttu-id="105dc-124">To configure doAzureParallel with the account credentials you obtained previously, generate a configuration file called *credentials.json* in your working directory:</span><span class="sxs-lookup"><span data-stu-id="105dc-124">To configure doAzureParallel with the account credentials you obtained previously, generate a configuration file called *credentials.json* in your working directory:</span></span> 

```R
generateCredentialsConfig("credentials.json") 
``` 

<span data-ttu-id="105dc-125">Populate this file with your Batch and storage account names and keys.</span><span class="sxs-lookup"><span data-stu-id="105dc-125">Populate this file with your Batch and storage account names and keys.</span></span> <span data-ttu-id="105dc-126">Leave the `githubAuthenticationToken` setting unchanged.</span><span class="sxs-lookup"><span data-stu-id="105dc-126">Leave the `githubAuthenticationToken` setting unchanged.</span></span>

<span data-ttu-id="105dc-127">When complete, the credentials file looks similar to the following:</span><span class="sxs-lookup"><span data-stu-id="105dc-127">When complete, the credentials file looks similar to the following:</span></span> 

```json
{
  "batchAccount": {
    "name": "mybatchaccount",
    "key": "xxxxxxxxxxxxxxxxE+yXrRvJAqT9BlXwwo1CwF+SwAYOxxxxxxxxxxxxxxxx43pXi/gdiATkvbpLRl3x14pcEQ==",
    "url": "https://mybatchaccount.mybatchregion.batch.azure.com"
  },
  "storageAccount": {
    "name": "mystorageaccount",
    "key": "xxxxxxxxxxxxxxxxy4/xxxxxxxxxxxxxxxxfwpbIC5aAWA8wDu+AFXZB827Mt9lybZB1nUcQbQiUrkPtilK5BQ=="
  },
  "githubAuthenticationToken": ""
}
```

<span data-ttu-id="105dc-128">Save the file.</span><span class="sxs-lookup"><span data-stu-id="105dc-128">Save the file.</span></span> <span data-ttu-id="105dc-129">Then, run the following command to set the credentials for your current R session:</span><span class="sxs-lookup"><span data-stu-id="105dc-129">Then, run the following command to set the credentials for your current R session:</span></span> 

```R
setCredentials("credentials.json") 
```

## <a name="create-a-batch-pool"></a><span data-ttu-id="105dc-130">Create a Batch pool</span><span class="sxs-lookup"><span data-stu-id="105dc-130">Create a Batch pool</span></span> 

<span data-ttu-id="105dc-131">doAzureParallel includes a function to generate an Azure Batch pool (cluster) to run parallel R jobs.</span><span class="sxs-lookup"><span data-stu-id="105dc-131">doAzureParallel includes a function to generate an Azure Batch pool (cluster) to run parallel R jobs.</span></span> <span data-ttu-id="105dc-132">The nodes run an Ubuntu-based [Azure Data Science Virtual Machine](../machine-learning/data-science-virtual-machine/overview.md).</span><span class="sxs-lookup"><span data-stu-id="105dc-132">The nodes run an Ubuntu-based [Azure Data Science Virtual Machine](../machine-learning/data-science-virtual-machine/overview.md).</span></span> <span data-ttu-id="105dc-133">Microsoft R Open and popular R packages are pre-installed on this image.</span><span class="sxs-lookup"><span data-stu-id="105dc-133">Microsoft R Open and popular R packages are pre-installed on this image.</span></span> <span data-ttu-id="105dc-134">You can view or customize certain cluster settings, such as the number and size of the nodes.</span><span class="sxs-lookup"><span data-stu-id="105dc-134">You can view or customize certain cluster settings, such as the number and size of the nodes.</span></span> 

<span data-ttu-id="105dc-135">To generate a cluster configuration JSON file in your working directory:</span><span class="sxs-lookup"><span data-stu-id="105dc-135">To generate a cluster configuration JSON file in your working directory:</span></span> 
 
```R
generateClusterConfig("cluster.json")
``` 
 
<span data-ttu-id="105dc-136">Open the file to view the default configuration, which includes 3 dedicated nodes and 3 [low-priority](batch-low-pri-vms.md) nodes.</span><span class="sxs-lookup"><span data-stu-id="105dc-136">Open the file to view the default configuration, which includes 3 dedicated nodes and 3 [low-priority](batch-low-pri-vms.md) nodes.</span></span> <span data-ttu-id="105dc-137">These settings are just examples that you can experiment with or modify.</span><span class="sxs-lookup"><span data-stu-id="105dc-137">These settings are just examples that you can experiment with or modify.</span></span> <span data-ttu-id="105dc-138">Dedicated nodes are reserved for your pool.</span><span class="sxs-lookup"><span data-stu-id="105dc-138">Dedicated nodes are reserved for your pool.</span></span> <span data-ttu-id="105dc-139">Low-priority nodes are offered at a reduced price from surplus VM capacity in Azure.</span><span class="sxs-lookup"><span data-stu-id="105dc-139">Low-priority nodes are offered at a reduced price from surplus VM capacity in Azure.</span></span> <span data-ttu-id="105dc-140">Low-priority nodes become unavailable if Azure does not have enough capacity.</span><span class="sxs-lookup"><span data-stu-id="105dc-140">Low-priority nodes become unavailable if Azure does not have enough capacity.</span></span> 

<span data-ttu-id="105dc-141">For this tutorial, change the configuration as follows:</span><span class="sxs-lookup"><span data-stu-id="105dc-141">For this tutorial, change the configuration as follows:</span></span>

* <span data-ttu-id="105dc-142">Increase the `maxTasksPerNode` to *2*, to take advantage of both cores on each node</span><span class="sxs-lookup"><span data-stu-id="105dc-142">Increase the `maxTasksPerNode` to *2*, to take advantage of both cores on each node</span></span>
* <span data-ttu-id="105dc-143">Set `dedicatedNodes` to *0*, so you can try the low-priority VMs available for Batch.</span><span class="sxs-lookup"><span data-stu-id="105dc-143">Set `dedicatedNodes` to *0*, so you can try the low-priority VMs available for Batch.</span></span> <span data-ttu-id="105dc-144">Set the `min` of `lowPriorityNodes` to *5*.</span><span class="sxs-lookup"><span data-stu-id="105dc-144">Set the `min` of `lowPriorityNodes` to *5*.</span></span> <span data-ttu-id="105dc-145">and the `max` to *10*, or choose smaller numbers if desired.</span><span class="sxs-lookup"><span data-stu-id="105dc-145">and the `max` to *10*, or choose smaller numbers if desired.</span></span> 

<span data-ttu-id="105dc-146">Leave defaults for the remaining settings, and save the file.</span><span class="sxs-lookup"><span data-stu-id="105dc-146">Leave defaults for the remaining settings, and save the file.</span></span> <span data-ttu-id="105dc-147">It should look similar to the following:</span><span class="sxs-lookup"><span data-stu-id="105dc-147">It should look similar to the following:</span></span>

```json
{
  "name": "myPoolName",
  "vmSize": "Standard_D2_v2",
  "maxTasksPerNode": 4,
  "poolSize": {
    "dedicatedNodes": {
      "min": 0,
      "max": 0
    },
    "lowPriorityNodes": {
      "min": 5,
      "max": 10
    },
    "autoscaleFormula": "QUEUE"
  },
  "containerImage": "rocker/tidyverse:latest",
  "rPackages": {
    "cran": [],
    "github": [],
    "bioconductor": []
  },
  "commandLine": []
}
```

<span data-ttu-id="105dc-148">Now create the cluster.</span><span class="sxs-lookup"><span data-stu-id="105dc-148">Now create the cluster.</span></span> <span data-ttu-id="105dc-149">Batch creates the pool immediately, but it takes a few minutes to allocate and start the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="105dc-149">Batch creates the pool immediately, but it takes a few minutes to allocate and start the compute nodes.</span></span> <span data-ttu-id="105dc-150">After the cluster is available, register it as the parallel backend for your R session.</span><span class="sxs-lookup"><span data-stu-id="105dc-150">After the cluster is available, register it as the parallel backend for your R session.</span></span> 

```R
# Create your cluster if it does not exist; this takes a few minutes
cluster <- makeCluster("cluster.json") 
  
# Register your parallel backend 
registerDoAzureParallel(cluster) 
  
# Check that the nodes are running 
getDoParWorkers() 
```

<span data-ttu-id="105dc-151">Output shows the number of "execution workers" for doAzureParallel.</span><span class="sxs-lookup"><span data-stu-id="105dc-151">Output shows the number of "execution workers" for doAzureParallel.</span></span> <span data-ttu-id="105dc-152">This number is the number of nodes multiplied by the value of `maxTasksPerNode`.</span><span class="sxs-lookup"><span data-stu-id="105dc-152">This number is the number of nodes multiplied by the value of `maxTasksPerNode`.</span></span> <span data-ttu-id="105dc-153">If you modified the cluster configuration as described previously, the number is *10*.</span><span class="sxs-lookup"><span data-stu-id="105dc-153">If you modified the cluster configuration as described previously, the number is *10*.</span></span> 
 
## <a name="run-a-parallel-simulation"></a><span data-ttu-id="105dc-154">Run a parallel simulation</span><span class="sxs-lookup"><span data-stu-id="105dc-154">Run a parallel simulation</span></span>

<span data-ttu-id="105dc-155">Now that your cluster is created, you are ready to run your foreach loop with your registered parallel backend (Azure Batch pool).</span><span class="sxs-lookup"><span data-stu-id="105dc-155">Now that your cluster is created, you are ready to run your foreach loop with your registered parallel backend (Azure Batch pool).</span></span> <span data-ttu-id="105dc-156">As an example, run a Monte Carlo financial simulation, first locally using a standard foreach loop, and then running foreach with Batch.</span><span class="sxs-lookup"><span data-stu-id="105dc-156">As an example, run a Monte Carlo financial simulation, first locally using a standard foreach loop, and then running foreach with Batch.</span></span> <span data-ttu-id="105dc-157">This example is a simplified version of predicting a stock price by simulating a large number of different outcomes after 5 years.</span><span class="sxs-lookup"><span data-stu-id="105dc-157">This example is a simplified version of predicting a stock price by simulating a large number of different outcomes after 5 years.</span></span>

<span data-ttu-id="105dc-158">Suppose that the stock of Contoso Corporation gains on average 1.001 times its opening price each day, but has a volatility (standard deviation) of 0.01.</span><span class="sxs-lookup"><span data-stu-id="105dc-158">Suppose that the stock of Contoso Corporation gains on average 1.001 times its opening price each day, but has a volatility (standard deviation) of 0.01.</span></span> <span data-ttu-id="105dc-159">Given a starting price of $100, use a Monte Carlo pricing simulation to figure out Contoso's stock price after 5 years.</span><span class="sxs-lookup"><span data-stu-id="105dc-159">Given a starting price of $100, use a Monte Carlo pricing simulation to figure out Contoso's stock price after 5 years.</span></span>

<span data-ttu-id="105dc-160">Parameters for the Monte Carlo simulation:</span><span class="sxs-lookup"><span data-stu-id="105dc-160">Parameters for the Monte Carlo simulation:</span></span>

```R
mean_change = 1.001 
volatility = 0.01 
opening_price = 100 
```

<span data-ttu-id="105dc-161">To simulate closing prices, define the following function:</span><span class="sxs-lookup"><span data-stu-id="105dc-161">To simulate closing prices, define the following function:</span></span>

```R
getClosingPrice <- function() { 
  days <- 1825 # ~ 5 years 
  movement <- rnorm(days, mean=mean_change, sd=volatility) 
  path <- cumprod(c(opening_price, movement)) 
  closingPrice <- path[days] 
  return(closingPrice) 
} 
```

<span data-ttu-id="105dc-162">First run 10,000 simulations locally using a standard foreach loop with the `%do%` keyword:</span><span class="sxs-lookup"><span data-stu-id="105dc-162">First run 10,000 simulations locally using a standard foreach loop with the `%do%` keyword:</span></span>

```R
start_s <- Sys.time() 
# Run 10,000 simulations in series 
closingPrices_s <- foreach(i = 1:10, .combine='c') %do% { 
  replicate(1000, getClosingPrice()) 
} 
end_s <- Sys.time() 
```


<span data-ttu-id="105dc-163">Plot the closing prices in a histogram to show the distribution of outcomes:</span><span class="sxs-lookup"><span data-stu-id="105dc-163">Plot the closing prices in a histogram to show the distribution of outcomes:</span></span>

```R
hist(closingPrices_s)
``` 

<span data-ttu-id="105dc-164">Output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="105dc-164">Output is similar to the following:</span></span>

![Distribution of closing prices](media/tutorial-r-doazureparallel/closing-prices-local.png)
  
<span data-ttu-id="105dc-166">A local simulation completes in a few seconds or less:</span><span class="sxs-lookup"><span data-stu-id="105dc-166">A local simulation completes in a few seconds or less:</span></span>

```R
difftime(end_s, start_s) 
```

<span data-ttu-id="105dc-167">Estimated runtime for 10 million outcomes locally, using a linear approximation, is around 30 minutes:</span><span class="sxs-lookup"><span data-stu-id="105dc-167">Estimated runtime for 10 million outcomes locally, using a linear approximation, is around 30 minutes:</span></span>

```R 
1000 * difftime(end_s, start_s, unit = "min") 
```


<span data-ttu-id="105dc-168">Now run the code using `foreach` with the `%dopar%` keyword to compare how long it takes to run 10 million simulations in Azure.</span><span class="sxs-lookup"><span data-stu-id="105dc-168">Now run the code using `foreach` with the `%dopar%` keyword to compare how long it takes to run 10 million simulations in Azure.</span></span> <span data-ttu-id="105dc-169">To parallelize the simulation with Batch, run 100 iterations of 100,000 simulations:</span><span class="sxs-lookup"><span data-stu-id="105dc-169">To parallelize the simulation with Batch, run 100 iterations of 100,000 simulations:</span></span>

```R
# Optimize runtime. Chunking allows running multiple iterations on a single R instance.
opt <- list(chunkSize = 10) 
start_p <- Sys.time()  
closingPrices_p <- foreach(i = 1:100, .combine='c', .options.azure = opt) %dopar% { 
  replicate(100000, getClosingPrice()) 
} 
end_p <- Sys.time() 
```

<span data-ttu-id="105dc-170">The simulation distributes tasks to the nodes in the Batch pool.</span><span class="sxs-lookup"><span data-stu-id="105dc-170">The simulation distributes tasks to the nodes in the Batch pool.</span></span> <span data-ttu-id="105dc-171">You can see the activity in the heat map for the pool in the Azure portal].</span><span class="sxs-lookup"><span data-stu-id="105dc-171">You can see the activity in the heat map for the pool in the Azure portal].</span></span> <span data-ttu-id="105dc-172">Go to **Batch accounts** > *myBatchAccount*.</span><span class="sxs-lookup"><span data-stu-id="105dc-172">Go to **Batch accounts** > *myBatchAccount*.</span></span> <span data-ttu-id="105dc-173">Click **Pools** > *myPoolName*.</span><span class="sxs-lookup"><span data-stu-id="105dc-173">Click **Pools** > *myPoolName*.</span></span> 

![Heat map of pool running parallel R tasks](media/tutorial-r-doazureparallel/pool.png)

<span data-ttu-id="105dc-175">After a few minutes, the simulation finishes.</span><span class="sxs-lookup"><span data-stu-id="105dc-175">After a few minutes, the simulation finishes.</span></span> <span data-ttu-id="105dc-176">The package automatically merges the results and pulls them down from the nodes.</span><span class="sxs-lookup"><span data-stu-id="105dc-176">The package automatically merges the results and pulls them down from the nodes.</span></span> <span data-ttu-id="105dc-177">Then, you are ready to use the results in your R session.</span><span class="sxs-lookup"><span data-stu-id="105dc-177">Then, you are ready to use the results in your R session.</span></span> 

```R
hist(closingPrices_p) 
```

<span data-ttu-id="105dc-178">Output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="105dc-178">Output is similar to the following:</span></span>

![Distribution of closing prices](media/tutorial-r-doazureparallel/closing-prices.png)

<span data-ttu-id="105dc-180">How long did the parallel simulation take?</span><span class="sxs-lookup"><span data-stu-id="105dc-180">How long did the parallel simulation take?</span></span> 

```R
difftime(end_p, start_p, unit = "min")  
```

<span data-ttu-id="105dc-181">You should see that running the simulation on the Batch pool gives you a significant increase in performance over the expected time to run the simulation locally.</span><span class="sxs-lookup"><span data-stu-id="105dc-181">You should see that running the simulation on the Batch pool gives you a significant increase in performance over the expected time to run the simulation locally.</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="105dc-182">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="105dc-182">Clean up resources</span></span>

<span data-ttu-id="105dc-183">The job is deleted automatically after it completes.</span><span class="sxs-lookup"><span data-stu-id="105dc-183">The job is deleted automatically after it completes.</span></span> <span data-ttu-id="105dc-184">When the cluster is longer needed, call the `stopCluster` function in the doAzureParallel package to delete it:</span><span class="sxs-lookup"><span data-stu-id="105dc-184">When the cluster is longer needed, call the `stopCluster` function in the doAzureParallel package to delete it:</span></span>

```R
stopCluster(cluster)
```

## <a name="next-steps"></a><span data-ttu-id="105dc-185">Next steps</span><span class="sxs-lookup"><span data-stu-id="105dc-185">Next steps</span></span>
<span data-ttu-id="105dc-186">In this tutorial, you learned about how to:</span><span class="sxs-lookup"><span data-stu-id="105dc-186">In this tutorial, you learned about how to:</span></span>

> [!div class="checklist"]
<span data-ttu-id="105dc-187">Install doAzureParallel and configure it to access your Batch and storage accounts</span><span class="sxs-lookup"><span data-stu-id="105dc-187">Install doAzureParallel and configure it to access your Batch and storage accounts</span></span>
> * <span data-ttu-id="105dc-188">Create a Batch pool as a parallel backend for your R session</span><span class="sxs-lookup"><span data-stu-id="105dc-188">Create a Batch pool as a parallel backend for your R session</span></span>
> * <span data-ttu-id="105dc-189">Run a sample parallel simulation on the pool</span><span class="sxs-lookup"><span data-stu-id="105dc-189">Run a sample parallel simulation on the pool</span></span>


<span data-ttu-id="105dc-190">For more information about doAzureParallel, see the documentation and samples on GitHub.</span><span class="sxs-lookup"><span data-stu-id="105dc-190">For more information about doAzureParallel, see the documentation and samples on GitHub.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="105dc-191">doAzureParallel package</span><span class="sxs-lookup"><span data-stu-id="105dc-191">doAzureParallel package</span></span>](https://github.com/Azure/doAzureParallel/)




