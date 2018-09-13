---
title: Deploy multi-container groups in Azure Container Instances
description: Learn how to deploy a container group with multiple containers in Azure Container Instances.
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 06/08/2018
ms.author: marsma
ms.custom: mvc
ms.openlocfilehash: 8a3dbe67a835cc9f1b8deca6a103e3f4aaa66ff9
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866561"
---
# <a name="deploy-a-container-group"></a><span data-ttu-id="da1bb-103">Deploy a container group</span><span class="sxs-lookup"><span data-stu-id="da1bb-103">Deploy a container group</span></span>

<span data-ttu-id="da1bb-104">Azure Container Instances supports the deployment of multiple containers onto a single host using a [container group](container-instances-container-groups.md).</span><span class="sxs-lookup"><span data-stu-id="da1bb-104">Azure Container Instances supports the deployment of multiple containers onto a single host using a [container group](container-instances-container-groups.md).</span></span> <span data-ttu-id="da1bb-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span><span class="sxs-lookup"><span data-stu-id="da1bb-105">This is useful when building an application sidecar for logging, monitoring, or any other configuration where a service needs a second attached process.</span></span>

<span data-ttu-id="da1bb-106">There are two methods for deploying multi-container groups using the Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="da1bb-106">There are two methods for deploying multi-container groups using the Azure CLI:</span></span>

* <span data-ttu-id="da1bb-107">Resource Manager template deployment (this article)</span><span class="sxs-lookup"><span data-stu-id="da1bb-107">Resource Manager template deployment (this article)</span></span>
* [<span data-ttu-id="da1bb-108">YAML file deployment</span><span class="sxs-lookup"><span data-stu-id="da1bb-108">YAML file deployment</span></span>](container-instances-multi-container-yaml.md)

<span data-ttu-id="da1bb-109">Deployment with a Resource Manager template is recommended when you need to deploy additional Azure service resources (for example, an Azure Files share) at the time of container instance deployment.</span><span class="sxs-lookup"><span data-stu-id="da1bb-109">Deployment with a Resource Manager template is recommended when you need to deploy additional Azure service resources (for example, an Azure Files share) at the time of container instance deployment.</span></span> <span data-ttu-id="da1bb-110">Due to the YAML format's more concise nature, deployment with a YAML file is recommended when your deployment includes *only* container instances.</span><span class="sxs-lookup"><span data-stu-id="da1bb-110">Due to the YAML format's more concise nature, deployment with a YAML file is recommended when your deployment includes *only* container instances.</span></span>

> [!NOTE]
> <span data-ttu-id="da1bb-111">Multi-container groups are currently restricted to Linux containers.</span><span class="sxs-lookup"><span data-stu-id="da1bb-111">Multi-container groups are currently restricted to Linux containers.</span></span> <span data-ttu-id="da1bb-112">While we are working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span><span class="sxs-lookup"><span data-stu-id="da1bb-112">While we are working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).</span></span>

## <a name="configure-the-template"></a><span data-ttu-id="da1bb-113">Configure the template</span><span class="sxs-lookup"><span data-stu-id="da1bb-113">Configure the template</span></span>

<span data-ttu-id="da1bb-114">The sections in this article walk you through running a simple multi-container sidecar configuration by deploying an Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="da1bb-114">The sections in this article walk you through running a simple multi-container sidecar configuration by deploying an Azure Resource Manager template.</span></span>

<span data-ttu-id="da1bb-115">Start by creating a file named `azuredeploy.json`, then copy the following JSON into it.</span><span class="sxs-lookup"><span data-stu-id="da1bb-115">Start by creating a file named `azuredeploy.json`, then copy the following JSON into it.</span></span>

<span data-ttu-id="da1bb-116">This Resource Manager template defines a container group with two containers, a public IP address, and two exposed ports.</span><span class="sxs-lookup"><span data-stu-id="da1bb-116">This Resource Manager template defines a container group with two containers, a public IP address, and two exposed ports.</span></span> <span data-ttu-id="da1bb-117">The first container in the group runs an internet-facing application.</span><span class="sxs-lookup"><span data-stu-id="da1bb-117">The first container in the group runs an internet-facing application.</span></span> <span data-ttu-id="da1bb-118">The second container, the sidecar, makes an HTTP request to the main web application via the group's local network.</span><span class="sxs-lookup"><span data-stu-id="da1bb-118">The second container, the sidecar, makes an HTTP request to the main web application via the group's local network.</span></span>

