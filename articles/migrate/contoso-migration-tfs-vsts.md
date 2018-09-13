---
title: Refactor a Team Foundation Server deployment to Azure DevOps Services in Azure | Microsoft Docs
description: Learn how Contoso refactors its on-premises TFS deployment by migrating it to Azure DevOps Services in Azure.
services: site-recovery
author: rayne-wiselman
ms.service: site-recovery
ms.topic: conceptual
ms.date: 09/05/2018
ms.author: raynew
ms.openlocfilehash: a304cb08ec001587af5e6ea740853bd8435824e7
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965780"
---
# <a name="contoso-migration--refactor-a-team-foundation-server-deployment-to-azure-devops-services"></a><span data-ttu-id="1eb11-103">Contoso migration:  Refactor a Team Foundation Server deployment to Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="1eb11-103">Contoso migration:  Refactor a Team Foundation Server deployment to Azure DevOps Services</span></span>

<span data-ttu-id="1eb11-104">This article shows how Contoso are refactoring their on-premises Team Foundation Server (TFS) deployment by migrating it to Azure DevOps Services in Azure.</span><span class="sxs-lookup"><span data-stu-id="1eb11-104">This article shows how Contoso are refactoring their on-premises Team Foundation Server (TFS) deployment by migrating it to Azure DevOps Services in Azure.</span></span> <span data-ttu-id="1eb11-105">Contoso's development team have used TFS for team collaboration and source control for the past five years.</span><span class="sxs-lookup"><span data-stu-id="1eb11-105">Contoso's development team have used TFS for team collaboration and source control for the past five years.</span></span> <span data-ttu-id="1eb11-106">Now, they want to move to a cloud-based solution for dev and test work, and for source control.</span><span class="sxs-lookup"><span data-stu-id="1eb11-106">Now, they want to move to a cloud-based solution for dev and test work, and for source control.</span></span> <span data-ttu-id="1eb11-107">Azure DevOps Services will play a role as they move to an Azure DevOps model, and develop new cloud-native apps.</span><span class="sxs-lookup"><span data-stu-id="1eb11-107">Azure DevOps Services will play a role as they move to an Azure DevOps model, and develop new cloud-native apps.</span></span>

<span data-ttu-id="1eb11-108">This document is one in a series of articles that show how the fictitious company Contoso migrates its on-premises resources to the Microsoft Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="1eb11-108">This document is one in a series of articles that show how the fictitious company Contoso migrates its on-premises resources to the Microsoft Azure cloud.</span></span> <span data-ttu-id="1eb11-109">The series includes background information, and scenarios that illustrate how to set up a migration infrastructure, and run different types of migrations.</span><span class="sxs-lookup"><span data-stu-id="1eb11-109">The series includes background information, and scenarios that illustrate how to set up a migration infrastructure, and run different types of migrations.</span></span> <span data-ttu-id="1eb11-110">Scenarios grow in complexity.</span><span class="sxs-lookup"><span data-stu-id="1eb11-110">Scenarios grow in complexity.</span></span> <span data-ttu-id="1eb11-111">We'll add additional articles over time.</span><span class="sxs-lookup"><span data-stu-id="1eb11-111">We'll add additional articles over time.</span></span>

