---
title: Rebuild a Contoso on-premises app to Azure | Microsoft Docs
description: Learn how Contoso rebuilds an app to Azure using Azure App Services, the Kubernetes service, CosmosDB, Azure Functions, and Cognitive services.
services: site-recovery
author: rayne-wiselman
ms.service: site-recovery
ms.topic: conceptual
ms.date: 09/06/2018
ms.author: raynew
ms.openlocfilehash: 58ea0859af42f7614e69d1693bbd9f8e3a17ccb8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871272"
---
# <a name="contoso-migration-rebuild-an-on-premises-app-to-azure"></a><span data-ttu-id="e4009-103">Contoso migration: Rebuild an on-premises app to Azure</span><span class="sxs-lookup"><span data-stu-id="e4009-103">Contoso migration: Rebuild an on-premises app to Azure</span></span>

<span data-ttu-id="e4009-104">This article demonstrates how Contoso migrates and rebuilds the SmartHotel360 app in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4009-104">This article demonstrates how Contoso migrates and rebuilds the SmartHotel360 app in Azure.</span></span> <span data-ttu-id="e4009-105">Contoso migrates the app's front end VM to Azure App Services Web apps.</span><span class="sxs-lookup"><span data-stu-id="e4009-105">Contoso migrates the app's front end VM to Azure App Services Web apps.</span></span> <span data-ttu-id="e4009-106">The app back end is built using microservices deployed to containers managed by Azure Kubernetes Service (AKS).</span><span class="sxs-lookup"><span data-stu-id="e4009-106">The app back end is built using microservices deployed to containers managed by Azure Kubernetes Service (AKS).</span></span> <span data-ttu-id="e4009-107">The site interacts with Azure Functions to provide pet photo functionality.</span><span class="sxs-lookup"><span data-stu-id="e4009-107">The site interacts with Azure Functions to provide pet photo functionality.</span></span> 

<span data-ttu-id="e4009-108">This document is one in a series of articles that show how the fictitious company Contoso migrates on-premises resources to the Microsoft Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="e4009-108">This document is one in a series of articles that show how the fictitious company Contoso migrates on-premises resources to the Microsoft Azure cloud.</span></span> <span data-ttu-id="e4009-109">The series includes background information, and scenarios that illustrate setting up a migration infrastructure, assessing on-premises resources for migration, and running different types of migrations.</span><span class="sxs-lookup"><span data-stu-id="e4009-109">The series includes background information, and scenarios that illustrate setting up a migration infrastructure, assessing on-premises resources for migration, and running different types of migrations.</span></span> <span data-ttu-id="e4009-110">Scenarios grow in complexity.</span><span class="sxs-lookup"><span data-stu-id="e4009-110">Scenarios grow in complexity.</span></span> <span data-ttu-id="e4009-111">We'll add additional articles over time.</span><span class="sxs-lookup"><span data-stu-id="e4009-111">We'll add additional articles over time.</span></span>


