---
title: Mount a gitRepo volume Azure Container Instances
description: Learn how to mount a gitRepo volume to clone a Git repository into your container instances
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 06/15/2018
ms.author: marsma
ms.openlocfilehash: 86d85f9f84b8d3ae3c31ff59089ce264d5e3192e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866187"
---
# <a name="mount-a-gitrepo-volume-in-azure-container-instances"></a><span data-ttu-id="ed79f-103">Mount a gitRepo volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="ed79f-103">Mount a gitRepo volume in Azure Container Instances</span></span>

<span data-ttu-id="ed79f-104">Learn how to mount a *gitRepo* volume to clone a Git repository into your container instances.</span><span class="sxs-lookup"><span data-stu-id="ed79f-104">Learn how to mount a *gitRepo* volume to clone a Git repository into your container instances.</span></span>

> [!NOTE]
> <span data-ttu-id="ed79f-105">Mounting a *gitRepo* volume is currently restricted to Linux containers.</span><span class="sxs-lookup"><span data-stu-id="ed79f-105">Mounting a *gitRepo* volume is currently restricted to Linux containers.</span></span> <span data-ttu-id="ed79f-106">While we are working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span><span class="sxs-lookup"><span data-stu-id="ed79f-106">While we are working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span></span>

## <a name="gitrepo-volume"></a><span data-ttu-id="ed79f-107">gitRepo volume</span><span class="sxs-lookup"><span data-stu-id="ed79f-107">gitRepo volume</span></span>

<span data-ttu-id="ed79f-108">The *gitRepo* volume mounts a directory and clones the specified Git repository into it at container startup.</span><span class="sxs-lookup"><span data-stu-id="ed79f-108">The *gitRepo* volume mounts a directory and clones the specified Git repository into it at container startup.</span></span> <span data-ttu-id="ed79f-109">By using a *gitRepo* volume in your container instances, you can avoid adding the code for doing so in your applications.</span><span class="sxs-lookup"><span data-stu-id="ed79f-109">By using a *gitRepo* volume in your container instances, you can avoid adding the code for doing so in your applications.</span></span>

<span data-ttu-id="ed79f-110">When you mount a *gitRepo* volume, you can set three properties to configure the volume:</span><span class="sxs-lookup"><span data-stu-id="ed79f-110">When you mount a *gitRepo* volume, you can set three properties to configure the volume:</span></span>

| <span data-ttu-id="ed79f-111">Property</span><span class="sxs-lookup"><span data-stu-id="ed79f-111">Property</span></span> | <span data-ttu-id="ed79f-112">Required</span><span class="sxs-lookup"><span data-stu-id="ed79f-112">Required</span></span> | <span data-ttu-id="ed79f-113">Description</span><span class="sxs-lookup"><span data-stu-id="ed79f-113">Description</span></span> |
| -------- | -------- | ----------- |
| `repository` | <span data-ttu-id="ed79f-114">Yes</span><span class="sxs-lookup"><span data-stu-id="ed79f-114">Yes</span></span> | <span data-ttu-id="ed79f-115">The full URL, including `http://` or `https://`, of the Git repository to be cloned.</span><span class="sxs-lookup"><span data-stu-id="ed79f-115">The full URL, including `http://` or `https://`, of the Git repository to be cloned.</span></span>|
| `directory` | <span data-ttu-id="ed79f-116">No</span><span class="sxs-lookup"><span data-stu-id="ed79f-116">No</span></span> | <span data-ttu-id="ed79f-117">Directory into which the repository should be cloned.</span><span class="sxs-lookup"><span data-stu-id="ed79f-117">Directory into which the repository should be cloned.</span></span> <span data-ttu-id="ed79f-118">The path must not contain or start with "`..`".</span><span class="sxs-lookup"><span data-stu-id="ed79f-118">The path must not contain or start with "`..`".</span></span>  <span data-ttu-id="ed79f-119">If you specify "`.`", the repository is cloned into the volume's directory.</span><span class="sxs-lookup"><span data-stu-id="ed79f-119">If you specify "`.`", the repository is cloned into the volume's directory.</span></span> <span data-ttu-id="ed79f-120">Otherwise, the Git repository is cloned into a subdirectory of the given name within the volume directory.</span><span class="sxs-lookup"><span data-stu-id="ed79f-120">Otherwise, the Git repository is cloned into a subdirectory of the given name within the volume directory.</span></span> |
| `revision` | <span data-ttu-id="ed79f-121">No</span><span class="sxs-lookup"><span data-stu-id="ed79f-121">No</span></span> | <span data-ttu-id="ed79f-122">The commit hash of the revision to be cloned.</span><span class="sxs-lookup"><span data-stu-id="ed79f-122">The commit hash of the revision to be cloned.</span></span> <span data-ttu-id="ed79f-123">If unspecified, the `HEAD` revision is cloned.</span><span class="sxs-lookup"><span data-stu-id="ed79f-123">If unspecified, the `HEAD` revision is cloned.</span></span> |

