---
title: Rearchitect a Contoso app in an Azure container and Azure SQL Database | Microsoft Docs
description: Learn how Contoso rearchitect an app in Azure Windows containers and Azure SQL Database.
services: site-recovery
author: rayne-wiselman
ms.service: site-recovery
ms.topic: conceptual
ms.date: 09/05/2018
ms.author: raynew
ms.openlocfilehash: 00a0f396160c964144019b4cb8014f8abc34fe7a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866400"
---
# <a name="contoso-migration-rearchitect-an-on-premises-app-to-an-azure-container-and-azure-sql-database"></a><span data-ttu-id="c2076-103">Contoso migration: Rearchitect an on-premises app to an Azure container and Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c2076-103">Contoso migration: Rearchitect an on-premises app to an Azure container and Azure SQL Database</span></span>

<span data-ttu-id="c2076-104">This article demonstrates how Contoso migrates and rearchitect its SmartHotel360 app in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2076-104">This article demonstrates how Contoso migrates and rearchitect its SmartHotel360 app in Azure.</span></span> <span data-ttu-id="c2076-105">Contoso migrates the app frontend VM to an Azure Windows container, and the app database to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c2076-105">Contoso migrates the app frontend VM to an Azure Windows container, and the app database to an Azure SQL database.</span></span>

<span data-ttu-id="c2076-106">This document is one in a series of articles that show how the fictitious company Contoso migrates on-premises resources to the Microsoft Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="c2076-106">This document is one in a series of articles that show how the fictitious company Contoso migrates on-premises resources to the Microsoft Azure cloud.</span></span> <span data-ttu-id="c2076-107">The series includes background information, and scenarios that illustrate setting up a migration infrastructure, assessing on-premises resources for migration, and running different types of migrations.</span><span class="sxs-lookup"><span data-stu-id="c2076-107">The series includes background information, and scenarios that illustrate setting up a migration infrastructure, assessing on-premises resources for migration, and running different types of migrations.</span></span> <span data-ttu-id="c2076-108">Scenarios grow in complexity.</span><span class="sxs-lookup"><span data-stu-id="c2076-108">Scenarios grow in complexity.</span></span> <span data-ttu-id="c2076-109">Additional articles will be added over time.</span><span class="sxs-lookup"><span data-stu-id="c2076-109">Additional articles will be added over time.</span></span>

<span data-ttu-id="c2076-110">**Article**</span><span class="sxs-lookup"><span data-stu-id="c2076-110">**Article**</span></span> | <span data-ttu-id="c2076-111">**Details**</span><span class="sxs-lookup"><span data-stu-id="c2076-111">**Details**</span></span> | <span data-ttu-id="c2076-112">**Status**</span><span class="sxs-lookup"><span data-stu-id="c2076-112">**Status**</span></span>
--- | --- | ---
[<span data-ttu-id="c2076-113">Article 1: Overview</span><span class="sxs-lookup"><span data-stu-id="c2076-113">Article 1: Overview</span></span>](contoso-migration-overview.md) | <span data-ttu-id="c2076-114">Overview of the article series, Contoso's migration strategy, and the sample apps that are used in the series.</span><span class="sxs-lookup"><span data-stu-id="c2076-114">Overview of the article series, Contoso's migration strategy, and the sample apps that are used in the series.</span></span> | <span data-ttu-id="c2076-115">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-115">Available</span></span>
[<span data-ttu-id="c2076-116">Article 2: Deploy Azure infrastructure</span><span class="sxs-lookup"><span data-stu-id="c2076-116">Article 2: Deploy Azure infrastructure</span></span>](contoso-migration-infrastructure.md) | <span data-ttu-id="c2076-117">Contoso prepares its on-premises infrastructure and its Azure infrastructure for migration.</span><span class="sxs-lookup"><span data-stu-id="c2076-117">Contoso prepares its on-premises infrastructure and its Azure infrastructure for migration.</span></span> <span data-ttu-id="c2076-118">The same infrastructure is used for all migration articles in the series.</span><span class="sxs-lookup"><span data-stu-id="c2076-118">The same infrastructure is used for all migration articles in the series.</span></span> | <span data-ttu-id="c2076-119">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-119">Available</span></span>
[<span data-ttu-id="c2076-120">Article 3: Assess on-premises resources for migration to Azure</span><span class="sxs-lookup"><span data-stu-id="c2076-120">Article 3: Assess on-premises resources for migration to Azure</span></span>](contoso-migration-assessment.md)  | <span data-ttu-id="c2076-121">Contoso runs an assessment of its on-premises SmartHotel360 app running on VMware.</span><span class="sxs-lookup"><span data-stu-id="c2076-121">Contoso runs an assessment of its on-premises SmartHotel360 app running on VMware.</span></span> <span data-ttu-id="c2076-122">Contoso assesses app VMs using the Azure Migrate service, and the app SQL Server database using Data Migration Assistant.</span><span class="sxs-lookup"><span data-stu-id="c2076-122">Contoso assesses app VMs using the Azure Migrate service, and the app SQL Server database using Data Migration Assistant.</span></span> | <span data-ttu-id="c2076-123">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-123">Available</span></span>
[<span data-ttu-id="c2076-124">Article 4: Rehost an app on an Azure VM and SQL Database Managed Instance</span><span class="sxs-lookup"><span data-stu-id="c2076-124">Article 4: Rehost an app on an Azure VM and SQL Database Managed Instance</span></span>](contoso-migration-rehost-vm-sql-managed-instance.md) | <span data-ttu-id="c2076-125">Contoso runs a lift-and-shift migration to Azure for its on-premises SmartHotel360 app.</span><span class="sxs-lookup"><span data-stu-id="c2076-125">Contoso runs a lift-and-shift migration to Azure for its on-premises SmartHotel360 app.</span></span> <span data-ttu-id="c2076-126">Contoso migrates the app front-end VM using [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview).</span><span class="sxs-lookup"><span data-stu-id="c2076-126">Contoso migrates the app front-end VM using [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview).</span></span> <span data-ttu-id="c2076-127">Contoso migrates the app database to an Azure SQL Database Managed Instance using the [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).</span><span class="sxs-lookup"><span data-stu-id="c2076-127">Contoso migrates the app database to an Azure SQL Database Managed Instance using the [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).</span></span> | <span data-ttu-id="c2076-128">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-128">Available</span></span>   
[<span data-ttu-id="c2076-129">Article 5: Rehost an app on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="c2076-129">Article 5: Rehost an app on Azure VMs</span></span>](contoso-migration-rehost-vm.md) | <span data-ttu-id="c2076-130">Contoso migrates its SmartHotel360 app VMs to Azure VMs using the Site Recovery service.</span><span class="sxs-lookup"><span data-stu-id="c2076-130">Contoso migrates its SmartHotel360 app VMs to Azure VMs using the Site Recovery service.</span></span> | <span data-ttu-id="c2076-131">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-131">Available</span></span>
[<span data-ttu-id="c2076-132">Article 6: Rehost an app on Azure VMs and in a  SQL Server AlwaysOn availability group</span><span class="sxs-lookup"><span data-stu-id="c2076-132">Article 6: Rehost an app on Azure VMs and in a  SQL Server AlwaysOn availability group</span></span>](contoso-migration-rehost-vm-sql-ag.md) | <span data-ttu-id="c2076-133">Contoso migrates the SmartHotel360 app.</span><span class="sxs-lookup"><span data-stu-id="c2076-133">Contoso migrates the SmartHotel360 app.</span></span> <span data-ttu-id="c2076-134">Contoso uses Site Recovery to migrate the app VMs.</span><span class="sxs-lookup"><span data-stu-id="c2076-134">Contoso uses Site Recovery to migrate the app VMs.</span></span> <span data-ttu-id="c2076-135">It uses the Database Migration Service to migrate the app database to a SQL Server cluster that's protected by an AlwaysOn availability group.</span><span class="sxs-lookup"><span data-stu-id="c2076-135">It uses the Database Migration Service to migrate the app database to a SQL Server cluster that's protected by an AlwaysOn availability group.</span></span> | <span data-ttu-id="c2076-136">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-136">Available</span></span> 
[<span data-ttu-id="c2076-137">Article 7: Rehost a Linux app on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="c2076-137">Article 7: Rehost a Linux app on Azure VMs</span></span>](contoso-migration-rehost-linux-vm.md) | <span data-ttu-id="c2076-138">Contoso completes a lift-and-shift migration of the Linux osTicket app to Azure VMs, using Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="c2076-138">Contoso completes a lift-and-shift migration of the Linux osTicket app to Azure VMs, using Azure Site Recovery</span></span> | <span data-ttu-id="c2076-139">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-139">Available</span></span>
[<span data-ttu-id="c2076-140">Article 8: Rehost a Linux app on Azure VMs and Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="c2076-140">Article 8: Rehost a Linux app on Azure VMs and Azure MySQL</span></span>](contoso-migration-rehost-linux-vm-mysql.md) | <span data-ttu-id="c2076-141">Contoso migrates the Linux osTicket app to Azure VMs using Azure Site Recovery, and migrates the app database to an Azure MySQL Server instance using MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="c2076-141">Contoso migrates the Linux osTicket app to Azure VMs using Azure Site Recovery, and migrates the app database to an Azure MySQL Server instance using MySQL Workbench.</span></span> | <span data-ttu-id="c2076-142">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-142">Available</span></span>
[<span data-ttu-id="c2076-143">Article 9: Refactor an app on Azure Web Apps and Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="c2076-143">Article 9: Refactor an app on Azure Web Apps and Azure SQL database</span></span>](contoso-migration-refactor-web-app-sql.md) | <span data-ttu-id="c2076-144">Contoso migrates the SmartHotel360 app to an Azure Web App, and migrates the app database to an Azure SQL Server instance with Database Migration Assistant</span><span class="sxs-lookup"><span data-stu-id="c2076-144">Contoso migrates the SmartHotel360 app to an Azure Web App, and migrates the app database to an Azure SQL Server instance with Database Migration Assistant</span></span> | <span data-ttu-id="c2076-145">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-145">Available</span></span>
[<span data-ttu-id="c2076-146">Article 10: Refactor a Linux app on Azure Web Apps and Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="c2076-146">Article 10: Refactor a Linux app on Azure Web Apps and Azure MySQL</span></span>](contoso-migration-refactor-linux-app-service-mysql.md) | <span data-ttu-id="c2076-147">Contoso migrates its Linux osTicket app to an Azure web app on multiple Azure regions using Azure Traffic Manager, integrated with GitHub for continuous delivery.</span><span class="sxs-lookup"><span data-stu-id="c2076-147">Contoso migrates its Linux osTicket app to an Azure web app on multiple Azure regions using Azure Traffic Manager, integrated with GitHub for continuous delivery.</span></span> <span data-ttu-id="c2076-148">Contoso migrates the app database to an Azure Database for MySQL instance.</span><span class="sxs-lookup"><span data-stu-id="c2076-148">Contoso migrates the app database to an Azure Database for MySQL instance.</span></span> | <span data-ttu-id="c2076-149">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-149">Available</span></span> 
[<span data-ttu-id="c2076-150">Article 11: Refactor TFS on Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="c2076-150">Article 11: Refactor TFS on Azure DevOps Services</span></span>](contoso-migration-tfs-vsts.md) | <span data-ttu-id="c2076-151">Contoso migrates its on-premises Team Foundation Server deployment to Azure DevOps Services in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2076-151">Contoso migrates its on-premises Team Foundation Server deployment to Azure DevOps Services in Azure.</span></span> | <span data-ttu-id="c2076-152">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-152">Available</span></span>
<span data-ttu-id="c2076-153">Article 12: Rearchitect an app on Azure Containers and Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c2076-153">Article 12: Rearchitect an app on Azure Containers and Azure SQL Database</span></span> | <span data-ttu-id="c2076-154">Contoso migrates its SmartHotel app to Azure.</span><span class="sxs-lookup"><span data-stu-id="c2076-154">Contoso migrates its SmartHotel app to Azure.</span></span> <span data-ttu-id="c2076-155">Then, it rearchitects the app web tier as a Windows container running in Azure Service Fabric, and the database with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c2076-155">Then, it rearchitects the app web tier as a Windows container running in Azure Service Fabric, and the database with Azure SQL Database.</span></span> | <span data-ttu-id="c2076-156">This article</span><span class="sxs-lookup"><span data-stu-id="c2076-156">This article</span></span>
[<span data-ttu-id="c2076-157">Article 13: Rebuild an app in Azure</span><span class="sxs-lookup"><span data-stu-id="c2076-157">Article 13: Rebuild an app in Azure</span></span>](contoso-migration-rebuild.md) | <span data-ttu-id="c2076-158">Contoso rebuilds its SmartHotel app by using a range of Azure capabilities and services, including Azure App Service, Azure Kubernetes Service (AKS), Azure Functions, Azure Cognitive Services, and Azure Cosmos DB..</span><span class="sxs-lookup"><span data-stu-id="c2076-158">Contoso rebuilds its SmartHotel app by using a range of Azure capabilities and services, including Azure App Service, Azure Kubernetes Service (AKS), Azure Functions, Azure Cognitive Services, and Azure Cosmos DB..</span></span> | <span data-ttu-id="c2076-159">Available</span><span class="sxs-lookup"><span data-stu-id="c2076-159">Available</span></span>    

