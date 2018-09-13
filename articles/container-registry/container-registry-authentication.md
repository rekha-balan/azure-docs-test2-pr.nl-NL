---
title: Authenticate with an Azure container registry | Microsoft Docs
description: How to log in to an Azure container registry using an Azure Active Directory service principal or an admin account
services: container-registry
documentationcenter: ''
author: stevelas
manager: balans
editor: cristyg
tags: ''
keywords: ''
ms.assetid: 128a937a-766a-415b-b9fc-35a6c2f27417
ms.service: container-registry
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/14/2016
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ae6af47c82a5c0425f6cd53b8ba1134797505e6c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553183"
---
# <a name="authenticate-with-a-private-docker-container-registry"></a><span data-ttu-id="e0a9b-103">Authenticate with a private Docker container registry</span><span class="sxs-lookup"><span data-stu-id="e0a9b-103">Authenticate with a private Docker container registry</span></span>
<span data-ttu-id="e0a9b-104">To work with container images in an Azure container registry, you log in using the `docker login` command.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-104">To work with container images in an Azure container registry, you log in using the `docker login` command.</span></span> <span data-ttu-id="e0a9b-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-105">You can log in using either an **[Azure Active Directory service principal](../active-directory/active-directory-application-objects.md)** or a registry-specific **admin account**.</span></span> <span data-ttu-id="e0a9b-106">This article provides more detail about these identities.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-106">This article provides more detail about these identities.</span></span>



## <a name="service-principal"></a><span data-ttu-id="e0a9b-107">Service principal</span><span class="sxs-lookup"><span data-stu-id="e0a9b-107">Service principal</span></span>

