---
title: Refactor a Contoso Linux service desk app to the Azure App Service and Azure MySQL | Microsoft Docs
description: Learn how Contoso refactors on-premises Linux app by migrating it to Azure App Service using GitHub for Web Tier and Azure SQL Database.
author: rayne-wiselman
ms.service: site-recovery
ms.topic: conceptual
ms.date: 09/05/2018
ms.author: raynew
ms.openlocfilehash: 3f85d9d18aa49a378c63fa1f1692c7dc665489be
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869450"
---
# <a name="contoso-migration-refactor-a-contoso-linux-service-desk-app-to-multiple-regions-with-azure-app-service-traffic-manager-and-azure-mysql"></a><span data-ttu-id="0cc86-103">Contoso migration: Refactor a Contoso Linux service desk app to multiple regions with Azure App Service, Traffic Manager, and Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="0cc86-103">Contoso migration: Refactor a Contoso Linux service desk app to multiple regions with Azure App Service, Traffic Manager, and Azure MySQL</span></span>

<span data-ttu-id="0cc86-104">This article shows how Contoso refactors their on-premises two-tier Linux service desk app (osTicket), by migrating it to Azure App Service with GitHub integration, and Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="0cc86-104">This article shows how Contoso refactors their on-premises two-tier Linux service desk app (osTicket), by migrating it to Azure App Service with GitHub integration, and Azure MySQL.</span></span>

<span data-ttu-id="0cc86-105">This document is one in a series of articles that show how the fictitious company Contoso migrates its on-premises resources to the Microsoft Azure cloud.</span><span class="sxs-lookup"><span data-stu-id="0cc86-105">This document is one in a series of articles that show how the fictitious company Contoso migrates its on-premises resources to the Microsoft Azure cloud.</span></span> <span data-ttu-id="0cc86-106">The series includes background information, and scenarios that illustrate how to set up a migration infrastructure, and run different types of migrations.</span><span class="sxs-lookup"><span data-stu-id="0cc86-106">The series includes background information, and scenarios that illustrate how to set up a migration infrastructure, and run different types of migrations.</span></span> <span data-ttu-id="0cc86-107">Scenarios grow in complexity.</span><span class="sxs-lookup"><span data-stu-id="0cc86-107">Scenarios grow in complexity.</span></span> <span data-ttu-id="0cc86-108">We'll add additional articles over time.</span><span class="sxs-lookup"><span data-stu-id="0cc86-108">We'll add additional articles over time.</span></span>

