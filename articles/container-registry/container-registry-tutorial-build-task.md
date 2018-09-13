---
title: Tutorial - Automate container image builds with Azure Container Registry Build
description: In this tutorial, you learn how to configure a build task to automatically trigger container image builds in the cloud when you commit source code to a Git repository.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: tutorial
ms.date: 05/11/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: e2a6571b9dcd55be5dd3fc58669b87cf1adeace2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868502"
---
# <a name="tutorial-automate-container-image-builds-with-azure-container-registry-build"></a><span data-ttu-id="5226a-103">Tutorial: Automate container image builds with Azure Container Registry Build</span><span class="sxs-lookup"><span data-stu-id="5226a-103">Tutorial: Automate container image builds with Azure Container Registry Build</span></span>

<span data-ttu-id="5226a-104">In addition to [Quick Build](container-registry-tutorial-quick-build.md), ACR Build supports automated Docker container image builds with the *build task*.</span><span class="sxs-lookup"><span data-stu-id="5226a-104">In addition to [Quick Build](container-registry-tutorial-quick-build.md), ACR Build supports automated Docker container image builds with the *build task*.</span></span> <span data-ttu-id="5226a-105">In this tutorial, you use the Azure CLI to create a build task that automatically triggers image builds in the cloud when you commit source code to a Git repository.</span><span class="sxs-lookup"><span data-stu-id="5226a-105">In this tutorial, you use the Azure CLI to create a build task that automatically triggers image builds in the cloud when you commit source code to a Git repository.</span></span>

<span data-ttu-id="5226a-106">In this tutorial, part two in the series:</span><span class="sxs-lookup"><span data-stu-id="5226a-106">In this tutorial, part two in the series:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="5226a-107">Create a build task</span><span class="sxs-lookup"><span data-stu-id="5226a-107">Create a build task</span></span>
> * <span data-ttu-id="5226a-108">Test the build task</span><span class="sxs-lookup"><span data-stu-id="5226a-108">Test the build task</span></span>
> * <span data-ttu-id="5226a-109">View build status</span><span class="sxs-lookup"><span data-stu-id="5226a-109">View build status</span></span>
> * <span data-ttu-id="5226a-110">Trigger the build task with a code commit</span><span class="sxs-lookup"><span data-stu-id="5226a-110">Trigger the build task with a code commit</span></span>