## <a name="mount-gitrepo-volume-azure-cli"></a><span data-ttu-id="ed79f-124">Mount gitRepo volume: Azure CLI</span><span class="sxs-lookup"><span data-stu-id="ed79f-124">Mount gitRepo volume: Azure CLI</span></span>

<span data-ttu-id="ed79f-125">To mount a gitRepo volume when you deploy container instances with the [Azure CLI](/cli/azure), supply the `--gitrepo-url` and `--gitrepo-mount-path` parameters to the [az container create][az-container-create] command.</span><span class="sxs-lookup"><span data-stu-id="ed79f-125">To mount a gitRepo volume when you deploy container instances with the [Azure CLI](/cli/azure), supply the `--gitrepo-url` and `--gitrepo-mount-path` parameters to the [az container create][az-container-create] command.</span></span> <span data-ttu-id="ed79f-126">You can optionally specify the directory within the volume to clone into (`--gitrepo-dir`) and the commit hash of the revision to be cloned (`--gitrepo-revision`).</span><span class="sxs-lookup"><span data-stu-id="ed79f-126">You can optionally specify the directory within the volume to clone into (`--gitrepo-dir`) and the commit hash of the revision to be cloned (`--gitrepo-revision`).</span></span>

<span data-ttu-id="ed79f-127">This example command clones the [aci-helloworld][aci-helloworld] sample application into `/mnt/aci-helloworld` in the container instance:</span><span class="sxs-lookup"><span data-stu-id="ed79f-127">This example command clones the [aci-helloworld][aci-helloworld] sample application into `/mnt/aci-helloworld` in the container instance:</span></span>

```azurecli-interactive
az container create \
    --resource-group myResourceGroup \
    --name hellogitrepo \
    --image microsoft/aci-helloworld \
    --dns-name-label aci-demo \
    --ports 80 \
    --gitrepo-url https://github.com/Azure-Samples/aci-helloworld \
    --gitrepo-mount-path /mnt/aci-helloworld
```

<span data-ttu-id="ed79f-128">To verify the gitRepo volume was mounted, launch a shell in the container with [az container exec][az-container-exec] and list the directory:</span><span class="sxs-lookup"><span data-stu-id="ed79f-128">To verify the gitRepo volume was mounted, launch a shell in the container with [az container exec][az-container-exec] and list the directory:</span></span>

```console
$ az container exec --resource-group myResourceGroup --name hellogitrepo --exec-command /bin/sh
/usr/src/app # ls -l /mnt/aci-helloworld/
total 16
-rw-r--r--    1 root     root           144 Apr 16 16:35 Dockerfile
-rw-r--r--    1 root     root          1162 Apr 16 16:35 LICENSE
-rw-r--r--    1 root     root          1237 Apr 16 16:35 README.md
drwxr-xr-x    2 root     root          4096 Apr 16 16:35 app
```

