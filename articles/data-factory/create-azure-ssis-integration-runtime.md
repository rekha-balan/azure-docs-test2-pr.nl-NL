---
title: Create Azure-SSIS integration runtime in Azure Data Factory | Microsoft Docs
description: Learn how to create an Azure-SSIS integration runtime in Azure Data Factory so you can deploy and run SSIS packages in Azure.
services: data-factory
documentationcenter: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 08/16/2018
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: a497ceab45bb3ace4e3f1ea063ef9c3e33818426
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44870569"
---
# <a name="create-the-azure-ssis-integration-runtime-in-azure-data-factory"></a><span data-ttu-id="6c5de-103">Create the Azure-SSIS integration runtime in Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="6c5de-103">Create the Azure-SSIS integration runtime in Azure Data Factory</span></span>
<span data-ttu-id="6c5de-104">This article provides steps for provisioning an Azure-SSIS integration runtime in Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="6c5de-104">This article provides steps for provisioning an Azure-SSIS integration runtime in Azure Data Factory.</span></span> <span data-ttu-id="6c5de-105">Then, you can use SQL Server Data Tools (SSDT) or SQL Server Management Studio (SSMS) to deploy and run SQL Server Integration Services (SSIS) packages in this runtime in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c5de-105">Then, you can use SQL Server Data Tools (SSDT) or SQL Server Management Studio (SSMS) to deploy and run SQL Server Integration Services (SSIS) packages in this runtime in Azure.</span></span> 

<span data-ttu-id="6c5de-106">The tutorial [Tutorial: deploy SQL Server Integration Services packages (SSIS) to Azure](tutorial-create-azure-ssis-runtime-portal.md) shows you how to create an Azure-SSIS Integration Runtime (IR) by using Azure SQL Database to host the SSIS Catalog.</span><span class="sxs-lookup"><span data-stu-id="6c5de-106">The tutorial [Tutorial: deploy SQL Server Integration Services packages (SSIS) to Azure](tutorial-create-azure-ssis-runtime-portal.md) shows you how to create an Azure-SSIS Integration Runtime (IR) by using Azure SQL Database to host the SSIS Catalog.</span></span> <span data-ttu-id="6c5de-107">This article expands on the tutorial and shows you how to do the following things:</span><span class="sxs-lookup"><span data-stu-id="6c5de-107">This article expands on the tutorial and shows you how to do the following things:</span></span> 