<span data-ttu-id="5226a-111">This tutorial assumes you've already completed the steps in the [previous tutorial](container-registry-tutorial-quick-build.md).</span><span class="sxs-lookup"><span data-stu-id="5226a-111">This tutorial assumes you've already completed the steps in the [previous tutorial](container-registry-tutorial-quick-build.md).</span></span> <span data-ttu-id="5226a-112">If you haven't already done so, complete the steps in the [Prerequisites](container-registry-tutorial-quick-build.md#prerequisites) section of the previous tutorial before proceeding.</span><span class="sxs-lookup"><span data-stu-id="5226a-112">If you haven't already done so, complete the steps in the [Prerequisites](container-registry-tutorial-quick-build.md#prerequisites) section of the previous tutorial before proceeding.</span></span>

[!INCLUDE [container-registry-build-preview-note](../../includes/container-registry-build-preview-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5226a-113">If you'd like to use the Azure CLI locally, you must have Azure CLI version **2.0.32** or later installed.</span><span class="sxs-lookup"><span data-stu-id="5226a-113">If you'd like to use the Azure CLI locally, you must have Azure CLI version **2.0.32** or later installed.</span></span> <span data-ttu-id="5226a-114">Run `az --version` to find the version.</span><span class="sxs-lookup"><span data-stu-id="5226a-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="5226a-115">If you need to install or upgrade the CLI, see [Install Azure CLI][azure-cli].</span><span class="sxs-lookup"><span data-stu-id="5226a-115">If you need to install or upgrade the CLI, see [Install Azure CLI][azure-cli].</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5226a-116">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="5226a-116">Prerequisites</span></span>

### <a name="get-sample-code"></a><span data-ttu-id="5226a-117">Get sample code</span><span class="sxs-lookup"><span data-stu-id="5226a-117">Get sample code</span></span>

<span data-ttu-id="5226a-118">This tutorial assumes you've already completed the steps in the [previous tutorial](container-registry-tutorial-quick-build.md), and have forked and cloned the sample repository.</span><span class="sxs-lookup"><span data-stu-id="5226a-118">This tutorial assumes you've already completed the steps in the [previous tutorial](container-registry-tutorial-quick-build.md), and have forked and cloned the sample repository.</span></span> <span data-ttu-id="5226a-119">If you haven't already done so, complete the steps in the [Prerequisites](container-registry-tutorial-quick-build.md#prerequisites) section of the previous tutorial before proceeding.</span><span class="sxs-lookup"><span data-stu-id="5226a-119">If you haven't already done so, complete the steps in the [Prerequisites](container-registry-tutorial-quick-build.md#prerequisites) section of the previous tutorial before proceeding.</span></span>

### <a name="container-registry"></a><span data-ttu-id="5226a-120">Container registry</span><span class="sxs-lookup"><span data-stu-id="5226a-120">Container registry</span></span>

<span data-ttu-id="5226a-121">You must have an Azure container registry in your Azure subscription to complete this tutorial.</span><span class="sxs-lookup"><span data-stu-id="5226a-121">You must have an Azure container registry in your Azure subscription to complete this tutorial.</span></span> <span data-ttu-id="5226a-122">If you need a registry, see the [previous tutorial](container-registry-tutorial-quick-build.md), or [Quickstart: Create a container registry using the Azure CLI](container-registry-get-started-azure-cli.md).</span><span class="sxs-lookup"><span data-stu-id="5226a-122">If you need a registry, see the [previous tutorial](container-registry-tutorial-quick-build.md), or [Quickstart: Create a container registry using the Azure CLI](container-registry-get-started-azure-cli.md).</span></span>

## <a name="build-task"></a><span data-ttu-id="5226a-123">Build task</span><span class="sxs-lookup"><span data-stu-id="5226a-123">Build task</span></span>

<span data-ttu-id="5226a-124">A build task defines the properties of an automated build, including the location of the container image source code and the event that triggers the build.</span><span class="sxs-lookup"><span data-stu-id="5226a-124">A build task defines the properties of an automated build, including the location of the container image source code and the event that triggers the build.</span></span> <span data-ttu-id="5226a-125">When an event defined in the build task occurs, such as a commit to a Git repository, ACR Build initiates a container image build in the cloud.</span><span class="sxs-lookup"><span data-stu-id="5226a-125">When an event defined in the build task occurs, such as a commit to a Git repository, ACR Build initiates a container image build in the cloud.</span></span> <span data-ttu-id="5226a-126">By default, it then pushes a successfully built image to the Azure container registry specified in the task.</span><span class="sxs-lookup"><span data-stu-id="5226a-126">By default, it then pushes a successfully built image to the Azure container registry specified in the task.</span></span>

<span data-ttu-id="5226a-127">ACR Build currently supports the following build task triggers:</span><span class="sxs-lookup"><span data-stu-id="5226a-127">ACR Build currently supports the following build task triggers:</span></span>

* <span data-ttu-id="5226a-128">Commit to a Git repository</span><span class="sxs-lookup"><span data-stu-id="5226a-128">Commit to a Git repository</span></span>
* <span data-ttu-id="5226a-129">Base image update</span><span class="sxs-lookup"><span data-stu-id="5226a-129">Base image update</span></span>

## <a name="create-a-build-task"></a><span data-ttu-id="5226a-130">Create a build task</span><span class="sxs-lookup"><span data-stu-id="5226a-130">Create a build task</span></span>

<span data-ttu-id="5226a-131">In this section, you first create a GitHub personal access token (PAT) for use with ACR Build.</span><span class="sxs-lookup"><span data-stu-id="5226a-131">In this section, you first create a GitHub personal access token (PAT) for use with ACR Build.</span></span> <span data-ttu-id="5226a-132">Then, you create a build task that triggers a build when code is committed to your fork of the repository.</span><span class="sxs-lookup"><span data-stu-id="5226a-132">Then, you create a build task that triggers a build when code is committed to your fork of the repository.</span></span>

### <a name="create-a-github-personal-access-token"></a><span data-ttu-id="5226a-133">Create a GitHub personal access token</span><span class="sxs-lookup"><span data-stu-id="5226a-133">Create a GitHub personal access token</span></span>

<span data-ttu-id="5226a-134">To trigger a build on a commit to a Git repository, ACR Build needs a personal access token (PAT) to access the repository.</span><span class="sxs-lookup"><span data-stu-id="5226a-134">To trigger a build on a commit to a Git repository, ACR Build needs a personal access token (PAT) to access the repository.</span></span> <span data-ttu-id="5226a-135">Follow these steps to generate a PAT in GitHub:</span><span class="sxs-lookup"><span data-stu-id="5226a-135">Follow these steps to generate a PAT in GitHub:</span></span>

1. <span data-ttu-id="5226a-136">Navigate to the PAT creation page on GitHub at https://github.com/settings/tokens/new</span><span class="sxs-lookup"><span data-stu-id="5226a-136">Navigate to the PAT creation page on GitHub at https://github.com/settings/tokens/new</span></span>
1. <span data-ttu-id="5226a-137">Enter a short **description** for the token, for example, "ACR Build Task Demo"</span><span class="sxs-lookup"><span data-stu-id="5226a-137">Enter a short **description** for the token, for example, "ACR Build Task Demo"</span></span>
1. <span data-ttu-id="5226a-138">Under **repo**, enable **repo:status** and **public_repo**</span><span class="sxs-lookup"><span data-stu-id="5226a-138">Under **repo**, enable **repo:status** and **public_repo**</span></span>

   ![Screenshot of the Personal Access Token generation page in GitHub][build-task-01-new-token]

1. <span data-ttu-id="5226a-140">Select the **Generate token** button (you may be asked to confirm your password)</span><span class="sxs-lookup"><span data-stu-id="5226a-140">Select the **Generate token** button (you may be asked to confirm your password)</span></span>
1. <span data-ttu-id="5226a-141">Copy and save the generated token in a **secure location** (you use this token when you define a build task in the following section)</span><span class="sxs-lookup"><span data-stu-id="5226a-141">Copy and save the generated token in a **secure location** (you use this token when you define a build task in the following section)</span></span>

   ![Screenshot of the generated Personal Access Token in GitHub][build-task-02-generated-token]

### <a name="create-the-build-task"></a><span data-ttu-id="5226a-143">Create the build task</span><span class="sxs-lookup"><span data-stu-id="5226a-143">Create the build task</span></span>

<span data-ttu-id="5226a-144">Now that you've completed the steps required to enable ACR Build to read commit status and create webhooks in a repository, you can create a build task that triggers a container image build on commits to the repo.</span><span class="sxs-lookup"><span data-stu-id="5226a-144">Now that you've completed the steps required to enable ACR Build to read commit status and create webhooks in a repository, you can create a build task that triggers a container image build on commits to the repo.</span></span>

<span data-ttu-id="5226a-145">First, populate these shell environment variables with values appropriate for your environment.</span><span class="sxs-lookup"><span data-stu-id="5226a-145">First, populate these shell environment variables with values appropriate for your environment.</span></span> <span data-ttu-id="5226a-146">This isn't strictly required, but makes executing the multiline Azure CLI commands in this tutorial a bit easier.</span><span class="sxs-lookup"><span data-stu-id="5226a-146">This isn't strictly required, but makes executing the multiline Azure CLI commands in this tutorial a bit easier.</span></span> <span data-ttu-id="5226a-147">If you don't populate these, you must manually replace each value wherever they appear in the example commands.</span><span class="sxs-lookup"><span data-stu-id="5226a-147">If you don't populate these, you must manually replace each value wherever they appear in the example commands.</span></span>

```azurecli-interactive
ACR_NAME=mycontainerregistry # The name of your Azure container registry
GIT_USER=gituser             # Your GitHub user account name
GIT_PAT=personalaccesstoken  # The PAT you generated in the previous section
```

<span data-ttu-id="5226a-148">Now, create the build task by executing following [az acr build-task create][az-acr-build-task-create] command:</span><span class="sxs-lookup"><span data-stu-id="5226a-148">Now, create the build task by executing following [az acr build-task create][az-acr-build-task-create] command:</span></span>

```azurecli-interactive
az acr build-task create \
    --registry $ACR_NAME \
    --name buildhelloworld \
    --image helloworld:{{.Build.ID}} \
    --context https://github.com/$GIT_USER/acr-build-helloworld-node \
    --branch master \
    --git-access-token $GIT_PAT
```

<span data-ttu-id="5226a-149">This build task specifies that any time code is committed to the *master* branch in the repository specified by `--context`, ACR Build will build the container image from the code in that branch.</span><span class="sxs-lookup"><span data-stu-id="5226a-149">This build task specifies that any time code is committed to the *master* branch in the repository specified by `--context`, ACR Build will build the container image from the code in that branch.</span></span> <span data-ttu-id="5226a-150">The `--image` argument specifies a parameterized value of `{{.Build.ID}}` for the version portion of the image's tag, ensuring the built image correlates to a specific build, and is tagged uniquely.</span><span class="sxs-lookup"><span data-stu-id="5226a-150">The `--image` argument specifies a parameterized value of `{{.Build.ID}}` for the version portion of the image's tag, ensuring the built image correlates to a specific build, and is tagged uniquely.</span></span>

<span data-ttu-id="5226a-151">Output from a successful [az acr build-task create][az-acr-build-task-create] command is similar to the following:</span><span class="sxs-lookup"><span data-stu-id="5226a-151">Output from a successful [az acr build-task create][az-acr-build-task-create] command is similar to the following:</span></span>

```console
$ az acr build-task create \
>     --registry $ACR_NAME \
>     --name buildhelloworld \
>     --image helloworld:{{.Build.ID}} \
>     --context https://github.com/$GIT_USER/acr-build-helloworld-node \
>     --branch master \
>     --git-access-token $GIT_PAT
{
  "additionalProperties": {},
  "alias": "buildhelloworld",
  "creationDate": "2018-05-10T19:34:48.086776+00:00",
  "id": "/subscriptions/<Subscription ID>/resourceGroups/mycontainerregistry/providers/Microsoft.ContainerRegistry/registries/mycontainerregistry/buildTasks/buildhelloworld",
  "location": "eastus",
  "name": "buildhelloworld",
  "platform": {
    "additionalProperties": {},
    "cpu": 1,
    "osType": "Linux"
  },
  "properties": {
    "additionalProperties": {
      "imageName": null
    },
    "baseImageDependencies": null,
    "baseImageTrigger": "Runtime",
    "branch": "master",
    "buildArguments": [],
    "contextPath": null,
    "dockerFilePath": "Dockerfile",
    "imageNames": [
      "helloworld:{{.Build.ID}}"
    ],
    "isPushEnabled": true,
    "noCache": false,
    "provisioningState": "Succeeded",
    "type": "Docker"
  },
  "provisioningState": "Succeeded",
  "resourceGroup": "mycontainerregistry",
  "sourceRepository": {
    "additionalProperties": {},
    "isCommitTriggerEnabled": true,
    "repositoryUrl": "https://github.com/gituser/acr-build-helloworld-node",
    "sourceControlAuthProperties": null,
    "sourceControlType": "GitHub"
  },
  "status": "Enabled",
  "tags": null,
  "timeout": 3600,
  "type": "Microsoft.ContainerRegistry/registries/buildTasks"
}
```

## <a name="test-the-build-task"></a><span data-ttu-id="5226a-152">Test the build task</span><span class="sxs-lookup"><span data-stu-id="5226a-152">Test the build task</span></span>

<span data-ttu-id="5226a-153">You now have a build task that defines your build.</span><span class="sxs-lookup"><span data-stu-id="5226a-153">You now have a build task that defines your build.</span></span> <span data-ttu-id="5226a-154">To test the build pipeline, trigger a build manually by executing the [az acr build-task run][az-acr-build-task-run] command:</span><span class="sxs-lookup"><span data-stu-id="5226a-154">To test the build pipeline, trigger a build manually by executing the [az acr build-task run][az-acr-build-task-run] command:</span></span>

```azurecli-interactive
az acr build-task run --registry $ACR_NAME --name buildhelloworld
```

<span data-ttu-id="5226a-155">By default, the `az acr build-task run` command streams the log output to your console when you execute the command.</span><span class="sxs-lookup"><span data-stu-id="5226a-155">By default, the `az acr build-task run` command streams the log output to your console when you execute the command.</span></span> <span data-ttu-id="5226a-156">Here, the output shows that build **aa2** has been queued and built.</span><span class="sxs-lookup"><span data-stu-id="5226a-156">Here, the output shows that build **aa2** has been queued and built.</span></span>

```console
$ az acr build-task run --registry $ACR_NAME --name buildhelloworld
Queued a build with build ID: aa2
Waiting for a build agent...
time="2018-05-10T19:37:17Z" level=info msg="Running command git clone https://x-access-token:*************@github.com/gituser/acr-build-helloworld-node /root/acr-builder/src"
Cloning into '/root/acr-builder/src'...
time="2018-05-10T19:37:17Z" level=info msg="Running command git checkout master"
Already on 'master'
Your branch is up to date with 'origin/master'.
920f16cfafa36d0bc3f397c3dd48185a03499404
time="2018-05-10T19:37:17Z" level=info msg="Running command git rev-parse --verify HEAD"
time="2018-05-10T19:37:17Z" level=info msg="Running command docker build --pull -f Dockerfile -t mycontainerregistry.azurecr.io/helloworld:aa2 ."
Sending build context to Docker daemon  209.9kB
Step 1/5 : FROM node:9-alpine
9-alpine: Pulling from library/node
Digest: sha256:5149aec8f508d48998e6230cdc8e6832cba192088b442c8ef7e23df3c6892cd3
Status: Image is up to date for node:9-alpine
 ---> 7af437a39ec2
Step 2/5 : COPY . /src
 ---> 48a7735fa94e

[...]

26b0c207c4a9: Pushed
917e7cdebc8b: Pushed
aa2: digest: sha256:6975f01e2e202c084581e676acbe6047788fbe616836328b0b31ce8c58e9fc89 size: 1367
time="2018-05-10T19:37:57Z" level=info msg="Running command docker inspect --format \"{{json .RepoDigests}}\" mycontainerregistrtyy.azurecr.io/helloworld:aa2"
"["mycontainerregistrtyy.azurecr.io/helloworld@sha256:6975f01e2e202c084581e676acbe6047788fbe616836328b0b31ce8c58e9fc89"]"
time="2018-05-10T19:37:57Z" level=info msg="Running command docker inspect --format \"{{json .RepoDigests}}\" node:9-alpine"
"["node@sha256:5149aec8f508d48998e6230cdc8e6832cba192088b442c8ef7e23df3c6892cd3"]"
ACR Builder discovered the following dependencies:
- image:
    registry: mycontainerregistrtyy.azurecr.io
    repository: helloworld
    tag: aa2
    digest: sha256:6975f01e2e202c084581e676acbe6047788fbe616836328b0b31ce8c58e9fc89
  runtime-dependency:
    registry: registry.hub.docker.com
    repository: library/node
    tag: 9-alpine
    digest: sha256:5149aec8f508d48998e6230cdc8e6832cba192088b442c8ef7e23df3c6892cd3
  git:
    git-head-revision: 920f16cfafa36d0bc3f397c3dd48185a03499404

Build complete
Build ID: aa2 was successful after 46.491407373s
```

## <a name="view-build-status"></a><span data-ttu-id="5226a-157">View build status</span><span class="sxs-lookup"><span data-stu-id="5226a-157">View build status</span></span>

<span data-ttu-id="5226a-158">You may occasionally find it useful to view the status of an ongoing build you've not triggered manually.</span><span class="sxs-lookup"><span data-stu-id="5226a-158">You may occasionally find it useful to view the status of an ongoing build you've not triggered manually.</span></span> <span data-ttu-id="5226a-159">For example, while troubleshooting builds triggered by source code commits.</span><span class="sxs-lookup"><span data-stu-id="5226a-159">For example, while troubleshooting builds triggered by source code commits.</span></span> <span data-ttu-id="5226a-160">In this section, you trigger a manual build, but suppress the default behavior of streaming the build log to your console.</span><span class="sxs-lookup"><span data-stu-id="5226a-160">In this section, you trigger a manual build, but suppress the default behavior of streaming the build log to your console.</span></span> <span data-ttu-id="5226a-161">Then, you use the `az acr build-task logs` command to monitor the ongoing build.</span><span class="sxs-lookup"><span data-stu-id="5226a-161">Then, you use the `az acr build-task logs` command to monitor the ongoing build.</span></span>

<span data-ttu-id="5226a-162">First, trigger a build manually as you've done previously, but specify the `--no-logs` argument to suppress logging to your console:</span><span class="sxs-lookup"><span data-stu-id="5226a-162">First, trigger a build manually as you've done previously, but specify the `--no-logs` argument to suppress logging to your console:</span></span>

```azurecli-interactive
az acr build-task run --registry $ACR_NAME --name buildhelloworld --no-logs
```

<span data-ttu-id="5226a-163">Next, use the `az build-task logs` command to view the log of the currently running build:</span><span class="sxs-lookup"><span data-stu-id="5226a-163">Next, use the `az build-task logs` command to view the log of the currently running build:</span></span>

```azurecli-interactive
az acr build-task logs --registry $ACR_NAME
```

<span data-ttu-id="5226a-164">The log for the currently running build is streamed to your console, and should appear similar to the following output (shown here truncated):</span><span class="sxs-lookup"><span data-stu-id="5226a-164">The log for the currently running build is streamed to your console, and should appear similar to the following output (shown here truncated):</span></span>

```console
$ az acr build-task logs --registry $ACR_NAME
Showing logs for the last updated build
Build ID: aa3

[...]

Build complete
Build ID: aa3 was successful after 1m14.26397548s
```

## <a name="trigger-a-build-with-a-commit"></a><span data-ttu-id="5226a-165">Trigger a build with a commit</span><span class="sxs-lookup"><span data-stu-id="5226a-165">Trigger a build with a commit</span></span>

<span data-ttu-id="5226a-166">Now that you've tested the build task by manually running it, trigger it automatically with a source code change.</span><span class="sxs-lookup"><span data-stu-id="5226a-166">Now that you've tested the build task by manually running it, trigger it automatically with a source code change.</span></span>

<span data-ttu-id="5226a-167">First, ensure you're in the directory containing your local clone of the [repository][sample-repo]:</span><span class="sxs-lookup"><span data-stu-id="5226a-167">First, ensure you're in the directory containing your local clone of the [repository][sample-repo]:</span></span>

```azurecli-interactive
cd acr-build-helloworld-node
```

<span data-ttu-id="5226a-168">Next, execute the following commands to create, commit, and push a new file to your fork of the repo on GitHub:</span><span class="sxs-lookup"><span data-stu-id="5226a-168">Next, execute the following commands to create, commit, and push a new file to your fork of the repo on GitHub:</span></span>

```azurecli-interactive
echo "Hello World!" > hello.txt
git add hello.txt
git commit -m "Testing ACR Build"
git push origin master
```

<span data-ttu-id="5226a-169">You may be asked to provide your GitHub credentials when you execute the `git push` command.</span><span class="sxs-lookup"><span data-stu-id="5226a-169">You may be asked to provide your GitHub credentials when you execute the `git push` command.</span></span> <span data-ttu-id="5226a-170">Provide your GitHub username, and enter the personal access token (PAT) that you created earlier for the password.</span><span class="sxs-lookup"><span data-stu-id="5226a-170">Provide your GitHub username, and enter the personal access token (PAT) that you created earlier for the password.</span></span>

```console
$ git push origin master
Username for 'https://github.com': <github-username>
Password for 'https://githubuser@github.com': <personal-access-token>
```

<span data-ttu-id="5226a-171">Once you've pushed a commit to your repository, the webhook created by ACR Build fires and kicks off a build in Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="5226a-171">Once you've pushed a commit to your repository, the webhook created by ACR Build fires and kicks off a build in Azure Container Registry.</span></span> <span data-ttu-id="5226a-172">Display the build logs for the currently running build to verify and monitor the build progress:</span><span class="sxs-lookup"><span data-stu-id="5226a-172">Display the build logs for the currently running build to verify and monitor the build progress:</span></span>

```azurecli-interactive
az acr build-task logs --registry $ACR_NAME
```

<span data-ttu-id="5226a-173">Output is similar to the following, showing the currently executing (or last-executed) build:</span><span class="sxs-lookup"><span data-stu-id="5226a-173">Output is similar to the following, showing the currently executing (or last-executed) build:</span></span>

```console
$ az acr build-task logs --registry $ACR_NAME
Showing logs for the last updated build
Build ID: aa4

[...]

Build complete
Build ID: aa4 was successful after 39.164385024s
```

## <a name="list-builds"></a><span data-ttu-id="5226a-174">List builds</span><span class="sxs-lookup"><span data-stu-id="5226a-174">List builds</span></span>

<span data-ttu-id="5226a-175">To see a list of the builds that ACR Build has completed for your registry, run the [az acr build-task list-builds][az-acr-build-task-list-builds] command:</span><span class="sxs-lookup"><span data-stu-id="5226a-175">To see a list of the builds that ACR Build has completed for your registry, run the [az acr build-task list-builds][az-acr-build-task-list-builds] command:</span></span>

```azurecli-interactive
az acr build-task list-builds --registry $ACR_NAME --output table
```

<span data-ttu-id="5226a-176">Output from the command should appear similar to the following.</span><span class="sxs-lookup"><span data-stu-id="5226a-176">Output from the command should appear similar to the following.</span></span> <span data-ttu-id="5226a-177">The builds that ACR Build has executed are displayed, and "Git Commit" appears in the TRIGGER column for the most recent build:</span><span class="sxs-lookup"><span data-stu-id="5226a-177">The builds that ACR Build has executed are displayed, and "Git Commit" appears in the TRIGGER column for the most recent build:</span></span>

```console
$ az acr build-task list-builds --registry $ACR_NAME --output table
BUILD ID    TASK             PLATFORM    STATUS     TRIGGER     STARTED               DURATION
----------  ---------------  ----------  ---------  ----------  --------------------  ----------
aa4         buildhelloworld  Linux       Succeeded  Git Commit  2018-05-10T19:49:40Z  00:00:45
aa3         buildhelloworld  Linux       Succeeded  Manual      2018-05-10T19:41:50Z  00:01:20
aa2         buildhelloworld  Linux       Succeeded  Manual      2018-05-10T19:37:11Z  00:00:50
aa1                          Linux       Succeeded  Manual      2018-05-10T19:10:14Z  00:00:55
```

## <a name="next-steps"></a><span data-ttu-id="5226a-178">Next steps</span><span class="sxs-lookup"><span data-stu-id="5226a-178">Next steps</span></span>

<span data-ttu-id="5226a-179">In this tutorial, you learned how to use a build task to automatically trigger container image builds in Azure when you commit source code to a Git repository.</span><span class="sxs-lookup"><span data-stu-id="5226a-179">In this tutorial, you learned how to use a build task to automatically trigger container image builds in Azure when you commit source code to a Git repository.</span></span> <span data-ttu-id="5226a-180">Move on to the next tutorial to learn how to create build tasks that trigger builds when a container image's base image is updated.</span><span class="sxs-lookup"><span data-stu-id="5226a-180">Move on to the next tutorial to learn how to create build tasks that trigger builds when a container image's base image is updated.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5226a-181">Automate builds on base image update</span><span class="sxs-lookup"><span data-stu-id="5226a-181">Automate builds on base image update</span></span>](container-registry-tutorial-base-image-update.md)

<!-- LINKS - External -->
[sample-repo]: https://github.com/Azure-Samples/acr-build-helloworld-node

<!-- LINKS - Internal -->
[azure-cli]: /cli/azure/install-azure-cli
[az-acr-build-task]: /cli/azure/acr#az-acr-build-task
[az-acr-build-task-create]: /cli/azure/acr#az-acr-build-task-create
[az-acr-build-task-run]: /cli/azure/acr#az-acr-build-task-run
[az-acr-build-task-list-builds]: /cli/azure/acr#az-acr-build-task-list-build

<!-- IMAGES -->
[build-task-01-new-token]: ./media/container-registry-tutorial-build-tasks/build-task-01-new-token.png
[build-task-02-generated-token]: ./media/container-registry-tutorial-build-tasks/build-task-02-generated-token.png
