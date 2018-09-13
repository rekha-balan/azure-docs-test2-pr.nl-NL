---
title: Tutorial - Build container images in the cloud with Azure Container Registry Build
description: In this tutorial, you learn how to build a Docker container image in Azure with Azure Container Registry Build (ACR Build), then deploy it to Azure Container Instances.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: tutorial
ms.date: 05/11/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: d86c47c890fd15515c590e06b395ca82f9747ffe
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870626"
---
# <a name="tutorial-build-container-images-in-the-cloud-with-azure-container-registry-build"></a><span data-ttu-id="9bfe1-103">Tutorial: Build container images in the cloud with Azure Container Registry Build</span><span class="sxs-lookup"><span data-stu-id="9bfe1-103">Tutorial: Build container images in the cloud with Azure Container Registry Build</span></span>

<span data-ttu-id="9bfe1-104">**ACR Build** is a suite of features within Azure Container Registry that provides streamlined and efficient Docker container image builds in Azure.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-104">**ACR Build** is a suite of features within Azure Container Registry that provides streamlined and efficient Docker container image builds in Azure.</span></span> <span data-ttu-id="9bfe1-105">In this article, you learn how to use the *Quick Build* feature of ACR Build.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-105">In this article, you learn how to use the *Quick Build* feature of ACR Build.</span></span> <span data-ttu-id="9bfe1-106">Quick Build extends your development "inner loop" to the cloud, providing you with build success validation and automatic pushing of successfully built images to your container registry.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-106">Quick Build extends your development "inner loop" to the cloud, providing you with build success validation and automatic pushing of successfully built images to your container registry.</span></span> <span data-ttu-id="9bfe1-107">Your images are built natively in the cloud, close to your registry, enabling faster deployment.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-107">Your images are built natively in the cloud, close to your registry, enabling faster deployment.</span></span>

<span data-ttu-id="9bfe1-108">All your Dockerfile expertise is directly transferrable to ACR Build.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-108">All your Dockerfile expertise is directly transferrable to ACR Build.</span></span> <span data-ttu-id="9bfe1-109">You don't have to change your Dockerfiles to build in the cloud with ACR Build, just the command you run.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-109">You don't have to change your Dockerfiles to build in the cloud with ACR Build, just the command you run.</span></span>

<span data-ttu-id="9bfe1-110">In this tutorial, part one of a series:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-110">In this tutorial, part one of a series:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9bfe1-111">Get the sample application source code</span><span class="sxs-lookup"><span data-stu-id="9bfe1-111">Get the sample application source code</span></span>
> * <span data-ttu-id="9bfe1-112">Build a container image in Azure</span><span class="sxs-lookup"><span data-stu-id="9bfe1-112">Build a container image in Azure</span></span>
> * <span data-ttu-id="9bfe1-113">Deploy a container to Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="9bfe1-113">Deploy a container to Azure Container Instances</span></span>

<span data-ttu-id="9bfe1-114">In subsequent tutorials, you learn to use ACR Build's build tasks for automated container image builds on code commit and base image update.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-114">In subsequent tutorials, you learn to use ACR Build's build tasks for automated container image builds on code commit and base image update.</span></span>

