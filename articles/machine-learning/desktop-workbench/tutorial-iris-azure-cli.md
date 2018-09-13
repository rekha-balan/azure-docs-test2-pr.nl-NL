---
title: Tutorial article for Azure Machine Learning preview features - Command Line Interface  | Microsoft Docs
description: This tutorial walk through all the steps required to complete an Iris classification end-to-end from the command line interface.
services: machine-learning
author: jpe316
ms.author: jordane
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc, tutorial
ms.topic: tutorial
ms.date: 10/15/2017
ms.openlocfilehash: 97088b8e56f4c04833a1023fe3060d832eed27f9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870613"
---
# <a name="tutorial-classifying-iris-using-the-command-line-interface"></a><span data-ttu-id="71949-103">Tutorial: Classifying Iris using the command-line interface</span><span class="sxs-lookup"><span data-stu-id="71949-103">Tutorial: Classifying Iris using the command-line interface</span></span>
<span data-ttu-id="71949-104">Azure Machine Learning services (preview) are an integrated, end-to-end data science and advanced analytics solution for professional data scientists to prepare data, develop experiments and deploy models at cloud scale.</span><span class="sxs-lookup"><span data-stu-id="71949-104">Azure Machine Learning services (preview) are an integrated, end-to-end data science and advanced analytics solution for professional data scientists to prepare data, develop experiments and deploy models at cloud scale.</span></span>

<span data-ttu-id="71949-105">In this tutorial, you learn to use the command-line interface (CLI) tools in Azure Machine Learning preview features to:</span><span class="sxs-lookup"><span data-stu-id="71949-105">In this tutorial, you learn to use the command-line interface (CLI) tools in Azure Machine Learning preview features to:</span></span> 
> [!div class="checklist"]
> * <span data-ttu-id="71949-106">Set up an Experimentation account and create a workspace</span><span class="sxs-lookup"><span data-stu-id="71949-106">Set up an Experimentation account and create a workspace</span></span>
> * <span data-ttu-id="71949-107">Create a project</span><span class="sxs-lookup"><span data-stu-id="71949-107">Create a project</span></span>
> * <span data-ttu-id="71949-108">Submit an experiment to multiple compute targets</span><span class="sxs-lookup"><span data-stu-id="71949-108">Submit an experiment to multiple compute targets</span></span>
> * <span data-ttu-id="71949-109">Promote and register a trained model</span><span class="sxs-lookup"><span data-stu-id="71949-109">Promote and register a trained model</span></span>
> * <span data-ttu-id="71949-110">Deploy a web service to score new data</span><span class="sxs-lookup"><span data-stu-id="71949-110">Deploy a web service to score new data</span></span>

## <a name="prerequisites"></a><span data-ttu-id="71949-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="71949-111">Prerequisites</span></span>
<span data-ttu-id="71949-112">To complete this tutorial, you need:</span><span class="sxs-lookup"><span data-stu-id="71949-112">To complete this tutorial, you need:</span></span>
- <span data-ttu-id="71949-113">Access to an Azure subscription and permissions to create resources in that subscription.</span><span class="sxs-lookup"><span data-stu-id="71949-113">Access to an Azure subscription and permissions to create resources in that subscription.</span></span> 
  
  <span data-ttu-id="71949-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span><span class="sxs-lookup"><span data-stu-id="71949-114">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

- <span data-ttu-id="71949-115">Azure Machine Learning Workbench application installed as described in [Quickstart: Install and start Azure Machine Learning services](../service/quickstart-installation.md).</span><span class="sxs-lookup"><span data-stu-id="71949-115">Azure Machine Learning Workbench application installed as described in [Quickstart: Install and start Azure Machine Learning services](../service/quickstart-installation.md).</span></span> 

  >[!IMPORTANT]
  ><span data-ttu-id="71949-116">Do not create the Azure Machine Learning service accounts since you will do that using the CLI in this article.</span><span class="sxs-lookup"><span data-stu-id="71949-116">Do not create the Azure Machine Learning service accounts since you will do that using the CLI in this article.</span></span>
 
