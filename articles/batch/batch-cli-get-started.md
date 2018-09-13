---
title: Get started with Azure CLI for Batch | Microsoft Docs
description: Get a quick introduction to the Batch commands in Azure CLI for managing Azure Batch service resources
services: batch
documentationcenter: ''
author: tamram
manager: timlt
editor: ''
ms.assetid: fcd76587-1827-4bc8-a84d-bba1cd980d85
ms.service: batch
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 01/23/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 698c481e2eff5e0a3b893a0377d9f4cd2f052eb4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553006"
---
# <a name="manage-batch-resources-with-azure-cli"></a><span data-ttu-id="26c9b-103">Manage Batch resources with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="26c9b-103">Manage Batch resources with Azure CLI</span></span>

<span data-ttu-id="26c9b-104">The cross-platform Azure Command-Line Interface (Azure CLI) enables you to manage your Batch accounts and resources such as pools, jobs, and tasks in Linux, Mac, and Windows command shells.</span><span class="sxs-lookup"><span data-stu-id="26c9b-104">The cross-platform Azure Command-Line Interface (Azure CLI) enables you to manage your Batch accounts and resources such as pools, jobs, and tasks in Linux, Mac, and Windows command shells.</span></span> <span data-ttu-id="26c9b-105">With the Azure CLI, you can perform and script many of the same tasks you carry out with the Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span><span class="sxs-lookup"><span data-stu-id="26c9b-105">With the Azure CLI, you can perform and script many of the same tasks you carry out with the Batch APIs, Azure portal, and Batch PowerShell cmdlets.</span></span>

<span data-ttu-id="26c9b-106">This article is based on Azure CLI version 0.10.5.</span><span class="sxs-lookup"><span data-stu-id="26c9b-106">This article is based on Azure CLI version 0.10.5.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="26c9b-107">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="26c9b-107">Prerequisites</span></span>
* [<span data-ttu-id="26c9b-108">Install the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="26c9b-108">Install the Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="26c9b-109">Connect the Azure CLI to your Azure subscription</span><span class="sxs-lookup"><span data-stu-id="26c9b-109">Connect the Azure CLI to your Azure subscription</span></span>](../xplat-cli-connect.md)
* <span data-ttu-id="26c9b-110">Switch to **Resource Manager mode**: `azure config mode arm`</span><span class="sxs-lookup"><span data-stu-id="26c9b-110">Switch to **Resource Manager mode**: `azure config mode arm`</span></span>

> [!TIP]
> <span data-ttu-id="26c9b-111">We recommend that you update your Azure CLI installation frequently to take advantage of service updates and enhancements.</span><span class="sxs-lookup"><span data-stu-id="26c9b-111">We recommend that you update your Azure CLI installation frequently to take advantage of service updates and enhancements.</span></span>
> 
> 

## <a name="command-help"></a><span data-ttu-id="26c9b-112">Command help</span><span class="sxs-lookup"><span data-stu-id="26c9b-112">Command help</span></span>
<span data-ttu-id="26c9b-113">You can display help text for every command in the Azure CLI by appending `-h` as the only option after the command.</span><span class="sxs-lookup"><span data-stu-id="26c9b-113">You can display help text for every command in the Azure CLI by appending `-h` as the only option after the command.</span></span> <span data-ttu-id="26c9b-114">For example:</span><span class="sxs-lookup"><span data-stu-id="26c9b-114">For example:</span></span>

* <span data-ttu-id="26c9b-115">To get help for the `azure` command, enter: `azure -h`</span><span class="sxs-lookup"><span data-stu-id="26c9b-115">To get help for the `azure` command, enter: `azure -h`</span></span>
* <span data-ttu-id="26c9b-116">To get a list of all Batch commands in the CLI, use: `azure batch -h`</span><span class="sxs-lookup"><span data-stu-id="26c9b-116">To get a list of all Batch commands in the CLI, use: `azure batch -h`</span></span>
* <span data-ttu-id="26c9b-117">To get help on creating a Batch account, enter: `azure batch account create -h`</span><span class="sxs-lookup"><span data-stu-id="26c9b-117">To get help on creating a Batch account, enter: `azure batch account create -h`</span></span>

<span data-ttu-id="26c9b-118">When in doubt, use the `-h` command-line option to get help on any Azure CLI command.</span><span class="sxs-lookup"><span data-stu-id="26c9b-118">When in doubt, use the `-h` command-line option to get help on any Azure CLI command.</span></span>

## <a name="create-a-batch-account"></a><span data-ttu-id="26c9b-119">Create a Batch account</span><span class="sxs-lookup"><span data-stu-id="26c9b-119">Create a Batch account</span></span>
<span data-ttu-id="26c9b-120">Usage:</span><span class="sxs-lookup"><span data-stu-id="26c9b-120">Usage:</span></span>

    azure batch account create [options] <name>

<span data-ttu-id="26c9b-121">Example:</span><span class="sxs-lookup"><span data-stu-id="26c9b-121">Example:</span></span>

    azure batch account create --location "West US"  --resource-group "resgroup001" "batchaccount001"

