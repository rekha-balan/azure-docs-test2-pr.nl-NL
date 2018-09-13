---
title: Tutorial - Automate container image builds on base image update with Azure Container Registry Build
description: In this tutorial, you learn how to configure a build task to automatically trigger container image builds in the cloud when a base image is updated.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: tutorial
ms.date: 05/11/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: a302cdcf94baa869e55262c4cd380fc05bf64299
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867284"
---
# <a name="tutorial-automate-image-builds-on-base-image-update-with-azure-container-registry-build"></a><span data-ttu-id="d1c0d-103">Tutorial: Automate image builds on base image update with Azure Container Registry Build</span><span class="sxs-lookup"><span data-stu-id="d1c0d-103">Tutorial: Automate image builds on base image update with Azure Container Registry Build</span></span>

<span data-ttu-id="d1c0d-104">ACR Build supports automated build execution when a container's base image is updated, such as when you patch the OS or application framework in one of your base images.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-104">ACR Build supports automated build execution when a container's base image is updated, such as when you patch the OS or application framework in one of your base images.</span></span> <span data-ttu-id="d1c0d-105">In this tutorial, you learn how to create a build task in ACR Build that triggers a build in the cloud when a container's base image has been pushed to your registry.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-105">In this tutorial, you learn how to create a build task in ACR Build that triggers a build in the cloud when a container's base image has been pushed to your registry.</span></span>

<span data-ttu-id="d1c0d-106">In this tutorial, the last in the series:</span><span class="sxs-lookup"><span data-stu-id="d1c0d-106">In this tutorial, the last in the series:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="d1c0d-107">Build the base image</span><span class="sxs-lookup"><span data-stu-id="d1c0d-107">Build the base image</span></span>
> * <span data-ttu-id="d1c0d-108">Create an application image build task</span><span class="sxs-lookup"><span data-stu-id="d1c0d-108">Create an application image build task</span></span>
> * <span data-ttu-id="d1c0d-109">Update the base image to trigger an application image build</span><span class="sxs-lookup"><span data-stu-id="d1c0d-109">Update the base image to trigger an application image build</span></span>
> * <span data-ttu-id="d1c0d-110">Display the triggered build</span><span class="sxs-lookup"><span data-stu-id="d1c0d-110">Display the triggered build</span></span>
> * <span data-ttu-id="d1c0d-111">Verify updated application image</span><span class="sxs-lookup"><span data-stu-id="d1c0d-111">Verify updated application image</span></span>