```JSON
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "containerGroupName": {
      "type": "string",
      "defaultValue": "myContainerGroup",
      "metadata": {
        "description": "Container Group name."
      }
    }
  },
  "variables": {
    "container1name": "aci-tutorial-app",
    "container1image": "microsoft/aci-helloworld:latest",
    "container2name": "aci-tutorial-sidecar",
    "container2image": "microsoft/aci-tutorial-sidecar"
  },
  "resources": [
    {
      "name": "[parameters('containerGroupName')]",
      "type": "Microsoft.ContainerInstance/containerGroups",
      "apiVersion": "2018-04-01",
      "location": "[resourceGroup().location]",
      "properties": {
        "containers": [
          {
            "name": "[variables('container1name')]",
            "properties": {
              "image": "[variables('container1image')]",
              "resources": {
                "requests": {
                  "cpu": 1,
                  "memoryInGb": 1.5
                }
              },
              "ports": [
                {
                  "port": 80
                },
                {
                  "port": 8080
                }
              ]
            }
          },
          {
            "name": "[variables('container2name')]",
            "properties": {
              "image": "[variables('container2image')]",
              "resources": {
                "requests": {
                  "cpu": 1,
                  "memoryInGb": 1.5
                }
              }
            }
          }
        ],
        "osType": "Linux",
        "ipAddress": {
          "type": "Public",
          "ports": [
            {
              "protocol": "tcp",
              "port": "80"
            },
            {
                "protocol": "tcp",
                "port": "8080"
            }
          ]
        }
      }
    }
  ],
  "outputs": {
    "containerIPv4Address": {
      "type": "string",
      "value": "[reference(resourceId('Microsoft.ContainerInstance/containerGroups/', parameters('containerGroupName'))).ipAddress.ip]"
    }
  }
}
```

<span data-ttu-id="da1bb-119">To use a private container image registry, add an object to the JSON document with the following format.</span><span class="sxs-lookup"><span data-stu-id="da1bb-119">To use a private container image registry, add an object to the JSON document with the following format.</span></span> <span data-ttu-id="da1bb-120">For an example implementation of this configuration, see the [ACI Resource Manager template reference][template-reference] documentation.</span><span class="sxs-lookup"><span data-stu-id="da1bb-120">For an example implementation of this configuration, see the [ACI Resource Manager template reference][template-reference] documentation.</span></span>

```JSON
"imageRegistryCredentials": [
  {
    "server": "[parameters('imageRegistryLoginServer')]",
    "username": "[parameters('imageRegistryUsername')]",
    "password": "[parameters('imageRegistryPassword')]"
  }
]
```

## <a name="deploy-the-template"></a><span data-ttu-id="da1bb-121">Deploy the template</span><span class="sxs-lookup"><span data-stu-id="da1bb-121">Deploy the template</span></span>

