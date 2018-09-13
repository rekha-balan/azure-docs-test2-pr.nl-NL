---
title: Azure Machine Learning Model Management Setup and Configuration | Microsoft Docs
description: This document describes the steps and concepts involved in setting up and configuring Model Management in Azure Machine Learning.
services: machine-learning
author: raymondlaghaeian
ms.author: raymondl
manager: hjerez
ms.reviewer: jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 08/29/2017
ms.openlocfilehash: 883e3d2c5945a38c8fbca5c9f0f5e8a1e4093be1
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866345"
---
# <a name="model-management-setup"></a><span data-ttu-id="257c5-103">Model management setup</span><span class="sxs-lookup"><span data-stu-id="257c5-103">Model management setup</span></span>

## <a name="overview"></a><span data-ttu-id="257c5-104">Overview</span><span class="sxs-lookup"><span data-stu-id="257c5-104">Overview</span></span>
<span data-ttu-id="257c5-105">This document gets you started with using Azure ML model management to deploy and manage your machine learning models as web services.</span><span class="sxs-lookup"><span data-stu-id="257c5-105">This document gets you started with using Azure ML model management to deploy and manage your machine learning models as web services.</span></span> 

<span data-ttu-id="257c5-106">Using Azure ML model management, you can efficiently deploy and manage Machine Learning models that are built using a number of frameworks including SparkML, Keras, TensorFlow, the Microsoft Cognitive Toolkit, or Python.</span><span class="sxs-lookup"><span data-stu-id="257c5-106">Using Azure ML model management, you can efficiently deploy and manage Machine Learning models that are built using a number of frameworks including SparkML, Keras, TensorFlow, the Microsoft Cognitive Toolkit, or Python.</span></span> 

<span data-ttu-id="257c5-107">By the end of this document, you should be able to have your model management environment set up and ready for deploying your machine learning models.</span><span class="sxs-lookup"><span data-stu-id="257c5-107">By the end of this document, you should be able to have your model management environment set up and ready for deploying your machine learning models.</span></span>

## <a name="what-you-need-to-get-started"></a><span data-ttu-id="257c5-108">What you need to get started</span><span class="sxs-lookup"><span data-stu-id="257c5-108">What you need to get started</span></span>
<span data-ttu-id="257c5-109">To get the most out of this guide, you should have owner access to an Azure subscription that you can deploy your models to.</span><span class="sxs-lookup"><span data-stu-id="257c5-109">To get the most out of this guide, you should have owner access to an Azure subscription that you can deploy your models to.</span></span>
<span data-ttu-id="257c5-110">The CLI comes pre-installed on the Azure Machine Learning Workbench and on [Azure DSVMs](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview).</span><span class="sxs-lookup"><span data-stu-id="257c5-110">The CLI comes pre-installed on the Azure Machine Learning Workbench and on [Azure DSVMs](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview).</span></span>

## <a name="using-the-cli"></a><span data-ttu-id="257c5-111">Using the CLI</span><span class="sxs-lookup"><span data-stu-id="257c5-111">Using the CLI</span></span>
<span data-ttu-id="257c5-112">To use the command-line interfaces (CLIs) from the Workbench, click **File** -] **Open CommandLine Interface**.</span><span class="sxs-lookup"><span data-stu-id="257c5-112">To use the command-line interfaces (CLIs) from the Workbench, click **File** -] **Open CommandLine Interface**.</span></span> 

<span data-ttu-id="257c5-113">On a Data Science Virtual Machine, connect and open the command prompt.</span><span class="sxs-lookup"><span data-stu-id="257c5-113">On a Data Science Virtual Machine, connect and open the command prompt.</span></span> <span data-ttu-id="257c5-114">Type `az ml -h` to see the options.</span><span class="sxs-lookup"><span data-stu-id="257c5-114">Type `az ml -h` to see the options.</span></span> <span data-ttu-id="257c5-115">For more details on the commands, use the --help flag.</span><span class="sxs-lookup"><span data-stu-id="257c5-115">For more details on the commands, use the --help flag.</span></span>