[!INCLUDE [container-registry-build-preview-note](../../includes/container-registry-build-preview-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d1c0d-112">If you'd like to use the Azure CLI locally, you must have the Azure CLI version **2.0.32** or later installed.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-112">If you'd like to use the Azure CLI locally, you must have the Azure CLI version **2.0.32** or later installed.</span></span> <span data-ttu-id="d1c0d-113">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-113">Run `az --version` to find the version.</span></span> <span data-ttu-id="d1c0d-114">If you need to install or upgrade the CLI, see [Install Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="d1c0d-114">If you need to install or upgrade the CLI, see [Install Azure CLI][azure-cli].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1c0d-115">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="d1c0d-115">Prerequisites</span></span>

### <a name="complete-previous-tutorials"></a><span data-ttu-id="d1c0d-116">Complete previous tutorials</span><span class="sxs-lookup"><span data-stu-id="d1c0d-116">Complete previous tutorials</span></span>

<span data-ttu-id="d1c0d-117">This tutorial assumes you've already completed the steps in the first two tutorials in the series, in which you:</span><span class="sxs-lookup"><span data-stu-id="d1c0d-117">This tutorial assumes you've already completed the steps in the first two tutorials in the series, in which you:</span></span>

* <span data-ttu-id="d1c0d-118">Create Azure container registry</span><span class="sxs-lookup"><span data-stu-id="d1c0d-118">Create Azure container registry</span></span>
* <span data-ttu-id="d1c0d-119">Fork sample repository</span><span class="sxs-lookup"><span data-stu-id="d1c0d-119">Fork sample repository</span></span>
* <span data-ttu-id="d1c0d-120">Clone sample repository</span><span class="sxs-lookup"><span data-stu-id="d1c0d-120">Clone sample repository</span></span>
* <span data-ttu-id="d1c0d-121">Create GitHub personal access token</span><span class="sxs-lookup"><span data-stu-id="d1c0d-121">Create GitHub personal access token</span></span>

<span data-ttu-id="d1c0d-122">If you haven't already done so, complete the first two tutorials before proceeding:</span><span class="sxs-lookup"><span data-stu-id="d1c0d-122">If you haven't already done so, complete the first two tutorials before proceeding:</span></span>

[<span data-ttu-id="d1c0d-123">Build container images in the cloud with Azure Container Registry Build</span><span class="sxs-lookup"><span data-stu-id="d1c0d-123">Build container images in the cloud with Azure Container Registry Build</span></span>](container-registry-tutorial-quick-build.md)

[<span data-ttu-id="d1c0d-124">Automate container image builds with Azure Container Registry Build</span><span class="sxs-lookup"><span data-stu-id="d1c0d-124">Automate container image builds with Azure Container Registry Build</span></span>](container-registry-tutorial-build-task.md)

### <a name="configure-environment"></a><span data-ttu-id="d1c0d-125">Configure environment</span><span class="sxs-lookup"><span data-stu-id="d1c0d-125">Configure environment</span></span>

<span data-ttu-id="d1c0d-126">Populate these shell environment variables with values appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-126">Populate these shell environment variables with values appropriate for your environment.</span></span> <span data-ttu-id="d1c0d-127">This isn't strictly required, but makes executing the multiline Azure CLI commands in this tutorial a bit easier.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-127">This isn't strictly required, but makes executing the multiline Azure CLI commands in this tutorial a bit easier.</span></span> <span data-ttu-id="d1c0d-128">If you don't populate these, you must manually replace each value wherever they appear in the example commands.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-128">If you don't populate these, you must manually replace each value wherever they appear in the example commands.</span></span>

```azurecli-interactive
ACR_NAME=mycontainerregistry # The name of your Azure container registry
GIT_USER=gituser             # Your GitHub user account name
GIT_PAT=personalaccesstoken  # The PAT you generated in the second tutorial
```

## <a name="base-images"></a><span data-ttu-id="d1c0d-129">Base images</span><span class="sxs-lookup"><span data-stu-id="d1c0d-129">Base images</span></span>

<span data-ttu-id="d1c0d-130">Dockerfiles defining most container images specify a parent image from which it is based, often referred to as its *base image*.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-130">Dockerfiles defining most container images specify a parent image from which it is based, often referred to as its *base image*.</span></span> <span data-ttu-id="d1c0d-131">Base images typically contain the operating system, for example [Alpine Linux][base-alpine] or [Windows Nano Server][base-windows], on which the rest of the container's layers are applied.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-131">Base images typically contain the operating system, for example [Alpine Linux][base-alpine] or [Windows Nano Server][base-windows], on which the rest of the container's layers are applied.</span></span> <span data-ttu-id="d1c0d-132">They might also include application frameworks such as [Node.js][base-node] or [.NET Core][base-dotnet].</span><span class="sxs-lookup"><span data-stu-id="d1c0d-132">They might also include application frameworks such as [Node.js][base-node] or [.NET Core][base-dotnet].</span></span>

### <a name="base-image-updates"></a><span data-ttu-id="d1c0d-133">Base image updates</span><span class="sxs-lookup"><span data-stu-id="d1c0d-133">Base image updates</span></span>

<span data-ttu-id="d1c0d-134">A base image is often updated by the image maintainer to include new features or improvements to the OS or framework in the image.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-134">A base image is often updated by the image maintainer to include new features or improvements to the OS or framework in the image.</span></span> <span data-ttu-id="d1c0d-135">Security patches are another common cause for a base image update.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-135">Security patches are another common cause for a base image update.</span></span>

<span data-ttu-id="d1c0d-136">When a base image is updated, you're presented with the need to rebuild any container images in your registry based on it to include the new features and fixes.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-136">When a base image is updated, you're presented with the need to rebuild any container images in your registry based on it to include the new features and fixes.</span></span> <span data-ttu-id="d1c0d-137">ACR Build includes the ability to automatically build images for you when a container's base image is updated.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-137">ACR Build includes the ability to automatically build images for you when a container's base image is updated.</span></span>

### <a name="base-image-update-scenario"></a><span data-ttu-id="d1c0d-138">Base image update scenario</span><span class="sxs-lookup"><span data-stu-id="d1c0d-138">Base image update scenario</span></span>

<span data-ttu-id="d1c0d-139">This tutorial walks you through a base image update scenario.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-139">This tutorial walks you through a base image update scenario.</span></span> <span data-ttu-id="d1c0d-140">The [code sample][code-sample] includes two Dockerfiles: an application image, and an image it specifies as its base.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-140">The [code sample][code-sample] includes two Dockerfiles: an application image, and an image it specifies as its base.</span></span> <span data-ttu-id="d1c0d-141">In the following sections, you create an ACR Build task that automatically triggers a build of the application image when a new version of the base image is pushed to your container registry.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-141">In the following sections, you create an ACR Build task that automatically triggers a build of the application image when a new version of the base image is pushed to your container registry.</span></span>

<span data-ttu-id="d1c0d-142">[Dockerfile-app][dockerfile-app]: A small Node.js web application that renders a static web page displaying the Node.js version on which it's based.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-142">[Dockerfile-app][dockerfile-app]: A small Node.js web application that renders a static web page displaying the Node.js version on which it's based.</span></span> <span data-ttu-id="d1c0d-143">The version string is simulated, in that it displays the contents of an environment variable, `NODE_VERSION`, that's defined in the base image.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-143">The version string is simulated, in that it displays the contents of an environment variable, `NODE_VERSION`, that's defined in the base image.</span></span>

<span data-ttu-id="d1c0d-144">[Dockerfile-base][dockerfile-base]: The image that `Dockerfile-app` specifies as its base.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-144">[Dockerfile-base][dockerfile-base]: The image that `Dockerfile-app` specifies as its base.</span></span> <span data-ttu-id="d1c0d-145">It is itself based on a [Node][base-node] image, and includes the `NODE_VERSION` environment variable.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-145">It is itself based on a [Node][base-node] image, and includes the `NODE_VERSION` environment variable.</span></span>

<span data-ttu-id="d1c0d-146">In the following sections, you create a build task, update the `NODE_VERSION` value in the base image Dockerfile, then use ACR Build to build the base image.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-146">In the following sections, you create a build task, update the `NODE_VERSION` value in the base image Dockerfile, then use ACR Build to build the base image.</span></span> <span data-ttu-id="d1c0d-147">When ACR Build pushes the new base image to your registry, it automatically triggers a build of the application image.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-147">When ACR Build pushes the new base image to your registry, it automatically triggers a build of the application image.</span></span> <span data-ttu-id="d1c0d-148">Optionally, you run the application container image locally to see the different version strings in the built images.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-148">Optionally, you run the application container image locally to see the different version strings in the built images.</span></span>

## <a name="build-base-image"></a><span data-ttu-id="d1c0d-149">Build base image</span><span class="sxs-lookup"><span data-stu-id="d1c0d-149">Build base image</span></span>

<span data-ttu-id="d1c0d-150">Start by building the base image with an ACR Build *Quick Build*.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-150">Start by building the base image with an ACR Build *Quick Build*.</span></span> <span data-ttu-id="d1c0d-151">As discussed in the [first tutorial](container-registry-tutorial-quick-build.md) in the series, this not only builds the image, but pushes it to your container registry if the build is successful.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-151">As discussed in the [first tutorial](container-registry-tutorial-quick-build.md) in the series, this not only builds the image, but pushes it to your container registry if the build is successful.</span></span>

```azurecli-interactive
az acr build --registry $ACR_NAME --image baseimages/node:9-alpine --file Dockerfile-base .
```

## <a name="create-build-task"></a><span data-ttu-id="d1c0d-152">Create build task</span><span class="sxs-lookup"><span data-stu-id="d1c0d-152">Create build task</span></span>

<span data-ttu-id="d1c0d-153">Next, create a build task with [az acr build-task create][az-acr-build-task-create]:</span><span class="sxs-lookup"><span data-stu-id="d1c0d-153">Next, create a build task with [az acr build-task create][az-acr-build-task-create]:</span></span>

```azurecli-interactive
az acr build-task create \
    --registry $ACR_NAME \
    --name buildhelloworld \
    --image helloworld:{{.Build.ID}} \
    --build-arg REGISTRY_NAME=$ACR_NAME.azurecr.io \
    --context https://github.com/$GIT_USER/acr-build-helloworld-node \
    --file Dockerfile-app \
    --branch master \
    --git-access-token $GIT_PAT
```

<span data-ttu-id="d1c0d-154">This build task is similar to the task created in the [previous tutorial](container-registry-tutorial-build-task.md).</span><span class="sxs-lookup"><span data-stu-id="d1c0d-154">This build task is similar to the task created in the [previous tutorial](container-registry-tutorial-build-task.md).</span></span> <span data-ttu-id="d1c0d-155">It instructs ACR Build to trigger an image build when commits are pushed to the repository specified by `--context`.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-155">It instructs ACR Build to trigger an image build when commits are pushed to the repository specified by `--context`.</span></span>

<span data-ttu-id="d1c0d-156">Where it differs is in its behavior, in that it also triggers a build of the image when its *base image* is updated.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-156">Where it differs is in its behavior, in that it also triggers a build of the image when its *base image* is updated.</span></span> <span data-ttu-id="d1c0d-157">The Dockerfile specified by the `--file` argument, [Dockerfile-app][dockerfile-app], supports specifying an image from within the same registry as its base:</span><span class="sxs-lookup"><span data-stu-id="d1c0d-157">The Dockerfile specified by the `--file` argument, [Dockerfile-app][dockerfile-app], supports specifying an image from within the same registry as its base:</span></span>

```Dockerfile
FROM ${REGISTRY_NAME}/baseimages/node:9-alpine
```

<span data-ttu-id="d1c0d-158">When you run a build task, ACR Build detects an image's dependencies.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-158">When you run a build task, ACR Build detects an image's dependencies.</span></span> <span data-ttu-id="d1c0d-159">If the base image specified in the `FROM` statement resides within the same registry, it adds a hook to ensure this image is rebuilt any time its base is updated.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-159">If the base image specified in the `FROM` statement resides within the same registry, it adds a hook to ensure this image is rebuilt any time its base is updated.</span></span>

> [!NOTE]
> <span data-ttu-id="d1c0d-160">During preview, ACR Build supports triggering a derived image build only when both the base image and the image referencing it reside in the same Azure container registry.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-160">During preview, ACR Build supports triggering a derived image build only when both the base image and the image referencing it reside in the same Azure container registry.</span></span>

## <a name="build-application-container"></a><span data-ttu-id="d1c0d-161">Build application container</span><span class="sxs-lookup"><span data-stu-id="d1c0d-161">Build application container</span></span>

<span data-ttu-id="d1c0d-162">To enable ACR Build to determine and track a container image's dependencies--which include its base image--you **must** first trigger its build task **at least once**.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-162">To enable ACR Build to determine and track a container image's dependencies--which include its base image--you **must** first trigger its build task **at least once**.</span></span>

<span data-ttu-id="d1c0d-163">Use [az acr build-task run][az-acr-build-task-run] to manually trigger the build task and build the application image:</span><span class="sxs-lookup"><span data-stu-id="d1c0d-163">Use [az acr build-task run][az-acr-build-task-run] to manually trigger the build task and build the application image:</span></span>

```azurecli-interactive
az acr build-task run --registry $ACR_NAME --name buildhelloworld
```

<span data-ttu-id="d1c0d-164">Once the build has completed, take note of the **Build ID** (for example, "aa6") if you wish to complete the following optional step.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-164">Once the build has completed, take note of the **Build ID** (for example, "aa6") if you wish to complete the following optional step.</span></span>

### <a name="optional-run-application-container-locally"></a><span data-ttu-id="d1c0d-165">Optional: Run application container locally</span><span class="sxs-lookup"><span data-stu-id="d1c0d-165">Optional: Run application container locally</span></span>

<span data-ttu-id="d1c0d-166">If you're working locally (not in the Cloud Shell), and you have Docker installed, run the container to see the application rendered in a web browser before you rebuild its base image.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-166">If you're working locally (not in the Cloud Shell), and you have Docker installed, run the container to see the application rendered in a web browser before you rebuild its base image.</span></span> <span data-ttu-id="d1c0d-167">If you're using the Cloud Shell, skip this section (Cloud Shell does not support `az acr login` or `docker run`).</span><span class="sxs-lookup"><span data-stu-id="d1c0d-167">If you're using the Cloud Shell, skip this section (Cloud Shell does not support `az acr login` or `docker run`).</span></span>

<span data-ttu-id="d1c0d-168">First, log in to your container registry with [az acr login][az-acr-login]:</span><span class="sxs-lookup"><span data-stu-id="d1c0d-168">First, log in to your container registry with [az acr login][az-acr-login]:</span></span>

```azurecli
az acr login --name $ACR_NAME
```

<span data-ttu-id="d1c0d-169">Now, run the container locally with `docker run`.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-169">Now, run the container locally with `docker run`.</span></span> <span data-ttu-id="d1c0d-170">Replace **\<build-id\>** with the Build ID found in the output from the previous step (for example, "aa6").</span><span class="sxs-lookup"><span data-stu-id="d1c0d-170">Replace **\<build-id\>** with the Build ID found in the output from the previous step (for example, "aa6").</span></span>

```azurecli
docker run -d -p 8080:80 $ACR_NAME.azurecr.io/helloworld:<build-id>
```

<span data-ttu-id="d1c0d-171">Navigate to http://localhost:8080 in your browser, and you should see the Node.js version number rendered in the web page, similar to the following.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-171">Navigate to http://localhost:8080 in your browser, and you should see the Node.js version number rendered in the web page, similar to the following.</span></span> <span data-ttu-id="d1c0d-172">In a later step, you bump the version by adding an "a" to the version string.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-172">In a later step, you bump the version by adding an "a" to the version string.</span></span>

![Screenshot of sample application rendered in browser][base-update-01]

## <a name="list-builds"></a><span data-ttu-id="d1c0d-174">List builds</span><span class="sxs-lookup"><span data-stu-id="d1c0d-174">List builds</span></span>

<span data-ttu-id="d1c0d-175">Next, list the builds that ACR Build has completed for your registry:</span><span class="sxs-lookup"><span data-stu-id="d1c0d-175">Next, list the builds that ACR Build has completed for your registry:</span></span>

```azurecli-interactive
az acr build-task list-builds --registry $ACR_NAME --output table
```

<span data-ttu-id="d1c0d-176">If you completed the previous tutorial (and didn't delete the registry), you should see output similar to the following.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-176">If you completed the previous tutorial (and didn't delete the registry), you should see output similar to the following.</span></span> <span data-ttu-id="d1c0d-177">Take note of the number of builds, and the latest BUILD ID, so you can compare the output after you update the base image in the next section.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-177">Take note of the number of builds, and the latest BUILD ID, so you can compare the output after you update the base image in the next section.</span></span>

```console
$ az acr build-task list-builds --registry $ACR_NAME --output table
BUILD ID    TASK             PLATFORM    STATUS     TRIGGER     STARTED               DURATION
----------  ---------------  ----------  ---------  ----------  --------------------  ----------
aa6         buildhelloworld  Linux       Succeeded  Manual      2018-05-10T20:00:12Z  00:00:50
aa5                          Linux       Succeeded  Manual      2018-05-10T19:57:35Z  00:00:55
aa4         buildhelloworld  Linux       Succeeded  Git Commit  2018-05-10T19:49:40Z  00:00:45
aa3         buildhelloworld  Linux       Succeeded  Manual      2018-05-10T19:41:50Z  00:01:20
aa2         buildhelloworld  Linux       Succeeded  Manual      2018-05-10T19:37:11Z  00:00:50
aa1                          Linux       Succeeded  Manual      2018-05-10T19:10:14Z  00:00:55
```

## <a name="update-base-image"></a><span data-ttu-id="d1c0d-178">Update base image</span><span class="sxs-lookup"><span data-stu-id="d1c0d-178">Update base image</span></span>

<span data-ttu-id="d1c0d-179">Here you simulate a framework patch in the base image.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-179">Here you simulate a framework patch in the base image.</span></span> <span data-ttu-id="d1c0d-180">Edit **Dockerfile-base**, and add an "a" after the version number defined in `NODE_VERSION`:</span><span class="sxs-lookup"><span data-stu-id="d1c0d-180">Edit **Dockerfile-base**, and add an "a" after the version number defined in `NODE_VERSION`:</span></span>

```Dockerfile
ENV NODE_VERSION 9.11.1a
```

<span data-ttu-id="d1c0d-181">Run a Quick Build in ACR Build to build the modified base image.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-181">Run a Quick Build in ACR Build to build the modified base image.</span></span> <span data-ttu-id="d1c0d-182">Take note of the **Build ID** in the output.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-182">Take note of the **Build ID** in the output.</span></span>

```azurecli-interactive
az acr build --registry $ACR_NAME --image baseimages/node:9-alpine --file Dockerfile-base .
```

<span data-ttu-id="d1c0d-183">Once the build is complete and ACR Build has pushed the new base image to your registry, it triggers a build of the application image.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-183">Once the build is complete and ACR Build has pushed the new base image to your registry, it triggers a build of the application image.</span></span> <span data-ttu-id="d1c0d-184">It may take few moments for the ACR Build task you created earlier to trigger the application image build, as it must detect the newly completed and pushed base image.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-184">It may take few moments for the ACR Build task you created earlier to trigger the application image build, as it must detect the newly completed and pushed base image.</span></span>

## <a name="list-builds"></a><span data-ttu-id="d1c0d-185">List builds</span><span class="sxs-lookup"><span data-stu-id="d1c0d-185">List builds</span></span>

<span data-ttu-id="d1c0d-186">Now that you've updated the base image, list your builds again to compare to the earlier list.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-186">Now that you've updated the base image, list your builds again to compare to the earlier list.</span></span> <span data-ttu-id="d1c0d-187">If at first the output doesn't differ, periodically run the command to see the new build appear in the list.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-187">If at first the output doesn't differ, periodically run the command to see the new build appear in the list.</span></span>

```azurecli-interactive
az acr build-task list-builds --registry $ACR_NAME --output table
```

<span data-ttu-id="d1c0d-188">Output is similar to the following.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-188">Output is similar to the following.</span></span> <span data-ttu-id="d1c0d-189">The TRIGGER for the last-executed build should be "Image Update", indicating that the build task was kicked off by your Quick Build of the base image.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-189">The TRIGGER for the last-executed build should be "Image Update", indicating that the build task was kicked off by your Quick Build of the base image.</span></span>

```console
$ az acr build-task list-builds --registry $ACR_NAME --output table
BUILD ID    TASK             PLATFORM    STATUS     TRIGGER       STARTED               DURATION
----------  ---------------  ----------  ---------  ------------  --------------------  ----------
aa8         buildhelloworld  Linux       Succeeded  Image Update  2018-05-10T20:09:52Z  00:00:45
aa7                          Linux       Succeeded  Manual        2018-05-10T20:09:17Z  00:00:40
aa6         buildhelloworld  Linux       Succeeded  Manual        2018-05-10T20:00:12Z  00:00:50
aa5                          Linux       Succeeded  Manual        2018-05-10T19:57:35Z  00:00:55
aa4         buildhelloworld  Linux       Succeeded  Git Commit    2018-05-10T19:49:40Z  00:00:45
aa3         buildhelloworld  Linux       Succeeded  Manual        2018-05-10T19:41:50Z  00:01:20
aa2         buildhelloworld  Linux       Succeeded  Manual        2018-05-10T19:37:11Z  00:00:50
aa1                          Linux       Succeeded  Manual        2018-05-10T19:10:14Z  00:00:55
```

<span data-ttu-id="d1c0d-190">If you'd like to perform the following optional step of running the newly built container to see the updated version number, take note of the **BUILD ID** value for the Image Update-triggered build (in the preceding output, it's "aa8").</span><span class="sxs-lookup"><span data-stu-id="d1c0d-190">If you'd like to perform the following optional step of running the newly built container to see the updated version number, take note of the **BUILD ID** value for the Image Update-triggered build (in the preceding output, it's "aa8").</span></span>

