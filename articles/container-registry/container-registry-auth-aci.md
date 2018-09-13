---
title: Authenticate with Azure Container Registry from Azure Container Instances
description: Learn how to provide access to images in your private container registry from Azure Container Instances by using an Azure Active Directory service principal.
services: container-registry
author: mmacy
manager: jeconnoc
ms.service: container-registry
ms.topic: article
ms.date: 04/23/2018
ms.author: marsma
ms.openlocfilehash: daa9c098de0c410bd4033cc62ee911631eb3b634
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965553"
---
# <a name="authenticate-with-azure-container-registry-from-azure-container-instances"></a><span data-ttu-id="86454-103">Authenticate with Azure Container Registry from Azure Container Instances</span><span class="sxs-lookup"><span data-stu-id="86454-103">Authenticate with Azure Container Registry from Azure Container Instances</span></span>

<span data-ttu-id="86454-104">You can use an Azure Active Directory (Azure AD) service principal to provide access to your private container registries in Azure Container Registry.</span><span class="sxs-lookup"><span data-stu-id="86454-104">You can use an Azure Active Directory (Azure AD) service principal to provide access to your private container registries in Azure Container Registry.</span></span>

<span data-ttu-id="86454-105">In this article, you learn to create and configure an Azure AD service principal with *pull* permissions to your registry.</span><span class="sxs-lookup"><span data-stu-id="86454-105">In this article, you learn to create and configure an Azure AD service principal with *pull* permissions to your registry.</span></span> <span data-ttu-id="86454-106">Then, you start a container in Azure Container Instances (ACI) that pulls its image from your private registry, using the service principal for authentication.</span><span class="sxs-lookup"><span data-stu-id="86454-106">Then, you start a container in Azure Container Instances (ACI) that pulls its image from your private registry, using the service principal for authentication.</span></span>

## <a name="when-to-use-a-service-principal"></a><span data-ttu-id="86454-107">When to use a service principal</span><span class="sxs-lookup"><span data-stu-id="86454-107">When to use a service principal</span></span>

<span data-ttu-id="86454-108">You should use a service principal for authentication from ACI in **headless scenarios**, such as in applications or services that create container instances in an automated or otherwise unattended manner.</span><span class="sxs-lookup"><span data-stu-id="86454-108">You should use a service principal for authentication from ACI in **headless scenarios**, such as in applications or services that create container instances in an automated or otherwise unattended manner.</span></span>

<span data-ttu-id="86454-109">For example, if you have an automated script that runs nightly and creates a [task-based container instance](../container-instances/container-instances-restart-policy.md) to process some data, it can use a service principal with pull-only (Reader) permissions to authenticate to the registry.</span><span class="sxs-lookup"><span data-stu-id="86454-109">For example, if you have an automated script that runs nightly and creates a [task-based container instance](../container-instances/container-instances-restart-policy.md) to process some data, it can use a service principal with pull-only (Reader) permissions to authenticate to the registry.</span></span> <span data-ttu-id="86454-110">You can then rotate the service principal's credentials or revoke its access completely without affecting other services and applications.</span><span class="sxs-lookup"><span data-stu-id="86454-110">You can then rotate the service principal's credentials or revoke its access completely without affecting other services and applications.</span></span>

<span data-ttu-id="86454-111">Service principals should also be used when the registry [admin user](container-registry-authentication.md#admin-account) is disabled.</span><span class="sxs-lookup"><span data-stu-id="86454-111">Service principals should also be used when the registry [admin user](container-registry-authentication.md#admin-account) is disabled.</span></span>

[!INCLUDE [container-registry-service-principal](../../includes/container-registry-service-principal.md)]

## <a name="authenticate-using-the-service-principal"></a><span data-ttu-id="86454-112">Authenticate using the service principal</span><span class="sxs-lookup"><span data-stu-id="86454-112">Authenticate using the service principal</span></span>

<span data-ttu-id="86454-113">To launch a container in Azure Container Instances using a service principal, specify its ID for `--registry-username`, and its password for `--registry-password`.</span><span class="sxs-lookup"><span data-stu-id="86454-113">To launch a container in Azure Container Instances using a service principal, specify its ID for `--registry-username`, and its password for `--registry-password`.</span></span>

```azurecli-interactive
az container create \
    --resource-group myResourceGroup \
    --name mycontainer \
    --image mycontainerregistry.azurecr.io/myimage:v1 \
    --registry-login-server mycontainerregistry.azurecr.io \
    --registry-username <service-principal-ID> \
    --registry-password <service-principal-password>
```

## <a name="sample-scripts"></a><span data-ttu-id="86454-114">Sample scripts</span><span class="sxs-lookup"><span data-stu-id="86454-114">Sample scripts</span></span>

<span data-ttu-id="86454-115">You can find the preceding sample scripts for Azure CLI on GitHub, as well versions for Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="86454-115">You can find the preceding sample scripts for Azure CLI on GitHub, as well versions for Azure PowerShell:</span></span>

* <span data-ttu-id="86454-116">[Azure CLI][acr-scripts-cli]</span><span class="sxs-lookup"><span data-stu-id="86454-116">[Azure CLI][acr-scripts-cli]</span></span>
* <span data-ttu-id="86454-117">[Azure PowerShell][acr-scripts-psh]</span><span class="sxs-lookup"><span data-stu-id="86454-117">[Azure PowerShell][acr-scripts-psh]</span></span>

## <a name="next-steps"></a><span data-ttu-id="86454-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="86454-118">Next steps</span></span>

<span data-ttu-id="86454-119">The following articles contain additional details on working with service principals and ACR:</span><span class="sxs-lookup"><span data-stu-id="86454-119">The following articles contain additional details on working with service principals and ACR:</span></span>

* [<span data-ttu-id="86454-120">Azure Container Registry authentication with service principals</span><span class="sxs-lookup"><span data-stu-id="86454-120">Azure Container Registry authentication with service principals</span></span>](container-registry-auth-service-principal.md)
* [<span data-ttu-id="86454-121">Authenticate with Azure Container Registry from Azure Kubernetes Service (AKS)</span><span class="sxs-lookup"><span data-stu-id="86454-121">Authenticate with Azure Container Registry from Azure Kubernetes Service (AKS)</span></span>](container-registry-auth-aks.md)

<!-- IMAGES -->

<!-- LINKS - External -->
[acr-scripts-cli]: https://github.com/Azure/azure-docs-cli-python-samples/tree/master/container-registry
[acr-scripts-psh]: https://github.com/Azure/azure-docs-powershell-samples/tree/master/container-registry

<!-- LINKS - Internal -->
