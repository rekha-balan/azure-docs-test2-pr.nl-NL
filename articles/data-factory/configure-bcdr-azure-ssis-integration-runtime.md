---
title: Configure Azure-SSIS Integration Runtime for SQL Database failover | Microsoft Docs
description: This article describes how to configure the Azure-SSIS Integration Runtime with Azure SQL Database geo-replication and failover for the SSISDB database
services: data-factory
documentationcenter: ''
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: ''
ms.devlang: powershell
ms.topic: conceptual
ms.date: 08/14/2018
author: swinarko
ms.author: sawinark
ms.reviewer: douglasl
manager: craigg
ms.openlocfilehash: 2012ccf4d9fd3e62ba248f29f922f868077e4061
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869644"
---
# <a name="configure-the-azure-ssis-integration-runtime-with-azure-sql-database-geo-replication-and-failover"></a><span data-ttu-id="e0953-103">Configure the Azure-SSIS Integration Runtime with Azure SQL Database geo-replication and failover</span><span class="sxs-lookup"><span data-stu-id="e0953-103">Configure the Azure-SSIS Integration Runtime with Azure SQL Database geo-replication and failover</span></span>

<span data-ttu-id="e0953-104">This article describes how to configure the Azure-SSIS Integration Runtime with Azure SQL Database geo-replication for the SSISDB database.</span><span class="sxs-lookup"><span data-stu-id="e0953-104">This article describes how to configure the Azure-SSIS Integration Runtime with Azure SQL Database geo-replication for the SSISDB database.</span></span> <span data-ttu-id="e0953-105">When a failover occurs, you can ensure that the Azure-SSIS IR keeps working with the secondary database.</span><span class="sxs-lookup"><span data-stu-id="e0953-105">When a failover occurs, you can ensure that the Azure-SSIS IR keeps working with the secondary database.</span></span>