## <a name="getting-started"></a><span data-ttu-id="71949-117">Getting started</span><span class="sxs-lookup"><span data-stu-id="71949-117">Getting started</span></span>
<span data-ttu-id="71949-118">Azure Machine Learning command-line interface (CLI) allows you to perform all tasks required for an end-to-end data science workflow.</span><span class="sxs-lookup"><span data-stu-id="71949-118">Azure Machine Learning command-line interface (CLI) allows you to perform all tasks required for an end-to-end data science workflow.</span></span> <span data-ttu-id="71949-119">You can access the CLI tools in the following ways:</span><span class="sxs-lookup"><span data-stu-id="71949-119">You can access the CLI tools in the following ways:</span></span>

### <a name="option-1-launch-azure-ml-cli-from-azure-ml-workbench-log-in-dialog-box"></a><span data-ttu-id="71949-120">Option 1.</span><span class="sxs-lookup"><span data-stu-id="71949-120">Option 1.</span></span> <span data-ttu-id="71949-121">launch Azure ML CLI from Azure ML Workbench log-in dialog box</span><span class="sxs-lookup"><span data-stu-id="71949-121">launch Azure ML CLI from Azure ML Workbench log-in dialog box</span></span>
<span data-ttu-id="71949-122">When you launch Azure ML Workbench and log in for the first time, and if you don't have access to an Experimentation Account already, you are presented with the following screen:</span><span class="sxs-lookup"><span data-stu-id="71949-122">When you launch Azure ML Workbench and log in for the first time, and if you don't have access to an Experimentation Account already, you are presented with the following screen:</span></span>

![no account found](media/tutorial-iris-azure-cli/no_account_found.png)

<span data-ttu-id="71949-124">Click on the **Command Line Window** link in the dialog box to launch the command-line window.</span><span class="sxs-lookup"><span data-stu-id="71949-124">Click on the **Command Line Window** link in the dialog box to launch the command-line window.</span></span>

### <a name="option-2-launch-azure-ml-cli-from-azure-ml-workbench-app"></a><span data-ttu-id="71949-125">Option 2.</span><span class="sxs-lookup"><span data-stu-id="71949-125">Option 2.</span></span> <span data-ttu-id="71949-126">launch Azure ML CLI from Azure ML Workbench app</span><span class="sxs-lookup"><span data-stu-id="71949-126">launch Azure ML CLI from Azure ML Workbench app</span></span>
<span data-ttu-id="71949-127">If you already have access to an Experimentation Account, you can log in successfully.</span><span class="sxs-lookup"><span data-stu-id="71949-127">If you already have access to an Experimentation Account, you can log in successfully.</span></span> <span data-ttu-id="71949-128">And you can then open the command-line window by clicking on **File** --> **Open Command Prompt** menu.</span><span class="sxs-lookup"><span data-stu-id="71949-128">And you can then open the command-line window by clicking on **File** --> **Open Command Prompt** menu.</span></span>

### <a name="option-3-enable-azure-ml-cli-in-an-arbitrary-command-line-window"></a><span data-ttu-id="71949-129">Option 3.</span><span class="sxs-lookup"><span data-stu-id="71949-129">Option 3.</span></span> <span data-ttu-id="71949-130">enable Azure ML CLI in an arbitrary command-line window</span><span class="sxs-lookup"><span data-stu-id="71949-130">enable Azure ML CLI in an arbitrary command-line window</span></span>
<span data-ttu-id="71949-131">You can also enable Azure ML CLI in any command-line window.</span><span class="sxs-lookup"><span data-stu-id="71949-131">You can also enable Azure ML CLI in any command-line window.</span></span> <span data-ttu-id="71949-132">Do so by launching a command window, and enter the following commands:</span><span class="sxs-lookup"><span data-stu-id="71949-132">Do so by launching a command window, and enter the following commands:</span></span>

