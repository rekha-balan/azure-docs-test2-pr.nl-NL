---
title: Azure Machine Learning Model Management Setup and Configuration | Microsoft Docs
description: This document describes the steps and concepts involved in setting up and configuring Model Management in Azure Machine Learning.
services: machine-learning
author: aashishb
ms.author: aashishb
manager: hjerez
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: article
ms.date: 12/6/2017
ms.openlocfilehash: 150114184f6f04f22aa9da409758daa6a0d175b5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870194"
---
# <a name="model-management-setup"></a><span data-ttu-id="ea61c-103">Model management setup</span><span class="sxs-lookup"><span data-stu-id="ea61c-103">Model management setup</span></span>

<span data-ttu-id="ea61c-104">This document gets you started with using Azure ML model management to deploy and manage your machine learning models as web services.</span><span class="sxs-lookup"><span data-stu-id="ea61c-104">This document gets you started with using Azure ML model management to deploy and manage your machine learning models as web services.</span></span> 

<span data-ttu-id="ea61c-105">Using Azure ML model management, you can efficiently deploy and manage Machine Learning models that are built using a number of frameworks including SparkML, Keras, TensorFlow, the Microsoft Cognitive Toolkit, or Python.</span><span class="sxs-lookup"><span data-stu-id="ea61c-105">Using Azure ML model management, you can efficiently deploy and manage Machine Learning models that are built using a number of frameworks including SparkML, Keras, TensorFlow, the Microsoft Cognitive Toolkit, or Python.</span></span> 

<span data-ttu-id="ea61c-106">By the end of this document, you should be able to have your model management environment set up and ready for deploying your machine learning models.</span><span class="sxs-lookup"><span data-stu-id="ea61c-106">By the end of this document, you should be able to have your model management environment set up and ready for deploying your machine learning models.</span></span>