<span data-ttu-id="e0953-106">For more info about geo-replication and failover for SQL Database, see [Overview: Active geo-replication and auto-failover groups](../sql-database/sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0953-106">For more info about geo-replication and failover for SQL Database, see [Overview: Active geo-replication and auto-failover groups](../sql-database/sql-database-geo-replication-overview.md).</span></span>

## <a name="scenario-1---azure-ssis-ir-is-pointing-to-read-write-listener-endpoint"></a><span data-ttu-id="e0953-107">Scenario 1 - Azure-SSIS IR is pointing to read-write listener endpoint</span><span class="sxs-lookup"><span data-stu-id="e0953-107">Scenario 1 - Azure-SSIS IR is pointing to read-write listener endpoint</span></span>

### <a name="conditions"></a><span data-ttu-id="e0953-108">Conditions</span><span class="sxs-lookup"><span data-stu-id="e0953-108">Conditions</span></span>

<span data-ttu-id="e0953-109">This section applies when the following conditions are true:</span><span class="sxs-lookup"><span data-stu-id="e0953-109">This section applies when the following conditions are true:</span></span>

- <span data-ttu-id="e0953-110">The Azure-SSIS IR is pointing to the read-write listener endpoint of the failover group.</span><span class="sxs-lookup"><span data-stu-id="e0953-110">The Azure-SSIS IR is pointing to the read-write listener endpoint of the failover group.</span></span>

  <span data-ttu-id="e0953-111">AND</span><span class="sxs-lookup"><span data-stu-id="e0953-111">AND</span></span>

- <span data-ttu-id="e0953-112">The SQL Database server is *not* configured with the virtual network service endpoint rule.</span><span class="sxs-lookup"><span data-stu-id="e0953-112">The SQL Database server is *not* configured with the virtual network service endpoint rule.</span></span>

### <a name="solution"></a><span data-ttu-id="e0953-113">Solution</span><span class="sxs-lookup"><span data-stu-id="e0953-113">Solution</span></span>

<span data-ttu-id="e0953-114">When failover occurs, it is transparent to the Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="e0953-114">When failover occurs, it is transparent to the Azure-SSIS IR.</span></span> <span data-ttu-id="e0953-115">The Azure-SSIS IR automatically connects to the new primary of the failover group.</span><span class="sxs-lookup"><span data-stu-id="e0953-115">The Azure-SSIS IR automatically connects to the new primary of the failover group.</span></span>

## <a name="scenario-2---azure-ssis-ir-is-pointing-to-primary-server-endpoint"></a><span data-ttu-id="e0953-116">Scenario 2 - Azure-SSIS IR is pointing to primary server endpoint</span><span class="sxs-lookup"><span data-stu-id="e0953-116">Scenario 2 - Azure-SSIS IR is pointing to primary server endpoint</span></span>

### <a name="conditions"></a><span data-ttu-id="e0953-117">Conditions</span><span class="sxs-lookup"><span data-stu-id="e0953-117">Conditions</span></span>

<span data-ttu-id="e0953-118">This section applies when one of the following conditions is true:</span><span class="sxs-lookup"><span data-stu-id="e0953-118">This section applies when one of the following conditions is true:</span></span>

- <span data-ttu-id="e0953-119">The Azure-SSIS IR is pointing to the primary server endpoint of the failover group.</span><span class="sxs-lookup"><span data-stu-id="e0953-119">The Azure-SSIS IR is pointing to the primary server endpoint of the failover group.</span></span> <span data-ttu-id="e0953-120">This endpoint changes when failover occurs.</span><span class="sxs-lookup"><span data-stu-id="e0953-120">This endpoint changes when failover occurs.</span></span>

  <span data-ttu-id="e0953-121">OR</span><span class="sxs-lookup"><span data-stu-id="e0953-121">OR</span></span>

- <span data-ttu-id="e0953-122">The Azure SQL Database server is configured with the virtual network service endpoint rule.</span><span class="sxs-lookup"><span data-stu-id="e0953-122">The Azure SQL Database server is configured with the virtual network service endpoint rule.</span></span>

  <span data-ttu-id="e0953-123">OR</span><span class="sxs-lookup"><span data-stu-id="e0953-123">OR</span></span>

- <span data-ttu-id="e0953-124">The database server is a SQL Database Managed Instance configured with a virtual network.</span><span class="sxs-lookup"><span data-stu-id="e0953-124">The database server is a SQL Database Managed Instance configured with a virtual network.</span></span>

### <a name="solution"></a><span data-ttu-id="e0953-125">Solution</span><span class="sxs-lookup"><span data-stu-id="e0953-125">Solution</span></span>

<span data-ttu-id="e0953-126">When failover occurs, you have to do the following things:</span><span class="sxs-lookup"><span data-stu-id="e0953-126">When failover occurs, you have to do the following things:</span></span>

1. <span data-ttu-id="e0953-127">Stop the Azure-SSIS IR.</span><span class="sxs-lookup"><span data-stu-id="e0953-127">Stop the Azure-SSIS IR.</span></span>

2. <span data-ttu-id="e0953-128">Reconfigure the IR to point to the new primary endpoint and to a virtual network in the new region.</span><span class="sxs-lookup"><span data-stu-id="e0953-128">Reconfigure the IR to point to the new primary endpoint and to a virtual network in the new region.</span></span>

3. <span data-ttu-id="e0953-129">Restart the IR.</span><span class="sxs-lookup"><span data-stu-id="e0953-129">Restart the IR.</span></span>

<span data-ttu-id="e0953-130">The following sections describe these steps in more detail.</span><span class="sxs-lookup"><span data-stu-id="e0953-130">The following sections describe these steps in more detail.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="e0953-131">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="e0953-131">Prerequisites</span></span>

- <span data-ttu-id="e0953-132">Make sure that you have enabled disaster recovery for your Azure SQL Database server in case the server has an outage at the same time.</span><span class="sxs-lookup"><span data-stu-id="e0953-132">Make sure that you have enabled disaster recovery for your Azure SQL Database server in case the server has an outage at the same time.</span></span> <span data-ttu-id="e0953-133">For more info, see [Overview of business continuity with Azure SQL Database](../sql-database/sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="e0953-133">For more info, see [Overview of business continuity with Azure SQL Database](../sql-database/sql-database-business-continuity.md).</span></span>

- <span data-ttu-id="e0953-134">If you are using a virtual network in the current region, you need to use another virtual network in the new region to connect your Azure-SSIS integration runtime.</span><span class="sxs-lookup"><span data-stu-id="e0953-134">If you are using a virtual network in the current region, you need to use another virtual network in the new region to connect your Azure-SSIS integration runtime.</span></span> <span data-ttu-id="e0953-135">For more info, see [Join an Azure-SSIS integration runtime to a virtual network](join-azure-ssis-integration-runtime-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="e0953-135">For more info, see [Join an Azure-SSIS integration runtime to a virtual network](join-azure-ssis-integration-runtime-virtual-network.md).</span></span>

- <span data-ttu-id="e0953-136">If you are using a custom setup, you may need to prepare another SAS URI for the blob container that stores your custom setup script and associated files, so it continues to be accessible during an outage.</span><span class="sxs-lookup"><span data-stu-id="e0953-136">If you are using a custom setup, you may need to prepare another SAS URI for the blob container that stores your custom setup script and associated files, so it continues to be accessible during an outage.</span></span> <span data-ttu-id="e0953-137">For more info, see [Configure a custom setup on an Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md).</span><span class="sxs-lookup"><span data-stu-id="e0953-137">For more info, see [Configure a custom setup on an Azure-SSIS integration runtime](how-to-configure-azure-ssis-ir-custom-setup.md).</span></span>

### <a name="steps"></a><span data-ttu-id="e0953-138">Steps</span><span class="sxs-lookup"><span data-stu-id="e0953-138">Steps</span></span>

<span data-ttu-id="e0953-139">Follow these steps to stop your Azure-SSIS IR, switch the IR to a new region, and start it again.</span><span class="sxs-lookup"><span data-stu-id="e0953-139">Follow these steps to stop your Azure-SSIS IR, switch the IR to a new region, and start it again.</span></span>

1. <span data-ttu-id="e0953-140">Stop the IR in the original region.</span><span class="sxs-lookup"><span data-stu-id="e0953-140">Stop the IR in the original region.</span></span>

2. <span data-ttu-id="e0953-141">Call the following command in PowerShell to update the IR with the new settings.</span><span class="sxs-lookup"><span data-stu-id="e0953-141">Call the following command in PowerShell to update the IR with the new settings.</span></span>

    ```powershell
    Set-AzureRmDataFactoryV2IntegrationRuntime -Location "new region" `
                    -CatalogServerEndpoint "Azure SQL Database server endpoint" `
                    -CatalogAdminCredential "Azure SQL Database server admin credentials" `
                    -VNetId "new VNet" `
                    -Subnet "new subnet" `
                    -SetupScriptContainerSasUri "new custom setup SAS URI"
    ```

    <span data-ttu-id="e0953-142">For more info about this PowerShell command, see [Create the Azure-SSIS integration runtime in Azure Data Factory](create-azure-ssis-integration-runtime.md)</span><span class="sxs-lookup"><span data-stu-id="e0953-142">For more info about this PowerShell command, see [Create the Azure-SSIS integration runtime in Azure Data Factory](create-azure-ssis-integration-runtime.md)</span></span>

3. <span data-ttu-id="e0953-143">Start the IR again.</span><span class="sxs-lookup"><span data-stu-id="e0953-143">Start the IR again.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0953-144">Next steps</span><span class="sxs-lookup"><span data-stu-id="e0953-144">Next steps</span></span>

<span data-ttu-id="e0953-145">Consider these other configuration options for the Azure-SSIS IR:</span><span class="sxs-lookup"><span data-stu-id="e0953-145">Consider these other configuration options for the Azure-SSIS IR:</span></span>

- [<span data-ttu-id="e0953-146">Configure the Azure-SSIS Integration Runtime for high performance</span><span class="sxs-lookup"><span data-stu-id="e0953-146">Configure the Azure-SSIS Integration Runtime for high performance</span></span>](configure-azure-ssis-integration-runtime-performance.md)

- [<span data-ttu-id="e0953-147">Customize setup for the Azure-SSIS integration runtime</span><span class="sxs-lookup"><span data-stu-id="e0953-147">Customize setup for the Azure-SSIS integration runtime</span></span>](how-to-configure-azure-ssis-ir-custom-setup.md)

- [<span data-ttu-id="e0953-148">Provision Enterprise Edition for the Azure-SSIS Integration Runtime</span><span class="sxs-lookup"><span data-stu-id="e0953-148">Provision Enterprise Edition for the Azure-SSIS Integration Runtime</span></span>](how-to-configure-azure-ssis-ir-enterprise-edition.md)