<span data-ttu-id="c2076-160">In this article, Contoso migrates the two-tier Windows.</span><span class="sxs-lookup"><span data-stu-id="c2076-160">In this article, Contoso migrates the two-tier Windows.</span></span> <span data-ttu-id="c2076-161">NET SmartHotel360 app running on VMware VMs to Azure.</span><span class="sxs-lookup"><span data-stu-id="c2076-161">NET SmartHotel360 app running on VMware VMs to Azure.</span></span> <span data-ttu-id="c2076-162">If you'd like to use this app, it's provided as open source and you can download it from [GitHub](https://github.com/Microsoft/SmartHotel360).</span><span class="sxs-lookup"><span data-stu-id="c2076-162">If you'd like to use this app, it's provided as open source and you can download it from [GitHub](https://github.com/Microsoft/SmartHotel360).</span></span>

## <a name="business-drivers"></a><span data-ttu-id="c2076-163">Business drivers</span><span class="sxs-lookup"><span data-stu-id="c2076-163">Business drivers</span></span>

<span data-ttu-id="c2076-164">The Contoso IT leadership team has worked closely with business partners to understand what they want to achieve with this migration:</span><span class="sxs-lookup"><span data-stu-id="c2076-164">The Contoso IT leadership team has worked closely with business partners to understand what they want to achieve with this migration:</span></span>

- <span data-ttu-id="c2076-165">**Address business growth**: Contoso is growing, and as a result there is pressure on its on-premises systems and infrastructure.</span><span class="sxs-lookup"><span data-stu-id="c2076-165">**Address business growth**: Contoso is growing, and as a result there is pressure on its on-premises systems and infrastructure.</span></span>
- <span data-ttu-id="c2076-166">**Increase efficiency**: Contoso needs to remove unnecessary procedures, and streamline processes for developers and users.</span><span class="sxs-lookup"><span data-stu-id="c2076-166">**Increase efficiency**: Contoso needs to remove unnecessary procedures, and streamline processes for developers and users.</span></span>  <span data-ttu-id="c2076-167">The business needs IT to be fast and not waste time or money, thus delivering faster on customer requirements.</span><span class="sxs-lookup"><span data-stu-id="c2076-167">The business needs IT to be fast and not waste time or money, thus delivering faster on customer requirements.</span></span>
- <span data-ttu-id="c2076-168">**Increase agility**:  Contoso IT needs to be more responsive to the needs of the business.</span><span class="sxs-lookup"><span data-stu-id="c2076-168">**Increase agility**:  Contoso IT needs to be more responsive to the needs of the business.</span></span> <span data-ttu-id="c2076-169">It must be able to react faster than the changes in the marketplace, to enable the success in a global economy.</span><span class="sxs-lookup"><span data-stu-id="c2076-169">It must be able to react faster than the changes in the marketplace, to enable the success in a global economy.</span></span>  <span data-ttu-id="c2076-170">It mustn't get in the way, or become a business blocker.</span><span class="sxs-lookup"><span data-stu-id="c2076-170">It mustn't get in the way, or become a business blocker.</span></span>
- <span data-ttu-id="c2076-171">**Scale**: As the business grows successfully, Contoso IT must provide systems that are able to grow at the same pace.</span><span class="sxs-lookup"><span data-stu-id="c2076-171">**Scale**: As the business grows successfully, Contoso IT must provide systems that are able to grow at the same pace.</span></span>
- <span data-ttu-id="c2076-172">**Costs**: Contoso wants to minimize licensing costs.</span><span class="sxs-lookup"><span data-stu-id="c2076-172">**Costs**: Contoso wants to minimize licensing costs.</span></span>

## <a name="migration-goals"></a><span data-ttu-id="c2076-173">Migration goals</span><span class="sxs-lookup"><span data-stu-id="c2076-173">Migration goals</span></span>

<span data-ttu-id="c2076-174">The Contoso cloud team has pinned down goals for this migration.</span><span class="sxs-lookup"><span data-stu-id="c2076-174">The Contoso cloud team has pinned down goals for this migration.</span></span> <span data-ttu-id="c2076-175">These goals were used to determine the best migration method.</span><span class="sxs-lookup"><span data-stu-id="c2076-175">These goals were used to determine the best migration method.</span></span>

<span data-ttu-id="c2076-176">**Goals**</span><span class="sxs-lookup"><span data-stu-id="c2076-176">**Goals**</span></span> | <span data-ttu-id="c2076-177">**Details**</span><span class="sxs-lookup"><span data-stu-id="c2076-177">**Details**</span></span>
--- | --- 
<span data-ttu-id="c2076-178">**App reqs**</span><span class="sxs-lookup"><span data-stu-id="c2076-178">**App reqs**</span></span> | <span data-ttu-id="c2076-179">The app in Azure will remain as critical as it is today.</span><span class="sxs-lookup"><span data-stu-id="c2076-179">The app in Azure will remain as critical as it is today.</span></span><br/><br/> <span data-ttu-id="c2076-180">It should have the same performance capabilities as it currently does in VMWare.</span><span class="sxs-lookup"><span data-stu-id="c2076-180">It should have the same performance capabilities as it currently does in VMWare.</span></span><br/><br/> <span data-ttu-id="c2076-181">Contoso wants to stop supporting Windows Server 2008 R2, on which the app currently runs, and are willing to invest in the app.</span><span class="sxs-lookup"><span data-stu-id="c2076-181">Contoso wants to stop supporting Windows Server 2008 R2, on which the app currently runs, and are willing to invest in the app.</span></span><br/><br/> <span data-ttu-id="c2076-182">Contoso wants to move away from SQL Server 2008 R2 to a modern PaaS Database platform, which will minimize the need for management.</span><span class="sxs-lookup"><span data-stu-id="c2076-182">Contoso wants to move away from SQL Server 2008 R2 to a modern PaaS Database platform, which will minimize the need for management.</span></span><br/><br/> <span data-ttu-id="c2076-183">Contoso want to leverage its investment in SQL Server licensing and Software Assurance where possible.</span><span class="sxs-lookup"><span data-stu-id="c2076-183">Contoso want to leverage its investment in SQL Server licensing and Software Assurance where possible.</span></span><br/><br/> <span data-ttu-id="c2076-184">Contoso wants to be able to scale up the app web tier.</span><span class="sxs-lookup"><span data-stu-id="c2076-184">Contoso wants to be able to scale up the app web tier.</span></span>
<span data-ttu-id="c2076-185">**Limitations**</span><span class="sxs-lookup"><span data-stu-id="c2076-185">**Limitations**</span></span> | <span data-ttu-id="c2076-186">The app consists of an ASP.NET app and a WCF service running on the same VM.</span><span class="sxs-lookup"><span data-stu-id="c2076-186">The app consists of an ASP.NET app and a WCF service running on the same VM.</span></span> <span data-ttu-id="c2076-187">Contoso wants to split this across two web apps using the Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c2076-187">Contoso wants to split this across two web apps using the Azure App Service.</span></span> 
<span data-ttu-id="c2076-188">**Azure reqs**</span><span class="sxs-lookup"><span data-stu-id="c2076-188">**Azure reqs**</span></span> | <span data-ttu-id="c2076-189">Contoso wants to move the app to Azure, and run it in a container to extend app life.</span><span class="sxs-lookup"><span data-stu-id="c2076-189">Contoso wants to move the app to Azure, and run it in a container to extend app life.</span></span> <span data-ttu-id="c2076-190">It doesn't want to start completely from scratch to implement the app in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2076-190">It doesn't want to start completely from scratch to implement the app in Azure.</span></span> 
<span data-ttu-id="c2076-191">**DevOps**</span><span class="sxs-lookup"><span data-stu-id="c2076-191">**DevOps**</span></span> | <span data-ttu-id="c2076-192">Contoso wants to move to a DevOps model using Azure DevOps Services for code builds and release pipeline.</span><span class="sxs-lookup"><span data-stu-id="c2076-192">Contoso wants to move to a DevOps model using Azure DevOps Services for code builds and release pipeline.</span></span>

## <a name="solution-design"></a><span data-ttu-id="c2076-193">Solution design</span><span class="sxs-lookup"><span data-stu-id="c2076-193">Solution design</span></span>

<span data-ttu-id="c2076-194">After pinning down goals and requirements, Contoso designs and review a deployment solution, and identifies the migration process, including the Azure services that Contoso will use for the migration.</span><span class="sxs-lookup"><span data-stu-id="c2076-194">After pinning down goals and requirements, Contoso designs and review a deployment solution, and identifies the migration process, including the Azure services that Contoso will use for the migration.</span></span>

### <a name="current-app"></a><span data-ttu-id="c2076-195">Current app</span><span class="sxs-lookup"><span data-stu-id="c2076-195">Current app</span></span>

- <span data-ttu-id="c2076-196">The SmartHotel360 on-premises app is tiered across two VMs (WEBVM and SQLVM).</span><span class="sxs-lookup"><span data-stu-id="c2076-196">The SmartHotel360 on-premises app is tiered across two VMs (WEBVM and SQLVM).</span></span>
- <span data-ttu-id="c2076-197">The VMs are located on VMware ESXi host **contosohost1.contoso.com** (version 6.5)</span><span class="sxs-lookup"><span data-stu-id="c2076-197">The VMs are located on VMware ESXi host **contosohost1.contoso.com** (version 6.5)</span></span>
- <span data-ttu-id="c2076-198">The VMware environment is managed by vCenter Server 6.5 (**vcenter.contoso.com**), running on a VM.</span><span class="sxs-lookup"><span data-stu-id="c2076-198">The VMware environment is managed by vCenter Server 6.5 (**vcenter.contoso.com**), running on a VM.</span></span>
- <span data-ttu-id="c2076-199">Contoso has an on-premises datacenter (contoso-datacenter), with an on-premises domain controller (**contosodc1**).</span><span class="sxs-lookup"><span data-stu-id="c2076-199">Contoso has an on-premises datacenter (contoso-datacenter), with an on-premises domain controller (**contosodc1**).</span></span>
- <span data-ttu-id="c2076-200">The on-premises VMs in the Contoso datacenter will be decommissioned after the migration is done.</span><span class="sxs-lookup"><span data-stu-id="c2076-200">The on-premises VMs in the Contoso datacenter will be decommissioned after the migration is done.</span></span>


### <a name="proposed-architecture"></a><span data-ttu-id="c2076-201">Proposed architecture</span><span class="sxs-lookup"><span data-stu-id="c2076-201">Proposed architecture</span></span>

- <span data-ttu-id="c2076-202">For the database tier of the app, Contoso compared Azure SQL Database with SQL Server using [this article](https://docs.microsoft.com/azure/sql-database/sql-database-features).</span><span class="sxs-lookup"><span data-stu-id="c2076-202">For the database tier of the app, Contoso compared Azure SQL Database with SQL Server using [this article](https://docs.microsoft.com/azure/sql-database/sql-database-features).</span></span> <span data-ttu-id="c2076-203">It decided to go with Azure SQL Database for a few reasons:</span><span class="sxs-lookup"><span data-stu-id="c2076-203">It decided to go with Azure SQL Database for a few reasons:</span></span>
    - <span data-ttu-id="c2076-204">Azure SQL Database is a relational-database managed service.</span><span class="sxs-lookup"><span data-stu-id="c2076-204">Azure SQL Database is a relational-database managed service.</span></span> <span data-ttu-id="c2076-205">It delivers predictable performance at multiple service levels, with near-zero administration.</span><span class="sxs-lookup"><span data-stu-id="c2076-205">It delivers predictable performance at multiple service levels, with near-zero administration.</span></span> <span data-ttu-id="c2076-206">Advantages include dynamic scalability with no downtime, built-in intelligent optimization, and global scalability and availability.</span><span class="sxs-lookup"><span data-stu-id="c2076-206">Advantages include dynamic scalability with no downtime, built-in intelligent optimization, and global scalability and availability.</span></span>
    - <span data-ttu-id="c2076-207">Contoso leverages the lightweight Data Migration Assistant (DMA) to assess and migrate the on-premises database to Azure SQL.</span><span class="sxs-lookup"><span data-stu-id="c2076-207">Contoso leverages the lightweight Data Migration Assistant (DMA) to assess and migrate the on-premises database to Azure SQL.</span></span>
    - <span data-ttu-id="c2076-208">With Software Assurance, Contoso can exchange its existing licenses for discounted rates on a SQL Database, using the Azure Hybrid Benefit for SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c2076-208">With Software Assurance, Contoso can exchange its existing licenses for discounted rates on a SQL Database, using the Azure Hybrid Benefit for SQL Server.</span></span> <span data-ttu-id="c2076-209">This could provide savings of up to 30%.</span><span class="sxs-lookup"><span data-stu-id="c2076-209">This could provide savings of up to 30%.</span></span>
    - <span data-ttu-id="c2076-210">SQL Database provides a number of security features including always encrypted, dynamic data masking, and row-level security/threat detection.</span><span class="sxs-lookup"><span data-stu-id="c2076-210">SQL Database provides a number of security features including always encrypted, dynamic data masking, and row-level security/threat detection.</span></span>
- <span data-ttu-id="c2076-211">For the app web tier, Contoso has decided convert it to the Windows Container using Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c2076-211">For the app web tier, Contoso has decided convert it to the Windows Container using Visual Studio.</span></span>
    - <span data-ttu-id="c2076-212">Contoso will deploy the app using Azure Service Fabric, and pull the Windows container image from the Azure Container Registry (ACR).</span><span class="sxs-lookup"><span data-stu-id="c2076-212">Contoso will deploy the app using Azure Service Fabric, and pull the Windows container image from the Azure Container Registry (ACR).</span></span>
    - <span data-ttu-id="c2076-213">A prototype for extending the app to include sentiment analysis will be implemented as another service in Service Fabric, connected to Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c2076-213">A prototype for extending the app to include sentiment analysis will be implemented as another service in Service Fabric, connected to Cosmos DB.</span></span>  <span data-ttu-id="c2076-214">This will read information from Tweets, and display on the app.</span><span class="sxs-lookup"><span data-stu-id="c2076-214">This will read information from Tweets, and display on the app.</span></span>
- <span data-ttu-id="c2076-215">To implement a DevOps pipeline, Contoso will use Azure DevOps Services for source code management (SCM), with Git repos.</span><span class="sxs-lookup"><span data-stu-id="c2076-215">To implement a DevOps pipeline, Contoso will use Azure DevOps Services for source code management (SCM), with Git repos.</span></span>  <span data-ttu-id="c2076-216">Automated builds and releases will be used to build code, and deploy it to the Azure Container Registry and Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c2076-216">Automated builds and releases will be used to build code, and deploy it to the Azure Container Registry and Azure Service Fabric.</span></span>

    ![Scenario architecture](./media/contoso-migration-rearchitect-container-sql/architecture.png) 

  
### <a name="solution-review"></a><span data-ttu-id="c2076-218">Solution review</span><span class="sxs-lookup"><span data-stu-id="c2076-218">Solution review</span></span>
<span data-ttu-id="c2076-219">Contoso evaluates the proposed design by putting together a pros and cons list.</span><span class="sxs-lookup"><span data-stu-id="c2076-219">Contoso evaluates the proposed design by putting together a pros and cons list.</span></span>

<span data-ttu-id="c2076-220">**Consideration**</span><span class="sxs-lookup"><span data-stu-id="c2076-220">**Consideration**</span></span> | <span data-ttu-id="c2076-221">**Details**</span><span class="sxs-lookup"><span data-stu-id="c2076-221">**Details**</span></span>
--- | ---
<span data-ttu-id="c2076-222">**Pros**</span><span class="sxs-lookup"><span data-stu-id="c2076-222">**Pros**</span></span> | <span data-ttu-id="c2076-223">The SmartHotel360 app code will need to be altered for migration to Azure Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c2076-223">The SmartHotel360 app code will need to be altered for migration to Azure Service Fabric.</span></span> <span data-ttu-id="c2076-224">However, the effort is minimal, using the Service Fabric SDK tools for the changes.</span><span class="sxs-lookup"><span data-stu-id="c2076-224">However, the effort is minimal, using the Service Fabric SDK tools for the changes.</span></span><br/><br/> <span data-ttu-id="c2076-225">With the move to Service Fabric, Contoso can start to develop microservices to add to the application quickly over time, without risk to the original code base.</span><span class="sxs-lookup"><span data-stu-id="c2076-225">With the move to Service Fabric, Contoso can start to develop microservices to add to the application quickly over time, without risk to the original code base.</span></span><br/><br/> <span data-ttu-id="c2076-226">Windows Containers offer the same benefits as containers in general.</span><span class="sxs-lookup"><span data-stu-id="c2076-226">Windows Containers offer the same benefits as containers in general.</span></span> <span data-ttu-id="c2076-227">They improve agility, portability, and control.</span><span class="sxs-lookup"><span data-stu-id="c2076-227">They improve agility, portability, and control.</span></span><br/><br/> <span data-ttu-id="c2076-228">Contoso can leverage its investment in Software Assurance using the Azure Hybrid Benefit for both SQL Server and Windows Server.</span><span class="sxs-lookup"><span data-stu-id="c2076-228">Contoso can leverage its investment in Software Assurance using the Azure Hybrid Benefit for both SQL Server and Windows Server.</span></span><br/><br/> <span data-ttu-id="c2076-229">After the migration it will no longer need to support Windows Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="c2076-229">After the migration it will no longer need to support Windows Server 2008 R2.</span></span> <span data-ttu-id="c2076-230">[Learn more](https://support.microsoft.com/lifecycle).</span><span class="sxs-lookup"><span data-stu-id="c2076-230">[Learn more](https://support.microsoft.com/lifecycle).</span></span><br/><br/> <span data-ttu-id="c2076-231">Contoso can configure the web tier of the app with multiple instances, so that it's no longer a single point of failure.</span><span class="sxs-lookup"><span data-stu-id="c2076-231">Contoso can configure the web tier of the app with multiple instances, so that it's no longer a single point of failure.</span></span><br/><br/> <span data-ttu-id="c2076-232">It will no longer be dependent on the aging SQL Server 2008 R2.</span><span class="sxs-lookup"><span data-stu-id="c2076-232">It will no longer be dependent on the aging SQL Server 2008 R2.</span></span><br/><br/> <span data-ttu-id="c2076-233">SQL Database supports Contoso's technical requirements.</span><span class="sxs-lookup"><span data-stu-id="c2076-233">SQL Database supports Contoso's technical requirements.</span></span> <span data-ttu-id="c2076-234">Contoso admins assessed the on-premises database using the Database Migration Assistant and found it compatible.</span><span class="sxs-lookup"><span data-stu-id="c2076-234">Contoso admins assessed the on-premises database using the Database Migration Assistant and found it compatible.</span></span><br/><br/> <span data-ttu-id="c2076-235">SQL Database has built-in fault tolerance that Contoso doesn't need to set up.</span><span class="sxs-lookup"><span data-stu-id="c2076-235">SQL Database has built-in fault tolerance that Contoso doesn't need to set up.</span></span> <span data-ttu-id="c2076-236">This ensures that the data tier is no longer a single point of failover.</span><span class="sxs-lookup"><span data-stu-id="c2076-236">This ensures that the data tier is no longer a single point of failover.</span></span>
<span data-ttu-id="c2076-237">**Cons**</span><span class="sxs-lookup"><span data-stu-id="c2076-237">**Cons**</span></span> | <span data-ttu-id="c2076-238">Containers are more complex than other migration options.</span><span class="sxs-lookup"><span data-stu-id="c2076-238">Containers are more complex than other migration options.</span></span> <span data-ttu-id="c2076-239">The learning curve on containers could be an issue for Contoso.</span><span class="sxs-lookup"><span data-stu-id="c2076-239">The learning curve on containers could be an issue for Contoso.</span></span>  <span data-ttu-id="c2076-240">They introduce a new level of complexity that provides a lot of value in spite of the curve.</span><span class="sxs-lookup"><span data-stu-id="c2076-240">They introduce a new level of complexity that provides a lot of value in spite of the curve.</span></span><br/><br/> <span data-ttu-id="c2076-241">The operations team at Contoso will need to ramp up to understand and support Azure, containers and microservices for the app.</span><span class="sxs-lookup"><span data-stu-id="c2076-241">The operations team at Contoso will need to ramp up to understand and support Azure, containers and microservices for the app.</span></span><br/><br/> <span data-ttu-id="c2076-242">If Contoso uses the Data Migration Assistant instead of Data Migration Service to migrate the database, It won’t have the infrastructure ready for migrating databases at scale.</span><span class="sxs-lookup"><span data-stu-id="c2076-242">If Contoso uses the Data Migration Assistant instead of Data Migration Service to migrate the database, It won’t have the infrastructure ready for migrating databases at scale.</span></span>



### <a name="migration-process"></a><span data-ttu-id="c2076-243">Migration process</span><span class="sxs-lookup"><span data-stu-id="c2076-243">Migration process</span></span>

1. <span data-ttu-id="c2076-244">Contoso provisions the Azure service fabric cluster for Windows.</span><span class="sxs-lookup"><span data-stu-id="c2076-244">Contoso provisions the Azure service fabric cluster for Windows.</span></span>
2. <span data-ttu-id="c2076-245">It provisions an Azure SQL instance, and migrates the SmartHotel360 database to it.</span><span class="sxs-lookup"><span data-stu-id="c2076-245">It provisions an Azure SQL instance, and migrates the SmartHotel360 database to it.</span></span>
3. <span data-ttu-id="c2076-246">Contoso converts the Web tier VM to a Docker container using the Service Fabric SDK tools.</span><span class="sxs-lookup"><span data-stu-id="c2076-246">Contoso converts the Web tier VM to a Docker container using the Service Fabric SDK tools.</span></span>
4. <span data-ttu-id="c2076-247">It connects the service fabric cluster and the ACR, and deploys the app using Azure service fabric.</span><span class="sxs-lookup"><span data-stu-id="c2076-247">It connects the service fabric cluster and the ACR, and deploys the app using Azure service fabric.</span></span>

    ![Migration process](./media/contoso-migration-rearchitect-container-sql/migration-process.png) 

### <a name="azure-services"></a><span data-ttu-id="c2076-249">Azure services</span><span class="sxs-lookup"><span data-stu-id="c2076-249">Azure services</span></span>

<span data-ttu-id="c2076-250">**Service**</span><span class="sxs-lookup"><span data-stu-id="c2076-250">**Service**</span></span> | <span data-ttu-id="c2076-251">**Description**</span><span class="sxs-lookup"><span data-stu-id="c2076-251">**Description**</span></span> | <span data-ttu-id="c2076-252">**Cost**</span><span class="sxs-lookup"><span data-stu-id="c2076-252">**Cost**</span></span>
--- | --- | ---
[<span data-ttu-id="c2076-253">Database Migration Assistant (DMA)</span><span class="sxs-lookup"><span data-stu-id="c2076-253">Database Migration Assistant (DMA)</span></span>](https://docs.microsoft.com/sql/dma/dma-overview?view=ssdt-18vs2017) | <span data-ttu-id="c2076-254">Assesses and detect compatibility issues that might impact database functionality in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2076-254">Assesses and detect compatibility issues that might impact database functionality in Azure.</span></span> <span data-ttu-id="c2076-255">DMA assesses feature parity between SQL sources and targets, and recommends performance and reliability improvements.</span><span class="sxs-lookup"><span data-stu-id="c2076-255">DMA assesses feature parity between SQL sources and targets, and recommends performance and reliability improvements.</span></span> | <span data-ttu-id="c2076-256">It's a downloadable tool free of charge.</span><span class="sxs-lookup"><span data-stu-id="c2076-256">It's a downloadable tool free of charge.</span></span>
[<span data-ttu-id="c2076-257">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c2076-257">Azure SQL Database</span></span>](https://azure.microsoft.com/services/sql-database/) | <span data-ttu-id="c2076-258">Provides an intelligent, fully managed relational cloud database service.</span><span class="sxs-lookup"><span data-stu-id="c2076-258">Provides an intelligent, fully managed relational cloud database service.</span></span> | <span data-ttu-id="c2076-259">Cost based on features, throughput and size.</span><span class="sxs-lookup"><span data-stu-id="c2076-259">Cost based on features, throughput and size.</span></span> <span data-ttu-id="c2076-260">[Learn more](https://azure.microsoft.com/pricing/details/sql-database/managed/).</span><span class="sxs-lookup"><span data-stu-id="c2076-260">[Learn more](https://azure.microsoft.com/pricing/details/sql-database/managed/).</span></span>
[<span data-ttu-id="c2076-261">Azure Container Registry</span><span class="sxs-lookup"><span data-stu-id="c2076-261">Azure Container Registry</span></span>](https://azure.microsoft.com/services/container-registry/) | <span data-ttu-id="c2076-262">Stores images for all types of container deployments.</span><span class="sxs-lookup"><span data-stu-id="c2076-262">Stores images for all types of container deployments.</span></span> | <span data-ttu-id="c2076-263">Cost based on features, storage, and usage duration.</span><span class="sxs-lookup"><span data-stu-id="c2076-263">Cost based on features, storage, and usage duration.</span></span> <span data-ttu-id="c2076-264">[Learn more](https://azure.microsoft.com/pricing/details/container-registry/).</span><span class="sxs-lookup"><span data-stu-id="c2076-264">[Learn more](https://azure.microsoft.com/pricing/details/container-registry/).</span></span>
[<span data-ttu-id="c2076-265">Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c2076-265">Azure Service Fabric</span></span>](https://azure.microsoft.com/services/service-fabric/) | <span data-ttu-id="c2076-266">Builds and operate always-on, scalable and distributed apps</span><span class="sxs-lookup"><span data-stu-id="c2076-266">Builds and operate always-on, scalable and distributed apps</span></span> | <span data-ttu-id="c2076-267">Cost based on size, location, and duration of the compute nodes.</span><span class="sxs-lookup"><span data-stu-id="c2076-267">Cost based on size, location, and duration of the compute nodes.</span></span> <span data-ttu-id="c2076-268">[Learn more](https://azure.microsoft.com/pricing/details/service-fabric/).</span><span class="sxs-lookup"><span data-stu-id="c2076-268">[Learn more](https://azure.microsoft.com/pricing/details/service-fabric/).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2076-269">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="c2076-269">Prerequisites</span></span>

<span data-ttu-id="c2076-270">Here's what Contoso needs to run this scenario:</span><span class="sxs-lookup"><span data-stu-id="c2076-270">Here's what Contoso needs to run this scenario:</span></span>

<span data-ttu-id="c2076-271">**Requirements**</span><span class="sxs-lookup"><span data-stu-id="c2076-271">**Requirements**</span></span> | <span data-ttu-id="c2076-272">**Details**</span><span class="sxs-lookup"><span data-stu-id="c2076-272">**Details**</span></span>
--- | ---
<span data-ttu-id="c2076-273">**Azure subscription**</span><span class="sxs-lookup"><span data-stu-id="c2076-273">**Azure subscription**</span></span> | <span data-ttu-id="c2076-274">Contoso created subscriptions earlier in this article series.</span><span class="sxs-lookup"><span data-stu-id="c2076-274">Contoso created subscriptions earlier in this article series.</span></span> <span data-ttu-id="c2076-275">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c2076-275">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span><br/><br/> <span data-ttu-id="c2076-276">If you create a free account, you're the administrator of your subscription and can perform all actions.</span><span class="sxs-lookup"><span data-stu-id="c2076-276">If you create a free account, you're the administrator of your subscription and can perform all actions.</span></span><br/><br/> <span data-ttu-id="c2076-277">If you use an existing subscription and you're not the administrator, you need to work with the admin to assign you Owner or Contributor permissions.</span><span class="sxs-lookup"><span data-stu-id="c2076-277">If you use an existing subscription and you're not the administrator, you need to work with the admin to assign you Owner or Contributor permissions.</span></span>
<span data-ttu-id="c2076-278">**Azure infrastructure**</span><span class="sxs-lookup"><span data-stu-id="c2076-278">**Azure infrastructure**</span></span> | <span data-ttu-id="c2076-279">[Learn how](contoso-migration-infrastructure.md) Contoso previously set up an Azure infrastructure.</span><span class="sxs-lookup"><span data-stu-id="c2076-279">[Learn how](contoso-migration-infrastructure.md) Contoso previously set up an Azure infrastructure.</span></span>
<span data-ttu-id="c2076-280">**Developer prerequisites**</span><span class="sxs-lookup"><span data-stu-id="c2076-280">**Developer prerequisites**</span></span> | <span data-ttu-id="c2076-281">Contoso needs the following tools on a developer workstation:</span><span class="sxs-lookup"><span data-stu-id="c2076-281">Contoso needs the following tools on a developer workstation:</span></span><br/><br/> <span data-ttu-id="c2076-282">- [Visual Studio 2017 Community Edition: Version 15.5](https://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="c2076-282">- [Visual Studio 2017 Community Edition: Version 15.5](https://www.visualstudio.com/)</span></span><br/><br/> <span data-ttu-id="c2076-283">- .NET workload enabled.</span><span class="sxs-lookup"><span data-stu-id="c2076-283">- .NET workload enabled.</span></span><br/><br/> <span data-ttu-id="c2076-284">- [Git](https://git-scm.com/)</span><span class="sxs-lookup"><span data-stu-id="c2076-284">- [Git](https://git-scm.com/)</span></span><br/><br/> <span data-ttu-id="c2076-285">- [Service Fabric SDK v 3.0 or later](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started)</span><span class="sxs-lookup"><span data-stu-id="c2076-285">- [Service Fabric SDK v 3.0 or later](https://docs.microsoft.com/azure/service-fabric/service-fabric-get-started)</span></span><br/><br/> <span data-ttu-id="c2076-286">- [Docker CE (Windows 10) or Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install/) set to use Windows Containers.</span><span class="sxs-lookup"><span data-stu-id="c2076-286">- [Docker CE (Windows 10) or Docker EE (Windows Server)](https://docs.docker.com/docker-for-windows/install/) set to use Windows Containers.</span></span>



## <a name="scenario-steps"></a><span data-ttu-id="c2076-287">Scenario steps</span><span class="sxs-lookup"><span data-stu-id="c2076-287">Scenario steps</span></span>

<span data-ttu-id="c2076-288">Here's how Contoso runs the migration:</span><span class="sxs-lookup"><span data-stu-id="c2076-288">Here's how Contoso runs the migration:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="c2076-289">**Step 1: Provision a SQL Database instance in Azure**: Contoso provisions a SQL instance in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2076-289">**Step 1: Provision a SQL Database instance in Azure**: Contoso provisions a SQL instance in Azure.</span></span> <span data-ttu-id="c2076-290">After the frontend web VM is migrated to an Azure container, the container instance with the app web frontend will point to this database.</span><span class="sxs-lookup"><span data-stu-id="c2076-290">After the frontend web VM is migrated to an Azure container, the container instance with the app web frontend will point to this database.</span></span>
> * <span data-ttu-id="c2076-291">**Step 2: Create an Azure Container Registry (ACR)**: Contoso provisions an enterprise container registry for the docker container images.</span><span class="sxs-lookup"><span data-stu-id="c2076-291">**Step 2: Create an Azure Container Registry (ACR)**: Contoso provisions an enterprise container registry for the docker container images.</span></span>
> * <span data-ttu-id="c2076-292">**Step 3: Provision Azure Service Fabric**: It provisions a Service Fabric Cluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-292">**Step 3: Provision Azure Service Fabric**: It provisions a Service Fabric Cluster.</span></span>
> * <span data-ttu-id="c2076-293">**Step 4: Manage service fabric certificates**: Contoso sets up certificates for Azure DevOps Services access to the cluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-293">**Step 4: Manage service fabric certificates**: Contoso sets up certificates for Azure DevOps Services access to the cluster.</span></span>
> * <span data-ttu-id="c2076-294">**Step 5: Migrate the database with DMA**: It migrates the app database with the Database Migration Assistant.</span><span class="sxs-lookup"><span data-stu-id="c2076-294">**Step 5: Migrate the database with DMA**: It migrates the app database with the Database Migration Assistant.</span></span>
> * <span data-ttu-id="c2076-295">**Step 6: Set up Azure DevOps Services**: Contoso sets up a new project in Azure DevOps Services, and imports the code into the Git Repo.</span><span class="sxs-lookup"><span data-stu-id="c2076-295">**Step 6: Set up Azure DevOps Services**: Contoso sets up a new project in Azure DevOps Services, and imports the code into the Git Repo.</span></span>
> * <span data-ttu-id="c2076-296">**Step 7: Convert the app**: Contoso converts the app to a container using Visual Studio and SDK tools.</span><span class="sxs-lookup"><span data-stu-id="c2076-296">**Step 7: Convert the app**: Contoso converts the app to a container using Visual Studio and SDK tools.</span></span>
> * <span data-ttu-id="c2076-297">**Step 8: Set up build and release**: Contoso sets up the build and release pipelines to create and publish the app to the ACR and Service Fabric Cluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-297">**Step 8: Set up build and release**: Contoso sets up the build and release pipelines to create and publish the app to the ACR and Service Fabric Cluster.</span></span>
> * <span data-ttu-id="c2076-298">**Step 9: Extend the app**: After the app is public, Contoso extends it to take advantage of Azure capabilities, and republishes it to Azure using the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c2076-298">**Step 9: Extend the app**: After the app is public, Contoso extends it to take advantage of Azure capabilities, and republishes it to Azure using the pipeline.</span></span>



## <a name="step-1-provision-an-azure-sql-database"></a><span data-ttu-id="c2076-299">Step 1: Provision an Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="c2076-299">Step 1: Provision an Azure SQL Database</span></span>

<span data-ttu-id="c2076-300">Contoso admins provision an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c2076-300">Contoso admins provision an Azure SQL database.</span></span>

1. <span data-ttu-id="c2076-301">They select to create a **SQL Database** in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2076-301">They select to create a **SQL Database** in Azure.</span></span> 

    ![Provision SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql1.png)

2. <span data-ttu-id="c2076-303">They specify a database  name to match the database running on the on-premises VM (**SmartHotel.Registration**).</span><span class="sxs-lookup"><span data-stu-id="c2076-303">They specify a database  name to match the database running on the on-premises VM (**SmartHotel.Registration**).</span></span> <span data-ttu-id="c2076-304">They place the database in the ContosoRG resource group.</span><span class="sxs-lookup"><span data-stu-id="c2076-304">They place the database in the ContosoRG resource group.</span></span> <span data-ttu-id="c2076-305">This is the resource group they use for production resources in Azure.</span><span class="sxs-lookup"><span data-stu-id="c2076-305">This is the resource group they use for production resources in Azure.</span></span>

    ![Provision SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql2.png)

3. <span data-ttu-id="c2076-307">They set up a new SQL Server instance (**sql-smarthotel-eus2**) in the primary region.</span><span class="sxs-lookup"><span data-stu-id="c2076-307">They set up a new SQL Server instance (**sql-smarthotel-eus2**) in the primary region.</span></span>

    ![Provision SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql3.png)

4. <span data-ttu-id="c2076-309">They set the pricing tier to match server and database needs.</span><span class="sxs-lookup"><span data-stu-id="c2076-309">They set the pricing tier to match server and database needs.</span></span> <span data-ttu-id="c2076-310">And they select to save money with Azure Hybrid Benefit because they already have a SQL Server license.</span><span class="sxs-lookup"><span data-stu-id="c2076-310">And they select to save money with Azure Hybrid Benefit because they already have a SQL Server license.</span></span>
5. <span data-ttu-id="c2076-311">For sizing they use v-Core-based purchasing, and set the limits for the expected requirements.</span><span class="sxs-lookup"><span data-stu-id="c2076-311">For sizing they use v-Core-based purchasing, and set the limits for the expected requirements.</span></span>

    ![Provision SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql4.png)

6. <span data-ttu-id="c2076-313">Then they create the database instance.</span><span class="sxs-lookup"><span data-stu-id="c2076-313">Then they create the database instance.</span></span>

    ![Provision SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql5.png)

7. <span data-ttu-id="c2076-315">After the instance is created, they open the database, and note details they need when they use the Database Migration Assistance for migration.</span><span class="sxs-lookup"><span data-stu-id="c2076-315">After the instance is created, they open the database, and note details they need when they use the Database Migration Assistance for migration.</span></span>

    ![Provision SQL](./media/contoso-migration-rearchitect-container-sql/provision-sql6.png)


<span data-ttu-id="c2076-317">**Need more help?**</span><span class="sxs-lookup"><span data-stu-id="c2076-317">**Need more help?**</span></span>

- <span data-ttu-id="c2076-318">[Get help](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) provisioning a SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c2076-318">[Get help](https://docs.microsoft.com/azure/sql-database/sql-database-get-started-portal) provisioning a SQL Database.</span></span>
- <span data-ttu-id="c2076-319">[Learn about](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) v-Core resource limits.</span><span class="sxs-lookup"><span data-stu-id="c2076-319">[Learn about](https://docs.microsoft.com/azure/sql-database/sql-database-vcore-resource-limits-elastic-pools) v-Core resource limits.</span></span>



## <a name="step-2-create-an-acr-and-provision-an-azure-container"></a><span data-ttu-id="c2076-320">Step 2: Create an ACR and provision an Azure Container</span><span class="sxs-lookup"><span data-stu-id="c2076-320">Step 2: Create an ACR and provision an Azure Container</span></span>

<span data-ttu-id="c2076-321">The Azure container is created using the exported files from the Web VM.</span><span class="sxs-lookup"><span data-stu-id="c2076-321">The Azure container is created using the exported files from the Web VM.</span></span> <span data-ttu-id="c2076-322">The container is housed in the Azure Container Registry (ACR).</span><span class="sxs-lookup"><span data-stu-id="c2076-322">The container is housed in the Azure Container Registry (ACR).</span></span>


1. <span data-ttu-id="c2076-323">Contoso admins create a Container Registry in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c2076-323">Contoso admins create a Container Registry in the Azure portal.</span></span>

     ![Container Registry](./media/contoso-migration-rearchitect-container-sql/container-registry1.png)

2. <span data-ttu-id="c2076-325">They provide a name for the registry (**contosoacreus2**), and place it in the primary region, in the resource group they use for their infrastructure resources.</span><span class="sxs-lookup"><span data-stu-id="c2076-325">They provide a name for the registry (**contosoacreus2**), and place it in the primary region, in the resource group they use for their infrastructure resources.</span></span> <span data-ttu-id="c2076-326">They enable access for admin users, and set it as a premium SKU so that they can leverage geo-replication.</span><span class="sxs-lookup"><span data-stu-id="c2076-326">They enable access for admin users, and set it as a premium SKU so that they can leverage geo-replication.</span></span>

    ![Container Registry](./media/contoso-migration-rearchitect-container-sql/container-registry2.png)  


## <a name="step-3-provision-azure-service-fabric"></a><span data-ttu-id="c2076-328">Step 3: Provision Azure Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c2076-328">Step 3: Provision Azure Service Fabric</span></span>

<span data-ttu-id="c2076-329">The SmartHotel360 container will run in the Azure Service Fabric Sluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-329">The SmartHotel360 container will run in the Azure Service Fabric Sluster.</span></span> <span data-ttu-id="c2076-330">Contoso admins create the Service Fabric Cluster as follows:</span><span class="sxs-lookup"><span data-stu-id="c2076-330">Contoso admins create the Service Fabric Cluster as follows:</span></span>

1. <span data-ttu-id="c2076-331">Create a Service Fabric resource from the Azure Marketplace</span><span class="sxs-lookup"><span data-stu-id="c2076-331">Create a Service Fabric resource from the Azure Marketplace</span></span>

     ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric1.png)

2. <span data-ttu-id="c2076-333">In **Basic**, they provide a unique DS name for the cluster, and credentials for accessing the on-premises VM.</span><span class="sxs-lookup"><span data-stu-id="c2076-333">In **Basic**, they provide a unique DS name for the cluster, and credentials for accessing the on-premises VM.</span></span> <span data-ttu-id="c2076-334">They place the resource in the production resource group (**ContosoRG**) in the primary East US 2 region.</span><span class="sxs-lookup"><span data-stu-id="c2076-334">They place the resource in the production resource group (**ContosoRG**) in the primary East US 2 region.</span></span>

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric2.png) 

3. <span data-ttu-id="c2076-336">In **Node type configuration**, they input a node type name, durability settings, VM size, and app endpoints.</span><span class="sxs-lookup"><span data-stu-id="c2076-336">In **Node type configuration**, they input a node type name, durability settings, VM size, and app endpoints.</span></span>

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric3.png) 


4. <span data-ttu-id="c2076-338">In **Create key vault**, they create a new key vault in their infrastructure resource group, to house the certificate.</span><span class="sxs-lookup"><span data-stu-id="c2076-338">In **Create key vault**, they create a new key vault in their infrastructure resource group, to house the certificate.</span></span>

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric4.png) 


5. <span data-ttu-id="c2076-340">In **Access Policies** they enable access to virtual machines to deploy the key vault.</span><span class="sxs-lookup"><span data-stu-id="c2076-340">In **Access Policies** they enable access to virtual machines to deploy the key vault.</span></span>

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric5.png) 

6. <span data-ttu-id="c2076-342">They specify a name for the certificate.</span><span class="sxs-lookup"><span data-stu-id="c2076-342">They specify a name for the certificate.</span></span>

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric6.png) 

7. <span data-ttu-id="c2076-344">In the summary page, they copy the link that's used to download the certificate.</span><span class="sxs-lookup"><span data-stu-id="c2076-344">In the summary page, they copy the link that's used to download the certificate.</span></span> <span data-ttu-id="c2076-345">They need this to connect to the Service Fabric Cluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-345">They need this to connect to the Service Fabric Cluster.</span></span>

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric7.png) 

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric8.png) 