<span data-ttu-id="e4009-112">**Article**</span><span class="sxs-lookup"><span data-stu-id="e4009-112">**Article**</span></span> | <span data-ttu-id="e4009-113">**Details**</span><span class="sxs-lookup"><span data-stu-id="e4009-113">**Details**</span></span> | <span data-ttu-id="e4009-114">**Status**</span><span class="sxs-lookup"><span data-stu-id="e4009-114">**Status**</span></span>
--- | --- | ---
[<span data-ttu-id="e4009-115">Article 1: Overview</span><span class="sxs-lookup"><span data-stu-id="e4009-115">Article 1: Overview</span></span>](contoso-migration-overview.md) | <span data-ttu-id="e4009-116">Provides an overview of Contoso's migration strategy, the article series, and the sample apps we use.</span><span class="sxs-lookup"><span data-stu-id="e4009-116">Provides an overview of Contoso's migration strategy, the article series, and the sample apps we use.</span></span> | <span data-ttu-id="e4009-117">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-117">Available</span></span>
[<span data-ttu-id="e4009-118">Article 2: Deploy an Azure infrastructure</span><span class="sxs-lookup"><span data-stu-id="e4009-118">Article 2: Deploy an Azure infrastructure</span></span>](contoso-migration-infrastructure.md) | <span data-ttu-id="e4009-119">Describes how Contoso prepares its on-premises and Azure infrastructure for migration.</span><span class="sxs-lookup"><span data-stu-id="e4009-119">Describes how Contoso prepares its on-premises and Azure infrastructure for migration.</span></span> <span data-ttu-id="e4009-120">The same infrastructure is used for all migration articles.</span><span class="sxs-lookup"><span data-stu-id="e4009-120">The same infrastructure is used for all migration articles.</span></span> | <span data-ttu-id="e4009-121">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-121">Available</span></span>
[<span data-ttu-id="e4009-122">Article 3: Assess on-premises resources</span><span class="sxs-lookup"><span data-stu-id="e4009-122">Article 3: Assess on-premises resources</span></span>](contoso-migration-assessment.md)  | <span data-ttu-id="e4009-123">Shows how Contoso runs an assessment of an on-premises two-tier SmartHotel360 app running on VMware.</span><span class="sxs-lookup"><span data-stu-id="e4009-123">Shows how Contoso runs an assessment of an on-premises two-tier SmartHotel360 app running on VMware.</span></span> <span data-ttu-id="e4009-124">Contoso assesses app VMs with the [Azure Migrate](migrate-overview.md) service, and the app SQL Server database with the [Database Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="e4009-124">Contoso assesses app VMs with the [Azure Migrate](migrate-overview.md) service, and the app SQL Server database with the [Database Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017).</span></span> | <span data-ttu-id="e4009-125">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-125">Available</span></span>
[<span data-ttu-id="e4009-126">Article 4: Rehost an app on Azure VMs and a SQL Managed Instance</span><span class="sxs-lookup"><span data-stu-id="e4009-126">Article 4: Rehost an app on Azure VMs and a SQL Managed Instance</span></span>](contoso-migration-rehost-vm-sql-managed-instance.md) | <span data-ttu-id="e4009-127">Demonstrates how Contoso runs a lift-and-shift migration to Azure for the SmartHotel360 app.</span><span class="sxs-lookup"><span data-stu-id="e4009-127">Demonstrates how Contoso runs a lift-and-shift migration to Azure for the SmartHotel360 app.</span></span> <span data-ttu-id="e4009-128">Contoso migrates the app frontend VM using [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview), and the app database to a SQL Managed Instance, using the [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).</span><span class="sxs-lookup"><span data-stu-id="e4009-128">Contoso migrates the app frontend VM using [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview), and the app database to a SQL Managed Instance, using the [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).</span></span> | <span data-ttu-id="e4009-129">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-129">Available</span></span>
[<span data-ttu-id="e4009-130">Article 5: Rehost an app on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="e4009-130">Article 5: Rehost an app on Azure VMs</span></span>](contoso-migration-rehost-vm.md) | <span data-ttu-id="e4009-131">Shows how Contoso migrate the SmartHotel360 app VMs using Site Recovery only.</span><span class="sxs-lookup"><span data-stu-id="e4009-131">Shows how Contoso migrate the SmartHotel360 app VMs using Site Recovery only.</span></span> | <span data-ttu-id="e4009-132">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-132">Available</span></span>
[<span data-ttu-id="e4009-133">Article 6: Rehost an app to Azure VMs and SQL Server Always On Availability Group</span><span class="sxs-lookup"><span data-stu-id="e4009-133">Article 6: Rehost an app to Azure VMs and SQL Server Always On Availability Group</span></span>](contoso-migration-rehost-vm-sql-ag.md) | <span data-ttu-id="e4009-134">Shows how Contoso migrates the SmartHotel360 app.</span><span class="sxs-lookup"><span data-stu-id="e4009-134">Shows how Contoso migrates the SmartHotel360 app.</span></span> <span data-ttu-id="e4009-135">Contoso uses Site Recovery to migrate the app VMs, and the Database Migration service to migrate the app database to a SQL Server cluster protected by an AlwaysOn availability group.</span><span class="sxs-lookup"><span data-stu-id="e4009-135">Contoso uses Site Recovery to migrate the app VMs, and the Database Migration service to migrate the app database to a SQL Server cluster protected by an AlwaysOn availability group.</span></span> | <span data-ttu-id="e4009-136">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-136">Available</span></span>
[<span data-ttu-id="e4009-137">Article 7: Rehost a Linux app on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="e4009-137">Article 7: Rehost a Linux app on Azure VMs</span></span>](contoso-migration-rehost-linux-vm.md) | <span data-ttu-id="e4009-138">Shows how Contoso does a lift-and-shift migration of the Linux osTicket app to Azure VMs, using Site Recovery</span><span class="sxs-lookup"><span data-stu-id="e4009-138">Shows how Contoso does a lift-and-shift migration of the Linux osTicket app to Azure VMs, using Site Recovery</span></span> | <span data-ttu-id="e4009-139">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-139">Available</span></span>
[<span data-ttu-id="e4009-140">Article 8: Rehost a Linux app on Azure VMs and Azure MySQL Server</span><span class="sxs-lookup"><span data-stu-id="e4009-140">Article 8: Rehost a Linux app on Azure VMs and Azure MySQL Server</span></span>](contoso-migration-rehost-linux-vm-mysql.md) | <span data-ttu-id="e4009-141">Demonstrates how Contoso migrates the Linux osTicket app to Azure VMs using Site Recovery, and migrates the app database to an Azure MySQL Server instance using MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="e4009-141">Demonstrates how Contoso migrates the Linux osTicket app to Azure VMs using Site Recovery, and migrates the app database to an Azure MySQL Server instance using MySQL Workbench.</span></span> | <span data-ttu-id="e4009-142">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-142">Available</span></span>
[<span data-ttu-id="e4009-143">Article 9: Refactor an app on Azure Web Apps and Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="e4009-143">Article 9: Refactor an app on Azure Web Apps and Azure SQL database</span></span>](contoso-migration-refactor-web-app-sql.md) | <span data-ttu-id="e4009-144">Demonstrates how Contoso migrates the SmartHotel360 app to an Azure Web App, and migrates the app database to Azure SQL Server instance</span><span class="sxs-lookup"><span data-stu-id="e4009-144">Demonstrates how Contoso migrates the SmartHotel360 app to an Azure Web App, and migrates the app database to Azure SQL Server instance</span></span> | <span data-ttu-id="e4009-145">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-145">Available</span></span>
[<span data-ttu-id="e4009-146">Article 10: Refactor a Linux app to Azure Web Apps and Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="e4009-146">Article 10: Refactor a Linux app to Azure Web Apps and Azure MySQL</span></span>](contoso-migration-refactor-linux-app-service-mysql.md) | <span data-ttu-id="e4009-147">Shows how Contoso migrates the Linux osTicket app to Azure Web Apps in multiple sites, integrated with GitHub for continuous delivery.</span><span class="sxs-lookup"><span data-stu-id="e4009-147">Shows how Contoso migrates the Linux osTicket app to Azure Web Apps in multiple sites, integrated with GitHub for continuous delivery.</span></span> <span data-ttu-id="e4009-148">They migrate the app database to an Azure MySQL instance.</span><span class="sxs-lookup"><span data-stu-id="e4009-148">They migrate the app database to an Azure MySQL instance.</span></span> | <span data-ttu-id="e4009-149">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-149">Available</span></span>
[<span data-ttu-id="e4009-150">Article 11: Refactor TFS on Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="e4009-150">Article 11: Refactor TFS on Azure DevOps Services</span></span>](contoso-migration-tfs-vsts.md) | <span data-ttu-id="e4009-151">Shows how Contoso migrates the on-premises Team Foundation Server (TFS) deployment by migrating it to Azure DevOps Services in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4009-151">Shows how Contoso migrates the on-premises Team Foundation Server (TFS) deployment by migrating it to Azure DevOps Services in Azure.</span></span> | <span data-ttu-id="e4009-152">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-152">Available</span></span>
[<span data-ttu-id="e4009-153">Article 12: Rearchitect an app to Azure containers and SQL Database</span><span class="sxs-lookup"><span data-stu-id="e4009-153">Article 12: Rearchitect an app to Azure containers and SQL Database</span></span>](contoso-migration-rearchitect-container-sql.md) | <span data-ttu-id="e4009-154">Shows how Contoso migrates and rearchitects their SmartHotel app to Azure.</span><span class="sxs-lookup"><span data-stu-id="e4009-154">Shows how Contoso migrates and rearchitects their SmartHotel app to Azure.</span></span> <span data-ttu-id="e4009-155">They rearchitect the app web tier as a Windows container, and the app database in an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e4009-155">They rearchitect the app web tier as a Windows container, and the app database in an Azure SQL Database.</span></span> | <span data-ttu-id="e4009-156">Available</span><span class="sxs-lookup"><span data-stu-id="e4009-156">Available</span></span>
<span data-ttu-id="e4009-157">Article 13: Rebuild an app to Azure</span><span class="sxs-lookup"><span data-stu-id="e4009-157">Article 13: Rebuild an app to Azure</span></span> | <span data-ttu-id="e4009-158">Shows how Contoso rebuild their SmartHotel app using a range of Azure capabilities and services, including App Services, Azure Kubernetes, Azure Functions, Cognitive services, and Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4009-158">Shows how Contoso rebuild their SmartHotel app using a range of Azure capabilities and services, including App Services, Azure Kubernetes, Azure Functions, Cognitive services, and Cosmos DB.</span></span> | <span data-ttu-id="e4009-159">This article.</span><span class="sxs-lookup"><span data-stu-id="e4009-159">This article.</span></span>

<span data-ttu-id="e4009-160">In this article, Contoso migrates the two-tier Windows.</span><span class="sxs-lookup"><span data-stu-id="e4009-160">In this article, Contoso migrates the two-tier Windows.</span></span> <span data-ttu-id="e4009-161">NET SmartHotel360 app running on VMware VMs to Azure.</span><span class="sxs-lookup"><span data-stu-id="e4009-161">NET SmartHotel360 app running on VMware VMs to Azure.</span></span> <span data-ttu-id="e4009-162">If you'd like to use this app, it's provided as open source and you can download it from [GitHub](https://github.com/Microsoft/SmartHotel360).</span><span class="sxs-lookup"><span data-stu-id="e4009-162">If you'd like to use this app, it's provided as open source and you can download it from [GitHub](https://github.com/Microsoft/SmartHotel360).</span></span>

## <a name="business-drivers"></a><span data-ttu-id="e4009-163">Business drivers</span><span class="sxs-lookup"><span data-stu-id="e4009-163">Business drivers</span></span>

<span data-ttu-id="e4009-164">The IT leadership team has worked closely with business partners to understand what they want to achieve with this migration:</span><span class="sxs-lookup"><span data-stu-id="e4009-164">The IT leadership team has worked closely with business partners to understand what they want to achieve with this migration:</span></span>

- <span data-ttu-id="e4009-165">**Address business growth**: Contoso is growing, and wants to provide differentiated experiences for customers on Contoso websites.</span><span class="sxs-lookup"><span data-stu-id="e4009-165">**Address business growth**: Contoso is growing, and wants to provide differentiated experiences for customers on Contoso websites.</span></span>
- <span data-ttu-id="e4009-166">**Agility**: Contoso must be able to react faster than the changes in the marketplace, to enable the success in a global economy.</span><span class="sxs-lookup"><span data-stu-id="e4009-166">**Agility**: Contoso must be able to react faster than the changes in the marketplace, to enable the success in a global economy.</span></span> 
- <span data-ttu-id="e4009-167">**Scale**: As the business grows successfully, the Contoso IT team must provide systems that are able to grow at the same pace.</span><span class="sxs-lookup"><span data-stu-id="e4009-167">**Scale**: As the business grows successfully, the Contoso IT team must provide systems that are able to grow at the same pace.</span></span>
- <span data-ttu-id="e4009-168">**Costs**: Contoso wants to minimize licensing costs.</span><span class="sxs-lookup"><span data-stu-id="e4009-168">**Costs**: Contoso wants to minimize licensing costs.</span></span>

## <a name="migration-goals"></a><span data-ttu-id="e4009-169">Migration goals</span><span class="sxs-lookup"><span data-stu-id="e4009-169">Migration goals</span></span>

<span data-ttu-id="e4009-170">The Contoso cloud team has pinned down app requirements for this migration.</span><span class="sxs-lookup"><span data-stu-id="e4009-170">The Contoso cloud team has pinned down app requirements for this migration.</span></span> <span data-ttu-id="e4009-171">These requirements were used to determine the best migration method:</span><span class="sxs-lookup"><span data-stu-id="e4009-171">These requirements were used to determine the best migration method:</span></span>
 - <span data-ttu-id="e4009-172">The app in Azure will remain as critical as it is today.</span><span class="sxs-lookup"><span data-stu-id="e4009-172">The app in Azure will remain as critical as it is today.</span></span> <span data-ttu-id="e4009-173">It should perform well and scale easily.</span><span class="sxs-lookup"><span data-stu-id="e4009-173">It should perform well and scale easily.</span></span>
 - <span data-ttu-id="e4009-174">The app shouldn't use IaaS components.</span><span class="sxs-lookup"><span data-stu-id="e4009-174">The app shouldn't use IaaS components.</span></span> <span data-ttu-id="e4009-175">Everything should be built to use PaaS or serverless services.</span><span class="sxs-lookup"><span data-stu-id="e4009-175">Everything should be built to use PaaS or serverless services.</span></span>
 - <span data-ttu-id="e4009-176">The app builds should run in cloud services, and containers should reside in a private Enterprise-wide container registry in the cloud.</span><span class="sxs-lookup"><span data-stu-id="e4009-176">The app builds should run in cloud services, and containers should reside in a private Enterprise-wide container registry in the cloud.</span></span>
 - <span data-ttu-id="e4009-177">The API service used for pet photos should be accurate and reliable in the real world, since decisions made by the app must be honored in their hotels.</span><span class="sxs-lookup"><span data-stu-id="e4009-177">The API service used for pet photos should be accurate and reliable in the real world, since decisions made by the app must be honored in their hotels.</span></span> <span data-ttu-id="e4009-178">Any pet granted access is allowed to stay at the hotels.</span><span class="sxs-lookup"><span data-stu-id="e4009-178">Any pet granted access is allowed to stay at the hotels.</span></span>
 - <span data-ttu-id="e4009-179">To meet requirements for a DevOps pipeline, Contoso will use Visual Studio Team Services (VSTS) for Source Code Management (SCM), with Git Repos.</span><span class="sxs-lookup"><span data-stu-id="e4009-179">To meet requirements for a DevOps pipeline, Contoso will use Visual Studio Team Services (VSTS) for Source Code Management (SCM), with Git Repos.</span></span>  <span data-ttu-id="e4009-180">Automated builds and releases will be used to build code, and deploy it to the Azure Web Apps, Azure Functions and AKS.</span><span class="sxs-lookup"><span data-stu-id="e4009-180">Automated builds and releases will be used to build code, and deploy it to the Azure Web Apps, Azure Functions and AKS.</span></span>
 - <span data-ttu-id="e4009-181">Different CI/CD pipelines are needed for microservices on the backend, and for the web site on the frontend.</span><span class="sxs-lookup"><span data-stu-id="e4009-181">Different CI/CD pipelines are needed for microservices on the backend, and for the web site on the frontend.</span></span>
 - <span data-ttu-id="e4009-182">The backend services have a different release cycle from the frontend web app.</span><span class="sxs-lookup"><span data-stu-id="e4009-182">The backend services have a different release cycle from the frontend web app.</span></span>  <span data-ttu-id="e4009-183">To meet this requirement, they will deploy two different DevOps pipelines.</span><span class="sxs-lookup"><span data-stu-id="e4009-183">To meet this requirement, they will deploy two different DevOps pipelines.</span></span>
 - <span data-ttu-id="e4009-184">Contoso needs management approval for all front end website deployment, and the CI/CD pipeline must provide this.</span><span class="sxs-lookup"><span data-stu-id="e4009-184">Contoso needs management approval for all front end website deployment, and the CI/CD pipeline must provide this.</span></span>


## <a name="solution-design"></a><span data-ttu-id="e4009-185">Solution design</span><span class="sxs-lookup"><span data-stu-id="e4009-185">Solution design</span></span>

<span data-ttu-id="e4009-186">After pinning down goals and requirements, Contoso designs and review a deployment solution, and identifies the migration process, including the Azure services that will be used for the migration.</span><span class="sxs-lookup"><span data-stu-id="e4009-186">After pinning down goals and requirements, Contoso designs and review a deployment solution, and identifies the migration process, including the Azure services that will be used for the migration.</span></span>

### <a name="current-app"></a><span data-ttu-id="e4009-187">Current app</span><span class="sxs-lookup"><span data-stu-id="e4009-187">Current app</span></span>

- <span data-ttu-id="e4009-188">The SmartHotel360 on-premises app is tiered across two VMs (WEBVM and SQLVM).</span><span class="sxs-lookup"><span data-stu-id="e4009-188">The SmartHotel360 on-premises app is tiered across two VMs (WEBVM and SQLVM).</span></span>
- <span data-ttu-id="e4009-189">The VMs are located on VMware ESXi host **contosohost1.contoso.com** (version 6.5)</span><span class="sxs-lookup"><span data-stu-id="e4009-189">The VMs are located on VMware ESXi host **contosohost1.contoso.com** (version 6.5)</span></span>
- <span data-ttu-id="e4009-190">The VMware environment is managed by vCenter Server 6.5 (**vcenter.contoso.com**), running on a VM.</span><span class="sxs-lookup"><span data-stu-id="e4009-190">The VMware environment is managed by vCenter Server 6.5 (**vcenter.contoso.com**), running on a VM.</span></span>
- <span data-ttu-id="e4009-191">Contoso has an on-premises datacenter (contoso-datacenter), with an on-premises domain controller (**contosodc1**).</span><span class="sxs-lookup"><span data-stu-id="e4009-191">Contoso has an on-premises datacenter (contoso-datacenter), with an on-premises domain controller (**contosodc1**).</span></span>
- <span data-ttu-id="e4009-192">The on-premises VMs in the Contoso datacenter will be decommissioned after the migration is done.</span><span class="sxs-lookup"><span data-stu-id="e4009-192">The on-premises VMs in the Contoso datacenter will be decommissioned after the migration is done.</span></span>


### <a name="proposed-architecture"></a><span data-ttu-id="e4009-193">Proposed architecture</span><span class="sxs-lookup"><span data-stu-id="e4009-193">Proposed architecture</span></span>

- <span data-ttu-id="e4009-194">The frontend of the app is deployed as an Azure App Services Web app, in the primary Azure region.</span><span class="sxs-lookup"><span data-stu-id="e4009-194">The frontend of the app is deployed as an Azure App Services Web app, in the primary Azure region.</span></span>
- <span data-ttu-id="e4009-195">An Azure function provides uploads of pet photos, and the site interacts with this functionality.</span><span class="sxs-lookup"><span data-stu-id="e4009-195">An Azure function provides uploads of pet photos, and the site interacts with this functionality.</span></span>
- <span data-ttu-id="e4009-196">The pet photo function leverages Cognitive Services Vision API, and CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="e4009-196">The pet photo function leverages Cognitive Services Vision API, and CosmosDB.</span></span>
- <span data-ttu-id="e4009-197">The back end of the site is built using microservices.</span><span class="sxs-lookup"><span data-stu-id="e4009-197">The back end of the site is built using microservices.</span></span> <span data-ttu-id="e4009-198">These will be deployed to containers managed on the Azure Kubernetes service (AKS).</span><span class="sxs-lookup"><span data-stu-id="e4009-198">These will be deployed to containers managed on the Azure Kubernetes service (AKS).</span></span>
- <span data-ttu-id="e4009-199">Containers will be built using Azure DevOps, and pushed to the Azure Container Registry (ACR).</span><span class="sxs-lookup"><span data-stu-id="e4009-199">Containers will be built using Azure DevOps, and pushed to the Azure Container Registry (ACR).</span></span>
- <span data-ttu-id="e4009-200">For now, Contoso will manually deploy the Web app and function code using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4009-200">For now, Contoso will manually deploy the Web app and function code using Visual Studio.</span></span>
- <span data-ttu-id="e4009-201">Microservices will be deployed using a PowerShell script that calls Kubernetes command-line tools.</span><span class="sxs-lookup"><span data-stu-id="e4009-201">Microservices will be deployed using a PowerShell script that calls Kubernetes command-line tools.</span></span>

    ![Scenario architecture](./media/contoso-migration-rebuild/architecture.png) 

  
### <a name="solution-review"></a><span data-ttu-id="e4009-203">Solution review</span><span class="sxs-lookup"><span data-stu-id="e4009-203">Solution review</span></span>

<span data-ttu-id="e4009-204">Contoso evaluates the proposed design by putting together a pros and cons list.</span><span class="sxs-lookup"><span data-stu-id="e4009-204">Contoso evaluates the proposed design by putting together a pros and cons list.</span></span>

<span data-ttu-id="e4009-205">**Consideration**</span><span class="sxs-lookup"><span data-stu-id="e4009-205">**Consideration**</span></span> | <span data-ttu-id="e4009-206">**Details**</span><span class="sxs-lookup"><span data-stu-id="e4009-206">**Details**</span></span>
--- | ---
<span data-ttu-id="e4009-207">**Pros**</span><span class="sxs-lookup"><span data-stu-id="e4009-207">**Pros**</span></span> | <span data-ttu-id="e4009-208">Using PaaS and serverless solutions for the end-to-end deployment significantly reduces management time that Contoso must provide.</span><span class="sxs-lookup"><span data-stu-id="e4009-208">Using PaaS and serverless solutions for the end-to-end deployment significantly reduces management time that Contoso must provide.</span></span><br/><br/> <span data-ttu-id="e4009-209">Moving to a microservice architecture allows Contoso to easily extend the solution over time.</span><span class="sxs-lookup"><span data-stu-id="e4009-209">Moving to a microservice architecture allows Contoso to easily extend the solution over time.</span></span><br/><br/> <span data-ttu-id="e4009-210">New functionality can be brought online without disrupting any of the existing solutions code bases.</span><span class="sxs-lookup"><span data-stu-id="e4009-210">New functionality can be brought online without disrupting any of the existing solutions code bases.</span></span><br/><br/> <span data-ttu-id="e4009-211">The Web App will be configured with multiple instances with no single point of failure.</span><span class="sxs-lookup"><span data-stu-id="e4009-211">The Web App will be configured with multiple instances with no single point of failure.</span></span><br/><br/> <span data-ttu-id="e4009-212">Autoscaling will be enabled so that the app can handle differing traffic volumes.</span><span class="sxs-lookup"><span data-stu-id="e4009-212">Autoscaling will be enabled so that the app can handle differing traffic volumes.</span></span><br/><br/> <span data-ttu-id="e4009-213">With the move to PaaS services Contoso can retire out-of-date solutions running on Windows Server 2008 R2 operating system.</span><span class="sxs-lookup"><span data-stu-id="e4009-213">With the move to PaaS services Contoso can retire out-of-date solutions running on Windows Server 2008 R2 operating system.</span></span><br/><br/> <span data-ttu-id="e4009-214">CosmosDB has built-in fault tolerance, which requires no configuration by Contoso.</span><span class="sxs-lookup"><span data-stu-id="e4009-214">CosmosDB has built-in fault tolerance, which requires no configuration by Contoso.</span></span> <span data-ttu-id="e4009-215">This means that the data tier is no longer a single point of failover.</span><span class="sxs-lookup"><span data-stu-id="e4009-215">This means that the data tier is no longer a single point of failover.</span></span>
<span data-ttu-id="e4009-216">**Cons**</span><span class="sxs-lookup"><span data-stu-id="e4009-216">**Cons**</span></span> | <span data-ttu-id="e4009-217">Containers are more complex than other migration options.</span><span class="sxs-lookup"><span data-stu-id="e4009-217">Containers are more complex than other migration options.</span></span> <span data-ttu-id="e4009-218">The learning curve could be an issue for Contoso.</span><span class="sxs-lookup"><span data-stu-id="e4009-218">The learning curve could be an issue for Contoso.</span></span>  <span data-ttu-id="e4009-219">They introduce a new level of complexity that provides a lot of value in spite of the curve.</span><span class="sxs-lookup"><span data-stu-id="e4009-219">They introduce a new level of complexity that provides a lot of value in spite of the curve.</span></span><br/><br/> <span data-ttu-id="e4009-220">The operations team at Contoso needs to ramp up to understand and support Azure, containers and microservices for the app.</span><span class="sxs-lookup"><span data-stu-id="e4009-220">The operations team at Contoso needs to ramp up to understand and support Azure, containers and microservices for the app.</span></span><br/><br/> <span data-ttu-id="e4009-221">Contoso hasn't fully implemented DevOps for the entire solution.</span><span class="sxs-lookup"><span data-stu-id="e4009-221">Contoso hasn't fully implemented DevOps for the entire solution.</span></span> <span data-ttu-id="e4009-222">Contoso needs to think about that for the deployment of services to AKS, functions, and App Services.</span><span class="sxs-lookup"><span data-stu-id="e4009-222">Contoso needs to think about that for the deployment of services to AKS, functions, and App Services.</span></span>



### <a name="migration-process"></a><span data-ttu-id="e4009-223">Migration process</span><span class="sxs-lookup"><span data-stu-id="e4009-223">Migration process</span></span>

1. <span data-ttu-id="e4009-224">Contoso provision the ACR, AKS, and CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="e4009-224">Contoso provision the ACR, AKS, and CosmosDB.</span></span>
2. <span data-ttu-id="e4009-225">They provision the infrastructure for the deployment, including the Azure Web App, storage account, function, and API.</span><span class="sxs-lookup"><span data-stu-id="e4009-225">They provision the infrastructure for the deployment, including the Azure Web App, storage account, function, and API.</span></span> 
3. <span data-ttu-id="e4009-226">After the infrastructure is in place, they'll build their microservices container images using Azure DevOps, which pushes them to the ACR.</span><span class="sxs-lookup"><span data-stu-id="e4009-226">After the infrastructure is in place, they'll build their microservices container images using Azure DevOps, which pushes them to the ACR.</span></span>
4. <span data-ttu-id="e4009-227">Contoso will deploy these microservices to ASK using a PowerShell script.</span><span class="sxs-lookup"><span data-stu-id="e4009-227">Contoso will deploy these microservices to ASK using a PowerShell script.</span></span>
5. <span data-ttu-id="e4009-228">Finally, they'll deploy the Azure function and Web App.</span><span class="sxs-lookup"><span data-stu-id="e4009-228">Finally, they'll deploy the Azure function and Web App.</span></span>

    ![Migration process](./media/contoso-migration-rebuild/migration-process.png) 

### <a name="azure-services"></a><span data-ttu-id="e4009-230">Azure services</span><span class="sxs-lookup"><span data-stu-id="e4009-230">Azure services</span></span>

<span data-ttu-id="e4009-231">**Service**</span><span class="sxs-lookup"><span data-stu-id="e4009-231">**Service**</span></span> | <span data-ttu-id="e4009-232">**Description**</span><span class="sxs-lookup"><span data-stu-id="e4009-232">**Description**</span></span> | <span data-ttu-id="e4009-233">**Cost**</span><span class="sxs-lookup"><span data-stu-id="e4009-233">**Cost**</span></span>
--- | --- | ---
[<span data-ttu-id="e4009-234">AKS</span><span class="sxs-lookup"><span data-stu-id="e4009-234">AKS</span></span>](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | <span data-ttu-id="e4009-235">Simplifies Kubernetes management, deployment, and operations.</span><span class="sxs-lookup"><span data-stu-id="e4009-235">Simplifies Kubernetes management, deployment, and operations.</span></span> <span data-ttu-id="e4009-236">Provides a fully managed Kubernetes container orchestration service.</span><span class="sxs-lookup"><span data-stu-id="e4009-236">Provides a fully managed Kubernetes container orchestration service.</span></span>  | <span data-ttu-id="e4009-237">AKS is a free service.</span><span class="sxs-lookup"><span data-stu-id="e4009-237">AKS is a free service.</span></span>  <span data-ttu-id="e4009-238">Pay for only the virtual machines, and associated storage and networking resources consumed.</span><span class="sxs-lookup"><span data-stu-id="e4009-238">Pay for only the virtual machines, and associated storage and networking resources consumed.</span></span> <span data-ttu-id="e4009-239">[Learn more](https://azure.microsoft.com/pricing/details/kubernetes-service/).</span><span class="sxs-lookup"><span data-stu-id="e4009-239">[Learn more](https://azure.microsoft.com/pricing/details/kubernetes-service/).</span></span>
[<span data-ttu-id="e4009-240">Azure Functions</span><span class="sxs-lookup"><span data-stu-id="e4009-240">Azure Functions</span></span>](https://azure.microsoft.com/services/functions/) | <span data-ttu-id="e4009-241">Accelerates development with an event-driven, serverless compute experience.</span><span class="sxs-lookup"><span data-stu-id="e4009-241">Accelerates development with an event-driven, serverless compute experience.</span></span> <span data-ttu-id="e4009-242">Scale on demand.</span><span class="sxs-lookup"><span data-stu-id="e4009-242">Scale on demand.</span></span>  | <span data-ttu-id="e4009-243">Pay only for consumed resources.</span><span class="sxs-lookup"><span data-stu-id="e4009-243">Pay only for consumed resources.</span></span> <span data-ttu-id="e4009-244">Plan is billed based on per-second resource consumption and executions.</span><span class="sxs-lookup"><span data-stu-id="e4009-244">Plan is billed based on per-second resource consumption and executions.</span></span> <span data-ttu-id="e4009-245">[Learn more](https://azure.microsoft.com/pricing/details/functions/).</span><span class="sxs-lookup"><span data-stu-id="e4009-245">[Learn more](https://azure.microsoft.com/pricing/details/functions/).</span></span>
[<span data-ttu-id="e4009-246">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="e4009-246">Azure Container Registry</span></span>](https://azure.microsoft.com/services/container-registry/) | <span data-ttu-id="e4009-247">Stores images for all types of container deployments.</span><span class="sxs-lookup"><span data-stu-id="e4009-247">Stores images for all types of container deployments.</span></span> | <span data-ttu-id="e4009-248">Cost based on features, storage, and usage duration.</span><span class="sxs-lookup"><span data-stu-id="e4009-248">Cost based on features, storage, and usage duration.</span></span> <span data-ttu-id="e4009-249">[Learn more](https://azure.microsoft.com/pricing/details/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="e4009-249">[Learn more](https://azure.microsoft.com/pricing/details/container-registry/).</span></span>
[<span data-ttu-id="e4009-250">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e4009-250">Azure App Service</span></span>](https://azure.microsoft.com/services/app-service/containers/) | <span data-ttu-id="e4009-251">Quickly build, deploy, and scale enterprise-grade web, mobile, and API apps running on any platform.</span><span class="sxs-lookup"><span data-stu-id="e4009-251">Quickly build, deploy, and scale enterprise-grade web, mobile, and API apps running on any platform.</span></span> | <span data-ttu-id="e4009-252">App Service plans are billed on a per second basis.</span><span class="sxs-lookup"><span data-stu-id="e4009-252">App Service plans are billed on a per second basis.</span></span> <span data-ttu-id="e4009-253">[Learn more](https://azure.microsoft.com/pricing/details/app-service/windows/).</span><span class="sxs-lookup"><span data-stu-id="e4009-253">[Learn more](https://azure.microsoft.com/pricing/details/app-service/windows/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4009-254">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e4009-254">Prerequisites</span></span>

<span data-ttu-id="e4009-255">Here's what Contoso needs for this scenario:</span><span class="sxs-lookup"><span data-stu-id="e4009-255">Here's what Contoso needs for this scenario:</span></span>

<span data-ttu-id="e4009-256">**Requirements**</span><span class="sxs-lookup"><span data-stu-id="e4009-256">**Requirements**</span></span> | <span data-ttu-id="e4009-257">**Details**</span><span class="sxs-lookup"><span data-stu-id="e4009-257">**Details**</span></span>
--- | ---
<span data-ttu-id="e4009-258">**Azure subscription**</span><span class="sxs-lookup"><span data-stu-id="e4009-258">**Azure subscription**</span></span> | <span data-ttu-id="e4009-259">Contoso created subscriptions during an earlier article.</span><span class="sxs-lookup"><span data-stu-id="e4009-259">Contoso created subscriptions during an earlier article.</span></span> <span data-ttu-id="e4009-260">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="e4009-260">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span><br/><br/> <span data-ttu-id="e4009-261">If you create a free account, you're the administrator of your subscription and can perform all actions.</span><span class="sxs-lookup"><span data-stu-id="e4009-261">If you create a free account, you're the administrator of your subscription and can perform all actions.</span></span><br/><br/> <span data-ttu-id="e4009-262">If you use an existing subscription and you're not the administrator, you need to work with the admin to assign you Owner or Contributor permissions.</span><span class="sxs-lookup"><span data-stu-id="e4009-262">If you use an existing subscription and you're not the administrator, you need to work with the admin to assign you Owner or Contributor permissions.</span></span>
<span data-ttu-id="e4009-263">**Azure infrastructure**</span><span class="sxs-lookup"><span data-stu-id="e4009-263">**Azure infrastructure**</span></span> | <span data-ttu-id="e4009-264">[Learn how](contoso-migration-infrastructure.md) Contoso set up an Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="e4009-264">[Learn how](contoso-migration-infrastructure.md) Contoso set up an Azure infrastructure.</span></span>
<span data-ttu-id="e4009-265">**Developer prerequisites**</span><span class="sxs-lookup"><span data-stu-id="e4009-265">**Developer prerequisites**</span></span> | <span data-ttu-id="e4009-266">Contoso needs the following tools on a developer workstation:</span><span class="sxs-lookup"><span data-stu-id="e4009-266">Contoso needs the following tools on a developer workstation:</span></span><br/><br/> <span data-ttu-id="e4009-267">- [Visual Studio 2017 Community Edition: Version 15.5](https://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="e4009-267">- [Visual Studio 2017 Community Edition: Version 15.5](https://www.visualstudio.com/)</span></span><br/><br/> <span data-ttu-id="e4009-268">.NET workload enabled.</span><span class="sxs-lookup"><span data-stu-id="e4009-268">.NET workload enabled.</span></span><br/><br/> [<span data-ttu-id="e4009-269">Git</span><span class="sxs-lookup"><span data-stu-id="e4009-269">Git</span></span>](https://git-scm.com/)<br/><br/> [<span data-ttu-id="e4009-270">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4009-270">Azure PowerShell</span></span>](https://azure.microsoft.com/downloads/)<br/><br/> [<span data-ttu-id="e4009-271">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e4009-271">Azure CLI</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)<br/><br/> <span data-ttu-id="e4009-272">[Docker CE (Windows 10) or Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install/) set to use Windows Containers.</span><span class="sxs-lookup"><span data-stu-id="e4009-272">[Docker CE (Windows 10) or Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install/) set to use Windows Containers.</span></span>



## <a name="scenario-steps"></a><span data-ttu-id="e4009-273">Scenario steps</span><span class="sxs-lookup"><span data-stu-id="e4009-273">Scenario steps</span></span>

<span data-ttu-id="e4009-274">Here's how Contoso will run the migration:</span><span class="sxs-lookup"><span data-stu-id="e4009-274">Here's how Contoso will run the migration:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e4009-275">**Step 1: Provision AKS and ACR**: Contoso provisions the managed AKS cluster and Azure container registry using PowerShell</span><span class="sxs-lookup"><span data-stu-id="e4009-275">**Step 1: Provision AKS and ACR**: Contoso provisions the managed AKS cluster and Azure container registry using PowerShell</span></span>
> * <span data-ttu-id="e4009-276">**Step 2: Build Docker containers**: They set up CI for Docker containers using Azure DevOps, and push them to the ACR.</span><span class="sxs-lookup"><span data-stu-id="e4009-276">**Step 2: Build Docker containers**: They set up CI for Docker containers using Azure DevOps, and push them to the ACR.</span></span>
> * <span data-ttu-id="e4009-277">**Step 3: Deploy back-end microservices**: They deploy the rest of the infrastructure that will be leveraged by back-end microservices.</span><span class="sxs-lookup"><span data-stu-id="e4009-277">**Step 3: Deploy back-end microservices**: They deploy the rest of the infrastructure that will be leveraged by back-end microservices.</span></span>
> * <span data-ttu-id="e4009-278">**Step 4: Deploy front-end infrastructure**: They deploy the front-end infrastructure, inlcuding blob storage for the pet phones, the Cosmos DB, and Vision API.</span><span class="sxs-lookup"><span data-stu-id="e4009-278">**Step 4: Deploy front-end infrastructure**: They deploy the front-end infrastructure, inlcuding blob storage for the pet phones, the Cosmos DB, and Vision API.</span></span>
> * <span data-ttu-id="e4009-279">**Step 5: Migrate the back end**: They deploy microservices and run on AKS, to migrate the back end.</span><span class="sxs-lookup"><span data-stu-id="e4009-279">**Step 5: Migrate the back end**: They deploy microservices and run on AKS, to migrate the back end.</span></span>
> * <span data-ttu-id="e4009-280">**Step 6: Publish the front end**: They publish the SmartHotel360 app to the Azure App service, and the Function App that will be called by the pet service.</span><span class="sxs-lookup"><span data-stu-id="e4009-280">**Step 6: Publish the front end**: They publish the SmartHotel360 app to the Azure App service, and the Function App that will be called by the pet service.</span></span>



## <a name="step-1-provision-back-end-resources"></a><span data-ttu-id="e4009-281">Step 1: Provision back-end resources</span><span class="sxs-lookup"><span data-stu-id="e4009-281">Step 1: Provision back-end resources</span></span>

<span data-ttu-id="e4009-282">Contoso admins run a deployment script to create the managed Kubernetes cluster using AKS and the Azure Container Registry (ACR).</span><span class="sxs-lookup"><span data-stu-id="e4009-282">Contoso admins run a deployment script to create the managed Kubernetes cluster using AKS and the Azure Container Registry (ACR).</span></span>

- <span data-ttu-id="e4009-283">The instructions for this section use the **SmartHotel360-Azure-backend** repository.</span><span class="sxs-lookup"><span data-stu-id="e4009-283">The instructions for this section use the **SmartHotel360-Azure-backend** repository.</span></span>
- <span data-ttu-id="e4009-284">The **SmartHotel360-Azure-backend** GitHub repo contains all of the software for this part of the deployment.</span><span class="sxs-lookup"><span data-stu-id="e4009-284">The **SmartHotel360-Azure-backend** GitHub repo contains all of the software for this part of the deployment.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e4009-285">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e4009-285">Prerequisites</span></span>

1. <span data-ttu-id="e4009-286">Before they start, Contoso admins ensure that all prerequisitie software in installed on the dev machine they're using for the deployment.</span><span class="sxs-lookup"><span data-stu-id="e4009-286">Before they start, Contoso admins ensure that all prerequisitie software in installed on the dev machine they're using for the deployment.</span></span>
2. <span data-ttu-id="e4009-287">They clone the repo local to the dev machine using Git: **git clone https://github.com/Microsoft/SmartHotel360-Azure-backend.git**</span><span class="sxs-lookup"><span data-stu-id="e4009-287">They clone the repo local to the dev machine using Git: **git clone https://github.com/Microsoft/SmartHotel360-Azure-backend.git**</span></span>


### <a name="provision-aks-and-acr"></a><span data-ttu-id="e4009-288">Provision AKS and ACR</span><span class="sxs-lookup"><span data-stu-id="e4009-288">Provision AKS and ACR</span></span>

<span data-ttu-id="e4009-289">The Contoso admins provision as follows:</span><span class="sxs-lookup"><span data-stu-id="e4009-289">The Contoso admins provision as follows:</span></span>

1.  <span data-ttu-id="e4009-290">They open the folder using Visual Studio Code, and moves to the **/deploy/k8s** directory, which contains the script **gen-aks-env.ps1**.</span><span class="sxs-lookup"><span data-stu-id="e4009-290">They open the folder using Visual Studio Code, and moves to the **/deploy/k8s** directory, which contains the script **gen-aks-env.ps1**.</span></span>
2. <span data-ttu-id="e4009-291">They run the script to create the managed Kubernetes cluster, using AKS and ACR.</span><span class="sxs-lookup"><span data-stu-id="e4009-291">They run the script to create the managed Kubernetes cluster, using AKS and ACR.</span></span>

    ![AKS](./media/contoso-migration-rebuild/aks1.png)
 
3.  <span data-ttu-id="e4009-293">With the file open, they update the $location parameter to **eastus2**, and save the file.</span><span class="sxs-lookup"><span data-stu-id="e4009-293">With the file open, they update the $location parameter to **eastus2**, and save the file.</span></span>

    ![AKS](./media/contoso-migration-rebuild/aks2.png)

4. <span data-ttu-id="e4009-295">They click **View** > **Integrated Terminal** to open the integrated terminal in Code.</span><span class="sxs-lookup"><span data-stu-id="e4009-295">They click **View** > **Integrated Terminal** to open the integrated terminal in Code.</span></span>

    ![AKS](./media/contoso-migration-rebuild/aks3.png)

5. <span data-ttu-id="e4009-297">In the PowerShell Integrated terminal, they sign into Azure using the Connect-AzureRmAccount command.</span><span class="sxs-lookup"><span data-stu-id="e4009-297">In the PowerShell Integrated terminal, they sign into Azure using the Connect-AzureRmAccount command.</span></span> <span data-ttu-id="e4009-298">[Learn more](https://docs.microsoft.com/powershell/azure/get-started-azureps) about getting started with PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e4009-298">[Learn more](https://docs.microsoft.com/powershell/azure/get-started-azureps) about getting started with PowerShell.</span></span>

    ![AKS](./media/contoso-migration-rebuild/aks4.png)

6. <span data-ttu-id="e4009-300">They authenticate Azure CLI by running the **az login** command, and following the instructions to authenticate using their web browser.</span><span class="sxs-lookup"><span data-stu-id="e4009-300">They authenticate Azure CLI by running the **az login** command, and following the instructions to authenticate using their web browser.</span></span> <span data-ttu-id="e4009-301">[Learn more](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest) about logging in with Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e4009-301">[Learn more](https://docs.microsoft.com/cli/azure/authenticate-azure-cli?view=azure-cli-latest) about logging in with Azure CLI.</span></span>

    ![AKS](./media/contoso-migration-rebuild/aks5.png)

7. <span data-ttu-id="e4009-303">They run the following command, passing the resource group name of ContosoRG, the name of the AKS cluster smarthotel-aks-eus2, and the new registry name.</span><span class="sxs-lookup"><span data-stu-id="e4009-303">They run the following command, passing the resource group name of ContosoRG, the name of the AKS cluster smarthotel-aks-eus2, and the new registry name.</span></span>

    ```
    .\gen-aks-env.ps1  -resourceGroupName ContosoRg -orchestratorName smarthotelakseus2 -registryName smarthotelacreus2
    ```
    ![AKS](./media/contoso-migration-rebuild/aks6.png)

8. <span data-ttu-id="e4009-305">Azure creates another resource group, containing the resources for the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="e4009-305">Azure creates another resource group, containing the resources for the AKS cluster.</span></span>

    ![AKS](./media/contoso-migration-rebuild/aks7.png)

9. <span data-ttu-id="e4009-307">After the deployment is finished, they install the **kubectl** command-line tool.</span><span class="sxs-lookup"><span data-stu-id="e4009-307">After the deployment is finished, they install the **kubectl** command-line tool.</span></span> <span data-ttu-id="e4009-308">The tool is already installed on the Azure CloudShell.</span><span class="sxs-lookup"><span data-stu-id="e4009-308">The tool is already installed on the Azure CloudShell.</span></span>

    <span data-ttu-id="e4009-309">**az aks install-cli**</span><span class="sxs-lookup"><span data-stu-id="e4009-309">**az aks install-cli**</span></span>

10. <span data-ttu-id="e4009-310">They verify the connection to the cluster by running the **kubectl get nodes** command.</span><span class="sxs-lookup"><span data-stu-id="e4009-310">They verify the connection to the cluster by running the **kubectl get nodes** command.</span></span> <span data-ttu-id="e4009-311">The node is the same name as the VM in the automatically created resource group.</span><span class="sxs-lookup"><span data-stu-id="e4009-311">The node is the same name as the VM in the automatically created resource group.</span></span>

    ![AKS](./media/contoso-migration-rebuild/aks8.png)

11. <span data-ttu-id="e4009-313">They run  the following command to start the Kubernetes Dashboard:</span><span class="sxs-lookup"><span data-stu-id="e4009-313">They run  the following command to start the Kubernetes Dashboard:</span></span> 

    <span data-ttu-id="e4009-314">**az aks browse --resource-group ContosoRG --name smarthotelakseus2**</span><span class="sxs-lookup"><span data-stu-id="e4009-314">**az aks browse --resource-group ContosoRG --name smarthotelakseus2**</span></span>

12. <span data-ttu-id="e4009-315">A browser tab opens to the Dashboard.</span><span class="sxs-lookup"><span data-stu-id="e4009-315">A browser tab opens to the Dashboard.</span></span> <span data-ttu-id="e4009-316">This is a tunneled connection using the Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="e4009-316">This is a tunneled connection using the Azure CLI.</span></span> 

    ![AKS](./media/contoso-migration-rebuild/aks9.png)




## <a name="step-2-configure-the-back-end-pipeline"></a><span data-ttu-id="e4009-318">Step 2: Configure the back-end pipeline</span><span class="sxs-lookup"><span data-stu-id="e4009-318">Step 2: Configure the back-end pipeline</span></span>

### <a name="create-an-azure-devops-project-and-build"></a><span data-ttu-id="e4009-319">Create an Azure DevOps project and build</span><span class="sxs-lookup"><span data-stu-id="e4009-319">Create an Azure DevOps project and build</span></span>

<span data-ttu-id="e4009-320">Contoso creates an Azure DevOps project, and configures a CI Build to create the container and then pushes it to the ACR.</span><span class="sxs-lookup"><span data-stu-id="e4009-320">Contoso creates an Azure DevOps project, and configures a CI Build to create the container and then pushes it to the ACR.</span></span> <span data-ttu-id="e4009-321">The instructions in this section use the [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend) repository.r</span><span class="sxs-lookup"><span data-stu-id="e4009-321">The instructions in this section use the [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend) repository.r</span></span>

1. <span data-ttu-id="e4009-322">From visualstudio.com, they create a new organization (**contosodevops360.visualstudio.com**), and configure it to use Git.</span><span class="sxs-lookup"><span data-stu-id="e4009-322">From visualstudio.com, they create a new organization (**contosodevops360.visualstudio.com**), and configure it to use Git.</span></span>

2. <span data-ttu-id="e4009-323">They create a new project (**SmartHotelBackend**) using Git for version control, and Agile for the workflow.</span><span class="sxs-lookup"><span data-stu-id="e4009-323">They create a new project (**SmartHotelBackend**) using Git for version control, and Agile for the workflow.</span></span>

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts1.png) 


3. <span data-ttu-id="e4009-325">They import the GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="e4009-325">They import the GitHub repo.</span></span>

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts2.png)
    
4. <span data-ttu-id="e4009-327">In **Build and Release**, they create a new pipeline using Azure Repos Git as a source, from the imported **smarthotel** repository.</span><span class="sxs-lookup"><span data-stu-id="e4009-327">In **Build and Release**, they create a new pipeline using Azure Repos Git as a source, from the imported **smarthotel** repository.</span></span> 

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts3.png)

6. <span data-ttu-id="e4009-329">They select to start with an empty pipeline.</span><span class="sxs-lookup"><span data-stu-id="e4009-329">They select to start with an empty pipeline.</span></span>

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts4.png)  

7. <span data-ttu-id="e4009-331">They select **Hosted Linux Preview** for the build pipeline.</span><span class="sxs-lookup"><span data-stu-id="e4009-331">They select **Hosted Linux Preview** for the build pipeline.</span></span>

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts5.png) 
 
8. <span data-ttu-id="e4009-333">In **Phase 1**, they add a **Docker Compose** task.</span><span class="sxs-lookup"><span data-stu-id="e4009-333">In **Phase 1**, they add a **Docker Compose** task.</span></span> <span data-ttu-id="e4009-334">This task builds the Docker compose.</span><span class="sxs-lookup"><span data-stu-id="e4009-334">This task builds the Docker compose.</span></span>

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts6.png) 

9. <span data-ttu-id="e4009-336">They repeat and add another **Docker Compose** task.</span><span class="sxs-lookup"><span data-stu-id="e4009-336">They repeat and add another **Docker Compose** task.</span></span> <span data-ttu-id="e4009-337">This one pushes the containers to ACR.</span><span class="sxs-lookup"><span data-stu-id="e4009-337">This one pushes the containers to ACR.</span></span>

     ![Azure DevOps](./media/contoso-migration-rebuild/vsts7.png) 

8. <span data-ttu-id="e4009-339">They select the first task (to build), and configure the build with the Azure subscription, authorization, and the ACR.</span><span class="sxs-lookup"><span data-stu-id="e4009-339">They select the first task (to build), and configure the build with the Azure subscription, authorization, and the ACR.</span></span> 

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts8.png)

9. <span data-ttu-id="e4009-341">They specify the path of the **docket-compose.yaml** file, in the **src** folder of the repo.</span><span class="sxs-lookup"><span data-stu-id="e4009-341">They specify the path of the **docket-compose.yaml** file, in the **src** folder of the repo.</span></span> <span data-ttu-id="e4009-342">They select to build service images, and include the latest tag.</span><span class="sxs-lookup"><span data-stu-id="e4009-342">They select to build service images, and include the latest tag.</span></span> <span data-ttu-id="e4009-343">When the action changes to **Build service images**, the name of the Azure DevOps task changes to **Build services automatically**</span><span class="sxs-lookup"><span data-stu-id="e4009-343">When the action changes to **Build service images**, the name of the Azure DevOps task changes to **Build services automatically**</span></span>

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts9.png)

10. <span data-ttu-id="e4009-345">Now, they configure the second Docker task (to push).</span><span class="sxs-lookup"><span data-stu-id="e4009-345">Now, they configure the second Docker task (to push).</span></span> <span data-ttu-id="e4009-346">They select the subscription and the **smarthotelacreus2** ACR.</span><span class="sxs-lookup"><span data-stu-id="e4009-346">They select the subscription and the **smarthotelacreus2** ACR.</span></span> 

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts10.png)

