---
title: Install and use the CLI for top tasks - Azure Machine Learning
description: Learn how to install and use the CLI for the most common machine learning tasks in Azure Machine Learning.
services: machine-learning
author: haining
ms.author: haining
manager: cgronlun
ms.reviewer: mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.topic: conceptual
ms.date: 03/10/2018
ms.openlocfilehash: 15b716163a98325a96d6ce1619abe6569a4f8a0a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871041"
---
# <a name="install-and-use-the-machine-learning-cli-for-top-tasks-in-azure-machine-learning"></a><span data-ttu-id="d9e67-103">Install and use the machine learning CLI for top tasks in Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d9e67-103">Install and use the machine learning CLI for top tasks in Azure Machine Learning</span></span>

<span data-ttu-id="d9e67-104">Azure Machine Learning services are an integrated, end-to-end data science and advanced analytics solution.</span><span class="sxs-lookup"><span data-stu-id="d9e67-104">Azure Machine Learning services are an integrated, end-to-end data science and advanced analytics solution.</span></span> <span data-ttu-id="d9e67-105">Professional data scientists can use Azure Machine Learning services to prepare data, develop experiments, and deploy models at cloud scale.</span><span class="sxs-lookup"><span data-stu-id="d9e67-105">Professional data scientists can use Azure Machine Learning services to prepare data, develop experiments, and deploy models at cloud scale.</span></span> 

<span data-ttu-id="d9e67-106">Azure Machine Learning provides a command-line interface (CLI) with which you can:</span><span class="sxs-lookup"><span data-stu-id="d9e67-106">Azure Machine Learning provides a command-line interface (CLI) with which you can:</span></span>
+ <span data-ttu-id="d9e67-107">Manage your workspace and projects</span><span class="sxs-lookup"><span data-stu-id="d9e67-107">Manage your workspace and projects</span></span>
+ <span data-ttu-id="d9e67-108">Set up compute targets</span><span class="sxs-lookup"><span data-stu-id="d9e67-108">Set up compute targets</span></span>
+ <span data-ttu-id="d9e67-109">Run training experiments</span><span class="sxs-lookup"><span data-stu-id="d9e67-109">Run training experiments</span></span>
+ <span data-ttu-id="d9e67-110">View history and metrics for past runs</span><span class="sxs-lookup"><span data-stu-id="d9e67-110">View history and metrics for past runs</span></span>
+ <span data-ttu-id="d9e67-111">Deploy models into production as web services</span><span class="sxs-lookup"><span data-stu-id="d9e67-111">Deploy models into production as web services</span></span>
+ <span data-ttu-id="d9e67-112">Manage production models and services</span><span class="sxs-lookup"><span data-stu-id="d9e67-112">Manage production models and services</span></span>

<span data-ttu-id="d9e67-113">This article presents some of the most useful CLI commands for your convenience.</span><span class="sxs-lookup"><span data-stu-id="d9e67-113">This article presents some of the most useful CLI commands for your convenience.</span></span> 

![Azure Machine Learning CLI](media/cli-for-azure-machine-learning/flow.png)

## <a name="what-you-need-to-get-started"></a><span data-ttu-id="d9e67-115">What you need to get started</span><span class="sxs-lookup"><span data-stu-id="d9e67-115">What you need to get started</span></span>

<span data-ttu-id="d9e67-116">You need contributer access to an Azure subscription or a resource group where you can deploy your models.</span><span class="sxs-lookup"><span data-stu-id="d9e67-116">You need contributer access to an Azure subscription or a resource group where you can deploy your models.</span></span> <span data-ttu-id="d9e67-117">Also, you need to install Azure Machine Learning Workbench in order to run the CLI.</span><span class="sxs-lookup"><span data-stu-id="d9e67-117">Also, you need to install Azure Machine Learning Workbench in order to run the CLI.</span></span> 