8. <span data-ttu-id="c2076-348">After validation passes, they provision the cluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-348">After validation passes, they provision the cluster.</span></span>

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric9.png) 

9. <span data-ttu-id="c2076-350">In the Certificate Import Wizard, they import the downloaded certificate to dev machines.</span><span class="sxs-lookup"><span data-stu-id="c2076-350">In the Certificate Import Wizard, they import the downloaded certificate to dev machines.</span></span> <span data-ttu-id="c2076-351">The certificate is used to authenticate to the cluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-351">The certificate is used to authenticate to the cluster.</span></span>

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric10.png) 

10. <span data-ttu-id="c2076-353">After the cluster is provisioned, they connect to the Service Fabric Cluster Explorer.</span><span class="sxs-lookup"><span data-stu-id="c2076-353">After the cluster is provisioned, they connect to the Service Fabric Cluster Explorer.</span></span>

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric11.png) 

11. <span data-ttu-id="c2076-355">They need to select the correct certificate.</span><span class="sxs-lookup"><span data-stu-id="c2076-355">They need to select the correct certificate.</span></span>

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric12.png) 

12. <span data-ttu-id="c2076-357">The Service Fabric Explorer loads, and the Contoso Admin can manage the cluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-357">The Service Fabric Explorer loads, and the Contoso Admin can manage the cluster.</span></span>

    ![Service Fabric](./media/contoso-migration-rearchitect-container-sql/service-fabric13.png) 


