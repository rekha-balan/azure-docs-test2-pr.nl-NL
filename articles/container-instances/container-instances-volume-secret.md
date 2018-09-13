---
title: Mount a secret volume in Azure Container Instances
description: Learn how to mount a secret volume to store sensitive information for access by your container instances
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 07/19/2018
ms.author: marsma
ms.openlocfilehash: 572e6701bbe69bbb07c76d468a309030fc37d984
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967002"
---
# <a name="mount-a-secret-volume-in-azure-container-instances"></a><span data-ttu-id="622cf-103">Mount a secret volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="622cf-103">Mount a secret volume in Azure Container Instances</span></span>

<span data-ttu-id="622cf-104">Use a *secret* volume to supply sensitive information to the containers in a container group.</span><span class="sxs-lookup"><span data-stu-id="622cf-104">Use a *secret* volume to supply sensitive information to the containers in a container group.</span></span> <span data-ttu-id="622cf-105">The *secret* volume stores your secrets in files within the volume, accessible by the containers in the container group.</span><span class="sxs-lookup"><span data-stu-id="622cf-105">The *secret* volume stores your secrets in files within the volume, accessible by the containers in the container group.</span></span> <span data-ttu-id="622cf-106">By storing secrets in a *secret* volume, you can avoid adding sensitive data like SSH keys or database credentials to your application code.</span><span class="sxs-lookup"><span data-stu-id="622cf-106">By storing secrets in a *secret* volume, you can avoid adding sensitive data like SSH keys or database credentials to your application code.</span></span>

<span data-ttu-id="622cf-107">All *secret* volumes are backed by [tmpfs][tmpfs], a RAM-backed filesystem; their contents are never written to non-volatile storage.</span><span class="sxs-lookup"><span data-stu-id="622cf-107">All *secret* volumes are backed by [tmpfs][tmpfs], a RAM-backed filesystem; their contents are never written to non-volatile storage.</span></span>

> [!NOTE]
> <span data-ttu-id="622cf-108">*Secret* volumes are currently restricted to Linux containers.</span><span class="sxs-lookup"><span data-stu-id="622cf-108">*Secret* volumes are currently restricted to Linux containers.</span></span> <span data-ttu-id="622cf-109">Learn how to pass secure environment variables for both Windows and Linux containers in [Set environment variables](container-instances-environment-variables.md).</span><span class="sxs-lookup"><span data-stu-id="622cf-109">Learn how to pass secure environment variables for both Windows and Linux containers in [Set environment variables](container-instances-environment-variables.md).</span></span> <span data-ttu-id="622cf-110">While we're working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span><span class="sxs-lookup"><span data-stu-id="622cf-110">While we're working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span></span>

## <a name="mount-secret-volume---azure-cli"></a><span data-ttu-id="622cf-111">Mount secret volume - Azure CLI</span><span class="sxs-lookup"><span data-stu-id="622cf-111">Mount secret volume - Azure CLI</span></span>

<span data-ttu-id="622cf-112">To deploy a container with one or more secrets by using the Azure CLI, include the `--secrets` and `--secrets-mount-path` parameters in the [az container create][az-container-create] command.</span><span class="sxs-lookup"><span data-stu-id="622cf-112">To deploy a container with one or more secrets by using the Azure CLI, include the `--secrets` and `--secrets-mount-path` parameters in the [az container create][az-container-create] command.</span></span> <span data-ttu-id="622cf-113">This example mounts a *secret* volume consisting of two secrets, "mysecret1" and "mysecret2," at `/mnt/secrets`:</span><span class="sxs-lookup"><span data-stu-id="622cf-113">This example mounts a *secret* volume consisting of two secrets, "mysecret1" and "mysecret2," at `/mnt/secrets`:</span></span>

```azurecli-interactive
az container create \
    --resource-group myResourceGroup \
    --name secret-volume-demo \
    --image microsoft/aci-helloworld \
    --secrets mysecret1="My first secret FOO" mysecret2="My second secret BAR" \
    --secrets-mount-path /mnt/secrets
```

<span data-ttu-id="622cf-114">The following [az container exec][az-container-exec] output shows opening a shell in the running container, listing the files within the secret volume, then displaying their contents:</span><span class="sxs-lookup"><span data-stu-id="622cf-114">The following [az container exec][az-container-exec] output shows opening a shell in the running container, listing the files within the secret volume, then displaying their contents:</span></span>

```console
$ az container exec --resource-group myResourceGroup --name secret-volume-demo --exec-command "/bin/sh"
/usr/src/app # ls -1 /mnt/secrets
mysecret1
mysecret2
/usr/src/app # cat /mnt/secrets/mysecret1
My first secret FOO
/usr/src/app # cat /mnt/secrets/mysecret2
My second secret BAR
/usr/src/app # exit
Bye.
```

