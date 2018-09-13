---
title: Deploy multi-container groups in Azure Container Instances with Azure CLI and YAML
description: Learn how to deploy a container group with multiple containers in Azure Container Instances by using the Azure CLI and a YAML file.
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 07/17/2018
ms.author: marsma
ms.openlocfilehash: 1d1885112b8e7f7b1e187073c86d561eb57fd23f
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856979"
---
# <a name="deploy-a-multi-container-container-group-with-yaml"></a><span data-ttu-id="14a08-103">Deploy a multi-container container group with YAML</span><span class="sxs-lookup"><span data-stu-id="14a08-103">Deploy a multi-container container group with YAML</span></span>

<span data-ttu-id="14a08-104">Azure Container Instances supports the deployment of multiple containers onto a single host by using a [container group](container-instances-container-groups.md).</span><span class="sxs-lookup"><span data-stu-id="14a08-104">Azure Container Instances supports the deployment of multiple containers onto a single host by using a [container group](container-instances-container-groups.md).</span></span> <span data-ttu-id="14a08-105">Multi-container container groups are useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span><span class="sxs-lookup"><span data-stu-id="14a08-105">Multi-container container groups are useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span>

<span data-ttu-id="14a08-106">There are two methods for deploying multi-container groups using the Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="14a08-106">There are two methods for deploying multi-container groups using the Azure CLI:</span></span>

* <span data-ttu-id="14a08-107">YAML file deployment (this article)</span><span class="sxs-lookup"><span data-stu-id="14a08-107">YAML file deployment (this article)</span></span>
* [<span data-ttu-id="14a08-108">Resource Manager template deployment</span><span class="sxs-lookup"><span data-stu-id="14a08-108">Resource Manager template deployment</span></span>](container-instances-multi-container-group.md)

<span data-ttu-id="14a08-109">Due to the YAML format's more concise nature, deployment with a YAML file is recommended when your deployment includes *only* container instances.</span><span class="sxs-lookup"><span data-stu-id="14a08-109">Due to the YAML format's more concise nature, deployment with a YAML file is recommended when your deployment includes *only* container instances.</span></span> <span data-ttu-id="14a08-110">If you need to deploy additional Azure service resources (for example, an Azure Files share) at the time of container instance deployment, Resource Manager template deployment is recommended.</span><span class="sxs-lookup"><span data-stu-id="14a08-110">If you need to deploy additional Azure service resources (for example, an Azure Files share) at the time of container instance deployment, Resource Manager template deployment is recommended.</span></span>

> [!NOTE]
> <span data-ttu-id="14a08-111">Multi-container groups are currently restricted to Linux containers.</span><span class="sxs-lookup"><span data-stu-id="14a08-111">Multi-container groups are currently restricted to Linux containers.</span></span> <span data-ttu-id="14a08-112">While we're working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span><span class="sxs-lookup"><span data-stu-id="14a08-112">While we're working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span></span>

## <a name="configure-the-yaml-file"></a><span data-ttu-id="14a08-113">Configure the YAML file</span><span class="sxs-lookup"><span data-stu-id="14a08-113">Configure the YAML file</span></span>

<span data-ttu-id="14a08-114">To deploy a multi-container container group with the [az container create][az-container-create] command in the Azure CLI, you must specify the container group configuration in a YAML file, then pass the YAML file as a parameter to the  command.</span><span class="sxs-lookup"><span data-stu-id="14a08-114">To deploy a multi-container container group with the [az container create][az-container-create] command in the Azure CLI, you must specify the container group configuration in a YAML file, then pass the YAML file as a parameter to the  command.</span></span>

<span data-ttu-id="14a08-115">Start by copying the following YAML into a new file named **deploy-aci.yaml**.</span><span class="sxs-lookup"><span data-stu-id="14a08-115">Start by copying the following YAML into a new file named **deploy-aci.yaml**.</span></span>