```sh
# Windows Command Prompt
set PATH=%LOCALAPPDATA%\amlworkbench\Python;%LOCALAPPDATA%\amlworkbench\Python\Scripts;%PATH%

# Windows PowerShell
$env:Path = $env:LOCALAPPDATA+"\amlworkbench\Python;"+$env:LOCALAPPDATA+"\amlworkbench\Python\Scripts;"+$env:Path

# macOS Bash Shell
PATH=$HOME/Library/Caches/AmlWorkbench/Python/bin:$PATH
```
<span data-ttu-id="71949-133">To make the change permanent, you can use `SETX` on Windows.</span><span class="sxs-lookup"><span data-stu-id="71949-133">To make the change permanent, you can use `SETX` on Windows.</span></span> <span data-ttu-id="71949-134">For macOS, you can use `setenv`.</span><span class="sxs-lookup"><span data-stu-id="71949-134">For macOS, you can use `setenv`.</span></span>

>[!TIP]
><span data-ttu-id="71949-135">You can enable Azure CLI in your favorite terminal window by setting the preceding environment variables.</span><span class="sxs-lookup"><span data-stu-id="71949-135">You can enable Azure CLI in your favorite terminal window by setting the preceding environment variables.</span></span>

## <a name="step-1-log-in-to-azure"></a><span data-ttu-id="71949-136">Step 1.</span><span class="sxs-lookup"><span data-stu-id="71949-136">Step 1.</span></span> <span data-ttu-id="71949-137">Log in to Azure</span><span class="sxs-lookup"><span data-stu-id="71949-137">Log in to Azure</span></span>
<span data-ttu-id="71949-138">The first step is to open the CLI from the AMLWorkbench App (File > Open Command Prompt).</span><span class="sxs-lookup"><span data-stu-id="71949-138">The first step is to open the CLI from the AMLWorkbench App (File > Open Command Prompt).</span></span> <span data-ttu-id="71949-139">Doing so ensures that you have the correct python environment and that the ML CLI commands are available.</span><span class="sxs-lookup"><span data-stu-id="71949-139">Doing so ensures that you have the correct python environment and that the ML CLI commands are available.</span></span> 

<span data-ttu-id="71949-140">Now, you can set the right context in your CLI to access and manage Azure resources.</span><span class="sxs-lookup"><span data-stu-id="71949-140">Now, you can set the right context in your CLI to access and manage Azure resources.</span></span>
 
```azure-cli
# log in
$ az login

# list all subscriptions
$ az account list -o table

# set the current subscription
$ az account set -s <subscription id or name>
```

## <a name="step-2-create-a-new-azure-machine-learning-experimentation-account-and-workspace"></a><span data-ttu-id="71949-141">Step 2.</span><span class="sxs-lookup"><span data-stu-id="71949-141">Step 2.</span></span> <span data-ttu-id="71949-142">Create a new Azure Machine Learning Experimentation Account and Workspace</span><span class="sxs-lookup"><span data-stu-id="71949-142">Create a new Azure Machine Learning Experimentation Account and Workspace</span></span>

<span data-ttu-id="71949-143">In this step, you create a new Experimentation account and a new workspace.</span><span class="sxs-lookup"><span data-stu-id="71949-143">In this step, you create a new Experimentation account and a new workspace.</span></span> <span data-ttu-id="71949-144">See [Azure Machine Learning concepts](overview-general-concepts.md) for more details about experimentation accounts and workspaces.</span><span class="sxs-lookup"><span data-stu-id="71949-144">See [Azure Machine Learning concepts](overview-general-concepts.md) for more details about experimentation accounts and workspaces.</span></span>

> [!NOTE]
> <span data-ttu-id="71949-145">Experimentation accounts require a storage account, which is used to store the outputs of your experiment runs.</span><span class="sxs-lookup"><span data-stu-id="71949-145">Experimentation accounts require a storage account, which is used to store the outputs of your experiment runs.</span></span> <span data-ttu-id="71949-146">The storage account name has to be globally unique in Azure because there is an url associated with it.</span><span class="sxs-lookup"><span data-stu-id="71949-146">The storage account name has to be globally unique in Azure because there is an url associated with it.</span></span> <span data-ttu-id="71949-147">If you don't specify an existing storage account, your experimentation account name is used to create a new storage account.</span><span class="sxs-lookup"><span data-stu-id="71949-147">If you don't specify an existing storage account, your experimentation account name is used to create a new storage account.</span></span> <span data-ttu-id="71949-148">Make sure to use a unique name, or you will get an error such as _"The storage account named \<storage_account_name> is already taken."_</span><span class="sxs-lookup"><span data-stu-id="71949-148">Make sure to use a unique name, or you will get an error such as _"The storage account named \<storage_account_name> is already taken."_</span></span> <span data-ttu-id="71949-149">Alternatively, you can use the `--storage` argument to supply an existing storage account.</span><span class="sxs-lookup"><span data-stu-id="71949-149">Alternatively, you can use the `--storage` argument to supply an existing storage account.</span></span>

