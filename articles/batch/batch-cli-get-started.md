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
# <a name="manage-batch-resources-with-azure-cli"></a>Manage Batch resources with Azure CLI

The cross-platform Azure Command-Line Interface (Azure CLI) enables you to manage your Batch accounts and resources such as pools, jobs, and tasks in Linux, Mac, and Windows command shells. With the Azure CLI, you can perform and script many of the same tasks you carry out with the Batch APIs, Azure portal, and Batch PowerShell cmdlets.

This article is based on Azure CLI version 0.10.5.

## <a name="prerequisites"></a>Prerequisites
* [Install the Azure CLI](../cli-install-nodejs.md)
* [Connect the Azure CLI to your Azure subscription](../xplat-cli-connect.md)
* Switch to **Resource Manager mode**: `azure config mode arm`

> [!TIP]
> We recommend that you update your Azure CLI installation frequently to take advantage of service updates and enhancements.
> 
> 

## <a name="command-help"></a>Command help
You can display help text for every command in the Azure CLI by appending `-h` as the only option after the command. For example:

* To get help for the `azure` command, enter: `azure -h`
* To get a list of all Batch commands in the CLI, use: `azure batch -h`
* To get help on creating a Batch account, enter: `azure batch account create -h`

When in doubt, use the `-h` command-line option to get help on any Azure CLI command.

## <a name="create-a-batch-account"></a>Create a Batch account
Usage:

    azure batch account create [options] <name>

Example:

    azure batch account create --location "West US"  --resource-group "resgroup001" "batchaccount001"

Creates a new Batch account with the specified parameters. You must specify at least a location, resource group, and account name. If you don't already have a resource group, create one by running `azure group create`, and specify one of the Azure regions (such as "West US") for the `--location` option. For example:

    azure group create --name "resgroup001" --location "West US"

> [!NOTE]
> The Batch account name must be unique within the Azure region the account is created. It may contain only lowercase alphanumeric characters, and must be 3-24 characters in length. You can't use special characters like `-` or `_` in Batch account names.
> 
> 

### <a name="linked-storage-account-autostorage"></a>Linked storage account (autostorage)
You can (optionally) link a **General purpose** Storage account to your Batch account when you create it. The [application packages](batch-application-packages.md) feature of Batch uses blob storage in a linked General purpose Storage account, as does the [Batch File Conventions .NET](batch-task-output.md) library. These optional features assist you in deploying the applications your Batch tasks run, and persisting the data they produce.

To link an existing Azure Storage account to a new Batch account when you create it, specify the `--autostorage-account-id` option. This option requires the fully qualified resource ID of the storage account.

First, show your storage account's details:

    azure storage account show --resource-group "resgroup001" "storageaccount001"

Then use the **Url** value for the `--autostorage-account-id` option. The Url value starts with "/subscriptions/" and contains your subscription ID and resource path to the Storage account:

    azure batch account create --location "West US"  --resource-group "resgroup001" --autostorage-account-id "/subscriptions/8ffffff8-4444-4444-bfbf-8ffffff84444/resourceGroups/resgroup001/providers/Microsoft.Storage/storageAccounts/storageaccount001" "batchaccount001"

## <a name="delete-a-batch-account"></a>Delete a Batch account
Usage:

    azure batch account delete [options] <name>

Example:

    azure batch account delete --resource-group "resgroup001" "batchaccount001"

Deletes the specified Batch account. When prompted, confirm you want to remove the account (account removal can take some time to complete).