<span data-ttu-id="257c5-116">On all other systems, you would have to install the CLIs.</span><span class="sxs-lookup"><span data-stu-id="257c5-116">On all other systems, you would have to install the CLIs.</span></span>

### <a name="installing-or-updating-on-windows"></a><span data-ttu-id="257c5-117">Installing (or updating) on Windows</span><span class="sxs-lookup"><span data-stu-id="257c5-117">Installing (or updating) on Windows</span></span>

<span data-ttu-id="257c5-118">Install Python from https://www.python.org/.</span><span class="sxs-lookup"><span data-stu-id="257c5-118">Install Python from https://www.python.org/.</span></span> <span data-ttu-id="257c5-119">Ensure that you have selected to install pip.</span><span class="sxs-lookup"><span data-stu-id="257c5-119">Ensure that you have selected to install pip.</span></span>

<span data-ttu-id="257c5-120">Open a command prompt using Run As Administrator and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="257c5-120">Open a command prompt using Run As Administrator and run the following commands:</span></span>

```cmd
pip install azure-cli
pip install azure-cli-ml
```
 
>[!NOTE]
><span data-ttu-id="257c5-121">If you have an earlier version, uninstall it first using the following command:</span><span class="sxs-lookup"><span data-stu-id="257c5-121">If you have an earlier version, uninstall it first using the following command:</span></span>
>

```cmd
pip uninstall azure-cli-ml
```

### <a name="installing-or-updating-on-linux"></a><span data-ttu-id="257c5-122">Installing (or updating) on Linux</span><span class="sxs-lookup"><span data-stu-id="257c5-122">Installing (or updating) on Linux</span></span>
<span data-ttu-id="257c5-123">Run the following command from the command line, and follow the prompts:</span><span class="sxs-lookup"><span data-stu-id="257c5-123">Run the following command from the command line, and follow the prompts:</span></span>

```bash
sudo -i
pip install azure-cli
pip install azure-cli-ml
```

<span data-ttu-id="257c5-124">After intallation is complete, run the following command:</span><span class="sxs-lookup"><span data-stu-id="257c5-124">After intallation is complete, run the following command:</span></span>

```bash
sudo /opt/microsoft/azureml/initial_setup.sh
```

>[!NOTE]
><span data-ttu-id="257c5-125">Log out and log back in to your SSH session for the changes to take effect.</span><span class="sxs-lookup"><span data-stu-id="257c5-125">Log out and log back in to your SSH session for the changes to take effect.</span></span>
><span data-ttu-id="257c5-126">You can use the previous commands to update an earlier version of the CLIs on the DSVM.</span><span class="sxs-lookup"><span data-stu-id="257c5-126">You can use the previous commands to update an earlier version of the CLIs on the DSVM.</span></span>
>

## <a name="deploying-your-model"></a><span data-ttu-id="257c5-127">Deploying your model</span><span class="sxs-lookup"><span data-stu-id="257c5-127">Deploying your model</span></span>
<span data-ttu-id="257c5-128">Use the CLIs to deploy models as web services.</span><span class="sxs-lookup"><span data-stu-id="257c5-128">Use the CLIs to deploy models as web services.</span></span> <span data-ttu-id="257c5-129">The web services can be deployed locally or to a cluster.</span><span class="sxs-lookup"><span data-stu-id="257c5-129">The web services can be deployed locally or to a cluster.</span></span>

<span data-ttu-id="257c5-130">Start with a local deployment, validate that your model and code work, then deploy to a cluster for production scale use.</span><span class="sxs-lookup"><span data-stu-id="257c5-130">Start with a local deployment, validate that your model and code work, then deploy to a cluster for production scale use.</span></span>