```azure-cli
# create a resource group 
$ az group create --name <resource group name> --location <supported Azure region>

# create a new experimentation account with a new storage account
$ az ml account experimentation create --name <experimentation account name> --resource-group <resource group name>

# create a new experimentation account with an existing storage account
$ az ml account experimentation create --name <experimentation account name>  --resource-group <resource group name> --storage <storage account Azure Resource ID>

# create a workspace in the experimentation account
az ml workspace create --name <workspace name> --account <experimentation account name> --resource-group <resource group name>
```

## <a name="step-2a-optional-share-a-workspace-with-co-worker"></a><span data-ttu-id="71949-150">Step 2.a (optional) Share a workspace with co-worker</span><span class="sxs-lookup"><span data-stu-id="71949-150">Step 2.a (optional) Share a workspace with co-worker</span></span>
<span data-ttu-id="71949-151">Here you can explore how to share access to a workspace with a co-worker.</span><span class="sxs-lookup"><span data-stu-id="71949-151">Here you can explore how to share access to a workspace with a co-worker.</span></span> <span data-ttu-id="71949-152">The steps to share access to an experimentation account or to a project would be the same.</span><span class="sxs-lookup"><span data-stu-id="71949-152">The steps to share access to an experimentation account or to a project would be the same.</span></span> <span data-ttu-id="71949-153">Only the way of getting the Azure Resource ID would need to be updated.</span><span class="sxs-lookup"><span data-stu-id="71949-153">Only the way of getting the Azure Resource ID would need to be updated.</span></span>

```azure-cli
# find the workspace Azure Resource ID
$az ml workspace show --name <workspace name> --account <experimentation account name> --resource-group <resource group name>

# add Bob to this workspace as a new owner
$az role assignment create --assignee bob@contoso.com --role owner --scope <workspace Azure Resource ID>
```

> [!TIP]
> <span data-ttu-id="71949-154">`bob@contoso.com` in the above command must be a valid Azure AD identity in the directory where the current subscription belongs to.</span><span class="sxs-lookup"><span data-stu-id="71949-154">`bob@contoso.com` in the above command must be a valid Azure AD identity in the directory where the current subscription belongs to.</span></span>

## <a name="step-3-create-a-new-project"></a><span data-ttu-id="71949-155">Step 3.</span><span class="sxs-lookup"><span data-stu-id="71949-155">Step 3.</span></span> <span data-ttu-id="71949-156">Create a new project</span><span class="sxs-lookup"><span data-stu-id="71949-156">Create a new project</span></span>
<span data-ttu-id="71949-157">Our next step is to create a new project.</span><span class="sxs-lookup"><span data-stu-id="71949-157">Our next step is to create a new project.</span></span> <span data-ttu-id="71949-158">There are several ways to get started with a new project.</span><span class="sxs-lookup"><span data-stu-id="71949-158">There are several ways to get started with a new project.</span></span>

### <a name="create-a-new-blank-project"></a><span data-ttu-id="71949-159">Create a new blank project</span><span class="sxs-lookup"><span data-stu-id="71949-159">Create a new blank project</span></span>

```azure-cli
# create a new project
$ az ml project create --name <project name> --workspace <workspace name> --account <experimentation account name> --resource-group <resource group name> --path <local folder path>
```