<span data-ttu-id="0cc86-109">**Article**</span><span class="sxs-lookup"><span data-stu-id="0cc86-109">**Article**</span></span> | <span data-ttu-id="0cc86-110">**Details**</span><span class="sxs-lookup"><span data-stu-id="0cc86-110">**Details**</span></span> | <span data-ttu-id="0cc86-111">**Status**</span><span class="sxs-lookup"><span data-stu-id="0cc86-111">**Status**</span></span>
--- | --- | ---
[<span data-ttu-id="0cc86-112">Article 1: Overview</span><span class="sxs-lookup"><span data-stu-id="0cc86-112">Article 1: Overview</span></span>](contoso-migration-overview.md) | <span data-ttu-id="0cc86-113">Overview of the article series, Contoso's migration strategy, and the sample apps that are used in the series.</span><span class="sxs-lookup"><span data-stu-id="0cc86-113">Overview of the article series, Contoso's migration strategy, and the sample apps that are used in the series.</span></span> | <span data-ttu-id="0cc86-114">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-114">Available</span></span>
[<span data-ttu-id="0cc86-115">Article 2: Deploy Azure infrastructure</span><span class="sxs-lookup"><span data-stu-id="0cc86-115">Article 2: Deploy Azure infrastructure</span></span>](contoso-migration-infrastructure.md) | <span data-ttu-id="0cc86-116">Contoso prepares its on-premises infrastructure and its Azure infrastructure for migration.</span><span class="sxs-lookup"><span data-stu-id="0cc86-116">Contoso prepares its on-premises infrastructure and its Azure infrastructure for migration.</span></span> <span data-ttu-id="0cc86-117">The same infrastructure is used for all migration articles in the series.</span><span class="sxs-lookup"><span data-stu-id="0cc86-117">The same infrastructure is used for all migration articles in the series.</span></span> | <span data-ttu-id="0cc86-118">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-118">Available</span></span>
[<span data-ttu-id="0cc86-119">Article 3: Assess on-premises resources for migration to Azure</span><span class="sxs-lookup"><span data-stu-id="0cc86-119">Article 3: Assess on-premises resources for migration to Azure</span></span>](contoso-migration-assessment.md)  | <span data-ttu-id="0cc86-120">Contoso runs an assessment of its on-premises SmartHotel360 app running on VMware.</span><span class="sxs-lookup"><span data-stu-id="0cc86-120">Contoso runs an assessment of its on-premises SmartHotel360 app running on VMware.</span></span> <span data-ttu-id="0cc86-121">Contoso assesses app VMs using the Azure Migrate service, and the app SQL Server database using Data Migration Assistant.</span><span class="sxs-lookup"><span data-stu-id="0cc86-121">Contoso assesses app VMs using the Azure Migrate service, and the app SQL Server database using Data Migration Assistant.</span></span> | <span data-ttu-id="0cc86-122">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-122">Available</span></span>
[<span data-ttu-id="0cc86-123">Article 4: Rehost an app on an Azure VM and SQL Database Managed Instance</span><span class="sxs-lookup"><span data-stu-id="0cc86-123">Article 4: Rehost an app on an Azure VM and SQL Database Managed Instance</span></span>](contoso-migration-rehost-vm-sql-managed-instance.md) | <span data-ttu-id="0cc86-124">Contoso runs a lift-and-shift migration to Azure for its on-premises SmartHotel360 app.</span><span class="sxs-lookup"><span data-stu-id="0cc86-124">Contoso runs a lift-and-shift migration to Azure for its on-premises SmartHotel360 app.</span></span> <span data-ttu-id="0cc86-125">Contoso migrates the app front-end VM using [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview).</span><span class="sxs-lookup"><span data-stu-id="0cc86-125">Contoso migrates the app front-end VM using [Azure Site Recovery](https://docs.microsoft.com/azure/site-recovery/site-recovery-overview).</span></span> <span data-ttu-id="0cc86-126">Contoso migrates the app database to an Azure SQL Database Managed Instance using the [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).</span><span class="sxs-lookup"><span data-stu-id="0cc86-126">Contoso migrates the app database to an Azure SQL Database Managed Instance using the [Azure Database Migration Service](https://docs.microsoft.com/azure/dms/dms-overview).</span></span> | <span data-ttu-id="0cc86-127">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-127">Available</span></span>   
[<span data-ttu-id="0cc86-128">Article 5: Rehost an app on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="0cc86-128">Article 5: Rehost an app on Azure VMs</span></span>](contoso-migration-rehost-vm.md) | <span data-ttu-id="0cc86-129">Contoso migrates its SmartHotel360 app VMs to Azure VMs using the Site Recovery service.</span><span class="sxs-lookup"><span data-stu-id="0cc86-129">Contoso migrates its SmartHotel360 app VMs to Azure VMs using the Site Recovery service.</span></span> | <span data-ttu-id="0cc86-130">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-130">Available</span></span>
[<span data-ttu-id="0cc86-131">Article 6: Rehost an app on Azure VMs and in a  SQL Server AlwaysOn availability group</span><span class="sxs-lookup"><span data-stu-id="0cc86-131">Article 6: Rehost an app on Azure VMs and in a  SQL Server AlwaysOn availability group</span></span>](contoso-migration-rehost-vm-sql-ag.md) | <span data-ttu-id="0cc86-132">Contoso migrates the SmartHotel360 app.</span><span class="sxs-lookup"><span data-stu-id="0cc86-132">Contoso migrates the SmartHotel360 app.</span></span> <span data-ttu-id="0cc86-133">Contoso uses Site Recovery to migrate the app VMs.</span><span class="sxs-lookup"><span data-stu-id="0cc86-133">Contoso uses Site Recovery to migrate the app VMs.</span></span> <span data-ttu-id="0cc86-134">It uses the Database Migration Service to migrate the app database to a SQL Server cluster that's protected by an AlwaysOn availability group.</span><span class="sxs-lookup"><span data-stu-id="0cc86-134">It uses the Database Migration Service to migrate the app database to a SQL Server cluster that's protected by an AlwaysOn availability group.</span></span> | <span data-ttu-id="0cc86-135">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-135">Available</span></span> 
[<span data-ttu-id="0cc86-136">Article 7: Rehost a Linux app on Azure VMs</span><span class="sxs-lookup"><span data-stu-id="0cc86-136">Article 7: Rehost a Linux app on Azure VMs</span></span>](contoso-migration-rehost-linux-vm.md) | <span data-ttu-id="0cc86-137">Contoso completes a lift-and-shift migration of the Linux osTicket app to Azure VMs, using Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0cc86-137">Contoso completes a lift-and-shift migration of the Linux osTicket app to Azure VMs, using Azure Site Recovery</span></span> | <span data-ttu-id="0cc86-138">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-138">Available</span></span>
[<span data-ttu-id="0cc86-139">Article 8: Rehost a Linux app on Azure VMs and Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="0cc86-139">Article 8: Rehost a Linux app on Azure VMs and Azure MySQL</span></span>](contoso-migration-rehost-linux-vm-mysql.md) | <span data-ttu-id="0cc86-140">Contoso migrates the Linux osTicket app to Azure VMs using Azure Site Recovery, and migrates the app database to an Azure MySQL Server instance using MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="0cc86-140">Contoso migrates the Linux osTicket app to Azure VMs using Azure Site Recovery, and migrates the app database to an Azure MySQL Server instance using MySQL Workbench.</span></span> | <span data-ttu-id="0cc86-141">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-141">Available</span></span>
[<span data-ttu-id="0cc86-142">Article 9: Refactor an app on Azure Web Apps and Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="0cc86-142">Article 9: Refactor an app on Azure Web Apps and Azure SQL database</span></span>](contoso-migration-refactor-web-app-sql.md) | <span data-ttu-id="0cc86-143">Contoso migrates the SmartHotel360 app to an Azure Web App, and migrates the app database to an Azure SQL Server instance with Database Migration Assistant</span><span class="sxs-lookup"><span data-stu-id="0cc86-143">Contoso migrates the SmartHotel360 app to an Azure Web App, and migrates the app database to an Azure SQL Server instance with Database Migration Assistant</span></span> | <span data-ttu-id="0cc86-144">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-144">Available</span></span>
<span data-ttu-id="0cc86-145">Article 10: Refactor a Linux app on Azure Web Apps and Azure MySQL</span><span class="sxs-lookup"><span data-stu-id="0cc86-145">Article 10: Refactor a Linux app on Azure Web Apps and Azure MySQL</span></span> | <span data-ttu-id="0cc86-146">Contoso migrates its Linux osTicket app to an Azure web app on multiple Azure regions using Azure Traffic Manager, integrated with GitHub for continuous delivery.</span><span class="sxs-lookup"><span data-stu-id="0cc86-146">Contoso migrates its Linux osTicket app to an Azure web app on multiple Azure regions using Azure Traffic Manager, integrated with GitHub for continuous delivery.</span></span> <span data-ttu-id="0cc86-147">Contoso migrates the app database to an Azure Database for MySQL instance.</span><span class="sxs-lookup"><span data-stu-id="0cc86-147">Contoso migrates the app database to an Azure Database for MySQL instance.</span></span> | <span data-ttu-id="0cc86-148">This article</span><span class="sxs-lookup"><span data-stu-id="0cc86-148">This article</span></span>
[<span data-ttu-id="0cc86-149">Article 11: Refactor TFS on Azure DevOps Services</span><span class="sxs-lookup"><span data-stu-id="0cc86-149">Article 11: Refactor TFS on Azure DevOps Services</span></span>](contoso-migration-tfs-vsts.md) | <span data-ttu-id="0cc86-150">Contoso migrates its on-premises Team Foundation Server deployment to Azure DevOps Services in Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc86-150">Contoso migrates its on-premises Team Foundation Server deployment to Azure DevOps Services in Azure.</span></span> | <span data-ttu-id="0cc86-151">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-151">Available</span></span>
[<span data-ttu-id="0cc86-152">Article 12: Rearchitect an app on Azure containers and Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="0cc86-152">Article 12: Rearchitect an app on Azure containers and Azure SQL Database</span></span>](contoso-migration-rearchitect-container-sql.md) | <span data-ttu-id="0cc86-153">Contoso migrates its SmartHotel app to Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc86-153">Contoso migrates its SmartHotel app to Azure.</span></span> <span data-ttu-id="0cc86-154">Then, it rearchitects the app web tier as a Windows container running in Azure Service Fabric, and the database with Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="0cc86-154">Then, it rearchitects the app web tier as a Windows container running in Azure Service Fabric, and the database with Azure SQL Database.</span></span> | <span data-ttu-id="0cc86-155">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-155">Available</span></span>
[<span data-ttu-id="0cc86-156">Article 13: Rebuild an app in Azure</span><span class="sxs-lookup"><span data-stu-id="0cc86-156">Article 13: Rebuild an app in Azure</span></span>](contoso-migration-rebuild.md) | <span data-ttu-id="0cc86-157">Contoso rebuilds its SmartHotel360 app by using a range of Azure capabilities and services, including Azure App Service, Azure Kubernetes Service (AKS), Azure Functions, Azure Cognitive Services, and Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="0cc86-157">Contoso rebuilds its SmartHotel360 app by using a range of Azure capabilities and services, including Azure App Service, Azure Kubernetes Service (AKS), Azure Functions, Azure Cognitive Services, and Azure Cosmos DB.</span></span> | <span data-ttu-id="0cc86-158">Available</span><span class="sxs-lookup"><span data-stu-id="0cc86-158">Available</span></span>

<span data-ttu-id="0cc86-159">In this article, Contoso migrates a two-tier Linux Apache MySQL PHP (LAMP) service desk app (osTicket) to Azure.</span><span class="sxs-lookup"><span data-stu-id="0cc86-159">In this article, Contoso migrates a two-tier Linux Apache MySQL PHP (LAMP) service desk app (osTicket) to Azure.</span></span> <span data-ttu-id="0cc86-160">If you'd like to use this open-source app, you can download it from [GitHub](https://github.com/osTicket/osTicket).</span><span class="sxs-lookup"><span data-stu-id="0cc86-160">If you'd like to use this open-source app, you can download it from [GitHub](https://github.com/osTicket/osTicket).</span></span>


## <a name="business-drivers"></a><span data-ttu-id="0cc86-161">Business drivers</span><span class="sxs-lookup"><span data-stu-id="0cc86-161">Business drivers</span></span>

<span data-ttu-id="0cc86-162">The IT Leadership team has worked closely with business partners to understand what they want to achieve:</span><span class="sxs-lookup"><span data-stu-id="0cc86-162">The IT Leadership team has worked closely with business partners to understand what they want to achieve:</span></span>

- <span data-ttu-id="0cc86-163">**Address business growth**: Contoso is growing and moving into new markets.</span><span class="sxs-lookup"><span data-stu-id="0cc86-163">**Address business growth**: Contoso is growing and moving into new markets.</span></span> <span data-ttu-id="0cc86-164">It needs additional customer service agents.</span><span class="sxs-lookup"><span data-stu-id="0cc86-164">It needs additional customer service agents.</span></span> 
- <span data-ttu-id="0cc86-165">**Scale**: The solution should be built so that Contoso can add more customer service agents as the business scales.</span><span class="sxs-lookup"><span data-stu-id="0cc86-165">**Scale**: The solution should be built so that Contoso can add more customer service agents as the business scales.</span></span>
- <span data-ttu-id="0cc86-166">**Increase resiliency**:  In the past issues with the system affected internal users only.</span><span class="sxs-lookup"><span data-stu-id="0cc86-166">**Increase resiliency**:  In the past issues with the system affected internal users only.</span></span> <span data-ttu-id="0cc86-167">With the new business model, external users will be affected, and Contoso need the app up and running at all times.</span><span class="sxs-lookup"><span data-stu-id="0cc86-167">With the new business model, external users will be affected, and Contoso need the app up and running at all times.</span></span>

## <a name="migration-goals"></a><span data-ttu-id="0cc86-168">Migration goals</span><span class="sxs-lookup"><span data-stu-id="0cc86-168">Migration goals</span></span>

<span data-ttu-id="0cc86-169">The Contoso cloud team has pinned down goals for this migration, in order to determine the best migration method:</span><span class="sxs-lookup"><span data-stu-id="0cc86-169">The Contoso cloud team has pinned down goals for this migration, in order to determine the best migration method:</span></span>

- <span data-ttu-id="0cc86-170">The application should scale beyond current on-premises capacity and performance.</span><span class="sxs-lookup"><span data-stu-id="0cc86-170">The application should scale beyond current on-premises capacity and performance.</span></span>  <span data-ttu-id="0cc86-171">Contoso is moving the application to take advantage of Azure's on-demand scaling.</span><span class="sxs-lookup"><span data-stu-id="0cc86-171">Contoso is moving the application to take advantage of Azure's on-demand scaling.</span></span>
- <span data-ttu-id="0cc86-172">Contoso want to move the app code base to a continuous delivery pipeline.</span><span class="sxs-lookup"><span data-stu-id="0cc86-172">Contoso want to move the app code base to a continuous delivery pipeline.</span></span>  <span data-ttu-id="0cc86-173">As app changes are pushed to GitHub, Contoso want to deploy those changes without tasks for operations staff.</span><span class="sxs-lookup"><span data-stu-id="0cc86-173">As app changes are pushed to GitHub, Contoso want to deploy those changes without tasks for operations staff.</span></span>
- <span data-ttu-id="0cc86-174">The application must be resilient with capabilities for growth and failover.</span><span class="sxs-lookup"><span data-stu-id="0cc86-174">The application must be resilient with capabilities for growth and failover.</span></span> <span data-ttu-id="0cc86-175">Contoso want to deploy the app in two different Azure regions, and set it up to scale automatically.</span><span class="sxs-lookup"><span data-stu-id="0cc86-175">Contoso want to deploy the app in two different Azure regions, and set it up to scale automatically.</span></span>
- <span data-ttu-id="0cc86-176">Contoso wants to minimize database admin tasks after the app is moved to the cloud.</span><span class="sxs-lookup"><span data-stu-id="0cc86-176">Contoso wants to minimize database admin tasks after the app is moved to the cloud.</span></span>

## <a name="solution-design"></a><span data-ttu-id="0cc86-177">Solution design</span><span class="sxs-lookup"><span data-stu-id="0cc86-177">Solution design</span></span>
<span data-ttu-id="0cc86-178">After pinning down their goals and requirements, Contoso designs and reviews a deployment solution, and identifies the migration process, including the Azure services that will be used for the migration.</span><span class="sxs-lookup"><span data-stu-id="0cc86-178">After pinning down their goals and requirements, Contoso designs and reviews a deployment solution, and identifies the migration process, including the Azure services that will be used for the migration.</span></span>


## <a name="current-architecture"></a><span data-ttu-id="0cc86-179">Current architecture</span><span class="sxs-lookup"><span data-stu-id="0cc86-179">Current architecture</span></span>

- <span data-ttu-id="0cc86-180">The app is tiered across two VMs (OSTICKETWEB and OSTICKETMYSQL).</span><span class="sxs-lookup"><span data-stu-id="0cc86-180">The app is tiered across two VMs (OSTICKETWEB and OSTICKETMYSQL).</span></span>
- <span data-ttu-id="0cc86-181">The VMs are located on VMware ESXi host **contosohost1.contoso.com** (version 6.5).</span><span class="sxs-lookup"><span data-stu-id="0cc86-181">The VMs are located on VMware ESXi host **contosohost1.contoso.com** (version 6.5).</span></span>
- <span data-ttu-id="0cc86-182">The VMware environment is managed by vCenter Server 6.5 (**vcenter.contoso.com**), running on a VM.</span><span class="sxs-lookup"><span data-stu-id="0cc86-182">The VMware environment is managed by vCenter Server 6.5 (**vcenter.contoso.com**), running on a VM.</span></span>
- <span data-ttu-id="0cc86-183">Contoso has an on-premises datacenter (contoso-datacenter), with an on-premises domain controller (**contosodc1**).</span><span class="sxs-lookup"><span data-stu-id="0cc86-183">Contoso has an on-premises datacenter (contoso-datacenter), with an on-premises domain controller (**contosodc1**).</span></span>

![Current architecture](./media/contoso-migration-refactor-linux-app-service-mysql/current-architecture.png) 


## <a name="proposed-architecture"></a><span data-ttu-id="0cc86-185">Proposed architecture</span><span class="sxs-lookup"><span data-stu-id="0cc86-185">Proposed architecture</span></span>

<span data-ttu-id="0cc86-186">Here's the proposed architecture:</span><span class="sxs-lookup"><span data-stu-id="0cc86-186">Here's the proposed architecture:</span></span>

- <span data-ttu-id="0cc86-187">The web tier app on OSTICKETWEB will be migrated by building an Azure App Service in two Azure regions.</span><span class="sxs-lookup"><span data-stu-id="0cc86-187">The web tier app on OSTICKETWEB will be migrated by building an Azure App Service in two Azure regions.</span></span> <span data-ttu-id="0cc86-188">Azure App Service for Linux will be implemented using the PHP 7.0 Docker container.</span><span class="sxs-lookup"><span data-stu-id="0cc86-188">Azure App Service for Linux will be implemented using the PHP 7.0 Docker container.</span></span>
- <span data-ttu-id="0cc86-189">The app code will be moved to GitHub, and Azure Web App will be configured for continuous delivery with GitHub.</span><span class="sxs-lookup"><span data-stu-id="0cc86-189">The app code will be moved to GitHub, and Azure Web App will be configured for continuous delivery with GitHub.</span></span>
- <span data-ttu-id="0cc86-190">Azure App Servers will be deployed in both the primary (East US 2) and secondary (Central US) region.</span><span class="sxs-lookup"><span data-stu-id="0cc86-190">Azure App Servers will be deployed in both the primary (East US 2) and secondary (Central US) region.</span></span>
- <span data-ttu-id="0cc86-191">Traffic Manager will be set up in front of the two Azure Web Apps in both regions.</span><span class="sxs-lookup"><span data-stu-id="0cc86-191">Traffic Manager will be set up in front of the two Azure Web Apps in both regions.</span></span>
- <span data-ttu-id="0cc86-192">Traffic Manager will be configured in priority mode to force the traffic through East US 2.</span><span class="sxs-lookup"><span data-stu-id="0cc86-192">Traffic Manager will be configured in priority mode to force the traffic through East US 2.</span></span>
- <span data-ttu-id="0cc86-193">If the Azure App Server in East US 2 goes offline, users can access the failed over app in Central US.</span><span class="sxs-lookup"><span data-stu-id="0cc86-193">If the Azure App Server in East US 2 goes offline, users can access the failed over app in Central US.</span></span>
- <span data-ttu-id="0cc86-194">The app database will be migrated to the Azure MySQL PaaS service using MySQL Workbench tools.</span><span class="sxs-lookup"><span data-stu-id="0cc86-194">The app database will be migrated to the Azure MySQL PaaS service using MySQL Workbench tools.</span></span> <span data-ttu-id="0cc86-195">The on-premises database will be backed up locally, and restored directly to Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="0cc86-195">The on-premises database will be backed up locally, and restored directly to Azure MySQL.</span></span>
- <span data-ttu-id="0cc86-196">The database will reside in the primary East US 2 region, in the database subnet (PROD-DB-EUS2) in the production network (VNET-PROD-EUS2):</span><span class="sxs-lookup"><span data-stu-id="0cc86-196">The database will reside in the primary East US 2 region, in the database subnet (PROD-DB-EUS2) in the production network (VNET-PROD-EUS2):</span></span>
- <span data-ttu-id="0cc86-197">Since they're migrating a production workload, Azure resources for the app will reside in the production resource group **ContosoRG**.</span><span class="sxs-lookup"><span data-stu-id="0cc86-197">Since they're migrating a production workload, Azure resources for the app will reside in the production resource group **ContosoRG**.</span></span>
- <span data-ttu-id="0cc86-198">The Traffic Manager resource will be deployed in Contoso's infrastructure resource group **ContosoInfraRG**.</span><span class="sxs-lookup"><span data-stu-id="0cc86-198">The Traffic Manager resource will be deployed in Contoso's infrastructure resource group **ContosoInfraRG**.</span></span>
- <span data-ttu-id="0cc86-199">The on-premises VMs in the Contoso datacenter will be decommissioned after the migration is done.</span><span class="sxs-lookup"><span data-stu-id="0cc86-199">The on-premises VMs in the Contoso datacenter will be decommissioned after the migration is done.</span></span>


![Scenario architecture](./media/contoso-migration-refactor-linux-app-service-mysql/proposed-architecture.png) 


## <a name="migration-process"></a><span data-ttu-id="0cc86-201">Migration process</span><span class="sxs-lookup"><span data-stu-id="0cc86-201">Migration process</span></span>

<span data-ttu-id="0cc86-202">Contoso will complete the migration process as follows:</span><span class="sxs-lookup"><span data-stu-id="0cc86-202">Contoso will complete the migration process as follows:</span></span>

1. <span data-ttu-id="0cc86-203">As a first step, Contoso admins set up the Azure infrastructure, including provisioning Azure App Services, setting up Traffic Manager, and provisioning an Azure MySQL instance.</span><span class="sxs-lookup"><span data-stu-id="0cc86-203">As a first step, Contoso admins set up the Azure infrastructure, including provisioning Azure App Services, setting up Traffic Manager, and provisioning an Azure MySQL instance.</span></span>
2. <span data-ttu-id="0cc86-204">After preparing the Azure, they migrate the database using MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="0cc86-204">After preparing the Azure, they migrate the database using MySQL Workbench.</span></span> 
3. <span data-ttu-id="0cc86-205">After the database is running in Azure, they up a GitHub private repo for the Azure App Service with continuous delivery, and load it with the osTicket app.</span><span class="sxs-lookup"><span data-stu-id="0cc86-205">After the database is running in Azure, they up a GitHub private repo for the Azure App Service with continuous delivery, and load it with the osTicket app.</span></span>
4. <span data-ttu-id="0cc86-206">In the Azure portal, they load the app from GitHub to the Docker container running Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="0cc86-206">In the Azure portal, they load the app from GitHub to the Docker container running Azure App Service.</span></span> 
5. <span data-ttu-id="0cc86-207">They tweak DNS settings, and configure autoscaling for the app.</span><span class="sxs-lookup"><span data-stu-id="0cc86-207">They tweak DNS settings, and configure autoscaling for the app.</span></span>

![Migration process](./media/contoso-migration-refactor-linux-app-service-mysql/migration-process.png) 


### <a name="azure-services"></a><span data-ttu-id="0cc86-209">Azure services</span><span class="sxs-lookup"><span data-stu-id="0cc86-209">Azure services</span></span>

<span data-ttu-id="0cc86-210">**Service**</span><span class="sxs-lookup"><span data-stu-id="0cc86-210">**Service**</span></span> | <span data-ttu-id="0cc86-211">**Description**</span><span class="sxs-lookup"><span data-stu-id="0cc86-211">**Description**</span></span> | <span data-ttu-id="0cc86-212">**Cost**</span><span class="sxs-lookup"><span data-stu-id="0cc86-212">**Cost**</span></span>
--- | --- | ---
[<span data-ttu-id="0cc86-213">Azure App Service</span><span class="sxs-lookup"><span data-stu-id="0cc86-213">Azure App Service</span></span>](https://azure.microsoft.com/services/app-service/) | <span data-ttu-id="0cc86-214">The service runs and scales applications using the Azure PaaS service for websites.</span><span class="sxs-lookup"><span data-stu-id="0cc86-214">The service runs and scales applications using the Azure PaaS service for websites.</span></span>  | <span data-ttu-id="0cc86-215">Pricing is based on the size of the instances, and the features required.</span><span class="sxs-lookup"><span data-stu-id="0cc86-215">Pricing is based on the size of the instances, and the features required.</span></span> <span data-ttu-id="0cc86-216">[Learn more](https://azure.microsoft.com/pricing/details/app-service/windows/).</span><span class="sxs-lookup"><span data-stu-id="0cc86-216">[Learn more](https://azure.microsoft.com/pricing/details/app-service/windows/).</span></span>
[<span data-ttu-id="0cc86-217">Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0cc86-217">Traffic Manager</span></span>](https://azure.microsoft.com/services/traffic-manager/) | <span data-ttu-id="0cc86-218">A load balancer that uses DNS to direct users to Azure, or external websites and services.</span><span class="sxs-lookup"><span data-stu-id="0cc86-218">A load balancer that uses DNS to direct users to Azure, or external websites and services.</span></span> | <span data-ttu-id="0cc86-219">Pricing is based on the number of DNS queries received, and the number of monitored endpoints.</span><span class="sxs-lookup"><span data-stu-id="0cc86-219">Pricing is based on the number of DNS queries received, and the number of monitored endpoints.</span></span> | <span data-ttu-id="0cc86-220">[Learn more](https://azure.microsoft.com/pricing/details/traffic-manager/).</span><span class="sxs-lookup"><span data-stu-id="0cc86-220">[Learn more](https://azure.microsoft.com/pricing/details/traffic-manager/).</span></span>
[<span data-ttu-id="0cc86-221">Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="0cc86-221">Azure Database for MySQL</span></span>](https://docs.microsoft.com/azure/mysql/) | <span data-ttu-id="0cc86-222">The database is based on the open-source MySQL Server engine.</span><span class="sxs-lookup"><span data-stu-id="0cc86-222">The database is based on the open-source MySQL Server engine.</span></span> <span data-ttu-id="0cc86-223">It provides a fully managed, enterprise-ready community MySQL database, as a service for app development and deployment.</span><span class="sxs-lookup"><span data-stu-id="0cc86-223">It provides a fully managed, enterprise-ready community MySQL database, as a service for app development and deployment.</span></span> | <span data-ttu-id="0cc86-224">Pricing based on compute, storage, and backup requirements.</span><span class="sxs-lookup"><span data-stu-id="0cc86-224">Pricing based on compute, storage, and backup requirements.</span></span> <span data-ttu-id="0cc86-225">[Learn more](https://azure.microsoft.com/pricing/details/mysql/).</span><span class="sxs-lookup"><span data-stu-id="0cc86-225">[Learn more](https://azure.microsoft.com/pricing/details/mysql/).</span></span>

 
## <a name="prerequisites"></a><span data-ttu-id="0cc86-226">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="0cc86-226">Prerequisites</span></span>

<span data-ttu-id="0cc86-227">Here's what Contoso needs to run this scenario.</span><span class="sxs-lookup"><span data-stu-id="0cc86-227">Here's what Contoso needs to run this scenario.</span></span>

<span data-ttu-id="0cc86-228">**Requirements**</span><span class="sxs-lookup"><span data-stu-id="0cc86-228">**Requirements**</span></span> | <span data-ttu-id="0cc86-229">**Details**</span><span class="sxs-lookup"><span data-stu-id="0cc86-229">**Details**</span></span>
--- | ---
<span data-ttu-id="0cc86-230">**Azure subscription**</span><span class="sxs-lookup"><span data-stu-id="0cc86-230">**Azure subscription**</span></span> | <span data-ttu-id="0cc86-231">Contoso created subscriptions earlier in this article series.</span><span class="sxs-lookup"><span data-stu-id="0cc86-231">Contoso created subscriptions earlier in this article series.</span></span> <span data-ttu-id="0cc86-232">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="0cc86-232">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/pricing/free-trial/).</span></span><br/><br/> <span data-ttu-id="0cc86-233">If you create a free account, you're the administrator of your subscription and can perform all actions.</span><span class="sxs-lookup"><span data-stu-id="0cc86-233">If you create a free account, you're the administrator of your subscription and can perform all actions.</span></span><br/><br/> <span data-ttu-id="0cc86-234">If you use an existing subscription and you're not the administrator, you need to work with the admin to assign you Owner or Contributor permissions.</span><span class="sxs-lookup"><span data-stu-id="0cc86-234">If you use an existing subscription and you're not the administrator, you need to work with the admin to assign you Owner or Contributor permissions.</span></span> 
<span data-ttu-id="0cc86-235">**Azure infrastructure**</span><span class="sxs-lookup"><span data-stu-id="0cc86-235">**Azure infrastructure**</span></span> | <span data-ttu-id="0cc86-236">Contoso set up their Azure infrastructure as described in [Azure infrastructure for migration](contoso-migration-infrastructure.md).</span><span class="sxs-lookup"><span data-stu-id="0cc86-236">Contoso set up their Azure infrastructure as described in [Azure infrastructure for migration](contoso-migration-infrastructure.md).</span></span>



## <a name="scenario-steps"></a><span data-ttu-id="0cc86-237">Scenario steps</span><span class="sxs-lookup"><span data-stu-id="0cc86-237">Scenario steps</span></span>

<span data-ttu-id="0cc86-238">Here's how Contoso will complete the migration:</span><span class="sxs-lookup"><span data-stu-id="0cc86-238">Here's how Contoso will complete the migration:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="0cc86-239">**Step 1: Provision Azure App Services**: Contoso admins will provision Web Apps in the primary and secondary regions.</span><span class="sxs-lookup"><span data-stu-id="0cc86-239">**Step 1: Provision Azure App Services**: Contoso admins will provision Web Apps in the primary and secondary regions.</span></span>
> * <span data-ttu-id="0cc86-240">**Step 2: Set up Traffic Manager**: They set up Traffic Manager in front of the Web Apps, for routing and load balancing traffic.</span><span class="sxs-lookup"><span data-stu-id="0cc86-240">**Step 2: Set up Traffic Manager**: They set up Traffic Manager in front of the Web Apps, for routing and load balancing traffic.</span></span>
> * <span data-ttu-id="0cc86-241">**Step 3: Provision MySQL**: In Azure, they provision an instance of Azure MySQL database.</span><span class="sxs-lookup"><span data-stu-id="0cc86-241">**Step 3: Provision MySQL**: In Azure, they provision an instance of Azure MySQL database.</span></span>
> * <span data-ttu-id="0cc86-242">**Step 4: Migrate the database**: They migrate the database using MySQL Workbench.</span><span class="sxs-lookup"><span data-stu-id="0cc86-242">**Step 4: Migrate the database**: They migrate the database using MySQL Workbench.</span></span> 
> * <span data-ttu-id="0cc86-243">**Step 5: Set up GitHub**: They set up a local GitHub repository for the app web sites/code.</span><span class="sxs-lookup"><span data-stu-id="0cc86-243">**Step 5: Set up GitHub**: They set up a local GitHub repository for the app web sites/code.</span></span>
> * <span data-ttu-id="0cc86-244">**Step 6: Deploy the web apps**: They deploy the web apps from GitHub.</span><span class="sxs-lookup"><span data-stu-id="0cc86-244">**Step 6: Deploy the web apps**: They deploy the web apps from GitHub.</span></span>




## <a name="step-1-provision-azure-app-services"></a><span data-ttu-id="0cc86-245">Step 1: Provision Azure App Services</span><span class="sxs-lookup"><span data-stu-id="0cc86-245">Step 1: Provision Azure App Services</span></span>

<span data-ttu-id="0cc86-246">Contoso admins provision two Web apps (one in each region) using Azure App Services.</span><span class="sxs-lookup"><span data-stu-id="0cc86-246">Contoso admins provision two Web apps (one in each region) using Azure App Services.</span></span>

1. <span data-ttu-id="0cc86-247">They create a Web App resource in the primary East US 2 region (**osticket-eus2**) from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0cc86-247">They create a Web App resource in the primary East US 2 region (**osticket-eus2**) from the Azure Marketplace.</span></span>
2. <span data-ttu-id="0cc86-248">They put the resource in the production resource group **ContosoRG**.</span><span class="sxs-lookup"><span data-stu-id="0cc86-248">They put the resource in the production resource group **ContosoRG**.</span></span>

    ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app1.png) 

3. <span data-ttu-id="0cc86-250">They create a new App Service plan in the primary region (**APP-SVP-EUS2**), using the standard size.</span><span class="sxs-lookup"><span data-stu-id="0cc86-250">They create a new App Service plan in the primary region (**APP-SVP-EUS2**), using the standard size.</span></span>

     ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app2.png) 
    
4. <span data-ttu-id="0cc86-252">They select a Linux OS with PHP 7.0 runtime stack, which is a Docker container.</span><span class="sxs-lookup"><span data-stu-id="0cc86-252">They select a Linux OS with PHP 7.0 runtime stack, which is a Docker container.</span></span>

    ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app3.png) 

5. <span data-ttu-id="0cc86-254">They create a second web app (**osticket-cus**), and App service plan for the Central US region.</span><span class="sxs-lookup"><span data-stu-id="0cc86-254">They create a second web app (**osticket-cus**), and App service plan for the Central US region.</span></span>

    ![Azure App](./media/contoso-migration-refactor-linux-app-service-mysql/azure-app4.png) 


<span data-ttu-id="0cc86-256">**Need more help?**</span><span class="sxs-lookup"><span data-stu-id="0cc86-256">**Need more help?**</span></span>

- <span data-ttu-id="0cc86-257">Learn about [Azure App Service Web apps](https://docs.microsoft.com/azure/app-service/app-service-web-overview).</span><span class="sxs-lookup"><span data-stu-id="0cc86-257">Learn about [Azure App Service Web apps](https://docs.microsoft.com/azure/app-service/app-service-web-overview).</span></span>
- <span data-ttu-id="0cc86-258">Learn about [Azure App Service on Linux](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).</span><span class="sxs-lookup"><span data-stu-id="0cc86-258">Learn about [Azure App Service on Linux](https://docs.microsoft.com/azure/app-service/containers/app-service-linux-intro).</span></span>


## <a name="step-2-set-up-traffic-manager"></a><span data-ttu-id="0cc86-259">Step 2: Set up Traffic Manager</span><span class="sxs-lookup"><span data-stu-id="0cc86-259">Step 2: Set up Traffic Manager</span></span>

<span data-ttu-id="0cc86-260">Contoso admins set up Traffic Manager to direct inbound web requests to Web Apps running on the osTicket web tier.</span><span class="sxs-lookup"><span data-stu-id="0cc86-260">Contoso admins set up Traffic Manager to direct inbound web requests to Web Apps running on the osTicket web tier.</span></span>

1. <span data-ttu-id="0cc86-261">They create a Traffic Manager resource (**osticket.trafficmanager.net**) from the Azure Marketplace.</span><span class="sxs-lookup"><span data-stu-id="0cc86-261">They create a Traffic Manager resource (**osticket.trafficmanager.net**) from the Azure Marketplace.</span></span> <span data-ttu-id="0cc86-262">They use priority routing so that East US 2 is the primary site.</span><span class="sxs-lookup"><span data-stu-id="0cc86-262">They use priority routing so that East US 2 is the primary site.</span></span> <span data-ttu-id="0cc86-263">They place the resource in their infrastructure resource group (**ContosoInfraRG**).</span><span class="sxs-lookup"><span data-stu-id="0cc86-263">They place the resource in their infrastructure resource group (**ContosoInfraRG**).</span></span> <span data-ttu-id="0cc86-264">Note that Traffic Manager is global and not bound to a specific location</span><span class="sxs-lookup"><span data-stu-id="0cc86-264">Note that Traffic Manager is global and not bound to a specific location</span></span>

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager1.png) 

2. <span data-ttu-id="0cc86-266">Now, they configure Traffic Manager with endpoints.</span><span class="sxs-lookup"><span data-stu-id="0cc86-266">Now, they configure Traffic Manager with endpoints.</span></span> <span data-ttu-id="0cc86-267">They add East US 2 Web app as the primary site (**osticket-eus2**), and the Central US app as secondary (**osticket-cus**).</span><span class="sxs-lookup"><span data-stu-id="0cc86-267">They add East US 2 Web app as the primary site (**osticket-eus2**), and the Central US app as secondary (**osticket-cus**).</span></span>

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager2.png) 

3. <span data-ttu-id="0cc86-269">After adding the endpoints, they can monitor them.</span><span class="sxs-lookup"><span data-stu-id="0cc86-269">After adding the endpoints, they can monitor them.</span></span>

    ![Traffic Manager](./media/contoso-migration-refactor-linux-app-service-mysql/traffic-manager3.png)

<span data-ttu-id="0cc86-271">**Need more help?**</span><span class="sxs-lookup"><span data-stu-id="0cc86-271">**Need more help?**</span></span>

- <span data-ttu-id="0cc86-272">Learn about [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview).</span><span class="sxs-lookup"><span data-stu-id="0cc86-272">Learn about [Traffic Manager](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-overview).</span></span>
- <span data-ttu-id="0cc86-273">Learn about [routing traffic to a priority endpoint](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-configure-priority-routing-method).</span><span class="sxs-lookup"><span data-stu-id="0cc86-273">Learn about [routing traffic to a priority endpoint](https://docs.microsoft.com/azure/traffic-manager/traffic-manager-configure-priority-routing-method).</span></span>
 
## <a name="step-3-provision-azure-database-for-mysql"></a><span data-ttu-id="0cc86-274">Step 3: Provision Azure Database for MySQL</span><span class="sxs-lookup"><span data-stu-id="0cc86-274">Step 3: Provision Azure Database for MySQL</span></span>

<span data-ttu-id="0cc86-275">Contoso admins provision a MySQL database instance in the primary East US 2 region.</span><span class="sxs-lookup"><span data-stu-id="0cc86-275">Contoso admins provision a MySQL database instance in the primary East US 2 region.</span></span>

1. <span data-ttu-id="0cc86-276">In the Azure portal, they create an Azure Database for MySQL resource.</span><span class="sxs-lookup"><span data-stu-id="0cc86-276">In the Azure portal, they create an Azure Database for MySQL resource.</span></span> 

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-1.png)

2. <span data-ttu-id="0cc86-278">They add the name **contosoosticket** for the Azure database.</span><span class="sxs-lookup"><span data-stu-id="0cc86-278">They add the name **contosoosticket** for the Azure database.</span></span> <span data-ttu-id="0cc86-279">They add the database to the production resource group **ContosoRG**, and specify credentials for it.</span><span class="sxs-lookup"><span data-stu-id="0cc86-279">They add the database to the production resource group **ContosoRG**, and specify credentials for it.</span></span>
3. <span data-ttu-id="0cc86-280">The on-premises MySQL database is version 5.7, so they select this version for compatibility.</span><span class="sxs-lookup"><span data-stu-id="0cc86-280">The on-premises MySQL database is version 5.7, so they select this version for compatibility.</span></span> <span data-ttu-id="0cc86-281">They use the default sizes, which match their database requirements.</span><span class="sxs-lookup"><span data-stu-id="0cc86-281">They use the default sizes, which match their database requirements.</span></span>

     ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-2.png)