## <a name="mount-gitrepo-volume-resource-manager"></a><span data-ttu-id="ed79f-129">Mount gitRepo volume: Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ed79f-129">Mount gitRepo volume: Resource Manager</span></span>

<span data-ttu-id="ed79f-130">To mount a gitRepo volume when you deploy container instances with an [Azure Resource Manager template](/azure/templates/microsoft.containerinstance/containergroups), first populate the `volumes` array in the container group `properties` section of the template.</span><span class="sxs-lookup"><span data-stu-id="ed79f-130">To mount a gitRepo volume when you deploy container instances with an [Azure Resource Manager template](/azure/templates/microsoft.containerinstance/containergroups), first populate the `volumes` array in the container group `properties` section of the template.</span></span> <span data-ttu-id="ed79f-131">Then, for each container in the container group in which you'd like to mount the *gitRepo* volume, populate the `volumeMounts` array in the `properties` section of the container definition.</span><span class="sxs-lookup"><span data-stu-id="ed79f-131">Then, for each container in the container group in which you'd like to mount the *gitRepo* volume, populate the `volumeMounts` array in the `properties` section of the container definition.</span></span>

<span data-ttu-id="ed79f-132">For example, the following Resource Manager template creates a container group consisting of a single container.</span><span class="sxs-lookup"><span data-stu-id="ed79f-132">For example, the following Resource Manager template creates a container group consisting of a single container.</span></span> <span data-ttu-id="ed79f-133">The container clones two GitHub repositories specified by the *gitRepo* volume blocks.</span><span class="sxs-lookup"><span data-stu-id="ed79f-133">The container clones two GitHub repositories specified by the *gitRepo* volume blocks.</span></span> <span data-ttu-id="ed79f-134">The second volume includes additional properties specifying a directory to clone to, and the commit hash of a specific revision to clone.</span><span class="sxs-lookup"><span data-stu-id="ed79f-134">The second volume includes additional properties specifying a directory to clone to, and the commit hash of a specific revision to clone.</span></span>

<span data-ttu-id="ed79f-135"><!-- https://github.com/Azure/azure-docs-json-samples/blob/master/container-instances/aci-deploy-volume-gitrepo.json --> [!code-json[volume-gitrepo](~/azure-docs-json-samples/container-instances/aci-deploy-volume-gitrepo.json)]</span><span class="sxs-lookup"><span data-stu-id="ed79f-135"><!-- https://github.com/Azure/azure-docs-json-samples/blob/master/container-instances/aci-deploy-volume-gitrepo.json --> [!code-json[volume-gitrepo](~/azure-docs-json-samples/container-instances/aci-deploy-volume-gitrepo.json)]</span></span>

<span data-ttu-id="ed79f-136">The resulting directory structure of the two cloned repos defined in the preceding template is:</span><span class="sxs-lookup"><span data-stu-id="ed79f-136">The resulting directory structure of the two cloned repos defined in the preceding template is:</span></span>

```
/mnt/repo1/aci-helloworld
/mnt/repo2/my-custom-clone-directory
```

<span data-ttu-id="ed79f-137">To see an example of container instance deployment with an Azure Resource Manager template, see [Deploy multi-container groups in Azure Container Instances](container-instances-multi-container-group.md).</span><span class="sxs-lookup"><span data-stu-id="ed79f-137">To see an example of container instance deployment with an Azure Resource Manager template, see [Deploy multi-container groups in Azure Container Instances](container-instances-multi-container-group.md).</span></span>

## <a name="private-git-repo-authentication"></a><span data-ttu-id="ed79f-138">Private Git repo authentication</span><span class="sxs-lookup"><span data-stu-id="ed79f-138">Private Git repo authentication</span></span>