### <a name="optional-run-newly-built-image"></a><span data-ttu-id="d1c0d-191">Optional: Run newly built image</span><span class="sxs-lookup"><span data-stu-id="d1c0d-191">Optional: Run newly built image</span></span>

<span data-ttu-id="d1c0d-192">If you're working locally (not in the Cloud Shell), and you have Docker installed, run the new application image once its build has completed.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-192">If you're working locally (not in the Cloud Shell), and you have Docker installed, run the new application image once its build has completed.</span></span> <span data-ttu-id="d1c0d-193">Replace `<build-id>` with the BUILD ID you obtained in the previous step.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-193">Replace `<build-id>` with the BUILD ID you obtained in the previous step.</span></span> <span data-ttu-id="d1c0d-194">If you're using the Cloud Shell, skip this section (Cloud Shell does not support `docker run`).</span><span class="sxs-lookup"><span data-stu-id="d1c0d-194">If you're using the Cloud Shell, skip this section (Cloud Shell does not support `docker run`).</span></span>

```bash
docker run -d -p 8081:80 $ACR_NAME.azurecr.io/helloworld:<build-id>
```

<span data-ttu-id="d1c0d-195">Navigate to http://localhost:8081 in your browser, and you should see the updated Node.js version number (with the "a") in the web page:</span><span class="sxs-lookup"><span data-stu-id="d1c0d-195">Navigate to http://localhost:8081 in your browser, and you should see the updated Node.js version number (with the "a") in the web page:</span></span>