>[!IMPORTANT]
><span data-ttu-id="d9e67-118">The CLI delivered with Azure Machine Learning services is different from the [Azure CLI](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest), which is used for managing Azure resources.</span><span class="sxs-lookup"><span data-stu-id="d9e67-118">The CLI delivered with Azure Machine Learning services is different from the [Azure CLI](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest), which is used for managing Azure resources.</span></span>

## <a name="get-and-start-cli"></a><span data-ttu-id="d9e67-119">Get and start CLI</span><span class="sxs-lookup"><span data-stu-id="d9e67-119">Get and start CLI</span></span>

<span data-ttu-id="d9e67-120">To get this CLI, install Azure Machine Learning Workbench, which can be downloaded from here:</span><span class="sxs-lookup"><span data-stu-id="d9e67-120">To get this CLI, install Azure Machine Learning Workbench, which can be downloaded from here:</span></span>
    + <span data-ttu-id="d9e67-121">Windows - https://aka.ms/azureml-wb-msi</span><span class="sxs-lookup"><span data-stu-id="d9e67-121">Windows - https://aka.ms/azureml-wb-msi</span></span> 
    + <span data-ttu-id="d9e67-122">MacOS - https://aka.ms/azureml-wb-dmg</span><span class="sxs-lookup"><span data-stu-id="d9e67-122">MacOS - https://aka.ms/azureml-wb-dmg</span></span> 

<span data-ttu-id="d9e67-123">To start the CLI:</span><span class="sxs-lookup"><span data-stu-id="d9e67-123">To start the CLI:</span></span>
+ <span data-ttu-id="d9e67-124">In Azure Machine Learning Workbench, launch the CLI from the menu **File -> Open Command Prompt.**</span><span class="sxs-lookup"><span data-stu-id="d9e67-124">In Azure Machine Learning Workbench, launch the CLI from the menu **File -> Open Command Prompt.**</span></span>

## <a name="get-command-help"></a><span data-ttu-id="d9e67-125">Get command help</span><span class="sxs-lookup"><span data-stu-id="d9e67-125">Get command help</span></span> 

<span data-ttu-id="d9e67-126">You can get extra information about CLI commands using `--debug` or `--help` after the commands such as `az ml <xyz> --debug` where `<xyz>` is the command name.</span><span class="sxs-lookup"><span data-stu-id="d9e67-126">You can get extra information about CLI commands using `--debug` or `--help` after the commands such as `az ml <xyz> --debug` where `<xyz>` is the command name.</span></span> <span data-ttu-id="d9e67-127">For example:</span><span class="sxs-lookup"><span data-stu-id="d9e67-127">For example:</span></span>
```azurecli
az ml computetarget --debug 

az ml experiment --help
```

## <a name="common-cli-tasks-for-azure-machine-learning"></a><span data-ttu-id="d9e67-128">Common CLI tasks for Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d9e67-128">Common CLI tasks for Azure Machine Learning</span></span> 