## <a name="step-4-manage-service-fabric-certificates"></a><span data-ttu-id="c2076-359">Step 4: Manage Service Fabric certificates</span><span class="sxs-lookup"><span data-stu-id="c2076-359">Step 4: Manage Service Fabric certificates</span></span>

<span data-ttu-id="c2076-360">Contoso needs cluster certificates to allow Azure DevOps Services access to the cluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-360">Contoso needs cluster certificates to allow Azure DevOps Services access to the cluster.</span></span> <span data-ttu-id="c2076-361">Contoso admins set this up.</span><span class="sxs-lookup"><span data-stu-id="c2076-361">Contoso admins set this up.</span></span>

1. <span data-ttu-id="c2076-362">They open the Azure portal and browse to the KeyVault.</span><span class="sxs-lookup"><span data-stu-id="c2076-362">They open the Azure portal and browse to the KeyVault.</span></span>
2. <span data-ttu-id="c2076-363">They open the certificates, and copy the thumbprint of the certificate that was created during the provisioning process.</span><span class="sxs-lookup"><span data-stu-id="c2076-363">They open the certificates, and copy the thumbprint of the certificate that was created during the provisioning process.</span></span>

    ![Copy thumbprint](./media/contoso-migration-rearchitect-container-sql/cert1.png)
 