11. <span data-ttu-id="e4009-348">Again, they enter the file to the docker-compose.yaml file, and select **Push service images** and include the latest tag.</span><span class="sxs-lookup"><span data-stu-id="e4009-348">Again, they enter the file to the docker-compose.yaml file, and select **Push service images** and include the latest tag.</span></span> <span data-ttu-id="e4009-349">When the action changes to **Push service images**, the name of the Azure DevOps task changes to **Push services automatically**</span><span class="sxs-lookup"><span data-stu-id="e4009-349">When the action changes to **Push service images**, the name of the Azure DevOps task changes to **Push services automatically**</span></span>

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts11.png)

12. <span data-ttu-id="e4009-351">With the Azure DevOps tasks configured, Contoso saves the build pipeline, and starts the build process.</span><span class="sxs-lookup"><span data-stu-id="e4009-351">With the Azure DevOps tasks configured, Contoso saves the build pipeline, and starts the build process.</span></span>

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts12.png)

13. <span data-ttu-id="e4009-353">They click on the build job to check progress.</span><span class="sxs-lookup"><span data-stu-id="e4009-353">They click on the build job to check progress.</span></span>

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts13.png)

14. <span data-ttu-id="e4009-355">After the build finishes, the ACR shows the new repos, which are populated with the containers used by the microservices.</span><span class="sxs-lookup"><span data-stu-id="e4009-355">After the build finishes, the ACR shows the new repos, which are populated with the containers used by the microservices.</span></span>

    ![Azure DevOps](./media/contoso-migration-rebuild/vsts14.png)


