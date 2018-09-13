---
title: Planned maintenance for Windows VMs in Azure | Microsoft Docs
description: Understand what Azure planned maintenance is and how it affects your Windows virtual machines running in Azure.
services: virtual-machines-windows
documentationcenter: ''
author: ''
manager: timlt
editor: ''
tags: azure-service-management,azure-resource-manager
ms.assetid: eb4b92d8-be0f-44f6-a6c3-f8f7efab09fe
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/27/2017
ms.author: ''
ms.openlocfilehash: ded4d2a842c404dc83783faa956a1bffbc111d38
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44553718"
---
# <a name="planned-maintenance-for-windows-virtual-machines"></a><span data-ttu-id="bfe61-103">Planned maintenance for Windows virtual machines</span><span class="sxs-lookup"><span data-stu-id="bfe61-103">Planned maintenance for Windows virtual machines</span></span> 

<span data-ttu-id="bfe61-104">Microsoft Azure periodically performs updates across the globe to improve the reliability, performance, and security of the host infrastructure that underlies virtual machines.</span><span class="sxs-lookup"><span data-stu-id="bfe61-104">Microsoft Azure periodically performs updates across the globe to improve the reliability, performance, and security of the host infrastructure that underlies virtual machines.</span></span> <span data-ttu-id="bfe61-105">Such updates range from patching software components in the hosting environment (OS, hypervisor and various agents deployed on the host), upgrading networking components, all the way to hardware decommissioning.</span><span class="sxs-lookup"><span data-stu-id="bfe61-105">Such updates range from patching software components in the hosting environment (OS, hypervisor and various agents deployed on the host), upgrading networking components, all the way to hardware decommissioning.</span></span>

<span data-ttu-id="bfe61-106">The majority of these updates are performed without any impact to hosted virtual machines or cloud services.</span><span class="sxs-lookup"><span data-stu-id="bfe61-106">The majority of these updates are performed without any impact to hosted virtual machines or cloud services.</span></span>

<span data-ttu-id="bfe61-107">However, there are cases where updates do have an impact to hosted virtual machines:</span><span class="sxs-lookup"><span data-stu-id="bfe61-107">However, there are cases where updates do have an impact to hosted virtual machines:</span></span>

-   <span data-ttu-id="bfe61-108">VM preserving maintenance using In-place VM migration describes a class of updates where virtual machines are not rebooted during the maintenance.</span><span class="sxs-lookup"><span data-stu-id="bfe61-108">VM preserving maintenance using In-place VM migration describes a class of updates where virtual machines are not rebooted during the maintenance.</span></span>

-   <span data-ttu-id="bfe61-109">VM restarting maintenance which require a reboot or redeploy to hosted virtual machines.</span><span class="sxs-lookup"><span data-stu-id="bfe61-109">VM restarting maintenance which require a reboot or redeploy to hosted virtual machines.</span></span>

<span data-ttu-id="bfe61-110">Please note that this page describes how Microsoft Azure performs planned maintenance.</span><span class="sxs-lookup"><span data-stu-id="bfe61-110">Please note that this page describes how Microsoft Azure performs planned maintenance.</span></span> <span data-ttu-id="bfe61-111">For more information about unplanned events (outages), see [Manage the availability of virtual machines](manage-availability.md).</span><span class="sxs-lookup"><span data-stu-id="bfe61-111">For more information about unplanned events (outages), see [Manage the availability of virtual machines](manage-availability.md).</span></span>