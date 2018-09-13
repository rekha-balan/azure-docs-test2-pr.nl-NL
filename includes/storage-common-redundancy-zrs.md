---
title: include file
description: include file
services: storage
author: tamram
ms.service: storage
ms.topic: include
ms.date: 07/11/2018
ms.author: tamram
ms.custom: include file
ms.openlocfilehash: 4a43966180850645584043690b1be9d6ae232f6e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870271"
---
<span data-ttu-id="8ebb3-103">Zone-redundant storage (ZRS) replicates your data synchronously across three storage clusters in a single region.</span><span class="sxs-lookup"><span data-stu-id="8ebb3-103">Zone-redundant storage (ZRS) replicates your data synchronously across three storage clusters in a single region.</span></span> <span data-ttu-id="8ebb3-104">Each storage cluster is physically separated from the others and resides in its own availability zone (AZ).</span><span class="sxs-lookup"><span data-stu-id="8ebb3-104">Each storage cluster is physically separated from the others and resides in its own availability zone (AZ).</span></span> <span data-ttu-id="8ebb3-105">Each availability zone, and the ZRS cluster within it, is autonomous, with separate utilities and networking capabilities.</span><span class="sxs-lookup"><span data-stu-id="8ebb3-105">Each availability zone, and the ZRS cluster within it, is autonomous, with separate utilities and networking capabilities.</span></span>

<span data-ttu-id="8ebb3-106">Storing your data in a ZRS account ensures that you will be able access and manage your data in the event that a zone becomes unavailable.</span><span class="sxs-lookup"><span data-stu-id="8ebb3-106">Storing your data in a ZRS account ensures that you will be able access and manage your data in the event that a zone becomes unavailable.</span></span> <span data-ttu-id="8ebb3-107">ZRS provides excellent performance and low latency.</span><span class="sxs-lookup"><span data-stu-id="8ebb3-107">ZRS provides excellent performance and low latency.</span></span> <span data-ttu-id="8ebb3-108">ZRS offers the same [scalability targets](../articles/storage/common/storage-scalability-targets.md) as [locally-redundant storage (LRS)](../articles/storage/common/storage-redundancy-lrs.md).</span><span class="sxs-lookup"><span data-stu-id="8ebb3-108">ZRS offers the same [scalability targets](../articles/storage/common/storage-scalability-targets.md) as [locally-redundant storage (LRS)](../articles/storage/common/storage-redundancy-lrs.md).</span></span>

<span data-ttu-id="8ebb3-109">Consider ZRS for scenarios that require strong consistency, strong durability, and high availability even if an outage or natural disaster renders a zonal data center unavailable.</span><span class="sxs-lookup"><span data-stu-id="8ebb3-109">Consider ZRS for scenarios that require strong consistency, strong durability, and high availability even if an outage or natural disaster renders a zonal data center unavailable.</span></span> <span data-ttu-id="8ebb3-110">ZRS offers durability for storage objects of at least 99.9999999999% (12 9's) over a given year.</span><span class="sxs-lookup"><span data-stu-id="8ebb3-110">ZRS offers durability for storage objects of at least 99.9999999999% (12 9's) over a given year.</span></span>

<span data-ttu-id="8ebb3-111">For more information about availability zones, see [Availability Zones overview](https://docs.microsoft.com/azure/availability-zones/az-overview).</span><span class="sxs-lookup"><span data-stu-id="8ebb3-111">For more information about availability zones, see [Availability Zones overview](https://docs.microsoft.com/azure/availability-zones/az-overview).</span></span>