### <a name="deploy-the-back-end-infrastructure"></a><span data-ttu-id="e4009-357">Deploy the back-end infrastructure</span><span class="sxs-lookup"><span data-stu-id="e4009-357">Deploy the back-end infrastructure</span></span>

<span data-ttu-id="e4009-358">With the AKS cluster created and the Docker images built, Contoso admins now deploy the rest of the infrastructure that will be leveraged by back-end microservices.</span><span class="sxs-lookup"><span data-stu-id="e4009-358">With the AKS cluster created and the Docker images built, Contoso admins now deploy the rest of the infrastructure that will be leveraged by back-end microservices.</span></span>

- <span data-ttu-id="e4009-359">Instructions in the section use the [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend) repo.</span><span class="sxs-lookup"><span data-stu-id="e4009-359">Instructions in the section use the [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend) repo.</span></span>
- <span data-ttu-id="e4009-360">In the **/deploy/k8s/arm** folder, there's a single script to create all items.</span><span class="sxs-lookup"><span data-stu-id="e4009-360">In the **/deploy/k8s/arm** folder, there's a single script to create all items.</span></span> 

<span data-ttu-id="e4009-361">They deploy as follows:</span><span class="sxs-lookup"><span data-stu-id="e4009-361">They deploy as follows:</span></span>