### <a name="create-a-new-project-with-a-default-project-template"></a><span data-ttu-id="71949-160">Create a new project with a default project template</span><span class="sxs-lookup"><span data-stu-id="71949-160">Create a new project with a default project template</span></span>
<span data-ttu-id="71949-161">You can create a new project with a default template.</span><span class="sxs-lookup"><span data-stu-id="71949-161">You can create a new project with a default template.</span></span>

```azure-cli
$ az ml project create --name <project name> --workspace <workspace name> --account <experimentation account name> --resource-group <resource group name> --path <local folder path> --template
```

### <a name="create-a-new-project-associated-with-a-cloud-git-repository"></a><span data-ttu-id="71949-162">Create a new project associated with a cloud Git repository</span><span class="sxs-lookup"><span data-stu-id="71949-162">Create a new project associated with a cloud Git repository</span></span>
<span data-ttu-id="71949-163">You can create a new project associated with a Azure DevOps Git repository.</span><span class="sxs-lookup"><span data-stu-id="71949-163">You can create a new project associated with a Azure DevOps Git repository.</span></span> <span data-ttu-id="71949-164">Every time an experiment is submitted, a snapshot of the entire project folder is committed to the remote Git repo.</span><span class="sxs-lookup"><span data-stu-id="71949-164">Every time an experiment is submitted, a snapshot of the entire project folder is committed to the remote Git repo.</span></span> <span data-ttu-id="71949-165">See [Using Git repository with an Azure Machine Learning Workbench project](using-git-ml-project.md) for more details.</span><span class="sxs-lookup"><span data-stu-id="71949-165">See [Using Git repository with an Azure Machine Learning Workbench project](using-git-ml-project.md) for more details.</span></span>

> [!NOTE]
> <span data-ttu-id="71949-166">Azure Machine Learning only supports empty Git repos created in Azure DevOps.</span><span class="sxs-lookup"><span data-stu-id="71949-166">Azure Machine Learning only supports empty Git repos created in Azure DevOps.</span></span>

```azure-cli
$ az ml project create --name <project name> --workspace <workspace name> --account <experimentation account name> --resource-group <resource group name> --path <local folder path> --repo <VSTS repo URL>
```
> [!TIP]
> <span data-ttu-id="71949-167">If you are getting an error "Repository url might be invalid or user might not have access", you can create a security token in Azure DevOps (under _Security_, _Add personal access tokens_ menu) and use the `--vststoken` argument when creating your project.</span><span class="sxs-lookup"><span data-stu-id="71949-167">If you are getting an error "Repository url might be invalid or user might not have access", you can create a security token in Azure DevOps (under _Security_, _Add personal access tokens_ menu) and use the `--vststoken` argument when creating your project.</span></span> 

### <a name="sample_create"></a><span data-ttu-id="71949-168">Create a new project from a sample</span><span class="sxs-lookup"><span data-stu-id="71949-168">Create a new project from a sample</span></span>
<span data-ttu-id="71949-169">In this example, you create a new project using a sample project as a template.</span><span class="sxs-lookup"><span data-stu-id="71949-169">In this example, you create a new project using a sample project as a template.</span></span>

```azure-cli
# List the project samples, find the Classifying Iris sample
$ az ml project sample list

# Create a new project from the sample
az ml project create --name <project name> --workspace <workspace name> --account <experimentation account name> --resource-group <resource group name> --path <local folder path> --template-url https://github.com/MicrosoftDocs/MachineLearningSamples-Iris
```
<span data-ttu-id="71949-170">Once your project is created, use `cd` command to enter the project directory.</span><span class="sxs-lookup"><span data-stu-id="71949-170">Once your project is created, use `cd` command to enter the project directory.</span></span>