4. <span data-ttu-id="0cc86-283">For **Backup Redundancy Options**, they select to use **Geo-Redundant**.</span><span class="sxs-lookup"><span data-stu-id="0cc86-283">For **Backup Redundancy Options**, they select to use **Geo-Redundant**.</span></span> <span data-ttu-id="0cc86-284">This option allows them to restore the database in their secondary Central US region if an outage occurs.</span><span class="sxs-lookup"><span data-stu-id="0cc86-284">This option allows them to restore the database in their secondary Central US region if an outage occurs.</span></span> <span data-ttu-id="0cc86-285">They can only configure this option when they provision the database.</span><span class="sxs-lookup"><span data-stu-id="0cc86-285">They can only configure this option when they provision the database.</span></span>

    ![Redundancy](./media/contoso-migration-refactor-linux-app-service-mysql/db-redundancy.png)

4. <span data-ttu-id="0cc86-287">They set up connection security.</span><span class="sxs-lookup"><span data-stu-id="0cc86-287">They set up connection security.</span></span> <span data-ttu-id="0cc86-288">In the database > **Connection Security**, they set up Firewall rules to allow the database to access Azure services.</span><span class="sxs-lookup"><span data-stu-id="0cc86-288">In the database > **Connection Security**, they set up Firewall rules to allow the database to access Azure services.</span></span>
5. <span data-ttu-id="0cc86-289">They add the local workstation client IP address to the start and end IP addresses.</span><span class="sxs-lookup"><span data-stu-id="0cc86-289">They add the local workstation client IP address to the start and end IP addresses.</span></span> <span data-ttu-id="0cc86-290">This allows the Web apps to access the MySQL database, along with the database client that's performing the migration.</span><span class="sxs-lookup"><span data-stu-id="0cc86-290">This allows the Web apps to access the MySQL database, along with the database client that's performing the migration.</span></span>

    ![MySQL](./media/contoso-migration-refactor-linux-app-service-mysql/mysql-3.png)



