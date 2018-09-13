---
title: Authenticate with an Azure container registry
description: Authentication options for an Azure container registry, including Azure Active Directory service principals direct and registry login.
services: container-registry
author: stevelas
manager: jeconnoc
ms.service: container-registry
ms.topic: article
ms.date: 01/23/2018
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: be8adf9779c2d168c0ac7a0ed7dbc3e85935df68
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44791120"
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="13bda-103">Authenticate with a private Docker container registry</span><span class="sxs-lookup"><span data-stu-id="13bda-103">Authenticate with a private Docker container registry</span></span>

<span data-ttu-id="13bda-104">There are several ways to authenticate with an Azure container registry, each of which is applicable to one or more registry usage scenarios.</span><span class="sxs-lookup"><span data-stu-id="13bda-104">There are several ways to authenticate with an Azure container registry, each of which is applicable to one or more registry usage scenarios.</span></span>

<span data-ttu-id="13bda-105">You can log in to a registry directly via [individual login](#individual-login-with-azure-ad), and your applications and container orchestrators can perform unattended, or "headless," authentication by using an Azure Active Directory (Azure AD) [service principal](#service-principal).</span><span class="sxs-lookup"><span data-stu-id="13bda-105">You can log in to a registry directly via [individual login](#individual-login-with-azure-ad), and your applications and container orchestrators can perform unattended, or "headless," authentication by using an Azure Active Directory (Azure AD) [service principal](#service-principal).</span></span>

<span data-ttu-id="13bda-106">Azure Container Registry does not support unauthenticated Docker operations or anonymous access.</span><span class="sxs-lookup"><span data-stu-id="13bda-106">Azure Container Registry does not support unauthenticated Docker operations or anonymous access.</span></span> <span data-ttu-id="13bda-107">For public images, you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="13bda-107">For public images, you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

## <a name="individual-login-with-azure-ad"></a><span data-ttu-id="13bda-108">Individual login with Azure AD</span><span class="sxs-lookup"><span data-stu-id="13bda-108">Individual login with Azure AD</span></span>

<span data-ttu-id="13bda-109">When working with your registry directly, such as pulling images to and pushing images from your development workstation, authenticate by using the [az acr login](/cli/azure/acr?view=azure-cli-latest#az-acr-login) command in the [Azure CLI](/cli/azure/install-azure-cli):</span><span class="sxs-lookup"><span data-stu-id="13bda-109">When working with your registry directly, such as pulling images to and pushing images from your development workstation, authenticate by using the [az acr login](/cli/azure/acr?view=azure-cli-latest#az-acr-login) command in the [Azure CLI](/cli/azure/install-azure-cli):</span></span>

```azurecli
az acr login --name <acrName>
```

<span data-ttu-id="13bda-110">When you log in with `az acr login`, the CLI uses the token created when you executed `az login` to seamlessly authenticate your session with your registry.</span><span class="sxs-lookup"><span data-stu-id="13bda-110">When you log in with `az acr login`, the CLI uses the token created when you executed `az login` to seamlessly authenticate your session with your registry.</span></span> <span data-ttu-id="13bda-111">Once you've logged in this way, your credentials are cached, and subsequent `docker` commands do not require a username or password.</span><span class="sxs-lookup"><span data-stu-id="13bda-111">Once you've logged in this way, your credentials are cached, and subsequent `docker` commands do not require a username or password.</span></span> <span data-ttu-id="13bda-112">If your token expires, you can refresh it by using the `az acr login` command again to reauthenticate.</span><span class="sxs-lookup"><span data-stu-id="13bda-112">If your token expires, you can refresh it by using the `az acr login` command again to reauthenticate.</span></span> <span data-ttu-id="13bda-113">Using `az acr login` with Azure identities provides [role-based access](../role-based-access-control/role-assignments-portal.md).</span><span class="sxs-lookup"><span data-stu-id="13bda-113">Using `az acr login` with Azure identities provides [role-based access](../role-based-access-control/role-assignments-portal.md).</span></span>

## <a name="service-principal"></a><span data-ttu-id="13bda-114">Service principal</span><span class="sxs-lookup"><span data-stu-id="13bda-114">Service principal</span></span>

<span data-ttu-id="13bda-115">You can assign a [service principal](../active-directory/develop/app-objects-and-service-principals.md) to your registry, and your application or service can use it for headless authentication.</span><span class="sxs-lookup"><span data-stu-id="13bda-115">You can assign a [service principal](../active-directory/develop/app-objects-and-service-principals.md) to your registry, and your application or service can use it for headless authentication.</span></span> <span data-ttu-id="13bda-116">Service principals allow [role-based access](../role-based-access-control/role-assignments-portal.md) to a registry, and you can assign multiple service principals to a registry.</span><span class="sxs-lookup"><span data-stu-id="13bda-116">Service principals allow [role-based access](../role-based-access-control/role-assignments-portal.md) to a registry, and you can assign multiple service principals to a registry.</span></span> <span data-ttu-id="13bda-117">Multiple service principals allow you to define different access for different applications.</span><span class="sxs-lookup"><span data-stu-id="13bda-117">Multiple service principals allow you to define different access for different applications.</span></span>

<span data-ttu-id="13bda-118">The available roles are:</span><span class="sxs-lookup"><span data-stu-id="13bda-118">The available roles are:</span></span>

  * <span data-ttu-id="13bda-119">**Reader**: pull</span><span class="sxs-lookup"><span data-stu-id="13bda-119">**Reader**: pull</span></span>
  * <span data-ttu-id="13bda-120">**Contributor**: pull and push</span><span class="sxs-lookup"><span data-stu-id="13bda-120">**Contributor**: pull and push</span></span>
  * <span data-ttu-id="13bda-121">**Owner**: pull, push, and assign roles to other users</span><span class="sxs-lookup"><span data-stu-id="13bda-121">**Owner**: pull, push, and assign roles to other users</span></span>

<span data-ttu-id="13bda-122">Service principals enable headless connectivity to a registry in both push and pull scenarios like the following:</span><span class="sxs-lookup"><span data-stu-id="13bda-122">Service principals enable headless connectivity to a registry in both push and pull scenarios like the following:</span></span>

  * <span data-ttu-id="13bda-123">*Reader*: Container deployments from a registry to orchestration systems including Kubernetes, DC/OS, and Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="13bda-123">*Reader*: Container deployments from a registry to orchestration systems including Kubernetes, DC/OS, and Docker Swarm.</span></span> <span data-ttu-id="13bda-124">You can also pull from container registries to related Azure services such as [AKS](../aks/index.yml), [App Service](../app-service/index.yml), [Batch](../batch/index.yml), [Service Fabric](/azure/service-fabric/), and others.</span><span class="sxs-lookup"><span data-stu-id="13bda-124">You can also pull from container registries to related Azure services such as [AKS](../aks/index.yml), [App Service](../app-service/index.yml), [Batch](../batch/index.yml), [Service Fabric](/azure/service-fabric/), and others.</span></span>

  * <span data-ttu-id="13bda-125">*Contributor*: Continuous integration and deployment solutions like Azure DevOps or Jenkins that build container images and push them to a registry.</span><span class="sxs-lookup"><span data-stu-id="13bda-125">*Contributor*: Continuous integration and deployment solutions like Azure DevOps or Jenkins that build container images and push them to a registry.</span></span>

> [!TIP]
> <span data-ttu-id="13bda-126">You can regenerate the password of a service principal by running the [az ad sp reset-credentials](/cli/azure/ad/sp?view=azure-cli-latest#az-ad-sp-reset-credentials) command.</span><span class="sxs-lookup"><span data-stu-id="13bda-126">You can regenerate the password of a service principal by running the [az ad sp reset-credentials](/cli/azure/ad/sp?view=azure-cli-latest#az-ad-sp-reset-credentials) command.</span></span>
>

<span data-ttu-id="13bda-127">You can also log in directly with a service principal.</span><span class="sxs-lookup"><span data-stu-id="13bda-127">You can also log in directly with a service principal.</span></span> <span data-ttu-id="13bda-128">Provide the app ID and password of the service principal to the `docker login` command:</span><span class="sxs-lookup"><span data-stu-id="13bda-128">Provide the app ID and password of the service principal to the `docker login` command:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="13bda-129">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span><span class="sxs-lookup"><span data-stu-id="13bda-129">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span></span>

<span data-ttu-id="13bda-130">Depending on the version of Docker you have installed, you might see a security warning recommending the use of the `--password-stdin` parameter.</span><span class="sxs-lookup"><span data-stu-id="13bda-130">Depending on the version of Docker you have installed, you might see a security warning recommending the use of the `--password-stdin` parameter.</span></span> <span data-ttu-id="13bda-131">While its use is outside the scope of this article, we recommend following this best practice.</span><span class="sxs-lookup"><span data-stu-id="13bda-131">While its use is outside the scope of this article, we recommend following this best practice.</span></span> <span data-ttu-id="13bda-132">For more information, see the [docker login](https://docs.docker.com/engine/reference/commandline/login/) command reference.</span><span class="sxs-lookup"><span data-stu-id="13bda-132">For more information, see the [docker login](https://docs.docker.com/engine/reference/commandline/login/) command reference.</span></span>

<span data-ttu-id="13bda-133">For more information on using a service principal for headless authentication to ACR, see [Azure Container Registry authentication with service principals](container-registry-auth-service-principal.md).</span><span class="sxs-lookup"><span data-stu-id="13bda-133">For more information on using a service principal for headless authentication to ACR, see [Azure Container Registry authentication with service principals](container-registry-auth-service-principal.md).</span></span>

## <a name="admin-account"></a><span data-ttu-id="13bda-134">Admin account</span><span class="sxs-lookup"><span data-stu-id="13bda-134">Admin account</span></span>

<span data-ttu-id="13bda-135">Each container registry includes an admin user account, which is disabled by default.</span><span class="sxs-lookup"><span data-stu-id="13bda-135">Each container registry includes an admin user account, which is disabled by default.</span></span> <span data-ttu-id="13bda-136">You can enable the admin user and manage its credentials in the [Azure portal](container-registry-get-started-portal.md#create-a-container-registry), or by using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="13bda-136">You can enable the admin user and manage its credentials in the [Azure portal](container-registry-get-started-portal.md#create-a-container-registry), or by using the Azure CLI.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="13bda-137">The admin account is designed for a single user to access the registry, mainly for testing purposes.</span><span class="sxs-lookup"><span data-stu-id="13bda-137">The admin account is designed for a single user to access the registry, mainly for testing purposes.</span></span> <span data-ttu-id="13bda-138">We do not recommend sharing the admin account credentials with multiple users.</span><span class="sxs-lookup"><span data-stu-id="13bda-138">We do not recommend sharing the admin account credentials with multiple users.</span></span> <span data-ttu-id="13bda-139">All users authenticating with the admin account appear as a single user with push and pull access to the registry.</span><span class="sxs-lookup"><span data-stu-id="13bda-139">All users authenticating with the admin account appear as a single user with push and pull access to the registry.</span></span> <span data-ttu-id="13bda-140">Changing or disabling this account disables registry access for all users who use its credentials.</span><span class="sxs-lookup"><span data-stu-id="13bda-140">Changing or disabling this account disables registry access for all users who use its credentials.</span></span> <span data-ttu-id="13bda-141">Individual identity is recommended for users and service principals for headless scenarios.</span><span class="sxs-lookup"><span data-stu-id="13bda-141">Individual identity is recommended for users and service principals for headless scenarios.</span></span>
>

<span data-ttu-id="13bda-142">The admin account is provided with two passwords, both of which can be regenerated.</span><span class="sxs-lookup"><span data-stu-id="13bda-142">The admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="13bda-143">Two passwords allow you to maintain connection to the registry by using one password while you regenerate the other.</span><span class="sxs-lookup"><span data-stu-id="13bda-143">Two passwords allow you to maintain connection to the registry by using one password while you regenerate the other.</span></span> <span data-ttu-id="13bda-144">If the admin account is enabled, you can pass the username and either password to the `docker login` command for basic authentication to the registry.</span><span class="sxs-lookup"><span data-stu-id="13bda-144">If the admin account is enabled, you can pass the username and either password to the `docker login` command for basic authentication to the registry.</span></span> <span data-ttu-id="13bda-145">For example:</span><span class="sxs-lookup"><span data-stu-id="13bda-145">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

<span data-ttu-id="13bda-146">Again, Docker recommends that you use the `--password-stdin` parameter instead of supplying it on the command line for increased security.</span><span class="sxs-lookup"><span data-stu-id="13bda-146">Again, Docker recommends that you use the `--password-stdin` parameter instead of supplying it on the command line for increased security.</span></span> <span data-ttu-id="13bda-147">You can also specify only your username, without `-p`, and enter your password when prompted.</span><span class="sxs-lookup"><span data-stu-id="13bda-147">You can also specify only your username, without `-p`, and enter your password when prompted.</span></span>

<span data-ttu-id="13bda-148">To enable the admin user for an existing registry, you can use the `--admin-enabled` parameter of the [az acr update](/cli/azure/acr?view=azure-cli-latest#az-acr-update) command in the Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="13bda-148">To enable the admin user for an existing registry, you can use the `--admin-enabled` parameter of the [az acr update](/cli/azure/acr?view=azure-cli-latest#az-acr-update) command in the Azure CLI:</span></span>

```azurecli
az acr update -n <acrName> --admin-enabled true
```

<span data-ttu-id="13bda-149">You can enable the admin user in the Azure portal by navigating your registry, selecting **Access keys** under **SETTINGS**, then **Enable** under **Admin user**.</span><span class="sxs-lookup"><span data-stu-id="13bda-149">You can enable the admin user in the Azure portal by navigating your registry, selecting **Access keys** under **SETTINGS**, then **Enable** under **Admin user**.</span></span>

![Enable admin user UI in the Azure portal][auth-portal-01]

## <a name="next-steps"></a><span data-ttu-id="13bda-151">Next steps</span><span class="sxs-lookup"><span data-stu-id="13bda-151">Next steps</span></span>

* [<span data-ttu-id="13bda-152">Push your first image using the Azure CLI</span><span class="sxs-lookup"><span data-stu-id="13bda-152">Push your first image using the Azure CLI</span></span>](container-registry-get-started-azure-cli.md)

<!-- IMAGES -->
[auth-portal-01]: ./media/container-registry-authentication/auth-portal-01.png