## <a name="mount-secret-volume---yaml"></a><span data-ttu-id="622cf-115">Mount secret volume - YAML</span><span class="sxs-lookup"><span data-stu-id="622cf-115">Mount secret volume - YAML</span></span>

<span data-ttu-id="622cf-116">You can also deploy container groups with the Azure CLI and a [YAML template](container-instances-multi-container-yaml.md).</span><span class="sxs-lookup"><span data-stu-id="622cf-116">You can also deploy container groups with the Azure CLI and a [YAML template](container-instances-multi-container-yaml.md).</span></span> <span data-ttu-id="622cf-117">Deploying by YAML template is the preferred method when deploying container groups consisting of multiple containers.</span><span class="sxs-lookup"><span data-stu-id="622cf-117">Deploying by YAML template is the preferred method when deploying container groups consisting of multiple containers.</span></span>

<span data-ttu-id="622cf-118">When you deploy with a YAML template, the secret values must be **Base64-encoded** in the template.</span><span class="sxs-lookup"><span data-stu-id="622cf-118">When you deploy with a YAML template, the secret values must be **Base64-encoded** in the template.</span></span> <span data-ttu-id="622cf-119">However, the secret values appear in plaintext within the files in the container.</span><span class="sxs-lookup"><span data-stu-id="622cf-119">However, the secret values appear in plaintext within the files in the container.</span></span>

<span data-ttu-id="622cf-120">The following YAML template defines a container group with one container that mounts a *secret* volume at `/mnt/secrets`.</span><span class="sxs-lookup"><span data-stu-id="622cf-120">The following YAML template defines a container group with one container that mounts a *secret* volume at `/mnt/secrets`.</span></span> <span data-ttu-id="622cf-121">The secret volume has two secrets, "mysecret1" and "mysecret2."</span><span class="sxs-lookup"><span data-stu-id="622cf-121">The secret volume has two secrets, "mysecret1" and "mysecret2."</span></span>

```yaml
apiVersion: '2018-06-01'
location: eastus
name: secret-volume-demo
properties:
  containers:
  - name: aci-tutorial-app
    properties:
      environmentVariables: []
      image: microsoft/aci-helloworld:latest
      ports: []
      resources:
        requests:
          cpu: 1.0
          memoryInGB: 1.5
      volumeMounts:
      - mountPath: /mnt/secrets
        name: secretvolume1
  osType: Linux
  restartPolicy: Always
  volumes:
  - name: secretvolume1
    secret:
      mysecret1: TXkgZmlyc3Qgc2VjcmV0IEZPTwo=
      mysecret2: TXkgc2Vjb25kIHNlY3JldCBCQVIK
tags: {}
type: Microsoft.ContainerInstance/containerGroups
```

<span data-ttu-id="622cf-122">To deploy with the YAML template, save the preceding YAML to a file named `deploy-aci.yaml`, then execute the [az container create][az-container-create] command with the `--file` parameter:</span><span class="sxs-lookup"><span data-stu-id="622cf-122">To deploy with the YAML template, save the preceding YAML to a file named `deploy-aci.yaml`, then execute the [az container create][az-container-create] command with the `--file` parameter:</span></span>

```azurecli-interactive
# Deploy with YAML template
az container create --resource-group myResourceGroup --file deploy-aci.yaml
```

## <a name="mount-secret-volume---resource-manager"></a><span data-ttu-id="622cf-123">Mount secret volume - Resource Manager</span><span class="sxs-lookup"><span data-stu-id="622cf-123">Mount secret volume - Resource Manager</span></span>

<span data-ttu-id="622cf-124">In addition to CLI and YAML deployment, you can deploy a container group using an Azure [Resource Manager template](/azure/templates/microsoft.containerinstance/containergroups).</span><span class="sxs-lookup"><span data-stu-id="622cf-124">In addition to CLI and YAML deployment, you can deploy a container group using an Azure [Resource Manager template](/azure/templates/microsoft.containerinstance/containergroups).</span></span>

<span data-ttu-id="622cf-125">First, populate the `volumes` array in the container group `properties` section of the template.</span><span class="sxs-lookup"><span data-stu-id="622cf-125">First, populate the `volumes` array in the container group `properties` section of the template.</span></span> <span data-ttu-id="622cf-126">When you deploy with a Resource Manager template, the secret values must be **Base64-encoded** in the template.</span><span class="sxs-lookup"><span data-stu-id="622cf-126">When you deploy with a Resource Manager template, the secret values must be **Base64-encoded** in the template.</span></span> <span data-ttu-id="622cf-127">However, the secret values appear in plaintext within the files in the container.</span><span class="sxs-lookup"><span data-stu-id="622cf-127">However, the secret values appear in plaintext within the files in the container.</span></span>