<span data-ttu-id="14a08-116">This YAML file defines a container group named "myContainerGroup" with two containers, a public IP address, and two exposed ports.</span><span class="sxs-lookup"><span data-stu-id="14a08-116">This YAML file defines a container group named "myContainerGroup" with two containers, a public IP address, and two exposed ports.</span></span> <span data-ttu-id="14a08-117">The first container in the group runs an internet-facing web application.</span><span class="sxs-lookup"><span data-stu-id="14a08-117">The first container in the group runs an internet-facing web application.</span></span> <span data-ttu-id="14a08-118">The second container, the sidecar, periodically makes HTTP requests to the web application running in the first container via the container group's local network.</span><span class="sxs-lookup"><span data-stu-id="14a08-118">The second container, the sidecar, periodically makes HTTP requests to the web application running in the first container via the container group's local network.</span></span>

```YAML
apiVersion: 2018-06-01
location: eastus
name: myContainerGroup
properties:
  containers:
  - name: aci-tutorial-app
    properties:
      image: microsoft/aci-helloworld:latest
      resources:
        requests:
          cpu: 1
          memoryInGb: 1.5
      ports:
      - port: 80
      - port: 8080
  - name: aci-tutorial-sidecar
    properties:
      image: microsoft/aci-tutorial-sidecar
      resources:
        requests:
          cpu: 1
          memoryInGb: 1.5
  osType: Linux
  ipAddress:
    type: Public
    ports:
    - protocol: tcp
      port: '80'
    - protocol: tcp
      port: '8080'
tags: null
type: Microsoft.ContainerInstance/containerGroups
```

## <a name="deploy-the-container-group"></a><span data-ttu-id="14a08-119">Deploy the container group</span><span class="sxs-lookup"><span data-stu-id="14a08-119">Deploy the container group</span></span>

<span data-ttu-id="14a08-120">Create a resource group with the [az group create][az-group-create] command:</span><span class="sxs-lookup"><span data-stu-id="14a08-120">Create a resource group with the [az group create][az-group-create] command:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="14a08-121">Deploy the container group with the [az container create][az-container-create] command, passing the YAML file as an argument:</span><span class="sxs-lookup"><span data-stu-id="14a08-121">Deploy the container group with the [az container create][az-container-create] command, passing the YAML file as an argument:</span></span>

```azurecli-interactive
az container create --resource-group myResourceGroup --file deploy-aci.yaml
```

<span data-ttu-id="14a08-122">Within a few seconds, you should receive an initial response from Azure.</span><span class="sxs-lookup"><span data-stu-id="14a08-122">Within a few seconds, you should receive an initial response from Azure.</span></span>

## <a name="view-deployment-state"></a><span data-ttu-id="14a08-123">View deployment state</span><span class="sxs-lookup"><span data-stu-id="14a08-123">View deployment state</span></span>