<span data-ttu-id="1eb11-112">**Article**</span><span class="sxs-lookup"><span data-stu-id="1eb11-112">**Article**</span></span> | <span data-ttu-id="1eb11-113">**Details**</span><span class="sxs-lookup"><span data-stu-id="1eb11-113">**Details**</span></span> | <span data-ttu-id="1eb11-114">**Status**</span><span class="sxs-lookup"><span data-stu-id="1eb11-114">**Status**</span></span>
--- | --- | ---
[<span data-ttu-id="1eb11-115">Article 1: Overview</span><span class="sxs-lookup"><span data-stu-id="1eb11-115">Article 1: Overview</span></span>](contoso-migration-overview.md) | <span data-ttu-id="1eb11-116">Provides an overview of Contoso's migration strategy, the article series, and the sample apps we use.</span><span class="sxs-lookup"><span data-stu-id="1eb11-116">Provides an overview of Contoso's migration strategy, the article series, and the sample apps we use.</span></span> | <span data-ttu-id="1eb11-117">Available</span><span class="sxs-lookup"><span data-stu-id="1eb11-117">Available</span></span>
[<span data-ttu-id="1eb11-118">Article 2: Deploy an Azure infrastructure</span><span class="sxs-lookup"><span data-stu-id="1eb11-118">Article 2: Deploy an Azure infrastructure</span></span>](contoso-migration-infrastructure.md) | <span data-ttu-id="1eb11-119">Describes how Contoso prepares its on-premises and Azure infrastructure for migration.</span><span class="sxs-lookup"><span data-stu-id="1eb11-119">Describes how Contoso prepares its on-premises and Azure infrastructure for migration.</span></span> <span data-ttu-id="1eb11-120">The same infrastructure is used for all Contoso migration scenarios.</span><span class="sxs-lookup"><span data-stu-id="1eb11-120">The same infrastructure is used for all Contoso migration scenarios.</span></span> | <span data-ttu-id="1eb11-121">Available</span><span class="sxs-lookup"><span data-stu-id="1eb11-121">Available</span></span>
[<span data-ttu-id="1eb11-122">Article 3: Assess on-premises resources</span><span class="sxs-lookup"><span data-stu-id="1eb11-122">Article 3: Assess on-premises resources</span></span>](contoso-migration-assessment.md)  | <span data-ttu-id="1eb11-123">Shows how Contoso runs an assessment of their on-premises two-tier SmartHotel app running on VMware.</span><span class="sxs-lookup"><span data-stu-id="1eb11-123">Shows how Contoso runs an assessment of their on-premises two-tier SmartHotel app running on VMware.</span></span> <span data-ttu-id="1eb11-124">They assess app VMs with the [Azure Migrate](migrate-overview.md) service, and the app SQL Server database with the [Azure Database Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017).</span><span class="sxs-lookup"><span data-stu-id="1eb11-124">They assess app VMs with the [Azure Migrate](migrate-overview.md) service, and the app SQL Server database with the [Azure Database Migration Assistant](https://docs.microsoft.com/sql/dma/dma-overview?view=sql-server-2017).</span></span> | <span data-ttu-id="1eb11-125">Available</span><span class="sxs-lookup"><span data-stu-id="1eb11-125">Available</span></span>
[<span data-ttu-id="1eb11-126">Article 4: Rehost to Azure VMs and a SQL Managed Instance</span><span class="sxs-lookup"><span data-stu-id="1eb11-126">Article 4: Rehost to Azure VMs and a SQL Managed Instance</span></span>](contoso-migration-rehost-vm-sql-managed-instance.md) | <span data-ttu-id="1eb11-127">Demonstrates how Contoso migrates the SmartHotel app to Azure.</span><span class="sxs-lookup"><span data-stu-id="1eb11-127">Demonstrates how Contoso migrates the SmartHotel app to Azure.</span></span> <span data-ttu-id="1eb11-128">They migrate the app web VM using [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview), and the app database using the [Azure Database Migration](https://docs.microsoft.com/azure/dms/dms-overview) service, to migrate to a SQL Managed Instance.</span><span class="sxs-lookup"><span data-stu-id="1eb11-128">They migrate the app web VM using [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview), and the app database using the [Azure Database Migration](https://docs.microsoft.com/azure/dms/dms-overview) service, to migrate to a SQL Managed Instance.</span></span> | <span data-ttu-id="1eb11-129">Available</span><span class="sxs-lookup"><span data-stu-id="1eb11-129">Available</span></span>
[<span data-ttu-id="1eb11-130">Article 5: Rehost to Azure VMs</span><span class="sxs-lookup"><span data-stu-id="1eb11-130">Article 5: Rehost to Azure VMs</span></span>](contoso-migration-rehost-vm.md) | <span data-ttu-id="1eb11-131">Shows how Contoso migrate their SmartHotel to Azure IaaS VMs, using the Site Recovery service.</span><span class="sxs-lookup"><span data-stu-id="1eb11-131">Shows how Contoso migrate their SmartHotel to Azure IaaS VMs, using the Site Recovery service.</span></span>
[<span data-ttu-id="1eb11-132">Article 6: Rehost to Azure VMs and SQL Server Availability Groups</span><span class="sxs-lookup"><span data-stu-id="1eb11-132">Article 6: Rehost to Azure VMs and SQL Server Availability Groups</span></span>](contoso-migration-rehost-vm-sql-ag.md) | <span data-ttu-id="1eb11-133">Shows how Contoso migrates the SmartHotel app.</span><span class="sxs-lookup"><span data-stu-id="1eb11-133">Shows how Contoso migrates the SmartHotel app.</span></span> <span data-ttu-id="1eb11-134">They use Site Recovery to migrate the app VMs, and the Database Migration service to migrate the app database to a SQL Server Availability Group.</span><span class="sxs-lookup"><span data-stu-id="1eb11-134">They use Site Recovery to migrate the app VMs, and the Database Migration service to migrate the app database to a SQL Server Availability Group.</span></span> | <span data-ttu-id="1eb11-135">Available</span><span class="sxs-lookup"><span data-stu-id="1eb11-135">Available</span></span>
[<span data-ttu-id="1eb11-136">Article 7: Rehost a Linux app to Azure VMs</span><span class="sxs-lookup"><span data-stu-id="1eb11-136">Article 7: Rehost a Linux app to Azure VMs</span></span>](contoso-migration-rehost-linux-vm.md) | <span data-ttu-id="1eb11-137">Shows how Contoso migrates their osTicket Linux app to Azure IaaS VMs using Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="1eb11-137">Shows how Contoso migrates their osTicket Linux app to Azure IaaS VMs using Azure Site Recovery.</span></span>
[<span data-ttu-id="1eb11-138">Article 8: Rehost a Linux app to Azure VMs and Azure MySQL Server</span><span class="sxs-lookup"><span data-stu-id="1eb11-138">Article 8: Rehost a Linux app to Azure VMs and Azure MySQL Server</span></span>](contoso-migration-rehost-linux-vm-mysql.md) | <span data-ttu-id="1eb11-139">Demonstrates how Contoso migrates the osTicket Linux app.</span><span class="sxs-lookup"><span data-stu-id="1eb11-139">Demonstrates how Contoso migrates the osTicket Linux app.</span></span> <span data-ttu-id="1eb11-140">They use Site Recovery for VM migration, and MySQL Workbench to migrate to an Azure MySQL Server instance.</span><span class="sxs-lookup"><span data-stu-id="1eb11-140">They use Site Recovery for VM migration, and MySQL Workbench to migrate to an Azure MySQL Server instance.</span></span> | <span data-ttu-id="1eb11-141">Available</span><span class="sxs-lookup"><span data-stu-id="1eb11-141">Available</span></span>
[<span data-ttu-id="1eb11-142">Article 9: Refactor an app to an Azure Web App and Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1eb11-142">Article 9: Refactor an app to an Azure Web App and Azure SQL Database</span></span>](contoso-migration-refactor-web-app-sql.md) | <span data-ttu-id="1eb11-143">Demonstrates how Contoso migrates the SmartHotel app to an Azure container-based web app, and migrates the app database to Azure SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1eb11-143">Demonstrates how Contoso migrates the SmartHotel app to an Azure container-based web app, and migrates the app database to Azure SQL Server.</span></span> | <span data-ttu-id="1eb11-144">Available</span><span class="sxs-lookup"><span data-stu-id="1eb11-144">Available</span></span>
[<span data-ttu-id="1eb11-145">Article 10: Refactor a Linux app to Azure App Service and Azure MySQL Server</span><span class="sxs-lookup"><span data-stu-id="1eb11-145">Article 10: Refactor a Linux app to Azure App Service and Azure MySQL Server</span></span>](contoso-migration-refactor-linux-app-service-mysql.md) | <span data-ttu-id="1eb11-146">Shows how Contoso migrates the osTicket Linux app to Azure App Service using PHP 7.0 Docker container.</span><span class="sxs-lookup"><span data-stu-id="1eb11-146">Shows how Contoso migrates the osTicket Linux app to Azure App Service using PHP 7.0 Docker container.</span></span> <span data-ttu-id="1eb11-147">The code base for the deployment is migrated to GitHub.</span><span class="sxs-lookup"><span data-stu-id="1eb11-147">The code base for the deployment is migrated to GitHub.</span></span> <span data-ttu-id="1eb11-148">The app database is migrated to Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="1eb11-148">The app database is migrated to Azure MySQL.</span></span> | <span data-ttu-id="1eb11-149">Available</span><span class="sxs-lookup"><span data-stu-id="1eb11-149">Available</span></span>
<span data-ttu-id="1eb11-150">Article 11: Refactor a TFS deployment in Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="1eb11-150">Article 11: Refactor a TFS deployment in Azure DevOps Services</span></span> | <span data-ttu-id="1eb11-151">Migrate the dev app TFS to Azure DevOps Services in Azure</span><span class="sxs-lookup"><span data-stu-id="1eb11-151">Migrate the dev app TFS to Azure DevOps Services in Azure</span></span> | <span data-ttu-id="1eb11-152">This article</span><span class="sxs-lookup"><span data-stu-id="1eb11-152">This article</span></span>
[<span data-ttu-id="1eb11-153">Article 12: Rearchitect an app on Azure containers and Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="1eb11-153">Article 12: Rearchitect an app on Azure containers and Azure SQL Database</span></span>](contoso-migration-rearchitect-container-sql.md) | <span data-ttu-id="1eb11-154">Shows how Contoso migrates and rearchitects their SmartHotel app to Azure.</span><span class="sxs-lookup"><span data-stu-id="1eb11-154">Shows how Contoso migrates and rearchitects their SmartHotel app to Azure.</span></span> <span data-ttu-id="1eb11-155">They rearchitect the app web tier as a Windows container, and the app database in an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="1eb11-155">They rearchitect the app web tier as a Windows container, and the app database in an Azure SQL Database.</span></span> | <span data-ttu-id="1eb11-156">Available</span><span class="sxs-lookup"><span data-stu-id="1eb11-156">Available</span></span>
[<span data-ttu-id="1eb11-157">Article 13: Rebuild an app in Azure</span><span class="sxs-lookup"><span data-stu-id="1eb11-157">Article 13: Rebuild an app in Azure</span></span>](contoso-migration-rebuild.md) | <span data-ttu-id="1eb11-158">Shows how Contoso rebuild their SmartHotel app using a range of Azure capabilities and services, including App Services, Azure Kubernetes, Azure Functions, Cognitive services, and Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="1eb11-158">Shows how Contoso rebuild their SmartHotel app using a range of Azure capabilities and services, including App Services, Azure Kubernetes, Azure Functions, Cognitive services, and Cosmos DB.</span></span> | <span data-ttu-id="1eb11-159">Available</span><span class="sxs-lookup"><span data-stu-id="1eb11-159">Available</span></span>


## <a name="business-drivers"></a><span data-ttu-id="1eb11-160">Business drivers</span><span class="sxs-lookup"><span data-stu-id="1eb11-160">Business drivers</span></span>

<span data-ttu-id="1eb11-161">The IT Leadership team has worked closely with business partners to identify future goals.</span><span class="sxs-lookup"><span data-stu-id="1eb11-161">The IT Leadership team has worked closely with business partners to identify future goals.</span></span> <span data-ttu-id="1eb11-162">Partners aren't overly concerned with dev tools and technologies, but they have captured these points:</span><span class="sxs-lookup"><span data-stu-id="1eb11-162">Partners aren't overly concerned with dev tools and technologies, but they have captured these points:</span></span>

- <span data-ttu-id="1eb11-163">**Software**: Regardless of the core business, all companies are now software companies, including Contoso.</span><span class="sxs-lookup"><span data-stu-id="1eb11-163">**Software**: Regardless of the core business, all companies are now software companies, including Contoso.</span></span> <span data-ttu-id="1eb11-164">Business leadership is interested in how IT can help lead the company with new working practices for users, and experiences for their customers.</span><span class="sxs-lookup"><span data-stu-id="1eb11-164">Business leadership is interested in how IT can help lead the company with new working practices for users, and experiences for their customers.</span></span>
- <span data-ttu-id="1eb11-165">**Efficiency**: Contoso needs to streamline process and remove unnecessary procedures for developers and users.</span><span class="sxs-lookup"><span data-stu-id="1eb11-165">**Efficiency**: Contoso needs to streamline process and remove unnecessary procedures for developers and users.</span></span> <span data-ttu-id="1eb11-166">This will allow the company to deliver on customer requirements more efficiently.</span><span class="sxs-lookup"><span data-stu-id="1eb11-166">This will allow the company to deliver on customer requirements more efficiently.</span></span> <span data-ttu-id="1eb11-167">The business needs IT to fast, without wasting time or money.</span><span class="sxs-lookup"><span data-stu-id="1eb11-167">The business needs IT to fast, without wasting time or money.</span></span>
- <span data-ttu-id="1eb11-168">**Agility**:  Contoso IT needs to respond to business needs, and react more quickly than the marketplace to enable success in a global economy.</span><span class="sxs-lookup"><span data-stu-id="1eb11-168">**Agility**:  Contoso IT needs to respond to business needs, and react more quickly than the marketplace to enable success in a global economy.</span></span> <span data-ttu-id="1eb11-169">IT mustn't be a blocker for the business.</span><span class="sxs-lookup"><span data-stu-id="1eb11-169">IT mustn't be a blocker for the business.</span></span>

## <a name="migration-goals"></a><span data-ttu-id="1eb11-170">Migration goals</span><span class="sxs-lookup"><span data-stu-id="1eb11-170">Migration goals</span></span>

<span data-ttu-id="1eb11-171">The Contoso cloud team has pinned down goals for the migration to Azure DevOps Services:</span><span class="sxs-lookup"><span data-stu-id="1eb11-171">The Contoso cloud team has pinned down goals for the migration to Azure DevOps Services:</span></span>

- <span data-ttu-id="1eb11-172">The team needs a tool to migrate the data to the cloud.</span><span class="sxs-lookup"><span data-stu-id="1eb11-172">The team needs a tool to migrate the data to the cloud.</span></span> <span data-ttu-id="1eb11-173">Few manual processes should be needed.</span><span class="sxs-lookup"><span data-stu-id="1eb11-173">Few manual processes should be needed.</span></span>
- <span data-ttu-id="1eb11-174">Work item data and history for the last year must be migrated.</span><span class="sxs-lookup"><span data-stu-id="1eb11-174">Work item data and history for the last year must be migrated.</span></span>
- <span data-ttu-id="1eb11-175">They don't want to set up new user names and passwords.</span><span class="sxs-lookup"><span data-stu-id="1eb11-175">They don't want to set up new user names and passwords.</span></span> <span data-ttu-id="1eb11-176">All current system assignments must be maintained.</span><span class="sxs-lookup"><span data-stu-id="1eb11-176">All current system assignments must be maintained.</span></span>
- <span data-ttu-id="1eb11-177">They want to move away from Team Foundation Version Control (TFVC) to Git for source control.</span><span class="sxs-lookup"><span data-stu-id="1eb11-177">They want to move away from Team Foundation Version Control (TFVC) to Git for source control.</span></span>
- <span data-ttu-id="1eb11-178">The cutover to Git will be a "tip migration" that imports only the latest version of the source code.</span><span class="sxs-lookup"><span data-stu-id="1eb11-178">The cutover to Git will be a "tip migration" that imports only the latest version of the source code.</span></span> <span data-ttu-id="1eb11-179">It will happen during a downtime when all work will be halted as the codebase shifts.</span><span class="sxs-lookup"><span data-stu-id="1eb11-179">It will happen during a downtime when all work will be halted as the codebase shifts.</span></span> <span data-ttu-id="1eb11-180">They understand that only the current master branch history will be available after the move.</span><span class="sxs-lookup"><span data-stu-id="1eb11-180">They understand that only the current master branch history will be available after the move.</span></span>
- <span data-ttu-id="1eb11-181">They're concerned about the change and want to test it before doing a full move.</span><span class="sxs-lookup"><span data-stu-id="1eb11-181">They're concerned about the change and want to test it before doing a full move.</span></span> <span data-ttu-id="1eb11-182">They want to retain access to TFS even after the move to Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="1eb11-182">They want to retain access to TFS even after the move to Azure DevOps Services.</span></span>
- <span data-ttu-id="1eb11-183">They have multiple collections, and want to start with one that has only a few projects to better understand the process.</span><span class="sxs-lookup"><span data-stu-id="1eb11-183">They have multiple collections, and want to start with one that has only a few projects to better understand the process.</span></span>
- <span data-ttu-id="1eb11-184">They understand that TFS collections are a one-to-one relationship with Azure DevOps Services organizations, so they'll have multiple URLs.</span><span class="sxs-lookup"><span data-stu-id="1eb11-184">They understand that TFS collections are a one-to-one relationship with Azure DevOps Services organizations, so they'll have multiple URLs.</span></span> <span data-ttu-id="1eb11-185">However, this matches their current model of separation for code bases and projects.</span><span class="sxs-lookup"><span data-stu-id="1eb11-185">However, this matches their current model of separation for code bases and projects.</span></span>


## <a name="proposed-architecture"></a><span data-ttu-id="1eb11-186">Proposed architecture</span><span class="sxs-lookup"><span data-stu-id="1eb11-186">Proposed architecture</span></span>

- <span data-ttu-id="1eb11-187">Contoso will move their TFS projects to the cloud, and no longer host their projects or source control on-premises.</span><span class="sxs-lookup"><span data-stu-id="1eb11-187">Contoso will move their TFS projects to the cloud, and no longer host their projects or source control on-premises.</span></span>
- <span data-ttu-id="1eb11-188">TFS will be migrated to Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="1eb11-188">TFS will be migrated to Azure DevOps Services.</span></span>
- <span data-ttu-id="1eb11-189">Currently Contoso has one TFS collection named **ContosoDev**, which will be migrated to an Azure DevOps Services organization called **contosodevmigration.visualstudio.com**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-189">Currently Contoso has one TFS collection named **ContosoDev**, which will be migrated to an Azure DevOps Services organization called **contosodevmigration.visualstudio.com**.</span></span>
- <span data-ttu-id="1eb11-190">The projects, work items, bugs and iterations from the last year will be migrated to Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="1eb11-190">The projects, work items, bugs and iterations from the last year will be migrated to Azure DevOps Services.</span></span>
- <span data-ttu-id="1eb11-191">Contoso will leverage their Azure Active Directory, which they set up when they [deployed their Azure infrastructure](contoso-migration-infrastructure.md) at the beginning of their migration planning.</span><span class="sxs-lookup"><span data-stu-id="1eb11-191">Contoso will leverage their Azure Active Directory, which they set up when they [deployed their Azure infrastructure](contoso-migration-infrastructure.md) at the beginning of their migration planning.</span></span> 


![Scenario architecture](./media/contoso-migration-tfs-vsts/architecture.png) 


## <a name="migration-process"></a><span data-ttu-id="1eb11-193">Migration process</span><span class="sxs-lookup"><span data-stu-id="1eb11-193">Migration process</span></span>

<span data-ttu-id="1eb11-194">Contoso will complete the migration process as follows:</span><span class="sxs-lookup"><span data-stu-id="1eb11-194">Contoso will complete the migration process as follows:</span></span>

1. <span data-ttu-id="1eb11-195">There's a lot of  preparation involved.</span><span class="sxs-lookup"><span data-stu-id="1eb11-195">There's a lot of  preparation involved.</span></span> <span data-ttu-id="1eb11-196">As a first step, Contoso needs to upgrade their TFS implementation to a supported level.</span><span class="sxs-lookup"><span data-stu-id="1eb11-196">As a first step, Contoso needs to upgrade their TFS implementation to a supported level.</span></span> <span data-ttu-id="1eb11-197">Contoso is currently running TFS 2017 Update 3, but to use database migration it needs to run a supported 2018 version with the latest updates.</span><span class="sxs-lookup"><span data-stu-id="1eb11-197">Contoso is currently running TFS 2017 Update 3, but to use database migration it needs to run a supported 2018 version with the latest updates.</span></span>
2. <span data-ttu-id="1eb11-198">After upgrading, Contoso will run the TFS migration tool, and validate their collection.</span><span class="sxs-lookup"><span data-stu-id="1eb11-198">After upgrading, Contoso will run the TFS migration tool, and validate their collection.</span></span>
3. <span data-ttu-id="1eb11-199">Contoso will build a set of preparation files, and perform a migration dry run for testing.</span><span class="sxs-lookup"><span data-stu-id="1eb11-199">Contoso will build a set of preparation files, and perform a migration dry run for testing.</span></span>
4. <span data-ttu-id="1eb11-200">Contoso will then run another migration, this time a full migration that includes work items, bugs, sprints, and code.</span><span class="sxs-lookup"><span data-stu-id="1eb11-200">Contoso will then run another migration, this time a full migration that includes work items, bugs, sprints, and code.</span></span>
5. <span data-ttu-id="1eb11-201">After the migration, Contoso will move their code from TFVC to Git.</span><span class="sxs-lookup"><span data-stu-id="1eb11-201">After the migration, Contoso will move their code from TFVC to Git.</span></span>

![Migration process](./media/contoso-migration-tfs-vsts/migration-process.png) 


## <a name="scenario-steps"></a><span data-ttu-id="1eb11-203">Scenario steps</span><span class="sxs-lookup"><span data-stu-id="1eb11-203">Scenario steps</span></span>

<span data-ttu-id="1eb11-204">Here's how Contoso will complete the migration:</span><span class="sxs-lookup"><span data-stu-id="1eb11-204">Here's how Contoso will complete the migration:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="1eb11-205">**Step 1: Create an Azure storage account**: This storage account will be used during the migration process.</span><span class="sxs-lookup"><span data-stu-id="1eb11-205">**Step 1: Create an Azure storage account**: This storage account will be used during the migration process.</span></span>
> * <span data-ttu-id="1eb11-206">**Step 2: Upgrade TFS**: Contoso will upgrade their deployment to TFS 2018 Upgrade 2.</span><span class="sxs-lookup"><span data-stu-id="1eb11-206">**Step 2: Upgrade TFS**: Contoso will upgrade their deployment to TFS 2018 Upgrade 2.</span></span> 
> * <span data-ttu-id="1eb11-207">**Step 3: Validate collection**: Contoso will validate the TFS collection in preparation for migration.</span><span class="sxs-lookup"><span data-stu-id="1eb11-207">**Step 3: Validate collection**: Contoso will validate the TFS collection in preparation for migration.</span></span>
> * <span data-ttu-id="1eb11-208">**Step 4: Build preparation file**: Contoso will create the migration files using the TFS Migration Tool.</span><span class="sxs-lookup"><span data-stu-id="1eb11-208">**Step 4: Build preparation file**: Contoso will create the migration files using the TFS Migration Tool.</span></span> 


## <a name="step-1-create-a-storage-account"></a><span data-ttu-id="1eb11-209">Step 1: Create a storage account</span><span class="sxs-lookup"><span data-stu-id="1eb11-209">Step 1: Create a storage account</span></span>

1. <span data-ttu-id="1eb11-210">In the Azure portal, Contoso admins create a storage account (**contosodevmigration**).</span><span class="sxs-lookup"><span data-stu-id="1eb11-210">In the Azure portal, Contoso admins create a storage account (**contosodevmigration**).</span></span>
2. <span data-ttu-id="1eb11-211">They place the account in their secondary region they use for failover - Central US.</span><span class="sxs-lookup"><span data-stu-id="1eb11-211">They place the account in their secondary region they use for failover - Central US.</span></span> <span data-ttu-id="1eb11-212">They use a general-purpose standard account with locally-redudant storage.</span><span class="sxs-lookup"><span data-stu-id="1eb11-212">They use a general-purpose standard account with locally-redudant storage.</span></span>

    ![Storage account](./media/contoso-migration-tfs-vsts/storage1.png) 


<span data-ttu-id="1eb11-214">**Need more help?**</span><span class="sxs-lookup"><span data-stu-id="1eb11-214">**Need more help?**</span></span>

- <span data-ttu-id="1eb11-215">[Introduction to Azure storage](https://docs.microsoft.com/azure/storage/common/storage-introduction).</span><span class="sxs-lookup"><span data-stu-id="1eb11-215">[Introduction to Azure storage](https://docs.microsoft.com/azure/storage/common/storage-introduction).</span></span>
- <span data-ttu-id="1eb11-216">[Create a storage account](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span><span class="sxs-lookup"><span data-stu-id="1eb11-216">[Create a storage account](https://docs.microsoft.com/azure/storage/common/storage-create-storage-account).</span></span>


## <a name="step-2-upgrade-tfs"></a><span data-ttu-id="1eb11-217">Step 2: Upgrade TFS</span><span class="sxs-lookup"><span data-stu-id="1eb11-217">Step 2: Upgrade TFS</span></span>

<span data-ttu-id="1eb11-218">Contoso admins upgrade the TFS server to TFS 2018 Update 2.</span><span class="sxs-lookup"><span data-stu-id="1eb11-218">Contoso admins upgrade the TFS server to TFS 2018 Update 2.</span></span> <span data-ttu-id="1eb11-219">Before they start:</span><span class="sxs-lookup"><span data-stu-id="1eb11-219">Before they start:</span></span>

- <span data-ttu-id="1eb11-220">They download [TFS 2018 Update 2](https://visualstudio.microsoft.com/downloads/)</span><span class="sxs-lookup"><span data-stu-id="1eb11-220">They download [TFS 2018 Update 2](https://visualstudio.microsoft.com/downloads/)</span></span>
- <span data-ttu-id="1eb11-221">They verify the [hardware requirements](https://docs.microsoft.com/tfs/server/requirements), and read through the [release notes](https://docs.microsoft.com/visualstudio/releasenotes/tfs2018-relnotes) and [upgrade gotchas](https://docs.microsoft.com/tfs/server/upgrade/get-started#before-you-upgrade-to-tfs-2018).</span><span class="sxs-lookup"><span data-stu-id="1eb11-221">They verify the [hardware requirements](https://docs.microsoft.com/tfs/server/requirements), and read through the [release notes](https://docs.microsoft.com/visualstudio/releasenotes/tfs2018-relnotes) and [upgrade gotchas](https://docs.microsoft.com/tfs/server/upgrade/get-started#before-you-upgrade-to-tfs-2018).</span></span>

<span data-ttu-id="1eb11-222">They upgrade as follows:</span><span class="sxs-lookup"><span data-stu-id="1eb11-222">They upgrade as follows:</span></span>

1. <span data-ttu-id="1eb11-223">To start, they back up their TFS server (running on a VMware vM) and take a VMware snapshot.</span><span class="sxs-lookup"><span data-stu-id="1eb11-223">To start, they back up their TFS server (running on a VMware vM) and take a VMware snapshot.</span></span>

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade1.png) 

2. <span data-ttu-id="1eb11-225">The TFS installer starts, and they choose the install location.</span><span class="sxs-lookup"><span data-stu-id="1eb11-225">The TFS installer starts, and they choose the install location.</span></span> <span data-ttu-id="1eb11-226">The installer needs internet access.</span><span class="sxs-lookup"><span data-stu-id="1eb11-226">The installer needs internet access.</span></span>

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade2.png) 

3. <span data-ttu-id="1eb11-228">After the installation finishes, the Server Configuration Wizard starts.</span><span class="sxs-lookup"><span data-stu-id="1eb11-228">After the installation finishes, the Server Configuration Wizard starts.</span></span>

    ![TFS](./media/contoso-migration-tfs-vsts/upgrade3.png) 

4. <span data-ttu-id="1eb11-230">After verification, the Wizard completes the upgrade.</span><span class="sxs-lookup"><span data-stu-id="1eb11-230">After verification, the Wizard completes the upgrade.</span></span>

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade4.png) 

5. <span data-ttu-id="1eb11-232">They verify the TFS installation by reviewing projects, work items, and code.</span><span class="sxs-lookup"><span data-stu-id="1eb11-232">They verify the TFS installation by reviewing projects, work items, and code.</span></span>

     ![TFS](./media/contoso-migration-tfs-vsts/upgrade5.png) 

> [!NOTE]
> <span data-ttu-id="1eb11-234">Some TFS upgrades need to run the Configure Features Wizard after the upgrade completes.</span><span class="sxs-lookup"><span data-stu-id="1eb11-234">Some TFS upgrades need to run the Configure Features Wizard after the upgrade completes.</span></span> <span data-ttu-id="1eb11-235">[Learn more](https://docs.microsoft.com/azure/devops/reference/configure-features-after-upgrade?utm_source=ms&utm_medium=guide&utm_campaign=vstsdataimportguide&view=vsts).</span><span class="sxs-lookup"><span data-stu-id="1eb11-235">[Learn more](https://docs.microsoft.com/azure/devops/reference/configure-features-after-upgrade?utm_source=ms&utm_medium=guide&utm_campaign=vstsdataimportguide&view=vsts).</span></span>

<span data-ttu-id="1eb11-236">**Need more help?**</span><span class="sxs-lookup"><span data-stu-id="1eb11-236">**Need more help?**</span></span>

<span data-ttu-id="1eb11-237">Learn about [upgrading TFS](https://docs.microsoft.com/tfs/server/upgrade/get-started).</span><span class="sxs-lookup"><span data-stu-id="1eb11-237">Learn about [upgrading TFS](https://docs.microsoft.com/tfs/server/upgrade/get-started).</span></span>

## <a name="step-3-validate-the-tfs-collection"></a><span data-ttu-id="1eb11-238">Step 3: Validate the TFS collection</span><span class="sxs-lookup"><span data-stu-id="1eb11-238">Step 3: Validate the TFS collection</span></span>

<span data-ttu-id="1eb11-239">Contoso admins run the TFS Migration Tool against the ContosoDev collection database to validate it before migration.</span><span class="sxs-lookup"><span data-stu-id="1eb11-239">Contoso admins run the TFS Migration Tool against the ContosoDev collection database to validate it before migration.</span></span>

1. <span data-ttu-id="1eb11-240">They download and unzip the [TFS Migration Tool](https://www.microsoft.com/download/details.aspx?id=54274).</span><span class="sxs-lookup"><span data-stu-id="1eb11-240">They download and unzip the [TFS Migration Tool](https://www.microsoft.com/download/details.aspx?id=54274).</span></span> <span data-ttu-id="1eb11-241">It's important to download the version for the TFS update that's running.</span><span class="sxs-lookup"><span data-stu-id="1eb11-241">It's important to download the version for the TFS update that's running.</span></span> <span data-ttu-id="1eb11-242">The version can be checked in the admin console.</span><span class="sxs-lookup"><span data-stu-id="1eb11-242">The version can be checked in the admin console.</span></span>

    ![TFS](./media/contoso-migration-tfs-vsts/collection1.png)

2. <span data-ttu-id="1eb11-244">They run the tool to perform the validation, by specifying the URL of the project collection:</span><span class="sxs-lookup"><span data-stu-id="1eb11-244">They run the tool to perform the validation, by specifying the URL of the project collection:</span></span>

        **TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev**


3. <span data-ttu-id="1eb11-245">The tool shows an error.</span><span class="sxs-lookup"><span data-stu-id="1eb11-245">The tool shows an error.</span></span>

    ![TFS](./media/contoso-migration-tfs-vsts/collection2.png)

5. <span data-ttu-id="1eb11-247">They located the log files are located in the **Logs** folder, just before the tool location.</span><span class="sxs-lookup"><span data-stu-id="1eb11-247">They located the log files are located in the **Logs** folder, just before the tool location.</span></span> <span data-ttu-id="1eb11-248">A log file is generated for each major validation.</span><span class="sxs-lookup"><span data-stu-id="1eb11-248">A log file is generated for each major validation.</span></span> <span data-ttu-id="1eb11-249">**TfsMigration.log** holds the main information.</span><span class="sxs-lookup"><span data-stu-id="1eb11-249">**TfsMigration.log** holds the main information.</span></span>

    ![TFS](./media/contoso-migration-tfs-vsts/collection3.png)

4. <span data-ttu-id="1eb11-251">They find this entry, related to identity.</span><span class="sxs-lookup"><span data-stu-id="1eb11-251">They find this entry, related to identity.</span></span>

    ![TFS](./media/contoso-migration-tfs-vsts/collection4.png)

5. <span data-ttu-id="1eb11-253">They run **TfsMigration validate /help** at the command line, and see that the command **/tenantDomainName** seems to be required to validate identities.</span><span class="sxs-lookup"><span data-stu-id="1eb11-253">They run **TfsMigration validate /help** at the command line, and see that the command **/tenantDomainName** seems to be required to validate identities.</span></span>

     ![TFS](./media/contoso-migration-tfs-vsts/collection5.png)

6. <span data-ttu-id="1eb11-255">They run the validation command again, and include this value, along with their Azure AD name: **TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-255">They run the validation command again, and include this value, along with their Azure AD name: **TfsMigrator validate /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com**.</span></span>

    ![TFS](./media/contoso-migration-tfs-vsts/collection7.png)

7. <span data-ttu-id="1eb11-257">An Azure AD Sign In screen appears, and they enter the credentials of a Global Admin user.</span><span class="sxs-lookup"><span data-stu-id="1eb11-257">An Azure AD Sign In screen appears, and they enter the credentials of a Global Admin user.</span></span>

     ![TFS](./media/contoso-migration-tfs-vsts/collection8.png)

8. <span data-ttu-id="1eb11-259">The validation passes, and is confirmed by the tool.</span><span class="sxs-lookup"><span data-stu-id="1eb11-259">The validation passes, and is confirmed by the tool.</span></span>

    ![TFS](./media/contoso-migration-tfs-vsts/collection9.png)



## <a name="step-4-create-the-migration-files"></a><span data-ttu-id="1eb11-261">Step 4: Create the migration files</span><span class="sxs-lookup"><span data-stu-id="1eb11-261">Step 4: Create the migration files</span></span>

<span data-ttu-id="1eb11-262">With the validation complete, Contoso admins can use the TFS Migration Tool to build the migration files.</span><span class="sxs-lookup"><span data-stu-id="1eb11-262">With the validation complete, Contoso admins can use the TFS Migration Tool to build the migration files.</span></span>

1. <span data-ttu-id="1eb11-263">They run the prepare step in the tool.</span><span class="sxs-lookup"><span data-stu-id="1eb11-263">They run the prepare step in the tool.</span></span>

    <span data-ttu-id="1eb11-264">**TfsMigrator prepare /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com /accountRegion:cus**</span><span class="sxs-lookup"><span data-stu-id="1eb11-264">**TfsMigrator prepare /collection:http://contosotfs:8080/tfs/ContosoDev /tenantDomainName:contosomigration.onmicrosoft.com /accountRegion:cus**</span></span>

     ![Prepare](./media/contoso-migration-tfs-vsts/prep1.png)

    <span data-ttu-id="1eb11-266">Prepare does the following:</span><span class="sxs-lookup"><span data-stu-id="1eb11-266">Prepare does the following:</span></span>
    - <span data-ttu-id="1eb11-267">Scans the collection to find a list of all users and populates the identify map log (**IdentityMapLog.csv**])</span><span class="sxs-lookup"><span data-stu-id="1eb11-267">Scans the collection to find a list of all users and populates the identify map log (**IdentityMapLog.csv**])</span></span>
    - <span data-ttu-id="1eb11-268">Prepares the connection to Azure Active Directory to find a match for each identity.</span><span class="sxs-lookup"><span data-stu-id="1eb11-268">Prepares the connection to Azure Active Directory to find a match for each identity.</span></span>
    - <span data-ttu-id="1eb11-269">Contoso has already deployed Azure AD and synchronized it using AD Connect, so Prepare should be able to find the matching identities and mark them as Active.</span><span class="sxs-lookup"><span data-stu-id="1eb11-269">Contoso has already deployed Azure AD and synchronized it using AD Connect, so Prepare should be able to find the matching identities and mark them as Active.</span></span>

2. <span data-ttu-id="1eb11-270">An Azure AD Sign In screen appears, and they enter the credentials of a Global Admin.</span><span class="sxs-lookup"><span data-stu-id="1eb11-270">An Azure AD Sign In screen appears, and they enter the credentials of a Global Admin.</span></span>

    ![Prepare](./media/contoso-migration-tfs-vsts/prep2.png)

3. <span data-ttu-id="1eb11-272">Prepare completes, and the tool reports that the import files have been generated successfully.</span><span class="sxs-lookup"><span data-stu-id="1eb11-272">Prepare completes, and the tool reports that the import files have been generated successfully.</span></span>

    ![Prepare](./media/contoso-migration-tfs-vsts/prep3.png)

4. <span data-ttu-id="1eb11-274">They can now see that both the IdentityMapLog.csv and the import.json file have been created in a new folder.</span><span class="sxs-lookup"><span data-stu-id="1eb11-274">They can now see that both the IdentityMapLog.csv and the import.json file have been created in a new folder.</span></span>

    ![Prepare](./media/contoso-migration-tfs-vsts/prep4.png)

5. <span data-ttu-id="1eb11-276">The import.json file provides import settings.</span><span class="sxs-lookup"><span data-stu-id="1eb11-276">The import.json file provides import settings.</span></span> <span data-ttu-id="1eb11-277">It includes information such as the desired organization name, and storage account information.</span><span class="sxs-lookup"><span data-stu-id="1eb11-277">It includes information such as the desired organization name, and storage account information.</span></span> <span data-ttu-id="1eb11-278">Most of the fields are populated automatically.</span><span class="sxs-lookup"><span data-stu-id="1eb11-278">Most of the fields are populated automatically.</span></span> <span data-ttu-id="1eb11-279">Some fields required user input.</span><span class="sxs-lookup"><span data-stu-id="1eb11-279">Some fields required user input.</span></span> <span data-ttu-id="1eb11-280">Contoso opens the file, and adds the Azure DevOps Services organization name to be created: **contosodevmigration**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-280">Contoso opens the file, and adds the Azure DevOps Services organization name to be created: **contosodevmigration**.</span></span> <span data-ttu-id="1eb11-281">With this name, their Azure DevOps Services URL will be **contosodevmigration.visualstudio.com**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-281">With this name, their Azure DevOps Services URL will be **contosodevmigration.visualstudio.com**.</span></span>

    ![Prepare](./media/contoso-migration-tfs-vsts/prep5.png)

    > [!NOTE]
    > <span data-ttu-id="1eb11-283">The organization must be created before the migration, It can be changed after migration is done.</span><span class="sxs-lookup"><span data-stu-id="1eb11-283">The organization must be created before the migration, It can be changed after migration is done.</span></span>

6. <span data-ttu-id="1eb11-284">They review the identity log map file that shows the accounts that will be brought into Azure DevOps Services during the import.</span><span class="sxs-lookup"><span data-stu-id="1eb11-284">They review the identity log map file that shows the accounts that will be brought into Azure DevOps Services during the import.</span></span> 

    - <span data-ttu-id="1eb11-285">Active identities refer to identities that will become users in Azure DevOps Services after the import.</span><span class="sxs-lookup"><span data-stu-id="1eb11-285">Active identities refer to identities that will become users in Azure DevOps Services after the import.</span></span>
    - <span data-ttu-id="1eb11-286">On Azure DevOps Services, these identities will be licensed, and show up as a user in the organization after migration.</span><span class="sxs-lookup"><span data-stu-id="1eb11-286">On Azure DevOps Services, these identities will be licensed, and show up as a user in the organization after migration.</span></span>
    - <span data-ttu-id="1eb11-287">These identities are marked as **Active** in the **Expected Import Status** column in the file.</span><span class="sxs-lookup"><span data-stu-id="1eb11-287">These identities are marked as **Active** in the **Expected Import Status** column in the file.</span></span>

    ![Prepare](./media/contoso-migration-tfs-vsts/prep6.png)



## <a name="step-5-migrate-to-azure-devops-services"></a><span data-ttu-id="1eb11-289">Step 5: Migrate to Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="1eb11-289">Step 5: Migrate to Azure DevOps Services</span></span>

<span data-ttu-id="1eb11-290">With preparation in place, Contoso admins can now focus on the migration.</span><span class="sxs-lookup"><span data-stu-id="1eb11-290">With preparation in place, Contoso admins can now focus on the migration.</span></span> <span data-ttu-id="1eb11-291">After running the migration, they'll switch from using TFVC to Git for version control.</span><span class="sxs-lookup"><span data-stu-id="1eb11-291">After running the migration, they'll switch from using TFVC to Git for version control.</span></span>

<span data-ttu-id="1eb11-292">Before they start, the admins schedule downtime with the dev team, to take the collection offline for migration.</span><span class="sxs-lookup"><span data-stu-id="1eb11-292">Before they start, the admins schedule downtime with the dev team, to take the collection offline for migration.</span></span> <span data-ttu-id="1eb11-293">These are the steps for the migration process:</span><span class="sxs-lookup"><span data-stu-id="1eb11-293">These are the steps for the migration process:</span></span>

1. <span data-ttu-id="1eb11-294">**Detach the collection**: Identity data for the collection resides in the TFS server configuration database while the collection is attached and online.</span><span class="sxs-lookup"><span data-stu-id="1eb11-294">**Detach the collection**: Identity data for the collection resides in the TFS server configuration database while the collection is attached and online.</span></span> <span data-ttu-id="1eb11-295">When a collection is detached from the TFS server, it takes a copy of that identity data, and packages it with the collection for transport.</span><span class="sxs-lookup"><span data-stu-id="1eb11-295">When a collection is detached from the TFS server, it takes a copy of that identity data, and packages it with the collection for transport.</span></span> <span data-ttu-id="1eb11-296">Without this data, the identity portion of the import cannot be executed.</span><span class="sxs-lookup"><span data-stu-id="1eb11-296">Without this data, the identity portion of the import cannot be executed.</span></span> <span data-ttu-id="1eb11-297">It's recommended that the collection stay detached until the import has been completed, as there's no way to import the changes which occurred during the import.</span><span class="sxs-lookup"><span data-stu-id="1eb11-297">It's recommended that the collection stay detached until the import has been completed, as there's no way to import the changes which occurred during the import.</span></span>
2. <span data-ttu-id="1eb11-298">**Generate a backup**: The next step of the migration process is to generate a backup that can be imported into Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="1eb11-298">**Generate a backup**: The next step of the migration process is to generate a backup that can be imported into Azure DevOps Services.</span></span> <span data-ttu-id="1eb11-299">Data-tier Application Component Packages (DACPAC), is a SQL Server feature that allows database changes to be packaged into a single file, and deployed to other instances of SQL.</span><span class="sxs-lookup"><span data-stu-id="1eb11-299">Data-tier Application Component Packages (DACPAC), is a SQL Server feature that allows database changes to be packaged into a single file, and deployed to other instances of SQL.</span></span> <span data-ttu-id="1eb11-300">It can also be restored directly to Azure DevOps Services, and is therefore used as the packaging method for getting collection data into the cloud.</span><span class="sxs-lookup"><span data-stu-id="1eb11-300">It can also be restored directly to Azure DevOps Services, and is therefore used as the packaging method for getting collection data into the cloud.</span></span> <span data-ttu-id="1eb11-301">Contoso will use the SqlPackage.exe tool to generate the DACPAC.</span><span class="sxs-lookup"><span data-stu-id="1eb11-301">Contoso will use the SqlPackage.exe tool to generate the DACPAC.</span></span> <span data-ttu-id="1eb11-302">This tool is included in SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="1eb11-302">This tool is included in SQL Server Data Tools.</span></span>
3. <span data-ttu-id="1eb11-303">**Upload to storage**: AFter the DACPAC is created, they upload it to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1eb11-303">**Upload to storage**: AFter the DACPAC is created, they upload it to Azure Storage.</span></span> <span data-ttu-id="1eb11-304">After it's uploaded, they get a shared access signature (SAS), to allow the TFS Migration Tool access to the storage.</span><span class="sxs-lookup"><span data-stu-id="1eb11-304">After it's uploaded, they get a shared access signature (SAS), to allow the TFS Migration Tool access to the storage.</span></span>
4. <span data-ttu-id="1eb11-305">**Fill out the import**: Contoso can then fill out missing fields in the import file, including the DACPAC setting.</span><span class="sxs-lookup"><span data-stu-id="1eb11-305">**Fill out the import**: Contoso can then fill out missing fields in the import file, including the DACPAC setting.</span></span> <span data-ttu-id="1eb11-306">To start with they'll specify that they want to do a **DryRun** import, to check that everything's working properly before the full migration.</span><span class="sxs-lookup"><span data-stu-id="1eb11-306">To start with they'll specify that they want to do a **DryRun** import, to check that everything's working properly before the full migration.</span></span>
5. <span data-ttu-id="1eb11-307">**Do a dry run**: Dry run imports help test collection migration.</span><span class="sxs-lookup"><span data-stu-id="1eb11-307">**Do a dry run**: Dry run imports help test collection migration.</span></span> <span data-ttu-id="1eb11-308">Dry runs have limited life, and are deleted before a production migration runs.</span><span class="sxs-lookup"><span data-stu-id="1eb11-308">Dry runs have limited life, and are deleted before a production migration runs.</span></span> <span data-ttu-id="1eb11-309">They're deleted automatically after a set period of time.</span><span class="sxs-lookup"><span data-stu-id="1eb11-309">They're deleted automatically after a set period of time.</span></span> <span data-ttu-id="1eb11-310">A note about when the dry run will be deleted is included in the success email received after the import finishes.</span><span class="sxs-lookup"><span data-stu-id="1eb11-310">A note about when the dry run will be deleted is included in the success email received after the import finishes.</span></span> <span data-ttu-id="1eb11-311">Take note and plan accordingly.</span><span class="sxs-lookup"><span data-stu-id="1eb11-311">Take note and plan accordingly.</span></span>
6. <span data-ttu-id="1eb11-312">**Complete the production migration**: With the Dry Run migration completed, Contoso admins do the final migration by updating the import.json, and running import again.</span><span class="sxs-lookup"><span data-stu-id="1eb11-312">**Complete the production migration**: With the Dry Run migration completed, Contoso admins do the final migration by updating the import.json, and running import again.</span></span>



### <a name="detach-the-collection"></a><span data-ttu-id="1eb11-313">Detach the collection</span><span class="sxs-lookup"><span data-stu-id="1eb11-313">Detach the collection</span></span>

<span data-ttu-id="1eb11-314">Before starting, Contoso admins take a local SQL Server backup, and VMware snapshot of the TFS server, before detaching.</span><span class="sxs-lookup"><span data-stu-id="1eb11-314">Before starting, Contoso admins take a local SQL Server backup, and VMware snapshot of the TFS server, before detaching.</span></span>

1.  <span data-ttu-id="1eb11-315">In the TFS Admin console, they select the collection they want to detach  (**ContosoDev**).</span><span class="sxs-lookup"><span data-stu-id="1eb11-315">In the TFS Admin console, they select the collection they want to detach  (**ContosoDev**).</span></span>

    ![Migrate](./media/contoso-migration-tfs-vsts/migrate1.png)

2. <span data-ttu-id="1eb11-317">In **General**, they select **Detach Collection**</span><span class="sxs-lookup"><span data-stu-id="1eb11-317">In **General**, they select **Detach Collection**</span></span>

    ![Migrate](./media/contoso-migration-tfs-vsts/migrate2.png)

3. <span data-ttu-id="1eb11-319">In the Detach Team Project Collection Wizard > **Servicing Message**, they provide a message for users who might try to connect to projects in the collection.</span><span class="sxs-lookup"><span data-stu-id="1eb11-319">In the Detach Team Project Collection Wizard > **Servicing Message**, they provide a message for users who might try to connect to projects in the collection.</span></span>

    ![Migrate](./media/contoso-migration-tfs-vsts/migrate3.png)

4. <span data-ttu-id="1eb11-321">In **Detach Progress**, they monitor progress and click **Next** when the process finishes.</span><span class="sxs-lookup"><span data-stu-id="1eb11-321">In **Detach Progress**, they monitor progress and click **Next** when the process finishes.</span></span>

    ![Migrate](./media/contoso-migration-tfs-vsts/migrate4.png)

5. <span data-ttu-id="1eb11-323">In **Readiness Checks**, when checks finish they click **Detach**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-323">In **Readiness Checks**, when checks finish they click **Detach**.</span></span>

    ![Migrate](./media/contoso-migration-tfs-vsts/migrate5.png)

6. <span data-ttu-id="1eb11-325">They click **Close** to finish up.</span><span class="sxs-lookup"><span data-stu-id="1eb11-325">They click **Close** to finish up.</span></span>

    ![Migrate](./media/contoso-migration-tfs-vsts/migrate6.png)

6. <span data-ttu-id="1eb11-327">The collection is no longer referenced in the TFS Admin console.</span><span class="sxs-lookup"><span data-stu-id="1eb11-327">The collection is no longer referenced in the TFS Admin console.</span></span>

    ![Migrate](./media/contoso-migration-tfs-vsts/migrate7.png)


### <a name="generate-a-dacpac"></a><span data-ttu-id="1eb11-329">Generate a DACPAC</span><span class="sxs-lookup"><span data-stu-id="1eb11-329">Generate a DACPAC</span></span>

<span data-ttu-id="1eb11-330">Contoso creates a backup (DACPAC) for import into Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="1eb11-330">Contoso creates a backup (DACPAC) for import into Azure DevOps Services.</span></span>

- <span data-ttu-id="1eb11-331">SqlPackage.exe in SQL Server Data Tools is used to create the DACPAC.</span><span class="sxs-lookup"><span data-stu-id="1eb11-331">SqlPackage.exe in SQL Server Data Tools is used to create the DACPAC.</span></span> <span data-ttu-id="1eb11-332">There are multiple versions of SqlPackage.exe installed with SQL Server Data Tools, located under folders with names such as 120, 130, and 140.</span><span class="sxs-lookup"><span data-stu-id="1eb11-332">There are multiple versions of SqlPackage.exe installed with SQL Server Data Tools, located under folders with names such as 120, 130, and 140.</span></span> <span data-ttu-id="1eb11-333">It's important to use the right version to prepare the DACPAC.</span><span class="sxs-lookup"><span data-stu-id="1eb11-333">It's important to use the right version to prepare the DACPAC.</span></span>
- <span data-ttu-id="1eb11-334">TFS 2018 imports need to use SqlPackage.exe from the 140 folder or higher.</span><span class="sxs-lookup"><span data-stu-id="1eb11-334">TFS 2018 imports need to use SqlPackage.exe from the 140 folder or higher.</span></span>  <span data-ttu-id="1eb11-335">For CONTOSOTFS, this file is located in folder: **C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Extensions\Microsoft\SQLDB\DAC\140**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-335">For CONTOSOTFS, this file is located in folder: **C:\Program Files (x86)\Microsoft Visual Studio\2017\Enterprise\Common7\IDE\Extensions\Microsoft\SQLDB\DAC\140**.</span></span>


<span data-ttu-id="1eb11-336">Contoso admins generate the DACPAC as follows:</span><span class="sxs-lookup"><span data-stu-id="1eb11-336">Contoso admins generate the DACPAC as follows:</span></span>

1. <span data-ttu-id="1eb11-337">They open a command prompt and navigate to the SQLPackage.exe location.</span><span class="sxs-lookup"><span data-stu-id="1eb11-337">They open a command prompt and navigate to the SQLPackage.exe location.</span></span> <span data-ttu-id="1eb11-338">They type this following command to generate the DACPAC:</span><span class="sxs-lookup"><span data-stu-id="1eb11-338">They type this following command to generate the DACPAC:</span></span>

    <span data-ttu-id="1eb11-339">**SqlPackage.exe /sourceconnectionstring:"Data Source=SQLSERVERNAME\INSTANCENAME;Initial Catalog=Tfs_ContosoDev;Integrated Security=True" /targetFile:C:\TFSMigrator\Tfs_ContosoDev.dacpac /action:extract /p:ExtractAllTableData=true /p:IgnoreUserLoginMappings=true /p:IgnorePermissions=true /p:Storage=Memory**</span><span class="sxs-lookup"><span data-stu-id="1eb11-339">**SqlPackage.exe /sourceconnectionstring:"Data Source=SQLSERVERNAME\INSTANCENAME;Initial Catalog=Tfs_ContosoDev;Integrated Security=True" /targetFile:C:\TFSMigrator\Tfs_ContosoDev.dacpac /action:extract /p:ExtractAllTableData=true /p:IgnoreUserLoginMappings=true /p:IgnorePermissions=true /p:Storage=Memory**</span></span> 

    ![Backup](./media/contoso-migration-tfs-vsts/backup1.png)

2. <span data-ttu-id="1eb11-341">The following message appears after the command runs.</span><span class="sxs-lookup"><span data-stu-id="1eb11-341">The following message appears after the command runs.</span></span>

    ![Backup](./media/contoso-migration-tfs-vsts/backup2.png)

3. <span data-ttu-id="1eb11-343">They verify the properties of the DACPACfile</span><span class="sxs-lookup"><span data-stu-id="1eb11-343">They verify the properties of the DACPACfile</span></span>

    ![Backup](./media/contoso-migration-tfs-vsts/backup3.png)

### <a name="update-the-file-to-storage"></a><span data-ttu-id="1eb11-345">Update the file to storage</span><span class="sxs-lookup"><span data-stu-id="1eb11-345">Update the file to storage</span></span>

<span data-ttu-id="1eb11-346">After the DACPAC is created, Contoso uploads it to Azure Storage.</span><span class="sxs-lookup"><span data-stu-id="1eb11-346">After the DACPAC is created, Contoso uploads it to Azure Storage.</span></span>

1. <span data-ttu-id="1eb11-347">They [download and install](https://azure.microsoft.com/features/storage-explorer/) Azure Storage Explorer.</span><span class="sxs-lookup"><span data-stu-id="1eb11-347">They [download and install](https://azure.microsoft.com/features/storage-explorer/) Azure Storage Explorer.</span></span>

    ![Upload](./media/contoso-migration-tfs-vsts/backup5.png)

4. <span data-ttu-id="1eb11-349">They connect to their subscription and locate the storage account they created for the migration (**contosodevmigration**).</span><span class="sxs-lookup"><span data-stu-id="1eb11-349">They connect to their subscription and locate the storage account they created for the migration (**contosodevmigration**).</span></span> <span data-ttu-id="1eb11-350">They create a new blob container, **azuredevopsmigration**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-350">They create a new blob container, **azuredevopsmigration**.</span></span>

    ![Upload](./media/contoso-migration-tfs-vsts/backup6.png)

5. <span data-ttu-id="1eb11-352">They specify the DACPAC file for upload as a block blob.</span><span class="sxs-lookup"><span data-stu-id="1eb11-352">They specify the DACPAC file for upload as a block blob.</span></span>

    ![Upload](./media/contoso-migration-tfs-vsts/backup7.png)
    
7. <span data-ttu-id="1eb11-354">After the file's uploaded, they click the file name > **Generate SAS**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-354">After the file's uploaded, they click the file name > **Generate SAS**.</span></span> <span data-ttu-id="1eb11-355">They expand the blob containers under the storage account, select the container with the import files, and click **Get Shared Access Signature**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-355">They expand the blob containers under the storage account, select the container with the import files, and click **Get Shared Access Signature**.</span></span>

    ![Upload](./media/contoso-migration-tfs-vsts/backup8.png)

8. <span data-ttu-id="1eb11-357">They accept the defaults and click **Create**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-357">They accept the defaults and click **Create**.</span></span> <span data-ttu-id="1eb11-358">This enables access for 24 hours.</span><span class="sxs-lookup"><span data-stu-id="1eb11-358">This enables access for 24 hours.</span></span>

    ![Upload](./media/contoso-migration-tfs-vsts/backup9.png)

9. <span data-ttu-id="1eb11-360">They copy the Shared Access Signature URL, so that it can be used by the TFS Migration Tool.</span><span class="sxs-lookup"><span data-stu-id="1eb11-360">They copy the Shared Access Signature URL, so that it can be used by the TFS Migration Tool.</span></span>

    ![Upload](./media/contoso-migration-tfs-vsts/backup10.png)

> [!NOTE]
> <span data-ttu-id="1eb11-362">The migration must happen before within the allowed time window or permissions will expire.</span><span class="sxs-lookup"><span data-stu-id="1eb11-362">The migration must happen before within the allowed time window or permissions will expire.</span></span>
> <span data-ttu-id="1eb11-363">Don't generate an SAS key from the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="1eb11-363">Don't generate an SAS key from the Azure portal.</span></span> <span data-ttu-id="1eb11-364">Keys generated like this are account-scoped, and won't work with the import.</span><span class="sxs-lookup"><span data-stu-id="1eb11-364">Keys generated like this are account-scoped, and won't work with the import.</span></span>

### <a name="fill-in-the-import-settings"></a><span data-ttu-id="1eb11-365">Fill in the import settings</span><span class="sxs-lookup"><span data-stu-id="1eb11-365">Fill in the import settings</span></span>

<span data-ttu-id="1eb11-366">Earlier, Contoso admins partially filled out the import specification file (import.json).</span><span class="sxs-lookup"><span data-stu-id="1eb11-366">Earlier, Contoso admins partially filled out the import specification file (import.json).</span></span> <span data-ttu-id="1eb11-367">Now, they need to add the remaining settings.</span><span class="sxs-lookup"><span data-stu-id="1eb11-367">Now, they need to add the remaining settings.</span></span>

<span data-ttu-id="1eb11-368">They open the import.json file, and fill out the following fields: •   Location: Location of the SAS key that was generated above.</span><span class="sxs-lookup"><span data-stu-id="1eb11-368">They open the import.json file, and fill out the following fields: •   Location: Location of the SAS key that was generated above.</span></span>
<span data-ttu-id="1eb11-369">•   Dacpac: Set the name to the DACPAC file you uploaded to the storage account.</span><span class="sxs-lookup"><span data-stu-id="1eb11-369">•   Dacpac: Set the name to the DACPAC file you uploaded to the storage account.</span></span> <span data-ttu-id="1eb11-370">Include the ".dacpac" extension.</span><span class="sxs-lookup"><span data-stu-id="1eb11-370">Include the ".dacpac" extension.</span></span>
<span data-ttu-id="1eb11-371">•   ImportType: Set to DryRun for now.</span><span class="sxs-lookup"><span data-stu-id="1eb11-371">•   ImportType: Set to DryRun for now.</span></span>


![Import settings](./media/contoso-migration-tfs-vsts/import1.png)


### <a name="do-a-dry-run-migration"></a><span data-ttu-id="1eb11-373">Do a dry run migration</span><span class="sxs-lookup"><span data-stu-id="1eb11-373">Do a dry run migration</span></span>

<span data-ttu-id="1eb11-374">Contoso admins start with a dry run migration, to make sure everything's working as expected.</span><span class="sxs-lookup"><span data-stu-id="1eb11-374">Contoso admins start with a dry run migration, to make sure everything's working as expected.</span></span>

1. <span data-ttu-id="1eb11-375">They open a command prompt, and locate to the TfsMigration location (C:\TFSMigrator).</span><span class="sxs-lookup"><span data-stu-id="1eb11-375">They open a command prompt, and locate to the TfsMigration location (C:\TFSMigrator).</span></span>
2. <span data-ttu-id="1eb11-376">As a first step they validate the import file.</span><span class="sxs-lookup"><span data-stu-id="1eb11-376">As a first step they validate the import file.</span></span> <span data-ttu-id="1eb11-377">They want to be sure the file is formatted properly, and that the SAS key is working.</span><span class="sxs-lookup"><span data-stu-id="1eb11-377">They want to be sure the file is formatted properly, and that the SAS key is working.</span></span>

    <span data-ttu-id="1eb11-378">**TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly**</span><span class="sxs-lookup"><span data-stu-id="1eb11-378">**TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly**</span></span>

3. <span data-ttu-id="1eb11-379">The validation returns an error that the SAS key needs a longer expiry time.</span><span class="sxs-lookup"><span data-stu-id="1eb11-379">The validation returns an error that the SAS key needs a longer expiry time.</span></span>

    ![Dry run](./media/contoso-migration-tfs-vsts/test1.png)

3. <span data-ttu-id="1eb11-381">They use Azure Storage Explorer to create a new SAS key with expiry set to seven days.</span><span class="sxs-lookup"><span data-stu-id="1eb11-381">They use Azure Storage Explorer to create a new SAS key with expiry set to seven days.</span></span>

    ![Dry run](./media/contoso-migration-tfs-vsts/test2.png)

3. <span data-ttu-id="1eb11-383">They update the import.json file and run the validation again.</span><span class="sxs-lookup"><span data-stu-id="1eb11-383">They update the import.json file and run the validation again.</span></span> <span data-ttu-id="1eb11-384">This time it completes successfully.</span><span class="sxs-lookup"><span data-stu-id="1eb11-384">This time it completes successfully.</span></span>

    <span data-ttu-id="1eb11-385">**TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly**</span><span class="sxs-lookup"><span data-stu-id="1eb11-385">**TfsMigrator import /importFile:C:\TFSMigrator\import.json /validateonly**</span></span>

    ![Dry run](./media/contoso-migration-tfs-vsts/test3.png)
    
7. <span data-ttu-id="1eb11-387">They start the dry run:</span><span class="sxs-lookup"><span data-stu-id="1eb11-387">They start the dry run:</span></span>

    <span data-ttu-id="1eb11-388">**TfsMigrator import /importFile:C:\TFSMigrator\import.json**</span><span class="sxs-lookup"><span data-stu-id="1eb11-388">**TfsMigrator import /importFile:C:\TFSMigrator\import.json**</span></span>

8. <span data-ttu-id="1eb11-389">A message is issued to confirm the migration.</span><span class="sxs-lookup"><span data-stu-id="1eb11-389">A message is issued to confirm the migration.</span></span> <span data-ttu-id="1eb11-390">Note the length of time for which the staged data will be maintained after the dry run.</span><span class="sxs-lookup"><span data-stu-id="1eb11-390">Note the length of time for which the staged data will be maintained after the dry run.</span></span>

    ![Dry run](./media/contoso-migration-tfs-vsts/test4.png)

9. <span data-ttu-id="1eb11-392">Azure AD Sign In appears, and should be completing with Contoso Admin sign-in.</span><span class="sxs-lookup"><span data-stu-id="1eb11-392">Azure AD Sign In appears, and should be completing with Contoso Admin sign-in.</span></span>

    ![Dry run](./media/contoso-migration-tfs-vsts/test5.png)

10. <span data-ttu-id="1eb11-394">A message shows information about the import.</span><span class="sxs-lookup"><span data-stu-id="1eb11-394">A message shows information about the import.</span></span>

    ![Dry run](./media/contoso-migration-tfs-vsts/test6.png)

11. <span data-ttu-id="1eb11-396">After 15 minutes or so, they browse to the URL, and see the following information:</span><span class="sxs-lookup"><span data-stu-id="1eb11-396">After 15 minutes or so, they browse to the URL, and see the following information:</span></span>

     ![Dry run](./media/contoso-migration-tfs-vsts/test7.png)

12. <span data-ttu-id="1eb11-398">After the migration finishes a Contoso Dev Leads signs into Azure DevOps Services to check that the dry run worked properly.</span><span class="sxs-lookup"><span data-stu-id="1eb11-398">After the migration finishes a Contoso Dev Leads signs into Azure DevOps Services to check that the dry run worked properly.</span></span> <span data-ttu-id="1eb11-399">After authentication, Azure DevOps Services needs a few details to confirm the organization.</span><span class="sxs-lookup"><span data-stu-id="1eb11-399">After authentication, Azure DevOps Services needs a few details to confirm the organization.</span></span>

    ![Dry run](./media/contoso-migration-tfs-vsts/test8.png)

13. <span data-ttu-id="1eb11-401">In Azure DevOps Services, the Dev Lead can see that the projects have been migrated to Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="1eb11-401">In Azure DevOps Services, the Dev Lead can see that the projects have been migrated to Azure DevOps Services.</span></span> <span data-ttu-id="1eb11-402">There's a notice that the organization will be deleted in 15 days.</span><span class="sxs-lookup"><span data-stu-id="1eb11-402">There's a notice that the organization will be deleted in 15 days.</span></span>

    ![Dry run](./media/contoso-migration-tfs-vsts/test9.png)

14. <span data-ttu-id="1eb11-404">The Dev Lead opens one of the projects and opens **Work Items** > **Assigned to me**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-404">The Dev Lead opens one of the projects and opens **Work Items** > **Assigned to me**.</span></span> <span data-ttu-id="1eb11-405">This shows that work item data has been migrated, along with identity.</span><span class="sxs-lookup"><span data-stu-id="1eb11-405">This shows that work item data has been migrated, along with identity.</span></span>

    ![Dry run](./media/contoso-migration-tfs-vsts/test10.png)

15. <span data-ttu-id="1eb11-407">The lead also checks other projects and code, to confirm that the source code and history has been migrated.</span><span class="sxs-lookup"><span data-stu-id="1eb11-407">The lead also checks other projects and code, to confirm that the source code and history has been migrated.</span></span>

    ![Dry run](./media/contoso-migration-tfs-vsts/test11.png)


### <a name="run-the-production-migration"></a><span data-ttu-id="1eb11-409">Run the production migration</span><span class="sxs-lookup"><span data-stu-id="1eb11-409">Run the production migration</span></span>

<span data-ttu-id="1eb11-410">With the dry run complete, Contoso admins move on to the production migration.</span><span class="sxs-lookup"><span data-stu-id="1eb11-410">With the dry run complete, Contoso admins move on to the production migration.</span></span> <span data-ttu-id="1eb11-411">They delete the dry run, update the import settings, and run import again.</span><span class="sxs-lookup"><span data-stu-id="1eb11-411">They delete the dry run, update the import settings, and run import again.</span></span>

1. <span data-ttu-id="1eb11-412">In the Azure DevOps Services portal, they delete the dry run organization.</span><span class="sxs-lookup"><span data-stu-id="1eb11-412">In the Azure DevOps Services portal, they delete the dry run organization.</span></span>
2. <span data-ttu-id="1eb11-413">They update the import.json file to set the **ImportType** to **ProductionRun**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-413">They update the import.json file to set the **ImportType** to **ProductionRun**.</span></span>

    ![Production](./media/contoso-migration-tfs-vsts/full1.png)

3. <span data-ttu-id="1eb11-415">They start the migration as they did for the dry run: **TfsMigrator import /importFile:C:\TFSMigrator\import.json**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-415">They start the migration as they did for the dry run: **TfsMigrator import /importFile:C:\TFSMigrator\import.json**.</span></span>
4. <span data-ttu-id="1eb11-416">A message shows to confirm the migration, and warns that data could be held in a secure location as a staging area for up to seven days.</span><span class="sxs-lookup"><span data-stu-id="1eb11-416">A message shows to confirm the migration, and warns that data could be held in a secure location as a staging area for up to seven days.</span></span>

    ![Production](./media/contoso-migration-tfs-vsts/full2.png)

5. <span data-ttu-id="1eb11-418">In Azure AD Sign In, they specify a Contoso Admin sign-in.</span><span class="sxs-lookup"><span data-stu-id="1eb11-418">In Azure AD Sign In, they specify a Contoso Admin sign-in.</span></span>

    ![Production](./media/contoso-migration-tfs-vsts/full3.png)

6. <span data-ttu-id="1eb11-420">A message shows information about the import.</span><span class="sxs-lookup"><span data-stu-id="1eb11-420">A message shows information about the import.</span></span>

    ![Production](./media/contoso-migration-tfs-vsts/full4.png)

7. <span data-ttu-id="1eb11-422">After around 15 minutes, they browse to the URL, and sees the following information:</span><span class="sxs-lookup"><span data-stu-id="1eb11-422">After around 15 minutes, they browse to the URL, and sees the following information:</span></span>

    ![Production](./media/contoso-migration-tfs-vsts/full5.png)

8. <span data-ttu-id="1eb11-424">After the migration finishes, a Contoso Dev Lead logs onto Azure DevOps Services to check that the migration worked properly.</span><span class="sxs-lookup"><span data-stu-id="1eb11-424">After the migration finishes, a Contoso Dev Lead logs onto Azure DevOps Services to check that the migration worked properly.</span></span> <span data-ttu-id="1eb11-425">After login, he can see that projects have been migrated.</span><span class="sxs-lookup"><span data-stu-id="1eb11-425">After login, he can see that projects have been migrated.</span></span>

    ![Production](./media/contoso-migration-tfs-vsts/full6.png)

8. <span data-ttu-id="1eb11-427">The Dev Lead opens one of the projects and opens **Work Items** > **Assigned to me**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-427">The Dev Lead opens one of the projects and opens **Work Items** > **Assigned to me**.</span></span> <span data-ttu-id="1eb11-428">This shows that work item data has been migrated, along with identity.</span><span class="sxs-lookup"><span data-stu-id="1eb11-428">This shows that work item data has been migrated, along with identity.</span></span>

    ![Production](./media/contoso-migration-tfs-vsts/full7.png)

9. <span data-ttu-id="1eb11-430">The lead checks other work item data to confirm.</span><span class="sxs-lookup"><span data-stu-id="1eb11-430">The lead checks other work item data to confirm.</span></span>

    ![Production](./media/contoso-migration-tfs-vsts/full8.png)

15. <span data-ttu-id="1eb11-432">The lead also checks other projects and code, to confirm that the source code and history has been migrated.</span><span class="sxs-lookup"><span data-stu-id="1eb11-432">The lead also checks other projects and code, to confirm that the source code and history has been migrated.</span></span>

    ![Production](./media/contoso-migration-tfs-vsts/full9.png)


### <a name="move-source-control-from-tfvc-to-git"></a><span data-ttu-id="1eb11-434">Move source control from TFVC to GIT</span><span class="sxs-lookup"><span data-stu-id="1eb11-434">Move source control from TFVC to GIT</span></span>

<span data-ttu-id="1eb11-435">With migration complete, Contoso wants to move from TFVC to Git for source code management.</span><span class="sxs-lookup"><span data-stu-id="1eb11-435">With migration complete, Contoso wants to move from TFVC to Git for source code management.</span></span> <span data-ttu-id="1eb11-436">They need to import the source code currently in their Azure DevOps Services organization as Git repos in the same organization.</span><span class="sxs-lookup"><span data-stu-id="1eb11-436">They need to import the source code currently in their Azure DevOps Services organization as Git repos in the same organization.</span></span>

1. <span data-ttu-id="1eb11-437">In the Azure DevOps Services portal, they open one of the TFVC repos (**$/PolicyConnect**) and review it.</span><span class="sxs-lookup"><span data-stu-id="1eb11-437">In the Azure DevOps Services portal, they open one of the TFVC repos (**$/PolicyConnect**) and review it.</span></span>

    ![Git](./media/contoso-migration-tfs-vsts/git1.png)

2. <span data-ttu-id="1eb11-439">They click the **Source** dropdown > **Import**.</span><span class="sxs-lookup"><span data-stu-id="1eb11-439">They click the **Source** dropdown > **Import**.</span></span>

    ![Git](./media/contoso-migration-tfs-vsts/git2.png)

3. <span data-ttu-id="1eb11-441">In **Source type** they select **TFVC**, and specify the path to the repo.</span><span class="sxs-lookup"><span data-stu-id="1eb11-441">In **Source type** they select **TFVC**, and specify the path to the repo.</span></span> <span data-ttu-id="1eb11-442">They've decided not to migrate the history.</span><span class="sxs-lookup"><span data-stu-id="1eb11-442">They've decided not to migrate the history.</span></span>

    ![Git](./media/contoso-migration-tfs-vsts/git3.png)

    > [!NOTE]
    > <span data-ttu-id="1eb11-444">Due to differences in how TFVC and Git store version control information, we recommend that Contoso don't migrate history.</span><span class="sxs-lookup"><span data-stu-id="1eb11-444">Due to differences in how TFVC and Git store version control information, we recommend that Contoso don't migrate history.</span></span> <span data-ttu-id="1eb11-445">This is the approach that Microsoft took when it migrated Windows and other products from centralized version control to Git.</span><span class="sxs-lookup"><span data-stu-id="1eb11-445">This is the approach that Microsoft took when it migrated Windows and other products from centralized version control to Git.</span></span>

4. <span data-ttu-id="1eb11-446">After the import, admins review the code.</span><span class="sxs-lookup"><span data-stu-id="1eb11-446">After the import, admins review the code.</span></span>

    ![Git](./media/contoso-migration-tfs-vsts/git4.png)

5. <span data-ttu-id="1eb11-448">They repeat the process for the second repository (**$/SmartHotelContainer**).</span><span class="sxs-lookup"><span data-stu-id="1eb11-448">They repeat the process for the second repository (**$/SmartHotelContainer**).</span></span>

    ![Git](./media/contoso-migration-tfs-vsts/git5.png)

6. <span data-ttu-id="1eb11-450">After reviewing the source, the Dev Leads agree that the migration to Azure DevOps Services is done.</span><span class="sxs-lookup"><span data-stu-id="1eb11-450">After reviewing the source, the Dev Leads agree that the migration to Azure DevOps Services is done.</span></span> <span data-ttu-id="1eb11-451">Azure DevOps Services now becomes the source for all development within teams involved in the migration.</span><span class="sxs-lookup"><span data-stu-id="1eb11-451">Azure DevOps Services now becomes the source for all development within teams involved in the migration.</span></span>

    ![Git](./media/contoso-migration-tfs-vsts/git6.png)



<span data-ttu-id="1eb11-453">**Need more help?**</span><span class="sxs-lookup"><span data-stu-id="1eb11-453">**Need more help?**</span></span>

<span data-ttu-id="1eb11-454">[Learn more](https://docs.microsoft.com/azure/devops/repos/git/import-from-TFVC?view=vsts) about importing from TFVC.</span><span class="sxs-lookup"><span data-stu-id="1eb11-454">[Learn more](https://docs.microsoft.com/azure/devops/repos/git/import-from-TFVC?view=vsts) about importing from TFVC.</span></span>

##  <a name="clean-up-after-migration"></a><span data-ttu-id="1eb11-455">Clean up after migration</span><span class="sxs-lookup"><span data-stu-id="1eb11-455">Clean up after migration</span></span>

<span data-ttu-id="1eb11-456">With migration complete, Contoso needs to do the following:</span><span class="sxs-lookup"><span data-stu-id="1eb11-456">With migration complete, Contoso needs to do the following:</span></span>

- <span data-ttu-id="1eb11-457">Review the [post-import](https://docs.microsoft.com/azure/devops/articles/migration-post-import?view=vsts) article for information about additional import activities.</span><span class="sxs-lookup"><span data-stu-id="1eb11-457">Review the [post-import](https://docs.microsoft.com/azure/devops/articles/migration-post-import?view=vsts) article for information about additional import activities.</span></span>
- <span data-ttu-id="1eb11-458">Either delete the TFVC repos, or place them in read-only mode.</span><span class="sxs-lookup"><span data-stu-id="1eb11-458">Either delete the TFVC repos, or place them in read-only mode.</span></span> <span data-ttu-id="1eb11-459">The code bases mustn't used, but can be referenced for their history.</span><span class="sxs-lookup"><span data-stu-id="1eb11-459">The code bases mustn't used, but can be referenced for their history.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1eb11-460">Next steps</span><span class="sxs-lookup"><span data-stu-id="1eb11-460">Next steps</span></span>

<span data-ttu-id="1eb11-461">Contoso will need to provide Azure DevOps Services and Git training for relevant team members.</span><span class="sxs-lookup"><span data-stu-id="1eb11-461">Contoso will need to provide Azure DevOps Services and Git training for relevant team members.</span></span>