<span data-ttu-id="257c5-131">To start, you need to set up your deployment environment.</span><span class="sxs-lookup"><span data-stu-id="257c5-131">To start, you need to set up your deployment environment.</span></span> <span data-ttu-id="257c5-132">The environment setup is a one time task.</span><span class="sxs-lookup"><span data-stu-id="257c5-132">The environment setup is a one time task.</span></span> <span data-ttu-id="257c5-133">Once the setup is complete, you can reuse the environment for subsequent deployments.</span><span class="sxs-lookup"><span data-stu-id="257c5-133">Once the setup is complete, you can reuse the environment for subsequent deployments.</span></span> <span data-ttu-id="257c5-134">See the following section for more detail.</span><span class="sxs-lookup"><span data-stu-id="257c5-134">See the following section for more detail.</span></span>

<span data-ttu-id="257c5-135">When completing the environment setup:</span><span class="sxs-lookup"><span data-stu-id="257c5-135">When completing the environment setup:</span></span>
- <span data-ttu-id="257c5-136">You are prompted to sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="257c5-136">You are prompted to sign in to Azure.</span></span> <span data-ttu-id="257c5-137">To sign in, use a web browser to open the page https://aka.ms/devicelogin and enter the provided code to authenticate.</span><span class="sxs-lookup"><span data-stu-id="257c5-137">To sign in, use a web browser to open the page https://aka.ms/devicelogin and enter the provided code to authenticate.</span></span>
- <span data-ttu-id="257c5-138">During the authentication process, you are prompted for an account to authenticate with.</span><span class="sxs-lookup"><span data-stu-id="257c5-138">During the authentication process, you are prompted for an account to authenticate with.</span></span> <span data-ttu-id="257c5-139">Important: Select an account that has a valid Azure subscription and sufficient permissions to create resources in the account.- When the log-in is complete, your subscription information is presented and you are prompted whether you wish to continue with the selected account.</span><span class="sxs-lookup"><span data-stu-id="257c5-139">Important: Select an account that has a valid Azure subscription and sufficient permissions to create resources in the account.- When the log-in is complete, your subscription information is presented and you are prompted whether you wish to continue with the selected account.</span></span>

### <a name="environment-setup"></a><span data-ttu-id="257c5-140">Environment Setup</span><span class="sxs-lookup"><span data-stu-id="257c5-140">Environment Setup</span></span>
<span data-ttu-id="257c5-141">To start the setup process, you need to register the environment provider by entering the following command:</span><span class="sxs-lookup"><span data-stu-id="257c5-141">To start the setup process, you need to register the environment provider by entering the following command:</span></span>

```azurecli
az provider register -n Microsoft.MachineLearningCompute
```

#### <a name="local-deployment"></a><span data-ttu-id="257c5-142">Local deployment</span><span class="sxs-lookup"><span data-stu-id="257c5-142">Local deployment</span></span>
<span data-ttu-id="257c5-143">To deploy and test your web service on the local machine, set up a local environment using the following command:</span><span class="sxs-lookup"><span data-stu-id="257c5-143">To deploy and test your web service on the local machine, set up a local environment using the following command:</span></span>

```azurecli
az ml env setup -l [location of Azure Region, e.g. eastus2] -n [your environment name] [-g [existing resource group]]
```
>[!NOTE] 
><span data-ttu-id="257c5-144">Local web service deployment requires your to install Docker on the local machine.</span><span class="sxs-lookup"><span data-stu-id="257c5-144">Local web service deployment requires your to install Docker on the local machine.</span></span> 
>