## <a name="step-4-run-the-training-experiment"></a><span data-ttu-id="71949-171">Step 4 Run the training experiment</span><span class="sxs-lookup"><span data-stu-id="71949-171">Step 4 Run the training experiment</span></span> 
<span data-ttu-id="71949-172">The following steps assume that you have a project with the Iris sample (see [Create a new project from an online sample](#sample_create)).</span><span class="sxs-lookup"><span data-stu-id="71949-172">The following steps assume that you have a project with the Iris sample (see [Create a new project from an online sample](#sample_create)).</span></span>

### <a name="prepare-your-environment"></a><span data-ttu-id="71949-173">Prepare your environment</span><span class="sxs-lookup"><span data-stu-id="71949-173">Prepare your environment</span></span> 
<span data-ttu-id="71949-174">For the Iris sample, you must install matplotlib.</span><span class="sxs-lookup"><span data-stu-id="71949-174">For the Iris sample, you must install matplotlib.</span></span>

```azure-cli
$ pip install matplotlib
```

###  <a name="submit-the-experiment"></a><span data-ttu-id="71949-175">Submit the experiment</span><span class="sxs-lookup"><span data-stu-id="71949-175">Submit the experiment</span></span>

```azure-cli
# Execute the file
$ az ml experiment submit --run-configuration local iris_sklearn.py
```

### <a name="iterate-on-your-experiment-with-descending-regularization-rates"></a><span data-ttu-id="71949-176">Iterate on your experiment with descending regularization rates</span><span class="sxs-lookup"><span data-stu-id="71949-176">Iterate on your experiment with descending regularization rates</span></span>
<span data-ttu-id="71949-177">With some creativity, it's simple to put together a Python script that submits experiments with different regularization rates.</span><span class="sxs-lookup"><span data-stu-id="71949-177">With some creativity, it's simple to put together a Python script that submits experiments with different regularization rates.</span></span> <span data-ttu-id="71949-178">(You might have to edit the file to point to the right project path.)</span><span class="sxs-lookup"><span data-stu-id="71949-178">(You might have to edit the file to point to the right project path.)</span></span>

```azure-cli
$ python run.py
```

## <a name="step-5-view-run-history"></a><span data-ttu-id="71949-179">Step 5.</span><span class="sxs-lookup"><span data-stu-id="71949-179">Step 5.</span></span> <span data-ttu-id="71949-180">View run history</span><span class="sxs-lookup"><span data-stu-id="71949-180">View run history</span></span>
<span data-ttu-id="71949-181">Following command lists all the previous runs executed.</span><span class="sxs-lookup"><span data-stu-id="71949-181">Following command lists all the previous runs executed.</span></span> 

```azure-cli
$ az ml history list -o table
```
<span data-ttu-id="71949-182">Running the preceding command displays a list of all the runs belonging to this project.</span><span class="sxs-lookup"><span data-stu-id="71949-182">Running the preceding command displays a list of all the runs belonging to this project.</span></span> <span data-ttu-id="71949-183">You can see that accuracy and regularization rate metrics are listed too.</span><span class="sxs-lookup"><span data-stu-id="71949-183">You can see that accuracy and regularization rate metrics are listed too.</span></span> <span data-ttu-id="71949-184">This makes it easy to identify the best run from the list.</span><span class="sxs-lookup"><span data-stu-id="71949-184">This makes it easy to identify the best run from the list.</span></span>

## <a name="step-5a-view-attachment-created-by-a-given-run"></a><span data-ttu-id="71949-185">Step 5.a View attachment created by a given run</span><span class="sxs-lookup"><span data-stu-id="71949-185">Step 5.a View attachment created by a given run</span></span> 
<span data-ttu-id="71949-186">To view the attachment associated with a given run, you can use the info command of run history.</span><span class="sxs-lookup"><span data-stu-id="71949-186">To view the attachment associated with a given run, you can use the info command of run history.</span></span> <span data-ttu-id="71949-187">Find a run ID of a specific run from the preceding list.</span><span class="sxs-lookup"><span data-stu-id="71949-187">Find a run ID of a specific run from the preceding list.</span></span>

```azure-cli
$ az ml history info --run <run id> --artifact driver_log
```

<span data-ttu-id="71949-188">To download the artifacts from a run, you can use below command:</span><span class="sxs-lookup"><span data-stu-id="71949-188">To download the artifacts from a run, you can use below command:</span></span>

```azure-cli
# Stream a given attachment 
$ az ml history info --run <run id> --artifact <artifact location>
```

## <a name="step-6-promote-artifacts-of-a-run"></a><span data-ttu-id="71949-189">Step 6.</span><span class="sxs-lookup"><span data-stu-id="71949-189">Step 6.</span></span> <span data-ttu-id="71949-190">Promote artifacts of a run</span><span class="sxs-lookup"><span data-stu-id="71949-190">Promote artifacts of a run</span></span> 
<span data-ttu-id="71949-191">One of the runs has a better AUC, so this is the one to use when creating a scoring web service to deploy to production.</span><span class="sxs-lookup"><span data-stu-id="71949-191">One of the runs has a better AUC, so this is the one to use when creating a scoring web service to deploy to production.</span></span> <span data-ttu-id="71949-192">In order to do so, you first need to promote the artifacts into an asset.</span><span class="sxs-lookup"><span data-stu-id="71949-192">In order to do so, you first need to promote the artifacts into an asset.</span></span>

```azure-cli
$ az ml history promote --run <run id> --artifact-path outputs/model.pkl --name model.pkl
```

<span data-ttu-id="71949-193">This creates an `assets` folder in your project directory with a `model.pkl.link` file.</span><span class="sxs-lookup"><span data-stu-id="71949-193">This creates an `assets` folder in your project directory with a `model.pkl.link` file.</span></span> <span data-ttu-id="71949-194">This link file is used to reference a promoted asset.</span><span class="sxs-lookup"><span data-stu-id="71949-194">This link file is used to reference a promoted asset.</span></span>

## <a name="step-7-download-the-files-to-be-operationalized"></a><span data-ttu-id="71949-195">Step 7.</span><span class="sxs-lookup"><span data-stu-id="71949-195">Step 7.</span></span> <span data-ttu-id="71949-196">Download the files to be operationalized</span><span class="sxs-lookup"><span data-stu-id="71949-196">Download the files to be operationalized</span></span>
<span data-ttu-id="71949-197">Download the promoted model so you can use them to create a prediction web service.</span><span class="sxs-lookup"><span data-stu-id="71949-197">Download the promoted model so you can use them to create a prediction web service.</span></span> 

```azure-cli
$ az ml asset download --link-file assets\pickle.link -d asset_download
```

## <a name="step-8-set-up-your-model-management-environment"></a><span data-ttu-id="71949-198">Step 8.</span><span class="sxs-lookup"><span data-stu-id="71949-198">Step 8.</span></span> <span data-ttu-id="71949-199">Set up your model management environment</span><span class="sxs-lookup"><span data-stu-id="71949-199">Set up your model management environment</span></span> 
<span data-ttu-id="71949-200">Create an environment to deploy web services.</span><span class="sxs-lookup"><span data-stu-id="71949-200">Create an environment to deploy web services.</span></span> <span data-ttu-id="71949-201">You can run the web service on the local machine using Docker.</span><span class="sxs-lookup"><span data-stu-id="71949-201">You can run the web service on the local machine using Docker.</span></span> <span data-ttu-id="71949-202">Or deploy it to an ACS cluster for high-scale operations.</span><span class="sxs-lookup"><span data-stu-id="71949-202">Or deploy it to an ACS cluster for high-scale operations.</span></span> 

```azure-cli
# Create new local operationalization environment
$ az ml env setup -l <supported Azure region> -n <env name>
# Once setup is complete, set your environment for current context
$ az ml env set -g <resource group name> -n <env name>
```

## <a name="step-9-create-a-model-management-account"></a><span data-ttu-id="71949-203">Step 9.</span><span class="sxs-lookup"><span data-stu-id="71949-203">Step 9.</span></span> <span data-ttu-id="71949-204">Create a model management account</span><span class="sxs-lookup"><span data-stu-id="71949-204">Create a model management account</span></span> 
<span data-ttu-id="71949-205">A model management account is required to deploy and track your models in production.</span><span class="sxs-lookup"><span data-stu-id="71949-205">A model management account is required to deploy and track your models in production.</span></span> 

```azure-cli
$ az ml account modelmanagement create -n <model management account name> -g <resource group name> -l <supported Azure region>
```

## <a name="step-10-create-a-web-service"></a><span data-ttu-id="71949-206">Step 10.</span><span class="sxs-lookup"><span data-stu-id="71949-206">Step 10.</span></span> <span data-ttu-id="71949-207">Create a web service</span><span class="sxs-lookup"><span data-stu-id="71949-207">Create a web service</span></span>
<span data-ttu-id="71949-208">Create a web service that returns a prediction using the model you deployed.</span><span class="sxs-lookup"><span data-stu-id="71949-208">Create a web service that returns a prediction using the model you deployed.</span></span> 

```azure-cli
$ az ml service create realtime -m asset_download/model.pkl -f score_iris.py -r python –n <web service name>
```

## <a name="step-11-run-the-web-service"></a><span data-ttu-id="71949-209">Step 11.</span><span class="sxs-lookup"><span data-stu-id="71949-209">Step 11.</span></span> <span data-ttu-id="71949-210">Run the web service</span><span class="sxs-lookup"><span data-stu-id="71949-210">Run the web service</span></span>
<span data-ttu-id="71949-211">Using the web service ID from the output of the previous step, call the web service and test it.</span><span class="sxs-lookup"><span data-stu-id="71949-211">Using the web service ID from the output of the previous step, call the web service and test it.</span></span> 

```azure-cli
# Get web service usage information 
$ az ml service usage realtime -i <web service id>

# Call the web service with the run command:
$ az ml service run realtime -i <web service id> -d <input data>
```

## <a name="step-12-deleting-all-the-resources"></a><span data-ttu-id="71949-212">Step 12.</span><span class="sxs-lookup"><span data-stu-id="71949-212">Step 12.</span></span> <span data-ttu-id="71949-213">Deleting all the resources</span><span class="sxs-lookup"><span data-stu-id="71949-213">Deleting all the resources</span></span> 
<span data-ttu-id="71949-214">Let's complete this tutorial by deleting all the resources that were created, unless you want to keep working on it.</span><span class="sxs-lookup"><span data-stu-id="71949-214">Let's complete this tutorial by deleting all the resources that were created, unless you want to keep working on it.</span></span> 

<span data-ttu-id="71949-215">To do so, delete the resource group holding the resources.</span><span class="sxs-lookup"><span data-stu-id="71949-215">To do so, delete the resource group holding the resources.</span></span> 

```azure-cli
az group delete --name <resource group name>
```

## <a name="next-steps"></a><span data-ttu-id="71949-216">Next Steps</span><span class="sxs-lookup"><span data-stu-id="71949-216">Next Steps</span></span>
<span data-ttu-id="71949-217">In this tutorial, you have learned to use the Azure Machine Learning to:</span><span class="sxs-lookup"><span data-stu-id="71949-217">In this tutorial, you have learned to use the Azure Machine Learning to:</span></span> 
> [!div class="checklist"]
> * <span data-ttu-id="71949-218">Set up an experimentation account, creating workspace</span><span class="sxs-lookup"><span data-stu-id="71949-218">Set up an experimentation account, creating workspace</span></span>
> * <span data-ttu-id="71949-219">Create projects</span><span class="sxs-lookup"><span data-stu-id="71949-219">Create projects</span></span>
> * <span data-ttu-id="71949-220">Submit experiments to multiple compute target</span><span class="sxs-lookup"><span data-stu-id="71949-220">Submit experiments to multiple compute target</span></span>
> * <span data-ttu-id="71949-221">Promote and register a trained model</span><span class="sxs-lookup"><span data-stu-id="71949-221">Promote and register a trained model</span></span>
> * <span data-ttu-id="71949-222">Create a model management account for model management</span><span class="sxs-lookup"><span data-stu-id="71949-222">Create a model management account for model management</span></span>
> * <span data-ttu-id="71949-223">Create an environment for deploying web services</span><span class="sxs-lookup"><span data-stu-id="71949-223">Create an environment for deploying web services</span></span>
> * <span data-ttu-id="71949-224">Deploy a web-service and score with new data</span><span class="sxs-lookup"><span data-stu-id="71949-224">Deploy a web-service and score with new data</span></span>