## <a name="step-4-migrate-the-database"></a><span data-ttu-id="0cc86-292">Step 4: Migrate the database</span><span class="sxs-lookup"><span data-stu-id="0cc86-292">Step 4: Migrate the database</span></span>

<span data-ttu-id="0cc86-293">Contoso admins migrate the database using backup and restore, with MySQL tools.</span><span class="sxs-lookup"><span data-stu-id="0cc86-293">Contoso admins migrate the database using backup and restore, with MySQL tools.</span></span> <span data-ttu-id="0cc86-294">They install MySQL Workbench, back up the database from OSTICKETMYSQL, and then restore it to Azure Database for MySQL Server.</span><span class="sxs-lookup"><span data-stu-id="0cc86-294">They install MySQL Workbench, back up the database from OSTICKETMYSQL, and then restore it to Azure Database for MySQL Server.</span></span>

### <a name="install-mysql-workbench"></a><span data-ttu-id="0cc86-295">Install MySQL Workbench</span><span class="sxs-lookup"><span data-stu-id="0cc86-295">Install MySQL Workbench</span></span>

1. <span data-ttu-id="0cc86-296">They check the [prerequisites and downloads MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).</span><span class="sxs-lookup"><span data-stu-id="0cc86-296">They check the [prerequisites and downloads MySQL Workbench](https://dev.mysql.com/downloads/workbench/?utm_source=tuicool).</span></span>
2. <span data-ttu-id="0cc86-297">They install MySQL Workbench for Windows in accordance with the [installation instructions](https://dev.mysql.com/doc/workbench/en/wb-installing.html).</span><span class="sxs-lookup"><span data-stu-id="0cc86-297">They install MySQL Workbench for Windows in accordance with the [installation instructions](https://dev.mysql.com/doc/workbench/en/wb-installing.html).</span></span> <span data-ttu-id="0cc86-298">The machine on which they install must be accessible to the OSTICKETMYSQL VM, and Azure via the internet.</span><span class="sxs-lookup"><span data-stu-id="0cc86-298">The machine on which they install must be accessible to the OSTICKETMYSQL VM, and Azure via the internet.</span></span>
3. <span data-ttu-id="0cc86-299">In MySQL Workbench, they create a MySQL connection to OSTICKETMYSQL.</span><span class="sxs-lookup"><span data-stu-id="0cc86-299">In MySQL Workbench, they create a MySQL connection to OSTICKETMYSQL.</span></span> 

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench1.png)

4. <span data-ttu-id="0cc86-301">They export the database as **osticket**, to a local self-contained file.</span><span class="sxs-lookup"><span data-stu-id="0cc86-301">They export the database as **osticket**, to a local self-contained file.</span></span>

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench2.png)

