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
# <a name="create-a-private-docker-container-registry-using-the-azure-cli-20"></a><span data-ttu-id="ffc5d-103">Create a private Docker container registry using the Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="ffc5d-103">Create a private Docker container registry using the Azure CLI 2.0</span></span>
<span data-ttu-id="ffc5d-104">Use commands in the [Azure CLI 2.0](https://github.com/Azure/azure-cli) to create a container registry and manage its settings from your Linux, Mac, or Windows computer.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-104">Use commands in the [Azure CLI 2.0](https://github.com/Azure/azure-cli) to create a container registry and manage its settings from your Linux, Mac, or Windows computer.</span></span> <span data-ttu-id="ffc5d-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="ffc5d-105">You can also create and manage container registries using the [Azure portal](container-registry-get-started-portal.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>


* <span data-ttu-id="ffc5d-106">For background and concepts, see [the overview](container-registry-intro.md)</span><span class="sxs-lookup"><span data-stu-id="ffc5d-106">For background and concepts, see [the overview](container-registry-intro.md)</span></span>
* <span data-ttu-id="ffc5d-107">For help on Container Registry CLI commands (`az acr` commands), pass the `-h` parameter to any command.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-107">For help on Container Registry CLI commands (`az acr` commands), pass the `-h` parameter to any command.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ffc5d-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ffc5d-108">Prerequisites</span></span>
* <span data-ttu-id="ffc5d-109">**Azure CLI 2.0**: To install and get started with the CLI 2.0, see the [installation instructions](/cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ffc5d-109">**Azure CLI 2.0**: To install and get started with the CLI 2.0, see the [installation instructions](/cli/azure/install-azure-cli).</span></span> <span data-ttu-id="ffc5d-110">Log in to your Azure subscription by running `az login`.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-110">Log in to your Azure subscription by running `az login`.</span></span> <span data-ttu-id="ffc5d-111">For more information, see [Get started with the CLI 2.0](/cli/azure/get-started-with-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="ffc5d-111">For more information, see [Get started with the CLI 2.0](/cli/azure/get-started-with-azure-cli).</span></span>
* <span data-ttu-id="ffc5d-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-112">**Resource group**: Create a [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) before creating a container registry, or use an existing resource group.</span></span> <span data-ttu-id="ffc5d-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="ffc5d-113">Make sure the resource group is in a location where the Container Registry service is [available](https://azure.microsoft.com/regions/services/).</span></span> <span data-ttu-id="ffc5d-114">To create a resource group using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/group).</span><span class="sxs-lookup"><span data-stu-id="ffc5d-114">To create a resource group using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/group).</span></span>
* <span data-ttu-id="ffc5d-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/storage-introduction.md) to back the container registry in the same location.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-115">**Storage account** (optional): Create a standard Azure [storage account](../storage/storage-introduction.md) to back the container registry in the same location.</span></span> <span data-ttu-id="ffc5d-116">If you don't specify a storage account when creating a registry with `az acr create`, the command creates one for you.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-116">If you don't specify a storage account when creating a registry with `az acr create`, the command creates one for you.</span></span> <span data-ttu-id="ffc5d-117">To create a storage account using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/storage/account).</span><span class="sxs-lookup"><span data-stu-id="ffc5d-117">To create a storage account using the CLI 2.0, see [the CLI 2.0 reference](/cli/azure/storage/account).</span></span> <span data-ttu-id="ffc5d-118">Currently Premium Storage is not supported.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-118">Currently Premium Storage is not supported.</span></span>
* <span data-ttu-id="ffc5d-119">**Service principal** (optional): When you create a registry with the CLI, by default it is not set up for access.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-119">**Service principal** (optional): When you create a registry with the CLI, by default it is not set up for access.</span></span> <span data-ttu-id="ffc5d-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry (or create and assign a new one), or enable the registry's admin user account.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-120">Depending on your needs, you can assign an existing Azure Active Directory service principal to a registry (or create and assign a new one), or enable the registry's admin user account.</span></span> <span data-ttu-id="ffc5d-121">See the sections later in this article.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-121">See the sections later in this article.</span></span> <span data-ttu-id="ffc5d-122">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ffc5d-122">For more information about registry access, see [Authenticate with the container registry](container-registry-authentication.md).</span></span>

## <a name="create-a-container-registry"></a><span data-ttu-id="ffc5d-123">Create a container registry</span><span class="sxs-lookup"><span data-stu-id="ffc5d-123">Create a container registry</span></span>
<span data-ttu-id="ffc5d-124">Run the `az acr create` command to create a container registry.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-124">Run the `az acr create` command to create a container registry.</span></span>

> [!TIP]
> <span data-ttu-id="ffc5d-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-125">When you create a registry, specify a globally unique top-level domain name, containing only letters and numbers.</span></span> <span data-ttu-id="ffc5d-126">The registry name in the examples is `myRegistry1`, but substitute a unique name of your own.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-126">The registry name in the examples is `myRegistry1`, but substitute a unique name of your own.</span></span>
>
>

<span data-ttu-id="ffc5d-127">The following command uses the minimal parameters to create container registry `myRegistry1` in the resource group `myResourceGroup` in the South Central US location:</span><span class="sxs-lookup"><span data-stu-id="ffc5d-127">The following command uses the minimal parameters to create container registry `myRegistry1` in the resource group `myResourceGroup` in the South Central US location:</span></span>

```azurecli
az acr create -n myRegistry1 -g myResourceGroup -l southcentralus
```

* <span data-ttu-id="ffc5d-128">`--storage-account-name` is optional.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-128">`--storage-account-name` is optional.</span></span> <span data-ttu-id="ffc5d-129">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-129">If not specified, a storage account is created with a name consisting of the registry name and a timestamp in the specified resource group.</span></span>

<span data-ttu-id="ffc5d-130">The output is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="ffc5d-130">The output is similar to the following:</span></span>

![az acr create output](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-registry/media/container-registry-get-started-azure-cli/acr_create.png)


<span data-ttu-id="ffc5d-132">Take special note:</span><span class="sxs-lookup"><span data-stu-id="ffc5d-132">Take special note:</span></span>

* <span data-ttu-id="ffc5d-133">`id` - Identifier for the registry in your subscription, which you need if you want to assign a service principal.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-133">`id` - Identifier for the registry in your subscription, which you need if you want to assign a service principal.</span></span>
* <span data-ttu-id="ffc5d-134">`loginServer` - The fully qualified name you specify to [log in to the registry](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="ffc5d-134">`loginServer` - The fully qualified name you specify to [log in to the registry](container-registry-authentication.md).</span></span> <span data-ttu-id="ffc5d-135">In this example, the name is `myregistry1.exp.azurecr.io` (all lowercase).</span><span class="sxs-lookup"><span data-stu-id="ffc5d-135">In this example, the name is `myregistry1.exp.azurecr.io` (all lowercase).</span></span>

## <a name="assign-a-service-principal"></a><span data-ttu-id="ffc5d-136">Assign a service principal</span><span class="sxs-lookup"><span data-stu-id="ffc5d-136">Assign a service principal</span></span>
<span data-ttu-id="ffc5d-137">Use CLI 2.0 commands to assign an Azure Active Directory service principal to a registry.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-137">Use CLI 2.0 commands to assign an Azure Active Directory service principal to a registry.</span></span> <span data-ttu-id="ffc5d-138">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-138">The service principal in these examples is assigned the Owner role, but you can assign [other roles](../active-directory/role-based-access-control-configure.md) if you want.</span></span>

### <a name="create-a-service-principal-and-assign-access-to-the-registry"></a><span data-ttu-id="ffc5d-139">Create a service principal and assign access to the registry</span><span class="sxs-lookup"><span data-stu-id="ffc5d-139">Create a service principal and assign access to the registry</span></span>
<span data-ttu-id="ffc5d-140">In the following command, a new service principal is assigned Owner role access to the registry identifier passed with the `--scopes` parameter.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-140">In the following command, a new service principal is assigned Owner role access to the registry identifier passed with the `--scopes` parameter.</span></span> <span data-ttu-id="ffc5d-141">Specify a strong password with the `--password` parameter.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-141">Specify a strong password with the `--password` parameter.</span></span>

```azurecli
az ad sp create-for-rbac --scopes /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --password myPassword
```



### <a name="assign-an-existing-service-principal"></a><span data-ttu-id="ffc5d-142">Assign an existing service principal</span><span class="sxs-lookup"><span data-stu-id="ffc5d-142">Assign an existing service principal</span></span>
<span data-ttu-id="ffc5d-143">If you already have a service principal and want to assign it Owner role access to the registry, run a command similar to the following example.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-143">If you already have a service principal and want to assign it Owner role access to the registry, run a command similar to the following example.</span></span> <span data-ttu-id="ffc5d-144">You pass the service principal app ID using the `--assignee` parameter:</span><span class="sxs-lookup"><span data-stu-id="ffc5d-144">You pass the service principal app ID using the `--assignee` parameter:</span></span>

```azurecli
az role assignment create --scope /subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myregistry1 --role Owner --assignee myAppId
```



## <a name="manage-admin-credentials"></a><span data-ttu-id="ffc5d-145">Manage admin credentials</span><span class="sxs-lookup"><span data-stu-id="ffc5d-145">Manage admin credentials</span></span>
<span data-ttu-id="ffc5d-146">An admin account is automatically created for each container registry and is disabled by default.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-146">An admin account is automatically created for each container registry and is disabled by default.</span></span> <span data-ttu-id="ffc5d-147">The following examples show `az acr` CLI commands to manage the admin credentials for your container registry.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-147">The following examples show `az acr` CLI commands to manage the admin credentials for your container registry.</span></span>

### <a name="obtain-admin-user-credentials"></a><span data-ttu-id="ffc5d-148">Obtain admin user credentials</span><span class="sxs-lookup"><span data-stu-id="ffc5d-148">Obtain admin user credentials</span></span>
```azurecli
az acr credential show -n myRegistry1
```

### <a name="enable-admin-user-for-an-existing-registry"></a><span data-ttu-id="ffc5d-149">Enable admin user for an existing registry</span><span class="sxs-lookup"><span data-stu-id="ffc5d-149">Enable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled true
```

### <a name="disable-admin-user-for-an-existing-registry"></a><span data-ttu-id="ffc5d-150">Disable admin user for an existing registry</span><span class="sxs-lookup"><span data-stu-id="ffc5d-150">Disable admin user for an existing registry</span></span>
```azurecli
az acr update -n myRegistry1 --admin-enabled false
```

## <a name="list-images-and-tags"></a><span data-ttu-id="ffc5d-151">List images and tags</span><span class="sxs-lookup"><span data-stu-id="ffc5d-151">List images and tags</span></span>
<span data-ttu-id="ffc5d-152">Use the `az acr` CLI commands to query the images and tags in a repository.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-152">Use the `az acr` CLI commands to query the images and tags in a repository.</span></span>

> [!NOTE]
> <span data-ttu-id="ffc5d-153">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span><span class="sxs-lookup"><span data-stu-id="ffc5d-153">Currently, Container Registry does not support the `docker search` command to query for images and tags.</span></span>


### <a name="list-repositories"></a><span data-ttu-id="ffc5d-154">List repositories</span><span class="sxs-lookup"><span data-stu-id="ffc5d-154">List repositories</span></span>
<span data-ttu-id="ffc5d-155">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span><span class="sxs-lookup"><span data-stu-id="ffc5d-155">The following example lists the repositories in a registry, in JSON (JavaScript Object Notation) format:</span></span>

```azurecli
az acr repository list -n myRegistry1 -o json
```

### <a name="list-tags"></a><span data-ttu-id="ffc5d-156">List tags</span><span class="sxs-lookup"><span data-stu-id="ffc5d-156">List tags</span></span>
<span data-ttu-id="ffc5d-157">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span><span class="sxs-lookup"><span data-stu-id="ffc5d-157">The following example lists the tags on the **samples/nginx** repository, in JSON format:</span></span>

```azurecli
az acr repository show-tags -n myRegistry1 --repository samples/nginx -o json
```

## <a name="next-steps"></a><span data-ttu-id="ffc5d-158">Next steps</span><span class="sxs-lookup"><span data-stu-id="ffc5d-158">Next steps</span></span>
* [<span data-ttu-id="ffc5d-159">Push your first image using the Docker CLI</span><span class="sxs-lookup"><span data-stu-id="ffc5d-159">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)

