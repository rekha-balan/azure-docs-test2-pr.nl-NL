---
title: Azure Container Instances overview
description: Understand Azure Container Instances
services: container-instances
author: seanmck
manager: jeconnoc
ms.service: container-instances
ms.topic: overview
ms.date: 07/19/2018
ms.author: seanmck
ms.custom: mvc
ms.openlocfilehash: 953d1dfd633f2fee52a2e6d197c6f32e7ab053f7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866483"
---
# <a name="azure-container-instances"></a>Azure Container Instances

Containers are becoming the preferred way to package, deploy, and manage cloud applications. Azure Container Instances offers the fastest and simplest way to run a container in Azure, without having to manage any virtual machines and without having to adopt a higher-level service.

Azure Container Instances is a great solution for any scenario that can operate in isolated containers, including simple applications, task automation, and build jobs. For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend [Azure Kubernetes Service (AKS)](../aks/index.yml).

## <a name="fast-startup-times"></a>Fast startup times

Containers offer significant startup benefits over virtual machines. Azure Container Instances can start containers in Azure in seconds, without the need to provision and manage VMs.

## <a name="public-ip-connectivity-and-dns-name"></a>Public IP connectivity and DNS name

Azure Container Instances enables exposing your containers directly to the internet with an IP address and a fully qualified domain name (FQDN). When you create a container instance, you can specify a custom DNS name label so your application is reachable at *customlabel*.*azureregion*.azurecontainer.io.

## <a name="hypervisor-level-security"></a>Hypervisor-level security

Historically, containers have offered application dependency isolation and resource governance but have not been considered sufficiently hardened for hostile multi-tenant usage. Azure Container Instances guarantees your application is as isolated in a container as it would be in a VM.

## <a name="custom-sizes"></a>Custom sizes

Containers are typically optimized to run just a single application, but the exact needs of those applications can differ greatly. Azure Container Instances provides optimum utilization by allowing exact specifications of CPU cores and memory. You pay based on what you need and get billed by the second, so you can fine-tune your spending based on actual need.

## <a name="persistent-storage"></a>Persistent storage

To retrieve and persist state with Azure Container Instances, we offer direct [mounting of Azure Files shares](container-instances-mounting-azure-files-volume.md).

## <a name="linux-and-windows-containers"></a>Linux and Windows containers

Azure Container Instances can schedule both Windows and Linux containers with the same API. Simply specify the OS type when you create your [container groups](container-instances-container-groups.md).

Some features are currently restricted to Linux containers. While we work to bring feature parity to Windows containers, you can find current platform differences in [Quotas and region availability for Azure Container Instances](container-instances-quotas.md).

Azure Container Instances supports Windows images based on Long-Term Servicing Channel (LTSC) versions. Windows Semi-Annual Channel (SAC) releases like 1709 and 1803 are unsupported.

## <a name="co-scheduled-groups"></a>Co-scheduled groups

Azure Container Instances supports scheduling of [multi-container groups](container-instances-container-groups.md) that share a host machine, local network, storage, and lifecycle. This enables you to combine your main application container with other supporting role containers, such as logging sidecars.

## <a name="next-steps"></a>Next steps

Try deploying a container to Azure with a single command using our quickstart guide:

> [!div class="nextstepaction"]
> [Azure Container Instances Quickstart](container-instances-quickstart.md)