5. <span data-ttu-id="0cc86-303">After the database has been backed up locally, they create a connection to the Azure Database for MySQL instance.</span><span class="sxs-lookup"><span data-stu-id="0cc86-303">After the database has been backed up locally, they create a connection to the Azure Database for MySQL instance.</span></span>

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench3.png)

6. <span data-ttu-id="0cc86-305">Now, they can import (restore) the database in the Azure MySQL instance, from the self-contained file.</span><span class="sxs-lookup"><span data-stu-id="0cc86-305">Now, they can import (restore) the database in the Azure MySQL instance, from the self-contained file.</span></span> <span data-ttu-id="0cc86-306">A new schema (osticket) is created for the instance.</span><span class="sxs-lookup"><span data-stu-id="0cc86-306">A new schema (osticket) is created for the instance.</span></span>

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench4.png)

7. <span data-ttu-id="0cc86-308">After data is restored, it can be queried using Workbench, and appears in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0cc86-308">After data is restored, it can be queried using Workbench, and appears in the Azure portal.</span></span>

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench5.png)

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench6.png)

8. <span data-ttu-id="0cc86-311">Finally, they need to update the database information on the web apps.</span><span class="sxs-lookup"><span data-stu-id="0cc86-311">Finally, they need to update the database information on the web apps.</span></span> <span data-ttu-id="0cc86-312">On the MySQL instance, they open **Connection Strings**.</span><span class="sxs-lookup"><span data-stu-id="0cc86-312">On the MySQL instance, they open **Connection Strings**.</span></span> 

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench7.png)