<span data-ttu-id="622cf-128">Next, for each container in the container group in which you'd like to mount the *secret* volume, populate the `volumeMounts` array in the `properties` section of the container definition.</span><span class="sxs-lookup"><span data-stu-id="622cf-128">Next, for each container in the container group in which you'd like to mount the *secret* volume, populate the `volumeMounts` array in the `properties` section of the container definition.</span></span>

<span data-ttu-id="622cf-129">The following Resource Manager template defines a container group with one container that mounts a *secret* volume at `/mnt/secrets`.</span><span class="sxs-lookup"><span data-stu-id="622cf-129">The following Resource Manager template defines a container group with one container that mounts a *secret* volume at `/mnt/secrets`.</span></span> <span data-ttu-id="622cf-130">The secret volume has two secrets, "mysecret1" and "mysecret2."</span><span class="sxs-lookup"><span data-stu-id="622cf-130">The secret volume has two secrets, "mysecret1" and "mysecret2."</span></span>

<span data-ttu-id="622cf-131"><!-- https://github.com/Azure/azure-docs-json-samples/blob/master/container-instances/aci-deploy-volume-secret.json --> [!code-json[volume-secret](~/azure-docs-json-samples/container-instances/aci-deploy-volume-secret.json)]</span><span class="sxs-lookup"><span data-stu-id="622cf-131"><!-- https://github.com/Azure/azure-docs-json-samples/blob/master/container-instances/aci-deploy-volume-secret.json --> [!code-json[volume-secret](~/azure-docs-json-samples/container-instances/aci-deploy-volume-secret.json)]</span></span>

<span data-ttu-id="622cf-132">To deploy with the Resource Manager template, save the preceding JSON to a file named `deploy-aci.json`, then execute the [az group deployment create][az-group-deployment-create] command with the `--template-file` parameter:</span><span class="sxs-lookup"><span data-stu-id="622cf-132">To deploy with the Resource Manager template, save the preceding JSON to a file named `deploy-aci.json`, then execute the [az group deployment create][az-group-deployment-create] command with the `--template-file` parameter:</span></span>

```azurecli-interactive
# Deploy with Resource Manager template
az group deployment create --resource-group myResourceGroup --template-file deploy-aci.json
```

## <a name="next-steps"></a><span data-ttu-id="622cf-133">Next steps</span><span class="sxs-lookup"><span data-stu-id="622cf-133">Next steps</span></span>

### <a name="volumes"></a><span data-ttu-id="622cf-134">Volumes</span><span class="sxs-lookup"><span data-stu-id="622cf-134">Volumes</span></span>

<span data-ttu-id="622cf-135">Learn how to mount other volume types in Azure Container Instances:</span><span class="sxs-lookup"><span data-stu-id="622cf-135">Learn how to mount other volume types in Azure Container Instances:</span></span>

* [<span data-ttu-id="622cf-136">Mount an Azure file share in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="622cf-136">Mount an Azure file share in Azure Container Instances</span></span>](container-instances-volume-azure-files.md)
* [<span data-ttu-id="622cf-137">Mount an emptyDir volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="622cf-137">Mount an emptyDir volume in Azure Container Instances</span></span>](container-instances-volume-emptydir.md)
* [<span data-ttu-id="622cf-138">Mount a gitRepo volume in Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="622cf-138">Mount a gitRepo volume in Azure Container Instances</span></span>](container-instances-volume-gitrepo.md)

### <a name="secure-environment-variables"></a><span data-ttu-id="622cf-139">Secure environment variables</span><span class="sxs-lookup"><span data-stu-id="622cf-139">Secure environment variables</span></span>

<span data-ttu-id="622cf-140">Another method for providing sensitive information to containers (including Windows containers) is through the use of [secure environment variables](container-instances-environment-variables.md#secure-values).</span><span class="sxs-lookup"><span data-stu-id="622cf-140">Another method for providing sensitive information to containers (including Windows containers) is through the use of [secure environment variables](container-instances-environment-variables.md#secure-values).</span></span>

<!-- LINKS - External -->
[tmpfs]: https://wikipedia.org/wiki/Tmpfs

<!-- LINKS - Internal -->
[az-container-create]: /cli/azure/container#az-container-create
[az-container-exec]: /cli/azure/container#az-container-exec
[az-group-deployment-create]: /cli/azure/group/deployment#az-group-deployment-create
