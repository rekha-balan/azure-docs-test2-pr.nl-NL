---
title: Planned maintenance for Liunx VMs in Azure | Microsoft Docs
description: Understand what Azure planned maintenance is and how it affects your Windows virtual machines running in Azure.
services: virtual-machines-linux
documentationcenter: ''
author: ''
manager: timlt
editor: ''
tags: azure-resource-manager,azure-service-management
ms.assetid: ''
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/27/2017
ms.author: ''
ms.openlocfilehash: 0197496087a7a49cf3cbc74be5d726030204c367
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564552"
---
# <a name="planned-maintenance-for-linux-virtual-machines"></a><span data-ttu-id="b90ba-103">Planned maintenance for Linux virtual machines</span><span class="sxs-lookup"><span data-stu-id="b90ba-103">Planned maintenance for Linux virtual machines</span></span> 

<span data-ttu-id="b90ba-104">Microsoft Azure periodically performs updates across the globe to improve the reliability, performance, and security of the host infrastructure that underlies virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b90ba-104">Microsoft Azure periodically performs updates across the globe to improve the reliability, performance, and security of the host infrastructure that underlies virtual machines.</span></span> <span data-ttu-id="b90ba-105">Such updates range from patching software components in the hosting environment (OS, hypervisor and various agents deployed on the host), upgrading networking components, all the way to hardware decommissioning.</span><span class="sxs-lookup"><span data-stu-id="b90ba-105">Such updates range from patching software components in the hosting environment (OS, hypervisor and various agents deployed on the host), upgrading networking components, all the way to hardware decommissioning.</span></span>

<span data-ttu-id="b90ba-106">The majority of these updates are performed without any impact to hosted virtual machines or cloud services.</span><span class="sxs-lookup"><span data-stu-id="b90ba-106">The majority of these updates are performed without any impact to hosted virtual machines or cloud services.</span></span>

<span data-ttu-id="b90ba-107">However, there are cases where updates do have an impact to hosted virtual machines:</span><span class="sxs-lookup"><span data-stu-id="b90ba-107">However, there are cases where updates do have an impact to hosted virtual machines:</span></span>

-   <span data-ttu-id="b90ba-108">VM preserving maintenance using In-place VM migration describes a class of updates where virtual machines are not rebooted during the maintenance.</span><span class="sxs-lookup"><span data-stu-id="b90ba-108">VM preserving maintenance using In-place VM migration describes a class of updates where virtual machines are not rebooted during the maintenance.</span></span>

-   <span data-ttu-id="b90ba-109">VM restarting maintenance which require a reboot or redeploy to hosted virtual machines.</span><span class="sxs-lookup"><span data-stu-id="b90ba-109">VM restarting maintenance which require a reboot or redeploy to hosted virtual machines.</span></span>

<span data-ttu-id="b90ba-110">Please note that this page describes how Microsoft Azure performs planned maintenance.</span><span class="sxs-lookup"><span data-stu-id="b90ba-110">Please note that this page describes how Microsoft Azure performs planned maintenance.</span></span> <span data-ttu-id="b90ba-111">For more information about unplanned events (outages), see [Manage the availability of virtual machines](../windows/manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="b90ba-111">For more information about unplanned events (outages), see [Manage the availability of virtual machines](../windows/manage-availability.md).</span></span>