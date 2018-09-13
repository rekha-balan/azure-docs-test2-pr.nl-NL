---
title: Mount an emptyDir volume in Azure Container Instances
description: Learn how to mount an emptyDir volume to share data between the containers in a container group in Azure Container Instances
services: container-instances
author: mmacy
manager: jeconnoc
ms.service: container-instances
ms.topic: article
ms.date: 02/08/2018
ms.author: marsma
ms.openlocfilehash: 89289a7a0bb5c486c662d528c5014bdbd8eebaca
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857078"
---
# <a name="mount-an-emptydir-volume-in-azure-container-instances"></a>Mount an emptyDir volume in Azure Container Instances

Learn how to mount an *emptyDir* volume to share data between the containers in a container group in Azure Container Instances.

> [!NOTE]
> Mounting an *emptyDir* volume is currently restricted to Linux containers. While we are working to bring all features to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).

## <a name="emptydir-volume"></a>emptyDir volume

The *emptyDir* volume provides a writable directory accessible to each container in a container group. Containers in the group can read and write the same files in the volume, and it can be mounted using the same or different paths in each container.

Some example uses for an *emptyDir* volume:

* Scratch space
* Checkpointing during long-running tasks
* Store data retrieved by a sidecar container and served by an application container

Data in an *emptyDir* volume is persisted through container crashes. Containers that are restarted, however, are not guaranteed to persist the data in an *emptyDir* volume.

## <a name="mount-an-emptydir-volume"></a>Mount an emptyDir volume

To mount an emptyDir volume in a container instance, you must deploy using an [Azure Resource Manager template](/azure/templates/microsoft.containerinstance/containergroups).

First, populate the `volumes` array in the container group `properties` section of the template. Next, for each container in the container group in which you'd like to mount the *emptyDir* volume, populate the `volumeMounts` array in the `properties` section of the container definition.

For example, the following Resource Manager template creates a container group consisting of two containers, each of which mounts the *emptyDir* volume:

<!-- https://github.com/Azure/azure-docs-json-samples/blob/master/container-instances/aci-deploy-volume-emptydir.json --> [!code-json[volume-emptydir](~/azure-docs-json-samples/container-instances/aci-deploy-volume-emptydir.json)]

To see an example of container instance deployment with an Azure Resource Manager template, see [Deploy multi-container groups in Azure Container Instances](container-instances-multi-container-group.md).

## <a name="next-steps"></a>Next steps

Learn how to mount other volume types in Azure Container Instances:

* [Mount an Azure file share in Azure Container Instances](container-instances-volume-azure-files.md)
* [Mount a gitRepo volume in Azure Container Instances](container-instances-volume-gitrepo.md)
* [Mount a secret volume in Azure Container Instances](container-instances-volume-secret.md)