9. <span data-ttu-id="0cc86-314">In the strings list, they locate the Web App settings, and click to copy them.</span><span class="sxs-lookup"><span data-stu-id="0cc86-314">In the strings list, they locate the Web App settings, and click to copy them.</span></span>

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench8.png)

10. <span data-ttu-id="0cc86-316">They open a Notepad window and paste the string into a new file, and update it to match the osticket database, MySQL instance, and credentials settings.</span><span class="sxs-lookup"><span data-stu-id="0cc86-316">They open a Notepad window and paste the string into a new file, and update it to match the osticket database, MySQL instance, and credentials settings.</span></span>

     ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench9.png)

11. <span data-ttu-id="0cc86-318">Tney can verify the server name and login from **Overview** in the MySQL instance in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0cc86-318">Tney can verify the server name and login from **Overview** in the MySQL instance in the Azure portal.</span></span>

    ![MySQL Workbench](./media/contoso-migration-refactor-linux-app-service-mysql/workbench10.png)


## <a name="step-5-set-up-github"></a><span data-ttu-id="0cc86-320">Step 5: Set up GitHub</span><span class="sxs-lookup"><span data-stu-id="0cc86-320">Step 5: Set up GitHub</span></span>

<span data-ttu-id="0cc86-321">Contoso admins create a new private GitHub repo, and sets up a connection to the osTicket database in Azure MySQL.</span><span class="sxs-lookup"><span data-stu-id="0cc86-321">Contoso admins create a new private GitHub repo, and sets up a connection to the osTicket database in Azure MySQL.</span></span> <span data-ttu-id="0cc86-322">Then, they load the Azure Web App with the app.</span><span class="sxs-lookup"><span data-stu-id="0cc86-322">Then, they load the Azure Web App with the app.</span></span>  

