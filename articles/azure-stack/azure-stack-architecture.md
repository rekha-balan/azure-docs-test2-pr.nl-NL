---
title: Microsoft Azure Stack Proof Of Concept (POC) architecture | Microsoft Docs
description: View the Microsoft Azure Stack POC architecture.
services: azure-stack
documentationcenter: ''
author: heathl17
manager: byronr
editor: ''
ms.assetid: a7e61ea4-be2f-4e55-9beb-7a079f348e05
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/30/2017
ms.author: helaw
ms.openlocfilehash: 674fbea928b95c995e8896ecdd35cb9adbb1856d
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556355"
---
# <a name="microsoft-azure-stack-poc-architecture"></a>Microsoft Azure Stack POC architecture
The Azure Stack POC is a one-node deployment of Azure Stack Technical Preview 3. All the components are installed in virtual machines running on a single host machine. 

## <a name="logical-architecture-diagram"></a>Logical architecture diagram
The following diagram illustrates the logical architecture of the Azure Stack POC and its components.

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-architecture/image1.png)

## <a name="virtual-machine-roles"></a>Virtual machine roles
The Azure Stack POC offers services using the following VMs on the POC host:

| Name | Description |
| ----- | ----- |
| **MAS-ACS01** | Azure Stack storage services.|
| **MAS-ADFS01** | Active Directory Federation Services (ADFS).  |
| **MAS-BGPNAT01** | Edge router and provides NAT and VPN capabilities for Azure Stack. |
| **MAS-CA01** | Certificate authority services for Azure Stack role services.|
| **MAS-CON01** | Console machine available for installing PowerShell, Visual Studio, and other tools.|
| **MAS-DC01** | Active Directory, DNS, and DHCP services for Microsoft Azure Stack.|
| **MAS-ERCS01** | Emergency Recovery Console VM. |
| **MAS-GWY01** | Edge gateway services such as VPN site-to-site connections for tenant networks.|
| **MAS-NC01** | Network Controller, which manages Azure Stack network services.  |
| **MAS-SLB01** | Load balancing multiplexer services in Azure Stack for both tenants and Azure Stack infrastructure services.  |
| **MAS-SUS01** | Windows Server Update Services, and responsible for providing updates to other Azure Stack virtual machines.|
| **MAS-SQL01** | Internal data store for Azure Stack infrastructure roles.  |
| **MAS-WAS01** | Azure Stack administrative portal and Azure Resource Manager services.|
| **MAS-WASP01**| Azure Stack user (tenant) portal and Azure Resource Manager services.|
| **MAS-XRP01** | Infrastructure management controller for Microsoft Azure Stack, including the Compute, Network, and Storage resource providers.|

## <a name="storage-services"></a>Storage services
**Virtual Disk**, **Storage Space**, and **Storage Spaces Direct** are the respective underlying storage technology in Windows Server that enable the Microsoft Azure Stack storage resource provider.  Additional storage services installed in the operating system on the physical host include:

| Name | Description |
| ----- | ----- |
| **ACS Blob Service** | Azure Consistent Storage Blob service, which provides blob and table storage services. |
| **SoFS** | Scale-out File Server.|
| **ReFS CSV** |Resilient File System Cluster Shared Volume.|


## <a name="next-steps"></a>Next steps
[Deploy Azure Stack](azure-stack-deploy.md)

[First scenarios to try](azure-stack-first-scenarios.md)