## <a name="what-you-need-to-get-started"></a><span data-ttu-id="ea61c-107">What you need to get started</span><span class="sxs-lookup"><span data-stu-id="ea61c-107">What you need to get started</span></span>
<span data-ttu-id="ea61c-108">To get the most out of this guide, you should have contributer access to an Azure subscription or a resource group that you can deploy your models to.</span><span class="sxs-lookup"><span data-stu-id="ea61c-108">To get the most out of this guide, you should have contributer access to an Azure subscription or a resource group that you can deploy your models to.</span></span>
<span data-ttu-id="ea61c-109">The CLI comes pre-installed on the Azure Machine Learning Workbench and on [Azure DSVMs](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview).</span><span class="sxs-lookup"><span data-stu-id="ea61c-109">The CLI comes pre-installed on the Azure Machine Learning Workbench and on [Azure DSVMs](https://docs.microsoft.com/azure/machine-learning/machine-learning-data-science-virtual-machine-overview).</span></span>

## <a name="using-the-cli"></a><span data-ttu-id="ea61c-110">Using the CLI</span><span class="sxs-lookup"><span data-stu-id="ea61c-110">Using the CLI</span></span>
<span data-ttu-id="ea61c-111">To use the command-line interfaces (CLIs) from the Workbench, click **File** -> **Open Command Prompt**.</span><span class="sxs-lookup"><span data-stu-id="ea61c-111">To use the command-line interfaces (CLIs) from the Workbench, click **File** -> **Open Command Prompt**.</span></span> 

<span data-ttu-id="ea61c-112">On a Data Science Virtual Machine, connect and open the command prompt.</span><span class="sxs-lookup"><span data-stu-id="ea61c-112">On a Data Science Virtual Machine, connect and open the command prompt.</span></span> <span data-ttu-id="ea61c-113">Type `az ml -h` to see the options.</span><span class="sxs-lookup"><span data-stu-id="ea61c-113">Type `az ml -h` to see the options.</span></span> <span data-ttu-id="ea61c-114">For more details on the commands, use the --help flag.</span><span class="sxs-lookup"><span data-stu-id="ea61c-114">For more details on the commands, use the --help flag.</span></span>

<span data-ttu-id="ea61c-115">On all other systems, you would have to install the CLIs.</span><span class="sxs-lookup"><span data-stu-id="ea61c-115">On all other systems, you would have to install the CLIs.</span></span>

>[!NOTE]
> <span data-ttu-id="ea61c-116">In a Jupyter notebook on a Linux DSVM, you can access the Azure CLI and Azure ML CLI with the command format below.</span><span class="sxs-lookup"><span data-stu-id="ea61c-116">In a Jupyter notebook on a Linux DSVM, you can access the Azure CLI and Azure ML CLI with the command format below.</span></span>  <span data-ttu-id="ea61c-117">**This is for a Jupyter notebook on a Linux DSVM, specifically**.</span><span class="sxs-lookup"><span data-stu-id="ea61c-117">**This is for a Jupyter notebook on a Linux DSVM, specifically**.</span></span>  <span data-ttu-id="ea61c-118">These commands access the current Python kernel in the notebook (e.g. the conda `py35` environment)</span><span class="sxs-lookup"><span data-stu-id="ea61c-118">These commands access the current Python kernel in the notebook (e.g. the conda `py35` environment)</span></span>
>```
>import sys
>! {sys.executable} -m azure.cli login
>! {sys.executable} -m azure.cli ml -h
>```

### <a name="installing-or-updating-on-windows"></a><span data-ttu-id="ea61c-119">Installing (or updating) on Windows</span><span class="sxs-lookup"><span data-stu-id="ea61c-119">Installing (or updating) on Windows</span></span>

<span data-ttu-id="ea61c-120">Install Python from https://www.python.org/.</span><span class="sxs-lookup"><span data-stu-id="ea61c-120">Install Python from https://www.python.org/.</span></span> <span data-ttu-id="ea61c-121">Ensure that you have selected to install pip.</span><span class="sxs-lookup"><span data-stu-id="ea61c-121">Ensure that you have selected to install pip.</span></span>

<span data-ttu-id="ea61c-122">Open a command prompt using Run As Administrator and run the following commands:</span><span class="sxs-lookup"><span data-stu-id="ea61c-122">Open a command prompt using Run As Administrator and run the following commands:</span></span>

```cmd
pip install -r https://aka.ms/az-ml-o16n-cli-requirements-file
```

### <a name="installing-or-updating-on-linux"></a><span data-ttu-id="ea61c-123">Installing (or updating) on Linux</span><span class="sxs-lookup"><span data-stu-id="ea61c-123">Installing (or updating) on Linux</span></span>
<span data-ttu-id="ea61c-124">Run the following command from the command line, and follow the prompts:</span><span class="sxs-lookup"><span data-stu-id="ea61c-124">Run the following command from the command line, and follow the prompts:</span></span>

```bash
sudo -i
pip install -r https://aka.ms/az-ml-o16n-cli-requirements-file
```

### <a name="configuring-docker-on-linux"></a><span data-ttu-id="ea61c-125">Configuring Docker on Linux</span><span class="sxs-lookup"><span data-stu-id="ea61c-125">Configuring Docker on Linux</span></span>
<span data-ttu-id="ea61c-126">In order to configure Docker on Linux for use by non-root users, follow the instructions here: [Post-installation steps for Linux](https://docs.docker.com/engine/installation/linux/linux-postinstall/)</span><span class="sxs-lookup"><span data-stu-id="ea61c-126">In order to configure Docker on Linux for use by non-root users, follow the instructions here: [Post-installation steps for Linux](https://docs.docker.com/engine/installation/linux/linux-postinstall/)</span></span>

>[!NOTE]
> <span data-ttu-id="ea61c-127">On a Linux DSVM, you can run the script below to configure Docker correctly.</span><span class="sxs-lookup"><span data-stu-id="ea61c-127">On a Linux DSVM, you can run the script below to configure Docker correctly.</span></span> <span data-ttu-id="ea61c-128">**Remember to log out and log back in after running the script.**</span><span class="sxs-lookup"><span data-stu-id="ea61c-128">**Remember to log out and log back in after running the script.**</span></span>
>```
>sudo /opt/microsoft/azureml/initial_setup.sh
>```

## <a name="deploying-your-model"></a><span data-ttu-id="ea61c-129">Deploying your model</span><span class="sxs-lookup"><span data-stu-id="ea61c-129">Deploying your model</span></span>
<span data-ttu-id="ea61c-130">Use the CLI to deploy models as web services.</span><span class="sxs-lookup"><span data-stu-id="ea61c-130">Use the CLI to deploy models as web services.</span></span> <span data-ttu-id="ea61c-131">The web services can be deployed locally or to a cluster.</span><span class="sxs-lookup"><span data-stu-id="ea61c-131">The web services can be deployed locally or to a cluster.</span></span>

<span data-ttu-id="ea61c-132">Start with a local deployment, validate that your model and code work, then deploy to a cluster for production scale use.</span><span class="sxs-lookup"><span data-stu-id="ea61c-132">Start with a local deployment, validate that your model and code work, then deploy to a cluster for production scale use.</span></span>

<span data-ttu-id="ea61c-133">To start, you need to set up your deployment environment.</span><span class="sxs-lookup"><span data-stu-id="ea61c-133">To start, you need to set up your deployment environment.</span></span> <span data-ttu-id="ea61c-134">The environment setup is a one time task.</span><span class="sxs-lookup"><span data-stu-id="ea61c-134">The environment setup is a one time task.</span></span> <span data-ttu-id="ea61c-135">Once the setup is complete, you can reuse the environment for subsequent deployments.</span><span class="sxs-lookup"><span data-stu-id="ea61c-135">Once the setup is complete, you can reuse the environment for subsequent deployments.</span></span> <span data-ttu-id="ea61c-136">See the following section for more detail.</span><span class="sxs-lookup"><span data-stu-id="ea61c-136">See the following section for more detail.</span></span>

<span data-ttu-id="ea61c-137">When completing the environment setup:</span><span class="sxs-lookup"><span data-stu-id="ea61c-137">When completing the environment setup:</span></span>
- <span data-ttu-id="ea61c-138">You are prompted to sign in to Azure.</span><span class="sxs-lookup"><span data-stu-id="ea61c-138">You are prompted to sign in to Azure.</span></span> <span data-ttu-id="ea61c-139">To sign in, use a web browser to open the page https://aka.ms/devicelogin and enter the provided code to authenticate.</span><span class="sxs-lookup"><span data-stu-id="ea61c-139">To sign in, use a web browser to open the page https://aka.ms/devicelogin and enter the provided code to authenticate.</span></span>
- <span data-ttu-id="ea61c-140">During the authentication process, you are prompted for an account to authenticate with.</span><span class="sxs-lookup"><span data-stu-id="ea61c-140">During the authentication process, you are prompted for an account to authenticate with.</span></span> <span data-ttu-id="ea61c-141">Important: Select an account that has a valid Azure subscription and sufficient permissions to create resources in the account.</span><span class="sxs-lookup"><span data-stu-id="ea61c-141">Important: Select an account that has a valid Azure subscription and sufficient permissions to create resources in the account.</span></span> <span data-ttu-id="ea61c-142">When the log-in is complete, your subscription information is presented and you are prompted whether you wish to continue with the selected account.</span><span class="sxs-lookup"><span data-stu-id="ea61c-142">When the log-in is complete, your subscription information is presented and you are prompted whether you wish to continue with the selected account.</span></span>

### <a name="environment-setup"></a><span data-ttu-id="ea61c-143">Environment Setup</span><span class="sxs-lookup"><span data-stu-id="ea61c-143">Environment Setup</span></span>
<span data-ttu-id="ea61c-144">To start the setup process, you need to register a few environment providers by entering the following commands:</span><span class="sxs-lookup"><span data-stu-id="ea61c-144">To start the setup process, you need to register a few environment providers by entering the following commands:</span></span>

```azurecli
az provider register -n Microsoft.MachineLearningCompute
az provider register -n Microsoft.ContainerRegistry
az provider register -n Microsoft.ContainerService
```
#### <a name="local-deployment"></a><span data-ttu-id="ea61c-145">Local deployment</span><span class="sxs-lookup"><span data-stu-id="ea61c-145">Local deployment</span></span>
<span data-ttu-id="ea61c-146">To deploy and test your web service on the local machine, set up a local environment using the following command.</span><span class="sxs-lookup"><span data-stu-id="ea61c-146">To deploy and test your web service on the local machine, set up a local environment using the following command.</span></span> <span data-ttu-id="ea61c-147">The resource group name is optional.</span><span class="sxs-lookup"><span data-stu-id="ea61c-147">The resource group name is optional.</span></span>

```azurecli
az ml env setup -l [Azure Region, e.g. eastus2] -n [your environment name] [-g [existing resource group]]
```
>[!NOTE] 
><span data-ttu-id="ea61c-148">Local web service deployment requires you to install Docker on the local machine.</span><span class="sxs-lookup"><span data-stu-id="ea61c-148">Local web service deployment requires you to install Docker on the local machine.</span></span> 
>

<span data-ttu-id="ea61c-149">The local environment setup command creates the following resources in your subscription:</span><span class="sxs-lookup"><span data-stu-id="ea61c-149">The local environment setup command creates the following resources in your subscription:</span></span>
- <span data-ttu-id="ea61c-150">A resource group (if not provided, or if the name provided does not exist)</span><span class="sxs-lookup"><span data-stu-id="ea61c-150">A resource group (if not provided, or if the name provided does not exist)</span></span>
- <span data-ttu-id="ea61c-151">A storage account</span><span class="sxs-lookup"><span data-stu-id="ea61c-151">A storage account</span></span>
- <span data-ttu-id="ea61c-152">An Azure Container Registry (ACR)</span><span class="sxs-lookup"><span data-stu-id="ea61c-152">An Azure Container Registry (ACR)</span></span>
- <span data-ttu-id="ea61c-153">An Application insights account</span><span class="sxs-lookup"><span data-stu-id="ea61c-153">An Application insights account</span></span>

<span data-ttu-id="ea61c-154">After setup completes successfully, set the environment to be used using the following command:</span><span class="sxs-lookup"><span data-stu-id="ea61c-154">After setup completes successfully, set the environment to be used using the following command:</span></span>

```azurecli
az ml env set -n [environment name] -g [resource group]
```

#### <a name="cluster-deployment"></a><span data-ttu-id="ea61c-155">Cluster deployment</span><span class="sxs-lookup"><span data-stu-id="ea61c-155">Cluster deployment</span></span>
<span data-ttu-id="ea61c-156">Use Cluster deployment for high-scale production scenarios.</span><span class="sxs-lookup"><span data-stu-id="ea61c-156">Use Cluster deployment for high-scale production scenarios.</span></span> <span data-ttu-id="ea61c-157">It sets up an ACS cluster with Kubernetes as the orchestrator.</span><span class="sxs-lookup"><span data-stu-id="ea61c-157">It sets up an ACS cluster with Kubernetes as the orchestrator.</span></span> <span data-ttu-id="ea61c-158">The ACS cluster can be scaled out to handle larger throughput for your web service calls.</span><span class="sxs-lookup"><span data-stu-id="ea61c-158">The ACS cluster can be scaled out to handle larger throughput for your web service calls.</span></span>

<span data-ttu-id="ea61c-159">To deploy your web service to a production environment, first set up the environment using the following command:</span><span class="sxs-lookup"><span data-stu-id="ea61c-159">To deploy your web service to a production environment, first set up the environment using the following command:</span></span>

```azurecli
az ml env setup --cluster -n [your environment name] -l [Azure region e.g. eastus2] [-g [resource group]]
```

<span data-ttu-id="ea61c-160">The cluster environment setup command creates the following resources in your subscription:</span><span class="sxs-lookup"><span data-stu-id="ea61c-160">The cluster environment setup command creates the following resources in your subscription:</span></span>
- <span data-ttu-id="ea61c-161">A resource group (if not provided, or if the name provided does not exist)</span><span class="sxs-lookup"><span data-stu-id="ea61c-161">A resource group (if not provided, or if the name provided does not exist)</span></span>
- <span data-ttu-id="ea61c-162">A storage account</span><span class="sxs-lookup"><span data-stu-id="ea61c-162">A storage account</span></span>
- <span data-ttu-id="ea61c-163">An Azure Container Registry (ACR)</span><span class="sxs-lookup"><span data-stu-id="ea61c-163">An Azure Container Registry (ACR)</span></span>
- <span data-ttu-id="ea61c-164">A Kubernetes deployment on an Azure Container Service (ACS) cluster</span><span class="sxs-lookup"><span data-stu-id="ea61c-164">A Kubernetes deployment on an Azure Container Service (ACS) cluster</span></span>
- <span data-ttu-id="ea61c-165">An Application insights account</span><span class="sxs-lookup"><span data-stu-id="ea61c-165">An Application insights account</span></span>

>[!IMPORTANT]
> <span data-ttu-id="ea61c-166">In order to successfully create a cluster environment, you will need to be have contributor access on the Azure subscription or the resource group.</span><span class="sxs-lookup"><span data-stu-id="ea61c-166">In order to successfully create a cluster environment, you will need to be have contributor access on the Azure subscription or the resource group.</span></span>

<span data-ttu-id="ea61c-167">The resource group, storage account, and ACR are created quickly.</span><span class="sxs-lookup"><span data-stu-id="ea61c-167">The resource group, storage account, and ACR are created quickly.</span></span> <span data-ttu-id="ea61c-168">The ACS deployment can take up to 20 minutes.</span><span class="sxs-lookup"><span data-stu-id="ea61c-168">The ACS deployment can take up to 20 minutes.</span></span> 

<span data-ttu-id="ea61c-169">To check the status of an ongoing cluster provisioning, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ea61c-169">To check the status of an ongoing cluster provisioning, use the following command:</span></span>

```azurecli
az ml env show -n [environment name] -g [resource group]
```

<span data-ttu-id="ea61c-170">After setup is complete, you need to set the environment to be used for this deployment.</span><span class="sxs-lookup"><span data-stu-id="ea61c-170">After setup is complete, you need to set the environment to be used for this deployment.</span></span> <span data-ttu-id="ea61c-171">Use the following command:</span><span class="sxs-lookup"><span data-stu-id="ea61c-171">Use the following command:</span></span>

```azurecli
az ml env set -n [environment name] -g [resource group]
```

>[!NOTE] 
> <span data-ttu-id="ea61c-172">After the environment is created, for subsequent deployments, you only need to use the set command above to reuse it.</span><span class="sxs-lookup"><span data-stu-id="ea61c-172">After the environment is created, for subsequent deployments, you only need to use the set command above to reuse it.</span></span>
>

### <a name="create-a-model-management-account"></a><span data-ttu-id="ea61c-173">Create a Model Management Account</span><span class="sxs-lookup"><span data-stu-id="ea61c-173">Create a Model Management Account</span></span>
<span data-ttu-id="ea61c-174">A model management account is required for deploying models.</span><span class="sxs-lookup"><span data-stu-id="ea61c-174">A model management account is required for deploying models.</span></span> <span data-ttu-id="ea61c-175">You need to do this once per subscription, and can reuse the same account in multiple deployments.</span><span class="sxs-lookup"><span data-stu-id="ea61c-175">You need to do this once per subscription, and can reuse the same account in multiple deployments.</span></span>

<span data-ttu-id="ea61c-176">To create a new account, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ea61c-176">To create a new account, use the following command:</span></span>

```azurecli
az ml account modelmanagement create -l [Azure region, e.g. eastus2] -n [your account name] -g [resource group name] --sku-instances [number of instances, e.g. 1] --sku-name [Pricing tier for example S1]
```

<span data-ttu-id="ea61c-177">To use an existing account, use the following command:</span><span class="sxs-lookup"><span data-stu-id="ea61c-177">To use an existing account, use the following command:</span></span>
```azurecli
az ml account modelmanagement set -n [your account name] -g [resource group it was created in]
```

<span data-ttu-id="ea61c-178">As a result of this process, the environment is ready and the model management account has been created to provide the features needed to manage and deploy Machine Learning models (see [Azure Machine Learning Model Management](model-management-overview.md) for an overview).</span><span class="sxs-lookup"><span data-stu-id="ea61c-178">As a result of this process, the environment is ready and the model management account has been created to provide the features needed to manage and deploy Machine Learning models (see [Azure Machine Learning Model Management](model-management-overview.md) for an overview).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ea61c-179">Next steps</span><span class="sxs-lookup"><span data-stu-id="ea61c-179">Next steps</span></span>

* <span data-ttu-id="ea61c-180">For instructions on how to deploy web services to run on a local machine or a cluster continue on to [Deploying a Machine Learning Model as a Web Service](model-management-service-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="ea61c-180">For instructions on how to deploy web services to run on a local machine or a cluster continue on to [Deploying a Machine Learning Model as a Web Service](model-management-service-deploy.md).</span></span>
* <span data-ttu-id="ea61c-181">Try one of the many samples in the Gallery.</span><span class="sxs-lookup"><span data-stu-id="ea61c-181">Try one of the many samples in the Gallery.</span></span>