1. <span data-ttu-id="e4009-362">They open a developer command prompt, and use the command az login for the Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="e4009-362">They open a developer command prompt, and use the command az login for the Azure subscription.</span></span>
2. <span data-ttu-id="e4009-363">They use the deploy.cmd file to deploy the Azure resources in the ContosoRG resource group and EUS2 region, by typing the following command:</span><span class="sxs-lookup"><span data-stu-id="e4009-363">They use the deploy.cmd file to deploy the Azure resources in the ContosoRG resource group and EUS2 region, by typing the following command:</span></span>

    <span data-ttu-id="e4009-364">**.\deploy.cmd azuredeploy ContosoRG -c eastus2**</span><span class="sxs-lookup"><span data-stu-id="e4009-364">**.\deploy.cmd azuredeploy ContosoRG -c eastus2**</span></span>

    ![Deploy backend](./media/contoso-migration-rebuild/backend1.png)

2. <span data-ttu-id="e4009-366">In the Azure portal, they capture the connection string for each database, to be used later.</span><span class="sxs-lookup"><span data-stu-id="e4009-366">In the Azure portal, they capture the connection string for each database, to be used later.</span></span>

    ![Deploy backend](./media/contoso-migration-rebuild/backend2.png)

### <a name="create-the-back-end-release-pipeline"></a><span data-ttu-id="e4009-368">Create the back-end release pipeline</span><span class="sxs-lookup"><span data-stu-id="e4009-368">Create the back-end release pipeline</span></span>

<span data-ttu-id="e4009-369">Now, Contoso admins do the following:</span><span class="sxs-lookup"><span data-stu-id="e4009-369">Now, Contoso admins do the following:</span></span>

- <span data-ttu-id="e4009-370">Deploy the NGINX ingress controller to allow inbound traffic to the services.</span><span class="sxs-lookup"><span data-stu-id="e4009-370">Deploy the NGINX ingress controller to allow inbound traffic to the services.</span></span>
- <span data-ttu-id="e4009-371">Deploy the microservices to the AKS cluster.</span><span class="sxs-lookup"><span data-stu-id="e4009-371">Deploy the microservices to the AKS cluster.</span></span>
- <span data-ttu-id="e4009-372">As a first step they update the connection strings to the microservices using VSTS.</span><span class="sxs-lookup"><span data-stu-id="e4009-372">As a first step they update the connection strings to the microservices using VSTS.</span></span> <span data-ttu-id="e4009-373">They then configure a new VSTS Release pipeline to deploy the microservices.</span><span class="sxs-lookup"><span data-stu-id="e4009-373">They then configure a new VSTS Release pipeline to deploy the microservices.</span></span>
- <span data-ttu-id="e4009-374">The instructions in this section use the [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend) repo.</span><span class="sxs-lookup"><span data-stu-id="e4009-374">The instructions in this section use the [SmartHotel360-Azure-Backend](https://github.com/Microsoft/SmartHotel360-Azure-backend) repo.</span></span>
- <span data-ttu-id="e4009-375">Note that Some of the configuration settings (for example Active Directory B2C) aren’t covered in this article.</span><span class="sxs-lookup"><span data-stu-id="e4009-375">Note that Some of the configuration settings (for example Active Directory B2C) aren’t covered in this article.</span></span> <span data-ttu-id="e4009-376">Read more information about these settings in the repo.</span><span class="sxs-lookup"><span data-stu-id="e4009-376">Read more information about these settings in the repo.</span></span>

<span data-ttu-id="e4009-377">They create the pipeline:</span><span class="sxs-lookup"><span data-stu-id="e4009-377">They create the pipeline:</span></span>

1. <span data-ttu-id="e4009-378">Using Visual Studio they update the **/deploy/k8s/config_local.yml** file with the database connection information they noted earlier.</span><span class="sxs-lookup"><span data-stu-id="e4009-378">Using Visual Studio they update the **/deploy/k8s/config_local.yml** file with the database connection information they noted earlier.</span></span>

    ![DB connections](./media/contoso-migration-rebuild/back-pipe1.png)

2. <span data-ttu-id="e4009-380">They open VSTS, and in the SmartHotel360 project, in **Releases**, they click **+New Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="e4009-380">They open VSTS, and in the SmartHotel360 project, in **Releases**, they click **+New Pipeline**.</span></span>

    ![New pipeline](./media/contoso-migration-rebuild/back-pipe2.png)

3. <span data-ttu-id="e4009-382">They click **Empty Job** to start the pipeline without a template.</span><span class="sxs-lookup"><span data-stu-id="e4009-382">They click **Empty Job** to start the pipeline without a template.</span></span>

    ![Empty job](./media/contoso-migration-rebuild/back-pipe3.png)

4. <span data-ttu-id="e4009-384">They provide the environment and pipeline names.</span><span class="sxs-lookup"><span data-stu-id="e4009-384">They provide the environment and pipeline names.</span></span>

      ![Environment name](./media/contoso-migration-rebuild/back-pipe4.png)

      ![Pipeline name](./media/contoso-migration-rebuild/back-pipe5.png)

5. <span data-ttu-id="e4009-387">They add an artifact.</span><span class="sxs-lookup"><span data-stu-id="e4009-387">They add an artifact.</span></span>

     ![Add artifact](./media/contoso-migration-rebuild/back-pipe6.png)

6. <span data-ttu-id="e4009-389">They select **Git** as the source type, and specify the project, source, and master branch for the SmartHotel360 app.</span><span class="sxs-lookup"><span data-stu-id="e4009-389">They select **Git** as the source type, and specify the project, source, and master branch for the SmartHotel360 app.</span></span>

    ![Artifact settings](./media/contoso-migration-rebuild/back-pipe7.png)

7. <span data-ttu-id="e4009-391">They click the task link.</span><span class="sxs-lookup"><span data-stu-id="e4009-391">They click the task link.</span></span>

    ![Task link](./media/contoso-migration-rebuild/back-pipe8.png)

8. <span data-ttu-id="e4009-393">They add a new Auzre PowerShell task so that they can run a PowerShell script in an Azure environment.</span><span class="sxs-lookup"><span data-stu-id="e4009-393">They add a new Auzre PowerShell task so that they can run a PowerShell script in an Azure environment.</span></span>

    ![PowerShell in Azure](./media/contoso-migration-rebuild/back-pipe9.png)

9. <span data-ttu-id="e4009-395">They select the Azure subscription for the task, and select the **deploy.ps1** script from the Git repo.</span><span class="sxs-lookup"><span data-stu-id="e4009-395">They select the Azure subscription for the task, and select the **deploy.ps1** script from the Git repo.</span></span>

    ![Run script](./media/contoso-migration-rebuild/back-pipe10.png)


10. <span data-ttu-id="e4009-397">They add arguments to the script.</span><span class="sxs-lookup"><span data-stu-id="e4009-397">They add arguments to the script.</span></span> <span data-ttu-id="e4009-398">the script will delete all cluster content (except **ingress** and **ingress controller**), and deploy the microservices.</span><span class="sxs-lookup"><span data-stu-id="e4009-398">the script will delete all cluster content (except **ingress** and **ingress controller**), and deploy the microservices.</span></span>

    ![Script arguments](./media/contoso-migration-rebuild/back-pipe11.png)

11. <span data-ttu-id="e4009-400">They set the preferred Azure PowerShell version to the latest, and save the pipeline.</span><span class="sxs-lookup"><span data-stu-id="e4009-400">They set the preferred Azure PowerShell version to the latest, and save the pipeline.</span></span>
12. <span data-ttu-id="e4009-401">They move back to the **Release** page, and manually create a new release.</span><span class="sxs-lookup"><span data-stu-id="e4009-401">They move back to the **Release** page, and manually create a new release.</span></span>

    ![New release](./media/contoso-migration-rebuild/back-pipe12.png)

13. <span data-ttu-id="e4009-403">They click the release after creating it, and in **Actions**, they click **Deploy**.</span><span class="sxs-lookup"><span data-stu-id="e4009-403">They click the release after creating it, and in **Actions**, they click **Deploy**.</span></span>

      ![Deploy release](./media/contoso-migration-rebuild/back-pipe13.png)  

14. <span data-ttu-id="e4009-405">When the deployment is complete, they run the following command to check the status of services, using the Azure Cloud Shell: **kubectl get services**.</span><span class="sxs-lookup"><span data-stu-id="e4009-405">When the deployment is complete, they run the following command to check the status of services, using the Azure Cloud Shell: **kubectl get services**.</span></span>


## <a name="step-3-provision-front-end-services"></a><span data-ttu-id="e4009-406">Step 3: Provision front-end services</span><span class="sxs-lookup"><span data-stu-id="e4009-406">Step 3: Provision front-end services</span></span>

<span data-ttu-id="e4009-407">Contoso admins need to deploy the infrastructure that will be used by the front end apps.</span><span class="sxs-lookup"><span data-stu-id="e4009-407">Contoso admins need to deploy the infrastructure that will be used by the front end apps.</span></span> <span data-ttu-id="e4009-408">They create a blob storage container for storing the pet images; the Cosmos database to store documents with the pet information; and the Vision API for the website.</span><span class="sxs-lookup"><span data-stu-id="e4009-408">They create a blob storage container for storing the pet images; the Cosmos database to store documents with the pet information; and the Vision API for the website.</span></span> 

<span data-ttu-id="e4009-409">Instructions for this section use the [SmartHotel360-public-web](https://github.com/Microsoft/SmartHotel360-public-web) repo.</span><span class="sxs-lookup"><span data-stu-id="e4009-409">Instructions for this section use the [SmartHotel360-public-web](https://github.com/Microsoft/SmartHotel360-public-web) repo.</span></span>

### <a name="create-blob-storage-containers"></a><span data-ttu-id="e4009-410">Create blob storage containers</span><span class="sxs-lookup"><span data-stu-id="e4009-410">Create blob storage containers</span></span>

1.  <span data-ttu-id="e4009-411">In Azure portal, they open the storage account that was created, and clicks **Blobs**.</span><span class="sxs-lookup"><span data-stu-id="e4009-411">In Azure portal, they open the storage account that was created, and clicks **Blobs**.</span></span>
2.  <span data-ttu-id="e4009-412">They create a new container (**Pets**) with the public access level set to container.</span><span class="sxs-lookup"><span data-stu-id="e4009-412">They create a new container (**Pets**) with the public access level set to container.</span></span> <span data-ttu-id="e4009-413">Users will upload their pet photos to this container.</span><span class="sxs-lookup"><span data-stu-id="e4009-413">Users will upload their pet photos to this container.</span></span>

    ![Storage blob](./media/contoso-migration-rebuild/blob1.png)

3. <span data-ttu-id="e4009-415">They create a second new container named **settings**.</span><span class="sxs-lookup"><span data-stu-id="e4009-415">They create a second new container named **settings**.</span></span> <span data-ttu-id="e4009-416">A file with all the front end app settings will be placed in this container.</span><span class="sxs-lookup"><span data-stu-id="e4009-416">A file with all the front end app settings will be placed in this container.</span></span>

    ![Storage blob](./media/contoso-migration-rebuild/blob2.png)

4. <span data-ttu-id="e4009-418">They capture the access details for the storage account in a text file, for future reference.</span><span class="sxs-lookup"><span data-stu-id="e4009-418">They capture the access details for the storage account in a text file, for future reference.</span></span>

    ![Storage blob](./media/contoso-migration-rebuild/blob2.png)

### <a name="provision-a-cosmos-database"></a><span data-ttu-id="e4009-420">Provision a Cosmos database</span><span class="sxs-lookup"><span data-stu-id="e4009-420">Provision a Cosmos database</span></span>

<span data-ttu-id="e4009-421">Contoso admins provision a Cosmos database to be used for pet information.</span><span class="sxs-lookup"><span data-stu-id="e4009-421">Contoso admins provision a Cosmos database to be used for pet information.</span></span>

1. <span data-ttu-id="e4009-422">They create an **Azure Cosmos DB** in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e4009-422">They create an **Azure Cosmos DB** in the Azure Marketplace.</span></span>

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos1.png)

2. <span data-ttu-id="e4009-424">They specify a name (**contosomarthotel**), select the SQL API, and place it in the production resource group ContosoRG, in the main East US 2 region.</span><span class="sxs-lookup"><span data-stu-id="e4009-424">They specify a name (**contosomarthotel**), select the SQL API, and place it in the production resource group ContosoRG, in the main East US 2 region.</span></span>

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos2.png)

