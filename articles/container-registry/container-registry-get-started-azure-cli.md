---
title: Create private Docker container registry - Azure CLI | Microsoft Docs
description: Get started creating and managing private Docker container registries with the Azure CLI 2.0
services: container-registry
documentationcenter: ''
author: stevelas
manager: balans
editor: cristyg
tags: ''
keywords: ''
ms.assetid: 29e20d75-bf39-4f7d-815f-a2e47209be7d
ms.service: container-registry
ms.devlang: azurecli
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/03/2017
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: dfa3bed38d7df0399fce15908c1ed20132f7ef5a
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44540661"
---
# <a name="create-a-private-docker-container-registry-using-the-azure-cli-20"></a>Create a private Docker container registry using the Azure CLI 2.0
Use commands in the [Azure CLI 2.0](https://github.com/Azure/azure-cli) to create a container registry and manage its settings from your Linux, Mac, or Windows computer. You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).


* For background and concepts, see [the overview](container-registry-intro.md)
* For help on Container Registry CLI commands (`az acr` commands), pass the `-h` parameter to any command.


## <a name="prerequisites"></a>Prerequisites
* **Azure CLI 2.0**: To install and get started with the CLI 2.0, see the [installation instructions](/cli/azure/install-azure-cli). Log in to your Azure subscription by running `az login`. For more information, see [Get started with the CLI 2.0](/cli/azure/get-started-with-azure-cli).
* **Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group. Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/). To create a resource group using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/group).
* **Storage account** (optional): Create a standard Azure [storage account](../storage/storage-introduction.md) to back the container registry in the same location. If you don't specify a storage account when creating a registry with `az acr create`, the command creates one for you. To create a storage account using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/storage/account). Currently Premium Storage is not supported.
* **Service principal** (optional): When you create a registry with the CLI, by default it is not set up for access. Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry (or create and assign a new one), or enable the registry's admin user account. See the sections later in this article. For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).

## <a name="create-a-container-registry"></a>Create a container registry
Run the `az acr create` command to create a container registry.

> [!TIP]
> When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers. The registry name in the examples is `myRegistry1`, but substitute a unique name of your own.
>
>

The following command uses the minimal parameters to create container registry `myRegistry1` in the resource group `myResourceGroup` in the South Central US location:

```azurecli
az acr create -n myRegistry1 -g myResourceGroup -l southcentralus
```

* `--storage-account-name` is optional. If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.

The output is similar to the following:

![az acr create output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-registry/media/container-registry-get-started-azure-cli/acr_create.png)


Take special note:

* `id` - Identifier for the registry in your subscription, which you need if you want to assign a service principal.
* `loginServer` - The fully qualified name you specify to [log in to the registry](container-registry-authentication.md). In this example, the name is `myregistry1.exp.azurecr.io` (all lowercase).

## <a name="assign-a-service-principal"></a>Assign a service principal
Use CLI 2.0 commands to assign an Azure Active Directory service principal to a registry. The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.

### <a name="create-a-service-principal-and-assign-access-to-the-registry"></a>Create a service principal and assign access to the registry
In the following command, a new service principal is assigned Owner role access to the registry identifier passed with the `--scopes` parameter. Specify a strong password with the `--password` parameter.

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a>Assign an existing service principal
If you already have a service principal and want to assign it Owner role access to the registry, run a command similar to the following example. You pass the service principal app ID using the `--assignee` parameter:

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a>Manage admin credentials
An admin account is automatically created for each container registry and is disabled by default. The following examples show `az acr` CLI commands to manage the admin credentials for your container registry.

### <a name="obtain-admin-user-credentials"></a>Obtain admin user credentials
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a>Enable admin user for an existing registry
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a>Disable admin user for an existing registry
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a>List images and tags
Use the `az acr` CLI commands to query the images and tags in a repository.

> [!NOTE]
> Currently, Container Registry does not support the `docker search` command to query for images and tags.


### <a name="list-repositories"></a>List repositories
The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a>List tags
The following example lists the tags on the **samples/nginx** repository, in JSON format:

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a>Next steps
* [Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md)