<span data-ttu-id="e0a9b-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) to your registry and use it for basic Docker authentication.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-108">You can [assign a service principal](container-registry-get-started-azure-cli.md#assign-a-service-principal) to your registry and use it for basic Docker authentication.</span></span> <span data-ttu-id="e0a9b-109">Using a service principal is recommended for most scenarios.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-109">Using a service principal is recommended for most scenarios.</span></span> <span data-ttu-id="e0a9b-110">Provide the app ID and password of the service principal to the `docker login` command, as shown in the following example:</span><span class="sxs-lookup"><span data-stu-id="e0a9b-110">Provide the app ID and password of the service principal to the `docker login` command, as shown in the following example:</span></span>

```
docker login myregistry.azurecr.io -u xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx -p myPassword
```

<span data-ttu-id="e0a9b-111">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-111">Once logged in, Docker caches the credentials, so you don't need to remember the app ID.</span></span>

> [!TIP]
> <span data-ttu-id="e0a9b-112">If you want, you can regenerate the password of a service principal by running the `az ad sp reset-credentials` command.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-112">If you want, you can regenerate the password of a service principal by running the `az ad sp reset-credentials` command.</span></span>
>


<span data-ttu-id="e0a9b-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) to a registry.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-113">Service principals allow [role-based access](../active-directory/role-based-access-control-configure.md) to a registry.</span></span> <span data-ttu-id="e0a9b-114">Available roles are:</span><span class="sxs-lookup"><span data-stu-id="e0a9b-114">Available roles are:</span></span>
  * <span data-ttu-id="e0a9b-115">Reader (pull only access).</span><span class="sxs-lookup"><span data-stu-id="e0a9b-115">Reader (pull only access).</span></span>
  * <span data-ttu-id="e0a9b-116">Contributor (pull and push).</span><span class="sxs-lookup"><span data-stu-id="e0a9b-116">Contributor (pull and push).</span></span>
  * <span data-ttu-id="e0a9b-117">Owner (pull, push, and assign roles to other users).</span><span class="sxs-lookup"><span data-stu-id="e0a9b-117">Owner (pull, push, and assign roles to other users).</span></span>

<span data-ttu-id="e0a9b-118">Anonymous access is not available on Azure Container Registries.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-118">Anonymous access is not available on Azure Container Registries.</span></span> <span data-ttu-id="e0a9b-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span><span class="sxs-lookup"><span data-stu-id="e0a9b-119">For public images you can use [Docker Hub](https://docs.docker.com/docker-hub/).</span></span>

<span data-ttu-id="e0a9b-120">You can assign multiple service principals to a registry, which allows you to define access for different users or applications.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-120">You can assign multiple service principals to a registry, which allows you to define access for different users or applications.</span></span> <span data-ttu-id="e0a9b-121">Service principals also enable "headless" connectivity to a registry in developer or DevOps scenarios such as the following examples:</span><span class="sxs-lookup"><span data-stu-id="e0a9b-121">Service principals also enable "headless" connectivity to a registry in developer or DevOps scenarios such as the following examples:</span></span>

  * <span data-ttu-id="e0a9b-122">Container deployments from a registry to orchestration systems including DC/OS, Docker Swarm and Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-122">Container deployments from a registry to orchestration systems including DC/OS, Docker Swarm and Kubernetes.</span></span> <span data-ttu-id="e0a9b-123">You can also pull container registries to related Azure services such as [Container Service](../container-service/index.md), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](../service-fabric/index.md), and others.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-123">You can also pull container registries to related Azure services such as [Container Service](../container-service/index.md), [App Service](../app-service/index.md), [Batch](../batch/index.md), [Service Fabric](../service-fabric/index.md), and others.</span></span>

  * <span data-ttu-id="e0a9b-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them to a registry.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-124">Continuous integration and deployment solutions (such as Visual Studio Team Services or Jenkins) that build container images and push them to a registry.</span></span>





## <a name="admin-account"></a><span data-ttu-id="e0a9b-125">Admin account</span><span class="sxs-lookup"><span data-stu-id="e0a9b-125">Admin account</span></span>
<span data-ttu-id="e0a9b-126">With each registry you create, an admin account gets created automatically.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-126">With each registry you create, an admin account gets created automatically.</span></span> <span data-ttu-id="e0a9b-127">By default the account is disabled, but you can enable it and manage the credentials, for example through the [portal](container-registry-get-started-portal.md#manage-registry-settings) or using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span><span class="sxs-lookup"><span data-stu-id="e0a9b-127">By default the account is disabled, but you can enable it and manage the credentials, for example through the [portal](container-registry-get-started-portal.md#manage-registry-settings) or using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md#manage-admin-credentials).</span></span> <span data-ttu-id="e0a9b-128">Each admin account is provided with two passwords, both of which can be regenerated.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-128">Each admin account is provided with two passwords, both of which can be regenerated.</span></span> <span data-ttu-id="e0a9b-129">The two passwords allow you to maintain connections to the registry by using one password while you regenerate the other password.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-129">The two passwords allow you to maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="e0a9b-130">If the account is enabled, you can pass the user name and either password to the `docker login` command for basic authentication to the registry.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-130">If the account is enabled, you can pass the user name and either password to the `docker login` command for basic authentication to the registry.</span></span> <span data-ttu-id="e0a9b-131">For example:</span><span class="sxs-lookup"><span data-stu-id="e0a9b-131">For example:</span></span>

```
docker login myregistry.azurecr.io -u myAdminName -p myPassword1
```

> [!IMPORTANT]
> <span data-ttu-id="e0a9b-132">The admin account is designed for a single user to access the registry, mainly for test purposes.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-132">The admin account is designed for a single user to access the registry, mainly for test purposes.</span></span> <span data-ttu-id="e0a9b-133">It is not recommended to share the admin account credentials among other users.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-133">It is not recommended to share the admin account credentials among other users.</span></span> <span data-ttu-id="e0a9b-134">All users appear as a single user to the registry.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-134">All users appear as a single user to the registry.</span></span> <span data-ttu-id="e0a9b-135">Changing or disabling this account disables registry access for all users who use the credentials.</span><span class="sxs-lookup"><span data-stu-id="e0a9b-135">Changing or disabling this account disables registry access for all users who use the credentials.</span></span>
>


### <a name="next-steps"></a><span data-ttu-id="e0a9b-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="e0a9b-136">Next steps</span></span>
* <span data-ttu-id="e0a9b-137">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md).</span><span class="sxs-lookup"><span data-stu-id="e0a9b-137">[Push your first image using the Docker CLI](container-registry-get-started-docker-cli.md).</span></span>
* <span data-ttu-id="e0a9b-138">For more information about authentication in the Container Registry preview, see the [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span><span class="sxs-lookup"><span data-stu-id="e0a9b-138">For more information about authentication in the Container Registry preview, see the [blog post](https://blogs.msdn.microsoft.com/stevelasker/2016/11/17/azure-container-registry-user-accounts/).</span></span>