<span data-ttu-id="d9e67-129">Learn about the most common tasks you can perform with the CLI in this section, including:</span><span class="sxs-lookup"><span data-stu-id="d9e67-129">Learn about the most common tasks you can perform with the CLI in this section, including:</span></span>
+ [<span data-ttu-id="d9e67-130">Setting up compute targets</span><span class="sxs-lookup"><span data-stu-id="d9e67-130">Setting up compute targets</span></span>](#target)
+ [<span data-ttu-id="d9e67-131">Submitting jobs for remote execution</span><span class="sxs-lookup"><span data-stu-id="d9e67-131">Submitting jobs for remote execution</span></span>](#jobs)
+ [<span data-ttu-id="d9e67-132">Working with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="d9e67-132">Working with Jupyter notebooks</span></span>](#jupyter)
+ [<span data-ttu-id="d9e67-133">Interacting with run histories</span><span class="sxs-lookup"><span data-stu-id="d9e67-133">Interacting with run histories</span></span>](#history)
+ [<span data-ttu-id="d9e67-134">Configuring your environment to operationalize</span><span class="sxs-lookup"><span data-stu-id="d9e67-134">Configuring your environment to operationalize</span></span>](#o16n)

<a name="target"></a>

### <a name="set-up-a-compute-target"></a><span data-ttu-id="d9e67-135">Set up a compute target</span><span class="sxs-lookup"><span data-stu-id="d9e67-135">Set up a compute target</span></span>

<span data-ttu-id="d9e67-136">You can compute your machine learning model in different targets, including:</span><span class="sxs-lookup"><span data-stu-id="d9e67-136">You can compute your machine learning model in different targets, including:</span></span>
+ <span data-ttu-id="d9e67-137">in local mode</span><span class="sxs-lookup"><span data-stu-id="d9e67-137">in local mode</span></span>
+ <span data-ttu-id="d9e67-138">in a Data Science VM (DSVM)</span><span class="sxs-lookup"><span data-stu-id="d9e67-138">in a Data Science VM (DSVM)</span></span>
+ <span data-ttu-id="d9e67-139">on an HDInsight cluster</span><span class="sxs-lookup"><span data-stu-id="d9e67-139">on an HDInsight cluster</span></span>

<span data-ttu-id="d9e67-140">To attach a Data Science VM target:</span><span class="sxs-lookup"><span data-stu-id="d9e67-140">To attach a Data Science VM target:</span></span>
```azurecli
az ml computetarget attach remotedocker -n <target name> -a <ip address or FQDN> -u <username> -w <password>
``` 

<span data-ttu-id="d9e67-141">To attach an HDInsight target:</span><span class="sxs-lookup"><span data-stu-id="d9e67-141">To attach an HDInsight target:</span></span>
```azurecli
az ml computetarget attach cluster -n <target name> -a <cluster name, e.g. myhdicluster-ssh.azurehdinsight.net> -u <ssh username> -w <ssh password>
```

<span data-ttu-id="d9e67-142">Within the **aml_config** folder, you can change the conda dependencies.</span><span class="sxs-lookup"><span data-stu-id="d9e67-142">Within the **aml_config** folder, you can change the conda dependencies.</span></span> 

<span data-ttu-id="d9e67-143">Also, you can operate with PySpark, Python, or Python in a GPU DSVM.</span><span class="sxs-lookup"><span data-stu-id="d9e67-143">Also, you can operate with PySpark, Python, or Python in a GPU DSVM.</span></span> 

<span data-ttu-id="d9e67-144">To define the Python operation mode:</span><span class="sxs-lookup"><span data-stu-id="d9e67-144">To define the Python operation mode:</span></span>
+ <span data-ttu-id="d9e67-145">For Python, add `Framework:Python` in `<target name>.runconfig`</span><span class="sxs-lookup"><span data-stu-id="d9e67-145">For Python, add `Framework:Python` in `<target name>.runconfig`</span></span> 

+ <span data-ttu-id="d9e67-146">For PySpark, add `Framework:PySpark` in `<target name>.runconfig`</span><span class="sxs-lookup"><span data-stu-id="d9e67-146">For PySpark, add `Framework:PySpark` in `<target name>.runconfig`</span></span> 

+ <span data-ttu-id="d9e67-147">For Python in a GPU DSVM,</span><span class="sxs-lookup"><span data-stu-id="d9e67-147">For Python in a GPU DSVM,</span></span>
    1. <span data-ttu-id="d9e67-148">Add `Framework:Python` in `<target name>.runconfig`</span><span class="sxs-lookup"><span data-stu-id="d9e67-148">Add `Framework:Python` in `<target name>.runconfig`</span></span> 

    1. <span data-ttu-id="d9e67-149">Also, add `baseDockerImage: microsoft/mmlspark:plus-gpu-0.9.9 and nvidiaDocker:true` in `<target name>.compute`</span><span class="sxs-lookup"><span data-stu-id="d9e67-149">Also, add `baseDockerImage: microsoft/mmlspark:plus-gpu-0.9.9 and nvidiaDocker:true` in `<target name>.compute`</span></span>

<span data-ttu-id="d9e67-150">To prepare the compute target:</span><span class="sxs-lookup"><span data-stu-id="d9e67-150">To prepare the compute target:</span></span>
```azurecli
az ml experiment prepare -c <target name>
```

>[!TIP]
><span data-ttu-id="d9e67-151">To show your subscription:</span><span class="sxs-lookup"><span data-stu-id="d9e67-151">To show your subscription:</span></span><br/>
>`az account show`<br/>
>
><span data-ttu-id="d9e67-152">To set your subscription:</span><span class="sxs-lookup"><span data-stu-id="d9e67-152">To set your subscription:</span></span><br/>
>`az account set –s "my subscription name" `

<a name="jobs"></a>

### <a name="submit-remote-jobs"></a><span data-ttu-id="d9e67-153">Submit remote jobs</span><span class="sxs-lookup"><span data-stu-id="d9e67-153">Submit remote jobs</span></span>

<span data-ttu-id="d9e67-154">To submit a job to a remote target:</span><span class="sxs-lookup"><span data-stu-id="d9e67-154">To submit a job to a remote target:</span></span>
```azurecli
az ml experiment submit -c <target name> myscript.py
```

<a name="jupyter"></a>

### <a name="work-with-jupyter-notebooks"></a><span data-ttu-id="d9e67-155">Work with Jupyter notebooks</span><span class="sxs-lookup"><span data-stu-id="d9e67-155">Work with Jupyter notebooks</span></span>

<span data-ttu-id="d9e67-156">To start a Jupyter notebook:</span><span class="sxs-lookup"><span data-stu-id="d9e67-156">To start a Jupyter notebook:</span></span>
```azurecli
az ml notebook start
```

<span data-ttu-id="d9e67-157">This command starts a Jupyter notebook in localhost.</span><span class="sxs-lookup"><span data-stu-id="d9e67-157">This command starts a Jupyter notebook in localhost.</span></span> <span data-ttu-id="d9e67-158">You can work in local by selecting the kernel Python 3, or work in your remote VM by selecting the kernel `<target name>`.</span><span class="sxs-lookup"><span data-stu-id="d9e67-158">You can work in local by selecting the kernel Python 3, or work in your remote VM by selecting the kernel `<target name>`.</span></span>

<a name="history"></a>

### <a name="interact-with-and-explore-the-run-history"></a><span data-ttu-id="d9e67-159">Interact with and explore the run history</span><span class="sxs-lookup"><span data-stu-id="d9e67-159">Interact with and explore the run history</span></span>

<span data-ttu-id="d9e67-160">To list the run history:</span><span class="sxs-lookup"><span data-stu-id="d9e67-160">To list the run history:</span></span>
```azurecli
az ml history list -o table
```

<span data-ttu-id="d9e67-161">To list all completed runs:</span><span class="sxs-lookup"><span data-stu-id="d9e67-161">To list all completed runs:</span></span>
```azurecli
az ml history list --query "[?status=='Completed']" -o table
```

<span data-ttu-id="d9e67-162">To find runs with the best accuracy:</span><span class="sxs-lookup"><span data-stu-id="d9e67-162">To find runs with the best accuracy:</span></span>
```azurecli
az ml history list --query "@[?Accuracy != null] | max_by(@, &Accuracy).Accuracy"
```

<span data-ttu-id="d9e67-163">You can also download the files generated by each run.</span><span class="sxs-lookup"><span data-stu-id="d9e67-163">You can also download the files generated by each run.</span></span> 

<span data-ttu-id="d9e67-164">To promote a model that is saved in the folder outputs:</span><span class="sxs-lookup"><span data-stu-id="d9e67-164">To promote a model that is saved in the folder outputs:</span></span>
```azurecli
az ml history promote -r <run id> -ap outputs/model.pkl -n <model name>
```

<span data-ttu-id="d9e67-165">To download that model:</span><span class="sxs-lookup"><span data-stu-id="d9e67-165">To download that model:</span></span>
```azurecli
az ml asset download -l assets/model.pkl.link -d <model folder path>
```

<a name="o16n"></a>

### <a name="configure-your-environment-to-operationalize"></a><span data-ttu-id="d9e67-166">Configure your environment to operationalize</span><span class="sxs-lookup"><span data-stu-id="d9e67-166">Configure your environment to operationalize</span></span>

<span data-ttu-id="d9e67-167">To set up your operationalization environment, you must create:</span><span class="sxs-lookup"><span data-stu-id="d9e67-167">To set up your operationalization environment, you must create:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d9e67-168">A resource group</span><span class="sxs-lookup"><span data-stu-id="d9e67-168">A resource group</span></span> 
> * <span data-ttu-id="d9e67-169">A storage account</span><span class="sxs-lookup"><span data-stu-id="d9e67-169">A storage account</span></span>
> * <span data-ttu-id="d9e67-170">An Azure Container Registry (ACR)</span><span class="sxs-lookup"><span data-stu-id="d9e67-170">An Azure Container Registry (ACR)</span></span>
> * <span data-ttu-id="d9e67-171">An Application insight account</span><span class="sxs-lookup"><span data-stu-id="d9e67-171">An Application insight account</span></span>
> * <span data-ttu-id="d9e67-172">A Kubernetes deployment on an Azure Container Service (ACS) cluster</span><span class="sxs-lookup"><span data-stu-id="d9e67-172">A Kubernetes deployment on an Azure Container Service (ACS) cluster</span></span>


<span data-ttu-id="d9e67-173">To set up a local deployment for testing in a Docker container:</span><span class="sxs-lookup"><span data-stu-id="d9e67-173">To set up a local deployment for testing in a Docker container:</span></span>
```azurecli
az ml env setup -l <region, e.g. eastus2> -n <env name> -g <resource group name>
```

<span data-ttu-id="d9e67-174">To set up an ACS cluster with Kubernetes:</span><span class="sxs-lookup"><span data-stu-id="d9e67-174">To set up an ACS cluster with Kubernetes:</span></span>
```azurecli
az ml env setup -l <region, e.g. eastus2> -n <env name> -g <resource group name> --cluster
```

<span data-ttu-id="d9e67-175">To monitor the status of the deployment:</span><span class="sxs-lookup"><span data-stu-id="d9e67-175">To monitor the status of the deployment:</span></span>
```azurecli
az ml env show -n <environment name> -g <resource group name>
```

<span data-ttu-id="d9e67-176">To set the environment that should be used:</span><span class="sxs-lookup"><span data-stu-id="d9e67-176">To set the environment that should be used:</span></span>
```azurecli
az ml env set -n <environment name> -g <resource group name>
```

## <a name="next-steps"></a><span data-ttu-id="d9e67-177">Next steps</span><span class="sxs-lookup"><span data-stu-id="d9e67-177">Next steps</span></span>

<span data-ttu-id="d9e67-178">Get started with one of these articles:</span><span class="sxs-lookup"><span data-stu-id="d9e67-178">Get started with one of these articles:</span></span> 
+ [<span data-ttu-id="d9e67-179">Install and start using Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="d9e67-179">Install and start using Azure Machine Learning</span></span>](../service/quickstart-installation.md)
+ [<span data-ttu-id="d9e67-180">Classifying Iris Data Tutorial: Part 1</span><span class="sxs-lookup"><span data-stu-id="d9e67-180">Classifying Iris Data Tutorial: Part 1</span></span>](tutorial-classifying-iris-part-1.md)

<span data-ttu-id="d9e67-181">Dig deeper with one of these articles:</span><span class="sxs-lookup"><span data-stu-id="d9e67-181">Dig deeper with one of these articles:</span></span>
+ [<span data-ttu-id="d9e67-182">CLI commands for managing models</span><span class="sxs-lookup"><span data-stu-id="d9e67-182">CLI commands for managing models</span></span>](model-management-cli-reference.md)
