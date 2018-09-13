---
title: Migrate machines after assessment with Azure Migrate | Microsoft Docs
description: Describes how to get recommendations for migrating machines after you run an assessment with the Azure Migrate service.
author: rayne-wiselman
ms.service: azure-migrate
ms.topic: article
ms.date: 06/19/2018
ms.author: raynew
ms.openlocfilehash: 571bd2424d1d38e6c0048a95b263dda000477e44
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857116"
---
# <a name="migrate-machines-after-assessment"></a><span data-ttu-id="bbc77-103">Migrate machines after assessment</span><span class="sxs-lookup"><span data-stu-id="bbc77-103">Migrate machines after assessment</span></span>


<span data-ttu-id="bbc77-104">[Azure Migrate](migrate-overview.md) assesses on-premises machines to check whether they're suitable for migration to Azure, and provides sizing and cost estimations for running the machine in Azure.</span><span class="sxs-lookup"><span data-stu-id="bbc77-104">[Azure Migrate](migrate-overview.md) assesses on-premises machines to check whether they're suitable for migration to Azure, and provides sizing and cost estimations for running the machine in Azure.</span></span> <span data-ttu-id="bbc77-105">Currently, Azure Migrate only assesses machines for migration.</span><span class="sxs-lookup"><span data-stu-id="bbc77-105">Currently, Azure Migrate only assesses machines for migration.</span></span> <span data-ttu-id="bbc77-106">The migration itself is currently performed using other Azure services.</span><span class="sxs-lookup"><span data-stu-id="bbc77-106">The migration itself is currently performed using other Azure services.</span></span>

<span data-ttu-id="bbc77-107">This article describes how to get suggestions for a migration tool after you've run a migration assessment.</span><span class="sxs-lookup"><span data-stu-id="bbc77-107">This article describes how to get suggestions for a migration tool after you've run a migration assessment.</span></span>

## <a name="migration-tool-suggestion"></a><span data-ttu-id="bbc77-108">Migration tool suggestion</span><span class="sxs-lookup"><span data-stu-id="bbc77-108">Migration tool suggestion</span></span>

<span data-ttu-id="bbc77-109">To get suggestions regarding migration tools, you need to do a deep discovery of the on-premises environment.</span><span class="sxs-lookup"><span data-stu-id="bbc77-109">To get suggestions regarding migration tools, you need to do a deep discovery of the on-premises environment.</span></span> <span data-ttu-id="bbc77-110">The deep discovery is done by installing agents on the on-premises machines.</span><span class="sxs-lookup"><span data-stu-id="bbc77-110">The deep discovery is done by installing agents on the on-premises machines.</span></span>  