[!INCLUDE [container-registry-build-preview-note](../../includes/container-registry-build-preview-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="9bfe1-115">If you'd like to use the Azure CLI locally, you must have Azure CLI version **2.0.32** or later installed.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-115">If you'd like to use the Azure CLI locally, you must have Azure CLI version **2.0.32** or later installed.</span></span> <span data-ttu-id="9bfe1-116">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-116">Run `az --version` to find the version.</span></span> <span data-ttu-id="9bfe1-117">If you need to install or upgrade the CLI, see [Install Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="9bfe1-117">If you need to install or upgrade the CLI, see [Install Azure CLI][azure-cli].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9bfe1-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="9bfe1-118">Prerequisites</span></span>

### <a name="github-account"></a><span data-ttu-id="9bfe1-119">GitHub account</span><span class="sxs-lookup"><span data-stu-id="9bfe1-119">GitHub account</span></span>

<span data-ttu-id="9bfe1-120">Create an account on https://github.com if you don't already have one.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-120">Create an account on https://github.com if you don't already have one.</span></span> <span data-ttu-id="9bfe1-121">This tutorial series uses a GitHub repository to demonstrate automated image builds in ACR Build.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-121">This tutorial series uses a GitHub repository to demonstrate automated image builds in ACR Build.</span></span>

### <a name="fork-sample-repository"></a><span data-ttu-id="9bfe1-122">Fork sample repository</span><span class="sxs-lookup"><span data-stu-id="9bfe1-122">Fork sample repository</span></span>

<span data-ttu-id="9bfe1-123">Next, use the GitHub UI to fork the sample repository into your GitHub account.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-123">Next, use the GitHub UI to fork the sample repository into your GitHub account.</span></span> <span data-ttu-id="9bfe1-124">In this tutorial, you build a container image from the source in the repo, and in the next tutorial, you push a commit to your fork of the repo to kick off an automated build.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-124">In this tutorial, you build a container image from the source in the repo, and in the next tutorial, you push a commit to your fork of the repo to kick off an automated build.</span></span>

<span data-ttu-id="9bfe1-125">Fork this repository: https://github.com/Azure-Samples/acr-build-helloworld-node</span><span class="sxs-lookup"><span data-stu-id="9bfe1-125">Fork this repository: https://github.com/Azure-Samples/acr-build-helloworld-node</span></span>

![Screenshot of the Fork button (highlighted) in GitHub][quick-build-01-fork]

### <a name="clone-your-fork"></a><span data-ttu-id="9bfe1-127">Clone your fork</span><span class="sxs-lookup"><span data-stu-id="9bfe1-127">Clone your fork</span></span>

<span data-ttu-id="9bfe1-128">Once you've forked the repo, clone your fork and enter the directory containing your local clone.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-128">Once you've forked the repo, clone your fork and enter the directory containing your local clone.</span></span>

<span data-ttu-id="9bfe1-129">Clone the repo with `git`, replace **\<your-github-username\>** with your GitHub username:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-129">Clone the repo with `git`, replace **\<your-github-username\>** with your GitHub username:</span></span>

```azurecli-interactive
git clone https://github.com/<your-github-username>/acr-build-helloworld-node
```

<span data-ttu-id="9bfe1-130">Enter the directory containing the source code:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-130">Enter the directory containing the source code:</span></span>

```azurecli-interactive
cd acr-build-helloworld-node
```

### <a name="bash-shell"></a><span data-ttu-id="9bfe1-131">Bash shell</span><span class="sxs-lookup"><span data-stu-id="9bfe1-131">Bash shell</span></span>

<span data-ttu-id="9bfe1-132">The commands in this tutorial series are formatted for the Bash shell.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-132">The commands in this tutorial series are formatted for the Bash shell.</span></span> <span data-ttu-id="9bfe1-133">If you prefer to use PowerShell, Command Prompt, or another shell, you may need to adjust the line continuation and environment variable format accordingly.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-133">If you prefer to use PowerShell, Command Prompt, or another shell, you may need to adjust the line continuation and environment variable format accordingly.</span></span>

## <a name="build-in-azure-with-acr-build"></a><span data-ttu-id="9bfe1-134">Build in Azure with ACR Build</span><span class="sxs-lookup"><span data-stu-id="9bfe1-134">Build in Azure with ACR Build</span></span>

<span data-ttu-id="9bfe1-135">Now that you've pulled the source code down to your machine, follow these steps to create a container registry and build the container image with ACR Build.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-135">Now that you've pulled the source code down to your machine, follow these steps to create a container registry and build the container image with ACR Build.</span></span>

<span data-ttu-id="9bfe1-136">To make executing the sample commands easier, the tutorials in this series use shell environment variables.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-136">To make executing the sample commands easier, the tutorials in this series use shell environment variables.</span></span> <span data-ttu-id="9bfe1-137">Execute the following command to set the `ACR_NAME` variable.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-137">Execute the following command to set the `ACR_NAME` variable.</span></span> <span data-ttu-id="9bfe1-138">Replace **\<registry-name\>** with a unique name for your new container registry.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-138">Replace **\<registry-name\>** with a unique name for your new container registry.</span></span> <span data-ttu-id="9bfe1-139">The registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-139">The registry name must be unique within Azure, and contain 5-50 alphanumeric characters.</span></span> <span data-ttu-id="9bfe1-140">The other resources you create in the tutorial are based on this name, so you should need to modify only this first variable.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-140">The other resources you create in the tutorial are based on this name, so you should need to modify only this first variable.</span></span>

```azurecli-interactive
ACR_NAME=<registry-name>
```

<span data-ttu-id="9bfe1-141">With the container registry environment variable populated, you should now be able to copy and paste the remainder of the commands in the tutorial without editing any values.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-141">With the container registry environment variable populated, you should now be able to copy and paste the remainder of the commands in the tutorial without editing any values.</span></span> <span data-ttu-id="9bfe1-142">Execute the following commands to create a resource group and container registry:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-142">Execute the following commands to create a resource group and container registry:</span></span>

```azurecli-interactive
RES_GROUP=$ACR_NAME # Resource Group name

az group create --resource-group $RES_GROUP --location eastus
az acr create --resource-group $RES_GROUP --name $ACR_NAME --sku Standard --location eastus
```

<span data-ttu-id="9bfe1-143">Now that you have a registry, use ACR Build to build a container image from the sample code.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-143">Now that you have a registry, use ACR Build to build a container image from the sample code.</span></span> <span data-ttu-id="9bfe1-144">Execute the [az acr build][az-acr-build] command to perform a *Quick Build*:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-144">Execute the [az acr build][az-acr-build] command to perform a *Quick Build*:</span></span>

```azurecli-interactive
az acr build --registry $ACR_NAME --image helloacrbuild:v1 .
```

<span data-ttu-id="9bfe1-145">Output from the [az acr build][az-acr-build] command is similar to the following.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-145">Output from the [az acr build][az-acr-build] command is similar to the following.</span></span> <span data-ttu-id="9bfe1-146">You can see the upload of the source code (the "context") to Azure, and the details of the `docker build` operation that ACR Build runs in the cloud.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-146">You can see the upload of the source code (the "context") to Azure, and the details of the `docker build` operation that ACR Build runs in the cloud.</span></span> <span data-ttu-id="9bfe1-147">Because ACR Build uses `docker build` to build your images, no changes to your Dockerfiles are required to start using ACR Build immediately.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-147">Because ACR Build uses `docker build` to build your images, no changes to your Dockerfiles are required to start using ACR Build immediately.</span></span>

```console
$ az acr build --registry $ACR_NAME --image helloacrbuild:v1 .
Sending build context (4.909 KiB) to ACR.
Queued a build with build ID: aa1
Waiting for a build agent...
Sending build context to Docker daemon  22.53kB
Step 1/5 : FROM node:9-alpine
9-alpine: Pulling from library/node
Digest: sha256:5149aec8f508d48998e6230cdc8e6832cba192088b442c8ef7e23df3c6892cd3
Status: Image is up to date for node:9-alpine
 ---> 7af437a39ec2
Step 2/5 : COPY . /src
 ---> 0c4814714938
Step 3/5 : RUN cd /src && npm install
 ---> Running in 4f77ce7b330d
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN helloworld@1.0.0 No repository field.

up to date in 0.096s
Removing intermediate container 4f77ce7b330d
 ---> e0eb24339e07
Step 4/5 : EXPOSE 80
 ---> Running in 872bd29edbc7
Removing intermediate container 872bd29edbc7
 ---> 22ba8d8ffb4e
Step 5/5 : CMD ["node", "/src/server.js"]
 ---> Running in 1a40c05c4122
Removing intermediate container 1a40c05c4122
 ---> 0a9a4b74fb53
Successfully built 0a9a4b74fb53
Successfully tagged mycontainerregistry.azurecr.io/helloacrbuild:v1
time="2018-05-10T19:10:20Z" level=info msg="Running command docker push mycontainerregistry.azurecr.io/helloacrbuild:v1"
The push refers to repository [mycontainerregistry.azurecr.io/helloacrbuild]
d2b301f7ef94: Preparing
d0e0f2bb8747: Preparing
26b0c207c4a9: Preparing
917e7cdebc8b: Preparing
9dfa40a0da3b: Preparing
26b0c207c4a9: Pushed
d2b301f7ef94: Pushed
d0e0f2bb8747: Pushed
9dfa40a0da3b: Pushed
917e7cdebc8b: Pushed
v1: digest: sha256:78d7980b4c80a078192bd4749c27eeae56421079606ed7b7d8ae84dbb04193fd size: 1366
time="2018-05-10T19:11:07Z" level=info msg="Running command docker inspect --format \"{{json .RepoDigests}}\" mycontainerregistry.azurecr.io/helloacrbuild:v1"
"["mycontainerregistry.azurecr.io/helloacrbuild@sha256:78d7980b4c80a078192bd4749c27eeae56421079606ed7b7d8ae84dbb04193fd"]"
time="2018-05-10T19:11:07Z" level=info msg="Running command docker inspect --format \"{{json .RepoDigests}}\" node:9-alpine"
"["node@sha256:5149aec8f508d48998e6230cdc8e6832cba192088b442c8ef7e23df3c6892cd3"]"
ACR Builder discovered the following dependencies:
- image:
    registry: mycontainerregistry.azurecr.io
    repository: helloacrbuild
    tag: v1
    digest: sha256:78d7980b4c80a078192bd4749c27eeae56421079606ed7b7d8ae84dbb04193fd
  runtime-dependency:
    registry: registry.hub.docker.com
    repository: library/node
    tag: 9-alpine
    digest: sha256:5149aec8f508d48998e6230cdc8e6832cba192088b442c8ef7e23df3c6892cd3

Build complete
Build ID: aa1 was successful after 52.522222729s
```

<span data-ttu-id="9bfe1-148">Near the end of the output, ACR Build displays the dependencies it's discovered for your image.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-148">Near the end of the output, ACR Build displays the dependencies it's discovered for your image.</span></span> <span data-ttu-id="9bfe1-149">This enables ACR Build to automate image builds on base image updates, such as when a base image is updated with OS or framework patches.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-149">This enables ACR Build to automate image builds on base image updates, such as when a base image is updated with OS or framework patches.</span></span> <span data-ttu-id="9bfe1-150">You learn about ACR Build's support for base image updates later in this tutorial series.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-150">You learn about ACR Build's support for base image updates later in this tutorial series.</span></span>

## <a name="deploy-to-azure-container-instances"></a><span data-ttu-id="9bfe1-151">Deploy to Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="9bfe1-151">Deploy to Azure Container Instances</span></span>

<span data-ttu-id="9bfe1-152">ACR Build automatically pushes successfully built images to your registry by default, allowing you to deploy them from your registry immediately.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-152">ACR Build automatically pushes successfully built images to your registry by default, allowing you to deploy them from your registry immediately.</span></span>

<span data-ttu-id="9bfe1-153">In this section, you create an Azure Key Vault and service principal, then deploy the container to Azure Container Instances (ACI) using the service principal's credentials.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-153">In this section, you create an Azure Key Vault and service principal, then deploy the container to Azure Container Instances (ACI) using the service principal's credentials.</span></span>

### <a name="configure-registry-authentication"></a><span data-ttu-id="9bfe1-154">Configure registry authentication</span><span class="sxs-lookup"><span data-stu-id="9bfe1-154">Configure registry authentication</span></span>

<span data-ttu-id="9bfe1-155">All production scenarios should use [service principals][service-principal-auth] to access an Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-155">All production scenarios should use [service principals][service-principal-auth] to access an Azure container registry.</span></span> <span data-ttu-id="9bfe1-156">Service principals allow you to provide role-based access control to your container images.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-156">Service principals allow you to provide role-based access control to your container images.</span></span> <span data-ttu-id="9bfe1-157">For example, you can configure a service principal with pull-only access to a registry.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-157">For example, you can configure a service principal with pull-only access to a registry.</span></span>

#### <a name="create-key-vault"></a><span data-ttu-id="9bfe1-158">Create key vault</span><span class="sxs-lookup"><span data-stu-id="9bfe1-158">Create key vault</span></span>

<span data-ttu-id="9bfe1-159">If you don't already have a vault in [Azure Key Vault](/azure/key-vault/), create one with the Azure CLI using the following commands.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-159">If you don't already have a vault in [Azure Key Vault](/azure/key-vault/), create one with the Azure CLI using the following commands.</span></span>

```azurecli-interactive
AKV_NAME=$ACR_NAME-vault

az keyvault create --resource-group $RES_GROUP --name $AKV_NAME
```

#### <a name="create-service-principal-and-store-credentials"></a><span data-ttu-id="9bfe1-160">Create service principal and store credentials</span><span class="sxs-lookup"><span data-stu-id="9bfe1-160">Create service principal and store credentials</span></span>

<span data-ttu-id="9bfe1-161">You now need to create a service principal and store its credentials in your key vault.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-161">You now need to create a service principal and store its credentials in your key vault.</span></span>

<span data-ttu-id="9bfe1-162">Use the [az ad sp create-for-rbac][az-ad-sp-create-for-rbac] command to create the service principal, and [az keyvault secret set][az-keyvault-secret-set] to store the service principal's **password** in the vault:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-162">Use the [az ad sp create-for-rbac][az-ad-sp-create-for-rbac] command to create the service principal, and [az keyvault secret set][az-keyvault-secret-set] to store the service principal's **password** in the vault:</span></span>

```azurecli-interactive
# Create service principal, store its password in AKV (the registry *password*)
az keyvault secret set \
  --vault-name $AKV_NAME \
  --name $ACR_NAME-pull-pwd \
  --value $(az ad sp create-for-rbac \
                --name $ACR_NAME-pull \
                --scopes $(az acr show --name $ACR_NAME --query id --output tsv) \
                --role reader \
                --query password \
                --output tsv)
```

<span data-ttu-id="9bfe1-163">The `--role` argument in the preceding command configures the service principal with the *reader* role, which grants it pull-only access to the registry.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-163">The `--role` argument in the preceding command configures the service principal with the *reader* role, which grants it pull-only access to the registry.</span></span> <span data-ttu-id="9bfe1-164">To grant both push and pull access, change the `--role` argument to *contributor*.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-164">To grant both push and pull access, change the `--role` argument to *contributor*.</span></span>

<span data-ttu-id="9bfe1-165">Next, store the service principal's *appId* in the vault, which is the **username** you pass to Azure Container Registry for authentication:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-165">Next, store the service principal's *appId* in the vault, which is the **username** you pass to Azure Container Registry for authentication:</span></span>

```azurecli-interactive
# Store service principal ID in AKV (the registry *username*)
az keyvault secret set \
    --vault-name $AKV_NAME \
    --name $ACR_NAME-pull-usr \
    --value $(az ad sp show --id http://$ACR_NAME-pull --query appId --output tsv)
```

<span data-ttu-id="9bfe1-166">You've created an Azure Key Vault and stored two secrets in it:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-166">You've created an Azure Key Vault and stored two secrets in it:</span></span>

* <span data-ttu-id="9bfe1-167">`$ACR_NAME-pull-usr`: The service principal ID, for use as the container registry **username**.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-167">`$ACR_NAME-pull-usr`: The service principal ID, for use as the container registry **username**.</span></span>
* <span data-ttu-id="9bfe1-168">`$ACR_NAME-pull-pwd`: The service principal password, for use as the container registry **password**.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-168">`$ACR_NAME-pull-pwd`: The service principal password, for use as the container registry **password**.</span></span>

<span data-ttu-id="9bfe1-169">You can now reference these secrets by name when you or your applications and services pull images from the registry.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-169">You can now reference these secrets by name when you or your applications and services pull images from the registry.</span></span>

### <a name="deploy-container-with-azure-cli"></a><span data-ttu-id="9bfe1-170">Deploy container with Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9bfe1-170">Deploy container with Azure CLI</span></span>

<span data-ttu-id="9bfe1-171">Now that the service principal credentials are stored as Azure Key Vault secrets, your applications and services can use them to access your private registry.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-171">Now that the service principal credentials are stored as Azure Key Vault secrets, your applications and services can use them to access your private registry.</span></span>

<span data-ttu-id="9bfe1-172">Execute the following [az container create][az-container-create] command to deploy a container instance.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-172">Execute the following [az container create][az-container-create] command to deploy a container instance.</span></span> <span data-ttu-id="9bfe1-173">The command uses the service principal's credentials stored in Azure Key Vault to authenticate to your container registry.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-173">The command uses the service principal's credentials stored in Azure Key Vault to authenticate to your container registry.</span></span>

```azurecli-interactive
az container create \
    --resource-group $RES_GROUP \
    --name acr-build \
    --image $ACR_NAME.azurecr.io/helloacrbuild:v1 \
    --registry-login-server $ACR_NAME.azurecr.io \
    --registry-username $(az keyvault secret show --vault-name $AKV_NAME --name $ACR_NAME-pull-usr --query value -o tsv) \
    --registry-password $(az keyvault secret show --vault-name $AKV_NAME --name $ACR_NAME-pull-pwd --query value -o tsv) \
    --dns-name-label acr-build-$ACR_NAME \
    --query "{FQDN:ipAddress.fqdn}" \
    --output table
```

<span data-ttu-id="9bfe1-174">The `--dns-name-label` value must be unique within Azure, so the preceding command appends your container registry's name to the container's DNS name label.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-174">The `--dns-name-label` value must be unique within Azure, so the preceding command appends your container registry's name to the container's DNS name label.</span></span> <span data-ttu-id="9bfe1-175">The output from the command displays the container's fully qualified domain name (FQDN), for example:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-175">The output from the command displays the container's fully qualified domain name (FQDN), for example:</span></span>

```console
$ az container create \
>     --resource-group $RES_GROUP \
>     --name acr-build \
>     --image $ACR_NAME.azurecr.io/helloacrbuild:v1 \
>     --registry-login-server $ACR_NAME.azurecr.io \
>     --registry-username $(az keyvault secret show --vault-name $AKV_NAME --name $ACR_NAME-pull-usr --query value -o tsv) \
>     --registry-password $(az keyvault secret show --vault-name $AKV_NAME --name $ACR_NAME-pull-pwd --query value -o tsv) \
>     --dns-name-label acr-build-$ACR_NAME \
>     --query "{FQDN:ipAddress.fqdn}" \
>     --output table
FQDN
-------------------------------------------
acr-build-1175.eastus.azurecontainer.io
```

<span data-ttu-id="9bfe1-176">Take note of the container's FQDN, you'll use it in the next section.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-176">Take note of the container's FQDN, you'll use it in the next section.</span></span>

### <a name="verify-deployment"></a><span data-ttu-id="9bfe1-177">Verify deployment</span><span class="sxs-lookup"><span data-stu-id="9bfe1-177">Verify deployment</span></span>

<span data-ttu-id="9bfe1-178">To watch the startup process of the container, use the [az container attach][az-container-attach] command:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-178">To watch the startup process of the container, use the [az container attach][az-container-attach] command:</span></span>

```azurecli-interactive
az container attach --resource-group $RES_GROUP --name acr-build
```

<span data-ttu-id="9bfe1-179">The `az container attach` output first displays the container's status as it pulls the image and starts, then binds your local console's STDOUT and STDERR to that of the container's.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-179">The `az container attach` output first displays the container's status as it pulls the image and starts, then binds your local console's STDOUT and STDERR to that of the container's.</span></span>

```console
$ az container attach --resource-group $RES_GROUP --name acr-build
Container 'acr-build' is in state 'Waiting'...
Container 'acr-build' is in state 'Running'...
(count: 1) (last timestamp: 2018-04-03 19:45:37+00:00) pulling image "mycontainerregistry.azurecr.io/helloacrbuild:v1"
(count: 1) (last timestamp: 2018-04-03 19:45:44+00:00) Successfully pulled image "mycontainerregistry.azurecr.io/helloacrbuild:v1"
(count: 1) (last timestamp: 2018-04-03 19:45:44+00:00) Created container with id 094ab4da40138b36ca15fc2ad5cac351c358a7540a32e22b52f78e96a4cb3413
(count: 1) (last timestamp: 2018-04-03 19:45:44+00:00) Started container with id 094ab4da40138b36ca15fc2ad5cac351c358a7540a32e22b52f78e96a4cb3413

Start streaming logs:
Server running at http://localhost:80
```

<span data-ttu-id="9bfe1-180">When `Server running at http://localhost:80` appears, navigate to the container's FQDN in your brower to see the running application:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-180">When `Server running at http://localhost:80` appears, navigate to the container's FQDN in your brower to see the running application:</span></span>

![Screenshot of sample application rendered in browser][quick-build-02-browser]

<span data-ttu-id="9bfe1-182">To detach your console from the container, hit `Control+C`.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-182">To detach your console from the container, hit `Control+C`.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="9bfe1-183">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="9bfe1-183">Clean up resources</span></span>

<span data-ttu-id="9bfe1-184">Stop the container instance with the [az container delete][az-container-delete] command:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-184">Stop the container instance with the [az container delete][az-container-delete] command:</span></span>

```azurecli-interactive
az container delete --resource-group $RES_GROUP --name acr-build
```

<span data-ttu-id="9bfe1-185">To remove *all* resources you've created in this tutorial, including the container registry, key vault, and service principal, issue the following commands.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-185">To remove *all* resources you've created in this tutorial, including the container registry, key vault, and service principal, issue the following commands.</span></span> <span data-ttu-id="9bfe1-186">These resources are used in the [next tutorial](container-registry-tutorial-build-task.md) in the series, however, so you might want to keep them if you move on directly to the next tutorial.</span><span class="sxs-lookup"><span data-stu-id="9bfe1-186">These resources are used in the [next tutorial](container-registry-tutorial-build-task.md) in the series, however, so you might want to keep them if you move on directly to the next tutorial.</span></span>

```azurecli-interactive
az group delete --resource-group $RES_GROUP
az ad sp delete --id http://$ACR_NAME-pull
```

## <a name="next-steps"></a><span data-ttu-id="9bfe1-187">Next steps</span><span class="sxs-lookup"><span data-stu-id="9bfe1-187">Next steps</span></span>

<span data-ttu-id="9bfe1-188">Now that you've tested your inner loop with a quick build, configure a **build task** to trigger container images builds when you commit source code to a Git repository:</span><span class="sxs-lookup"><span data-stu-id="9bfe1-188">Now that you've tested your inner loop with a quick build, configure a **build task** to trigger container images builds when you commit source code to a Git repository:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9bfe1-189">Trigger automatic builds with build tasks</span><span class="sxs-lookup"><span data-stu-id="9bfe1-189">Trigger automatic builds with build tasks</span></span>](container-registry-tutorial-build-task.md)

<!-- LINKS - External -->
[sample-archive]: https://github.com/Azure-Samples/acr-build-helloworld-node/archive/master.zip

<!-- LINKS - Internal -->
[azure-cli]: /cli/azure/install-azure-cli
[az-acr-build]: /cli/azure/acr#az-acr-build
[az-ad-sp-create-for-rbac]: /cli/azure/ad/sp#az-ad-sp-create-for-rbac
[az-container-attach]: /cli/azure/container#az-container-attach
[az-container-create]: /cli/azure/container#az-container-create
[az-container-delete]: /cli/azure/container#az-container-delete
[az-keyvault-create]: /cli/azure/keyvault/secret#az-keyvault-create
[az-keyvault-secret-set]: /cli/azure/keyvault/secret#az-keyvault-secret-set
[service-principal-auth]: container-registry-auth-service-principal.md

<!-- IMAGES -->
[quick-build-01-fork]: ./media/container-registry-tutorial-quick-build/quick-build-01-fork.png
[quick-build-02-browser]: ./media/container-registry-tutorial-quick-build/quick-build-02-browser.png