<span data-ttu-id="14a08-124">To view the state of the deployment, use the following [az container show][az-container-show] command:</span><span class="sxs-lookup"><span data-stu-id="14a08-124">To view the state of the deployment, use the following [az container show][az-container-show] command:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name myContainerGroup --output table
```

<span data-ttu-id="14a08-125">If you'd like to view the running application, navigate to its IP address in your browser.</span><span class="sxs-lookup"><span data-stu-id="14a08-125">If you'd like to view the running application, navigate to its IP address in your browser.</span></span> <span data-ttu-id="14a08-126">For example, the IP is `52.168.26.124` in this example output:</span><span class="sxs-lookup"><span data-stu-id="14a08-126">For example, the IP is `52.168.26.124` in this example output:</span></span>

```bash
Name              ResourceGroup    ProvisioningState    Image                                                           IP:ports               CPU/Memory       OsType    Location
----------------  ---------------  -------------------  --------------------------------------------------------------  ---------------------  ---------------  --------  ----------
myContainerGroup  myResourceGroup  Succeeded            microsoft/aci-helloworld:latest,microsoft/aci-tutorial-sidecar  52.168.26.124:80,8080  1.0 core/1.5 gb  Linux     eastus
```

## <a name="view-logs"></a><span data-ttu-id="14a08-127">View logs</span><span class="sxs-lookup"><span data-stu-id="14a08-127">View logs</span></span>

<span data-ttu-id="14a08-128">View the log output of a container using the [az container logs][az-container-logs] command.</span><span class="sxs-lookup"><span data-stu-id="14a08-128">View the log output of a container using the [az container logs][az-container-logs] command.</span></span> <span data-ttu-id="14a08-129">The `--container-name` argument specifies the container from which to pull logs.</span><span class="sxs-lookup"><span data-stu-id="14a08-129">The `--container-name` argument specifies the container from which to pull logs.</span></span> <span data-ttu-id="14a08-130">In this example, the first container is specified.</span><span class="sxs-lookup"><span data-stu-id="14a08-130">In this example, the first container is specified.</span></span>

```azurecli-interactive
az container logs --resource-group myResourceGroup --name myContainerGroup --container-name aci-tutorial-app
```

<span data-ttu-id="14a08-131">Output:</span><span class="sxs-lookup"><span data-stu-id="14a08-131">Output:</span></span>

```console
listening on port 80
::1 - - [09/Jan/2018:23:17:48 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [09/Jan/2018:23:17:51 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [09/Jan/2018:23:17:54 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="14a08-132">To see the logs for the side-car container, run the same command specifying the second container name.</span><span class="sxs-lookup"><span data-stu-id="14a08-132">To see the logs for the side-car container, run the same command specifying the second container name.</span></span>

```azurecli-interactive
az container logs --resource-group myResourceGroup --name myContainerGroup --container-name aci-tutorial-sidecar
```

<span data-ttu-id="14a08-133">Output:</span><span class="sxs-lookup"><span data-stu-id="14a08-133">Output:</span></span>

```console
Every 3s: curl -I http://localhost                          2018-01-09 23:25:11

  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
  0  1663    0     0    0     0      0      0 --:--:-- --:--:-- --:--:--     0
HTTP/1.1 200 OK
X-Powered-By: Express
Accept-Ranges: bytes
Cache-Control: public, max-age=0
Last-Modified: Wed, 29 Nov 2017 06:40:40 GMT
ETag: W/"67f-16006818640"
Content-Type: text/html; charset=UTF-8
Content-Length: 1663
Date: Tue, 09 Jan 2018 23:25:11 GMT
Connection: keep-alive
```

<span data-ttu-id="14a08-134">As you can see, the sidecar is periodically making an HTTP request to the main web application via the group's local network to ensure that it is running.</span><span class="sxs-lookup"><span data-stu-id="14a08-134">As you can see, the sidecar is periodically making an HTTP request to the main web application via the group's local network to ensure that it is running.</span></span> <span data-ttu-id="14a08-135">This sidecar example could be expanded to trigger an alert if it received an HTTP response code other than 200 OK.</span><span class="sxs-lookup"><span data-stu-id="14a08-135">This sidecar example could be expanded to trigger an alert if it received an HTTP response code other than 200 OK.</span></span>

## <a name="deploy-from-private-registry"></a><span data-ttu-id="14a08-136">Deploy from private registry</span><span class="sxs-lookup"><span data-stu-id="14a08-136">Deploy from private registry</span></span>

<span data-ttu-id="14a08-137">To use a private container image registry, include the following YAML with values modified for your environment:</span><span class="sxs-lookup"><span data-stu-id="14a08-137">To use a private container image registry, include the following YAML with values modified for your environment:</span></span>

```YAML
  imageRegistryCredentials:
  - server: imageRegistryLoginServer
    username: imageRegistryUsername
    password: imageRegistryPassword
```

<span data-ttu-id="14a08-138">For example, the following YAML deploys a container group with a single container whose image is pulled from a private Azure Container Registry named "myregistry":</span><span class="sxs-lookup"><span data-stu-id="14a08-138">For example, the following YAML deploys a container group with a single container whose image is pulled from a private Azure Container Registry named "myregistry":</span></span>

```YAML
apiVersion: 2018-06-01
location: eastus
name: myContainerGroup2
properties:
  containers:
  - name: aci-tutorial-app
    properties:
      image: myregistry.azurecr.io/aci-helloworld:latest
      resources:
        requests:
          cpu: 1
          memoryInGb: 1.5
      ports:
      - port: 80
  osType: Linux
  ipAddress:
    type: Public
    ports:
    - protocol: tcp
      port: '80'
  imageRegistryCredentials:
  - server: myregistry.azurecr.io
    username: myregistry
    password: REGISTRY_PASSWORD
tags: null
type: Microsoft.ContainerInstance/containerGroups
```

## <a name="export-container-group-to-yaml"></a><span data-ttu-id="14a08-139">Export container group to YAML</span><span class="sxs-lookup"><span data-stu-id="14a08-139">Export container group to YAML</span></span>

<span data-ttu-id="14a08-140">You can export the configuration of an existing container group to a YAML file by using the Azure CLI command [az container export][az-container-export].</span><span class="sxs-lookup"><span data-stu-id="14a08-140">You can export the configuration of an existing container group to a YAML file by using the Azure CLI command [az container export][az-container-export].</span></span>

<span data-ttu-id="14a08-141">Useful for preserving a container group's configuration, export allows you to store your container group configurations in version control for "configuration as code."</span><span class="sxs-lookup"><span data-stu-id="14a08-141">Useful for preserving a container group's configuration, export allows you to store your container group configurations in version control for "configuration as code."</span></span> <span data-ttu-id="14a08-142">Or, use the exported file as a starting point when developing a new configuration in YAML.</span><span class="sxs-lookup"><span data-stu-id="14a08-142">Or, use the exported file as a starting point when developing a new configuration in YAML.</span></span>

<span data-ttu-id="14a08-143">Export the configuration for the container group you created earlier by issuing the following [az container export][az-container-export] command:</span><span class="sxs-lookup"><span data-stu-id="14a08-143">Export the configuration for the container group you created earlier by issuing the following [az container export][az-container-export] command:</span></span>

```azurecli-interactive
az container export --resource-group myResourceGroup --name myContainerGroup --file deployed-aci.yaml
```

<span data-ttu-id="14a08-144">No output is displayed if the command is successful, but you can view the contents of the file to see the result.</span><span class="sxs-lookup"><span data-stu-id="14a08-144">No output is displayed if the command is successful, but you can view the contents of the file to see the result.</span></span> <span data-ttu-id="14a08-145">For example, the first few lines with `head`:</span><span class="sxs-lookup"><span data-stu-id="14a08-145">For example, the first few lines with `head`:</span></span>

```console
$ head deployed-aci.yaml
additional_properties: {}
apiVersion: '2018-06-01'
location: eastus
name: myContainerGroup
properties:
  containers:
  - name: aci-tutorial-app
    properties:
      environmentVariables: []
      image: microsoft/aci-helloworld:latest
```

## <a name="next-steps"></a><span data-ttu-id="14a08-146">Next steps</span><span class="sxs-lookup"><span data-stu-id="14a08-146">Next steps</span></span>

<span data-ttu-id="14a08-147">This article covered the steps needed for deploying a multi-container Azure container instance.</span><span class="sxs-lookup"><span data-stu-id="14a08-147">This article covered the steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="14a08-148">For an end-to-end Azure Container Instances experience, including using a private Azure container registry, see the Azure Container Instances tutorial.</span><span class="sxs-lookup"><span data-stu-id="14a08-148">For an end-to-end Azure Container Instances experience, including using a private Azure container registry, see the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="14a08-149">[Azure Container Instances tutorial][aci-tutorial]</span><span class="sxs-lookup"><span data-stu-id="14a08-149">[Azure Container Instances tutorial][aci-tutorial]</span></span>

<!-- LINKS - External -->
[cli-issue-6525]: https://github.com/Azure/azure-cli/issues/6525

<!-- LINKS - Internal -->
[aci-tutorial]: ./container-instances-tutorial-prepare-app.md
[az-container-create]: /cli/azure/container#az-container-create
[az-container-export]: /cli/azure/container#az-container-export
[az-container-logs]: /cli/azure/container#az-container-logs
[az-container-show]: /cli/azure/container#az-container-show
[az-group-create]: /cli/azure/group#az-group-create
[az-group-deployment-create]: /cli/azure/group/deployment#az-group-deployment-create
[template-reference]: https://docs.microsoft.com/azure/templates/microsoft.containerinstance/containergroups