![Screenshot of sample application rendered in browser][base-update-02]

<span data-ttu-id="d1c0d-197">What's important to note is that you updated your **base** image with a new version number, but the last-built **application** image displays the new version.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-197">What's important to note is that you updated your **base** image with a new version number, but the last-built **application** image displays the new version.</span></span> <span data-ttu-id="d1c0d-198">ACR Build picked up your change to the base image, and rebuilt your application image automatically.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-198">ACR Build picked up your change to the base image, and rebuilt your application image automatically.</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="d1c0d-199">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="d1c0d-199">Clean up resources</span></span>

<span data-ttu-id="d1c0d-200">To remove all resources you've created in this tutorial series, including the container registry, container instance, key vault, and service principal, issue the following commands:</span><span class="sxs-lookup"><span data-stu-id="d1c0d-200">To remove all resources you've created in this tutorial series, including the container registry, container instance, key vault, and service principal, issue the following commands:</span></span>

```azurecli-interactive
az group delete --resource-group $RES_GROUP
az ad sp delete --id http://$ACR_NAME-pull
```

## <a name="next-steps"></a><span data-ttu-id="d1c0d-201">Next steps</span><span class="sxs-lookup"><span data-stu-id="d1c0d-201">Next steps</span></span>

<span data-ttu-id="d1c0d-202">In this tutorial, you learned how to use a build task to automatically trigger container image builds when the image's base image has been updated.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-202">In this tutorial, you learned how to use a build task to automatically trigger container image builds when the image's base image has been updated.</span></span> <span data-ttu-id="d1c0d-203">Now, move on to learning about authentication for your container registry.</span><span class="sxs-lookup"><span data-stu-id="d1c0d-203">Now, move on to learning about authentication for your container registry.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d1c0d-204">Authentication in Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="d1c0d-204">Authentication in Azure Container Registry</span></span>](container-registry-authentication.md)

<!-- LINKS - External -->
[base-alpine]: https://hub.docker.com/_/alpine/
[base-dotnet]: https://hub.docker.com/r/microsoft/dotnet/
[base-node]: https://hub.docker.com/_/node/
[base-windows]: https://hub.docker.com/r/microsoft/nanoserver/
[code-sample]: https://github.com/Azure-Samples/acr-build-helloworld-node
[dockerfile-app]: https://github.com/Azure-Samples/acr-build-helloworld-node/blob/master/Dockerfile-app
[dockerfile-base]: https://github.com/Azure-Samples/acr-build-helloworld-node/blob/master/Dockerfile-base

<!-- LINKS - Internal -->
[azure-cli]: /cli/azure/install-azure-cli
[az-acr-build]: /cli/azure/acr#az-acr-build-run
[az-acr-build-task-create]: /cli/azure/acr#az-acr-build-task-create
[az-acr-build-task-run]: /cli/azure/acr#az-acr-build-task-run
[az-acr-login]: /cli/azure/acr#az-acr-login

<!-- IMAGES -->
[base-update-01]: ./media/container-registry-tutorial-base-image-update/base-update-01.png
[base-update-02]: ./media/container-registry-tutorial-base-image-update/base-update-02.png