<span data-ttu-id="26c9b-122">Creates a new Batch account with the specified parameters.</span><span class="sxs-lookup"><span data-stu-id="26c9b-122">Creates a new Batch account with the specified parameters.</span></span> <span data-ttu-id="26c9b-123">You must specify at least a location, resource group, and account name.</span><span class="sxs-lookup"><span data-stu-id="26c9b-123">You must specify at least a location, resource group, and account name.</span></span> <span data-ttu-id="26c9b-124">If you don't already have a resource group, create one by running `azure group create`, and specify one of the Azure regions (such as "West US") for the `--location` option.</span><span class="sxs-lookup"><span data-stu-id="26c9b-124">If you don't already have a resource group, create one by running `azure group create`, and specify one of the Azure regions (such as "West US") for the `--location` option.</span></span> <span data-ttu-id="26c9b-125">For example:</span><span class="sxs-lookup"><span data-stu-id="26c9b-125">For example:</span></span>

    azure group create --name "resgroup001" --location "West US"

> [!NOTE]
> <span data-ttu-id="26c9b-126">The Batch account name must be unique within the Azure region the account is created.</span><span class="sxs-lookup"><span data-stu-id="26c9b-126">The Batch account name must be unique within the Azure region the account is created.</span></span> <span data-ttu-id="26c9b-127">It may contain only lowercase alphanumeric characters, and must be 3-24 characters in length.</span><span class="sxs-lookup"><span data-stu-id="26c9b-127">It may contain only lowercase alphanumeric characters, and must be 3-24 characters in length.</span></span> <span data-ttu-id="26c9b-128">You can't use special characters like `-` or `_` in Batch account names.</span><span class="sxs-lookup"><span data-stu-id="26c9b-128">You can't use special characters like `-` or `_` in Batch account names.</span></span>
> 
> 

### <a name="linked-storage-account-autostorage"></a><span data-ttu-id="26c9b-129">Linked storage account (autostorage)</span><span class="sxs-lookup"><span data-stu-id="26c9b-129">Linked storage account (autostorage)</span></span>
<span data-ttu-id="26c9b-130">You can (optionally) link a **General purpose** Storage account to your Batch account when you create it.</span><span class="sxs-lookup"><span data-stu-id="26c9b-130">You can (optionally) link a **General purpose** Storage account to your Batch account when you create it.</span></span> <span data-ttu-id="26c9b-131">The [application packages](batch-application-packages.md) feature of Batch uses blob storage in a linked General purpose Storage account, as does the [Batch File Conventions .NET](batch-task-output.md) library.</span><span class="sxs-lookup"><span data-stu-id="26c9b-131">The [application packages](batch-application-packages.md) feature of Batch uses blob storage in a linked General purpose Storage account, as does the [Batch File Conventions .NET](batch-task-output.md) library.</span></span> <span data-ttu-id="26c9b-132">These optional features assist you in deploying the applications your Batch tasks run, and persisting the data they produce.</span><span class="sxs-lookup"><span data-stu-id="26c9b-132">These optional features assist you in deploying the applications your Batch tasks run, and persisting the data they produce.</span></span>

<span data-ttu-id="26c9b-133">To link an existing Azure Storage account to a new Batch account when you create it, specify the `--autostorage-account-id` option.</span><span class="sxs-lookup"><span data-stu-id="26c9b-133">To link an existing Azure Storage account to a new Batch account when you create it, specify the `--autostorage-account-id` option.</span></span> <span data-ttu-id="26c9b-134">This option requires the fully qualified resource ID of the storage account.</span><span class="sxs-lookup"><span data-stu-id="26c9b-134">This option requires the fully qualified resource ID of the storage account.</span></span>

<span data-ttu-id="26c9b-135">First, show your storage account's details:</span><span class="sxs-lookup"><span data-stu-id="26c9b-135">First, show your storage account's details:</span></span>

    azure storage account show --resource-group "resgroup001" "storageaccount001"

<span data-ttu-id="26c9b-136">Then use the **Url** value for the `--autostorage-account-id` option.</span><span class="sxs-lookup"><span data-stu-id="26c9b-136">Then use the **Url** value for the `--autostorage-account-id` option.</span></span> <span data-ttu-id="26c9b-137">The Url value starts with "/subscriptions/" and contains your subscription ID and resource path to the Storage account:</span><span class="sxs-lookup"><span data-stu-id="26c9b-137">The Url value starts with "/subscriptions/" and contains your subscription ID and resource path to the Storage account:</span></span>

    azure batch account create --location "West US"  --resource-group "resgroup001" --autostorage-account-id "/subscriptions/8ffffff8-4444-4444-bfbf-8ffffff84444/resourceGroups/resgroup001/providers/Microsoft.Storage/storageAccounts/storageaccount001" "batchaccount001"