3. <span data-ttu-id="c2076-365">They copy it to a text file for later reference.</span><span class="sxs-lookup"><span data-stu-id="c2076-365">They copy it to a text file for later reference.</span></span>
4. <span data-ttu-id="c2076-366">Now, they add a client certificate that will become an Admin client certificate on the cluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-366">Now, they add a client certificate that will become an Admin client certificate on the cluster.</span></span> <span data-ttu-id="c2076-367">This allows Azure DevOps Services to connect to the cluster for the app deployment in the release pipeline.</span><span class="sxs-lookup"><span data-stu-id="c2076-367">This allows Azure DevOps Services to connect to the cluster for the app deployment in the release pipeline.</span></span> <span data-ttu-id="c2076-368">To do they, they open KeyVault in the portal, and select **Certificates** > **Generate/Import**.</span><span class="sxs-lookup"><span data-stu-id="c2076-368">To do they, they open KeyVault in the portal, and select **Certificates** > **Generate/Import**.</span></span>

    ![Generate client cert](./media/contoso-migration-rearchitect-container-sql/cert2.png)

5. <span data-ttu-id="c2076-370">They enter the name of the certificate, and provide an X.509 distinguished name in **Subject**.</span><span class="sxs-lookup"><span data-stu-id="c2076-370">They enter the name of the certificate, and provide an X.509 distinguished name in **Subject**.</span></span>

     ![Cert name](./media/contoso-migration-rearchitect-container-sql/cert3.png)

6. <span data-ttu-id="c2076-372">After the certificate is created, they download it locally in PFX format.</span><span class="sxs-lookup"><span data-stu-id="c2076-372">After the certificate is created, they download it locally in PFX format.</span></span>

     ![Download cert](./media/contoso-migration-rearchitect-container-sql/cert4.png)

7. <span data-ttu-id="c2076-374">Now, they go back to the certificates list in the KeyVault, and copy the thumbprint of the client certificate that's just been created.</span><span class="sxs-lookup"><span data-stu-id="c2076-374">Now, they go back to the certificates list in the KeyVault, and copy the thumbprint of the client certificate that's just been created.</span></span> <span data-ttu-id="c2076-375">They save it in the text file.</span><span class="sxs-lookup"><span data-stu-id="c2076-375">They save it in the text file.</span></span>

     ![Client cert thumbprint](./media/contoso-migration-rearchitect-container-sql/cert5.png)

8. <span data-ttu-id="c2076-377">For Azure DevOps Services deployment, they need to determine the Base64 value of the certificate.</span><span class="sxs-lookup"><span data-stu-id="c2076-377">For Azure DevOps Services deployment, they need to determine the Base64 value of the certificate.</span></span> <span data-ttu-id="c2076-378">They do this on the local developer workstation using PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c2076-378">They do this on the local developer workstation using PowerShell.</span></span> <span data-ttu-id="c2076-379">They paste the output into a text file for later use.</span><span class="sxs-lookup"><span data-stu-id="c2076-379">They paste the output into a text file for later use.</span></span>

    ```
        [System.Convert]::ToBase64String([System.IO.File]::ReadAllBytes("C:\path\to\certificate.pfx")) 
    ```

     ![Base64 value](./media/contoso-migration-rearchitect-container-sql/cert6.png)

9. <span data-ttu-id="c2076-381">Finally, they add the new certificate to the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-381">Finally, they add the new certificate to the Service Fabric cluster.</span></span> <span data-ttu-id="c2076-382">To do this, in the portal they open the cluster, and click **Security**.</span><span class="sxs-lookup"><span data-stu-id="c2076-382">To do this, in the portal they open the cluster, and click **Security**.</span></span>

     ![Add client cert](./media/contoso-migration-rearchitect-container-sql/cert7.png)

10. <span data-ttu-id="c2076-384">They click **Add** > **Admin Client**, and paste in the thumbprint of the new client certificate.</span><span class="sxs-lookup"><span data-stu-id="c2076-384">They click **Add** > **Admin Client**, and paste in the thumbprint of the new client certificate.</span></span> <span data-ttu-id="c2076-385">Then they click **Add**.</span><span class="sxs-lookup"><span data-stu-id="c2076-385">Then they click **Add**.</span></span> <span data-ttu-id="c2076-386">This can take up to 15 minutes.</span><span class="sxs-lookup"><span data-stu-id="c2076-386">This can take up to 15 minutes.</span></span>

     ![Add client cert](./media/contoso-migration-rearchitect-container-sql/cert8.png)

## <a name="step-5-migrate-the-database-with-dma"></a><span data-ttu-id="c2076-388">Step 5: Migrate the database with DMA</span><span class="sxs-lookup"><span data-stu-id="c2076-388">Step 5: Migrate the database with DMA</span></span>

<span data-ttu-id="c2076-389">Contoso admins can now migrate the SmartHotel360 database using DMA.</span><span class="sxs-lookup"><span data-stu-id="c2076-389">Contoso admins can now migrate the SmartHotel360 database using DMA.</span></span>

### <a name="install-dma"></a><span data-ttu-id="c2076-390">Install DMA</span><span class="sxs-lookup"><span data-stu-id="c2076-390">Install DMA</span></span>

1. <span data-ttu-id="c2076-391">They download the tool from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) to the on-premises SQL Server VM (**SQLVM**).</span><span class="sxs-lookup"><span data-stu-id="c2076-391">They download the tool from the [Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=53595) to the on-premises SQL Server VM (**SQLVM**).</span></span>
2. <span data-ttu-id="c2076-392">They run setup (DownloadMigrationAssistant.msi) on the VM.</span><span class="sxs-lookup"><span data-stu-id="c2076-392">They run setup (DownloadMigrationAssistant.msi) on the VM.</span></span>
3. <span data-ttu-id="c2076-393">On the **Finish** page, they select **Launch Microsoft Data Migration Assistant** before finishing the wizard.</span><span class="sxs-lookup"><span data-stu-id="c2076-393">On the **Finish** page, they select **Launch Microsoft Data Migration Assistant** before finishing the wizard.</span></span>

### <a name="configure-the-firewall"></a><span data-ttu-id="c2076-394">Configure the firewall</span><span class="sxs-lookup"><span data-stu-id="c2076-394">Configure the firewall</span></span>