1.  <span data-ttu-id="0cc86-323">They browse to the OsTicket software public GitHub repo, and fork it to the Contoso GitHub account.</span><span class="sxs-lookup"><span data-stu-id="0cc86-323">They browse to the OsTicket software public GitHub repo, and fork it to the Contoso GitHub account.</span></span>

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github1.png)

2. <span data-ttu-id="0cc86-325">After forking, they navigate to the **include** folder, and find the **ost-config.php** file.</span><span class="sxs-lookup"><span data-stu-id="0cc86-325">After forking, they navigate to the **include** folder, and find the **ost-config.php** file.</span></span>

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github2.png)


3. <span data-ttu-id="0cc86-327">The file opens in the browser and they edit it.</span><span class="sxs-lookup"><span data-stu-id="0cc86-327">The file opens in the browser and they edit it.</span></span>

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github3.png)

4. <span data-ttu-id="0cc86-329">In the editor, they update the database details, specifically **DBHOST** and **DBUSER**.</span><span class="sxs-lookup"><span data-stu-id="0cc86-329">In the editor, they update the database details, specifically **DBHOST** and **DBUSER**.</span></span> 

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github4.png)

5. <span data-ttu-id="0cc86-331">Then they commit the changes.</span><span class="sxs-lookup"><span data-stu-id="0cc86-331">Then they commit the changes.</span></span>

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github5.png)

6. <span data-ttu-id="0cc86-333">For each web app (**osticket-eus2** and **osticket-cus**), they modify the **Application settings** in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0cc86-333">For each web app (**osticket-eus2** and **osticket-cus**), they modify the **Application settings** in the Azure portal.</span></span>

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github6.png)

7. <span data-ttu-id="0cc86-335">They enter the connection string with the name **osticket**, and copy the string from notepad into the **value area**.</span><span class="sxs-lookup"><span data-stu-id="0cc86-335">They enter the connection string with the name **osticket**, and copy the string from notepad into the **value area**.</span></span> <span data-ttu-id="0cc86-336">They select **MySQL** in the dropdown list next to the string, and save the settings.</span><span class="sxs-lookup"><span data-stu-id="0cc86-336">They select **MySQL** in the dropdown list next to the string, and save the settings.</span></span>

    ![GitHub](./media/contoso-migration-refactor-linux-app-service-mysql/github7.png)

## <a name="step-6-configure-the-web-apps"></a><span data-ttu-id="0cc86-338">Step 6: Configure the Web Apps</span><span class="sxs-lookup"><span data-stu-id="0cc86-338">Step 6: Configure the Web Apps</span></span>

<span data-ttu-id="0cc86-339">As the final step in the migration process, Contoso admins configure the web apps with the osTicket web sites.</span><span class="sxs-lookup"><span data-stu-id="0cc86-339">As the final step in the migration process, Contoso admins configure the web apps with the osTicket web sites.</span></span>



1. <span data-ttu-id="0cc86-340">In the primary web app (**osticket-eus2**) they open **Deployment option** and set the source to **GitHub**.</span><span class="sxs-lookup"><span data-stu-id="0cc86-340">In the primary web app (**osticket-eus2**) they open **Deployment option** and set the source to **GitHub**.</span></span>

    ![Configure app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app1.png)

2. <span data-ttu-id="0cc86-342">They select the deployment options.</span><span class="sxs-lookup"><span data-stu-id="0cc86-342">They select the deployment options.</span></span>

    ![Configure app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app2.png)

3. <span data-ttu-id="0cc86-344">After setting the options, the configuration shows as pending in the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="0cc86-344">After setting the options, the configuration shows as pending in the Azure portal.</span></span>

    ![Configure app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app3.png)

4. <span data-ttu-id="0cc86-346">After the configuration is updated and the osTicket web app is loaded from GitHub to the Docket container running the Azure App Service, the site shows as Active.</span><span class="sxs-lookup"><span data-stu-id="0cc86-346">After the configuration is updated and the osTicket web app is loaded from GitHub to the Docket container running the Azure App Service, the site shows as Active.</span></span>

    ![Configure app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app4.png)

