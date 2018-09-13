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
# <a name="understand-the-imagestoreconnectionstring-setting"></a>Understand the ImageStoreConnectionString setting

In some of our documentation, we briefly mention the existence of an "ImageStoreConnectionString" parameter without describing what it really means. And after going through an article like [Deploy and remove applications using PowerShell][10], it looks like all you do is copy/paste the value as it appears in the cluster manifest of the target cluster. So the setting must be configurable per cluster, but when you create a cluster through the [Azure portal][11], there's no option to configure this setting and it's always "fabric:ImageStore". What's the purpose of this setting then?

![Cluster Manifest][img_cm]

Service Fabric started off as a platform for internal Microsoft consumption by many diverse teams, so some aspects of it are highly customizable - the "Image Store" is one such aspect. Essentially, the Image Store is a pluggable repository for storing application packages. When your application is deployed to a node in the cluster, that node downloads the contents of your application package from the Image Store. The ImageStoreConnectionString is a setting that includes all the necessary information for both clients and nodes to find the correct Image Store for a given cluster.

There are currently three possible kinds of Image Store providers and their corresponding connection strings are as follows:

1. Image Store Service: "fabric:ImageStore"

2. File System: "file:[file system path]"

3. Azure Storage: "xstore:DefaultEndpointsProtocol=https;AccountName=[...];AccountKey=[...];Container=[...]"

The provider type used in production is the Image Store Service, which is a stateful persisted system service that you can see from Service Fabric Explorer. 

![Image Store Service][img_is]

Hosting the Image Store in a system service within the cluster itself eliminates external dependencies for the package repository and gives us more control over the locality of storage. Future improvements around the Image Store are likely to target the Image Store provider first, if not exclusively. The connection string for the Image Store Service provider doesn't have any unique information since the client is already connected to the target cluster. The client only needs to know that protocols targeting the system service should be used.

The File System provider is used instead of the Image Store Service for local one-box clusters during development to bootstrap the cluster slightly faster. The difference is typically small, but it's a useful optimization for most folks during development. It's possible to deploy a local one-box cluster with the other storage provider types as well, but there's usually no reason to do so since the develop/test workflow remains the same regardless of provider. Other than this usage, the File System and Azure Storage providers only exist for legacy support.

So while the ImageStoreConnectionString is configurable, you generally just use the default setting. When publishing to Azure through [Visual Studio][12], the parameter is automatically set for you accordingly. For programmatic deployment to clusters hosted in Azure, the connection string is always "fabric:ImageStore". Though when in doubt, its value can always be verified by retrieving the cluster manifest by [PowerShell](https://docs.microsoft.com/powershell/servicefabric/vlatest/get-servicefabricclustermanifest), [.NET](https://msdn.microsoft.com/library/azure/mt161375.aspx), or [REST](https://docs.microsoft.com/rest/api/servicefabric/get-a-cluster-manifest). Both on-premise test and production clusters should always be configured to use the Image Store Service provider as well.

### <a name="next-steps"></a>Next steps
[Deploy and remove applications using PowerShell][10]

<!--Image references-->
[img_is]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-image-store-connection-string/image_store_service.png
[img_cm]: https://docstestmedia1.blob.core.windows.net/azure-media/articles/service-fabric/media/service-fabric-image-store-connection-string/cluster_manifest.png

[10]: service-fabric-deploy-remove-applications.md
[11]: service-fabric-cluster-creation-via-portal.md
[12]: service-fabric-publish-app-remote-cluster.md