<span data-ttu-id="ed79f-139">To mount a gitRepo volume for a private Git repository, specify credentials in the repository URL.</span><span class="sxs-lookup"><span data-stu-id="ed79f-139">To mount a gitRepo volume for a private Git repository, specify credentials in the repository URL.</span></span> <span data-ttu-id="ed79f-140">Typically, credentials are in the form of a user name and a personal access token (PAT) that grants scoped access to the repository.</span><span class="sxs-lookup"><span data-stu-id="ed79f-140">Typically, credentials are in the form of a user name and a personal access token (PAT) that grants scoped access to the repository.</span></span>

<span data-ttu-id="ed79f-141">For example, the Azure CLI `--gitrepo-url` parameter for a private GitHub repository would appear similar to the following (where "gituser" is the GitHub user name, and "abcdef1234fdsa4321abcdef" is the user's personal access token):</span><span class="sxs-lookup"><span data-stu-id="ed79f-141">For example, the Azure CLI `--gitrepo-url` parameter for a private GitHub repository would appear similar to the following (where "gituser" is the GitHub user name, and "abcdef1234fdsa4321abcdef" is the user's personal access token):</span></span>

```azurecli
--gitrepo-url https://gituser:abcdef1234fdsa4321abcdef@github.com/GitUser/some-private-repository
```

<span data-ttu-id="ed79f-142">For an Azure DevOps Git repository, specify any user name (you can use "azuredevopsuser" as in the following example) in combination with a valid PAT:</span><span class="sxs-lookup"><span data-stu-id="ed79f-142">For an Azure DevOps Git repository, specify any user name (you can use "azuredevopsuser" as in the following example) in combination with a valid PAT:</span></span>

```azurecli
--gitrepo-url https://azuredevopsuser:abcdef1234fdsa4321abcdef@azuredevopsorganizationname.visualstudio.com/_git/some-private-repository
```

<span data-ttu-id="ed79f-143">For more information about personal access tokens for GitHub and Azure DevOps, see the following:</span><span class="sxs-lookup"><span data-stu-id="ed79f-143">For more information about personal access tokens for GitHub and Azure DevOps, see the following:</span></span>

<span data-ttu-id="ed79f-144">GitHub: [Creating a personal access token for the command line][pat-github]</span><span class="sxs-lookup"><span data-stu-id="ed79f-144">GitHub: [Creating a personal access token for the command line][pat-github]</span></span>

<span data-ttu-id="ed79f-145">Azure DevOps: [Create personal access tokens to authenticate access][pat-vsts]</span><span class="sxs-lookup"><span data-stu-id="ed79f-145">Azure DevOps: [Create personal access tokens to authenticate access][pat-vsts]</span></span>

## <a name="next-steps"></a><span data-ttu-id="ed79f-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="ed79f-146">Next steps</span></span>

<span data-ttu-id="ed79f-147">Learn how to mount other volume types in Azure Container Instances:</span><span class="sxs-lookup"><span data-stu-id="ed79f-147">Learn how to mount other volume types in Azure Container Instances:</span></span>

* [<span data-ttu-id="ed79f-148">Mount an Azure file share in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="ed79f-148">Mount an Azure file share in Azure Container Instances</span></span>](container-instances-volume-azure-files.md)
* [<span data-ttu-id="ed79f-149">Mount an emptyDir volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="ed79f-149">Mount an emptyDir volume in Azure Container Instances</span></span>](container-instances-volume-emptydir.md)
* [<span data-ttu-id="ed79f-150">Mount a secret volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="ed79f-150">Mount a secret volume in Azure Container Instances</span></span>](container-instances-volume-secret.md)

<!-- LINKS - External -->
[aci-helloworld]: https://github.com/Azure-Samples/aci-helloworld
[pat-github]: https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/
[pat-vsts]: https://docs.microsoft.com/vsts/organizations/accounts/use-personal-access-tokens-to-authenticate

<!-- LINKS - Internal -->
[az-container-create]: /cli/azure/container#az-container-create
[az-container-exec]: /cli/azure/container#az-container-exec
