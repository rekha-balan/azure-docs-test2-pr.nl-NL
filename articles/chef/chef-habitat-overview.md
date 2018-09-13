---
title: Use Habitat to deploy your application to Azure
description: Learn how to consistently deploy your application to Azure virtual machines and containers
keywords: azure, chef, devops, virtual machines, overview, automate, habitat
ms.service: virtual-machines-linux
author: tomarcher
manager: jeconnoc
ms.author: tarcher
ms.date: 05/15/2018
ms.topic: article
ms.openlocfilehash: 73c6834eb53c0496fa673dd25ab90abc18a6a139
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869667"
---
# <a name="use-habitat-to-deploy-your-application-to-azure"></a>Use Habitat to deploy your application to Azure
[Habitat](https://www.habitat.sh/) is a first of its kind open-source project that offers an entirely new approach to application management. Habitat makes the application and its automation the unit of deployment. When applications are wrapped in a lightweight “habitat,” the runtime environment, whether it is a container, bare metal, or PaaS, is no longer the focus and does not constrain the application. 

This article describes the benefits of using Habitat.

## <a name="support-for-the-modern-application"></a>Support for the modern application
Habitat packages include everything that an application needs to run throughout its lifecycle. Habitat’s core components are:
- Packaging format - Applications in a Habitat package are atomic, immutable, and auditable.
- The Habitat supervisor runs application packages with awareness of the packages’ peer relationships, upgrade strategy, and security policies. The Habitat supervisor configures and manages the application for whatever environment is present.
- The Habitat ecosystem also provides a build service that takes a Habitat build plan, creates the Habitat package, and publishes it to a depot.

## <a name="run-any-application-anywhere"></a>Run any application anywhere
With Habitat, applications can run unmodified in any runtime environment. This includes everything from bare metal and virtual machines to containers (such as Docker), cluster-management systems (such as Mesosphere or Kubernetes), and PaaS systems (such as Pivotal Cloud Foundry).

## <a name="easily-port-legacy-applications"></a>Easily port legacy applications
When legacy applications are wrapped in a Habitat package, the applications are independent of the environment for which they were originally designed. The packages can quickly be moved to more modern environments such as the cloud or containers. Also, because Habitat packages have a standard, outward facing interface, legacy applications become much easier to manage.

## <a name="improve-the-container-experience"></a>Improve the container experience
Habitat reduces the complexity of managing containers in production environments. By automating application configuration within a container, Habitat addresses the challenges developers face when moving container-based applications from development environments into production.

## <a name="integrate-into-the-chef-devops-workflow"></a>Integrate into the Chef DevOps workflow
The Habitat project is sponsored by Chef. Habitat leverages Chef’s deep experience with infrastructure automation to bring unprecedented automation capabilities to applications. Chef will offer commercial support for Habitat and ensure seamless integration between Habitat and Chef Delivery to fully automate the application release cycle, from development to deployment.

## <a name="next-steps"></a>Next steps
* [Create a Windows virtual machine on Azure using Chef](/azure/virtual-machines/windows/chef-automation)