1. <span data-ttu-id="bbc77-111">Create an Azure Migrate project, discover on-premises machines, and create a migration assessment.</span><span class="sxs-lookup"><span data-stu-id="bbc77-111">Create an Azure Migrate project, discover on-premises machines, and create a migration assessment.</span></span> <span data-ttu-id="bbc77-112">[Learn more](tutorial-assessment-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="bbc77-112">[Learn more](tutorial-assessment-vmware.md).</span></span>
2. <span data-ttu-id="bbc77-113">Download and install the Azure Migrate agents on each on-premises machine for which you want to see a recommended migration method.</span><span class="sxs-lookup"><span data-stu-id="bbc77-113">Download and install the Azure Migrate agents on each on-premises machine for which you want to see a recommended migration method.</span></span> <span data-ttu-id="bbc77-114">[Follow this procedure](how-to-create-group-machine-dependencies.md#prepare-machines-for-dependency-mapping) to install the agents.</span><span class="sxs-lookup"><span data-stu-id="bbc77-114">[Follow this procedure](how-to-create-group-machine-dependencies.md#prepare-machines-for-dependency-mapping) to install the agents.</span></span>
2. <span data-ttu-id="bbc77-115">Identify your on-premises machines that are suitable for lift-and-shift migration.</span><span class="sxs-lookup"><span data-stu-id="bbc77-115">Identify your on-premises machines that are suitable for lift-and-shift migration.</span></span> <span data-ttu-id="bbc77-116">These are the VMs that don't require any changes to apps running on them, and can be migrated as is.</span><span class="sxs-lookup"><span data-stu-id="bbc77-116">These are the VMs that don't require any changes to apps running on them, and can be migrated as is.</span></span>
3. <span data-ttu-id="bbc77-117">For lift-and-shift migration, we suggest using Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="bbc77-117">For lift-and-shift migration, we suggest using Azure Site Recovery.</span></span> <span data-ttu-id="bbc77-118">[Learn more](../site-recovery/tutorial-migrate-on-premises-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="bbc77-118">[Learn more](../site-recovery/tutorial-migrate-on-premises-to-azure.md).</span></span> <span data-ttu-id="bbc77-119">Alternately, you can use third-party tools that support migration to Azure.</span><span class="sxs-lookup"><span data-stu-id="bbc77-119">Alternately, you can use third-party tools that support migration to Azure.</span></span>
4. <span data-ttu-id="bbc77-120">If you have on-premises machines that aren't suitable for a lift-and-shift migration, that is, if you want to migrate specific app rather than an entire VM, you can use other migration tools.</span><span class="sxs-lookup"><span data-stu-id="bbc77-120">If you have on-premises machines that aren't suitable for a lift-and-shift migration, that is, if you want to migrate specific app rather than an entire VM, you can use other migration tools.</span></span> <span data-ttu-id="bbc77-121">For example, we suggest the [Azure Database Migration service](https://azure.microsoft.com/campaigns/database-migration/) if you want to migrate on-premises databases such a SQL Server, MySQL, or Oracle to Azure.</span><span class="sxs-lookup"><span data-stu-id="bbc77-121">For example, we suggest the [Azure Database Migration service](https://azure.microsoft.com/campaigns/database-migration/) if you want to migrate on-premises databases such a SQL Server, MySQL, or Oracle to Azure.</span></span>


## <a name="review-suggested-migration-methods"></a><span data-ttu-id="bbc77-122">Review suggested migration methods</span><span class="sxs-lookup"><span data-stu-id="bbc77-122">Review suggested migration methods</span></span>

1. <span data-ttu-id="bbc77-123">Before you can get a suggested migration method, you need to create an Azure Migrate project, discover on-premises machines, and run a migration assessment.</span><span class="sxs-lookup"><span data-stu-id="bbc77-123">Before you can get a suggested migration method, you need to create an Azure Migrate project, discover on-premises machines, and run a migration assessment.</span></span> <span data-ttu-id="bbc77-124">[Learn more](tutorial-assessment-vmware.md).</span><span class="sxs-lookup"><span data-stu-id="bbc77-124">[Learn more](tutorial-assessment-vmware.md).</span></span>
2. <span data-ttu-id="bbc77-125">After the assessment is created, view it in the project > **Overview** > **Dashboard**.</span><span class="sxs-lookup"><span data-stu-id="bbc77-125">After the assessment is created, view it in the project > **Overview** > **Dashboard**.</span></span> <span data-ttu-id="bbc77-126">Click **Assessment Readiness**</span><span class="sxs-lookup"><span data-stu-id="bbc77-126">Click **Assessment Readiness**</span></span>

    ![Assessment readiness](./media/tutorial-assessment-vmware/assessment-report.png)  

3. <span data-ttu-id="bbc77-128">In **Suggested Tool**, review the suggestions for tools you can use for migration.</span><span class="sxs-lookup"><span data-stu-id="bbc77-128">In **Suggested Tool**, review the suggestions for tools you can use for migration.</span></span>

    ![Suggested tool](./media/tutorial-assessment-vmware/assessment-suitability.png) 




## <a name="next-steps"></a><span data-ttu-id="bbc77-130">Next steps</span><span class="sxs-lookup"><span data-stu-id="bbc77-130">Next steps</span></span>

<span data-ttu-id="bbc77-131">[Learn more](concepts-assessment-calculation.md) about how assessments are calculated.</span><span class="sxs-lookup"><span data-stu-id="bbc77-131">[Learn more](concepts-assessment-calculation.md) about how assessments are calculated.</span></span>
