---
title: Azure Analysis Services high availability | Microsoft Docs
description: Assuring Azure Analysis Services high availability.
services: analysis-services
documentationcenter: ''
author: minewiskan
manager: erikre
editor: ''
ms.assetid: ''
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/18/2017
ms.author: owend
ms.openlocfilehash: c4eb1162edc42baafe96e6c33699805ffc121204
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44669535"
---
# <a name="analysis-services-high-availability"></a><span data-ttu-id="79cd2-103">Analysis Services high availability</span><span class="sxs-lookup"><span data-stu-id="79cd2-103">Analysis Services high availability</span></span>
<span data-ttu-id="79cd2-104">This article describes assuring high availability for Azure Analysis Services servers.</span><span class="sxs-lookup"><span data-stu-id="79cd2-104">This article describes assuring high availability for Azure Analysis Services servers.</span></span> 


## <a name="assuring-high-availability-during-a-service-disruption"></a><span data-ttu-id="79cd2-105">Assuring high availability during a service disruption</span><span class="sxs-lookup"><span data-stu-id="79cd2-105">Assuring high availability during a service disruption</span></span>
<span data-ttu-id="79cd2-106">While rare, an Azure data center can have an outage.</span><span class="sxs-lookup"><span data-stu-id="79cd2-106">While rare, an Azure data center can have an outage.</span></span> <span data-ttu-id="79cd2-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span><span class="sxs-lookup"><span data-stu-id="79cd2-107">When an outage occurs, it causes a business disruption that might last a few minutes or might last for hours.</span></span> <span data-ttu-id="79cd2-108">High availability is most often achieved with server redundancy.</span><span class="sxs-lookup"><span data-stu-id="79cd2-108">High availability is most often achieved with server redundancy.</span></span> <span data-ttu-id="79cd2-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span><span class="sxs-lookup"><span data-stu-id="79cd2-109">With Azure Analysis Services, you can achieve redundancy by creating additional, secondary servers in one or more regions.</span></span> <span data-ttu-id="79cd2-110">When creating redundant servers, to assure the data and metadata on those servers is in-sync with the server in a region that has gone offline, you can:</span><span class="sxs-lookup"><span data-stu-id="79cd2-110">When creating redundant servers, to assure the data and metadata on those servers is in-sync with the server in a region that has gone offline, you can:</span></span>

* <span data-ttu-id="79cd2-111">Deploy models to redundant servers in other regions.</span><span class="sxs-lookup"><span data-stu-id="79cd2-111">Deploy models to redundant servers in other regions.</span></span> <span data-ttu-id="79cd2-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span><span class="sxs-lookup"><span data-stu-id="79cd2-112">This method requires processing data on both your primary server and redundant servers in-parallel, assuring all servers are in-sync.</span></span>

* <span data-ttu-id="79cd2-113">Backup databases from your primary server and restore on redundant servers.</span><span class="sxs-lookup"><span data-stu-id="79cd2-113">Backup databases from your primary server and restore on redundant servers.</span></span> <span data-ttu-id="79cd2-114">For example, you can automate nightly backups to Azure storage, and restore to other redundant servers in other regions.</span><span class="sxs-lookup"><span data-stu-id="79cd2-114">For example, you can automate nightly backups to Azure storage, and restore to other redundant servers in other regions.</span></span> 

<span data-ttu-id="79cd2-115">In either case, if your primary server experiences an outage, you must change the connection strings in reporting clients to connect to the server in a different regional datacenter.</span><span class="sxs-lookup"><span data-stu-id="79cd2-115">In either case, if your primary server experiences an outage, you must change the connection strings in reporting clients to connect to the server in a different regional datacenter.</span></span> <span data-ttu-id="79cd2-116">This cahnge should be considered a last resort and only if a catastrophic regional data center outage occurs.</span><span class="sxs-lookup"><span data-stu-id="79cd2-116">This cahnge should be considered a last resort and only if a catastrophic regional data center outage occurs.</span></span> <span data-ttu-id="79cd2-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span><span class="sxs-lookup"><span data-stu-id="79cd2-117">It's more likely a data center outage hosting your primary server would come back online before you could update connections on all clients.</span></span> 

<span data-ttu-id="79cd2-118">When determining how your organization handles a service disruption, consider how you assure your data is kept both up-to-date and secure.</span><span class="sxs-lookup"><span data-stu-id="79cd2-118">When determining how your organization handles a service disruption, consider how you assure your data is kept both up-to-date and secure.</span></span> 


## <a name="related-information"></a><span data-ttu-id="79cd2-119">Related information</span><span class="sxs-lookup"><span data-stu-id="79cd2-119">Related information</span></span>
<span data-ttu-id="79cd2-120">[Backup and restore](analysis-services-backup.md) 
[Manage Azure Analysis Services](analysis-services-manage.md)</span><span class="sxs-lookup"><span data-stu-id="79cd2-120">[Backup and restore](analysis-services-backup.md) 
[Manage Azure Analysis Services](analysis-services-manage.md)</span></span> 