5. <span data-ttu-id="0cc86-348">They repeat the above steps for the secondary web app (**osticket-cus**).</span><span class="sxs-lookup"><span data-stu-id="0cc86-348">They repeat the above steps for the secondary web app (**osticket-cus**).</span></span>
6. <span data-ttu-id="0cc86-349">After the site is configured, it's accessible via the Traffic Manager profile.</span><span class="sxs-lookup"><span data-stu-id="0cc86-349">After the site is configured, it's accessible via the Traffic Manager profile.</span></span> <span data-ttu-id="0cc86-350">The DNS name is the new location of the osTicket app.</span><span class="sxs-lookup"><span data-stu-id="0cc86-350">The DNS name is the new location of the osTicket app.</span></span> <span data-ttu-id="0cc86-351">[Learn more](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain#map-a-cname-record).</span><span class="sxs-lookup"><span data-stu-id="0cc86-351">[Learn more](https://docs.microsoft.com/azure/app-service/app-service-web-tutorial-custom-domain#map-a-cname-record).</span></span>

    ![Configure app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app5.png)
    
7. <span data-ttu-id="0cc86-353">Contoso wants a DNS name that's easy to remember.</span><span class="sxs-lookup"><span data-stu-id="0cc86-353">Contoso wants a DNS name that's easy to remember.</span></span> <span data-ttu-id="0cc86-354">They create an alias record (CNAME) **osticket.contoso.com** which points to the Traffic Manager name, in the DNS on their domain controllers.</span><span class="sxs-lookup"><span data-stu-id="0cc86-354">They create an alias record (CNAME) **osticket.contoso.com** which points to the Traffic Manager name, in the DNS on their domain controllers.</span></span>

    ![Configure app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app6.png)

8. <span data-ttu-id="0cc86-356">They configure both the **osticket-eus2** and **osticket-cus** web apps to allow the custom hostnames.</span><span class="sxs-lookup"><span data-stu-id="0cc86-356">They configure both the **osticket-eus2** and **osticket-cus** web apps to allow the custom hostnames.</span></span>

    ![Configure app](./media/contoso-migration-refactor-linux-app-service-mysql/configure-app7.png)

### <a name="set-up-autoscaling"></a><span data-ttu-id="0cc86-358">Set up autoscaling</span><span class="sxs-lookup"><span data-stu-id="0cc86-358">Set up autoscaling</span></span>

<span data-ttu-id="0cc86-359">Finally, they set up automatic scaling for the app.</span><span class="sxs-lookup"><span data-stu-id="0cc86-359">Finally, they set up automatic scaling for the app.</span></span> <span data-ttu-id="0cc86-360">This ensures that as agents use the app, the app instances increase and decrease according to business needs.</span><span class="sxs-lookup"><span data-stu-id="0cc86-360">This ensures that as agents use the app, the app instances increase and decrease according to business needs.</span></span> 

1. <span data-ttu-id="0cc86-361">In App Service **APP-SRV-EUS2**, they open **Scale Unit**.</span><span class="sxs-lookup"><span data-stu-id="0cc86-361">In App Service **APP-SRV-EUS2**, they open **Scale Unit**.</span></span>
2. <span data-ttu-id="0cc86-362">They configure a new autoscale setting with a single rule that increases the instance count by one when the CPU percentage for the current instance is above 70% for 10 minutes.</span><span class="sxs-lookup"><span data-stu-id="0cc86-362">They configure a new autoscale setting with a single rule that increases the instance count by one when the CPU percentage for the current instance is above 70% for 10 minutes.</span></span>

    ![Autoscale](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale1.png)

3. <span data-ttu-id="0cc86-364">They configure the same setting on **APP-SRV-CUS** to ensure that the same behavior applies if the app fails over to the secondary region.</span><span class="sxs-lookup"><span data-stu-id="0cc86-364">They configure the same setting on **APP-SRV-CUS** to ensure that the same behavior applies if the app fails over to the secondary region.</span></span> <span data-ttu-id="0cc86-365">The only difference is that they set the instance limit to 1 since this is for failovers only.</span><span class="sxs-lookup"><span data-stu-id="0cc86-365">The only difference is that they set the instance limit to 1 since this is for failovers only.</span></span>

   ![Autoscale](./media/contoso-migration-refactor-linux-app-service-mysql/autoscale2.png)

##  <a name="clean-up-after-migration"></a><span data-ttu-id="0cc86-367">Clean up after migration</span><span class="sxs-lookup"><span data-stu-id="0cc86-367">Clean up after migration</span></span>

<span data-ttu-id="0cc86-368">With migration complete, the osTicket app is refactored to running in an Azure Web app with continuous delivery using a private GitHub repo.</span><span class="sxs-lookup"><span data-stu-id="0cc86-368">With migration complete, the osTicket app is refactored to running in an Azure Web app with continuous delivery using a private GitHub repo.</span></span> <span data-ttu-id="0cc86-369">The app's running in two regions for increased resilience.</span><span class="sxs-lookup"><span data-stu-id="0cc86-369">The app's running in two regions for increased resilience.</span></span> <span data-ttu-id="0cc86-370">The osTicket database is running in Azure database for MySQL after migration to the PaaS platform.</span><span class="sxs-lookup"><span data-stu-id="0cc86-370">The osTicket database is running in Azure database for MySQL after migration to the PaaS platform.</span></span>

<span data-ttu-id="0cc86-371">For clean up, Contoso needs to do the following:</span><span class="sxs-lookup"><span data-stu-id="0cc86-371">For clean up, Contoso needs to do the following:</span></span> 
- <span data-ttu-id="0cc86-372">Remove the VMware VMs from the vCenter inventory.</span><span class="sxs-lookup"><span data-stu-id="0cc86-372">Remove the VMware VMs from the vCenter inventory.</span></span>
- <span data-ttu-id="0cc86-373">Remove the on-premises VMs from local backup jobs.</span><span class="sxs-lookup"><span data-stu-id="0cc86-373">Remove the on-premises VMs from local backup jobs.</span></span>
- <span data-ttu-id="0cc86-374">Update internal documentation show new locations and IP addresses.</span><span class="sxs-lookup"><span data-stu-id="0cc86-374">Update internal documentation show new locations and IP addresses.</span></span> 
- <span data-ttu-id="0cc86-375">Review any resources that interact with the on-premises VMs, and update any relevant settings or documentation to reflect the new configuration.</span><span class="sxs-lookup"><span data-stu-id="0cc86-375">Review any resources that interact with the on-premises VMs, and update any relevant settings or documentation to reflect the new configuration.</span></span>
- <span data-ttu-id="0cc86-376">Reconfigure monitoring to point at the osticket-trafficmanager.net URL, to track that the app is up and running.</span><span class="sxs-lookup"><span data-stu-id="0cc86-376">Reconfigure monitoring to point at the osticket-trafficmanager.net URL, to track that the app is up and running.</span></span>

## <a name="review-the-deployment"></a><span data-ttu-id="0cc86-377">Review the deployment</span><span class="sxs-lookup"><span data-stu-id="0cc86-377">Review the deployment</span></span>

<span data-ttu-id="0cc86-378">With the app now running, Contoso need to fully operationalize and secure their new infrastructure.</span><span class="sxs-lookup"><span data-stu-id="0cc86-378">With the app now running, Contoso need to fully operationalize and secure their new infrastructure.</span></span>

### <a name="security"></a><span data-ttu-id="0cc86-379">Security</span><span class="sxs-lookup"><span data-stu-id="0cc86-379">Security</span></span>

<span data-ttu-id="0cc86-380">The Contoso security team reviewed the app to determine any security issues.</span><span class="sxs-lookup"><span data-stu-id="0cc86-380">The Contoso security team reviewed the app to determine any security issues.</span></span> <span data-ttu-id="0cc86-381">They identified that the communication between the osTicket app and the MySQL database instance isn't configured for SSL.</span><span class="sxs-lookup"><span data-stu-id="0cc86-381">They identified that the communication between the osTicket app and the MySQL database instance isn't configured for SSL.</span></span> <span data-ttu-id="0cc86-382">They will need to do this to ensure that database traffic can't be hacked.</span><span class="sxs-lookup"><span data-stu-id="0cc86-382">They will need to do this to ensure that database traffic can't be hacked.</span></span> <span data-ttu-id="0cc86-383">[Learn more](https://docs.microsoft.com/azure/mysql/howto-configure-ssl).</span><span class="sxs-lookup"><span data-stu-id="0cc86-383">[Learn more](https://docs.microsoft.com/azure/mysql/howto-configure-ssl).</span></span>

### <a name="backups"></a><span data-ttu-id="0cc86-384">Backups</span><span class="sxs-lookup"><span data-stu-id="0cc86-384">Backups</span></span>

- <span data-ttu-id="0cc86-385">The osTicket web apps don't contain state data and thus don't need to be backed up.</span><span class="sxs-lookup"><span data-stu-id="0cc86-385">The osTicket web apps don't contain state data and thus don't need to be backed up.</span></span>
- <span data-ttu-id="0cc86-386">They don't need to configure backup for the database.</span><span class="sxs-lookup"><span data-stu-id="0cc86-386">They don't need to configure backup for the database.</span></span> <span data-ttu-id="0cc86-387">Azure Database for MySQL automatically creates server backups and stores.</span><span class="sxs-lookup"><span data-stu-id="0cc86-387">Azure Database for MySQL automatically creates server backups and stores.</span></span> <span data-ttu-id="0cc86-388">They selected to use geo-redundancy for the database, so it's resilient and production-ready.</span><span class="sxs-lookup"><span data-stu-id="0cc86-388">They selected to use geo-redundancy for the database, so it's resilient and production-ready.</span></span> <span data-ttu-id="0cc86-389">Backups can be used to restore your server to a point-in-time.</span><span class="sxs-lookup"><span data-stu-id="0cc86-389">Backups can be used to restore your server to a point-in-time.</span></span> <span data-ttu-id="0cc86-390">[Learn more](https://docs.microsoft.com/azure/mysql/concepts-backup).</span><span class="sxs-lookup"><span data-stu-id="0cc86-390">[Learn more](https://docs.microsoft.com/azure/mysql/concepts-backup).</span></span>


### <a name="licensing-and-cost-optimization"></a><span data-ttu-id="0cc86-391">Licensing and cost optimization</span><span class="sxs-lookup"><span data-stu-id="0cc86-391">Licensing and cost optimization</span></span>

- <span data-ttu-id="0cc86-392">There are no licensing issues for the PaaS deployment.</span><span class="sxs-lookup"><span data-stu-id="0cc86-392">There are no licensing issues for the PaaS deployment.</span></span>
- <span data-ttu-id="0cc86-393">Contoso will enable Azure Cost Management licensed by Cloudyn, a Microsoft subsidiary.</span><span class="sxs-lookup"><span data-stu-id="0cc86-393">Contoso will enable Azure Cost Management licensed by Cloudyn, a Microsoft subsidiary.</span></span> <span data-ttu-id="0cc86-394">It's a multi-cloud cost management solution that helps you to utilize and manage Azure and other cloud resources.</span><span class="sxs-lookup"><span data-stu-id="0cc86-394">It's a multi-cloud cost management solution that helps you to utilize and manage Azure and other cloud resources.</span></span>  <span data-ttu-id="0cc86-395">[Learn more](https://docs.microsoft.com/azure/cost-management/overview) about Azure Cost Management.</span><span class="sxs-lookup"><span data-stu-id="0cc86-395">[Learn more](https://docs.microsoft.com/azure/cost-management/overview) about Azure Cost Management.</span></span>



