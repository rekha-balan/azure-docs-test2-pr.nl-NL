---
title: Azure Stack Development Kit Architecture | Microsoft Docs
description: Describes the Azure Stack Development Kit (ASDK) architecture.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2018
ms.author: jeffgilb
ms.reviewer: misainat
ms.openlocfilehash: 68da3ac0eb135f5956dfea76e186d9c57beea79c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858048"
---
# <a name="microsoft-azure-stack-development-kit-architecture"></a>Microsoft Azure Stack Development Kit architecture
The Azure Stack Development Kit (ASDK) is a single-node deployment of Azure Stack. All the components are installed in virtual machines running on a single host machine. 

## <a name="logical-architecture-diagram"></a>Logical architecture diagram
The following diagram illustrates the logical architecture of the ASDK and its components.

![ASDK architecture](media/asdk-architecture/image1.png)

## <a name="virtual-machine-roles"></a>Virtual machine roles
The ASDK offers services using the following VMs hosted on the development kit host computer:

| Name | Description |
| ----- | ----- |
| **AzS-ACS01** | Azure Stack storage services.|
| **AzS-ADFS01** | Active Directory Federation Services (ADFS).  |
| **AzS-BGPNAT01** | Edge router and provides NAT and VPN capabilities for Azure Stack. |
| **AzS-CA01** | Certificate authority services for Azure Stack role services.|
| **AzS-DC01** | Active Directory, DNS, and DHCP services for Microsoft Azure Stack.|
| **AzS-ERCS01** | Emergency Recovery Console VM. |
| **AzS-GWY01** | Edge gateway services such as VPN site-to-site connections for tenant networks.|
| **AzS-NC01** | Network Controller, which manages Azure Stack network services.  |
| **AzS-SLB01** | Load balancing multiplexer services in Azure Stack for both tenants and Azure Stack infrastructure services.  |
| **AzS-SQL01** | Internal data store for Azure Stack infrastructure roles.  |
| **AzS-WAS01** | Azure Stack administrative portal and Azure Resource Manager services.|
| **AzS-WASP01**| Azure Stack user (tenant) portal and Azure Resource Manager services.|
| **AzS-XRP01** | Infrastructure management controller for Microsoft Azure Stack, including the Compute, Network, and Storage resource providers.|


## <a name="next-steps"></a>Next steps
[Learn about basic ASDK administration tasks](asdk-admin-basics.md)
