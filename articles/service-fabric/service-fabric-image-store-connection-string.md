---
title: Azure Service Fabric image store connnection string | Microsoft Docs
description: Understand the image store connection string
services: service-fabric
documentationcenter: .net
author: alexwun
manager: timlt
editor: ''
ms.assetid: 00f8059d-9d53-4cb8-b44a-b25149de3030
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 02/08/2017
ms.author: alexwun
ms.openlocfilehash: 4e94d66aae9e4297bb0d238c9602150fe9f975e4
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555977"
---
# <a name="understand-the-imagestoreconnectionstring-setting"></a><span data-ttu-id="1d365-103">Understand the ImageStoreConnectionString setting</span><span class="sxs-lookup"><span data-stu-id="1d365-103">Understand the ImageStoreConnectionString setting</span></span>

<span data-ttu-id="1d365-104">In some of our documentation, we briefly mention the existence of an "ImageStoreConnectionString" parameter without describing what it really means.</span><span class="sxs-lookup"><span data-stu-id="1d365-104">In some of our documentation, we briefly mention the existence of an "ImageStoreConnectionString" parameter without describing what it really means.</span></span> <span data-ttu-id="1d365-105">And after going through an article like [Deploy and remove applications using PowerShell][10], it looks like all you do is copy/paste the value as it appears in the cluster manifest of the target cluster.</span><span class="sxs-lookup"><span data-stu-id="1d365-105">And after going through an article like [Deploy and remove applications using PowerShell][10], it looks like all you do is copy/paste the value as it appears in the cluster manifest of the target cluster.</span></span> <span data-ttu-id="1d365-106">So the setting must be configurable per cluster, but when you create a cluster through the [Azure portal][11], there's no option to configure this setting and it's always "fabric:ImageStore".</span><span class="sxs-lookup"><span data-stu-id="1d365-106">So the setting must be configurable per cluster, but when you create a cluster through the [Azure portal][11], there's no option to configure this setting and it's always "fabric:ImageStore".</span></span> <span data-ttu-id="1d365-107">What's the purpose of this setting then?</span><span class="sxs-lookup"><span data-stu-id="1d365-107">What's the purpose of this setting then?</span></span>

![Cluster Manifest][img_cm]

<span data-ttu-id="1d365-109">Service Fabric started off as a platform for internal Microsoft consumption by many diverse teams, so some aspects of it are highly customizable - the "Image Store" is one such aspect.</span><span class="sxs-lookup"><span data-stu-id="1d365-109">Service Fabric started off as a platform for internal Microsoft consumption by many diverse teams, so some aspects of it are highly customizable - the "Image Store" is one such aspect.</span></span> <span data-ttu-id="1d365-110">Essentially, the Image Store is a pluggable repository for storing application packages.</span><span class="sxs-lookup"><span data-stu-id="1d365-110">Essentially, the Image Store is a pluggable repository for storing application packages.</span></span> <span data-ttu-id="1d365-111">When your application is deployed to a node in the cluster, that node downloads the contents of your application package from the Image Store.</span><span class="sxs-lookup"><span data-stu-id="1d365-111">When your application is deployed to a node in the cluster, that node downloads the contents of your application package from the Image Store.</span></span> <span data-ttu-id="1d365-112">The ImageStoreConnectionString is a setting that includes all the necessary information for both clients and nodes to find the correct Image Store for a given cluster.</span><span class="sxs-lookup"><span data-stu-id="1d365-112">The ImageStoreConnectionString is a setting that includes all the necessary information for both clients and nodes to find the correct Image Store for a given cluster.</span></span>

<span data-ttu-id="1d365-113">There are currently three possible kinds of Image Store providers and their corresponding connection strings are as follows:</span><span class="sxs-lookup"><span data-stu-id="1d365-113">There are currently three possible kinds of Image Store providers and their corresponding connection strings are as follows:</span></span>

1. <span data-ttu-id="1d365-114">Image Store Service: "fabric:ImageStore"</span><span class="sxs-lookup"><span data-stu-id="1d365-114">Image Store Service: "fabric:ImageStore"</span></span>

2. <span data-ttu-id="1d365-115">File System: "file:[file system path]"</span><span class="sxs-lookup"><span data-stu-id="1d365-115">File System: "file:[file system path]"</span></span>

3. <span data-ttu-id="1d365-116">Azure Storage: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"</span><span class="sxs-lookup"><span data-stu-id="1d365-116">Azure Storage: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"</span></span>

