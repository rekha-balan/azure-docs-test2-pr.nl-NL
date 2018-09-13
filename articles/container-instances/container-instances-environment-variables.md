---
title: Set environment variables in Azure Container Instances
description: Learn how to set environment variables in the containers you run in Azure Container Instances
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 07/19/2018
ms.author: marsma
ms.openlocfilehash: 7a3d521d4382e3d9b5b1b1cf4eb3e43fa02c9a40
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44969015"
---
# <a name="set-environment-variables"></a><span data-ttu-id="fbd51-103">Set environment variables</span><span class="sxs-lookup"><span data-stu-id="fbd51-103">Set environment variables</span></span>

<span data-ttu-id="fbd51-104">Setting environment variables in your container instances allows you to provide dynamic configuration of the application or script run by the container.</span><span class="sxs-lookup"><span data-stu-id="fbd51-104">Setting environment variables in your container instances allows you to provide dynamic configuration of the application or script run by the container.</span></span> <span data-ttu-id="fbd51-105">To set environment variables in a container, specify them when you create a container instance.</span><span class="sxs-lookup"><span data-stu-id="fbd51-105">To set environment variables in a container, specify them when you create a container instance.</span></span> <span data-ttu-id="fbd51-106">You can set environment variables when you start a container with the [Azure CLI](#azure-cli-example), [Azure PowerShell](#azure-powershell-example), and the [Azure portal](#azure-portal-example).</span><span class="sxs-lookup"><span data-stu-id="fbd51-106">You can set environment variables when you start a container with the [Azure CLI](#azure-cli-example), [Azure PowerShell](#azure-powershell-example), and the [Azure portal](#azure-portal-example).</span></span>

<span data-ttu-id="fbd51-107">For example, if you run the [microsoft/aci-wordcount][aci-wordcount] container image, you can modify its behavior by specifying the following environment variables:</span><span class="sxs-lookup"><span data-stu-id="fbd51-107">For example, if you run the [microsoft/aci-wordcount][aci-wordcount] container image, you can modify its behavior by specifying the following environment variables:</span></span>

<span data-ttu-id="fbd51-108">*NumWords*: The number of words sent to STDOUT.</span><span class="sxs-lookup"><span data-stu-id="fbd51-108">*NumWords*: The number of words sent to STDOUT.</span></span>

<span data-ttu-id="fbd51-109">*MinLength*: The minimum number of characters in a word for it to be counted.</span><span class="sxs-lookup"><span data-stu-id="fbd51-109">*MinLength*: The minimum number of characters in a word for it to be counted.</span></span> <span data-ttu-id="fbd51-110">A higher number ignores common words like "of" and "the."</span><span class="sxs-lookup"><span data-stu-id="fbd51-110">A higher number ignores common words like "of" and "the."</span></span>

<span data-ttu-id="fbd51-111">If you need to pass secrets as environment variables, Azure Container Instances supports [secure values](#secure-values) for both Windows and Linux containers.</span><span class="sxs-lookup"><span data-stu-id="fbd51-111">If you need to pass secrets as environment variables, Azure Container Instances supports [secure values](#secure-values) for both Windows and Linux containers.</span></span>

## <a name="azure-cli-example"></a><span data-ttu-id="fbd51-112">Azure CLI example</span><span class="sxs-lookup"><span data-stu-id="fbd51-112">Azure CLI example</span></span>

<span data-ttu-id="fbd51-113">To see the default output of the [microsoft/aci-wordcount][aci-wordcount] container, run it first with this [az container create][az-container-create] command (no environment variables specified):</span><span class="sxs-lookup"><span data-stu-id="fbd51-113">To see the default output of the [microsoft/aci-wordcount][aci-wordcount] container, run it first with this [az container create][az-container-create] command (no environment variables specified):</span></span>

```azurecli-interactive
az container create \
    --resource-group myResourceGroup \
    --name mycontainer1 \
    --image microsoft/aci-wordcount:latest \
    --restart-policy OnFailure
```

<span data-ttu-id="fbd51-114">To modify the output, start a second container with the `--environment-variables` argument added, specifying values for the *NumWords* and *MinLength* variables:</span><span class="sxs-lookup"><span data-stu-id="fbd51-114">To modify the output, start a second container with the `--environment-variables` argument added, specifying values for the *NumWords* and *MinLength* variables:</span></span>

```azurecli-interactive
az container create \
    --resource-group myResourceGroup \
    --name mycontainer2 \
    --image microsoft/aci-wordcount:latest \
    --restart-policy OnFailure \
    --environment-variables NumWords=5 MinLength=8
```

<span data-ttu-id="fbd51-115">Once both containers' state shows as *Terminated* (use [az container show][az-container-show] to check state), display their logs with [az container logs][az-container-logs] to see the output.</span><span class="sxs-lookup"><span data-stu-id="fbd51-115">Once both containers' state shows as *Terminated* (use [az container show][az-container-show] to check state), display their logs with [az container logs][az-container-logs] to see the output.</span></span>

```azurecli-interactive
az container logs --resource-group myResourceGroup --name mycontainer1
az container logs --resource-group myResourceGroup --name mycontainer2
```

<span data-ttu-id="fbd51-116">The output of the containers show how you've modified the second container's script behavior by setting environment variables.</span><span class="sxs-lookup"><span data-stu-id="fbd51-116">The output of the containers show how you've modified the second container's script behavior by setting environment variables.</span></span>

```console
azureuser@Azure:~$ az container logs --resource-group myResourceGroup --name mycontainer1
[('the', 990),
 ('and', 702),
 ('of', 628),
 ('to', 610),
 ('I', 544),
 ('you', 495),
 ('a', 453),
 ('my', 441),
 ('in', 399),
 ('HAMLET', 386)]

azureuser@Azure:~$ az container logs --resource-group myResourceGroup --name mycontainer2
[('CLAUDIUS', 120),
 ('POLONIUS', 113),
 ('GERTRUDE', 82),
 ('ROSENCRANTZ', 69),
 ('GUILDENSTERN', 54)]
```

## <a name="azure-powershell-example"></a><span data-ttu-id="fbd51-117">Azure PowerShell example</span><span class="sxs-lookup"><span data-stu-id="fbd51-117">Azure PowerShell example</span></span>

<span data-ttu-id="fbd51-118">Setting environment variables in PowerShell is similar to the CLI, but uses the `-EnvironmentVariable` command-line argument.</span><span class="sxs-lookup"><span data-stu-id="fbd51-118">Setting environment variables in PowerShell is similar to the CLI, but uses the `-EnvironmentVariable` command-line argument.</span></span>

<span data-ttu-id="fbd51-119">First, launch the [microsoft/aci-wordcount][aci-wordcount] container in its default configuration with this [New-AzureRmContainerGroup][new-azurermcontainergroup] command:</span><span class="sxs-lookup"><span data-stu-id="fbd51-119">First, launch the [microsoft/aci-wordcount][aci-wordcount] container in its default configuration with this [New-AzureRmContainerGroup][new-azurermcontainergroup] command:</span></span>

```azurepowershell-interactive
New-AzureRmContainerGroup `
    -ResourceGroupName myResourceGroup `
    -Name mycontainer1 `
    -Image microsoft/aci-wordcount:latest
```

<span data-ttu-id="fbd51-120">Now run the following [New-AzureRmContainerGroup][new-azurermcontainergroup] command.</span><span class="sxs-lookup"><span data-stu-id="fbd51-120">Now run the following [New-AzureRmContainerGroup][new-azurermcontainergroup] command.</span></span> <span data-ttu-id="fbd51-121">This one specifies the *NumWords* and *MinLength* environment variables after populating an array variable, `envVars`:</span><span class="sxs-lookup"><span data-stu-id="fbd51-121">This one specifies the *NumWords* and *MinLength* environment variables after populating an array variable, `envVars`:</span></span>

```azurepowershell-interactive
$envVars = @{NumWords=5;MinLength=8}
New-AzureRmContainerGroup `
    -ResourceGroupName myResourceGroup `
    -Name mycontainer2 `
    -Image microsoft/aci-wordcount:latest `
    -RestartPolicy OnFailure `
    -EnvironmentVariable $envVars
```

<span data-ttu-id="fbd51-122">Once both containers' state is *Terminated* (use [Get-AzureRmContainerInstanceLog][azure-instance-log] to check state), pull their logs with the [Get-AzureRmContainerInstanceLog][azure-instance-log] command.</span><span class="sxs-lookup"><span data-stu-id="fbd51-122">Once both containers' state is *Terminated* (use [Get-AzureRmContainerInstanceLog][azure-instance-log] to check state), pull their logs with the [Get-AzureRmContainerInstanceLog][azure-instance-log] command.</span></span>

```azurepowershell-interactive
Get-AzureRmContainerInstanceLog -ResourceGroupName myResourceGroup -ContainerGroupName mycontainer1
Get-AzureRmContainerInstanceLog -ResourceGroupName myResourceGroup -ContainerGroupName mycontainer2
```

<span data-ttu-id="fbd51-123">The output for each container shows how you've modified the script run by the container by setting environment variables.</span><span class="sxs-lookup"><span data-stu-id="fbd51-123">The output for each container shows how you've modified the script run by the container by setting environment variables.</span></span>

```console
PS Azure:\> Get-AzureRmContainerInstanceLog -ResourceGroupName myResourceGroup -ContainerGroupName mycontainer1
[('the', 990),
 ('and', 702),
 ('of', 628),
 ('to', 610),
 ('I', 544),
 ('you', 495),
 ('a', 453),
 ('my', 441),
 ('in', 399),
 ('HAMLET', 386)]

Azure:\
PS Azure:\> Get-AzureRmContainerInstanceLog -ResourceGroupName myResourceGroup -ContainerGroupName mycontainer2
[('CLAUDIUS', 120),
 ('POLONIUS', 113),
 ('GERTRUDE', 82),
 ('ROSENCRANTZ', 69),
 ('GUILDENSTERN', 54)]

Azure:\
```

## <a name="azure-portal-example"></a><span data-ttu-id="fbd51-124">Azure portal example</span><span class="sxs-lookup"><span data-stu-id="fbd51-124">Azure portal example</span></span>

<span data-ttu-id="fbd51-125">To set environment variables when you start a container in the Azure portal, specify them in the **Configuration** page when you create the container.</span><span class="sxs-lookup"><span data-stu-id="fbd51-125">To set environment variables when you start a container in the Azure portal, specify them in the **Configuration** page when you create the container.</span></span>

<span data-ttu-id="fbd51-126">When you deploy with the portal, you're currently limited to three variables, and you must enter them in this format: `"variableName":"value"`</span><span class="sxs-lookup"><span data-stu-id="fbd51-126">When you deploy with the portal, you're currently limited to three variables, and you must enter them in this format: `"variableName":"value"`</span></span>

<span data-ttu-id="fbd51-127">To see an example, start the [microsoft/aci-wordcount][aci-wordcount] container with the *NumWords* and *MinLength* variables.</span><span class="sxs-lookup"><span data-stu-id="fbd51-127">To see an example, start the [microsoft/aci-wordcount][aci-wordcount] container with the *NumWords* and *MinLength* variables.</span></span>

1. <span data-ttu-id="fbd51-128">In **Configuration**, set the **Restart policy** to *On failure*</span><span class="sxs-lookup"><span data-stu-id="fbd51-128">In **Configuration**, set the **Restart policy** to *On failure*</span></span>
2. <span data-ttu-id="fbd51-129">Enter `"NumWords":"5"` for the first variable, select **Yes** under **Add additional environment variables**, and enter `"MinLength":"8"` for the second variable.</span><span class="sxs-lookup"><span data-stu-id="fbd51-129">Enter `"NumWords":"5"` for the first variable, select **Yes** under **Add additional environment variables**, and enter `"MinLength":"8"` for the second variable.</span></span> <span data-ttu-id="fbd51-130">Select **OK** to verify and then deploy the container.</span><span class="sxs-lookup"><span data-stu-id="fbd51-130">Select **OK** to verify and then deploy the container.</span></span>

![Portal page showing environment variable Enable button and text boxes][portal-env-vars-01]

<span data-ttu-id="fbd51-132">To view the container's logs, under **SETTINGS** select **Containers**, then **Logs**.</span><span class="sxs-lookup"><span data-stu-id="fbd51-132">To view the container's logs, under **SETTINGS** select **Containers**, then **Logs**.</span></span> <span data-ttu-id="fbd51-133">Similar to the output shown in the previous CLI and PowerShell sections, you can see how the script's behavior has been modified by the environment variables.</span><span class="sxs-lookup"><span data-stu-id="fbd51-133">Similar to the output shown in the previous CLI and PowerShell sections, you can see how the script's behavior has been modified by the environment variables.</span></span> <span data-ttu-id="fbd51-134">Only five words are displayed, each with a minimum length of eight characters.</span><span class="sxs-lookup"><span data-stu-id="fbd51-134">Only five words are displayed, each with a minimum length of eight characters.</span></span>

![Portal showing container log output][portal-env-vars-02]

## <a name="secure-values"></a><span data-ttu-id="fbd51-136">Secure values</span><span class="sxs-lookup"><span data-stu-id="fbd51-136">Secure values</span></span>

<span data-ttu-id="fbd51-137">Objects with secure values are intended to hold sensitive information like passwords or keys for your application.</span><span class="sxs-lookup"><span data-stu-id="fbd51-137">Objects with secure values are intended to hold sensitive information like passwords or keys for your application.</span></span> <span data-ttu-id="fbd51-138">Using secure values for environment variables is both safer and more flexible than including it in your container's image.</span><span class="sxs-lookup"><span data-stu-id="fbd51-138">Using secure values for environment variables is both safer and more flexible than including it in your container's image.</span></span> <span data-ttu-id="fbd51-139">Another option is to use secret volumes, described in [Mount a secret volume in Azure Container Instances](container-instances-volume-secret.md).</span><span class="sxs-lookup"><span data-stu-id="fbd51-139">Another option is to use secret volumes, described in [Mount a secret volume in Azure Container Instances](container-instances-volume-secret.md).</span></span>

<span data-ttu-id="fbd51-140">Environment variables with secure values aren't visible in your container's properties--their values can be accessed only from within the container.</span><span class="sxs-lookup"><span data-stu-id="fbd51-140">Environment variables with secure values aren't visible in your container's properties--their values can be accessed only from within the container.</span></span> <span data-ttu-id="fbd51-141">For example, container properties viewed in the Azure portal or Azure CLI display only a secure variable's name, not its value.</span><span class="sxs-lookup"><span data-stu-id="fbd51-141">For example, container properties viewed in the Azure portal or Azure CLI display only a secure variable's name, not its value.</span></span>

<span data-ttu-id="fbd51-142">Set a secure environment variable by specifying the `secureValue` property instead of the regular `value` for the variable's type.</span><span class="sxs-lookup"><span data-stu-id="fbd51-142">Set a secure environment variable by specifying the `secureValue` property instead of the regular `value` for the variable's type.</span></span> <span data-ttu-id="fbd51-143">The two variables defined in the following YAML demonstrate the two variable types.</span><span class="sxs-lookup"><span data-stu-id="fbd51-143">The two variables defined in the following YAML demonstrate the two variable types.</span></span>

### <a name="yaml-deployment"></a><span data-ttu-id="fbd51-144">YAML deployment</span><span class="sxs-lookup"><span data-stu-id="fbd51-144">YAML deployment</span></span>

<span data-ttu-id="fbd51-145">Create a `secure-env.yaml` file with the following snippet.</span><span class="sxs-lookup"><span data-stu-id="fbd51-145">Create a `secure-env.yaml` file with the following snippet.</span></span>

```yaml
apiVersion: 2018-06-01
location: eastus
name: securetest
properties:
  containers:
  - name: mycontainer
    properties:
      environmentVariables:
        - "name": "NOTSECRET"
          "value": "my-exposed-value"
        - "name": "SECRET"
          "secureValue": "my-secret-value"
      image: nginx
      ports: []
      resources:
        requests:
          cpu: 1.0
          memoryInGB: 1.5
  osType: Linux
  restartPolicy: Always
tags: null
type: Microsoft.ContainerInstance/containerGroups
```

<span data-ttu-id="fbd51-146">Run the following command to deploy the container group with YAML (adjust the resource group name as necessary):</span><span class="sxs-lookup"><span data-stu-id="fbd51-146">Run the following command to deploy the container group with YAML (adjust the resource group name as necessary):</span></span>

```azurecli-interactive
az container create --resource-group myResourceGroup --file secure-env.yaml
```

### <a name="verify-environment-variables"></a><span data-ttu-id="fbd51-147">Verify environment variables</span><span class="sxs-lookup"><span data-stu-id="fbd51-147">Verify environment variables</span></span>

<span data-ttu-id="fbd51-148">Run the [az container show][az-container-show] command to query your container's environment variables:</span><span class="sxs-lookup"><span data-stu-id="fbd51-148">Run the [az container show][az-container-show] command to query your container's environment variables:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name securetest --query 'containers[].environmentVariables'
```

<span data-ttu-id="fbd51-149">The JSON response shows both the insecure environment variable's key and value, but only the name of the secure environment variable:</span><span class="sxs-lookup"><span data-stu-id="fbd51-149">The JSON response shows both the insecure environment variable's key and value, but only the name of the secure environment variable:</span></span>

```json
[
  [
    {
      "name": "NOTSECRET",
      "secureValue": null,
      "value": "my-exposed-value"
    },
    {
      "name": "SECRET",
      "secureValue": null,
      "value": null
    }
  ]
]
```

<span data-ttu-id="fbd51-150">With the [az container exec][az-container-exec] command, which enables executing a command in a running container, you can verify that the secure environment variable has been set.</span><span class="sxs-lookup"><span data-stu-id="fbd51-150">With the [az container exec][az-container-exec] command, which enables executing a command in a running container, you can verify that the secure environment variable has been set.</span></span> <span data-ttu-id="fbd51-151">Run the following command to start an interactive bash session in the container:</span><span class="sxs-lookup"><span data-stu-id="fbd51-151">Run the following command to start an interactive bash session in the container:</span></span>

```azurecli-interactive
az container exec --resource-group myResourceGroup --name securetest --exec-command "/bin/bash"
```

<span data-ttu-id="fbd51-152">Once you've opened an interactive shell within the container, you can access the `SECRET` variable's value:</span><span class="sxs-lookup"><span data-stu-id="fbd51-152">Once you've opened an interactive shell within the container, you can access the `SECRET` variable's value:</span></span>

```console
root@caas-ef3ee231482549629ac8a40c0d3807fd-3881559887-5374l:/# echo $SECRET
my-secret-value
```

## <a name="next-steps"></a><span data-ttu-id="fbd51-153">Next steps</span><span class="sxs-lookup"><span data-stu-id="fbd51-153">Next steps</span></span>

<span data-ttu-id="fbd51-154">Task-based scenarios, such as batch processing a large dataset with several containers, can benefit from custom environment variables at runtime.</span><span class="sxs-lookup"><span data-stu-id="fbd51-154">Task-based scenarios, such as batch processing a large dataset with several containers, can benefit from custom environment variables at runtime.</span></span> <span data-ttu-id="fbd51-155">For more information about running task-based containers, see [Run containerized tasks in Azure Container Instances](container-instances-restart-policy.md).</span><span class="sxs-lookup"><span data-stu-id="fbd51-155">For more information about running task-based containers, see [Run containerized tasks in Azure Container Instances](container-instances-restart-policy.md).</span></span>

<!-- IMAGES -->
[portal-env-vars-01]: ./media/container-instances-environment-variables/portal-env-vars-01.png
[portal-env-vars-02]: ./media/container-instances-environment-variables/portal-env-vars-02.png

<!-- LINKS - External -->
[aci-wordcount]: https://hub.docker.com/r/microsoft/aci-wordcount/

<!-- LINKS Internal -->
[az-container-create]: /cli/azure/container#az-container-create
[az-container-exec]: /cli/azure/container#az-container-exec
[az-container-logs]: /cli/azure/container#az-container-logs
[az-container-show]: /cli/azure/container#az-container-show
[azure-cli-install]: /cli/azure/
[azure-instance-log]: /powershell/module/azurerm.containerinstance/get-azurermcontainerinstancelog
[azure-powershell-install]: /powershell/azure/install-azurerm-ps
[new-azurermcontainergroup]: /powershell/module/azurerm.containerinstance/new-azurermcontainergroup
[portal]: https://portal.azure.com