<span data-ttu-id="c2076-395">To connect to the Azure SQL Database, Contoso admins set up a firewall rule to allow access.</span><span class="sxs-lookup"><span data-stu-id="c2076-395">To connect to the Azure SQL Database, Contoso admins set up a firewall rule to allow access.</span></span>

1. <span data-ttu-id="c2076-396">In the **Firewall and virtual networks** properties for the database, they allow access to Azure services, and add a rule for the client IP address of the on-premises SQL Server VM.</span><span class="sxs-lookup"><span data-stu-id="c2076-396">In the **Firewall and virtual networks** properties for the database, they allow access to Azure services, and add a rule for the client IP address of the on-premises SQL Server VM.</span></span>
2. <span data-ttu-id="c2076-397">A server-level firewall rule is created.</span><span class="sxs-lookup"><span data-stu-id="c2076-397">A server-level firewall rule is created.</span></span>

    ![Firewall](./media/contoso-migration-rearchitect-container-sql/sql-firewall.png)

<span data-ttu-id="c2076-399">Need more help?</span><span class="sxs-lookup"><span data-stu-id="c2076-399">Need more help?</span></span>

<span data-ttu-id="c2076-400">[Learn about](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure#creating-and-managing-firewall-rules) creating and managing firewall rules for Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c2076-400">[Learn about](https://docs.microsoft.com/azure/sql-database/sql-database-firewall-configure#creating-and-managing-firewall-rules) creating and managing firewall rules for Azure SQL Database.</span></span>

### <a name="migrate"></a><span data-ttu-id="c2076-401">Migrate</span><span class="sxs-lookup"><span data-stu-id="c2076-401">Migrate</span></span>

<span data-ttu-id="c2076-402">Contoso admins now migrate the database.</span><span class="sxs-lookup"><span data-stu-id="c2076-402">Contoso admins now migrate the database.</span></span>

1. <span data-ttu-id="c2076-403">In the DMA create a new project (**SmartHotelDB**) and select **Migration**</span><span class="sxs-lookup"><span data-stu-id="c2076-403">In the DMA create a new project (**SmartHotelDB**) and select **Migration**</span></span> 
2. <span data-ttu-id="c2076-404">They select the source server type as **SQL Server**, and the target as **Azure SQL Database**.</span><span class="sxs-lookup"><span data-stu-id="c2076-404">They select the source server type as **SQL Server**, and the target as **Azure SQL Database**.</span></span> 

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-1.png)

3. <span data-ttu-id="c2076-406">In the migration details, they add **SQLVM** as the source server, and the **SmartHotel.Registration** database.</span><span class="sxs-lookup"><span data-stu-id="c2076-406">In the migration details, they add **SQLVM** as the source server, and the **SmartHotel.Registration** database.</span></span> 

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-2.png)

4. <span data-ttu-id="c2076-408">They receive an error which seems to be associated with authentication.</span><span class="sxs-lookup"><span data-stu-id="c2076-408">They receive an error which seems to be associated with authentication.</span></span> <span data-ttu-id="c2076-409">However after investigating, the issue is the period (.) in the database name.</span><span class="sxs-lookup"><span data-stu-id="c2076-409">However after investigating, the issue is the period (.) in the database name.</span></span> <span data-ttu-id="c2076-410">As a workaround, they decided to provision a new SQL database using the name **SmartHotel-Registration**, to resolve the issue.</span><span class="sxs-lookup"><span data-stu-id="c2076-410">As a workaround, they decided to provision a new SQL database using the name **SmartHotel-Registration**, to resolve the issue.</span></span> <span data-ttu-id="c2076-411">When they run DMA again, they're able to select **SmartHotel-Registration**, and continue with the wizard.</span><span class="sxs-lookup"><span data-stu-id="c2076-411">When they run DMA again, they're able to select **SmartHotel-Registration**, and continue with the wizard.</span></span>

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-3.png)

5. <span data-ttu-id="c2076-413">In **Select Objects**, they select the database tables, and generate a SQL script.</span><span class="sxs-lookup"><span data-stu-id="c2076-413">In **Select Objects**, they select the database tables, and generate a SQL script.</span></span>

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-4.png)

6. <span data-ttu-id="c2076-415">After DMS creates the script, they click **Deploy schema**.</span><span class="sxs-lookup"><span data-stu-id="c2076-415">After DMS creates the script, they click **Deploy schema**.</span></span>

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-5.png)

7. <span data-ttu-id="c2076-417">DMA confirms that the deployment succeeded.</span><span class="sxs-lookup"><span data-stu-id="c2076-417">DMA confirms that the deployment succeeded.</span></span>

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-6.png)

8. <span data-ttu-id="c2076-419">Now they start the migration.</span><span class="sxs-lookup"><span data-stu-id="c2076-419">Now they start the migration.</span></span>

    ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-7.png)

9. <span data-ttu-id="c2076-421">After the migration finishes, Contoso can verify that the database is running on the Azure SQL instance.</span><span class="sxs-lookup"><span data-stu-id="c2076-421">After the migration finishes, Contoso can verify that the database is running on the Azure SQL instance.</span></span>

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-8.png)

10. <span data-ttu-id="c2076-423">They delete the extra SQL database **SmartHotel.Registration** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c2076-423">They delete the extra SQL database **SmartHotel.Registration** in the Azure portal.</span></span>

     ![DMA](./media/contoso-migration-rearchitect-container-sql/dma-9.png)


## <a name="step-6-set-up-azure-devops-services"></a><span data-ttu-id="c2076-425">Step 6: Set up Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="c2076-425">Step 6: Set up Azure DevOps Services</span></span>

<span data-ttu-id="c2076-426">Contoso needs to build the DevOps infrastructure and pipelines for the application.</span><span class="sxs-lookup"><span data-stu-id="c2076-426">Contoso needs to build the DevOps infrastructure and pipelines for the application.</span></span>  <span data-ttu-id="c2076-427">To do this, Contoso admins create a new Azure DevOps project, import their code, and then build and release pipelines.</span><span class="sxs-lookup"><span data-stu-id="c2076-427">To do this, Contoso admins create a new Azure DevOps project, import their code, and then build and release pipelines.</span></span>

1.   <span data-ttu-id="c2076-428">In the Contoso Azure DevOps account, they create a new project (**ContosoSmartHotelRearchitect**), and select **Git** for version control.</span><span class="sxs-lookup"><span data-stu-id="c2076-428">In the Contoso Azure DevOps account, they create a new project (**ContosoSmartHotelRearchitect**), and select **Git** for version control.</span></span>

    ![New project](./media/contoso-migration-rearchitect-container-sql/vsts1.png)

