---
title: Avoid service interruptions with Azure Stream Analytics jobs | Microsoft Docs
description: Guidance on making your Stream Analytics jobs upgrade resilient.
services: stream-analytics
documentationCenter: ''
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8dc19e1b37082c87d2990ad910d1af786f8b9280
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44554026"
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a><span data-ttu-id="cfea3-103">Guarantee Stream Analytics job reliability during service updates</span><span class="sxs-lookup"><span data-stu-id="cfea3-103">Guarantee Stream Analytics job reliability during service updates</span></span>

<span data-ttu-id="cfea3-104">Part of being a fully managed service is the capability to introduce new service functionality and improvements at a rapid pace.</span><span class="sxs-lookup"><span data-stu-id="cfea3-104">Part of being a fully managed service is the capability to introduce new service functionality and improvements at a rapid pace.</span></span> <span data-ttu-id="cfea3-105">As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis.</span><span class="sxs-lookup"><span data-stu-id="cfea3-105">As a result, Stream Analytics can have a service update deploy on a weekly (or more frequent) basis.</span></span> <span data-ttu-id="cfea3-106">No matter how much testing is done there is still a risk that an existing, running job may break due to the introduction of a bug.</span><span class="sxs-lookup"><span data-stu-id="cfea3-106">No matter how much testing is done there is still a risk that an existing, running job may break due to the introduction of a bug.</span></span> <span data-ttu-id="cfea3-107">For customers who run critical streaming processing jobs these risks need to be avoided.</span><span class="sxs-lookup"><span data-stu-id="cfea3-107">For customers who run critical streaming processing jobs these risks need to be avoided.</span></span> <span data-ttu-id="cfea3-108">A mechanism customers can use to reduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model.</span><span class="sxs-lookup"><span data-stu-id="cfea3-108">A mechanism customers can use to reduce this risk is Azure’s **[paired region](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** model.</span></span> 

## <a name="how-do-azure-paired-regions-address-this-concern"></a><span data-ttu-id="cfea3-109">How do Azure paired regions address this concern?</span><span class="sxs-lookup"><span data-stu-id="cfea3-109">How do Azure paired regions address this concern?</span></span>

<span data-ttu-id="cfea3-110">Stream Analytics guarantees jobs in paired regions are updated in separate batches.</span><span class="sxs-lookup"><span data-stu-id="cfea3-110">Stream Analytics guarantees jobs in paired regions are updated in separate batches.</span></span> <span data-ttu-id="cfea3-111">As a result there is a sufficient time gap between the updates to identify potential breaking bugs and remediate them.</span><span class="sxs-lookup"><span data-stu-id="cfea3-111">As a result there is a sufficient time gap between the updates to identify potential breaking bugs and remediate them.</span></span>

<span data-ttu-id="cfea3-112">_With the exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), the deployment of an update to Stream Analytics would not occur at the same time in a set of paired regions.</span><span class="sxs-lookup"><span data-stu-id="cfea3-112">_With the exception of Central India_ (whose paired region, South India, does not have Stream Analytics presence), the deployment of an update to Stream Analytics would not occur at the same time in a set of paired regions.</span></span> <span data-ttu-id="cfea3-113">Deployments in multiple regions **in the same group** may occur **at the same time**.</span><span class="sxs-lookup"><span data-stu-id="cfea3-113">Deployments in multiple regions **in the same group** may occur **at the same time**.</span></span>

<span data-ttu-id="cfea3-114">The article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has the most up-to-date information on which regions are paired.</span><span class="sxs-lookup"><span data-stu-id="cfea3-114">The article on **[availability and paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)** has the most up-to-date information on which regions are paired.</span></span>

<span data-ttu-id="cfea3-115">Customers are advised to deploy identical jobs to both paired regions.</span><span class="sxs-lookup"><span data-stu-id="cfea3-115">Customers are advised to deploy identical jobs to both paired regions.</span></span> <span data-ttu-id="cfea3-116">In addition to Stream Analytics internal monitoring capabilities, customers are also advised to monitor the jobs as if **both** are production jobs.</span><span class="sxs-lookup"><span data-stu-id="cfea3-116">In addition to Stream Analytics internal monitoring capabilities, customers are also advised to monitor the jobs as if **both** are production jobs.</span></span> <span data-ttu-id="cfea3-117">If a break is identified to be a result of the Stream Analytics service update, escalate appropriately and fail over any downstream consumers to the healthy job output.</span><span class="sxs-lookup"><span data-stu-id="cfea3-117">If a break is identified to be a result of the Stream Analytics service update, escalate appropriately and fail over any downstream consumers to the healthy job output.</span></span> <span data-ttu-id="cfea3-118">Escalation to support will prevent the paired region from being affected by the new deployment and maintain the integrity of the paired jobs.</span><span class="sxs-lookup"><span data-stu-id="cfea3-118">Escalation to support will prevent the paired region from being affected by the new deployment and maintain the integrity of the paired jobs.</span></span>