3. <span data-ttu-id="e4009-426">They add a new collection to the database, with default capacity and throughput.</span><span class="sxs-lookup"><span data-stu-id="e4009-426">They add a new collection to the database, with default capacity and throughput.</span></span>

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos3.png)


4. <span data-ttu-id="e4009-428">They note the connection information for the database, for future reference.</span><span class="sxs-lookup"><span data-stu-id="e4009-428">They note the connection information for the database, for future reference.</span></span> 

    ![Cosmos DB](./media/contoso-migration-rebuild/cosmos4.png)


### <a name="provision-computer-vision"></a><span data-ttu-id="e4009-430">Provision Computer Vision</span><span class="sxs-lookup"><span data-stu-id="e4009-430">Provision Computer Vision</span></span>

<span data-ttu-id="e4009-431">Contoso admins provision the Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="e4009-431">Contoso admins provision the Computer Vision API.</span></span> <span data-ttu-id="e4009-432">The API will be called by the function, to evaluate pictures uploaded by users.</span><span class="sxs-lookup"><span data-stu-id="e4009-432">The API will be called by the function, to evaluate pictures uploaded by users.</span></span>

1. <span data-ttu-id="e4009-433">They create a **Computer Vision** instance in the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="e4009-433">They create a **Computer Vision** instance in the Azure Marketplace.</span></span>

     ![Computer Vision](./media/contoso-migration-rebuild/vision1.png)

2. <span data-ttu-id="e4009-435">They provision the API (**smarthotelpets**) in the production resource group ContosoRG, in the main East US 2 region.</span><span class="sxs-lookup"><span data-stu-id="e4009-435">They provision the API (**smarthotelpets**) in the production resource group ContosoRG, in the main East US 2 region.</span></span>

    ![Computer Vision](./media/contoso-migration-rebuild/vision2.png)

3. <span data-ttu-id="e4009-437">They save the connection settings for the API to a text file for later reference.</span><span class="sxs-lookup"><span data-stu-id="e4009-437">They save the connection settings for the API to a text file for later reference.</span></span>

     ![Computer Vision](./media/contoso-migration-rebuild/vision3.png)


### <a name="provision-the-azure-web-app"></a><span data-ttu-id="e4009-439">Provision the Azure Web App</span><span class="sxs-lookup"><span data-stu-id="e4009-439">Provision the Azure Web App</span></span>

<span data-ttu-id="e4009-440">Contoso admins provision the web app using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="e4009-440">Contoso admins provision the web app using the Azure portal.</span></span>


1. <span data-ttu-id="e4009-441">They select **Web App** in the portal.</span><span class="sxs-lookup"><span data-stu-id="e4009-441">They select **Web App** in the portal.</span></span>

    ![Web app](media/contoso-migration-rebuild/web-app1.png)

2. <span data-ttu-id="e4009-443">They provide an app name (**smarthotelcontoso**), run it on Windows, and place it in the production resources group **ContosoRG**.</span><span class="sxs-lookup"><span data-stu-id="e4009-443">They provide an app name (**smarthotelcontoso**), run it on Windows, and place it in the production resources group **ContosoRG**.</span></span> <span data-ttu-id="e4009-444">They create a new Application Insights instance for app monitoring..</span><span class="sxs-lookup"><span data-stu-id="e4009-444">They create a new Application Insights instance for app monitoring..</span></span>

    ![Web app name](media/contoso-migration-rebuild/web-app2.png)

3. <span data-ttu-id="e4009-446">After they're done, they browse to the address of the app to check it's been created successfully.</span><span class="sxs-lookup"><span data-stu-id="e4009-446">After they're done, they browse to the address of the app to check it's been created successfully.</span></span>

4. <span data-ttu-id="e4009-447">Now, in the Azure portal they create a staging slot for the code.</span><span class="sxs-lookup"><span data-stu-id="e4009-447">Now, in the Azure portal they create a staging slot for the code.</span></span> <span data-ttu-id="e4009-448">the pipeline will deploy to this slot.</span><span class="sxs-lookup"><span data-stu-id="e4009-448">the pipeline will deploy to this slot.</span></span> <span data-ttu-id="e4009-449">This ensures that code isn't put into production until admins perform a release.</span><span class="sxs-lookup"><span data-stu-id="e4009-449">This ensures that code isn't put into production until admins perform a release.</span></span>

    ![Web app staging slot](media/contoso-migration-rebuild/web-app3.png)



### <a name="provision-the-azure-function-app"></a><span data-ttu-id="e4009-451">Provision the Azure function app</span><span class="sxs-lookup"><span data-stu-id="e4009-451">Provision the Azure function app</span></span>

<span data-ttu-id="e4009-452">In the Azure portal, Contoso admins provision the Function App.</span><span class="sxs-lookup"><span data-stu-id="e4009-452">In the Azure portal, Contoso admins provision the Function App.</span></span>

1. <span data-ttu-id="e4009-453">They select **Function App**.</span><span class="sxs-lookup"><span data-stu-id="e4009-453">They select **Function App**.</span></span>

    ![Create function app](./media/contoso-migration-rebuild/function-app1.png)

2. <span data-ttu-id="e4009-455">They provide an app name (**smarthotelpetchecker**).</span><span class="sxs-lookup"><span data-stu-id="e4009-455">They provide an app name (**smarthotelpetchecker**).</span></span> <span data-ttu-id="e4009-456">They place the app in the production resource group **ContosoRG**.They set the hosting place to **Consumption Plan**, and place the app in the East US 2 region.</span><span class="sxs-lookup"><span data-stu-id="e4009-456">They place the app in the production resource group **ContosoRG**.They set the hosting place to **Consumption Plan**, and place the app in the East US 2 region.</span></span> <span data-ttu-id="e4009-457">A new storage account is created, along with an Application Insights instance for monitoring.</span><span class="sxs-lookup"><span data-stu-id="e4009-457">A new storage account is created, along with an Application Insights instance for monitoring.</span></span>

    ![Function app settings](./media/contoso-migration-rebuild/function-app2.png)


3. <span data-ttu-id="e4009-459">After the app is deployed, they browse to the app address to check it's been created successfully.</span><span class="sxs-lookup"><span data-stu-id="e4009-459">After the app is deployed, they browse to the app address to check it's been created successfully.</span></span>


## <a name="step-4-set-up-the-front-end-pipeline"></a><span data-ttu-id="e4009-460">Step 4: Set up the front-end pipeline</span><span class="sxs-lookup"><span data-stu-id="e4009-460">Step 4: Set up the front-end pipeline</span></span>

<span data-ttu-id="e4009-461">Contoso admins create two different projects for the front-end site.</span><span class="sxs-lookup"><span data-stu-id="e4009-461">Contoso admins create two different projects for the front-end site.</span></span> 

1. <span data-ttu-id="e4009-462">In VSTS, they create a project **SmartHotelFrontend**.</span><span class="sxs-lookup"><span data-stu-id="e4009-462">In VSTS, they create a project **SmartHotelFrontend**.</span></span>

    ![Front-end project](./media/contoso-migration-rebuild/function-app1.png)