2. <span data-ttu-id="c2076-430">They import the Git Repo that currently holds their app code.</span><span class="sxs-lookup"><span data-stu-id="c2076-430">They import the Git Repo that currently holds their app code.</span></span> <span data-ttu-id="c2076-431">It's in a [public repo](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) and you can download it.</span><span class="sxs-lookup"><span data-stu-id="c2076-431">It's in a [public repo](https://github.com/Microsoft/SmartHotel360-internal-booking-apps) and you can download it.</span></span>

    ![Download app code](./media/contoso-migration-rearchitect-container-sql/vsts2.png)

3. <span data-ttu-id="c2076-433">After the code is imported, they connect Visual Studio to the repo, and clone the code using Team Explorer.</span><span class="sxs-lookup"><span data-stu-id="c2076-433">After the code is imported, they connect Visual Studio to the repo, and clone the code using Team Explorer.</span></span>

    ![Connect to repo](./media/contoso-migration-rearchitect-container-sql/vsts3.png)

4. <span data-ttu-id="c2076-435">After the repo is cloned to the developer machine, they open the Solution file for the app.</span><span class="sxs-lookup"><span data-stu-id="c2076-435">After the repo is cloned to the developer machine, they open the Solution file for the app.</span></span> <span data-ttu-id="c2076-436">The web app and wcf service each have separate project within the file.</span><span class="sxs-lookup"><span data-stu-id="c2076-436">The web app and wcf service each have separate project within the file.</span></span>

    ![Solution file](./media/contoso-migration-rearchitect-container-sql/vsts4.png)

## <a name="step-7-convert-the-app-to-a-container"></a><span data-ttu-id="c2076-438">Step 7: Convert the app to a container</span><span class="sxs-lookup"><span data-stu-id="c2076-438">Step 7: Convert the app to a container</span></span>

<span data-ttu-id="c2076-439">The  on-premises app is a traditional three tier app:</span><span class="sxs-lookup"><span data-stu-id="c2076-439">The  on-premises app is a traditional three tier app:</span></span>

- <span data-ttu-id="c2076-440">It contains WebForms and a WCF Service connecting to SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c2076-440">It contains WebForms and a WCF Service connecting to SQL Server.</span></span>
- <span data-ttu-id="c2076-441">It uses Entity Framework to integrate with the data in the SQL database, exposing it through a WCF service.</span><span class="sxs-lookup"><span data-stu-id="c2076-441">It uses Entity Framework to integrate with the data in the SQL database, exposing it through a WCF service.</span></span>
- <span data-ttu-id="c2076-442">The WebForms application  interacts with the WCF service.</span><span class="sxs-lookup"><span data-stu-id="c2076-442">The WebForms application  interacts with the WCF service.</span></span>

<span data-ttu-id="c2076-443">Contoso admins will convert the app to a container using isual Studio and the SDK Tools, as follows:</span><span class="sxs-lookup"><span data-stu-id="c2076-443">Contoso admins will convert the app to a container using isual Studio and the SDK Tools, as follows:</span></span>


1. <span data-ttu-id="c2076-444">Using Visual Studio, they review the open solution file (SmartHotel.Registration.sln) in the **SmartHotel360-internal-booking-apps\src\Registration** directory of the local repo.</span><span class="sxs-lookup"><span data-stu-id="c2076-444">Using Visual Studio, they review the open solution file (SmartHotel.Registration.sln) in the **SmartHotel360-internal-booking-apps\src\Registration** directory of the local repo.</span></span>  <span data-ttu-id="c2076-445">Two apps are shown.</span><span class="sxs-lookup"><span data-stu-id="c2076-445">Two apps are shown.</span></span> <span data-ttu-id="c2076-446">The web frontend SmartHotel.Registration.Web and the WCF service app SmartHotel.Registration.WCF.</span><span class="sxs-lookup"><span data-stu-id="c2076-446">The web frontend SmartHotel.Registration.Web and the WCF service app SmartHotel.Registration.WCF.</span></span>

    ![Container](./media/contoso-migration-rearchitect-container-sql/container2.png)


2. <span data-ttu-id="c2076-448">They right-click the web app > **Add** > **Container Orchestrator Support**.</span><span class="sxs-lookup"><span data-stu-id="c2076-448">They right-click the web app > **Add** > **Container Orchestrator Support**.</span></span>
3. <span data-ttu-id="c2076-449">In **Add Container Orchestra Support**, they select **Service Fabric**.</span><span class="sxs-lookup"><span data-stu-id="c2076-449">In **Add Container Orchestra Support**, they select **Service Fabric**.</span></span>

    ![Container](./media/contoso-migration-rearchitect-container-sql/container3.png)
    
4. <span data-ttu-id="c2076-451">They repeat the process for SmartHotel.Registration.WCF app.</span><span class="sxs-lookup"><span data-stu-id="c2076-451">They repeat the process for SmartHotel.Registration.WCF app.</span></span>
5. <span data-ttu-id="c2076-452">Now, they check how the solution has changed.</span><span class="sxs-lookup"><span data-stu-id="c2076-452">Now, they check how the solution has changed.</span></span>

    - <span data-ttu-id="c2076-453">The new app is **SmartHotel.RegistrationApplication/**</span><span class="sxs-lookup"><span data-stu-id="c2076-453">The new app is **SmartHotel.RegistrationApplication/**</span></span>
    - <span data-ttu-id="c2076-454">It contains two services: **SmartHotel.Registration.WCF** and **SmartHotel.Registration.Web**.</span><span class="sxs-lookup"><span data-stu-id="c2076-454">It contains two services: **SmartHotel.Registration.WCF** and **SmartHotel.Registration.Web**.</span></span>

    ![Container](./media/contoso-migration-rearchitect-container-sql/container4.png)

6. <span data-ttu-id="c2076-456">Visual Studio created the Docker file, and pulled down the required images locally to the developer machine.</span><span class="sxs-lookup"><span data-stu-id="c2076-456">Visual Studio created the Docker file, and pulled down the required images locally to the developer machine.</span></span>

    ![Container](./media/contoso-migration-rearchitect-container-sql/container5.png)

7. <span data-ttu-id="c2076-458">A manifest file (**ServiceManifest.xml**) is created and opened by Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c2076-458">A manifest file (**ServiceManifest.xml**) is created and opened by Visual Studio.</span></span> <span data-ttu-id="c2076-459">This file tells Service Fabric how to configure the container when it's deployed to Azure.</span><span class="sxs-lookup"><span data-stu-id="c2076-459">This file tells Service Fabric how to configure the container when it's deployed to Azure.</span></span>

    ![Container](./media/contoso-migration-rearchitect-container-sql/container6.png)

8. <span data-ttu-id="c2076-461">Another manifest file (\*\*ApplicationManifest.xml) contains the configuration applications for the containers.</span><span class="sxs-lookup"><span data-stu-id="c2076-461">Another manifest file (\*\*ApplicationManifest.xml) contains the configuration applications for the containers.</span></span>

    ![Container](./media/contoso-migration-rearchitect-container-sql/container7.png)

9. <span data-ttu-id="c2076-463">They open the **ApplicationParameters/Cloud.xml** file, and update the connection string to connect the app to the Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c2076-463">They open the **ApplicationParameters/Cloud.xml** file, and update the connection string to connect the app to the Azure SQL database.</span></span> <span data-ttu-id="c2076-464">The connection string can be located in the database in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="c2076-464">The connection string can be located in the database in the Azure portal.</span></span>

    ![Connection string](./media/contoso-migration-rearchitect-container-sql/container8.png)

10. <span data-ttu-id="c2076-466">They commit the updated code and push to Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="c2076-466">They commit the updated code and push to Azure DevOps Services.</span></span>

    ![Commit](./media/contoso-migration-rearchitect-container-sql/container9.png)

## <a name="step-8-build-and-release-pipelines-in-azure-devops-services"></a><span data-ttu-id="c2076-468">Step 8: Build and release pipelines in Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="c2076-468">Step 8: Build and release pipelines in Azure DevOps Services</span></span>

<span data-ttu-id="c2076-469">Contoso admins now configure Azure DevOps Services to perform build and release process to action the DevOps practices.</span><span class="sxs-lookup"><span data-stu-id="c2076-469">Contoso admins now configure Azure DevOps Services to perform build and release process to action the DevOps practices.</span></span>

1. <span data-ttu-id="c2076-470">In Azure DevOps Services, they click **Build and release** > **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="c2076-470">In Azure DevOps Services, they click **Build and release** > **New pipeline**.</span></span>

    ![New pipeline](./media/contoso-migration-rearchitect-container-sql/pipeline1.png)

2. <span data-ttu-id="c2076-472">They select **Azure DevOps Services Git** and the relevant repo.</span><span class="sxs-lookup"><span data-stu-id="c2076-472">They select **Azure DevOps Services Git** and the relevant repo.</span></span>

    ![Git and repo](./media/contoso-migration-rearchitect-container-sql/pipeline2.png)

3. <span data-ttu-id="c2076-474">In **Select a template**, they select fabric with Docker support.</span><span class="sxs-lookup"><span data-stu-id="c2076-474">In **Select a template**, they select fabric with Docker support.</span></span>

     ![Fabric and Docker](./media/contoso-migration-rearchitect-container-sql/pipeline3.png)
    
4. <span data-ttu-id="c2076-476">They change the tag images to build image, and configure the task to use the provisioned ACR.</span><span class="sxs-lookup"><span data-stu-id="c2076-476">They change the tag images to build image, and configure the task to use the provisioned ACR.</span></span>

     ![Registry](./media/contoso-migration-rearchitect-container-sql/pipeline4.png)

5. <span data-ttu-id="c2076-478">In the **Push images** task, they configure the image to be puhed to the ACR, and select to include the latest tag.</span><span class="sxs-lookup"><span data-stu-id="c2076-478">In the **Push images** task, they configure the image to be puhed to the ACR, and select to include the latest tag.</span></span>
6. <span data-ttu-id="c2076-479">In **Triggers**, they enable continuous integration, and add the master branch.</span><span class="sxs-lookup"><span data-stu-id="c2076-479">In **Triggers**, they enable continuous integration, and add the master branch.</span></span>

    ![Triggers](./media/contoso-migration-rearchitect-container-sql/pipeline5.png)

7. <span data-ttu-id="c2076-481">They click **Save and Queue** to start a build.</span><span class="sxs-lookup"><span data-stu-id="c2076-481">They click **Save and Queue** to start a build.</span></span>
8. <span data-ttu-id="c2076-482">After the build succeeds, they move onto the release pipeline.</span><span class="sxs-lookup"><span data-stu-id="c2076-482">After the build succeeds, they move onto the release pipeline.</span></span> <span data-ttu-id="c2076-483">In Azure DevOps Services they click **Releases** > **New pipeline**.</span><span class="sxs-lookup"><span data-stu-id="c2076-483">In Azure DevOps Services they click **Releases** > **New pipeline**.</span></span>

    ![Release pipeline](./media/contoso-migration-rearchitect-container-sql/pipeline6.png)    

9. <span data-ttu-id="c2076-485">They select the **Azure Service Fabric deployment** template, and name the environment (**SmartHotelSF**).</span><span class="sxs-lookup"><span data-stu-id="c2076-485">They select the **Azure Service Fabric deployment** template, and name the environment (**SmartHotelSF**).</span></span>

    ![Environment](./media/contoso-migration-rearchitect-container-sql/pipeline7.png)

10. <span data-ttu-id="c2076-487">They provide a pipeline name (**ContosoSmartHotelRearchitect**).</span><span class="sxs-lookup"><span data-stu-id="c2076-487">They provide a pipeline name (**ContosoSmartHotelRearchitect**).</span></span> <span data-ttu-id="c2076-488">For the environment, they click **1 phase, 1 task** to configure the Service Fabric deployment.</span><span class="sxs-lookup"><span data-stu-id="c2076-488">For the environment, they click **1 phase, 1 task** to configure the Service Fabric deployment.</span></span>

    ![Phase and task](./media/contoso-migration-rearchitect-container-sql/pipeline8.png)

11. <span data-ttu-id="c2076-490">Now, they click **New** to add a new cluster connection.</span><span class="sxs-lookup"><span data-stu-id="c2076-490">Now, they click **New** to add a new cluster connection.</span></span>

    ![New connection](./media/contoso-migration-rearchitect-container-sql/pipeline9.png)

12. <span data-ttu-id="c2076-492">In **Add Service Fabric service connection**, they configure the connection, and the authentication settings that will be used by Azure DevOps Services to deploy the app.</span><span class="sxs-lookup"><span data-stu-id="c2076-492">In **Add Service Fabric service connection**, they configure the connection, and the authentication settings that will be used by Azure DevOps Services to deploy the app.</span></span> <span data-ttu-id="c2076-493">The cluster endpoint can be located in the Azure portal, and they add **tcp://** as a prefix.</span><span class="sxs-lookup"><span data-stu-id="c2076-493">The cluster endpoint can be located in the Azure portal, and they add **tcp://** as a prefix.</span></span>
13. <span data-ttu-id="c2076-494">The certificate information they collected is input in **Server Certificate Thumbprint** and **Client Certificate**.</span><span class="sxs-lookup"><span data-stu-id="c2076-494">The certificate information they collected is input in **Server Certificate Thumbprint** and **Client Certificate**.</span></span>

    ![Certificate](./media/contoso-migration-rearchitect-container-sql/pipeline10.png)

13. <span data-ttu-id="c2076-496">They click the pipeline > **Add an artifact**.</span><span class="sxs-lookup"><span data-stu-id="c2076-496">They click the pipeline > **Add an artifact**.</span></span>

     ![Artifact](./media/contoso-migration-rearchitect-container-sql/pipeline11.png)

14. <span data-ttu-id="c2076-498">They select the project and build pipeline, using the latest version.</span><span class="sxs-lookup"><span data-stu-id="c2076-498">They select the project and build pipeline, using the latest version.</span></span>

     ![Build](./media/contoso-migration-rearchitect-container-sql/pipeline12.png)

15. <span data-ttu-id="c2076-500">Note that the lightning bolt on the artifact is checked.</span><span class="sxs-lookup"><span data-stu-id="c2076-500">Note that the lightning bolt on the artifact is checked.</span></span>

     ![Artifact status](./media/contoso-migration-rearchitect-container-sql/pipeline13.png)

16. <span data-ttu-id="c2076-502">In addition, note that the continuous deployment trigger is enabled.</span><span class="sxs-lookup"><span data-stu-id="c2076-502">In addition, note that the continuous deployment trigger is enabled.</span></span>

   ![Continuous deployment enabled](./media/contoso-migration-rearchitect-container-sql/pipeline14.png) 

17. <span data-ttu-id="c2076-504">They click **Save** > **Create a release**.</span><span class="sxs-lookup"><span data-stu-id="c2076-504">They click **Save** > **Create a release**.</span></span>

    ![Release](./media/contoso-migration-rearchitect-container-sql/pipeline15.png)

18. <span data-ttu-id="c2076-506">After the deployment finishes, SmartHotel360 will now be running Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c2076-506">After the deployment finishes, SmartHotel360 will now be running Service Fabric.</span></span>

    ![Publish](./media/contoso-migration-rearchitect-container-sql/publish4.png)

19. <span data-ttu-id="c2076-508">To connect to the app, they directs traffic to the public IP address of the Azure load balancer in front of their Service Fabric nodes.</span><span class="sxs-lookup"><span data-stu-id="c2076-508">To connect to the app, they directs traffic to the public IP address of the Azure load balancer in front of their Service Fabric nodes.</span></span>

    ![Publish](./media/contoso-migration-rearchitect-container-sql/publish5.png)

## <a name="step-9-extend-the-app-and-republish"></a><span data-ttu-id="c2076-510">Step 9: Extend the app and republish</span><span class="sxs-lookup"><span data-stu-id="c2076-510">Step 9: Extend the app and republish</span></span>

<span data-ttu-id="c2076-511">After the SmartHotel360 app and database are running in Azure, Contoso wants to extend the app.</span><span class="sxs-lookup"><span data-stu-id="c2076-511">After the SmartHotel360 app and database are running in Azure, Contoso wants to extend the app.</span></span>

- <span data-ttu-id="c2076-512">Contoso’s developers are prototyping a new .NET Core application which will run on the Service Fabric cluster.</span><span class="sxs-lookup"><span data-stu-id="c2076-512">Contoso’s developers are prototyping a new .NET Core application which will run on the Service Fabric cluster.</span></span>
- <span data-ttu-id="c2076-513">The app will be used to pull sentiment data from CosmosDB.</span><span class="sxs-lookup"><span data-stu-id="c2076-513">The app will be used to pull sentiment data from CosmosDB.</span></span>
- <span data-ttu-id="c2076-514">This data will be in the form of Tweets that are processed using a Serverless Azure Function, and the Cognitive Services Text Analysis API.</span><span class="sxs-lookup"><span data-stu-id="c2076-514">This data will be in the form of Tweets that are processed using a Serverless Azure Function, and the Cognitive Services Text Analysis API.</span></span>

### <a name="provision-azure-cosmos-db"></a><span data-ttu-id="c2076-515">Provision Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="c2076-515">Provision Azure Cosmos DB</span></span>

<span data-ttu-id="c2076-516">As a first step, Contoso admins provision an Azure Cosmos database.</span><span class="sxs-lookup"><span data-stu-id="c2076-516">As a first step, Contoso admins provision an Azure Cosmos database.</span></span>

1. <span data-ttu-id="c2076-517">They create an Azure Cosmos DB resource from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="c2076-517">They create an Azure Cosmos DB resource from the Azure Marketplace.</span></span>

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend1.png)

2. <span data-ttu-id="c2076-519">They provide a database name (**contososmarthotel**), select the SQL API, and place the resource in the production resource group, in the primary East US 2 region.</span><span class="sxs-lookup"><span data-stu-id="c2076-519">They provide a database name (**contososmarthotel**), select the SQL API, and place the resource in the production resource group, in the primary East US 2 region.</span></span>

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend2.png)

3. <span data-ttu-id="c2076-521">In **Getting Started**, they select **Data Explorer**, and add a new collection.</span><span class="sxs-lookup"><span data-stu-id="c2076-521">In **Getting Started**, they select **Data Explorer**, and add a new collection.</span></span>
4. <span data-ttu-id="c2076-522">In **Add Collection** they provide IDs and set storage capacity and throughput.</span><span class="sxs-lookup"><span data-stu-id="c2076-522">In **Add Collection** they provide IDs and set storage capacity and throughput.</span></span>

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend3.png)

5. <span data-ttu-id="c2076-524">In the portal, they open the new database > **Collection** > **Documents** and click **New Document**.</span><span class="sxs-lookup"><span data-stu-id="c2076-524">In the portal, they open the new database > **Collection** > **Documents** and click **New Document**.</span></span>
6. <span data-ttu-id="c2076-525">They paste the following JSON code into the document window.</span><span class="sxs-lookup"><span data-stu-id="c2076-525">They paste the following JSON code into the document window.</span></span> <span data-ttu-id="c2076-526">This is sample data in the form of a single tweet.</span><span class="sxs-lookup"><span data-stu-id="c2076-526">This is sample data in the form of a single tweet.</span></span>

    ```
    {
            "id": "2ed5e734-8034-bf3a-ac85-705b7713d911",
            "tweetId": 927750234331580911,
            "tweetUrl": "https://twitter.com/status/927750237331580911",
            "userName": "CoreySandersWA",
            "userAlias": "@CoreySandersWA",
            "userPictureUrl": "",
            "text": "This is a tweet about #SmartHotel360",
            "language": "en",
            "sentiment": 0.5,
            "retweet_count": 1,
            "followers": 500, 
            "hashtags": [
                ""
            ]
    }
    ```

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend4.png)

7. <span data-ttu-id="c2076-528">They locate the Cosmos DB endpoint, and the authentication key.</span><span class="sxs-lookup"><span data-stu-id="c2076-528">They locate the Cosmos DB endpoint, and the authentication key.</span></span> <span data-ttu-id="c2076-529">These are used in the app to connect to the collection.</span><span class="sxs-lookup"><span data-stu-id="c2076-529">These are used in the app to connect to the collection.</span></span> <span data-ttu-id="c2076-530">In the database, they click **Keys**, and copy the URI and primary key to Notepad.</span><span class="sxs-lookup"><span data-stu-id="c2076-530">In the database, they click **Keys**, and copy the URI and primary key to Notepad.</span></span>

    ![Extend](./media/contoso-migration-rearchitect-container-sql/extend5.png)

### <a name="update-the-sentiment-app"></a><span data-ttu-id="c2076-532">Update the sentiment app</span><span class="sxs-lookup"><span data-stu-id="c2076-532">Update the sentiment app</span></span>

<span data-ttu-id="c2076-533">With the Cosmos DB provisioned, Contoso admins can configure the app to connect to it.</span><span class="sxs-lookup"><span data-stu-id="c2076-533">With the Cosmos DB provisioned, Contoso admins can configure the app to connect to it.</span></span>

1. <span data-ttu-id="c2076-534">In Visual Studio, they open file ApplicationModern\ApplicationParameters\cloud.xml in Solution Explorer.</span><span class="sxs-lookup"><span data-stu-id="c2076-534">In Visual Studio, they open file ApplicationModern\ApplicationParameters\cloud.xml in Solution Explorer.</span></span>

    ![Sentiment app](./media/contoso-migration-rearchitect-container-sql/sentiment1.png)

2. <span data-ttu-id="c2076-536">They fill in the following two parameters:</span><span class="sxs-lookup"><span data-stu-id="c2076-536">They fill in the following two parameters:</span></span>

   ```
   <Parameter Name="SentimentIntegration.CosmosDBEndpoint" Value="[URI]" />
   ```
   
   ```
   <Parameter Name="SentimentIntegration.CosmosDBAuthKey" Value="[Key]" />
   ```

    ![Sentiment app](./media/contoso-migration-rearchitect-container-sql/sentiment2.png)

### <a name="republish-the-app"></a><span data-ttu-id="c2076-538">Republish the app</span><span class="sxs-lookup"><span data-stu-id="c2076-538">Republish the app</span></span>

<span data-ttu-id="c2076-539">After extending the app, Contoso admins republish it to Azure using the pipeline.</span><span class="sxs-lookup"><span data-stu-id="c2076-539">After extending the app, Contoso admins republish it to Azure using the pipeline.</span></span>

1. <span data-ttu-id="c2076-540">They commit and push their code to Azure DevOps Services.</span><span class="sxs-lookup"><span data-stu-id="c2076-540">They commit and push their code to Azure DevOps Services.</span></span> <span data-ttu-id="c2076-541">This kicks off the build and release pipelines.</span><span class="sxs-lookup"><span data-stu-id="c2076-541">This kicks off the build and release pipelines.</span></span>

2. <span data-ttu-id="c2076-542">After the build and deployment finishes, SmartHotel360 will now be running Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c2076-542">After the build and deployment finishes, SmartHotel360 will now be running Service Fabric.</span></span> <span data-ttu-id="c2076-543">The Servie Fabric Management console now shows three services.</span><span class="sxs-lookup"><span data-stu-id="c2076-543">The Servie Fabric Management console now shows three services.</span></span>

    ![Republish](./media/contoso-migration-rearchitect-container-sql/republish3.png)

3. <span data-ttu-id="c2076-545">They can now click through the services to see that the SentimentIntegration app is up and running</span><span class="sxs-lookup"><span data-stu-id="c2076-545">They can now click through the services to see that the SentimentIntegration app is up and running</span></span>

    ![Republish](./media/contoso-migration-rearchitect-container-sql/republish4.png)

## <a name="clean-up-after-migration"></a><span data-ttu-id="c2076-547">Clean up after migration</span><span class="sxs-lookup"><span data-stu-id="c2076-547">Clean up after migration</span></span>

<span data-ttu-id="c2076-548">After migration, Contoso needs to complete these cleanup steps:</span><span class="sxs-lookup"><span data-stu-id="c2076-548">After migration, Contoso needs to complete these cleanup steps:</span></span>  

- <span data-ttu-id="c2076-549">Remove the on-premises VMs from the vCenter inventory.</span><span class="sxs-lookup"><span data-stu-id="c2076-549">Remove the on-premises VMs from the vCenter inventory.</span></span>
- <span data-ttu-id="c2076-550">Remove the VMs from local backup jobs.</span><span class="sxs-lookup"><span data-stu-id="c2076-550">Remove the VMs from local backup jobs.</span></span>
- <span data-ttu-id="c2076-551">Update internal documentation to show the new locations for the SmartHotel360 app.</span><span class="sxs-lookup"><span data-stu-id="c2076-551">Update internal documentation to show the new locations for the SmartHotel360 app.</span></span> <span data-ttu-id="c2076-552">Show the database as running in Azure SQL database, and the front end as running in Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c2076-552">Show the database as running in Azure SQL database, and the front end as running in Service Fabric.</span></span>
- <span data-ttu-id="c2076-553">Review any resources that interact with the decommissioned VMs, and update any relevant settings or documentation to reflect the new configuration.</span><span class="sxs-lookup"><span data-stu-id="c2076-553">Review any resources that interact with the decommissioned VMs, and update any relevant settings or documentation to reflect the new configuration.</span></span>


## <a name="review-the-deployment"></a><span data-ttu-id="c2076-554">Review the deployment</span><span class="sxs-lookup"><span data-stu-id="c2076-554">Review the deployment</span></span>

<span data-ttu-id="c2076-555">With the migrated resources in Azure, Contoso needs to fully operationalize and secure their new infrastructure.</span><span class="sxs-lookup"><span data-stu-id="c2076-555">With the migrated resources in Azure, Contoso needs to fully operationalize and secure their new infrastructure.</span></span>

### <a name="security"></a><span data-ttu-id="c2076-556">Security</span><span class="sxs-lookup"><span data-stu-id="c2076-556">Security</span></span>

- <span data-ttu-id="c2076-557">Contoso admins need to ensure that their new **SmartHotel-Registration** database is secure.</span><span class="sxs-lookup"><span data-stu-id="c2076-557">Contoso admins need to ensure that their new **SmartHotel-Registration** database is secure.</span></span> <span data-ttu-id="c2076-558">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).</span><span class="sxs-lookup"><span data-stu-id="c2076-558">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-security-overview).</span></span>
- <span data-ttu-id="c2076-559">In particular, they should update the container to use SSL with certificates.</span><span class="sxs-lookup"><span data-stu-id="c2076-559">In particular, they should update the container to use SSL with certificates.</span></span>
- <span data-ttu-id="c2076-560">They should consider using KeyVault to protect secrets for their Service Fabric apps.</span><span class="sxs-lookup"><span data-stu-id="c2076-560">They should consider using KeyVault to protect secrets for their Service Fabric apps.</span></span> <span data-ttu-id="c2076-561">[Learn more](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).</span><span class="sxs-lookup"><span data-stu-id="c2076-561">[Learn more](https://docs.microsoft.com/azure/service-fabric/service-fabric-application-secret-management).</span></span>

### <a name="backups"></a><span data-ttu-id="c2076-562">Backups</span><span class="sxs-lookup"><span data-stu-id="c2076-562">Backups</span></span>

- <span data-ttu-id="c2076-563">Contoso needs to review backup requirements for the Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="c2076-563">Contoso needs to review backup requirements for the Azure SQL Database.</span></span> <span data-ttu-id="c2076-564">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).</span><span class="sxs-lookup"><span data-stu-id="c2076-564">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-automated-backups).</span></span>
- <span data-ttu-id="c2076-565">Contoso admins should consider implementing failover groups to provide regional failover for the database.</span><span class="sxs-lookup"><span data-stu-id="c2076-565">Contoso admins should consider implementing failover groups to provide regional failover for the database.</span></span> <span data-ttu-id="c2076-566">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).</span><span class="sxs-lookup"><span data-stu-id="c2076-566">[Learn more](https://docs.microsoft.com/azure/sql-database/sql-database-geo-replication-overview).</span></span>
- <span data-ttu-id="c2076-567">They can leverage geo-replication for the ACR premium SKU.</span><span class="sxs-lookup"><span data-stu-id="c2076-567">They can leverage geo-replication for the ACR premium SKU.</span></span> <span data-ttu-id="c2076-568">[Learn more](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).</span><span class="sxs-lookup"><span data-stu-id="c2076-568">[Learn more](https://docs.microsoft.com/azure/container-registry/container-registry-geo-replication).</span></span>
- <span data-ttu-id="c2076-569">Contoso need to consider deploying the Web App in the main East US 2 and Central US region when Web App for Containers becomes available.</span><span class="sxs-lookup"><span data-stu-id="c2076-569">Contoso need to consider deploying the Web App in the main East US 2 and Central US region when Web App for Containers becomes available.</span></span> <span data-ttu-id="c2076-570">Contoso admins could configure Traffic Manager to ensure failover in case of regional outages.</span><span class="sxs-lookup"><span data-stu-id="c2076-570">Contoso admins could configure Traffic Manager to ensure failover in case of regional outages.</span></span>
- <span data-ttu-id="c2076-571">Cosmos DB backs up automatically.</span><span class="sxs-lookup"><span data-stu-id="c2076-571">Cosmos DB backs up automatically.</span></span> <span data-ttu-id="c2076-572">Contoso [read about](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore) this process to learn more.</span><span class="sxs-lookup"><span data-stu-id="c2076-572">Contoso [read about](https://docs.microsoft.com/azure/cosmos-db/online-backup-and-restore) this process to learn more.</span></span>

### <a name="licensing-and-cost-optimization"></a><span data-ttu-id="c2076-573">Licensing and cost optimization</span><span class="sxs-lookup"><span data-stu-id="c2076-573">Licensing and cost optimization</span></span>

- <span data-ttu-id="c2076-574">After all resources are deployed, Contoso should assign Azure tags based on  [infrastructure planning](contoso-migration-infrastructure.md#set-up-tagging).</span><span class="sxs-lookup"><span data-stu-id="c2076-574">After all resources are deployed, Contoso should assign Azure tags based on  [infrastructure planning](contoso-migration-infrastructure.md#set-up-tagging).</span></span>
- <span data-ttu-id="c2076-575">All licensing is built into the cost of the PaaS services that Contoso is consuming.</span><span class="sxs-lookup"><span data-stu-id="c2076-575">All licensing is built into the cost of the PaaS services that Contoso is consuming.</span></span> <span data-ttu-id="c2076-576">This will be deducted from the EA.</span><span class="sxs-lookup"><span data-stu-id="c2076-576">This will be deducted from the EA.</span></span>
- <span data-ttu-id="c2076-577">Contoso will enable Azure Cost Management licensed by Cloudyn, a Microsoft subsidiary.</span><span class="sxs-lookup"><span data-stu-id="c2076-577">Contoso will enable Azure Cost Management licensed by Cloudyn, a Microsoft subsidiary.</span></span> <span data-ttu-id="c2076-578">It's a multi-cloud cost management solution that helps you to utilize and manage Azure and other cloud resources.</span><span class="sxs-lookup"><span data-stu-id="c2076-578">It's a multi-cloud cost management solution that helps you to utilize and manage Azure and other cloud resources.</span></span>  <span data-ttu-id="c2076-579">[Learn more](https://docs.microsoft.com/azure/cost-management/overview) about Azure Cost Management.</span><span class="sxs-lookup"><span data-stu-id="c2076-579">[Learn more](https://docs.microsoft.com/azure/cost-management/overview) about Azure Cost Management.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c2076-580">Conclusion</span><span class="sxs-lookup"><span data-stu-id="c2076-580">Conclusion</span></span>

<span data-ttu-id="c2076-581">In this article, Contoso refactored the SmartHotel360 app in Azure by migrating the app frontend VM to Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c2076-581">In this article, Contoso refactored the SmartHotel360 app in Azure by migrating the app frontend VM to Service Fabric.</span></span> <span data-ttu-id="c2076-582">The app database was migrated to an Azure SQL database.</span><span class="sxs-lookup"><span data-stu-id="c2076-582">The app database was migrated to an Azure SQL database.</span></span>