<span data-ttu-id="da1bb-122">Create a resource group with the [az group create][az-group-create] command.</span><span class="sxs-lookup"><span data-stu-id="da1bb-122">Create a resource group with the [az group create][az-group-create] command.</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location eastus
```

<span data-ttu-id="da1bb-123">Deploy the template with the [az group deployment create][az-group-deployment-create] command.</span><span class="sxs-lookup"><span data-stu-id="da1bb-123">Deploy the template with the [az group deployment create][az-group-deployment-create] command.</span></span>

```azurecli-interactive
az group deployment create --resource-group myResourceGroup --template-file azuredeploy.json
```

<span data-ttu-id="da1bb-124">Within a few seconds, you should receive an initial response from Azure.</span><span class="sxs-lookup"><span data-stu-id="da1bb-124">Within a few seconds, you should receive an initial response from Azure.</span></span>

## <a name="view-deployment-state"></a><span data-ttu-id="da1bb-125">View deployment state</span><span class="sxs-lookup"><span data-stu-id="da1bb-125">View deployment state</span></span>

<span data-ttu-id="da1bb-126">To view the state of the deployment, use the following [az container show][az-container-show] command:</span><span class="sxs-lookup"><span data-stu-id="da1bb-126">To view the state of the deployment, use the following [az container show][az-container-show] command:</span></span>

```azurecli-interactive
az container show --resource-group myResourceGroup --name myContainerGroup --output table
```

<span data-ttu-id="da1bb-127">If you'd like to view the running application, navigate to its IP address in your browser.</span><span class="sxs-lookup"><span data-stu-id="da1bb-127">If you'd like to view the running application, navigate to its IP address in your browser.</span></span> <span data-ttu-id="da1bb-128">For example, the IP is `52.168.26.124` in this example output:</span><span class="sxs-lookup"><span data-stu-id="da1bb-128">For example, the IP is `52.168.26.124` in this example output:</span></span>

```bash
Name              ResourceGroup    ProvisioningState    Image                                                           IP:ports               CPU/Memory       OsType    Location
----------------  ---------------  -------------------  --------------------------------------------------------------  ---------------------  ---------------  --------  ----------
myContainerGroup  myResourceGroup  Succeeded            microsoft/aci-helloworld:latest,microsoft/aci-tutorial-sidecar  52.168.26.124:80,8080  1.0 core/1.5 gb  Linux     westus
```

## <a name="view-logs"></a><span data-ttu-id="da1bb-129">View logs</span><span class="sxs-lookup"><span data-stu-id="da1bb-129">View logs</span></span>

<span data-ttu-id="da1bb-130">View the log output of a container using the [az container logs][az-container-logs] command.</span><span class="sxs-lookup"><span data-stu-id="da1bb-130">View the log output of a container using the [az container logs][az-container-logs] command.</span></span> <span data-ttu-id="da1bb-131">The `--container-name` argument specifies the container from which to pull logs.</span><span class="sxs-lookup"><span data-stu-id="da1bb-131">The `--container-name` argument specifies the container from which to pull logs.</span></span> <span data-ttu-id="da1bb-132">In this example, the first container is specified.</span><span class="sxs-lookup"><span data-stu-id="da1bb-132">In this example, the first container is specified.</span></span>

```azurecli-interactive
az container logs --resource-group myResourceGroup --name myContainerGroup --container-name aci-tutorial-app
```

<span data-ttu-id="da1bb-133">Output:</span><span class="sxs-lookup"><span data-stu-id="da1bb-133">Output:</span></span>

```bash
listening on port 80
::1 - - [09/Jan/2018:23:17:48 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [09/Jan/2018:23:17:51 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
::1 - - [09/Jan/2018:23:17:54 +0000] "HEAD / HTTP/1.1" 200 1663 "-" "curl/7.54.0"
```

<span data-ttu-id="da1bb-134">To see the logs for the side-car container, run the same command specifying the second container name.</span><span class="sxs-lookup"><span data-stu-id="da1bb-134">To see the logs for the side-car container, run the same command specifying the second container name.</span></span>

```azurecli-interactive
az container logs --resource-group myResourceGroup --name myContainerGroup --container-name aci-tutorial-sidecar
```

<span data-ttu-id="da1bb-135">Output:</span><span class="sxs-lookup"><span data-stu-id="da1bb-135">Output:</span></span>

```bash
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

<span data-ttu-id="da1bb-136">As you can see, the sidecar is periodically making an HTTP request to the main web application via the group's local network to ensure that it is running.</span><span class="sxs-lookup"><span data-stu-id="da1bb-136">As you can see, the sidecar is periodically making an HTTP request to the main web application via the group's local network to ensure that it is running.</span></span> <span data-ttu-id="da1bb-137">This sidecar example could be expanded to trigger an alert if it received an HTTP response code other than 200 OK.</span><span class="sxs-lookup"><span data-stu-id="da1bb-137">This sidecar example could be expanded to trigger an alert if it received an HTTP response code other than 200 OK.</span></span>

## <a name="next-steps"></a><span data-ttu-id="da1bb-138">Next steps</span><span class="sxs-lookup"><span data-stu-id="da1bb-138">Next steps</span></span>

<span data-ttu-id="da1bb-139">This article covered the steps needed for deploying a multi-container Azure container instance.</span><span class="sxs-lookup"><span data-stu-id="da1bb-139">This article covered the steps needed for deploying a multi-container Azure container instance.</span></span> <span data-ttu-id="da1bb-140">For an end-to-end Azure Container Instances experience, see the Azure Container Instances tutorial.</span><span class="sxs-lookup"><span data-stu-id="da1bb-140">For an end-to-end Azure Container Instances experience, see the Azure Container Instances tutorial.</span></span>

> [!div class="nextstepaction"]
> <span data-ttu-id="da1bb-141">[Azure Container Instances tutorial][aci-tutorial]</span><span class="sxs-lookup"><span data-stu-id="da1bb-141">[Azure Container Instances tutorial][aci-tutorial]</span></span>

<!-- LINKS - Internal -->
[aci-tutorial]: ./container-instances-tutorial-prepare-app.md
[az-container-logs]: /cli/azure/container#az-container-logs
[az-container-show]: /cli/azure/container#az-container-show
[az-group-create]: /cli/azure/group#az-group-create
[az-group-deployment-create]: /cli/azure/group/deployment#az-group-deployment-create
[template-reference]: https://docs.microsoft.com/azure/templates/microsoft.containerinstance/containergroups