2. <span data-ttu-id="e4009-464">They import the [SmartHotel360 front-end](https://github.com/Microsoft/SmartHotel360-public-web.git) Git repo into the new project.</span><span class="sxs-lookup"><span data-stu-id="e4009-464">They import the [SmartHotel360 front-end](https://github.com/Microsoft/SmartHotel360-public-web.git) Git repo into the new project.</span></span>
3. <span data-ttu-id="e4009-465">For the Function App, they create another VSTS project (SmartHotelPetChecker), and import the [PetChecker](https://github.com/Microsoft/SmartHotel360-PetCheckerFunction ) Git repo into this project.</span><span class="sxs-lookup"><span data-stu-id="e4009-465">For the Function App, they create another VSTS project (SmartHotelPetChecker), and import the [PetChecker](https://github.com/Microsoft/SmartHotel360-PetCheckerFunction ) Git repo into this project.</span></span>

### <a name="configure-the-web-app"></a><span data-ttu-id="e4009-466">Configure the Web App</span><span class="sxs-lookup"><span data-stu-id="e4009-466">Configure the Web App</span></span>

<span data-ttu-id="e4009-467">Now Contoso admins configure the Web App to use Contoso resources.</span><span class="sxs-lookup"><span data-stu-id="e4009-467">Now Contoso admins configure the Web App to use Contoso resources.</span></span>

1. <span data-ttu-id="e4009-468">They connect to the VSTS project, and clone the repo locally to the dev machine.</span><span class="sxs-lookup"><span data-stu-id="e4009-468">They connect to the VSTS project, and clone the repo locally to the dev machine.</span></span>
2. <span data-ttu-id="e4009-469">In Visual Studio, they open the folder to show all the files in the repo.</span><span class="sxs-lookup"><span data-stu-id="e4009-469">In Visual Studio, they open the folder to show all the files in the repo.</span></span>

    ![Repo files](./media/contoso-migration-rebuild/configure-webapp1.png)

3. <span data-ttu-id="e4009-471">They update the configuration changes as required.</span><span class="sxs-lookup"><span data-stu-id="e4009-471">They update the configuration changes as required.</span></span>

    - <span data-ttu-id="e4009-472">When the web app starts up, it looks for the **SettingsUrl** app setting.</span><span class="sxs-lookup"><span data-stu-id="e4009-472">When the web app starts up, it looks for the **SettingsUrl** app setting.</span></span>
    - <span data-ttu-id="e4009-473">This variable must contain a URL pointing to a configuration file.</span><span class="sxs-lookup"><span data-stu-id="e4009-473">This variable must contain a URL pointing to a configuration file.</span></span>
    - <span data-ttu-id="e4009-474">By default, the setting used is a public endpoint.</span><span class="sxs-lookup"><span data-stu-id="e4009-474">By default, the setting used is a public endpoint.</span></span>

4.  <span data-ttu-id="e4009-475">They update the /config-sample.json/sample.json file.</span><span class="sxs-lookup"><span data-stu-id="e4009-475">They update the /config-sample.json/sample.json file.</span></span>

    - <span data-ttu-id="e4009-476">This is the configuration file for the web when using the public endpoint.</span><span class="sxs-lookup"><span data-stu-id="e4009-476">This is the configuration file for the web when using the public endpoint.</span></span>
    - <span data-ttu-id="e4009-477">They edit the **urls** and **pets_config** sections with the values for the AKS API endpoints, storage accounts, and Cosmos database.</span><span class="sxs-lookup"><span data-stu-id="e4009-477">They edit the **urls** and **pets_config** sections with the values for the AKS API endpoints, storage accounts, and Cosmos database.</span></span>
    - <span data-ttu-id="e4009-478">The URLs should match the DNS name of the new web app that Contoso will create.</span><span class="sxs-lookup"><span data-stu-id="e4009-478">The URLs should match the DNS name of the new web app that Contoso will create.</span></span>
    - <span data-ttu-id="e4009-479">For Contoso, this is **smarthotelcontoso.eastus2.cloudapp.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="e4009-479">For Contoso, this is **smarthotelcontoso.eastus2.cloudapp.azure.com**.</span></span>

    ![Json settings](./media/contoso-migration-rebuild/configure-webapp2.png)

5. <span data-ttu-id="e4009-481">After the file is updated, they rename it **smarthotelsettingsurl**, and upload it to the storage blog they created earlier.</span><span class="sxs-lookup"><span data-stu-id="e4009-481">After the file is updated, they rename it **smarthotelsettingsurl**, and upload it to the storage blog they created earlier.</span></span>

    ![Rename and upload](./media/contoso-migration-rebuild/configure-webapp3.png)

6. <span data-ttu-id="e4009-483">They click the file to get the URL.</span><span class="sxs-lookup"><span data-stu-id="e4009-483">They click the file to get the URL.</span></span> <span data-ttu-id="e4009-484">The URL is used by the app when it pulls down the configuration files.</span><span class="sxs-lookup"><span data-stu-id="e4009-484">The URL is used by the app when it pulls down the configuration files.</span></span>

    ![App URL](./media/contoso-migration-rebuild/configure-webapp4.png)

7. <span data-ttu-id="e4009-486">In the **appsettings.Production.json** file, they update the **SettingsURL** to the URL of the new file.</span><span class="sxs-lookup"><span data-stu-id="e4009-486">In the **appsettings.Production.json** file, they update the **SettingsURL** to the URL of the new file.</span></span>

    ![Update URL](./media/contoso-migration-rebuild/configure-webapp5.png)

### <a name="deploy-the-website-to-the-azure-app-service"></a><span data-ttu-id="e4009-488">Deploy the website to the Azure App Service</span><span class="sxs-lookup"><span data-stu-id="e4009-488">Deploy the website to the Azure App Service</span></span>

<span data-ttu-id="e4009-489">Contoso admins can now publish the website.</span><span class="sxs-lookup"><span data-stu-id="e4009-489">Contoso admins can now publish the website.</span></span>


1. <span data-ttu-id="e4009-490">They open VSTS, and in the **SmartHotelFrontend** project, in **Builds and Releases**, they click **+New Pipeline**.</span><span class="sxs-lookup"><span data-stu-id="e4009-490">They open VSTS, and in the **SmartHotelFrontend** project, in **Builds and Releases**, they click **+New Pipeline**.</span></span>
2. <span data-ttu-id="e4009-491">They select **VSTS Git** as a source.</span><span class="sxs-lookup"><span data-stu-id="e4009-491">They select **VSTS Git** as a source.</span></span>

    ![New pipeline](./media/contoso-migration-rebuild/vsts-publishfront1.png)

3. <span data-ttu-id="e4009-493">They select the **ASP.NET Core** template.</span><span class="sxs-lookup"><span data-stu-id="e4009-493">They select the **ASP.NET Core** template.</span></span>
4. <span data-ttu-id="e4009-494">They review the pipeline, and check that **Publish Web Projects** and **Zip Published Projects** are selected.</span><span class="sxs-lookup"><span data-stu-id="e4009-494">They review the pipeline, and check that **Publish Web Projects** and **Zip Published Projects** are selected.</span></span>

    ![Pipeline settings](./media/contoso-migration-rebuild/vsts-publishfront2.png)

5. <span data-ttu-id="e4009-496">In **Triggers**, they enable continuous integration, and add the master branch.</span><span class="sxs-lookup"><span data-stu-id="e4009-496">In **Triggers**, they enable continuous integration, and add the master branch.</span></span> <span data-ttu-id="e4009-497">This ensures that each tim the solution has new code committed to the master branch, the build pipeline starts.</span><span class="sxs-lookup"><span data-stu-id="e4009-497">This ensures that each tim the solution has new code committed to the master branch, the build pipeline starts.</span></span>

    ![Continous integration](./media/contoso-migration-rebuild/vsts-publishfront3.png)

6. <span data-ttu-id="e4009-499">They click **Save & queue** to start a build.</span><span class="sxs-lookup"><span data-stu-id="e4009-499">They click **Save & queue** to start a build.</span></span>
7. <span data-ttu-id="e4009-500">After the build completes, they configure a release pipeline using the **Azure App Service Deployment**.</span><span class="sxs-lookup"><span data-stu-id="e4009-500">After the build completes, they configure a release pipeline using the **Azure App Service Deployment**.</span></span>
8. <span data-ttu-id="e4009-501">They provide an environment name **Staging**.</span><span class="sxs-lookup"><span data-stu-id="e4009-501">They provide an environment name **Staging**.</span></span>

    ![Environment name](./media/contoso-migration-rebuild/vsts-publishfront4.png)

9. <span data-ttu-id="e4009-503">They add an artifact, and select the build they just configured.</span><span class="sxs-lookup"><span data-stu-id="e4009-503">They add an artifact, and select the build they just configured.</span></span>

     ![Add artifact](./media/contoso-migration-rebuild/vsts-publishfront5.png)

6. <span data-ttu-id="e4009-505">They click the lightning bolt icon on the artifcat, and enable continuous deployment.</span><span class="sxs-lookup"><span data-stu-id="e4009-505">They click the lightning bolt icon on the artifcat, and enable continuous deployment.</span></span>

    ![Continuous deployment](./media/contoso-migration-rebuild/vsts-publishfront6.png)

7. <span data-ttu-id="e4009-507">In **Environment**, they click **1 phase, 1 task** under **Staging**.</span><span class="sxs-lookup"><span data-stu-id="e4009-507">In **Environment**, they click **1 phase, 1 task** under **Staging**.</span></span>
8. <span data-ttu-id="e4009-508">After selecting the subscription, and app name, they open the **Deploy Azure App Service** task.</span><span class="sxs-lookup"><span data-stu-id="e4009-508">After selecting the subscription, and app name, they open the **Deploy Azure App Service** task.</span></span> <span data-ttu-id="e4009-509">The deployment is configured to use the **staging** deployment slot.</span><span class="sxs-lookup"><span data-stu-id="e4009-509">The deployment is configured to use the **staging** deployment slot.</span></span> <span data-ttu-id="e4009-510">This automatically builds code for review and approval in this slot.</span><span class="sxs-lookup"><span data-stu-id="e4009-510">This automatically builds code for review and approval in this slot.</span></span>

     ![Slot](./media/contoso-migration-rebuild/vsts-publishfront7.png)

9. <span data-ttu-id="e4009-512">In the **New release pipeline**, they add a new environment.</span><span class="sxs-lookup"><span data-stu-id="e4009-512">In the **New release pipeline**, they add a new environment.</span></span>

    ![New environment](./media/contoso-migration-rebuild/vsts-publishfront8.png)

10. <span data-ttu-id="e4009-514">They select **Azure App Service deployment with slot**, and name the enviroment **Prod**.</span><span class="sxs-lookup"><span data-stu-id="e4009-514">They select **Azure App Service deployment with slot**, and name the enviroment **Prod**.</span></span>

    ![Environment name](./media/contoso-migration-rebuild/vsts-publishfront9.png)

11. <span data-ttu-id="e4009-516">They click on **1 phase, 2 tasks**, and select the subscription, app service name, and **staging** slot.</span><span class="sxs-lookup"><span data-stu-id="e4009-516">They click on **1 phase, 2 tasks**, and select the subscription, app service name, and **staging** slot.</span></span>

    ![Environment name](./media/contoso-migration-rebuild/vsts-publishfront10.png)

12. <span data-ttu-id="e4009-518">They remove the **Deploy Azure App Service to Slot** from the pipeline.</span><span class="sxs-lookup"><span data-stu-id="e4009-518">They remove the **Deploy Azure App Service to Slot** from the pipeline.</span></span> <span data-ttu-id="e4009-519">It was placed there by the previous steps.</span><span class="sxs-lookup"><span data-stu-id="e4009-519">It was placed there by the previous steps.</span></span>

    ![Remove from pipeline](./media/contoso-migration-rebuild/vsts-publishfront11.png)

13. <span data-ttu-id="e4009-521">They save the pipeline.</span><span class="sxs-lookup"><span data-stu-id="e4009-521">They save the pipeline.</span></span> <span data-ttu-id="e4009-522">On the pipeline, they click on **Post-deployment conditions**.</span><span class="sxs-lookup"><span data-stu-id="e4009-522">On the pipeline, they click on **Post-deployment conditions**.</span></span>

    ![Post-deployment](./media/contoso-migration-rebuild/vsts-publishfront12.png)

14. <span data-ttu-id="e4009-524">They enable **Post-deployment approvals**, and add a dev lead as the approver.</span><span class="sxs-lookup"><span data-stu-id="e4009-524">They enable **Post-deployment approvals**, and add a dev lead as the approver.</span></span>

    ![Post-deployment approval](./media/contoso-migration-rebuild/vsts-publishfront13.png)

15. <span data-ttu-id="e4009-526">In the Build pipeline, they manually kick off a build.</span><span class="sxs-lookup"><span data-stu-id="e4009-526">In the Build pipeline, they manually kick off a build.</span></span> <span data-ttu-id="e4009-527">This triggers the new release pipeline, which deploys the site to the staging slot.</span><span class="sxs-lookup"><span data-stu-id="e4009-527">This triggers the new release pipeline, which deploys the site to the staging slot.</span></span> <span data-ttu-id="e4009-528">For Contoso, the URL for the slot is **https://smarthotelcontoso-staging.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="e4009-528">For Contoso, the URL for the slot is **https://smarthotelcontoso-staging.azurewebsites.net/**.</span></span>
16. <span data-ttu-id="e4009-529">After the build finishes, and the release deploys to the slot, VSTS emails the dev lead for approval.</span><span class="sxs-lookup"><span data-stu-id="e4009-529">After the build finishes, and the release deploys to the slot, VSTS emails the dev lead for approval.</span></span>
17. <span data-ttu-id="e4009-530">The dev lead clicks **View approval**, and can approve or reject the request in the VSTS portal.</span><span class="sxs-lookup"><span data-stu-id="e4009-530">The dev lead clicks **View approval**, and can approve or reject the request in the VSTS portal.</span></span>

    ![Approval mail](./media/contoso-migration-rebuild/vsts-publishfront14.png)

16. <span data-ttu-id="e4009-532">The lead makes a comment and approves.</span><span class="sxs-lookup"><span data-stu-id="e4009-532">The lead makes a comment and approves.</span></span> <span data-ttu-id="e4009-533">This starts the swap of the **staging** and **prod** slots, and moves the build into production.</span><span class="sxs-lookup"><span data-stu-id="e4009-533">This starts the swap of the **staging** and **prod** slots, and moves the build into production.</span></span>

    ![Approve and swap](./media/contoso-migration-rebuild/vsts-publishfront15.png)

17. <span data-ttu-id="e4009-535">The pipeline completes the swap.</span><span class="sxs-lookup"><span data-stu-id="e4009-535">The pipeline completes the swap.</span></span>

    ![Complete swap](./media/contoso-migration-rebuild/vsts-publishfront16.png)

18. <span data-ttu-id="e4009-537">The team checks the **prod** slot to verify that the web app is in production at **https://smarthotelcontoso.azurewebsites.net/**.</span><span class="sxs-lookup"><span data-stu-id="e4009-537">The team checks the **prod** slot to verify that the web app is in production at **https://smarthotelcontoso.azurewebsites.net/**.</span></span>


### <a name="deploy-the-petchecker-function-app"></a><span data-ttu-id="e4009-538">Deploy the PetChecker Function App</span><span class="sxs-lookup"><span data-stu-id="e4009-538">Deploy the PetChecker Function App</span></span>

<span data-ttu-id="e4009-539">Contoso admins deploy the app as follows.</span><span class="sxs-lookup"><span data-stu-id="e4009-539">Contoso admins deploy the app as follows.</span></span>

1. <span data-ttu-id="e4009-540">They clone the repo locally to the dev machine by connecting to the VSTS project.</span><span class="sxs-lookup"><span data-stu-id="e4009-540">They clone the repo locally to the dev machine by connecting to the VSTS project.</span></span>
2. <span data-ttu-id="e4009-541">In Visual Studio, they open the folder to show all the files in the repo.</span><span class="sxs-lookup"><span data-stu-id="e4009-541">In Visual Studio, they open the folder to show all the files in the repo.</span></span>
3. <span data-ttu-id="e4009-542">They open the **src/PetCheckerFunction/local.settings.json** file, and add the app settings for storage, the Cosmos database, and the Computer Vision API.</span><span class="sxs-lookup"><span data-stu-id="e4009-542">They open the **src/PetCheckerFunction/local.settings.json** file, and add the app settings for storage, the Cosmos database, and the Computer Vision API.</span></span>

    ![Deploy the function](./media/contoso-migration-rebuild/function5.png)

4. <span data-ttu-id="e4009-544">They commit the code, and sync it back to VSTS, pushing their changes.</span><span class="sxs-lookup"><span data-stu-id="e4009-544">They commit the code, and sync it back to VSTS, pushing their changes.</span></span>
5. <span data-ttu-id="e4009-545">They add a new Build pipeline, and select **VSTS Git** for the source.</span><span class="sxs-lookup"><span data-stu-id="e4009-545">They add a new Build pipeline, and select **VSTS Git** for the source.</span></span>
6. <span data-ttu-id="e4009-546">They select the **ASP.NET Core (.NET Framework)** template.</span><span class="sxs-lookup"><span data-stu-id="e4009-546">They select the **ASP.NET Core (.NET Framework)** template.</span></span>
7. <span data-ttu-id="e4009-547">They accept the defaults for the template.</span><span class="sxs-lookup"><span data-stu-id="e4009-547">They accept the defaults for the template.</span></span>
8. <span data-ttu-id="e4009-548">In **Triggers**, then select to **Enable continuous integration**, and click **Save & Queue** to start a build.</span><span class="sxs-lookup"><span data-stu-id="e4009-548">In **Triggers**, then select to **Enable continuous integration**, and click **Save & Queue** to start a build.</span></span>
9. <span data-ttu-id="e4009-549">After the build succeeds, they build a Release pipeline, adding the **Azure App Service deployment with slot**.</span><span class="sxs-lookup"><span data-stu-id="e4009-549">After the build succeeds, they build a Release pipeline, adding the **Azure App Service deployment with slot**.</span></span>
10. <span data-ttu-id="e4009-550">They name the environment **Prod**, and select the subscription.</span><span class="sxs-lookup"><span data-stu-id="e4009-550">They name the environment **Prod**, and select the subscription.</span></span> <span data-ttu-id="e4009-551">They set the **App type** to **Function Ap**, and the app service name as **smarthotelpetchecker**.</span><span class="sxs-lookup"><span data-stu-id="e4009-551">They set the **App type** to **Function Ap**, and the app service name as **smarthotelpetchecker**.</span></span>

    ![Function app](./media/contoso-migration-rebuild/petchecker2.png)

11. <span data-ttu-id="e4009-553">They add an artifact **Build**.</span><span class="sxs-lookup"><span data-stu-id="e4009-553">They add an artifact **Build**.</span></span>

    ![Artifact](./media/contoso-migration-rebuild/petchecker3.png)

12. <span data-ttu-id="e4009-555">They enable **Continuous deployment trigger**, and click **Save**.</span><span class="sxs-lookup"><span data-stu-id="e4009-555">They enable **Continuous deployment trigger**, and click **Save**.</span></span>
13. <span data-ttu-id="e4009-556">They click **Queue new build** to run the full CI/CD pipeline.</span><span class="sxs-lookup"><span data-stu-id="e4009-556">They click **Queue new build** to run the full CI/CD pipeline.</span></span>
14. <span data-ttu-id="e4009-557">After the function is deployed, it appears in the Azure portal, with the **Running** status.</span><span class="sxs-lookup"><span data-stu-id="e4009-557">After the function is deployed, it appears in the Azure portal, with the **Running** status.</span></span>

    ![Deploy the function](./media/contoso-migration-rebuild/function6.png)


7. <span data-ttu-id="e4009-559">They browse to the app to test that the Pet Checker app is working as expected, at [http://smarthotel360public.azurewebsites.net/Pets](http://smarthotel360public.azurewebsites.net/Pets).</span><span class="sxs-lookup"><span data-stu-id="e4009-559">They browse to the app to test that the Pet Checker app is working as expected, at [http://smarthotel360public.azurewebsites.net/Pets](http://smarthotel360public.azurewebsites.net/Pets).</span></span>
8. <span data-ttu-id="e4009-560">They click on the avatar to upload a picture.</span><span class="sxs-lookup"><span data-stu-id="e4009-560">They click on the avatar to upload a picture.</span></span>

    ![Deploy the function](./media/contoso-migration-rebuild/function7.png)

9. <span data-ttu-id="e4009-562">The first photo they want to check is of a small dog.</span><span class="sxs-lookup"><span data-stu-id="e4009-562">The first photo they want to check is of a small dog.</span></span>

    ![Deploy the function](./media/contoso-migration-rebuild/function8.png)

10. <span data-ttu-id="e4009-564">The app returns a message of acceptance.</span><span class="sxs-lookup"><span data-stu-id="e4009-564">The app returns a message of acceptance.</span></span>

    ![Deploy the function](./media/contoso-migration-rebuild/function9.png)






## <a name="review-the-deployment"></a><span data-ttu-id="e4009-566">Review the deployment</span><span class="sxs-lookup"><span data-stu-id="e4009-566">Review the deployment</span></span>

<span data-ttu-id="e4009-567">With the migrated resources in Azure, Contoso now needs to fully operationalize and secure the new infrastructure.</span><span class="sxs-lookup"><span data-stu-id="e4009-567">With the migrated resources in Azure, Contoso now needs to fully operationalize and secure the new infrastructure.</span></span>

### <a name="security"></a><span data-ttu-id="e4009-568">Security</span><span class="sxs-lookup"><span data-stu-id="e4009-568">Security</span></span>

- <span data-ttu-id="e4009-569">Contoso needs to ensure that the new databases are secure.</span><span class="sxs-lookup"><span data-stu-id="e4009-569">Contoso needs to ensure that the new databases are secure.</span></span> <span data-ttu-id="e4009-570">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).</span><span class="sxs-lookup"><span data-stu-id="e4009-570">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).</span></span>
- <span data-ttu-id="e4009-571">The app needs to be updated to use SSL with certificates.</span><span class="sxs-lookup"><span data-stu-id="e4009-571">The app needs to be updated to use SSL with certificates.</span></span> <span data-ttu-id="e4009-572">The container instance should be redeployed to answer on 443.</span><span class="sxs-lookup"><span data-stu-id="e4009-572">The container instance should be redeployed to answer on 443.</span></span>
- <span data-ttu-id="e4009-573">Contoso should consider using KeyVault to protect secrets for their Service Fabric apps.</span><span class="sxs-lookup"><span data-stu-id="e4009-573">Contoso should consider using KeyVault to protect secrets for their Service Fabric apps.</span></span> <span data-ttu-id="e4009-574">[Learn more](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).</span><span class="sxs-lookup"><span data-stu-id="e4009-574">[Learn more](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).</span></span>

### <a name="backups-and-disaster-recovery"></a><span data-ttu-id="e4009-575">Backups and disaster recovery</span><span class="sxs-lookup"><span data-stu-id="e4009-575">Backups and disaster recovery</span></span>

- <span data-ttu-id="e4009-576">Contoso needs to review backup requirements for the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="e4009-576">Contoso needs to review backup requirements for the Azure SQL Database.</span></span> <span data-ttu-id="e4009-577">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="e4009-577">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).</span></span>
- <span data-ttu-id="e4009-578">Contoso should consider implementing SQL failover groups to provide regional failover for the database.</span><span class="sxs-lookup"><span data-stu-id="e4009-578">Contoso should consider implementing SQL failover groups to provide regional failover for the database.</span></span> <span data-ttu-id="e4009-579">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).</span><span class="sxs-lookup"><span data-stu-id="e4009-579">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).</span></span>
- <span data-ttu-id="e4009-580">Contoso can leverage geo-replication for the ACR premium SKU.</span><span class="sxs-lookup"><span data-stu-id="e4009-580">Contoso can leverage geo-replication for the ACR premium SKU.</span></span> <span data-ttu-id="e4009-581">[Learn more](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).</span><span class="sxs-lookup"><span data-stu-id="e4009-581">[Learn more](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).</span></span>
- <span data-ttu-id="e4009-582">Cosmos DB backs up automatically.</span><span class="sxs-lookup"><span data-stu-id="e4009-582">Cosmos DB backs up automatically.</span></span> <span data-ttu-id="e4009-583">Contoso can [learn more](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore) about this process.</span><span class="sxs-lookup"><span data-stu-id="e4009-583">Contoso can [learn more](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore) about this process.</span></span>

