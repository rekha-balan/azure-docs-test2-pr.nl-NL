---
title: VM preserving maintenance for Windows VMs in Azure | Microsoft Docs
description: In-place VM migration for memory preserving updates.
services: virtual-machines-windows
documentationcenter: ''
author: ''
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: ''
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ''
ms.openlocfilehash: bc903f7523295da704ea8f0128dd553e3fdd96a9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554167"
---
# <a name="vm-preserving-maintenance-with-in-place-vm-migration"></a>VM preserving maintenance with In-place VM migration

While the majority of updates have no impact to hosted VMs, there are cases where updates to components or services result in minimal interference to running VMs (without a full reboot of the virtual machine).

These updates are accomplished with technology that enables in-place live migration, also called “memory-preserving update”. When updating the host, the virtual machine is placed into a “paused” state, preserving the memory in RAM, while the hosting environment (e.g. the underlying operating system) applies the necessary updates and patches.
The virtual machine is then resumed within 30 seconds of being paused.
After resuming, the clock of the virtual machine is automatically synchronized.

Not all updates can be deployed by using this mechanism, but given the short pause period, deploying updates in this way greatly reduces impact to virtual machines.

Multi-instance updates (VMs in an availability set) are applied one update domain at a time.

Applications running in a virtual machine can learn about upcoming updates by calling the metadata service scheduled events. For more information about scheduled events, refer to [Azure Metadata Service - Scheduled Events](../virtual-machines-scheduled-events.md).