<span data-ttu-id="257c5-145">The local environment setup command creates the following resources in your subscription:</span><span class="sxs-lookup"><span data-stu-id="257c5-145">The local environment setup command creates the following resources in your subscription:</span></span>
- <span data-ttu-id="257c5-146">A resource group (if not provided)</span><span class="sxs-lookup"><span data-stu-id="257c5-146">A resource group (if not provided)</span></span>
- <span data-ttu-id="257c5-147">A storage account</span><span class="sxs-lookup"><span data-stu-id="257c5-147">A storage account</span></span>
- <span data-ttu-id="257c5-148">An Azure Container Registry (ACR)</span><span class="sxs-lookup"><span data-stu-id="257c5-148">An Azure Container Registry (ACR)</span></span>
- <span data-ttu-id="257c5-149">Application insights</span><span class="sxs-lookup"><span data-stu-id="257c5-149">Application insights</span></span>

<span data-ttu-id="257c5-150">After setup completes successfully, set the environment to be used using the following command:</span><span class="sxs-lookup"><span data-stu-id="257c5-150">After setup completes successfully, set the environment to be used using the following command:</span></span>

```azurecli
az ml env set -n [environment name] -g [resource group]
```

#### <a name="cluster-deployment"></a><span data-ttu-id="257c5-151">Cluster deployment</span><span class="sxs-lookup"><span data-stu-id="257c5-151">Cluster deployment</span></span>
<span data-ttu-id="257c5-152">Use Cluster deployment for high-scale production scenarios.</span><span class="sxs-lookup"><span data-stu-id="257c5-152">Use Cluster deployment for high-scale production scenarios.</span></span> <span data-ttu-id="257c5-153">It sets up an ACS cluster with Kubernetes as the orchestrator.</span><span class="sxs-lookup"><span data-stu-id="257c5-153">It sets up an ACS cluster with Kubernetes as the orchestrator.</span></span> <span data-ttu-id="257c5-154">The ACS cluster can be scaled out to handle larger throughput for your web service calls.</span><span class="sxs-lookup"><span data-stu-id="257c5-154">The ACS cluster can be scaled out to handle larger throughput for your web service calls.</span></span>

<span data-ttu-id="257c5-155">To deploy your web service to a production environment, first set up the environment using the following command:</span><span class="sxs-lookup"><span data-stu-id="257c5-155">To deploy your web service to a production environment, first set up the environment using the following command:</span></span>

```azurecli
az ml env setup -c --name [your environment name] --location [Azure region e.g. eastus2] [-g [resource group]]
```

<span data-ttu-id="257c5-156">The cluster environment setup command creates the following resources in your subscription:</span><span class="sxs-lookup"><span data-stu-id="257c5-156">The cluster environment setup command creates the following resources in your subscription:</span></span>
- <span data-ttu-id="257c5-157">A resource group (if not provided)</span><span class="sxs-lookup"><span data-stu-id="257c5-157">A resource group (if not provided)</span></span>
- <span data-ttu-id="257c5-158">A storage account</span><span class="sxs-lookup"><span data-stu-id="257c5-158">A storage account</span></span>
- <span data-ttu-id="257c5-159">An Azure Container Registry (ACR)</span><span class="sxs-lookup"><span data-stu-id="257c5-159">An Azure Container Registry (ACR)</span></span>
- <span data-ttu-id="257c5-160">A Kubernetes deployment on an Azure Container Service (ACS) cluster</span><span class="sxs-lookup"><span data-stu-id="257c5-160">A Kubernetes deployment on an Azure Container Service (ACS) cluster</span></span>
- <span data-ttu-id="257c5-161">Application insights</span><span class="sxs-lookup"><span data-stu-id="257c5-161">Application insights</span></span>

<span data-ttu-id="257c5-162">The resource group, storage account, and ACR are created quickly.</span><span class="sxs-lookup"><span data-stu-id="257c5-162">The resource group, storage account, and ACR are created quickly.</span></span> <span data-ttu-id="257c5-163">The ACS deployment can take up to 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="257c5-163">The ACS deployment can take up to 20 minutes.</span></span> 

<span data-ttu-id="257c5-164">After setup is complete, you need to set the environment to be used for this deployment.</span><span class="sxs-lookup"><span data-stu-id="257c5-164">After setup is complete, you need to set the environment to be used for this deployment.</span></span> <span data-ttu-id="257c5-165">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="257c5-165">Use the following command:</span></span>

