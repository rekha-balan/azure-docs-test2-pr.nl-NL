---
title: Create private Docker registry - Azure portal | Microsoft Docs
description: Get started creating and managing private Docker container registries with the Azure portal
services: container-registry
documentationcenter: ''
author: stevelas
manager: balans
editor: dlepow
tags: ''
keywords: ''
ms.assetid: 53a3b3cb-ab4b-4560-bc00-366e2759f1a1
ms.service: container-registry
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/14/2016
ms.author: stevelas
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0b34eaa35ef3e4bc6f5d0a8fd09401f4d0eab12d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563894"
---
# <a name="create-a-private-docker-container-registry-using-the-azure-portal"></a><span data-ttu-id="7cfed-103">Create a private Docker container registry using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="7cfed-103">Create a private Docker container registry using the Azure portal</span></span>
<span data-ttu-id="7cfed-104">Use the Azure portal to create a container registry and manage its settings.</span><span class="sxs-lookup"><span data-stu-id="7cfed-104">Use the Azure portal to create a container registry and manage its settings.</span></span> <span data-ttu-id="7cfed-105">You can also create and manage container registries using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span><span class="sxs-lookup"><span data-stu-id="7cfed-105">You can also create and manage container registries using the [Azure CLI 2.0 commands](container-registry-get-started-azure-cli.md) or programmatically with the Container Registry [REST API](https://go.microsoft.com/fwlink/p/?linkid=834376).</span></span>

<span data-ttu-id="7cfed-106">For background and concepts, see [the overview](container-registry-intro.md).</span><span class="sxs-lookup"><span data-stu-id="7cfed-106">For background and concepts, see [the overview](container-registry-intro.md).</span></span>



## <a name="create-a-container-registry"></a><span data-ttu-id="7cfed-107">Create a container registry</span><span class="sxs-lookup"><span data-stu-id="7cfed-107">Create a container registry</span></span>
1. <span data-ttu-id="7cfed-108">In the [Azure portal](https://portal.azure.com), click **+ New**.</span><span class="sxs-lookup"><span data-stu-id="7cfed-108">In the [Azure portal](https://portal.azure.com), click **+ New**.</span></span>
2. <span data-ttu-id="7cfed-109">Search the marketplace for **Azure container registry**.</span><span class="sxs-lookup"><span data-stu-id="7cfed-109">Search the marketplace for **Azure container registry**.</span></span>
3. <span data-ttu-id="7cfed-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span><span class="sxs-lookup"><span data-stu-id="7cfed-110">Select **Azure Container Registry**, with publisher **Microsoft**.</span></span>
    <span data-ttu-id="7cfed-111">![Container Registry service in Azure Marketplace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-registry/media/container-registry-get-started-portal/container-registry-marketplace.png)</span><span class="sxs-lookup"><span data-stu-id="7cfed-111">![Container Registry service in Azure Marketplace](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-registry/media/container-registry-get-started-portal/container-registry-marketplace.png)</span></span>
4. <span data-ttu-id="7cfed-112">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="7cfed-112">Click **Create**.</span></span> <span data-ttu-id="7cfed-113">The **Azure Container Registry** blade appears.</span><span class="sxs-lookup"><span data-stu-id="7cfed-113">The **Azure Container Registry** blade appears.</span></span>

    ![Container registry settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-registry/media/container-registry-get-started-portal/container-registry-settings.png)
5. <span data-ttu-id="7cfed-115">In the **Azure Container Registry** blade, enter the following information.</span><span class="sxs-lookup"><span data-stu-id="7cfed-115">In the **Azure Container Registry** blade, enter the following information.</span></span> <span data-ttu-id="7cfed-116">Click **Create** when you are done.</span><span class="sxs-lookup"><span data-stu-id="7cfed-116">Click **Create** when you are done.</span></span>

    <span data-ttu-id="7cfed-117">a.</span><span class="sxs-lookup"><span data-stu-id="7cfed-117">a.</span></span> <span data-ttu-id="7cfed-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span><span class="sxs-lookup"><span data-stu-id="7cfed-118">**Registry name**: A globally unique top-level domain name for your specific registry.</span></span> <span data-ttu-id="7cfed-119">In this example, the registry name is *myRegistry01*, but substitute a unique name of your own.</span><span class="sxs-lookup"><span data-stu-id="7cfed-119">In this example, the registry name is *myRegistry01*, but substitute a unique name of your own.</span></span> <span data-ttu-id="7cfed-120">The name can contain only letters and numbers.</span><span class="sxs-lookup"><span data-stu-id="7cfed-120">The name can contain only letters and numbers.</span></span>

    <span data-ttu-id="7cfed-121">b.</span><span class="sxs-lookup"><span data-stu-id="7cfed-121">b.</span></span> <span data-ttu-id="7cfed-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span><span class="sxs-lookup"><span data-stu-id="7cfed-122">**Resource group**: Select an existing [resource group](../azure-resource-manager/resource-group-overview.md#resource-groups) or type the name for a new one.</span></span>

    <span data-ttu-id="7cfed-123">c.</span><span class="sxs-lookup"><span data-stu-id="7cfed-123">c.</span></span> <span data-ttu-id="7cfed-124">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span><span class="sxs-lookup"><span data-stu-id="7cfed-124">**Location**: Select an Azure datacenter location where the service is [available](https://azure.microsoft.com/regions/services/), such as **South Central US**.</span></span>

    <span data-ttu-id="7cfed-125">d.</span><span class="sxs-lookup"><span data-stu-id="7cfed-125">d.</span></span> <span data-ttu-id="7cfed-126">**Admin user**: If you want, enable an admin user to access the registry.</span><span class="sxs-lookup"><span data-stu-id="7cfed-126">**Admin user**: If you want, enable an admin user to access the registry.</span></span> <span data-ttu-id="7cfed-127">You can change this setting after creating the registry.</span><span class="sxs-lookup"><span data-stu-id="7cfed-127">You can change this setting after creating the registry.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="7cfed-128">In addition to providing access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span><span class="sxs-lookup"><span data-stu-id="7cfed-128">In addition to providing access through an admin user account, container registries support authentication backed by Azure Active Directory service principals.</span></span> <span data-ttu-id="7cfed-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7cfed-129">For more information and considerations, see [Authenticate with a container registry](container-registry-authentication.md).</span></span>


    <span data-ttu-id="7cfed-130">e.</span><span class="sxs-lookup"><span data-stu-id="7cfed-130">e.</span></span> <span data-ttu-id="7cfed-131">**Storage account**: Use the default setting to create a [storage account](../storage/storage-introduction.md), or select an existing storage account in the same location.</span><span class="sxs-lookup"><span data-stu-id="7cfed-131">**Storage account**: Use the default setting to create a [storage account](../storage/storage-introduction.md), or select an existing storage account in the same location.</span></span> <span data-ttu-id="7cfed-132">Currently Premium Storage is not supported.</span><span class="sxs-lookup"><span data-stu-id="7cfed-132">Currently Premium Storage is not supported.</span></span>


## <a name="manage-registry-settings"></a><span data-ttu-id="7cfed-133">Manage registry settings</span><span class="sxs-lookup"><span data-stu-id="7cfed-133">Manage registry settings</span></span>
<span data-ttu-id="7cfed-134">After creating the registry, find the registry settings by starting at the **Container Registries** blade in the portal.</span><span class="sxs-lookup"><span data-stu-id="7cfed-134">After creating the registry, find the registry settings by starting at the **Container Registries** blade in the portal.</span></span> <span data-ttu-id="7cfed-135">For example, you might need the settings to log in to your registry, or you might want to enable or disable the admin user.</span><span class="sxs-lookup"><span data-stu-id="7cfed-135">For example, you might need the settings to log in to your registry, or you might want to enable or disable the admin user.</span></span>

1. <span data-ttu-id="7cfed-136">On the **Container Registries** blade, click the name of your registry.</span><span class="sxs-lookup"><span data-stu-id="7cfed-136">On the **Container Registries** blade, click the name of your registry.</span></span>

    ![Container registry blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-registry/media/container-registry-get-started-portal/container-registry-blade.png)
2. <span data-ttu-id="7cfed-138">To manage access settings, click **Access key**.</span><span class="sxs-lookup"><span data-stu-id="7cfed-138">To manage access settings, click **Access key**.</span></span>

    ![Container registry access](https://docstestmedia1.blob.core.windows.net/azure-media/articles/container-registry/media/container-registry-get-started-portal/container-registry-access.png)
3. <span data-ttu-id="7cfed-140">Note the following settings:</span><span class="sxs-lookup"><span data-stu-id="7cfed-140">Note the following settings:</span></span>

   * <span data-ttu-id="7cfed-141">**Login server** - The fully qualified name you use to log in to the registry.</span><span class="sxs-lookup"><span data-stu-id="7cfed-141">**Login server** - The fully qualified name you use to log in to the registry.</span></span> <span data-ttu-id="7cfed-142">In this example, it is `myregistry01.azurecr.io`.</span><span class="sxs-lookup"><span data-stu-id="7cfed-142">In this example, it is `myregistry01.azurecr.io`.</span></span>
   * <span data-ttu-id="7cfed-143">**Admin user** - Toggle to enable or disable the registry's admin user account.</span><span class="sxs-lookup"><span data-stu-id="7cfed-143">**Admin user** - Toggle to enable or disable the registry's admin user account.</span></span>
   * <span data-ttu-id="7cfed-144">**Username** and **Password** - The credentials of the admin user account (if enabled) you can use to log in to the registry.</span><span class="sxs-lookup"><span data-stu-id="7cfed-144">**Username** and **Password** - The credentials of the admin user account (if enabled) you can use to log in to the registry.</span></span> <span data-ttu-id="7cfed-145">You can optionally regenerate the passwords.</span><span class="sxs-lookup"><span data-stu-id="7cfed-145">You can optionally regenerate the passwords.</span></span> <span data-ttu-id="7cfed-146">Two passwords are created so that you can maintain connections to the registry by using one password while you regenerate the other password.</span><span class="sxs-lookup"><span data-stu-id="7cfed-146">Two passwords are created so that you can maintain connections to the registry by using one password while you regenerate the other password.</span></span> <span data-ttu-id="7cfed-147">To authenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="7cfed-147">To authenticate with a service principal instead, see [Authenticate with a private Docker container registry](container-registry-authentication.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7cfed-148">Next steps</span><span class="sxs-lookup"><span data-stu-id="7cfed-148">Next steps</span></span>
* [<span data-ttu-id="7cfed-149">Push your first image using the Docker CLI</span><span class="sxs-lookup"><span data-stu-id="7cfed-149">Push your first image using the Docker CLI</span></span>](container-registry-get-started-docker-cli.md)