### <a name="licensing-and-cost-optimization"></a><span data-ttu-id="e4009-584">Licensing and cost optimization</span><span class="sxs-lookup"><span data-stu-id="e4009-584">Licensing and cost optimization</span></span>

- <span data-ttu-id="e4009-585">After all resources are deployed, Contoso should assign Azure tags based on their [infrastructure planning](contoso-migration-infrastructure.md#set-up-tagging).</span><span class="sxs-lookup"><span data-stu-id="e4009-585">After all resources are deployed, Contoso should assign Azure tags based on their [infrastructure planning](contoso-migration-infrastructure.md#set-up-tagging).</span></span>
- <span data-ttu-id="e4009-586">All licensing is built into the cost of the PaaS services that Contoso is consuming.</span><span class="sxs-lookup"><span data-stu-id="e4009-586">All licensing is built into the cost of the PaaS services that Contoso is consuming.</span></span> <span data-ttu-id="e4009-587">This will be deducted from the EA.</span><span class="sxs-lookup"><span data-stu-id="e4009-587">This will be deducted from the EA.</span></span>
- <span data-ttu-id="e4009-588">Contoso will enable Azure Cost Management licensed by Cloudyn, a Microsoft subsidiary.</span><span class="sxs-lookup"><span data-stu-id="e4009-588">Contoso will enable Azure Cost Management licensed by Cloudyn, a Microsoft subsidiary.</span></span> <span data-ttu-id="e4009-589">It's a multi-cloud cost management solution that helps you to utilize and manage Azure and other cloud resources.</span><span class="sxs-lookup"><span data-stu-id="e4009-589">It's a multi-cloud cost management solution that helps you to utilize and manage Azure and other cloud resources.</span></span>  <span data-ttu-id="e4009-590">[Learn more](https://docs.microsoft.com/azure/cost-management/overview) about Azure Cost Management.</span><span class="sxs-lookup"><span data-stu-id="e4009-590">[Learn more](https://docs.microsoft.com/azure/cost-management/overview) about Azure Cost Management.</span></span>

## <a name="conclusion"></a><span data-ttu-id="e4009-591">Conclusion</span><span class="sxs-lookup"><span data-stu-id="e4009-591">Conclusion</span></span>

<span data-ttu-id="e4009-592">In this article, Contoso rebuilds the SmartHotel360 app in Azure.</span><span class="sxs-lookup"><span data-stu-id="e4009-592">In this article, Contoso rebuilds the SmartHotel360 app in Azure.</span></span> <span data-ttu-id="e4009-593">The on-premises app front-end VM is rebuilt to Azure App Services Web Apps.</span><span class="sxs-lookup"><span data-stu-id="e4009-593">The on-premises app front-end VM is rebuilt to Azure App Services Web Apps.</span></span> <span data-ttu-id="e4009-594">The app back end is built using microservices deployed to containers managed by Azure Kubernetes Service (AKS).</span><span class="sxs-lookup"><span data-stu-id="e4009-594">The app back end is built using microservices deployed to containers managed by Azure Kubernetes Service (AKS).</span></span> <span data-ttu-id="e4009-595">Contoso enhanced app functionality with a pet photo app.</span><span class="sxs-lookup"><span data-stu-id="e4009-595">Contoso enhanced app functionality with a pet photo app.</span></span>