```azurecli
az ml env set -n [environment name] -g [resource group]
```

>[!NOTE] 
> <span data-ttu-id="257c5-166">After the environment is created, for subsequent deployments, you only need to use the set command above to reuse it.</span><span class="sxs-lookup"><span data-stu-id="257c5-166">After the environment is created, for subsequent deployments, you only need to use the set command above to reuse it.</span></span>
>

>[!NOTE] 
><span data-ttu-id="257c5-167">To create an HTTPS endpoint, specify an SSL cert when creating a cluster by using the --cert-name and --cert-pem options in az ml env setup.</span><span class="sxs-lookup"><span data-stu-id="257c5-167">To create an HTTPS endpoint, specify an SSL cert when creating a cluster by using the --cert-name and --cert-pem options in az ml env setup.</span></span> <span data-ttu-id="257c5-168">This sets up the cluster to serve requests on https, secured using the provided certificate.</span><span class="sxs-lookup"><span data-stu-id="257c5-168">This sets up the cluster to serve requests on https, secured using the provided certificate.</span></span> <span data-ttu-id="257c5-169">After setup is complete, create a CNAME DNS record that points to the cluster’s FQDN.</span><span class="sxs-lookup"><span data-stu-id="257c5-169">After setup is complete, create a CNAME DNS record that points to the cluster’s FQDN.</span></span>

### <a name="create-an-account"></a><span data-ttu-id="257c5-170">Create an Account</span><span class="sxs-lookup"><span data-stu-id="257c5-170">Create an Account</span></span>
<span data-ttu-id="257c5-171">An account is required for deploying models.</span><span class="sxs-lookup"><span data-stu-id="257c5-171">An account is required for deploying models.</span></span> <span data-ttu-id="257c5-172">You need to do this once per account, and can reuse the same account in multiple deployments.</span><span class="sxs-lookup"><span data-stu-id="257c5-172">You need to do this once per account, and can reuse the same account in multiple deployments.</span></span>

<span data-ttu-id="257c5-173">To create a new account, use the following command:</span><span class="sxs-lookup"><span data-stu-id="257c5-173">To create a new account, use the following command:</span></span>

```azurecli
az ml account modelmanagement create -l [Azure region, e.g. eastus2] -n [your account name] -g [resource group name] --sku-instances [number of instances, e.g. 1] --sku-name [Pricing tier for example S1]
```

<span data-ttu-id="257c5-174">To use an existing account, use the following command:</span><span class="sxs-lookup"><span data-stu-id="257c5-174">To use an existing account, use the following command:</span></span>
```azurecli
az ml account modelmanagement set -n [your account name] -g [resource group it was created in]
```

### <a name="deploy-your-model"></a><span data-ttu-id="257c5-175">Deploy your model</span><span class="sxs-lookup"><span data-stu-id="257c5-175">Deploy your model</span></span>
<span data-ttu-id="257c5-176">You are now ready to deploy your saved model as a web service.</span><span class="sxs-lookup"><span data-stu-id="257c5-176">You are now ready to deploy your saved model as a web service.</span></span> 

```azurecli
az ml service create realtime --model-file [model file/folder path] -f [scoring file e.g. score.py] -n [your service name] -s [schema file e.g. service_schema.json] -r [runtime for the Docker container e.g. spark-py or python] -c [conda dependencies file for additional python packages]
```

### <a name="next-steps"></a><span data-ttu-id="257c5-177">Next Steps</span><span class="sxs-lookup"><span data-stu-id="257c5-177">Next Steps</span></span>
<span data-ttu-id="257c5-178">Try one of many samples in the Gallery.</span><span class="sxs-lookup"><span data-stu-id="257c5-178">Try one of many samples in the Gallery.</span></span>