<span data-ttu-id="1d365-117">The provider type used in production is the Image Store Service, which is a stateful persisted system service that you can see from Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="1d365-117">The provider type used in production is the Image Store Service, which is a stateful persisted system service that you can see from Service Fabric Explorer.</span></span> 

![Image Store Service][img_is]

<span data-ttu-id="1d365-119">Hosting the Image Store in a system service within the cluster itself eliminates external dependencies for the package repository and gives us more control over the locality of storage.</span><span class="sxs-lookup"><span data-stu-id="1d365-119">Hosting the Image Store in a system service within the cluster itself eliminates external dependencies for the package repository and gives us more control over the locality of storage.</span></span> <span data-ttu-id="1d365-120">Future improvements around the Image Store are likely to target the Image Store provider first, if not exclusively.</span><span class="sxs-lookup"><span data-stu-id="1d365-120">Future improvements around the Image Store are likely to target the Image Store provider first, if not exclusively.</span></span> <span data-ttu-id="1d365-121">The connection string for the Image Store Service provider doesn't have any unique information since the client is already connected to the target cluster.</span><span class="sxs-lookup"><span data-stu-id="1d365-121">The connection string for the Image Store Service provider doesn't have any unique information since the client is already connected to the target cluster.</span></span> <span data-ttu-id="1d365-122">The client only needs to know that protocols targeting the system service should be used.</span><span class="sxs-lookup"><span data-stu-id="1d365-122">The client only needs to know that protocols targeting the system service should be used.</span></span>

<span data-ttu-id="1d365-123">The File System provider is used instead of the Image Store Service for local one-box clusters during development to bootstrap the cluster slightly faster.</span><span class="sxs-lookup"><span data-stu-id="1d365-123">The File System provider is used instead of the Image Store Service for local one-box clusters during development to bootstrap the cluster slightly faster.</span></span> <span data-ttu-id="1d365-124">The difference is typically small, but it's a useful optimization for most folks during development.</span><span class="sxs-lookup"><span data-stu-id="1d365-124">The difference is typically small, but it's a useful optimization for most folks during development.</span></span> <span data-ttu-id="1d365-125">It's possible to deploy a local one-box cluster with the other storage provider types as well, but there's usually no reason to do so since the develop/test workflow remains the same regardless of provider.</span><span class="sxs-lookup"><span data-stu-id="1d365-125">It's possible to deploy a local one-box cluster with the other storage provider types as well, but there's usually no reason to do so since the develop/test workflow remains the same regardless of provider.</span></span> <span data-ttu-id="1d365-126">Other than this usage, the File System and Azure Storage providers only exist for legacy support.</span><span class="sxs-lookup"><span data-stu-id="1d365-126">Other than this usage, the File System and Azure Storage providers only exist for legacy support.</span></span>

<span data-ttu-id="1d365-127">So while the ImageStoreConnectionString is configurable, you generally just use the default setting.</span><span class="sxs-lookup"><span data-stu-id="1d365-127">So while the ImageStoreConnectionString is configurable, you generally just use the default setting.</span></span> <span data-ttu-id="1d365-128">When publishing to Azure through [Visual Studio][12], the parameter is automatically set for you accordingly.</span><span class="sxs-lookup"><span data-stu-id="1d365-128">When publishing to Azure through [Visual Studio][12], the parameter is automatically set for you accordingly.</span></span> <span data-ttu-id="1d365-129">For programmatic deployment to clusters hosted in Azure, the connection string is always "fabric:ImageStore".</span><span class="sxs-lookup"><span data-stu-id="1d365-129">For programmatic deployment to clusters hosted in Azure, the connection string is always "fabric:ImageStore".</span></span> <span data-ttu-id="1d365-130">Though when in doubt, its value can always be verified by retrieving the cluster manifest by [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), or [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest).</span><span class="sxs-lookup"><span data-stu-id="1d365-130">Though when in doubt, its value can always be verified by retrieving the cluster manifest by [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), or [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest).</span></span> <span data-ttu-id="1d365-131">Both on-premise test and production clusters should always be configured to use the Image Store Service provider as well.</span><span class="sxs-lookup"><span data-stu-id="1d365-131">Both on-premise test and production clusters should always be configured to use the Image Store Service provider as well.</span></span>

### <a name="next-steps"></a><span data-ttu-id="1d365-132">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d365-132">Next steps</span></span>
<span data-ttu-id="1d365-133">[Deploy and remove applications using PowerShell][10]</span><span class="sxs-lookup"><span data-stu-id="1d365-133">[Deploy and remove applications using PowerShell][10]</span></span>

<!--Image references-->
[img_is]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md