## <a name="delete-a-batch-account"></a><span data-ttu-id="26c9b-138">Delete a Batch account</span><span class="sxs-lookup"><span data-stu-id="26c9b-138">Delete a Batch account</span></span>
<span data-ttu-id="26c9b-139">Usage:</span><span class="sxs-lookup"><span data-stu-id="26c9b-139">Usage:</span></span>

    azure batch account delete [options] <name>

<span data-ttu-id="26c9b-140">Example:</span><span class="sxs-lookup"><span data-stu-id="26c9b-140">Example:</span></span>

    azure batch account delete --resource-group "resgroup001" "batchaccount001"

<span data-ttu-id="26c9b-141">Deletes the specified Batch account.</span><span class="sxs-lookup"><span data-stu-id="26c9b-141">Deletes the specified Batch account.</span></span> <span data-ttu-id="26c9b-142">When prompted, confirm you want to remove the account (account removal can take some time to complete).</span><span class="sxs-lookup"><span data-stu-id="26c9b-142">When prompted, confirm you want to remove the account (account removal can take some time to complete).</span></span>

## <a name="manage-account-access-keys"></a><span data-ttu-id="26c9b-143">Manage account access keys</span><span class="sxs-lookup"><span data-stu-id="26c9b-143">Manage account access keys</span></span>
<span data-ttu-id="26c9b-144">You need an access key to [create and modify resources](#create-and-modify-batch-resources) in your Batch account.</span><span class="sxs-lookup"><span data-stu-id="26c9b-144">You need an access key to [create and modify resources](#create-and-modify-batch-resources) in your Batch account.</span></span>

### <a name="list-access-keys"></a><span data-ttu-id="26c9b-145">List access keys</span><span class="sxs-lookup"><span data-stu-id="26c9b-145">List access keys</span></span>
<span data-ttu-id="26c9b-146">Usage:</span><span class="sxs-lookup"><span data-stu-id="26c9b-146">Usage:</span></span>

    azure batch account keys list [options] <name>

<span data-ttu-id="26c9b-147">Example:</span><span class="sxs-lookup"><span data-stu-id="26c9b-147">Example:</span></span>

    azure batch account keys list --resource-group "resgroup001" "batchaccount001"

<span data-ttu-id="26c9b-148">Lists the account keys for the given Batch account.</span><span class="sxs-lookup"><span data-stu-id="26c9b-148">Lists the account keys for the given Batch account.</span></span>

### <a name="generate-a-new-access-key"></a><span data-ttu-id="26c9b-149">Generate a new access key</span><span class="sxs-lookup"><span data-stu-id="26c9b-149">Generate a new access key</span></span>
<span data-ttu-id="26c9b-150">Usage:</span><span class="sxs-lookup"><span data-stu-id="26c9b-150">Usage:</span></span>

    azure batch account keys renew [options] --<primary|secondary> <name>

<span data-ttu-id="26c9b-151">Example:</span><span class="sxs-lookup"><span data-stu-id="26c9b-151">Example:</span></span>

    azure batch account keys renew --resource-group "resgroup001" --primary "batchaccount001"

<span data-ttu-id="26c9b-152">Regenerates the specified account key for the given Batch account.</span><span class="sxs-lookup"><span data-stu-id="26c9b-152">Regenerates the specified account key for the given Batch account.</span></span>

## <a name="create-and-modify-batch-resources"></a><span data-ttu-id="26c9b-153">Create and modify Batch resources</span><span class="sxs-lookup"><span data-stu-id="26c9b-153">Create and modify Batch resources</span></span>
<span data-ttu-id="26c9b-154">You can use the Azure CLI to create, read, update, and delete (CRUD) Batch resources like pools, compute nodes, jobs, and tasks.</span><span class="sxs-lookup"><span data-stu-id="26c9b-154">You can use the Azure CLI to create, read, update, and delete (CRUD) Batch resources like pools, compute nodes, jobs, and tasks.</span></span> <span data-ttu-id="26c9b-155">These CRUD operations require your Batch account name, access key, and endpoint.</span><span class="sxs-lookup"><span data-stu-id="26c9b-155">These CRUD operations require your Batch account name, access key, and endpoint.</span></span> <span data-ttu-id="26c9b-156">You can specify these with the `-a`, `-k`, and `-u` options, or set [environment variables](#credential-environment-variables) which the CLI uses automatically (if populated).</span><span class="sxs-lookup"><span data-stu-id="26c9b-156">You can specify these with the `-a`, `-k`, and `-u` options, or set [environment variables](#credential-environment-variables) which the CLI uses automatically (if populated).</span></span>

### <a name="credential-environment-variables"></a><span data-ttu-id="26c9b-157">Credential environment variables</span><span class="sxs-lookup"><span data-stu-id="26c9b-157">Credential environment variables</span></span>
<span data-ttu-id="26c9b-158">You can set `AZURE_BATCH_ACCOUNT`, `AZURE_BATCH_ACCESS_KEY`, and `AZURE_BATCH_ENDPOINT` environment variables instead of specifying `-a`, `-k`, and `-u` options on the command line for every command you execute.</span><span class="sxs-lookup"><span data-stu-id="26c9b-158">You can set `AZURE_BATCH_ACCOUNT`, `AZURE_BATCH_ACCESS_KEY`, and `AZURE_BATCH_ENDPOINT` environment variables instead of specifying `-a`, `-k`, and `-u` options on the command line for every command you execute.</span></span> <span data-ttu-id="26c9b-159">The Batch CLI uses these variables (if set) so that you can omit the `-a`, `-k`, and `-u` options.</span><span class="sxs-lookup"><span data-stu-id="26c9b-159">The Batch CLI uses these variables (if set) so that you can omit the `-a`, `-k`, and `-u` options.</span></span> <span data-ttu-id="26c9b-160">The remainder of this article assumes use of these environment variables.</span><span class="sxs-lookup"><span data-stu-id="26c9b-160">The remainder of this article assumes use of these environment variables.</span></span>

> [!TIP]
> <span data-ttu-id="26c9b-161">List your keys with `azure batch account keys list`, and display the account's endpoint with `azure batch account show`.</span><span class="sxs-lookup"><span data-stu-id="26c9b-161">List your keys with `azure batch account keys list`, and display the account's endpoint with `azure batch account show`.</span></span>
> 
> 

### <a name="json-files"></a><span data-ttu-id="26c9b-162">JSON files</span><span class="sxs-lookup"><span data-stu-id="26c9b-162">JSON files</span></span>
<span data-ttu-id="26c9b-163">When you create Batch resources like pools and jobs, you can specify a JSON file containing the new resource's configuration instead of passing its parameters as command-line options.</span><span class="sxs-lookup"><span data-stu-id="26c9b-163">When you create Batch resources like pools and jobs, you can specify a JSON file containing the new resource's configuration instead of passing its parameters as command-line options.</span></span> <span data-ttu-id="26c9b-164">For example:</span><span class="sxs-lookup"><span data-stu-id="26c9b-164">For example:</span></span>

`azure batch pool create my_batch_pool.json`

<span data-ttu-id="26c9b-165">While you can perform many resource creation operations using only command-line options, some features require a JSON-formatted file containing the resource details.</span><span class="sxs-lookup"><span data-stu-id="26c9b-165">While you can perform many resource creation operations using only command-line options, some features require a JSON-formatted file containing the resource details.</span></span> <span data-ttu-id="26c9b-166">For example, you must use a JSON file if you want to specify resource files for a start task.</span><span class="sxs-lookup"><span data-stu-id="26c9b-166">For example, you must use a JSON file if you want to specify resource files for a start task.</span></span>

<span data-ttu-id="26c9b-167">To find the JSON required to create a resource, refer to the [Batch REST API reference][rest_api] documentation on MSDN.</span><span class="sxs-lookup"><span data-stu-id="26c9b-167">To find the JSON required to create a resource, refer to the [Batch REST API reference][rest_api] documentation on MSDN.</span></span> <span data-ttu-id="26c9b-168">Each "Add *resource type*" topic contains example JSON for creating the resource, which you can use as templates for your JSON files.</span><span class="sxs-lookup"><span data-stu-id="26c9b-168">Each "Add *resource type*" topic contains example JSON for creating the resource, which you can use as templates for your JSON files.</span></span> <span data-ttu-id="26c9b-169">For example, JSON for pool creation can be found in [Add a pool to an account][rest_add_pool].</span><span class="sxs-lookup"><span data-stu-id="26c9b-169">For example, JSON for pool creation can be found in [Add a pool to an account][rest_add_pool].</span></span>

> [!NOTE]
> <span data-ttu-id="26c9b-170">If you specify a JSON file when you create a resource, all other parameters that you specify on the command line for that resource are ignored.</span><span class="sxs-lookup"><span data-stu-id="26c9b-170">If you specify a JSON file when you create a resource, all other parameters that you specify on the command line for that resource are ignored.</span></span>
> 
> 

## <a name="create-a-pool"></a><span data-ttu-id="26c9b-171">Create a pool</span><span class="sxs-lookup"><span data-stu-id="26c9b-171">Create a pool</span></span>
<span data-ttu-id="26c9b-172">Usage:</span><span class="sxs-lookup"><span data-stu-id="26c9b-172">Usage:</span></span>

    azure batch pool create [options] [json-file]

<span data-ttu-id="26c9b-173">Example (Virtual Machine Configuration):</span><span class="sxs-lookup"><span data-stu-id="26c9b-173">Example (Virtual Machine Configuration):</span></span>

    azure batch pool create --id "pool001" --target-dedicated 1 --vm-size "STANDARD_A1" --image-publisher "Canonical" --image-offer "UbuntuServer" --image-sku "14.04.2-LTS" --node-agent-id "batch.node.ubuntu 14.04"

<span data-ttu-id="26c9b-174">Example (Cloud Services Configuration):</span><span class="sxs-lookup"><span data-stu-id="26c9b-174">Example (Cloud Services Configuration):</span></span>

    azure batch pool create --id "pool002" --target-dedicated 1 --vm-size "small" --os-family "4"

<span data-ttu-id="26c9b-175">Creates a pool of compute nodes in the Batch service.</span><span class="sxs-lookup"><span data-stu-id="26c9b-175">Creates a pool of compute nodes in the Batch service.</span></span>

<span data-ttu-id="26c9b-176">As mentioned in the [Batch feature overview](batch-api-basics.md#pool), you have two options when you select an operating system for the nodes in your pool: **Virtual Machine Configuration** and **Cloud Services Configuration**.</span><span class="sxs-lookup"><span data-stu-id="26c9b-176">As mentioned in the [Batch feature overview](batch-api-basics.md#pool), you have two options when you select an operating system for the nodes in your pool: **Virtual Machine Configuration** and **Cloud Services Configuration**.</span></span> <span data-ttu-id="26c9b-177">Use the `--image-*` options to create Virtual Machine Configuration pools, and `--os-family` to create Cloud Services Configuration pools.</span><span class="sxs-lookup"><span data-stu-id="26c9b-177">Use the `--image-*` options to create Virtual Machine Configuration pools, and `--os-family` to create Cloud Services Configuration pools.</span></span> <span data-ttu-id="26c9b-178">You can't specify both `--os-family` and `--image-*` options.</span><span class="sxs-lookup"><span data-stu-id="26c9b-178">You can't specify both `--os-family` and `--image-*` options.</span></span>

<span data-ttu-id="26c9b-179">You can specify pool [application packages](batch-application-packages.md) and the command line for a [start task](batch-api-basics.md#start-task).</span><span class="sxs-lookup"><span data-stu-id="26c9b-179">You can specify pool [application packages](batch-application-packages.md) and the command line for a [start task](batch-api-basics.md#start-task).</span></span> <span data-ttu-id="26c9b-180">To specify resource files for the start task, however, you must instead use a [JSON file](#json-files).</span><span class="sxs-lookup"><span data-stu-id="26c9b-180">To specify resource files for the start task, however, you must instead use a [JSON file](#json-files).</span></span>

<span data-ttu-id="26c9b-181">Delete a pool with:</span><span class="sxs-lookup"><span data-stu-id="26c9b-181">Delete a pool with:</span></span>

    azure batch pool delete [pool-id]

> [!TIP]
> <span data-ttu-id="26c9b-182">Check the [list of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images) for values appropriate for the `--image-*` options.</span><span class="sxs-lookup"><span data-stu-id="26c9b-182">Check the [list of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images) for values appropriate for the `--image-*` options.</span></span>
> 
> 

## <a name="create-a-job"></a><span data-ttu-id="26c9b-183">Create a job</span><span class="sxs-lookup"><span data-stu-id="26c9b-183">Create a job</span></span>
<span data-ttu-id="26c9b-184">Usage:</span><span class="sxs-lookup"><span data-stu-id="26c9b-184">Usage:</span></span>

    azure batch job create [options] [json-file]

<span data-ttu-id="26c9b-185">Example:</span><span class="sxs-lookup"><span data-stu-id="26c9b-185">Example:</span></span>

    azure batch job create --id "job001" --pool-id "pool001"

<span data-ttu-id="26c9b-186">Adds a job to the Batch account and specifies the pool on which its tasks execute.</span><span class="sxs-lookup"><span data-stu-id="26c9b-186">Adds a job to the Batch account and specifies the pool on which its tasks execute.</span></span>

<span data-ttu-id="26c9b-187">Delete a job with:</span><span class="sxs-lookup"><span data-stu-id="26c9b-187">Delete a job with:</span></span>

    azure batch job delete [job-id]

## <a name="list-pools-jobs-tasks-and-other-resources"></a><span data-ttu-id="26c9b-188">List pools, jobs, tasks, and other resources</span><span class="sxs-lookup"><span data-stu-id="26c9b-188">List pools, jobs, tasks, and other resources</span></span>
<span data-ttu-id="26c9b-189">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span><span class="sxs-lookup"><span data-stu-id="26c9b-189">Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type.</span></span> <span data-ttu-id="26c9b-190">For example, you can list the pools in your account and the tasks in a job:</span><span class="sxs-lookup"><span data-stu-id="26c9b-190">For example, you can list the pools in your account and the tasks in a job:</span></span>

    azure batch pool list
    azure batch task list --job-id "job001"

### <a name="listing-resources-efficiently"></a><span data-ttu-id="26c9b-191">Listing resources efficiently</span><span class="sxs-lookup"><span data-stu-id="26c9b-191">Listing resources efficiently</span></span>
<span data-ttu-id="26c9b-192">For faster querying, you can specify **select**, **filter**, and **expand** clause options for `list` operations.</span><span class="sxs-lookup"><span data-stu-id="26c9b-192">For faster querying, you can specify **select**, **filter**, and **expand** clause options for `list` operations.</span></span> <span data-ttu-id="26c9b-193">Use these options to limit the amount of data returned by the Batch service.</span><span class="sxs-lookup"><span data-stu-id="26c9b-193">Use these options to limit the amount of data returned by the Batch service.</span></span> <span data-ttu-id="26c9b-194">Because all filtering occurs server-side, only the data you are interested in crosses the wire.</span><span class="sxs-lookup"><span data-stu-id="26c9b-194">Because all filtering occurs server-side, only the data you are interested in crosses the wire.</span></span> <span data-ttu-id="26c9b-195">Use these clauses to save bandwidth (and therefore time) when you perform list operations.</span><span class="sxs-lookup"><span data-stu-id="26c9b-195">Use these clauses to save bandwidth (and therefore time) when you perform list operations.</span></span>

<span data-ttu-id="26c9b-196">For example, this will return only pools whose ids start with "renderTask":</span><span class="sxs-lookup"><span data-stu-id="26c9b-196">For example, this will return only pools whose ids start with "renderTask":</span></span>

    azure batch task list --job-id "job001" --filter-clause "startswith(id, 'renderTask')"

<span data-ttu-id="26c9b-197">The Batch CLI supports all three clauses supported by the Batch service:</span><span class="sxs-lookup"><span data-stu-id="26c9b-197">The Batch CLI supports all three clauses supported by the Batch service:</span></span>

* <span data-ttu-id="26c9b-198">`--select-clause [select-clause]`  Return a subset of properties for each entity</span><span class="sxs-lookup"><span data-stu-id="26c9b-198">`--select-clause [select-clause]`  Return a subset of properties for each entity</span></span>
* <span data-ttu-id="26c9b-199">`--filter-clause [filter-clause]`  Return only entities that match the specified OData expression</span><span class="sxs-lookup"><span data-stu-id="26c9b-199">`--filter-clause [filter-clause]`  Return only entities that match the specified OData expression</span></span>
* <span data-ttu-id="26c9b-200">`--expand-clause [expand-clause]`  Obtain the entity information in a single underlying REST call.</span><span class="sxs-lookup"><span data-stu-id="26c9b-200">`--expand-clause [expand-clause]`  Obtain the entity information in a single underlying REST call.</span></span> <span data-ttu-id="26c9b-201">The expand clause supports only the `stats` property at this time.</span><span class="sxs-lookup"><span data-stu-id="26c9b-201">The expand clause supports only the `stats` property at this time.</span></span>

<span data-ttu-id="26c9b-202">For details on the three clauses and performing list queries with them, see [Query the Azure Batch service efficiently](batch-efficient-list-queries.md).</span><span class="sxs-lookup"><span data-stu-id="26c9b-202">For details on the three clauses and performing list queries with them, see [Query the Azure Batch service efficiently](batch-efficient-list-queries.md).</span></span>

## <a name="application-package-management"></a><span data-ttu-id="26c9b-203">Application package management</span><span class="sxs-lookup"><span data-stu-id="26c9b-203">Application package management</span></span>
<span data-ttu-id="26c9b-204">Application packages provide a simplified way to deploy applications to the compute nodes in your pools.</span><span class="sxs-lookup"><span data-stu-id="26c9b-204">Application packages provide a simplified way to deploy applications to the compute nodes in your pools.</span></span> <span data-ttu-id="26c9b-205">With the Azure CLI, you can upload application packages, manage package versions, and delete packages.</span><span class="sxs-lookup"><span data-stu-id="26c9b-205">With the Azure CLI, you can upload application packages, manage package versions, and delete packages.</span></span>

<span data-ttu-id="26c9b-206">To create a new application and add a package version:</span><span class="sxs-lookup"><span data-stu-id="26c9b-206">To create a new application and add a package version:</span></span>

<span data-ttu-id="26c9b-207">**Create** an application:</span><span class="sxs-lookup"><span data-stu-id="26c9b-207">**Create** an application:</span></span>

    azure batch application create "resgroup001" "batchaccount001" "MyTaskApplication"

<span data-ttu-id="26c9b-208">**Add** an application package:</span><span class="sxs-lookup"><span data-stu-id="26c9b-208">**Add** an application package:</span></span>

    azure batch application package create "resgroup001" "batchaccount001" "MyTaskApplication" "1.10-beta3" package001.zip

<span data-ttu-id="26c9b-209">**Activate** the package:</span><span class="sxs-lookup"><span data-stu-id="26c9b-209">**Activate** the package:</span></span>

    azure batch application package activate "resgroup001" "batchaccount001" "MyTaskApplication" "1.10-beta3" zip

<span data-ttu-id="26c9b-210">Set the **default version** for the application:</span><span class="sxs-lookup"><span data-stu-id="26c9b-210">Set the **default version** for the application:</span></span>

    azure batch application set "resgroup001" "batchaccount001" "MyTaskApplication" --default-version "1.10-beta3"

### <a name="deploy-an-application-package"></a><span data-ttu-id="26c9b-211">Deploy an application package</span><span class="sxs-lookup"><span data-stu-id="26c9b-211">Deploy an application package</span></span>
<span data-ttu-id="26c9b-212">You can specify one or more application packages for deployment when you create a new pool.</span><span class="sxs-lookup"><span data-stu-id="26c9b-212">You can specify one or more application packages for deployment when you create a new pool.</span></span> <span data-ttu-id="26c9b-213">When you specify a package at pool creation time, it is deployed to each node as the node joins pool.</span><span class="sxs-lookup"><span data-stu-id="26c9b-213">When you specify a package at pool creation time, it is deployed to each node as the node joins pool.</span></span> <span data-ttu-id="26c9b-214">Packages are also deployed when a node is rebooted or reimaged.</span><span class="sxs-lookup"><span data-stu-id="26c9b-214">Packages are also deployed when a node is rebooted or reimaged.</span></span>

<span data-ttu-id="26c9b-215">Specify the `--app-package-ref` option when creating a pool to deploy an application package to the pool's nodes as they join the pool.</span><span class="sxs-lookup"><span data-stu-id="26c9b-215">Specify the `--app-package-ref` option when creating a pool to deploy an application package to the pool's nodes as they join the pool.</span></span> <span data-ttu-id="26c9b-216">The `--app-package-ref` option accepts a semicolon-delimited list of application ids to deploy to the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="26c9b-216">The `--app-package-ref` option accepts a semicolon-delimited list of application ids to deploy to the compute nodes.</span></span>

    azure batch pool create --pool-id "pool001" --target-dedicated 1 --vm-size "small" --os-family "4" --app-package-ref "MyTaskApplication"

<span data-ttu-id="26c9b-217">When you create a pool by using command-line options, you cannot currently specify *which* application package version to deploy to the compute nodes, for example "1.10-beta3".</span><span class="sxs-lookup"><span data-stu-id="26c9b-217">When you create a pool by using command-line options, you cannot currently specify *which* application package version to deploy to the compute nodes, for example "1.10-beta3".</span></span> <span data-ttu-id="26c9b-218">Therefore, you must first specify a default version for the application with `azure batch application set [options] --default-version <version-id>` before you create the pool (see previous section).</span><span class="sxs-lookup"><span data-stu-id="26c9b-218">Therefore, you must first specify a default version for the application with `azure batch application set [options] --default-version <version-id>` before you create the pool (see previous section).</span></span> <span data-ttu-id="26c9b-219">You can, however, specify a package version for the pool if you use a [JSON file](#json-files) instead of command line options when you create the pool.</span><span class="sxs-lookup"><span data-stu-id="26c9b-219">You can, however, specify a package version for the pool if you use a [JSON file](#json-files) instead of command line options when you create the pool.</span></span>

<span data-ttu-id="26c9b-220">You can find more information on application packages in [Application deployment with Azure Batch application packages](batch-application-packages.md).</span><span class="sxs-lookup"><span data-stu-id="26c9b-220">You can find more information on application packages in [Application deployment with Azure Batch application packages](batch-application-packages.md).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26c9b-221">You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.</span><span class="sxs-lookup"><span data-stu-id="26c9b-221">You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.</span></span>
> 
> 

### <a name="update-a-pools-application-packages"></a><span data-ttu-id="26c9b-222">Update a pool's application packages</span><span class="sxs-lookup"><span data-stu-id="26c9b-222">Update a pool's application packages</span></span>
<span data-ttu-id="26c9b-223">To update the applications assigned to an existing pool, issue the `azure batch pool set` command with the `--app-package-ref` option:</span><span class="sxs-lookup"><span data-stu-id="26c9b-223">To update the applications assigned to an existing pool, issue the `azure batch pool set` command with the `--app-package-ref` option:</span></span>

    azure batch pool set --pool-id "pool001" --app-package-ref "MyTaskApplication2"

<span data-ttu-id="26c9b-224">To deploy the new application package to compute nodes already in an existing pool, you must restart or reimage those nodes:</span><span class="sxs-lookup"><span data-stu-id="26c9b-224">To deploy the new application package to compute nodes already in an existing pool, you must restart or reimage those nodes:</span></span>

    azure batch node reboot --pool-id "pool001" --node-id "tvm-3105992504_1-20160930t164509z"

> [!TIP]
> <span data-ttu-id="26c9b-225">You can obtain a list of the nodes in a pool, along with their node ids, with `azure batch node list`.</span><span class="sxs-lookup"><span data-stu-id="26c9b-225">You can obtain a list of the nodes in a pool, along with their node ids, with `azure batch node list`.</span></span>
> 
> 

<span data-ttu-id="26c9b-226">Keep in mind that you must already have configured the application with a default version prior to deployment (`azure batch application set [options] --default-version <version-id>`).</span><span class="sxs-lookup"><span data-stu-id="26c9b-226">Keep in mind that you must already have configured the application with a default version prior to deployment (`azure batch application set [options] --default-version <version-id>`).</span></span>

## <a name="troubleshooting-tips"></a><span data-ttu-id="26c9b-227">Troubleshooting tips</span><span class="sxs-lookup"><span data-stu-id="26c9b-227">Troubleshooting tips</span></span>
<span data-ttu-id="26c9b-228">This section is intended to provide you with resources to use when troubleshooting Azure CLI issues.</span><span class="sxs-lookup"><span data-stu-id="26c9b-228">This section is intended to provide you with resources to use when troubleshooting Azure CLI issues.</span></span> <span data-ttu-id="26c9b-229">It won't necessarily solve all problems, but it may help you narrow down the cause and point you to help resources.</span><span class="sxs-lookup"><span data-stu-id="26c9b-229">It won't necessarily solve all problems, but it may help you narrow down the cause and point you to help resources.</span></span>

* <span data-ttu-id="26c9b-230">Use `-h` to get **help text** for any CLI command</span><span class="sxs-lookup"><span data-stu-id="26c9b-230">Use `-h` to get **help text** for any CLI command</span></span>
* <span data-ttu-id="26c9b-231">Use `-v` and `-vv` to display **verbose** command output; `-vv` is "extra" verbose and displays the actual REST requests and responses.</span><span class="sxs-lookup"><span data-stu-id="26c9b-231">Use `-v` and `-vv` to display **verbose** command output; `-vv` is "extra" verbose and displays the actual REST requests and responses.</span></span> <span data-ttu-id="26c9b-232">These switches are handy for displaying full error output.</span><span class="sxs-lookup"><span data-stu-id="26c9b-232">These switches are handy for displaying full error output.</span></span>
* <span data-ttu-id="26c9b-233">You can view **command output as JSON** with the `--json` option.</span><span class="sxs-lookup"><span data-stu-id="26c9b-233">You can view **command output as JSON** with the `--json` option.</span></span> <span data-ttu-id="26c9b-234">For example, `azure batch pool show "pool001" --json` displays pool001's properties in JSON format.</span><span class="sxs-lookup"><span data-stu-id="26c9b-234">For example, `azure batch pool show "pool001" --json` displays pool001's properties in JSON format.</span></span> <span data-ttu-id="26c9b-235">You can then copy and modify this output to use in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span><span class="sxs-lookup"><span data-stu-id="26c9b-235">You can then copy and modify this output to use in a `--json-file` (see [JSON files](#json-files) earlier in this article).</span></span>
* <span data-ttu-id="26c9b-236">The [Batch forum on MSDN][batch_forum] is a great help resource, and is monitored closely by Batch team members.</span><span class="sxs-lookup"><span data-stu-id="26c9b-236">The [Batch forum on MSDN][batch_forum] is a great help resource, and is monitored closely by Batch team members.</span></span> <span data-ttu-id="26c9b-237">Be sure to post your questions there if you run into issues or would like help with a specific operation.</span><span class="sxs-lookup"><span data-stu-id="26c9b-237">Be sure to post your questions there if you run into issues or would like help with a specific operation.</span></span>
* <span data-ttu-id="26c9b-238">Not every Batch resource operation is currently supported by the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="26c9b-238">Not every Batch resource operation is currently supported by the Azure CLI.</span></span> <span data-ttu-id="26c9b-239">For example, you can't currently specify an application package *version* for a pool, only the package ID.</span><span class="sxs-lookup"><span data-stu-id="26c9b-239">For example, you can't currently specify an application package *version* for a pool, only the package ID.</span></span> <span data-ttu-id="26c9b-240">In such cases, you may need to supply a `--json-file` for your command instead of using command-line options.</span><span class="sxs-lookup"><span data-stu-id="26c9b-240">In such cases, you may need to supply a `--json-file` for your command instead of using command-line options.</span></span> <span data-ttu-id="26c9b-241">Be sure to stay up-to-date with the latest CLI version to pick up future enhancements.</span><span class="sxs-lookup"><span data-stu-id="26c9b-241">Be sure to stay up-to-date with the latest CLI version to pick up future enhancements.</span></span>

## <a name="next-steps"></a><span data-ttu-id="26c9b-242">Next steps</span><span class="sxs-lookup"><span data-stu-id="26c9b-242">Next steps</span></span>
* <span data-ttu-id="26c9b-243">See [Application deployment with Azure Batch application packages](batch-application-packages.md) to find out how to use this feature to manage and deploy the applications you execute on Batch compute nodes.</span><span class="sxs-lookup"><span data-stu-id="26c9b-243">See [Application deployment with Azure Batch application packages](batch-application-packages.md) to find out how to use this feature to manage and deploy the applications you execute on Batch compute nodes.</span></span>
* <span data-ttu-id="26c9b-244">See [Query the Batch service efficiently](batch-efficient-list-queries.md) for more about reducing the number of items and the type of information that is returned for queries to Batch.</span><span class="sxs-lookup"><span data-stu-id="26c9b-244">See [Query the Batch service efficiently](batch-efficient-list-queries.md) for more about reducing the number of items and the type of information that is returned for queries to Batch.</span></span>

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