- <span data-ttu-id="6c5de-108">Optionally use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) as the database server to host your SSIS catalog (SSISDB database).</span><span class="sxs-lookup"><span data-stu-id="6c5de-108">Optionally use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) as the database server to host your SSIS catalog (SSISDB database).</span></span> <span data-ttu-id="6c5de-109">For guidance in choosing the type of database server to host SSISDB, see [Compare SQL Database and Managed Instance (Preview)](create-azure-ssis-integration-runtime.md#compare-sql-database-and-managed-instance-preview).</span><span class="sxs-lookup"><span data-stu-id="6c5de-109">For guidance in choosing the type of database server to host SSISDB, see [Compare SQL Database and Managed Instance (Preview)](create-azure-ssis-integration-runtime.md#compare-sql-database-and-managed-instance-preview).</span></span> <span data-ttu-id="6c5de-110">As a prerequisite, you  need to join your Azure-SSIS IR to a virtual network and configure virtual network permissions and settings as necessary.</span><span class="sxs-lookup"><span data-stu-id="6c5de-110">As a prerequisite, you  need to join your Azure-SSIS IR to a virtual network and configure virtual network permissions and settings as necessary.</span></span> <span data-ttu-id="6c5de-111">See [Join Azure-SSIS IR to a virtual network](https://docs.microsoft.com/en-us/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="6c5de-111">See [Join Azure-SSIS IR to a virtual network](https://docs.microsoft.com/en-us/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).</span></span> 

- <span data-ttu-id="6c5de-112">Optionally use Azure Active Directory (AAD) authentication with your Azure Data Factory Managed Service Identity (MSI) for Azure-SSIS IR to connect to the database server.</span><span class="sxs-lookup"><span data-stu-id="6c5de-112">Optionally use Azure Active Directory (AAD) authentication with your Azure Data Factory Managed Service Identity (MSI) for Azure-SSIS IR to connect to the database server.</span></span> <span data-ttu-id="6c5de-113">As a prerequisite, you will need to add your Data Factory MSI into an AAD group with access permissions to the database server, see [Enable AAD authentication for Azure-SSIS IR](https://docs.microsoft.com/en-us/azure/data-factory/enable-aad-authentication-azure-ssis-ir).</span><span class="sxs-lookup"><span data-stu-id="6c5de-113">As a prerequisite, you will need to add your Data Factory MSI into an AAD group with access permissions to the database server, see [Enable AAD authentication for Azure-SSIS IR](https://docs.microsoft.com/en-us/azure/data-factory/enable-aad-authentication-azure-ssis-ir).</span></span> 

## <a name="overview"></a><span data-ttu-id="6c5de-114">Overview</span><span class="sxs-lookup"><span data-stu-id="6c5de-114">Overview</span></span>
<span data-ttu-id="6c5de-115">This article shows different ways of provisioning an Azure-SSIS IR:</span><span class="sxs-lookup"><span data-stu-id="6c5de-115">This article shows different ways of provisioning an Azure-SSIS IR:</span></span> 

- [<span data-ttu-id="6c5de-116">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6c5de-116">Azure portal</span></span>](#azure-portal) 
- [<span data-ttu-id="6c5de-117">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c5de-117">Azure PowerShell</span></span>](#azure-powershell) 
- [<span data-ttu-id="6c5de-118">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="6c5de-118">Azure Resource Manager template</span></span>](#azure-resource-manager-template) 

<span data-ttu-id="6c5de-119">When you create an Azure-SSIS IR, Data Factory connects to your Azure SQL Database to prepare the SSIS Catalog database (SSISDB).</span><span class="sxs-lookup"><span data-stu-id="6c5de-119">When you create an Azure-SSIS IR, Data Factory connects to your Azure SQL Database to prepare the SSIS Catalog database (SSISDB).</span></span> <span data-ttu-id="6c5de-120">The script also configures permissions and settings for your virtual network, if specified, and joins the new instance of Azure-SSIS integration runtime to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-120">The script also configures permissions and settings for your virtual network, if specified, and joins the new instance of Azure-SSIS integration runtime to the virtual network.</span></span> 

<span data-ttu-id="6c5de-121">When you provision an instance of Azure-SSIS IR, the Azure Feature Pack for SSIS and the Access Redistributable are also installed.</span><span class="sxs-lookup"><span data-stu-id="6c5de-121">When you provision an instance of Azure-SSIS IR, the Azure Feature Pack for SSIS and the Access Redistributable are also installed.</span></span> <span data-ttu-id="6c5de-122">These components provide connectivity to Excel and Access files and to various Azure data sources, in addition to the data sources supported by the built-in components.</span><span class="sxs-lookup"><span data-stu-id="6c5de-122">These components provide connectivity to Excel and Access files and to various Azure data sources, in addition to the data sources supported by the built-in components.</span></span> <span data-ttu-id="6c5de-123">You can also install additional components.</span><span class="sxs-lookup"><span data-stu-id="6c5de-123">You can also install additional components.</span></span> <span data-ttu-id="6c5de-124">For more info, see [Custom setup for the Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md).</span><span class="sxs-lookup"><span data-stu-id="6c5de-124">For more info, see [Custom setup for the Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md).</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6c5de-125">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6c5de-125">Prerequisites</span></span> 
- <span data-ttu-id="6c5de-126">**Azure subscription**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-126">**Azure subscription**.</span></span> <span data-ttu-id="6c5de-127">If you don't have a subscription, you can create a [free trial](http://azure.microsoft.com/pricing/free-trial/) account.</span><span class="sxs-lookup"><span data-stu-id="6c5de-127">If you don't have a subscription, you can create a [free trial](http://azure.microsoft.com/pricing/free-trial/) account.</span></span> 

- <span data-ttu-id="6c5de-128">**Azure SQL Database server/Managed Instance (Preview)**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-128">**Azure SQL Database server/Managed Instance (Preview)**.</span></span> <span data-ttu-id="6c5de-129">If you don't already have a database server, create one in the Azure portal before you get started.</span><span class="sxs-lookup"><span data-stu-id="6c5de-129">If you don't already have a database server, create one in the Azure portal before you get started.</span></span> <span data-ttu-id="6c5de-130">This server hosts the SSIS Catalog database (SSISDB).</span><span class="sxs-lookup"><span data-stu-id="6c5de-130">This server hosts the SSIS Catalog database (SSISDB).</span></span> <span data-ttu-id="6c5de-131">We recommend that you create the database server in the same Azure region as the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-131">We recommend that you create the database server in the same Azure region as the integration runtime.</span></span> <span data-ttu-id="6c5de-132">This configuration lets the integration runtime write execution logs to SSISDB without crossing Azure regions.</span><span class="sxs-lookup"><span data-stu-id="6c5de-132">This configuration lets the integration runtime write execution logs to SSISDB without crossing Azure regions.</span></span> <span data-ttu-id="6c5de-133">Based on the selected database server, SSISDB can be created on your behalf as a single database, part of an Elastic Pool, or in a Managed Instance (Preview) and accessible in public network or by joining a virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-133">Based on the selected database server, SSISDB can be created on your behalf as a single database, part of an Elastic Pool, or in a Managed Instance (Preview) and accessible in public network or by joining a virtual network.</span></span> <span data-ttu-id="6c5de-134">For a list of supported pricing tiers for Azure SQL Database, see [SQL Database resource limits](../sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="6c5de-134">For a list of supported pricing tiers for Azure SQL Database, see [SQL Database resource limits](../sql-database/sql-database-resource-limits.md).</span></span> 

    <span data-ttu-id="6c5de-135">Make sure that your Azure SQL Database server or Managed Instance (Preview) does not already have an SSIS Catalog (SSIDB database).</span><span class="sxs-lookup"><span data-stu-id="6c5de-135">Make sure that your Azure SQL Database server or Managed Instance (Preview) does not already have an SSIS Catalog (SSIDB database).</span></span> <span data-ttu-id="6c5de-136">The provisioning of Azure-SSIS IR does not support using an existing SSIS Catalog.</span><span class="sxs-lookup"><span data-stu-id="6c5de-136">The provisioning of Azure-SSIS IR does not support using an existing SSIS Catalog.</span></span> 

- <span data-ttu-id="6c5de-137">**Classic or Azure Resource Manager virtual network (optional)**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-137">**Classic or Azure Resource Manager virtual network (optional)**.</span></span> <span data-ttu-id="6c5de-138">You must have an Azure virtual network if at least one of the following conditions is true:</span><span class="sxs-lookup"><span data-stu-id="6c5de-138">You must have an Azure virtual network if at least one of the following conditions is true:</span></span> 
    - <span data-ttu-id="6c5de-139">You are hosting the SSIS Catalog database in Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) that is inside a virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-139">You are hosting the SSIS Catalog database in Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) that is inside a virtual network.</span></span> 
    - <span data-ttu-id="6c5de-140">You want to connect to on-premises data stores from SSIS packages running on an Azure-SSIS integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-140">You want to connect to on-premises data stores from SSIS packages running on an Azure-SSIS integration runtime.</span></span> 

- <span data-ttu-id="6c5de-141">**Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-141">**Azure PowerShell**.</span></span> <span data-ttu-id="6c5de-142">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps), if you use PowerShell to run a script to provision Azure-SSIS integration runtime that runs SSIS packages in the cloud.</span><span class="sxs-lookup"><span data-stu-id="6c5de-142">Follow the instructions in [How to install and configure Azure PowerShell](/powershell/azure/install-azurerm-ps), if you use PowerShell to run a script to provision Azure-SSIS integration runtime that runs SSIS packages in the cloud.</span></span> 

### <a name="region-support"></a><span data-ttu-id="6c5de-143">Region support</span><span class="sxs-lookup"><span data-stu-id="6c5de-143">Region support</span></span>
<span data-ttu-id="6c5de-144">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span><span class="sxs-lookup"><span data-stu-id="6c5de-144">For a list of Azure regions in which Data Factory is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **Data Factory**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).</span></span>

<span data-ttu-id="6c5de-145">For a list of Azure regions in which the Azure-SSIS Integration Runtime is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **SSIS Integration Runtime**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).### Compare SQL Database and Managed Instance (Preview)</span><span class="sxs-lookup"><span data-stu-id="6c5de-145">For a list of Azure regions in which the Azure-SSIS Integration Runtime is currently available, select the regions that interest you on the following page, and then expand **Analytics** to locate **SSIS Integration Runtime**: [Products available by region](https://azure.microsoft.com/global-infrastructure/services/).### Compare SQL Database and Managed Instance (Preview)</span></span>

### <a name="compare-sql-database-and-managed-instance-preview"></a><span data-ttu-id="6c5de-146">Compare SQL Database and Managed Instance (Preview)</span><span class="sxs-lookup"><span data-stu-id="6c5de-146">Compare SQL Database and Managed Instance (Preview)</span></span>

<span data-ttu-id="6c5de-147">The following table compares certain features of SQL Database and Managed Instance (Preview) as they relate to the Azure-SSIR IR:</span><span class="sxs-lookup"><span data-stu-id="6c5de-147">The following table compares certain features of SQL Database and Managed Instance (Preview) as they relate to the Azure-SSIR IR:</span></span>

| <span data-ttu-id="6c5de-148">Feature</span><span class="sxs-lookup"><span data-stu-id="6c5de-148">Feature</span></span> | <span data-ttu-id="6c5de-149">SQL Database</span><span class="sxs-lookup"><span data-stu-id="6c5de-149">SQL Database</span></span> | <span data-ttu-id="6c5de-150">Managed Instance</span><span class="sxs-lookup"><span data-stu-id="6c5de-150">Managed Instance</span></span> |
|---------|--------------|------------------|
| <span data-ttu-id="6c5de-151">**Scheduling**</span><span class="sxs-lookup"><span data-stu-id="6c5de-151">**Scheduling**</span></span> | <span data-ttu-id="6c5de-152">SQL Server Agent is not available.</span><span class="sxs-lookup"><span data-stu-id="6c5de-152">SQL Server Agent is not available.</span></span><br/><br/><span data-ttu-id="6c5de-153">See [Schedule a package as part of an Azure Data Factory pipeline](/sql/integration-services/lift-shift/ssis-azure-schedule-packages#activity).</span><span class="sxs-lookup"><span data-stu-id="6c5de-153">See [Schedule a package as part of an Azure Data Factory pipeline](/sql/integration-services/lift-shift/ssis-azure-schedule-packages#activity).</span></span>| <span data-ttu-id="6c5de-154">SQL Server Agent is available.</span><span class="sxs-lookup"><span data-stu-id="6c5de-154">SQL Server Agent is available.</span></span> |
| <span data-ttu-id="6c5de-155">**Authentication**</span><span class="sxs-lookup"><span data-stu-id="6c5de-155">**Authentication**</span></span> | <span data-ttu-id="6c5de-156">You can create a database with a contained database user account which represents any Azure Active Directory user in the **dbmanager** role.</span><span class="sxs-lookup"><span data-stu-id="6c5de-156">You can create a database with a contained database user account which represents any Azure Active Directory user in the **dbmanager** role.</span></span><br/><br/><span data-ttu-id="6c5de-157">See [Enable Azure AD on Azure SQL Database](enable-aad-authentication-azure-ssis-ir.md#enable-azure-ad-on-azure-sql-database).</span><span class="sxs-lookup"><span data-stu-id="6c5de-157">See [Enable Azure AD on Azure SQL Database](enable-aad-authentication-azure-ssis-ir.md#enable-azure-ad-on-azure-sql-database).</span></span> | <span data-ttu-id="6c5de-158">You cannot create a database with a contained database user account which represents any Azure Active Directory user other than an Azure AD admin.</span><span class="sxs-lookup"><span data-stu-id="6c5de-158">You cannot create a database with a contained database user account which represents any Azure Active Directory user other than an Azure AD admin.</span></span> <br/><br/><span data-ttu-id="6c5de-159">See [Enable Azure AD on Azure SQL Database Managed Instance](enable-aad-authentication-azure-ssis-ir.md#enable-azure-ad-on-azure-sql-database-managed-instance).</span><span class="sxs-lookup"><span data-stu-id="6c5de-159">See [Enable Azure AD on Azure SQL Database Managed Instance](enable-aad-authentication-azure-ssis-ir.md#enable-azure-ad-on-azure-sql-database-managed-instance).</span></span> |
| <span data-ttu-id="6c5de-160">**Service tier**</span><span class="sxs-lookup"><span data-stu-id="6c5de-160">**Service tier**</span></span> | <span data-ttu-id="6c5de-161">When you create the Azure-SSIS IR on SQL Database, you can select the service tier for SSISDB.</span><span class="sxs-lookup"><span data-stu-id="6c5de-161">When you create the Azure-SSIS IR on SQL Database, you can select the service tier for SSISDB.</span></span> <span data-ttu-id="6c5de-162">There are multiple services tiers.</span><span class="sxs-lookup"><span data-stu-id="6c5de-162">There are multiple services tiers.</span></span> | <span data-ttu-id="6c5de-163">When you create the Azure-SSIS IR on a Managed Instance, you cannot select the service tier for SSISDB.</span><span class="sxs-lookup"><span data-stu-id="6c5de-163">When you create the Azure-SSIS IR on a Managed Instance, you cannot select the service tier for SSISDB.</span></span> <span data-ttu-id="6c5de-164">All databases on the same Managed Instance share the same resource allocated to that instance.</span><span class="sxs-lookup"><span data-stu-id="6c5de-164">All databases on the same Managed Instance share the same resource allocated to that instance.</span></span> |
| <span data-ttu-id="6c5de-165">**Virtual network**</span><span class="sxs-lookup"><span data-stu-id="6c5de-165">**Virtual network**</span></span> | <span data-ttu-id="6c5de-166">Supports both Azure Resource Manager and classic virtual networks.</span><span class="sxs-lookup"><span data-stu-id="6c5de-166">Supports both Azure Resource Manager and classic virtual networks.</span></span> | <span data-ttu-id="6c5de-167">Only supports Azure Resource Manager virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-167">Only supports Azure Resource Manager virtual network.</span></span> <span data-ttu-id="6c5de-168">The virtual network is required.</span><span class="sxs-lookup"><span data-stu-id="6c5de-168">The virtual network is required.</span></span><br/><br/><span data-ttu-id="6c5de-169">If you join your Azure-SSIS IR to the same virtual network as the Managed Instance, make sure that the Azure-SSIS IR is in a different subnet than the  Managed Instance.</span><span class="sxs-lookup"><span data-stu-id="6c5de-169">If you join your Azure-SSIS IR to the same virtual network as the Managed Instance, make sure that the Azure-SSIS IR is in a different subnet than the  Managed Instance.</span></span> <span data-ttu-id="6c5de-170">If you join the Azure-SSIS IR to a different virtual network than the Managed Instance, we recommend either virtual network peering (which is limited to the same region) or a virtual network to virtual network connection.</span><span class="sxs-lookup"><span data-stu-id="6c5de-170">If you join the Azure-SSIS IR to a different virtual network than the Managed Instance, we recommend either virtual network peering (which is limited to the same region) or a virtual network to virtual network connection.</span></span> <span data-ttu-id="6c5de-171">See [Connect your application to Azure SQL Database Managed Instance](../sql-database/sql-database-managed-instance-connect-app.md).</span><span class="sxs-lookup"><span data-stu-id="6c5de-171">See [Connect your application to Azure SQL Database Managed Instance](../sql-database/sql-database-managed-instance-connect-app.md).</span></span> |
| <span data-ttu-id="6c5de-172">**Distributed transactions**</span><span class="sxs-lookup"><span data-stu-id="6c5de-172">**Distributed transactions**</span></span> | <span data-ttu-id="6c5de-173">Microsoft Distributed Transaction Coordinator (MSDTC) transactions are not supported.</span><span class="sxs-lookup"><span data-stu-id="6c5de-173">Microsoft Distributed Transaction Coordinator (MSDTC) transactions are not supported.</span></span> <span data-ttu-id="6c5de-174">If your packages use MSDTC to coordinate distributed transactions, you may be able to implement a temporary solution by using Elastic Transactions for SQL Database.</span><span class="sxs-lookup"><span data-stu-id="6c5de-174">If your packages use MSDTC to coordinate distributed transactions, you may be able to implement a temporary solution by using Elastic Transactions for SQL Database.</span></span> <span data-ttu-id="6c5de-175">At this time, SSIS doesn't have built-in support for Elastic Transactions.</span><span class="sxs-lookup"><span data-stu-id="6c5de-175">At this time, SSIS doesn't have built-in support for Elastic Transactions.</span></span> <span data-ttu-id="6c5de-176">To use Elastic Transactions in your SSIS package, you have to write custom ADO.NET code in a Script Task.</span><span class="sxs-lookup"><span data-stu-id="6c5de-176">To use Elastic Transactions in your SSIS package, you have to write custom ADO.NET code in a Script Task.</span></span> <span data-ttu-id="6c5de-177">This script task must include the beginning and end of the transaction, and all the actions that have to occur inside the transaction.</span><span class="sxs-lookup"><span data-stu-id="6c5de-177">This script task must include the beginning and end of the transaction, and all the actions that have to occur inside the transaction.</span></span><br/><br/><span data-ttu-id="6c5de-178">For more info about coding elastic transactions, see [Elastic Database Transactions with Azure SQL Database](https://azure.microsoft.com/en-us/blog/elastic-database-transactions-with-azure-sql-database/).</span><span class="sxs-lookup"><span data-stu-id="6c5de-178">For more info about coding elastic transactions, see [Elastic Database Transactions with Azure SQL Database](https://azure.microsoft.com/en-us/blog/elastic-database-transactions-with-azure-sql-database/).</span></span> <span data-ttu-id="6c5de-179">For more info about elastic transactions in general, see [Distributed transactions across cloud databases](../sql-database/sql-database-elastic-transactions-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c5de-179">For more info about elastic transactions in general, see [Distributed transactions across cloud databases](../sql-database/sql-database-elastic-transactions-overview.md).</span></span> | <span data-ttu-id="6c5de-180">Not supported.</span><span class="sxs-lookup"><span data-stu-id="6c5de-180">Not supported.</span></span> |
| | | |

## <a name="azure-portal"></a><span data-ttu-id="6c5de-181">Azure portal</span><span class="sxs-lookup"><span data-stu-id="6c5de-181">Azure portal</span></span>
<span data-ttu-id="6c5de-182">In this section, you use the Azure portal, specifically the Data Factory UI, to create an Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="6c5de-182">In this section, you use the Azure portal, specifically the Data Factory UI, to create an Azure-SSIS IR.</span></span> 

### <a name="create-a-data-factory"></a><span data-ttu-id="6c5de-183">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="6c5de-183">Create a data factory</span></span> 
1. <span data-ttu-id="6c5de-184">Launch **Microsoft Edge** or **Google Chrome** web browser.</span><span class="sxs-lookup"><span data-stu-id="6c5de-184">Launch **Microsoft Edge** or **Google Chrome** web browser.</span></span> <span data-ttu-id="6c5de-185">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span><span class="sxs-lookup"><span data-stu-id="6c5de-185">Currently, Data Factory UI is supported only in Microsoft Edge and Google Chrome web browsers.</span></span> 
1. <span data-ttu-id="6c5de-186">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="6c5de-186">Log in to the [Azure portal](https://portal.azure.com/).</span></span> 
1. <span data-ttu-id="6c5de-187">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-187">Click **New** on the left menu, click **Data + Analytics**, and click **Data Factory**.</span></span> 

   ![New->DataFactory](./media/tutorial-create-azure-ssis-runtime-portal/new-data-factory-menu.png)

1. <span data-ttu-id="6c5de-189">In the **New data factory** page, enter **MyAzureSsisDataFactory** for the **name**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-189">In the **New data factory** page, enter **MyAzureSsisDataFactory** for the **name**.</span></span> 

   ![New data factory page](./media/tutorial-create-azure-ssis-runtime-portal/new-azure-data-factory.png)

   <span data-ttu-id="6c5de-191">The name of the Azure data factory must be **globally unique**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-191">The name of the Azure data factory must be **globally unique**.</span></span> <span data-ttu-id="6c5de-192">If you receive the following error, change the name of the data factory (for example, yournameMyAzureSsisDataFactory) and try creating again.</span><span class="sxs-lookup"><span data-stu-id="6c5de-192">If you receive the following error, change the name of the data factory (for example, yournameMyAzureSsisDataFactory) and try creating again.</span></span> <span data-ttu-id="6c5de-193">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="6c5de-193">See [Data Factory - Naming Rules](naming-rules.md) article for naming rules for Data Factory artifacts.</span></span> 

   `Data factory name “MyAzureSsisDataFactory” is not available`

1. <span data-ttu-id="6c5de-194">Select your Azure **subscription** in which you want to create the data factory.</span><span class="sxs-lookup"><span data-stu-id="6c5de-194">Select your Azure **subscription** in which you want to create the data factory.</span></span> 
1. <span data-ttu-id="6c5de-195">For the **Resource Group**, do one of the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c5de-195">For the **Resource Group**, do one of the following steps:</span></span> 

   - <span data-ttu-id="6c5de-196">Select **Use existing**, and select an existing resource group from the drop-down list.</span><span class="sxs-lookup"><span data-stu-id="6c5de-196">Select **Use existing**, and select an existing resource group from the drop-down list.</span></span> 
   - <span data-ttu-id="6c5de-197">Select **Create new**, and enter the name of a resource group.</span><span class="sxs-lookup"><span data-stu-id="6c5de-197">Select **Create new**, and enter the name of a resource group.</span></span> 

   <span data-ttu-id="6c5de-198">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="6c5de-198">To learn about resource groups, see [Using resource groups to manage your Azure resources](../azure-resource-manager/resource-group-overview.md).</span></span> 

1. <span data-ttu-id="6c5de-199">Select **V2** for the **version**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-199">Select **V2** for the **version**.</span></span> 
1. <span data-ttu-id="6c5de-200">Select the **location** for the data factory.</span><span class="sxs-lookup"><span data-stu-id="6c5de-200">Select the **location** for the data factory.</span></span> <span data-ttu-id="6c5de-201">Only locations that are supported for creation of data factories are shown in the list.</span><span class="sxs-lookup"><span data-stu-id="6c5de-201">Only locations that are supported for creation of data factories are shown in the list.</span></span> 
1. <span data-ttu-id="6c5de-202">Select **Pin to dashboard**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-202">Select **Pin to dashboard**.</span></span> 
1. <span data-ttu-id="6c5de-203">Click **Create**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-203">Click **Create**.</span></span> 
1. <span data-ttu-id="6c5de-204">On the dashboard, you see the following tile with status: **Deploying data factory**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-204">On the dashboard, you see the following tile with status: **Deploying data factory**.</span></span> 

    ![deploying data factory tile](media/tutorial-create-azure-ssis-runtime-portal/deploying-data-factory.png)

1. <span data-ttu-id="6c5de-206">After the creation is complete, you see the **Data Factory** page as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="6c5de-206">After the creation is complete, you see the **Data Factory** page as shown in the image.</span></span> 

    ![Data factory home page](./media/tutorial-create-azure-ssis-runtime-portal/data-factory-home-page.png)

1. <span data-ttu-id="6c5de-208">Click **Author & Monitor** to launch the Data Factory User Interface (UI) in a separate tab.</span><span class="sxs-lookup"><span data-stu-id="6c5de-208">Click **Author & Monitor** to launch the Data Factory User Interface (UI) in a separate tab.</span></span> 

### <a name="provision-an-azure-ssis-integration-runtime"></a><span data-ttu-id="6c5de-209">Provision an Azure SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="6c5de-209">Provision an Azure SSIS integration runtime</span></span> 
1. <span data-ttu-id="6c5de-210">In the get started page, click **Configure SSIS Integration Runtime** tile.</span><span class="sxs-lookup"><span data-stu-id="6c5de-210">In the get started page, click **Configure SSIS Integration Runtime** tile.</span></span> 

   ![Configure SSIS Integration Runtime tile](./media/tutorial-create-azure-ssis-runtime-portal/configure-ssis-integration-runtime-tile.png)

1. <span data-ttu-id="6c5de-212">On the **General Settings** page of **Integration Runtime Setup**, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c5de-212">On the **General Settings** page of **Integration Runtime Setup**, complete the following steps:</span></span> 

   ![General settings](./media/tutorial-create-azure-ssis-runtime-portal/general-settings.png)

    <span data-ttu-id="6c5de-214">a.</span><span class="sxs-lookup"><span data-stu-id="6c5de-214">a.</span></span> <span data-ttu-id="6c5de-215">For **Name**, enter the name of your integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-215">For **Name**, enter the name of your integration runtime.</span></span> 

    <span data-ttu-id="6c5de-216">b.</span><span class="sxs-lookup"><span data-stu-id="6c5de-216">b.</span></span> <span data-ttu-id="6c5de-217">For **Description**, enter the description of your integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-217">For **Description**, enter the description of your integration runtime.</span></span> 

    <span data-ttu-id="6c5de-218">c.</span><span class="sxs-lookup"><span data-stu-id="6c5de-218">c.</span></span> <span data-ttu-id="6c5de-219">For **Location**, select the location of your integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-219">For **Location**, select the location of your integration runtime.</span></span> <span data-ttu-id="6c5de-220">Only supported locations are displayed.</span><span class="sxs-lookup"><span data-stu-id="6c5de-220">Only supported locations are displayed.</span></span> <span data-ttu-id="6c5de-221">We recommend that you select the same location of your database server to host SSISDB.</span><span class="sxs-lookup"><span data-stu-id="6c5de-221">We recommend that you select the same location of your database server to host SSISDB.</span></span> 

    <span data-ttu-id="6c5de-222">d.</span><span class="sxs-lookup"><span data-stu-id="6c5de-222">d.</span></span> <span data-ttu-id="6c5de-223">For **Node Size**, select the size of node in your integration runtime cluster.</span><span class="sxs-lookup"><span data-stu-id="6c5de-223">For **Node Size**, select the size of node in your integration runtime cluster.</span></span> <span data-ttu-id="6c5de-224">Only supported node sizes are displayed.</span><span class="sxs-lookup"><span data-stu-id="6c5de-224">Only supported node sizes are displayed.</span></span> <span data-ttu-id="6c5de-225">Select a large node size (scale up), if you want to run many compute/memory –intensive packages.</span><span class="sxs-lookup"><span data-stu-id="6c5de-225">Select a large node size (scale up), if you want to run many compute/memory –intensive packages.</span></span> 

    <span data-ttu-id="6c5de-226">e.</span><span class="sxs-lookup"><span data-stu-id="6c5de-226">e.</span></span> <span data-ttu-id="6c5de-227">For **Node Number**, select the number of nodes in your integration runtime cluster.</span><span class="sxs-lookup"><span data-stu-id="6c5de-227">For **Node Number**, select the number of nodes in your integration runtime cluster.</span></span> <span data-ttu-id="6c5de-228">Only supported node numbers are displayed.</span><span class="sxs-lookup"><span data-stu-id="6c5de-228">Only supported node numbers are displayed.</span></span> <span data-ttu-id="6c5de-229">Select a large cluster with many nodes (scale out), if you want to run many packages in parallel.</span><span class="sxs-lookup"><span data-stu-id="6c5de-229">Select a large cluster with many nodes (scale out), if you want to run many packages in parallel.</span></span> 

    <span data-ttu-id="6c5de-230">f.</span><span class="sxs-lookup"><span data-stu-id="6c5de-230">f.</span></span> <span data-ttu-id="6c5de-231">For **Edition/License**, select SQL Server edition/license for your integration runtime: Standard or Enterprise.</span><span class="sxs-lookup"><span data-stu-id="6c5de-231">For **Edition/License**, select SQL Server edition/license for your integration runtime: Standard or Enterprise.</span></span> <span data-ttu-id="6c5de-232">Select Enterprise, if you want to use advanced/premium features on your integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-232">Select Enterprise, if you want to use advanced/premium features on your integration runtime.</span></span> 

    <span data-ttu-id="6c5de-233">g.</span><span class="sxs-lookup"><span data-stu-id="6c5de-233">g.</span></span> <span data-ttu-id="6c5de-234">For **Save Money**, select Azure Hybrid Benefit (AHB) option for your integration runtime: Yes or No.</span><span class="sxs-lookup"><span data-stu-id="6c5de-234">For **Save Money**, select Azure Hybrid Benefit (AHB) option for your integration runtime: Yes or No.</span></span> <span data-ttu-id="6c5de-235">Select Yes, if you want to bring your own SQL Server license with Software Assurance to benefit from cost savings with hybrid use.</span><span class="sxs-lookup"><span data-stu-id="6c5de-235">Select Yes, if you want to bring your own SQL Server license with Software Assurance to benefit from cost savings with hybrid use.</span></span> 

    <span data-ttu-id="6c5de-236">h.</span><span class="sxs-lookup"><span data-stu-id="6c5de-236">h.</span></span> <span data-ttu-id="6c5de-237">Click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-237">Click **Next**.</span></span> 

1. <span data-ttu-id="6c5de-238">On the **SQL Settings** page, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c5de-238">On the **SQL Settings** page, complete the following steps:</span></span> 

   ![SQL settings](./media/tutorial-create-azure-ssis-runtime-portal/sql-settings.png)

    <span data-ttu-id="6c5de-240">a.</span><span class="sxs-lookup"><span data-stu-id="6c5de-240">a.</span></span> <span data-ttu-id="6c5de-241">For **Subscription**, select the Azure subscription that has your database server to host SSISDB.</span><span class="sxs-lookup"><span data-stu-id="6c5de-241">For **Subscription**, select the Azure subscription that has your database server to host SSISDB.</span></span> 

    <span data-ttu-id="6c5de-242">b.</span><span class="sxs-lookup"><span data-stu-id="6c5de-242">b.</span></span> <span data-ttu-id="6c5de-243">For **Location**, select the location of your database server to host SSISDB.</span><span class="sxs-lookup"><span data-stu-id="6c5de-243">For **Location**, select the location of your database server to host SSISDB.</span></span> <span data-ttu-id="6c5de-244">We recommend that you select the same location of your integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-244">We recommend that you select the same location of your integration runtime.</span></span> 

    <span data-ttu-id="6c5de-245">c.</span><span class="sxs-lookup"><span data-stu-id="6c5de-245">c.</span></span> <span data-ttu-id="6c5de-246">For **Catalog Database Server Endpoint**, select the endpoint of your database server to host SSISDB.</span><span class="sxs-lookup"><span data-stu-id="6c5de-246">For **Catalog Database Server Endpoint**, select the endpoint of your database server to host SSISDB.</span></span> <span data-ttu-id="6c5de-247">Based on the selected database server, SSISDB can be created on your behalf as a single database, part of an Elastic Pool, or in a Managed Instance (Preview) and accessible in public network or by joining a virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-247">Based on the selected database server, SSISDB can be created on your behalf as a single database, part of an Elastic Pool, or in a Managed Instance (Preview) and accessible in public network or by joining a virtual network.</span></span> 

    <span data-ttu-id="6c5de-248">d.</span><span class="sxs-lookup"><span data-stu-id="6c5de-248">d.</span></span> <span data-ttu-id="6c5de-249">On **Use AAD authentication...** checkbox, select the authentication method for your database server to host SSISDB: SQL or Azure Active Directory (AAD) with your Azure Data Factory Managed Service Identity (MSI).</span><span class="sxs-lookup"><span data-stu-id="6c5de-249">On **Use AAD authentication...** checkbox, select the authentication method for your database server to host SSISDB: SQL or Azure Active Directory (AAD) with your Azure Data Factory Managed Service Identity (MSI).</span></span> <span data-ttu-id="6c5de-250">If you check it, you need to add your Data Factory MSI into an AAD group with access permissions to the database server, see [Enable AAD authentication for Azure-SSIS IR](https://docs.microsoft.com/en-us/azure/data-factory/enable-aad-authentication-azure-ssis-ir).</span><span class="sxs-lookup"><span data-stu-id="6c5de-250">If you check it, you need to add your Data Factory MSI into an AAD group with access permissions to the database server, see [Enable AAD authentication for Azure-SSIS IR](https://docs.microsoft.com/en-us/azure/data-factory/enable-aad-authentication-azure-ssis-ir).</span></span> 

    <span data-ttu-id="6c5de-251">e.</span><span class="sxs-lookup"><span data-stu-id="6c5de-251">e.</span></span> <span data-ttu-id="6c5de-252">For **Admin Username**, enter SQL authentication username for your database server to host SSISDB.</span><span class="sxs-lookup"><span data-stu-id="6c5de-252">For **Admin Username**, enter SQL authentication username for your database server to host SSISDB.</span></span> 

    <span data-ttu-id="6c5de-253">f.</span><span class="sxs-lookup"><span data-stu-id="6c5de-253">f.</span></span> <span data-ttu-id="6c5de-254">For **Admin Password**, enter SQL authentication password for your database server to host SSISDB.</span><span class="sxs-lookup"><span data-stu-id="6c5de-254">For **Admin Password**, enter SQL authentication password for your database server to host SSISDB.</span></span> 

    <span data-ttu-id="6c5de-255">g.</span><span class="sxs-lookup"><span data-stu-id="6c5de-255">g.</span></span> <span data-ttu-id="6c5de-256">For **Catalog Database Service Tier**, select the service tier for your database server to host SSISDB: Basic/Standard/Premium tier or Elastic Pool name.</span><span class="sxs-lookup"><span data-stu-id="6c5de-256">For **Catalog Database Service Tier**, select the service tier for your database server to host SSISDB: Basic/Standard/Premium tier or Elastic Pool name.</span></span> 

    <span data-ttu-id="6c5de-257">h.</span><span class="sxs-lookup"><span data-stu-id="6c5de-257">h.</span></span> <span data-ttu-id="6c5de-258">Click **Test Connection** and if successful, click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-258">Click **Test Connection** and if successful, click **Next**.</span></span> 

1.  <span data-ttu-id="6c5de-259">On the **Advanced Settings** page, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c5de-259">On the **Advanced Settings** page, complete the following steps:</span></span> 

    ![Advanced settings](./media/tutorial-create-azure-ssis-runtime-portal/advanced-settings.png)

    <span data-ttu-id="6c5de-261">a.</span><span class="sxs-lookup"><span data-stu-id="6c5de-261">a.</span></span> <span data-ttu-id="6c5de-262">For **Maximum Parallel Executions Per Node**, select the maximum number of packages to execute concurrently per node in your integration runtime cluster.</span><span class="sxs-lookup"><span data-stu-id="6c5de-262">For **Maximum Parallel Executions Per Node**, select the maximum number of packages to execute concurrently per node in your integration runtime cluster.</span></span> <span data-ttu-id="6c5de-263">Only supported package numbers are displayed.</span><span class="sxs-lookup"><span data-stu-id="6c5de-263">Only supported package numbers are displayed.</span></span> <span data-ttu-id="6c5de-264">Select a low number, if you want to use more than one core to run a single large/heavy-weight package that is compute/memory -intensive.</span><span class="sxs-lookup"><span data-stu-id="6c5de-264">Select a low number, if you want to use more than one core to run a single large/heavy-weight package that is compute/memory -intensive.</span></span> <span data-ttu-id="6c5de-265">Select a high number, if you want to run one or more small/light-weight packages in a single core.</span><span class="sxs-lookup"><span data-stu-id="6c5de-265">Select a high number, if you want to run one or more small/light-weight packages in a single core.</span></span> 

    <span data-ttu-id="6c5de-266">b.</span><span class="sxs-lookup"><span data-stu-id="6c5de-266">b.</span></span> <span data-ttu-id="6c5de-267">For **Custom Setup Container SAS URI**, optionally enter Shared Access Signature (SAS) Uniform Resource Identifier (URI) of your Azure Storage Blob container where your setup script and its associated files are stored, see [Custom setup for Azure-SSIS IR](https://docs.microsoft.com/en-us/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup).</span><span class="sxs-lookup"><span data-stu-id="6c5de-267">For **Custom Setup Container SAS URI**, optionally enter Shared Access Signature (SAS) Uniform Resource Identifier (URI) of your Azure Storage Blob container where your setup script and its associated files are stored, see [Custom setup for Azure-SSIS IR](https://docs.microsoft.com/en-us/azure/data-factory/how-to-configure-azure-ssis-ir-custom-setup).</span></span> 

1. <span data-ttu-id="6c5de-268">On **Select a virtual network...** checkbox, select whether you want to join your integration runtime to a virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-268">On **Select a virtual network...** checkbox, select whether you want to join your integration runtime to a virtual network.</span></span> <span data-ttu-id="6c5de-269">Check it if you use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) to host SSISDB or require access to on-premises data; that is, you have on-premises data sources/destinations in your SSIS packages, see [Join Azure-SSIS IR to a virtual network](https://docs.microsoft.com/en-us/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="6c5de-269">Check it if you use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) to host SSISDB or require access to on-premises data; that is, you have on-premises data sources/destinations in your SSIS packages, see [Join Azure-SSIS IR to a virtual network](https://docs.microsoft.com/en-us/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).</span></span> <span data-ttu-id="6c5de-270">If you check it, complete the following steps:</span><span class="sxs-lookup"><span data-stu-id="6c5de-270">If you check it, complete the following steps:</span></span> 

   ![Advanced settings with virtual network](./media/tutorial-create-azure-ssis-runtime-portal/advanced-settings-vnet.png)

    <span data-ttu-id="6c5de-272">a.</span><span class="sxs-lookup"><span data-stu-id="6c5de-272">a.</span></span> <span data-ttu-id="6c5de-273">For **Subscription**, select the Azure subscription that has your virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-273">For **Subscription**, select the Azure subscription that has your virtual network.</span></span> 

    <span data-ttu-id="6c5de-274">b.</span><span class="sxs-lookup"><span data-stu-id="6c5de-274">b.</span></span> <span data-ttu-id="6c5de-275">For **Location**, the same location of your integration runtime is selected.</span><span class="sxs-lookup"><span data-stu-id="6c5de-275">For **Location**, the same location of your integration runtime is selected.</span></span> 

    <span data-ttu-id="6c5de-276">c.</span><span class="sxs-lookup"><span data-stu-id="6c5de-276">c.</span></span> <span data-ttu-id="6c5de-277">For **Type**, select the type of your virtual network: Classic or Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6c5de-277">For **Type**, select the type of your virtual network: Classic or Azure Resource Manager.</span></span> <span data-ttu-id="6c5de-278">We recommend that you select Azure Resource Manager virtual network, since Classic virtual network will be deprecated soon.</span><span class="sxs-lookup"><span data-stu-id="6c5de-278">We recommend that you select Azure Resource Manager virtual network, since Classic virtual network will be deprecated soon.</span></span> 

    <span data-ttu-id="6c5de-279">d.</span><span class="sxs-lookup"><span data-stu-id="6c5de-279">d.</span></span> <span data-ttu-id="6c5de-280">For **VNet Name**, select the name of your virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-280">For **VNet Name**, select the name of your virtual network.</span></span> <span data-ttu-id="6c5de-281">This virtual network should be the same virtual network used for Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) to host SSISDB and or the one connected to your on-premises network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-281">This virtual network should be the same virtual network used for Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) to host SSISDB and or the one connected to your on-premises network.</span></span> 

    <span data-ttu-id="6c5de-282">e.</span><span class="sxs-lookup"><span data-stu-id="6c5de-282">e.</span></span> <span data-ttu-id="6c5de-283">For **Subnet Name**, select the name of subnet for your virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-283">For **Subnet Name**, select the name of subnet for your virtual network.</span></span> <span data-ttu-id="6c5de-284">This should be a different subnet than the one used for Managed Instance (Preview) to host SSISDB.</span><span class="sxs-lookup"><span data-stu-id="6c5de-284">This should be a different subnet than the one used for Managed Instance (Preview) to host SSISDB.</span></span> 

1. <span data-ttu-id="6c5de-285">Click **VNet Validation** and if successful, click **Finish** to start the creation of your Azure-SSIS integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-285">Click **VNet Validation** and if successful, click **Finish** to start the creation of your Azure-SSIS integration runtime.</span></span> 

    > [!IMPORTANT]
    > - <span data-ttu-id="6c5de-286">This process takes approximately 20 to 30 minutes to complete</span><span class="sxs-lookup"><span data-stu-id="6c5de-286">This process takes approximately 20 to 30 minutes to complete</span></span>
    > - <span data-ttu-id="6c5de-287">The Data Factory service connects to your Azure SQL Database to prepare the SSIS Catalog database (SSISDB).</span><span class="sxs-lookup"><span data-stu-id="6c5de-287">The Data Factory service connects to your Azure SQL Database to prepare the SSIS Catalog database (SSISDB).</span></span> <span data-ttu-id="6c5de-288">The script also configures permissions and settings for your virtual network, if specified, and joins the new instance of Azure-SSIS integration runtime to the virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-288">The script also configures permissions and settings for your virtual network, if specified, and joins the new instance of Azure-SSIS integration runtime to the virtual network.</span></span> 

1. <span data-ttu-id="6c5de-289">In the **Connections** window, switch to **Integration Runtimes** if needed.</span><span class="sxs-lookup"><span data-stu-id="6c5de-289">In the **Connections** window, switch to **Integration Runtimes** if needed.</span></span> <span data-ttu-id="6c5de-290">Click **Refresh** to refresh the status.</span><span class="sxs-lookup"><span data-stu-id="6c5de-290">Click **Refresh** to refresh the status.</span></span> 

   ![Creation status](./media/tutorial-create-azure-ssis-runtime-portal/azure-ssis-ir-creation-status.png)

1. <span data-ttu-id="6c5de-292">Use the links under **Actions** column to stop/start, edit, or delete the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-292">Use the links under **Actions** column to stop/start, edit, or delete the integration runtime.</span></span> <span data-ttu-id="6c5de-293">Use the last link to view JSON code for the integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-293">Use the last link to view JSON code for the integration runtime.</span></span> <span data-ttu-id="6c5de-294">The edit and delete buttons are enabled only when the IR is stopped.</span><span class="sxs-lookup"><span data-stu-id="6c5de-294">The edit and delete buttons are enabled only when the IR is stopped.</span></span> 

   ![Azure SSIS IR - actions](./media/tutorial-create-azure-ssis-runtime-portal/azure-ssis-ir-actions.png)

### <a name="azure-ssis-integration-runtimes-in-the-portal"></a><span data-ttu-id="6c5de-296">Azure SSIS integration runtimes in the portal</span><span class="sxs-lookup"><span data-stu-id="6c5de-296">Azure SSIS integration runtimes in the portal</span></span>
1. <span data-ttu-id="6c5de-297">In the Azure Data Factory UI, switch to the **Edit** tab, click **Connections**, and then switch to **Integration Runtimes** tab to view existing integration runtimes in your data factory.</span><span class="sxs-lookup"><span data-stu-id="6c5de-297">In the Azure Data Factory UI, switch to the **Edit** tab, click **Connections**, and then switch to **Integration Runtimes** tab to view existing integration runtimes in your data factory.</span></span> 

   ![View existing IRs](./media/tutorial-create-azure-ssis-runtime-portal/view-azure-ssis-integration-runtimes.png)

1. <span data-ttu-id="6c5de-299">Click **New** to create a new Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="6c5de-299">Click **New** to create a new Azure-SSIS IR.</span></span> 

   ![Integration runtime via menu](./media/tutorial-create-azure-ssis-runtime-portal/edit-connections-new-integration-runtime-button.png)

1. <span data-ttu-id="6c5de-301">To create an Azure-SSIS integration runtime, click **New** as shown in the image.</span><span class="sxs-lookup"><span data-stu-id="6c5de-301">To create an Azure-SSIS integration runtime, click **New** as shown in the image.</span></span> 
1. <span data-ttu-id="6c5de-302">In the Integration Runtime Setup window, select **Lift-and-shift existing SSIS packages to execute in Azure**, and then click **Next**.</span><span class="sxs-lookup"><span data-stu-id="6c5de-302">In the Integration Runtime Setup window, select **Lift-and-shift existing SSIS packages to execute in Azure**, and then click **Next**.</span></span> 

   ![Specify the type of integration runtime](./media/tutorial-create-azure-ssis-runtime-portal/integration-runtime-setup-options.png)

1. <span data-ttu-id="6c5de-304">See the [Provision an Azure SSIS integration runtime](#provision-an-azure-ssis-integration-runtime) section for the remaining steps to set up an Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="6c5de-304">See the [Provision an Azure SSIS integration runtime](#provision-an-azure-ssis-integration-runtime) section for the remaining steps to set up an Azure-SSIS IR.</span></span> 

## <a name="azure-powershell"></a><span data-ttu-id="6c5de-305">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="6c5de-305">Azure PowerShell</span></span>
<span data-ttu-id="6c5de-306">In this section, you use the Azure PowerShell to create an Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="6c5de-306">In this section, you use the Azure PowerShell to create an Azure-SSIS IR.</span></span>

### <a name="create-variables"></a><span data-ttu-id="6c5de-307">Create variables</span><span class="sxs-lookup"><span data-stu-id="6c5de-307">Create variables</span></span>
<span data-ttu-id="6c5de-308">Define variables for use in the script in this tutorial:</span><span class="sxs-lookup"><span data-stu-id="6c5de-308">Define variables for use in the script in this tutorial:</span></span>

```powershell
### Azure Data Factory information 
# If your input contains a PSH special character, e.g. "$", precede it with the escape character "`" like "`$".
$SubscriptionName = "[your Azure subscription name]"
$ResourceGroupName = "[your Azure resource group name]"
$DataFactoryName = "[your data factory name]"
$DataFactoryLocation = "EastUS" 

### Azure-SSIS integration runtime information - This is the Data Factory compute resource for running SSIS packages
$AzureSSISName = "[specify a name for your Azure-SSIS IR]"
$AzureSSISDescription = "[specify a description for your Azure-SSIS IR]"
$AzureSSISLocation = "EastUS" 
# Only Standard_A4_v2|Standard_A8_v2|Standard_D1_v2|Standard_D2_v2|Standard_D3_v2|Standard_D4_v2 are supported.
$AzureSSISNodeSize = "Standard_D4_v2"
# Only 1-10 nodes are supported.
$AzureSSISNodeNumber = 2 
# Azure-SSIS IR edition/license info: Standard or Enterprise 
$AzureSSISEdition = "" # Standard by default, while Enterprise lets you use advanced/premium features on your Azure-SSIS IR
# Azure-SSIS IR hybrid usage info: LicenseIncluded or BasePrice
$AzureSSISLicenseType = "" # LicenseIncluded by default, while BasePrice lets you bring your own on-premises SQL Server license with Software Assurance to earn cost savings from Azure Hybrid Benefit (AHB) option
# For a Standard_D1_v2 node, 1-4 parallel executions per node are supported. For other nodes, it's 1-8.
$AzureSSISMaxParallelExecutionsPerNode = 8 
# Custom setup info
$SetupScriptContainerSasUri = "" # OPTIONAL to provide SAS URI of blob container where your custom setup script and its associated files are stored
# Virtual network info: Classic or Azure Resource Manager
$VnetId = "[your virtual network resource ID or leave it empty]" # REQUIRED if you use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview)/on-premises data, Azure Resource Manager virtual network is recommended, Classic virtual network will be deprecated soon    
$SubnetName = "[your subnet name or leave it empty]" # WARNING: Please use a different subnet than the one used for your Managed Instance (Preview)

### SSISDB info
$SSISDBServerEndpoint = "[your Azure SQL Database server name or Managed Instance (Preview) name.DNS prefix].database.windows.net" # WARNING: Please ensure that there is no existing SSISDB, so we can prepare and manage one on your behalf
# Authentication info: SQL or Azure Active Directory (AAD)
$SSISDBServerAdminUserName = "[your server admin username for SQL authentication or leave it empty for AAD authentication]"
$SSISDBServerAdminPassword = "[your server admin password for SQL authentication or leave it empty for AAD authentication]"
$SSISDBPricingTier = "[Basic|S0|S1|S2|S3|S4|S6|S7|S9|S12|P1|P2|P4|P6|P11|P15|…|ELASTIC_POOL(name = <elastic_pool_name>) for Azure SQL Database or leave it empty for Managed Instance (Preview)]"
```

### <a name="log-in-and-select-subscription"></a><span data-ttu-id="6c5de-309">Log in and select subscription</span><span class="sxs-lookup"><span data-stu-id="6c5de-309">Log in and select subscription</span></span>
<span data-ttu-id="6c5de-310">Add the following code the script to log in and select your Azure subscription:</span><span class="sxs-lookup"><span data-stu-id="6c5de-310">Add the following code the script to log in and select your Azure subscription:</span></span> 

```powershell
Connect-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $SubscriptionName
```

### <a name="validate-the-connection-to-database"></a><span data-ttu-id="6c5de-311">Validate the connection to database</span><span class="sxs-lookup"><span data-stu-id="6c5de-311">Validate the connection to database</span></span>
<span data-ttu-id="6c5de-312">Add the following script to validate your Azure SQL Database server endpoint.</span><span class="sxs-lookup"><span data-stu-id="6c5de-312">Add the following script to validate your Azure SQL Database server endpoint.</span></span> 

```powershell
# Validate only when you do not use VNet nor AAD authentication
if([string]::IsNullOrEmpty($VnetId) -and [string]::IsNullOrEmpty($SubnetName))
{
    if(![string]::IsNullOrEmpty($SSISDBServerAdminUserName) -and ![string]::IsNullOrEmpty($SSISDBServerAdminPassword))
    {
        $SSISDBConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID=" + $SSISDBServerAdminUserName + ";Password=" + $SSISDBServerAdminPassword    
        $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $SSISDBConnectionString;
        Try
        {
            $sqlConnection.Open();
        }
        Catch [System.Data.SqlClient.SqlException]
        {
            Write-Warning "Cannot connect to your Azure SQL Database server, exception: $_";
            Write-Warning "Please make sure the server you specified has already been created. Do you want to proceed? [Y/N]"
            $yn = Read-Host
            if(!($yn -ieq "Y"))
            {
                Return;
            } 
        }
    }
}
```

### <a name="configure-virtual-network"></a><span data-ttu-id="6c5de-313">Configure virtual network</span><span class="sxs-lookup"><span data-stu-id="6c5de-313">Configure virtual network</span></span>
<span data-ttu-id="6c5de-314">Add the following script to automatically configure virtual network permissions/settings for your Azure-SSIS integration runtime to join.</span><span class="sxs-lookup"><span data-stu-id="6c5de-314">Add the following script to automatically configure virtual network permissions/settings for your Azure-SSIS integration runtime to join.</span></span>

```powershell
# Make sure to run this script against the subscription to which the virtual network belongs.
if(![string]::IsNullOrEmpty($VnetId) -and ![string]::IsNullOrEmpty($SubnetName))
{
    # Register to the Azure Batch resource provider
    $BatchApplicationId = "ddbf3205-c6bd-46ae-8127-60eb93363864"
    $BatchObjectId = (Get-AzureRmADServicePrincipal -ServicePrincipalName $BatchApplicationId).Id
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
    while(!(Get-AzureRmResourceProvider -ProviderNamespace "Microsoft.Batch").RegistrationState.Contains("Registered"))
    {
    Start-Sleep -s 10
    }
    if($VnetId -match "/providers/Microsoft.ClassicNetwork/")
    {
        # Assign the VM contributor role to Microsoft.Batch
        New-AzureRmRoleAssignment -ObjectId $BatchObjectId -RoleDefinitionName "Classic Virtual Machine Contributor" -Scope $VnetId
    }
}
```

### <a name="create-a-resource-group"></a><span data-ttu-id="6c5de-315">Create a resource group</span><span class="sxs-lookup"><span data-stu-id="6c5de-315">Create a resource group</span></span>
<span data-ttu-id="6c5de-316">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span><span class="sxs-lookup"><span data-stu-id="6c5de-316">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) command.</span></span> <span data-ttu-id="6c5de-317">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span><span class="sxs-lookup"><span data-stu-id="6c5de-317">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> 

```powershell
New-AzureRmResourceGroup -Location $DataFactoryLocation -Name $ResourceGroupName
```

### <a name="create-a-data-factory"></a><span data-ttu-id="6c5de-318">Create a data factory</span><span class="sxs-lookup"><span data-stu-id="6c5de-318">Create a data factory</span></span>
<span data-ttu-id="6c5de-319">Run the following command to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="6c5de-319">Run the following command to create a data factory.</span></span>

```powershell
Set-AzureRmDataFactoryV2 -ResourceGroupName $ResourceGroupName `
                         -Location $DataFactoryLocation `
                         -Name $DataFactoryName
```

### <a name="create-an-integration-runtime"></a><span data-ttu-id="6c5de-320">Create an integration runtime</span><span class="sxs-lookup"><span data-stu-id="6c5de-320">Create an integration runtime</span></span>
<span data-ttu-id="6c5de-321">Run the following commands to create an Azure-SSIS integration runtime that runs SSIS packages in Azure.</span><span class="sxs-lookup"><span data-stu-id="6c5de-321">Run the following commands to create an Azure-SSIS integration runtime that runs SSIS packages in Azure.</span></span> 

<span data-ttu-id="6c5de-322">If you do not use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) to host SSISDB nor require access to on-premises data, you can omit VNetId and Subnet parameters or pass empty values for them.</span><span class="sxs-lookup"><span data-stu-id="6c5de-322">If you do not use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview) to host SSISDB nor require access to on-premises data, you can omit VNetId and Subnet parameters or pass empty values for them.</span></span> <span data-ttu-id="6c5de-323">Otherwise, you cannot omit them and must pass valid values from your virtual network configuration, see [Join Azure-SSIS IR to a virtual network](https://docs.microsoft.com/en-us/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="6c5de-323">Otherwise, you cannot omit them and must pass valid values from your virtual network configuration, see [Join Azure-SSIS IR to a virtual network](https://docs.microsoft.com/en-us/azure/data-factory/join-azure-ssis-integration-runtime-virtual-network).</span></span> 

<span data-ttu-id="6c5de-324">If you use Managed Instance (Preview) to host SSISDB, you can omit CatalogPricingTier parameter or pass an empty value for it.</span><span class="sxs-lookup"><span data-stu-id="6c5de-324">If you use Managed Instance (Preview) to host SSISDB, you can omit CatalogPricingTier parameter or pass an empty value for it.</span></span> <span data-ttu-id="6c5de-325">Otherwise, you cannot omit it and must pass a valid value from the list of supported pricing tiers for Azure SQL Database, see [SQL Database resource limits](../sql-database/sql-database-resource-limits.md).</span><span class="sxs-lookup"><span data-stu-id="6c5de-325">Otherwise, you cannot omit it and must pass a valid value from the list of supported pricing tiers for Azure SQL Database, see [SQL Database resource limits](../sql-database/sql-database-resource-limits.md).</span></span> 

<span data-ttu-id="6c5de-326">If you use Azure Active Directory (AAD) authentication with your Azure Data Factory Managed Service Identity (MSI) to connect to the database server, you can omit CatalogAdminCredential parameter, but you must add your Data Factory MSI into an AAD group with access permissions to the database server, see [Enable AAD authentication for Azure-SSIS IR](https://docs.microsoft.com/en-us/azure/data-factory/enable-aad-authentication-azure-ssis-ir).</span><span class="sxs-lookup"><span data-stu-id="6c5de-326">If you use Azure Active Directory (AAD) authentication with your Azure Data Factory Managed Service Identity (MSI) to connect to the database server, you can omit CatalogAdminCredential parameter, but you must add your Data Factory MSI into an AAD group with access permissions to the database server, see [Enable AAD authentication for Azure-SSIS IR](https://docs.microsoft.com/en-us/azure/data-factory/enable-aad-authentication-azure-ssis-ir).</span></span> <span data-ttu-id="6c5de-327">Otherwise, you cannot omit it and must pass a valid object formed from your server admin username and password for SQL authentication.</span><span class="sxs-lookup"><span data-stu-id="6c5de-327">Otherwise, you cannot omit it and must pass a valid object formed from your server admin username and password for SQL authentication.</span></span>

```powershell               
Set-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                           -DataFactoryName $DataFactoryName `
                                           -Type Managed `
                                           -Name $AzureSSISName `
                                           -Description $AzureSSISDescription `
                                           -Location $AzureSSISLocation `
                                           -NodeSize $AzureSSISNodeSize `
                                           -NodeCount $AzureSSISNodeNumber `
                                           -Edition $AzureSSISEdition `
                                           -LicenseType $AzureSSISLicenseType `
                                           -MaxParallelExecutionsPerNode $AzureSSISMaxParallelExecutionsPerNode `
                                           -SetupScriptContainerSasUri $SetupScriptContainerSasUri `
                                           -VnetId $VnetId `
                                           -Subnet $SubnetName `
                                           -CatalogServerEndpoint $SSISDBServerEndpoint `
                                           -CatalogPricingTier $SSISDBPricingTier

if(![string]::IsNullOrEmpty($SSISDBServerAdminUserName) –and ![string]::IsNullOrEmpty($SSISDBServerAdminPassword))
{
    $secpasswd = ConvertTo-SecureString $SSISDBServerAdminPassword -AsPlainText -Force
    $serverCreds = New-Object System.Management.Automation.PSCredential($SSISDBServerAdminUserName, $secpasswd)

    Set-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                               -DataFactoryName $DataFactoryName `
                                               -Name $AzureSSISName `
                                               -CatalogAdminCredential $serverCreds
}
```

### <a name="start-integration-runtime"></a><span data-ttu-id="6c5de-328">Start integration runtime</span><span class="sxs-lookup"><span data-stu-id="6c5de-328">Start integration runtime</span></span>
<span data-ttu-id="6c5de-329">Run the following command to start the Azure-SSIS integration runtime:</span><span class="sxs-lookup"><span data-stu-id="6c5de-329">Run the following command to start the Azure-SSIS integration runtime:</span></span> 

```powershell
write-host("##### Starting #####")
Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                             -DataFactoryName $DataFactoryName `
                                             -Name $AzureSSISName `
                                             -Force

write-host("##### Completed #####")
write-host("If any cmdlet is unsuccessful, please consider using -Debug option for diagnostics.")                                  
```

<span data-ttu-id="6c5de-330">This command takes from **20 to 30 minutes** to complete.</span><span class="sxs-lookup"><span data-stu-id="6c5de-330">This command takes from **20 to 30 minutes** to complete.</span></span> 

### <a name="full-script"></a><span data-ttu-id="6c5de-331">Full script</span><span class="sxs-lookup"><span data-stu-id="6c5de-331">Full script</span></span>
<span data-ttu-id="6c5de-332">Here is the full script that creates an Azure-SSIS integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-332">Here is the full script that creates an Azure-SSIS integration runtime.</span></span> 

```powershell
### Azure Data Factory information 
# If your input contains a PSH special character, e.g. "$", precede it with the escape character "`" like "`$".
$SubscriptionName = "[your Azure subscription name]"
$ResourceGroupName = "[your Azure resource group name]"
$DataFactoryName = "[your data factory name]"
$DataFactoryLocation = "EastUS" 

### Azure-SSIS integration runtime information - This is the Data Factory compute resource for running SSIS packages
$AzureSSISName = "[specify a name for your Azure-SSIS IR]"
$AzureSSISDescription = "[specify a description for your Azure-SSIS IR]"
$AzureSSISLocation = "EastUS" 
# Only Standard_A4_v2|Standard_A8_v2|Standard_D1_v2|Standard_D2_v2|Standard_D3_v2|Standard_D4_v2 are supported.
$AzureSSISNodeSize = "Standard_D4_v2"
# Only 1-10 nodes are supported.
$AzureSSISNodeNumber = 2 
# Azure-SSIS IR edition/license info: Standard or Enterprise 
$AzureSSISEdition = "" # Standard by default, while Enterprise lets you use advanced/premium features on your Azure-SSIS IR
# Azure-SSIS IR hybrid usage info: LicenseIncluded or BasePrice
$AzureSSISLicenseType = "" # LicenseIncluded by default, while BasePrice lets you bring your own on-premises SQL Server license with Software Assurance to earn cost savings from Azure Hybrid Benefit (AHB) option
# For a Standard_D1_v2 node, 1-4 parallel executions per node are supported. For other nodes, it's 1-8.
$AzureSSISMaxParallelExecutionsPerNode = 8 
# Custom setup info
$SetupScriptContainerSasUri = "" # OPTIONAL to provide SAS URI of blob container where your custom setup script and its associated files are stored
# Virtual network info: Classic or Azure Resource Manager
$VnetId = "[your virtual network resource ID or leave it empty]" # REQUIRED if you use Azure SQL Database with virtual network service endpoints/Managed Instance (Preview)/on-premises data, Azure Resource Manager virtual network is recommended, Classic virtual network will be deprecated soon    
$SubnetName = "[your subnet name or leave it empty]" # WARNING: Please use a different subnet than the one used for your Managed Instance (Preview)

### SSISDB info
$SSISDBServerEndpoint = "[your Azure SQL Database server name or Managed Instance (Preview) name.DNS prefix].database.windows.net" # WARNING: Please ensure that there is no existing SSISDB, so we can prepare and manage one on your behalf
# Authentication info: SQL or Azure Active Directory (AAD)
$SSISDBServerAdminUserName = "[your server admin username for SQL authentication or leave it empty for AAD authentication]"
$SSISDBServerAdminPassword = "[your server admin password for SQL authentication or leave it empty for AAD authentication]"
$SSISDBPricingTier = "[Basic|S0|S1|S2|S3|S4|S6|S7|S9|S12|P1|P2|P4|P6|P11|P15|…|ELASTIC_POOL(name = <elastic_pool_name>) for Azure SQL Database or leave it empty for Managed Instance (Preview)]"

### Log in and select subscription
Connect-AzureRmAccount
Select-AzureRmSubscription -SubscriptionName $SubscriptionName

### Validate the connection to database
# Validate only when you do not use VNet nor AAD authentication
if([string]::IsNullOrEmpty($VnetId) -and [string]::IsNullOrEmpty($SubnetName))
{
    if(![string]::IsNullOrEmpty($SSISDBServerAdminUserName) -and ![string]::IsNullOrEmpty($SSISDBServerAdminPassword))
    {
        $SSISDBConnectionString = "Data Source=" + $SSISDBServerEndpoint + ";User ID=" + $SSISDBServerAdminUserName + ";Password=" + $SSISDBServerAdminPassword    
        $sqlConnection = New-Object System.Data.SqlClient.SqlConnection $SSISDBConnectionString;
        Try
        {
            $sqlConnection.Open();
        }
        Catch [System.Data.SqlClient.SqlException]
        {
            Write-Warning "Cannot connect to your Azure SQL Database server, exception: $_";
            Write-Warning "Please make sure the server you specified has already been created. Do you want to proceed? [Y/N]"
            $yn = Read-Host
            if(!($yn -ieq "Y"))
            {
                Return;
            } 
        }
    }
}

### Configure virtual network
# Make sure to run this script against the subscription to which the virtual network belongs.
if(![string]::IsNullOrEmpty($VnetId) -and ![string]::IsNullOrEmpty($SubnetName))
{
    # Register to the Azure Batch resource provider
    $BatchApplicationId = "ddbf3205-c6bd-46ae-8127-60eb93363864"
    $BatchObjectId = (Get-AzureRmADServicePrincipal -ServicePrincipalName $BatchApplicationId).Id
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Batch
    while(!(Get-AzureRmResourceProvider -ProviderNamespace "Microsoft.Batch").RegistrationState.Contains("Registered"))
    {
    Start-Sleep -s 10
    }
    if($VnetId -match "/providers/Microsoft.ClassicNetwork/")
    {
        # Assign the VM contributor role to Microsoft.Batch
        New-AzureRmRoleAssignment -ObjectId $BatchObjectId -RoleDefinitionName "Classic Virtual Machine Contributor" -Scope $VnetId
    }
}

### Create a data factory
Set-AzureRmDataFactoryV2 -ResourceGroupName $ResourceGroupName `
                         -Location $DataFactoryLocation `
                         -Name $DataFactoryName

### Create an integration runtime
Set-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                           -DataFactoryName $DataFactoryName `
                                           -Type Managed `
                                           -Name $AzureSSISName `
                                           -Description $AzureSSISDescription `
                                           -Location $AzureSSISLocation `
                                           -NodeSize $AzureSSISNodeSize `
                                           -NodeCount $AzureSSISNodeNumber `
                                           -Edition $AzureSSISEdition `
                                           -LicenseType $AzureSSISLicenseType `
                                           -MaxParallelExecutionsPerNode $AzureSSISMaxParallelExecutionsPerNode `
                                           -SetupScriptContainerSasUri $SetupScriptContainerSasUri `
                                           -VnetId $VnetId `
                                           -Subnet $SubnetName `
                                           -CatalogServerEndpoint $SSISDBServerEndpoint `
                                           -CatalogPricingTier $SSISDBPricingTier

if(![string]::IsNullOrEmpty($SSISDBServerAdminUserName) –and ![string]::IsNullOrEmpty($SSISDBServerAdminPassword))
{
    $secpasswd = ConvertTo-SecureString $SSISDBServerAdminPassword -AsPlainText -Force
    $serverCreds = New-Object System.Management.Automation.PSCredential($SSISDBServerAdminUserName, $secpasswd)

    Set-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                               -DataFactoryName $DataFactoryName `
                                               -Name $AzureSSISName `
                                               -CatalogAdminCredential $serverCreds
}

### Start integration runtime   
write-host("##### Starting your Azure-SSIS integration runtime. This command takes 20 to 30 minutes to complete. #####")
Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName $ResourceGroupName `
                                             -DataFactoryName $DataFactoryName `
                                             -Name $AzureSSISName `
                                             -Force

write-host("##### Completed #####")
write-host("If any cmdlet is unsuccessful, please consider using -Debug option for diagnostics.")
```

## <a name="azure-resource-manager-template"></a><span data-ttu-id="6c5de-333">Azure Resource Manager template</span><span class="sxs-lookup"><span data-stu-id="6c5de-333">Azure Resource Manager template</span></span>
<span data-ttu-id="6c5de-334">In this section, you use the Azure Resource Manager template to create Azure-SSIS integration runtime.</span><span class="sxs-lookup"><span data-stu-id="6c5de-334">In this section, you use the Azure Resource Manager template to create Azure-SSIS integration runtime.</span></span> <span data-ttu-id="6c5de-335">Here is a sample walkthrough:</span><span class="sxs-lookup"><span data-stu-id="6c5de-335">Here is a sample walkthrough:</span></span> 

1. <span data-ttu-id="6c5de-336">Create a JSON file with the following Azure Resource Manager template.</span><span class="sxs-lookup"><span data-stu-id="6c5de-336">Create a JSON file with the following Azure Resource Manager template.</span></span> <span data-ttu-id="6c5de-337">Replace values in the angled brackets (place holders) with your own values.</span><span class="sxs-lookup"><span data-stu-id="6c5de-337">Replace values in the angled brackets (place holders) with your own values.</span></span> 

    ```json
    {
        "contentVersion": "1.0.0.0",
        "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
        "parameters": {},
        "variables": {},
        "resources": [{
            "name": "<Specify a name for your data factory>",
            "apiVersion": "2017-09-01-preview",
            "type": "Microsoft.DataFactory/factories",
            "location": "East US",
            "properties": {},
            "resources": [{
                "type": "integrationruntimes",
                "name": "<Specify a name for your Azure-SSIS IR>",
                "dependsOn": [ "<The name of the data factory you specified at the beginning>" ],
                "apiVersion": "2017-09-01-preview",
                "properties": {
                    "type": "Managed",
                    "typeProperties": {
                        "computeProperties": {
                            "location": "East US",
                            "nodeSize": "Standard_D4_v2",
                            "numberOfNodes": 1,
                            "maxParallelExecutionsPerNode": 8
                        },
                        "ssisProperties": {
                            "catalogInfo": {
                                "catalogServerEndpoint": "<Azure SQL Database server name>.database.windows.net",
                                "catalogAdminUserName": "<Azure SQL Database server admin username>",
                                "catalogAdminPassword": {
                                    "type": "SecureString",
                                    "value": "<Azure SQL Database server admin password>"
                                },
                                "catalogPricingTier": "Basic"
                            }
                        }
                    }
                }
            }]
        }]
    }
    ```
    
1. <span data-ttu-id="6c5de-338">To deploy the Azure Resource Manager template, run New-AzureRmResourceGroupDeployment command as shown in the following example, where ADFTutorialResourceGroup is the name of your resource group and ADFTutorialARM.json is the file that contains JSON definition for your data factory and Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="6c5de-338">To deploy the Azure Resource Manager template, run New-AzureRmResourceGroupDeployment command as shown in the following example, where ADFTutorialResourceGroup is the name of your resource group and ADFTutorialARM.json is the file that contains JSON definition for your data factory and Azure-SSIS IR.</span></span> 

    ```powershell
    New-AzureRmResourceGroupDeployment -Name MyARMDeployment -ResourceGroupName ADFTutorialResourceGroup -TemplateFile ADFTutorialARM.json
    ```

    <span data-ttu-id="6c5de-339">This command creates your data factory and Azure-SSIS IR in it, but it does not start the IR.</span><span class="sxs-lookup"><span data-stu-id="6c5de-339">This command creates your data factory and Azure-SSIS IR in it, but it does not start the IR.</span></span> 

1. <span data-ttu-id="6c5de-340">To start your Azure-SSIS IR, run Start-AzureRmDataFactoryV2IntegrationRuntime command:</span><span class="sxs-lookup"><span data-stu-id="6c5de-340">To start your Azure-SSIS IR, run Start-AzureRmDataFactoryV2IntegrationRuntime command:</span></span> 

    ```powershell
    Start-AzureRmDataFactoryV2IntegrationRuntime -ResourceGroupName "<Resource Group Name>" `
                                                 -DataFactoryName "<Data Factory Name>" `
                                                 -Name "<Azure SSIS IR Name>" `
                                                 -Force
    ``` 

## <a name="deploy-ssis-packages"></a><span data-ttu-id="6c5de-341">Deploy SSIS packages</span><span class="sxs-lookup"><span data-stu-id="6c5de-341">Deploy SSIS packages</span></span>
<span data-ttu-id="6c5de-342">Now, use SQL Server Data Tools (SSDT) or SQL Server Management Studio (SSMS) to deploy your SSIS packages to Azure.</span><span class="sxs-lookup"><span data-stu-id="6c5de-342">Now, use SQL Server Data Tools (SSDT) or SQL Server Management Studio (SSMS) to deploy your SSIS packages to Azure.</span></span> <span data-ttu-id="6c5de-343">Connect to your database server that hosts the SSIS catalog (SSISDB).</span><span class="sxs-lookup"><span data-stu-id="6c5de-343">Connect to your database server that hosts the SSIS catalog (SSISDB).</span></span> <span data-ttu-id="6c5de-344">The name of database server is in the format: &lt;Azure SQL Database server name&gt;.database.windows.net or &lt;Managed Instance (Preview) name.DNS prefix&gt;.database.windows.net.</span><span class="sxs-lookup"><span data-stu-id="6c5de-344">The name of database server is in the format: &lt;Azure SQL Database server name&gt;.database.windows.net or &lt;Managed Instance (Preview) name.DNS prefix&gt;.database.windows.net.</span></span> <span data-ttu-id="6c5de-345">See [Deploy packages](/sql/integration-services/packages/deploy-integration-services-ssis-projects-and-packages#deploy-packages-to-integration-services-server) article for instructions.</span><span class="sxs-lookup"><span data-stu-id="6c5de-345">See [Deploy packages](/sql/integration-services/packages/deploy-integration-services-ssis-projects-and-packages#deploy-packages-to-integration-services-server) article for instructions.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="6c5de-346">Next steps</span><span class="sxs-lookup"><span data-stu-id="6c5de-346">Next steps</span></span>
<span data-ttu-id="6c5de-347">See the other Azure-SSIS IR topics in this documentation:</span><span class="sxs-lookup"><span data-stu-id="6c5de-347">See the other Azure-SSIS IR topics in this documentation:</span></span> 

- <span data-ttu-id="6c5de-348">[Azure-SSIS Integration Runtime](concepts-integration-runtime.md#azure-ssis-integration-runtime).</span><span class="sxs-lookup"><span data-stu-id="6c5de-348">[Azure-SSIS Integration Runtime](concepts-integration-runtime.md#azure-ssis-integration-runtime).</span></span> <span data-ttu-id="6c5de-349">This article provides conceptual information about integration runtimes in general including the Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="6c5de-349">This article provides conceptual information about integration runtimes in general including the Azure-SSIS IR.</span></span> 
- <span data-ttu-id="6c5de-350">[Tutorial: deploy SSIS packages to Azure](tutorial-create-azure-ssis-runtime-portal.md).</span><span class="sxs-lookup"><span data-stu-id="6c5de-350">[Tutorial: deploy SSIS packages to Azure](tutorial-create-azure-ssis-runtime-portal.md).</span></span> <span data-ttu-id="6c5de-351">This article provides step-by-step instructions to create an Azure-SSIS IR and uses an Azure SQL database to host the SSIS catalog.</span><span class="sxs-lookup"><span data-stu-id="6c5de-351">This article provides step-by-step instructions to create an Azure-SSIS IR and uses an Azure SQL database to host the SSIS catalog.</span></span> 
- <span data-ttu-id="6c5de-352">[Monitor an Azure-SSIS IR](monitor-integration-runtime.md#azure-ssis-integration-runtime).</span><span class="sxs-lookup"><span data-stu-id="6c5de-352">[Monitor an Azure-SSIS IR](monitor-integration-runtime.md#azure-ssis-integration-runtime).</span></span> <span data-ttu-id="6c5de-353">This article shows you how to retrieve information about an Azure-SSIS IR and descriptions of statuses in the returned information.</span><span class="sxs-lookup"><span data-stu-id="6c5de-353">This article shows you how to retrieve information about an Azure-SSIS IR and descriptions of statuses in the returned information.</span></span> 
- <span data-ttu-id="6c5de-354">[Manage an Azure-SSIS IR](manage-azure-ssis-integration-runtime.md).</span><span class="sxs-lookup"><span data-stu-id="6c5de-354">[Manage an Azure-SSIS IR](manage-azure-ssis-integration-runtime.md).</span></span> <span data-ttu-id="6c5de-355">This article shows you how to stop, start, or remove an Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="6c5de-355">This article shows you how to stop, start, or remove an Azure-SSIS IR.</span></span> <span data-ttu-id="6c5de-356">It also shows you how to scale out your Azure-SSIS IR by adding more nodes to the IR.</span><span class="sxs-lookup"><span data-stu-id="6c5de-356">It also shows you how to scale out your Azure-SSIS IR by adding more nodes to the IR.</span></span> 
- <span data-ttu-id="6c5de-357">[Join an Azure-SSIS IR to a virtual network](join-azure-ssis-integration-runtime-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="6c5de-357">[Join an Azure-SSIS IR to a virtual network](join-azure-ssis-integration-runtime-virtual-network.md).</span></span> <span data-ttu-id="6c5de-358">This article provides conceptual information about joining your Azure-SSIS IR to an Azure virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-358">This article provides conceptual information about joining your Azure-SSIS IR to an Azure virtual network.</span></span> <span data-ttu-id="6c5de-359">It also provides steps to use Azure portal to configure virtual network so that Azure-SSIS IR can join the virtual network.</span><span class="sxs-lookup"><span data-stu-id="6c5de-359">It also provides steps to use Azure portal to configure virtual network so that Azure-SSIS IR can join the virtual network.</span></span> 