## <a name="manage-account-access-keys"></a>Manage account access keys
You need an access key to [create and modify resources](#create-and-modify-batch-resources) in your Batch account.

### <a name="list-access-keys"></a>List access keys
Usage:

    azure batch account keys list [options] <name>

Example:

    azure batch account keys list --resource-group "resgroup001" "batchaccount001"

Lists the account keys for the given Batch account.

### <a name="generate-a-new-access-key"></a>Generate a new access key
Usage:

    azure batch account keys renew [options] --<primary|secondary> <name>

Example:

    azure batch account keys renew --resource-group "resgroup001" --primary "batchaccount001"

Regenerates the specified account key for the given Batch account.

## <a name="create-and-modify-batch-resources"></a>Create and modify Batch resources
You can use the Azure CLI to create, read, update, and delete (CRUD) Batch resources like pools, compute nodes, jobs, and tasks. These CRUD operations require your Batch account name, access key, and endpoint. You can specify these with the `-a`, `-k`, and `-u` options, or set [environment variables](#credential-environment-variables) which the CLI uses automatically (if populated).

### <a name="credential-environment-variables"></a>Credential environment variables
You can set `AZURE_BATCH_ACCOUNT`, `AZURE_BATCH_ACCESS_KEY`, and `AZURE_BATCH_ENDPOINT` environment variables instead of specifying `-a`, `-k`, and `-u` options on the command line for every command you execute. The Batch CLI uses these variables (if set) so that you can omit the `-a`, `-k`, and `-u` options. The remainder of this article assumes use of these environment variables.

> [!TIP]
> List your keys with `azure batch account keys list`, and display the account's endpoint with `azure batch account show`.
> 
> 

### <a name="json-files"></a>JSON files
When you create Batch resources like pools and jobs, you can specify a JSON file containing the new resource's configuration instead of passing its parameters as command-line options. For example:

`azure batch pool create my_batch_pool.json`

While you can perform many resource creation operations using only command-line options, some features require a JSON-formatted file containing the resource details. For example, you must use a JSON file if you want to specify resource files for a start task.

To find the JSON required to create a resource, refer to the [Batch REST API reference][rest_api] documentation on MSDN. Each "Add *resource type*" topic contains example JSON for creating the resource, which you can use as templates for your JSON files. For example, JSON for pool creation can be found in [Add a pool to an account][rest_add_pool].

> [!NOTE]
> If you specify a JSON file when you create a resource, all other parameters that you specify on the command line for that resource are ignored.
> 
> 

## <a name="create-a-pool"></a>Create a pool
Usage:

    azure batch pool create [options] [json-file]

Example (Virtual Machine Configuration):

    azure batch pool create --id "pool001" --target-dedicated 1 --vm-size "STANDARD_A1" --image-publisher "Canonical" --image-offer "UbuntuServer" --image-sku "14.04.2-LTS" --node-agent-id "batch.node.ubuntu 14.04"

Example (Cloud Services Configuration):

    azure batch pool create --id "pool002" --target-dedicated 1 --vm-size "small" --os-family "4"

Creates a pool of compute nodes in the Batch service.

As mentioned in the [Batch feature overview](batch-api-basics.md#pool), you have two options when you select an operating system for the nodes in your pool: **Virtual Machine Configuration** and **Cloud Services Configuration**. Use the `--image-*` options to create Virtual Machine Configuration pools, and `--os-family` to create Cloud Services Configuration pools. You can't specify both `--os-family` and `--image-*` options.

You can specify pool [application packages](batch-application-packages.md) and the command line for a [start task](batch-api-basics.md#start-task). To specify resource files for the start task, however, you must instead use a [JSON file](#json-files).

Delete a pool with:

    azure batch pool delete [pool-id]

> [!TIP]
> Check the [list of virtual machine images](batch-linux-nodes.md#list-of-virtual-machine-images) for values appropriate for the `--image-*` options.
> 
> 

## <a name="create-a-job"></a>Create a job
Usage:

    azure batch job create [options] [json-file]

Example:

    azure batch job create --id "job001" --pool-id "pool001"

Adds a job to the Batch account and specifies the pool on which its tasks execute.

Delete a job with:

    azure batch job delete [job-id]

## <a name="list-pools-jobs-tasks-and-other-resources"></a>List pools, jobs, tasks, and other resources
Each Batch resource type supports a `list` command that queries your Batch account and lists resources of that type. For example, you can list the pools in your account and the tasks in a job:

    azure batch pool list
    azure batch task list --job-id "job001"

### <a name="listing-resources-efficiently"></a>Listing resources efficiently
For faster querying, you can specify **select**, **filter**, and **expand** clause options for `list` operations. Use these options to limit the amount of data returned by the Batch service. Because all filtering occurs server-side, only the data you are interested in crosses the wire. Use these clauses to save bandwidth (and therefore time) when you perform list operations.

For example, this will return only pools whose ids start with "renderTask":

    azure batch task list --job-id "job001" --filter-clause "startswith(id, 'renderTask')"

The Batch CLI supports all three clauses supported by the Batch service:

* `--select-clause [select-clause]`  Return a subset of properties for each entity
* `--filter-clause [filter-clause]`  Return only entities that match the specified OData expression
* `--expand-clause [expand-clause]`  Obtain the entity information in a single underlying REST call. The expand clause supports only the `stats` property at this time.

For details on the three clauses and performing list queries with them, see [Query the Azure Batch service efficiently](batch-efficient-list-queries.md).

## <a name="application-package-management"></a>Application package management
Application packages provide a simplified way to deploy applications to the compute nodes in your pools. With the Azure CLI, you can upload application packages, manage package versions, and delete packages.

To create a new application and add a package version:

**Create** an application:

    azure batch application create "resgroup001" "batchaccount001" "MyTaskApplication"

**Add** an application package:

    azure batch application package create "resgroup001" "batchaccount001" "MyTaskApplication" "1.10-beta3" package001.zip

**Activate** the package:

    azure batch application package activate "resgroup001" "batchaccount001" "MyTaskApplication" "1.10-beta3" zip

Set the **default version** for the application:

    azure batch application set "resgroup001" "batchaccount001" "MyTaskApplication" --default-version "1.10-beta3"

### <a name="deploy-an-application-package"></a>Deploy an application package
You can specify one or more application packages for deployment when you create a new pool. When you specify a package at pool creation time, it is deployed to each node as the node joins pool. Packages are also deployed when a node is rebooted or reimaged.

Specify the `--app-package-ref` option when creating a pool to deploy an application package to the pool's nodes as they join the pool. The `--app-package-ref` option accepts a semicolon-delimited list of application ids to deploy to the compute nodes.

    azure batch pool create --pool-id "pool001" --target-dedicated 1 --vm-size "small" --os-family "4" --app-package-ref "MyTaskApplication"

When you create a pool by using command-line options, you cannot currently specify *which* application package version to deploy to the compute nodes, for example "1.10-beta3". Therefore, you must first specify a default version for the application with `azure batch application set [options] --default-version <version-id>` before you create the pool (see previous section). You can, however, specify a package version for the pool if you use a [JSON file](#json-files) instead of command line options when you create the pool.

You can find more information on application packages in [Application deployment with Azure Batch application packages](batch-application-packages.md).

> [!IMPORTANT]
> You must [link an Azure Storage account](#linked-storage-account-autostorage) to your Batch account to use application packages.
> 
> 

### <a name="update-a-pools-application-packages"></a>Update a pool's application packages
To update the applications assigned to an existing pool, issue the `azure batch pool set` command with the `--app-package-ref` option:

    azure batch pool set --pool-id "pool001" --app-package-ref "MyTaskApplication2"

To deploy the new application package to compute nodes already in an existing pool, you must restart or reimage those nodes:

    azure batch node reboot --pool-id "pool001" --node-id "tvm-3105992504_1-20160930t164509z"

> [!TIP]
> You can obtain a list of the nodes in a pool, along with their node ids, with `azure batch node list`.
> 
> 

Keep in mind that you must already have configured the application with a default version prior to deployment (`azure batch application set [options] --default-version <version-id>`).

## <a name="troubleshooting-tips"></a>Troubleshooting tips
This section is intended to provide you with resources to use when troubleshooting Azure CLI issues. It won't necessarily solve all problems, but it may help you narrow down the cause and point you to help resources.

* Use `-h` to get **help text** for any CLI command
* Use `-v` and `-vv` to display **verbose** command output; `-vv` is "extra" verbose and displays the actual REST requests and responses. These switches are handy for displaying full error output.
* You can view **command output as JSON** with the `--json` option. For example, `azure batch pool show "pool001" --json` displays pool001's properties in JSON format. You can then copy and modify this output to use in a `--json-file` (see [JSON files](#json-files) earlier in this article).
* The [Batch forum on MSDN][batch_forum] is a great help resource, and is monitored closely by Batch team members. Be sure to post your questions there if you run into issues or would like help with a specific operation.
* Not every Batch resource operation is currently supported by the Azure CLI. For example, you can't currently specify an application package *version* for a pool, only the package ID. In such cases, you may need to supply a `--json-file` for your command instead of using command-line options. Be sure to stay up-to-date with the latest CLI version to pick up future enhancements.

## <a name="next-steps"></a>Next steps
* See [Application deployment with Azure Batch application packages](batch-application-packages.md) to find out how to use this feature to manage and deploy the applications you execute on Batch compute nodes.
* See [Query the Batch service efficiently](batch-efficient-list-queries.md) for more about reducing the number of items and the type of information that is returned for queries to Batch.

[batch_forum]: https://social.msdn.microsoft.com/forums/azure/en-US/home?forum=azurebatch
[github_readme]: https://github.com/Azure/azure-xplat-cli/blob/dev/README.md
[rest_api]: https://msdn.microsoft.com/library/azure/dn820158.aspx
[rest_add_pool]: https://msdn.microsoft.com/library/azure/dn820174.aspx
