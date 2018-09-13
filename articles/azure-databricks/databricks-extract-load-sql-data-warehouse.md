---
title: 'Tutorial: Perform ETL operations using Azure Databricks'
description: Learn how to extract data from Data Lake Store into Azure Databricks, transform the data, and then load the data into Azure SQL Data Warehouse.
services: azure-databricks
author: nitinme
ms.author: nitinme
manager: cgronlun
editor: cgronlun
ms.service: azure-databricks
ms.custom: mvc
ms.topic: tutorial
ms.workload: Active
ms.date: 07/26/2018
ms.openlocfilehash: 11046089bd25e1ca9e117d5d8908471858450e6d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865180"
---
# <a name="tutorial-extract-transform-and-load-data-using-azure-databricks"></a><span data-ttu-id="cc0e2-103">Tutorial: Extract, transform, and load data using Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="cc0e2-103">Tutorial: Extract, transform, and load data using Azure Databricks</span></span>

<span data-ttu-id="cc0e2-104">In this tutorial, you perform an ETL (extract, transform, and load data) operation using Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-104">In this tutorial, you perform an ETL (extract, transform, and load data) operation using Azure Databricks.</span></span> <span data-ttu-id="cc0e2-105">You extract data from Azure Data Lake Store into Azure Databricks, run transformations on the data in Azure Databricks, and then load the transformed data into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-105">You extract data from Azure Data Lake Store into Azure Databricks, run transformations on the data in Azure Databricks, and then load the transformed data into Azure SQL Data Warehouse.</span></span> 

<span data-ttu-id="cc0e2-106">The steps in this tutorial use the SQL Data Warehouse connector for Azure Databricks to transfer data to Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-106">The steps in this tutorial use the SQL Data Warehouse connector for Azure Databricks to transfer data to Azure Databricks.</span></span> <span data-ttu-id="cc0e2-107">This connector, in turn, uses Azure Blob Storage as temporary storage for the data being transferred between an Azure Databricks cluster and Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-107">This connector, in turn, uses Azure Blob Storage as temporary storage for the data being transferred between an Azure Databricks cluster and Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="cc0e2-108">The following illustration shows the application flow:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-108">The following illustration shows the application flow:</span></span>

<span data-ttu-id="cc0e2-109">![Azure Databricks with Data Lake Store and SQL Data Warehouse](./media/databricks-extract-load-sql-data-warehouse/databricks-extract-transform-load-sql-datawarehouse.png "Azure Databricks with Data Lake Store and SQL Data Warehouse")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-109">![Azure Databricks with Data Lake Store and SQL Data Warehouse](./media/databricks-extract-load-sql-data-warehouse/databricks-extract-transform-load-sql-datawarehouse.png "Azure Databricks with Data Lake Store and SQL Data Warehouse")</span></span>

<span data-ttu-id="cc0e2-110">This tutorial covers the following tasks:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-110">This tutorial covers the following tasks:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="cc0e2-111">Create an Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="cc0e2-111">Create an Azure Databricks workspace</span></span>
> * <span data-ttu-id="cc0e2-112">Create a Spark cluster in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="cc0e2-112">Create a Spark cluster in Azure Databricks</span></span>
> * <span data-ttu-id="cc0e2-113">Create an Azure Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="cc0e2-113">Create an Azure Data Lake Store account</span></span>
> * <span data-ttu-id="cc0e2-114">Upload data to Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cc0e2-114">Upload data to Azure Data Lake Store</span></span>
> * <span data-ttu-id="cc0e2-115">Create a notebook in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="cc0e2-115">Create a notebook in Azure Databricks</span></span>
> * <span data-ttu-id="cc0e2-116">Extract data from Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cc0e2-116">Extract data from Data Lake Store</span></span>
> * <span data-ttu-id="cc0e2-117">Transform data in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="cc0e2-117">Transform data in Azure Databricks</span></span>
> * <span data-ttu-id="cc0e2-118">Load data into Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="cc0e2-118">Load data into Azure SQL Data Warehouse</span></span>

<span data-ttu-id="cc0e2-119">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-119">If you don't have an Azure subscription, [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc0e2-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="cc0e2-120">Prerequisites</span></span>

<span data-ttu-id="cc0e2-121">Before you start with this tutorial, make sure to meet the following requirements:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-121">Before you start with this tutorial, make sure to meet the following requirements:</span></span>
- <span data-ttu-id="cc0e2-122">Create an Azure SQL Data Warehouse, create a server-level firewall rule, and connect to the server as a server admin. Follow the instructions at [Quickstart: Create an Azure SQL Data Warehouse](../sql-data-warehouse/create-data-warehouse-portal.md)</span><span class="sxs-lookup"><span data-stu-id="cc0e2-122">Create an Azure SQL Data Warehouse, create a server-level firewall rule, and connect to the server as a server admin. Follow the instructions at [Quickstart: Create an Azure SQL Data Warehouse](../sql-data-warehouse/create-data-warehouse-portal.md)</span></span>
- <span data-ttu-id="cc0e2-123">Create a database master key for the Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-123">Create a database master key for the Azure SQL Data Warehouse.</span></span> <span data-ttu-id="cc0e2-124">Follow the instructions at [Create a Database Master Key](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-a-database-master-key).</span><span class="sxs-lookup"><span data-stu-id="cc0e2-124">Follow the instructions at [Create a Database Master Key](https://docs.microsoft.com/sql/relational-databases/security/encryption/create-a-database-master-key).</span></span>
- <span data-ttu-id="cc0e2-125">Create an Azure Blob storage account, and a container within it.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-125">Create an Azure Blob storage account, and a container within it.</span></span> <span data-ttu-id="cc0e2-126">Also, retrieve the access key to access the storage account.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-126">Also, retrieve the access key to access the storage account.</span></span> <span data-ttu-id="cc0e2-127">Follow the instructions at [Quickstart: Create an Azure Blog storage account](../storage/blobs/storage-quickstart-blobs-portal.md).</span><span class="sxs-lookup"><span data-stu-id="cc0e2-127">Follow the instructions at [Quickstart: Create an Azure Blog storage account](../storage/blobs/storage-quickstart-blobs-portal.md).</span></span>

## <a name="log-in-to-the-azure-portal"></a><span data-ttu-id="cc0e2-128">Log in to the Azure portal</span><span class="sxs-lookup"><span data-stu-id="cc0e2-128">Log in to the Azure portal</span></span>

<span data-ttu-id="cc0e2-129">Log in to the [Azure portal](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="cc0e2-129">Log in to the [Azure portal](https://portal.azure.com/).</span></span>

## <a name="create-an-azure-databricks-workspace"></a><span data-ttu-id="cc0e2-130">Create an Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="cc0e2-130">Create an Azure Databricks workspace</span></span>

<span data-ttu-id="cc0e2-131">In this section, you create an Azure Databricks workspace using the Azure portal.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-131">In this section, you create an Azure Databricks workspace using the Azure portal.</span></span> 

1. <span data-ttu-id="cc0e2-132">In the Azure portal, select **Create a resource** > **Data + Analytics** > **Azure Databricks**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-132">In the Azure portal, select **Create a resource** > **Data + Analytics** > **Azure Databricks**.</span></span>

    <span data-ttu-id="cc0e2-133">![Databricks on Azure portal](./media/databricks-extract-load-sql-data-warehouse/azure-databricks-on-portal.png "Databricks on Azure portal")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-133">![Databricks on Azure portal](./media/databricks-extract-load-sql-data-warehouse/azure-databricks-on-portal.png "Databricks on Azure portal")</span></span>

3. <span data-ttu-id="cc0e2-134">Under **Azure Databricks Service**, provide the values to create a Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-134">Under **Azure Databricks Service**, provide the values to create a Databricks workspace.</span></span>

    <span data-ttu-id="cc0e2-135">![Create an Azure Databricks workspace](./media/databricks-extract-load-sql-data-warehouse/create-databricks-workspace.png "Create an Azure Databricks workspace")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-135">![Create an Azure Databricks workspace](./media/databricks-extract-load-sql-data-warehouse/create-databricks-workspace.png "Create an Azure Databricks workspace")</span></span>

    <span data-ttu-id="cc0e2-136">Provide the following values:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-136">Provide the following values:</span></span> 
     
    |<span data-ttu-id="cc0e2-137">Property</span><span class="sxs-lookup"><span data-stu-id="cc0e2-137">Property</span></span>  |<span data-ttu-id="cc0e2-138">Description</span><span class="sxs-lookup"><span data-stu-id="cc0e2-138">Description</span></span>  |
    |---------|---------|
    |<span data-ttu-id="cc0e2-139">**Workspace name**</span><span class="sxs-lookup"><span data-stu-id="cc0e2-139">**Workspace name**</span></span>     | <span data-ttu-id="cc0e2-140">Provide a name for your Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="cc0e2-140">Provide a name for your Databricks workspace</span></span>        |
    |<span data-ttu-id="cc0e2-141">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="cc0e2-141">**Subscription**</span></span>     | <span data-ttu-id="cc0e2-142">From the drop-down, select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-142">From the drop-down, select your Azure subscription.</span></span>        |
    |<span data-ttu-id="cc0e2-143">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="cc0e2-143">**Resource group**</span></span>     | <span data-ttu-id="cc0e2-144">Specify whether you want to create a new resource group or use an existing one.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-144">Specify whether you want to create a new resource group or use an existing one.</span></span> <span data-ttu-id="cc0e2-145">A resource group is a container that holds related resources for an Azure solution.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-145">A resource group is a container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="cc0e2-146">For more information, see [Azure Resource Group overview](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="cc0e2-146">For more information, see [Azure Resource Group overview](../azure-resource-manager/resource-group-overview.md).</span></span> |
    |<span data-ttu-id="cc0e2-147">**Location**</span><span class="sxs-lookup"><span data-stu-id="cc0e2-147">**Location**</span></span>     | <span data-ttu-id="cc0e2-148">Select **East US 2**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-148">Select **East US 2**.</span></span> <span data-ttu-id="cc0e2-149">For other available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).</span><span class="sxs-lookup"><span data-stu-id="cc0e2-149">For other available regions, see [Azure services available by region](https://azure.microsoft.com/regions/services/).</span></span>        |
    |<span data-ttu-id="cc0e2-150">**Pricing Tier**</span><span class="sxs-lookup"><span data-stu-id="cc0e2-150">**Pricing Tier**</span></span>     |  <span data-ttu-id="cc0e2-151">Choose between **Standard** or **Premium**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-151">Choose between **Standard** or **Premium**.</span></span> <span data-ttu-id="cc0e2-152">For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).</span><span class="sxs-lookup"><span data-stu-id="cc0e2-152">For more information on these tiers, see [Databricks pricing page](https://azure.microsoft.com/pricing/details/databricks/).</span></span>       |

    <span data-ttu-id="cc0e2-153">Select **Pin to dashboard** and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-153">Select **Pin to dashboard** and then select **Create**.</span></span>

4. <span data-ttu-id="cc0e2-154">The account creation takes a few minutes.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-154">The account creation takes a few minutes.</span></span> <span data-ttu-id="cc0e2-155">During account creation, the portal displays the **Submitting deployment for Azure Databricks** tile on the right side.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-155">During account creation, the portal displays the **Submitting deployment for Azure Databricks** tile on the right side.</span></span> <span data-ttu-id="cc0e2-156">You may need to scroll right on your dashboard to see the tile.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-156">You may need to scroll right on your dashboard to see the tile.</span></span> <span data-ttu-id="cc0e2-157">There is also a progress bar displayed near the top of the screen.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-157">There is also a progress bar displayed near the top of the screen.</span></span> <span data-ttu-id="cc0e2-158">You can watch either area for progress.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-158">You can watch either area for progress.</span></span>

    <span data-ttu-id="cc0e2-159">![Databricks deployment tile](./media/databricks-extract-load-sql-data-warehouse/databricks-deployment-tile.png "Databricks deployment tile")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-159">![Databricks deployment tile](./media/databricks-extract-load-sql-data-warehouse/databricks-deployment-tile.png "Databricks deployment tile")</span></span>

## <a name="create-a-spark-cluster-in-databricks"></a><span data-ttu-id="cc0e2-160">Create a Spark cluster in Databricks</span><span class="sxs-lookup"><span data-stu-id="cc0e2-160">Create a Spark cluster in Databricks</span></span>

1. <span data-ttu-id="cc0e2-161">In the Azure portal, go to the Databricks workspace that you created, and then select **Launch Workspace**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-161">In the Azure portal, go to the Databricks workspace that you created, and then select **Launch Workspace**.</span></span>

2. <span data-ttu-id="cc0e2-162">You are redirected to the Azure Databricks portal.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-162">You are redirected to the Azure Databricks portal.</span></span> <span data-ttu-id="cc0e2-163">From the portal, select **Cluster**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-163">From the portal, select **Cluster**.</span></span>

    <span data-ttu-id="cc0e2-164">![Databricks on Azure](./media/databricks-extract-load-sql-data-warehouse/databricks-on-azure.png "Databricks on Azure")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-164">![Databricks on Azure](./media/databricks-extract-load-sql-data-warehouse/databricks-on-azure.png "Databricks on Azure")</span></span>

3. <span data-ttu-id="cc0e2-165">In the **New cluster** page, provide the values to create a cluster.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-165">In the **New cluster** page, provide the values to create a cluster.</span></span>

    <span data-ttu-id="cc0e2-166">![Create Databricks Spark cluster on Azure](./media/databricks-extract-load-sql-data-warehouse/create-databricks-spark-cluster.png "Create Databricks Spark cluster on Azure")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-166">![Create Databricks Spark cluster on Azure](./media/databricks-extract-load-sql-data-warehouse/create-databricks-spark-cluster.png "Create Databricks Spark cluster on Azure")</span></span>

    <span data-ttu-id="cc0e2-167">Accept all other defaults other than the following values:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-167">Accept all other defaults other than the following values:</span></span>

    * <span data-ttu-id="cc0e2-168">Enter a name for the cluster.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-168">Enter a name for the cluster.</span></span>
    * <span data-ttu-id="cc0e2-169">For this article, create a cluster with **4.0** runtime.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-169">For this article, create a cluster with **4.0** runtime.</span></span> 
    * <span data-ttu-id="cc0e2-170">Make sure you select the **Terminate after ____ minutes of inactivity** checkbox.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-170">Make sure you select the **Terminate after ____ minutes of inactivity** checkbox.</span></span> <span data-ttu-id="cc0e2-171">Provide a duration (in minutes) to terminate the cluster, if the cluster is not being used.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-171">Provide a duration (in minutes) to terminate the cluster, if the cluster is not being used.</span></span>
    
    <span data-ttu-id="cc0e2-172">Select **Create cluster**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-172">Select **Create cluster**.</span></span> <span data-ttu-id="cc0e2-173">Once the cluster is running, you can attach notebooks to the cluster and run Spark jobs.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-173">Once the cluster is running, you can attach notebooks to the cluster and run Spark jobs.</span></span>

## <a name="create-an-azure-data-lake-store-account"></a><span data-ttu-id="cc0e2-174">Create an Azure Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="cc0e2-174">Create an Azure Data Lake Store account</span></span>

<span data-ttu-id="cc0e2-175">In this section, you create an Azure Data Lake Store account and associate an Azure Active Directory service principal with it.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-175">In this section, you create an Azure Data Lake Store account and associate an Azure Active Directory service principal with it.</span></span> <span data-ttu-id="cc0e2-176">Later in this tutorial, you use this service principal in Azure Databricks to access Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-176">Later in this tutorial, you use this service principal in Azure Databricks to access Azure Data Lake Store.</span></span> 

1. <span data-ttu-id="cc0e2-177">From the [Azure portal](https://portal.azure.com), select **Create a resource** > **Storage** > **Data Lake Store**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-177">From the [Azure portal](https://portal.azure.com), select **Create a resource** > **Storage** > **Data Lake Store**.</span></span>
3. <span data-ttu-id="cc0e2-178">In the **New Data Lake Store** blade, provide the values as shown in the following screenshot:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-178">In the **New Data Lake Store** blade, provide the values as shown in the following screenshot:</span></span>
   
    <span data-ttu-id="cc0e2-179">![Create a new Azure Data Lake Store account](./media/databricks-extract-load-sql-data-warehouse/create-new-datalake-store.png "Create a new Azure Data Lake account")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-179">![Create a new Azure Data Lake Store account](./media/databricks-extract-load-sql-data-warehouse/create-new-datalake-store.png "Create a new Azure Data Lake account")</span></span>

    <span data-ttu-id="cc0e2-180">Provide the following values:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-180">Provide the following values:</span></span> 
     
    |<span data-ttu-id="cc0e2-181">Property</span><span class="sxs-lookup"><span data-stu-id="cc0e2-181">Property</span></span>  |<span data-ttu-id="cc0e2-182">Description</span><span class="sxs-lookup"><span data-stu-id="cc0e2-182">Description</span></span>  |
    |---------|---------|
    |<span data-ttu-id="cc0e2-183">**Name**</span><span class="sxs-lookup"><span data-stu-id="cc0e2-183">**Name**</span></span>     | <span data-ttu-id="cc0e2-184">Enter a unique name for the Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-184">Enter a unique name for the Data Lake Store account.</span></span>        |
    |<span data-ttu-id="cc0e2-185">**Subscription**</span><span class="sxs-lookup"><span data-stu-id="cc0e2-185">**Subscription**</span></span>     | <span data-ttu-id="cc0e2-186">From the drop-down, select your Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-186">From the drop-down, select your Azure subscription.</span></span>        |
    |<span data-ttu-id="cc0e2-187">**Resource group**</span><span class="sxs-lookup"><span data-stu-id="cc0e2-187">**Resource group**</span></span>     | <span data-ttu-id="cc0e2-188">For this tutorial, select the same resource group you used while creating the Azure Databricks workspace.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-188">For this tutorial, select the same resource group you used while creating the Azure Databricks workspace.</span></span>  |
    |<span data-ttu-id="cc0e2-189">**Location**</span><span class="sxs-lookup"><span data-stu-id="cc0e2-189">**Location**</span></span>     | <span data-ttu-id="cc0e2-190">Select **East US 2**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-190">Select **East US 2**.</span></span>  |
    |<span data-ttu-id="cc0e2-191">**Pricing package**</span><span class="sxs-lookup"><span data-stu-id="cc0e2-191">**Pricing package**</span></span>     |  <span data-ttu-id="cc0e2-192">Select **Pay-as-you-go**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-192">Select **Pay-as-you-go**.</span></span> |
    | <span data-ttu-id="cc0e2-193">**Encryption Settings**</span><span class="sxs-lookup"><span data-stu-id="cc0e2-193">**Encryption Settings**</span></span> | <span data-ttu-id="cc0e2-194">Keep the default settings.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-194">Keep the default settings.</span></span> |

    <span data-ttu-id="cc0e2-195">Select **Pin to dashboard** and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-195">Select **Pin to dashboard** and then select **Create**.</span></span>

<span data-ttu-id="cc0e2-196">You now create an Azure Active Directory service principal and associate with the Data Lake Store account you created.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-196">You now create an Azure Active Directory service principal and associate with the Data Lake Store account you created.</span></span>

### <a name="create-an-azure-active-directory-service-principal"></a><span data-ttu-id="cc0e2-197">Create an Azure Active Directory service principal</span><span class="sxs-lookup"><span data-stu-id="cc0e2-197">Create an Azure Active Directory service principal</span></span>
   
1. <span data-ttu-id="cc0e2-198">From the [Azure portal](https://portal.azure.com), select **All services**, and then search for **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-198">From the [Azure portal](https://portal.azure.com), select **All services**, and then search for **Azure Active Directory**.</span></span>

2. <span data-ttu-id="cc0e2-199">Select **App registrations**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-199">Select **App registrations**.</span></span>

   ![select app registrations](./media/databricks-extract-load-sql-data-warehouse/select-app-registrations.png)

3. <span data-ttu-id="cc0e2-201">Select **New application registration**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-201">Select **New application registration**.</span></span>

   ![add app](./media/databricks-extract-load-sql-data-warehouse/select-add-app.png)

4. <span data-ttu-id="cc0e2-203">Provide a name and URL for the application.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-203">Provide a name and URL for the application.</span></span> <span data-ttu-id="cc0e2-204">Select **Web app / API** for the type of application you want to create.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-204">Select **Web app / API** for the type of application you want to create.</span></span> <span data-ttu-id="cc0e2-205">Provide a sign-on URL, and then select **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-205">Provide a sign-on URL, and then select **Create**.</span></span>

   ![name application](./media/databricks-extract-load-sql-data-warehouse/create-app.png)

<span data-ttu-id="cc0e2-207">To access the Data Lake Store account from Azure Databricks, you must have the following values for the Azure Active Directory service principal you created:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-207">To access the Data Lake Store account from Azure Databricks, you must have the following values for the Azure Active Directory service principal you created:</span></span>
- <span data-ttu-id="cc0e2-208">Application ID</span><span class="sxs-lookup"><span data-stu-id="cc0e2-208">Application ID</span></span>
- <span data-ttu-id="cc0e2-209">Authentication key</span><span class="sxs-lookup"><span data-stu-id="cc0e2-209">Authentication key</span></span>
- <span data-ttu-id="cc0e2-210">Tenant ID</span><span class="sxs-lookup"><span data-stu-id="cc0e2-210">Tenant ID</span></span>

<span data-ttu-id="cc0e2-211">In the following sections, you retrieve these values for the Azure Active Directory service principal you created earlier.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-211">In the following sections, you retrieve these values for the Azure Active Directory service principal you created earlier.</span></span>

### <a name="get-application-id-and-authentication-key-for-the-service-principal"></a><span data-ttu-id="cc0e2-212">Get application ID and authentication key for the service principal</span><span class="sxs-lookup"><span data-stu-id="cc0e2-212">Get application ID and authentication key for the service principal</span></span>

<span data-ttu-id="cc0e2-213">When programmatically logging in, you need the ID for your application and an authentication key.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-213">When programmatically logging in, you need the ID for your application and an authentication key.</span></span> <span data-ttu-id="cc0e2-214">To get those values, use the following steps:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-214">To get those values, use the following steps:</span></span>

1. <span data-ttu-id="cc0e2-215">From **App registrations** in Azure Active Directory, select your application.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-215">From **App registrations** in Azure Active Directory, select your application.</span></span>

   ![select application](./media/databricks-extract-load-sql-data-warehouse/select-app.png)

2. <span data-ttu-id="cc0e2-217">Copy the **Application ID** and store it in your application code.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-217">Copy the **Application ID** and store it in your application code.</span></span> <span data-ttu-id="cc0e2-218">Some [sample applications](#log-in-as-the-application) refer to this value as the client ID.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-218">Some [sample applications](#log-in-as-the-application) refer to this value as the client ID.</span></span>

   ![client ID](./media/databricks-extract-load-sql-data-warehouse/copy-app-id.png)

3. <span data-ttu-id="cc0e2-220">To generate an authentication key, select **Settings**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-220">To generate an authentication key, select **Settings**.</span></span>

   ![select settings](./media/databricks-extract-load-sql-data-warehouse/select-settings.png)

4. <span data-ttu-id="cc0e2-222">To generate an authentication key, select **Keys**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-222">To generate an authentication key, select **Keys**.</span></span>

   ![select keys](./media/databricks-extract-load-sql-data-warehouse/select-keys.png)

5. <span data-ttu-id="cc0e2-224">Provide a description of the key, and a duration for the key.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-224">Provide a description of the key, and a duration for the key.</span></span> <span data-ttu-id="cc0e2-225">When done, select **Save**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-225">When done, select **Save**.</span></span>

   ![save key](./media/databricks-extract-load-sql-data-warehouse/save-key.png)

   <span data-ttu-id="cc0e2-227">After saving the key, the value of the key is displayed.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-227">After saving the key, the value of the key is displayed.</span></span> <span data-ttu-id="cc0e2-228">Copy this value because you are not able to retrieve the key later.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-228">Copy this value because you are not able to retrieve the key later.</span></span> <span data-ttu-id="cc0e2-229">You provide the key value with the application ID to log in as the application.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-229">You provide the key value with the application ID to log in as the application.</span></span> <span data-ttu-id="cc0e2-230">Store the key value where your application can retrieve it.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-230">Store the key value where your application can retrieve it.</span></span>

   ![saved key](./media/databricks-extract-load-sql-data-warehouse/copy-key.png)

### <a name="get-tenant-id"></a><span data-ttu-id="cc0e2-232">Get tenant ID</span><span class="sxs-lookup"><span data-stu-id="cc0e2-232">Get tenant ID</span></span>

<span data-ttu-id="cc0e2-233">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-233">When programmatically logging in, you need to pass the tenant ID with your authentication request.</span></span>

1. <span data-ttu-id="cc0e2-234">Select **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-234">Select **Azure Active Directory**.</span></span>

   ![select azure active directory](./media/databricks-extract-load-sql-data-warehouse/select-active-directory.png)

1. <span data-ttu-id="cc0e2-236">To get the tenant ID, select **Properties** for your Azure AD tenant.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-236">To get the tenant ID, select **Properties** for your Azure AD tenant.</span></span>

   ![select Azure AD properties](./media/databricks-extract-load-sql-data-warehouse/select-ad-properties.png)

1. <span data-ttu-id="cc0e2-238">Copy the **Directory ID**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-238">Copy the **Directory ID**.</span></span> <span data-ttu-id="cc0e2-239">This value is your tenant ID.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-239">This value is your tenant ID.</span></span>

   ![tenant ID](./media/databricks-extract-load-sql-data-warehouse/copy-directory-id.png) 

## <a name="upload-data-to-data-lake-store"></a><span data-ttu-id="cc0e2-241">Upload data to Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cc0e2-241">Upload data to Data Lake Store</span></span>

<span data-ttu-id="cc0e2-242">In this section, you upload a sample data file to Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-242">In this section, you upload a sample data file to Data Lake Store.</span></span> <span data-ttu-id="cc0e2-243">You use this file later in Azure Databricks to run some transformations.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-243">You use this file later in Azure Databricks to run some transformations.</span></span> <span data-ttu-id="cc0e2-244">The sample data (**small_radio_json.json**) that you use in this tutorial is available in this [Github repo](https://github.com/Azure/usql/blob/master/Examples/Samples/Data/json/radiowebsite/small_radio_json.json).</span><span class="sxs-lookup"><span data-stu-id="cc0e2-244">The sample data (**small_radio_json.json**) that you use in this tutorial is available in this [Github repo](https://github.com/Azure/usql/blob/master/Examples/Samples/Data/json/radiowebsite/small_radio_json.json).</span></span>

1. <span data-ttu-id="cc0e2-245">From the [Azure portal](https://portal.azure.com), select the Data Lake Store account you created.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-245">From the [Azure portal](https://portal.azure.com), select the Data Lake Store account you created.</span></span>

2. <span data-ttu-id="cc0e2-246">From the **Overview** tab, click **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-246">From the **Overview** tab, click **Data Explorer**.</span></span>

    <span data-ttu-id="cc0e2-247">![Open Data Explorer](./media/databricks-extract-load-sql-data-warehouse/open-data-explorer.png "Open Data Explorer")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-247">![Open Data Explorer](./media/databricks-extract-load-sql-data-warehouse/open-data-explorer.png "Open Data Explorer")</span></span>

3. <span data-ttu-id="cc0e2-248">Within the Data Explorer, click **Upload**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-248">Within the Data Explorer, click **Upload**.</span></span>

    <span data-ttu-id="cc0e2-249">![Upload option](./media/databricks-extract-load-sql-data-warehouse/upload-to-data-lake-store.png "Upload option")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-249">![Upload option](./media/databricks-extract-load-sql-data-warehouse/upload-to-data-lake-store.png "Upload option")</span></span>

4. <span data-ttu-id="cc0e2-250">In **Upload files**, browse to the location of your sample data file, and then select **Add selected files**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-250">In **Upload files**, browse to the location of your sample data file, and then select **Add selected files**.</span></span>

    <span data-ttu-id="cc0e2-251">![Upload option](./media/databricks-extract-load-sql-data-warehouse/upload-data.png "Upload option")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-251">![Upload option](./media/databricks-extract-load-sql-data-warehouse/upload-data.png "Upload option")</span></span>

5. <span data-ttu-id="cc0e2-252">In this tutorial, you uploaded the data file to the root of the Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-252">In this tutorial, you uploaded the data file to the root of the Data Lake Store.</span></span> <span data-ttu-id="cc0e2-253">So, the file is now available at `adl://<YOUR_DATA_LAKE_STORE_ACCOUNT_NAME>.azuredatalakestore.net/small_radio_json.json`.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-253">So, the file is now available at `adl://<YOUR_DATA_LAKE_STORE_ACCOUNT_NAME>.azuredatalakestore.net/small_radio_json.json`.</span></span>

## <a name="associate-service-principal-with-azure-data-lake-store"></a><span data-ttu-id="cc0e2-254">Associate service principal with Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cc0e2-254">Associate service principal with Azure Data Lake Store</span></span>

<span data-ttu-id="cc0e2-255">In this section, you associate the data in Azure Data Lake Store account with the Azure Active Directory service principal you created.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-255">In this section, you associate the data in Azure Data Lake Store account with the Azure Active Directory service principal you created.</span></span> <span data-ttu-id="cc0e2-256">This ensures that you can access the Data Lake Store account from Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-256">This ensures that you can access the Data Lake Store account from Azure Databricks.</span></span> <span data-ttu-id="cc0e2-257">For the scenario in this article, you read the data in Data Lake Store to populate a table in SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-257">For the scenario in this article, you read the data in Data Lake Store to populate a table in SQL Data Warehouse.</span></span> <span data-ttu-id="cc0e2-258">According to [Overview of Access Control in Data Lake Store](../data-lake-store/data-lake-store-access-control.md#common-scenarios-related-to-permissions), to have read access on a file in Data Lake Store, you must have:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-258">According to [Overview of Access Control in Data Lake Store](../data-lake-store/data-lake-store-access-control.md#common-scenarios-related-to-permissions), to have read access on a file in Data Lake Store, you must have:</span></span>

- <span data-ttu-id="cc0e2-259">**Execute** permissions on all the folders in the folder structure leading up to the file.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-259">**Execute** permissions on all the folders in the folder structure leading up to the file.</span></span>
- <span data-ttu-id="cc0e2-260">**Read** permissions on the file itself.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-260">**Read** permissions on the file itself.</span></span>

<span data-ttu-id="cc0e2-261">Perform the following steps to grant these permissions.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-261">Perform the following steps to grant these permissions.</span></span>

1. <span data-ttu-id="cc0e2-262">From the [Azure portal](https://portal.azure.com), select the Data Lake Store account you created, and then select **Data Explorer**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-262">From the [Azure portal](https://portal.azure.com), select the Data Lake Store account you created, and then select **Data Explorer**.</span></span>

    <span data-ttu-id="cc0e2-263">![Launch Data Explorer](./media/databricks-extract-load-sql-data-warehouse/azure-databricks-data-explorer.png "Launch Data Explorer")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-263">![Launch Data Explorer](./media/databricks-extract-load-sql-data-warehouse/azure-databricks-data-explorer.png "Launch Data Explorer")</span></span>

2. <span data-ttu-id="cc0e2-264">In this scenario, because the sample data file is at the root of the folder structure, you only need to assign **Execute** permissions at the folder root.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-264">In this scenario, because the sample data file is at the root of the folder structure, you only need to assign **Execute** permissions at the folder root.</span></span> <span data-ttu-id="cc0e2-265">To do so, from the root of data explorer, select **Access**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-265">To do so, from the root of data explorer, select **Access**.</span></span>

    <span data-ttu-id="cc0e2-266">![Add ACLs for the folder](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-folder-1.png "Add ACLs for the folder")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-266">![Add ACLs for the folder](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-folder-1.png "Add ACLs for the folder")</span></span>

3. <span data-ttu-id="cc0e2-267">Under **Access**, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-267">Under **Access**, select **Add**.</span></span>

    <span data-ttu-id="cc0e2-268">![Add ACLs for the folder](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-folder-2.png "Add ACLs for the folder")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-268">![Add ACLs for the folder](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-folder-2.png "Add ACLs for the folder")</span></span>

4. <span data-ttu-id="cc0e2-269">Under **Assign permissions**, click **Select user or group** and search for the Azure Active Directory service principal you created earlier.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-269">Under **Assign permissions**, click **Select user or group** and search for the Azure Active Directory service principal you created earlier.</span></span>

    <span data-ttu-id="cc0e2-270">![Add Data Lake Store access](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-folder-3.png "Add Data Lake Store access")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-270">![Add Data Lake Store access](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-folder-3.png "Add Data Lake Store access")</span></span>

    <span data-ttu-id="cc0e2-271">Select the AAD service principal you want to assign and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-271">Select the AAD service principal you want to assign and click **Select**.</span></span>

5. <span data-ttu-id="cc0e2-272">Under **Assign permissions**, click **Select permissions** > **Execute**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-272">Under **Assign permissions**, click **Select permissions** > **Execute**.</span></span> <span data-ttu-id="cc0e2-273">Keep the other default values and select **OK** under **Select permissions** and then under **Assign permissions**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-273">Keep the other default values and select **OK** under **Select permissions** and then under **Assign permissions**.</span></span>

    <span data-ttu-id="cc0e2-274">![Add Data Lake Store access](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-folder-4.png "Add Data Lake Store access")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-274">![Add Data Lake Store access](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-folder-4.png "Add Data Lake Store access")</span></span>

6. <span data-ttu-id="cc0e2-275">Go back to the Data Explorer and now click the file on which you want to assign the read permission.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-275">Go back to the Data Explorer and now click the file on which you want to assign the read permission.</span></span> <span data-ttu-id="cc0e2-276">Under **File Preview**, select **Access**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-276">Under **File Preview**, select **Access**.</span></span>

    <span data-ttu-id="cc0e2-277">![Add Data Lake Store access](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-file-1.png "Add Data Lake Store access")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-277">![Add Data Lake Store access](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-file-1.png "Add Data Lake Store access")</span></span>

7. <span data-ttu-id="cc0e2-278">Under **Access**, select **Add**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-278">Under **Access**, select **Add**.</span></span> <span data-ttu-id="cc0e2-279">Under **Assign permissions**, click **Select user or group** and search for the Azure Active Directory service principal you created earlier.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-279">Under **Assign permissions**, click **Select user or group** and search for the Azure Active Directory service principal you created earlier.</span></span>

    <span data-ttu-id="cc0e2-280">![Add Data Lake Store access](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-folder-3.png "Add Data Lake Store access")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-280">![Add Data Lake Store access](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-folder-3.png "Add Data Lake Store access")</span></span>

    <span data-ttu-id="cc0e2-281">Select the AAD service principal you want to assign and click **Select**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-281">Select the AAD service principal you want to assign and click **Select**.</span></span>

8. <span data-ttu-id="cc0e2-282">Under **Assign permissions**, click **Select permissions** > **Read**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-282">Under **Assign permissions**, click **Select permissions** > **Read**.</span></span> <span data-ttu-id="cc0e2-283">Select **OK** under **Select permissions** and then under **Assign permissions**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-283">Select **OK** under **Select permissions** and then under **Assign permissions**.</span></span>

    <span data-ttu-id="cc0e2-284">![Add Data Lake Store access](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-file-2.png "Add Data Lake Store access")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-284">![Add Data Lake Store access](./media/databricks-extract-load-sql-data-warehouse/add-adls-access-file-2.png "Add Data Lake Store access")</span></span>

    <span data-ttu-id="cc0e2-285">The service principal now has sufficient permissions to read the sample data file from Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-285">The service principal now has sufficient permissions to read the sample data file from Azure Data Lake Store.</span></span>

## <a name="extract-data-from-data-lake-store"></a><span data-ttu-id="cc0e2-286">Extract data from Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cc0e2-286">Extract data from Data Lake Store</span></span>

<span data-ttu-id="cc0e2-287">In this section, you create a notebook in Azure Databricks workspace and then run code snippets to extract data from Data Lake Store into Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-287">In this section, you create a notebook in Azure Databricks workspace and then run code snippets to extract data from Data Lake Store into Azure Databricks.</span></span>

1. <span data-ttu-id="cc0e2-288">In the [Azure portal](https://portal.azure.com), go to the Azure Databricks workspace you created, and then select **Launch Workspace**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-288">In the [Azure portal](https://portal.azure.com), go to the Azure Databricks workspace you created, and then select **Launch Workspace**.</span></span>

2. <span data-ttu-id="cc0e2-289">In the left pane, select **Workspace**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-289">In the left pane, select **Workspace**.</span></span> <span data-ttu-id="cc0e2-290">From the **Workspace** drop-down, select **Create** > **Notebook**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-290">From the **Workspace** drop-down, select **Create** > **Notebook**.</span></span>

    <span data-ttu-id="cc0e2-291">![Create notebook in Databricks](./media/databricks-extract-load-sql-data-warehouse/databricks-create-notebook.png "Create notebook in Databricks")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-291">![Create notebook in Databricks](./media/databricks-extract-load-sql-data-warehouse/databricks-create-notebook.png "Create notebook in Databricks")</span></span>

2. <span data-ttu-id="cc0e2-292">In the **Create Notebook** dialog box, enter a name for the notebook.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-292">In the **Create Notebook** dialog box, enter a name for the notebook.</span></span> <span data-ttu-id="cc0e2-293">Select **Scala** as the language, and then select the Spark cluster that you created earlier.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-293">Select **Scala** as the language, and then select the Spark cluster that you created earlier.</span></span>

    <span data-ttu-id="cc0e2-294">![Create notebook in Databricks](./media/databricks-extract-load-sql-data-warehouse/databricks-notebook-details.png "Create notebook in Databricks")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-294">![Create notebook in Databricks](./media/databricks-extract-load-sql-data-warehouse/databricks-notebook-details.png "Create notebook in Databricks")</span></span>

    <span data-ttu-id="cc0e2-295">Select **Create**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-295">Select **Create**.</span></span>

3. <span data-ttu-id="cc0e2-296">Add the following snippet in an empty code cell and replace the placeholder values with the values you saved earlier for the Azure Active Directory service principal.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-296">Add the following snippet in an empty code cell and replace the placeholder values with the values you saved earlier for the Azure Active Directory service principal.</span></span>

        spark.conf.set("dfs.adls.oauth2.access.token.provider.type", "ClientCredential")
        spark.conf.set("dfs.adls.oauth2.client.id", "<APPLICATION-ID>")
        spark.conf.set("dfs.adls.oauth2.credential", "<AUTHENTICATION-KEY>")
        spark.conf.set("dfs.adls.oauth2.refresh.url", "https://login.microsoftonline.com/<TENANT-ID>/oauth2/token")

    <span data-ttu-id="cc0e2-297">Press **SHIFT + ENTER** to run the code cell.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-297">Press **SHIFT + ENTER** to run the code cell.</span></span>

4. <span data-ttu-id="cc0e2-298">You can now load the sample json file in Data Lake Store as a dataframe in Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-298">You can now load the sample json file in Data Lake Store as a dataframe in Azure Databricks.</span></span> <span data-ttu-id="cc0e2-299">Past the following snippet in a new code cell, replace the placeholder value, and then press **SHIFT + ENTER**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-299">Past the following snippet in a new code cell, replace the placeholder value, and then press **SHIFT + ENTER**.</span></span>

        val df = spark.read.json("adl://<DATA LAKE STORE NAME>.azuredatalakestore.net/small_radio_json.json")

5. <span data-ttu-id="cc0e2-300">Run the following code snippet to see the contents of the data frame.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-300">Run the following code snippet to see the contents of the data frame.</span></span>

        df.show()

    <span data-ttu-id="cc0e2-301">You see an output similar to the following snippet:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-301">You see an output similar to the following snippet:</span></span>

        +---------------------+---------+---------+------+-------------+----------+---------+-------+--------------------+------+--------+-------------+---------+--------------------+------+-------------+------+
        |               artist|     auth|firstName|gender|itemInSession|  lastName|   length|  level|            location|method|    page| registration|sessionId|                song|status|           ts|userId|
        +---------------------+---------+---------+------+-------------+----------+---------+-------+--------------------+------+--------+-------------+---------+--------------------+------+-------------+------+
        | El Arrebato         |Logged In| Annalyse|     F|            2|Montgomery|234.57914| free  |  Killeen-Temple, TX|   PUT|NextSong|1384448062332|     1879|Quiero Quererte Q...|   200|1409318650332|   309|
        | Creedence Clearwa...|Logged In|   Dylann|     M|            9|    Thomas|340.87138| paid  |       Anchorage, AK|   PUT|NextSong|1400723739332|       10|        Born To Move|   200|1409318653332|    11|
        | Gorillaz            |Logged In|     Liam|     M|           11|     Watts|246.17751| paid  |New York-Newark-J...|   PUT|NextSong|1406279422332|     2047|                DARE|   200|1409318685332|   201|
        ...
        ...

<span data-ttu-id="cc0e2-302">You have now extracted the data from Azure Data Lake Store into Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-302">You have now extracted the data from Azure Data Lake Store into Azure Databricks.</span></span>

## <a name="transform-data-in-azure-databricks"></a><span data-ttu-id="cc0e2-303">Transform data in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="cc0e2-303">Transform data in Azure Databricks</span></span>

<span data-ttu-id="cc0e2-304">The raw sample data **small_radio_json.json** captures the audience for a radio station and has a variety of columns.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-304">The raw sample data **small_radio_json.json** captures the audience for a radio station and has a variety of columns.</span></span> <span data-ttu-id="cc0e2-305">In this section, you transform the data to only retrieve specific columns in from the dataset.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-305">In this section, you transform the data to only retrieve specific columns in from the dataset.</span></span> 

1. <span data-ttu-id="cc0e2-306">Start by retrieving only the columns *firstName*, *lastName*, *gender*, *location*, and *level* from the dataframe you already created.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-306">Start by retrieving only the columns *firstName*, *lastName*, *gender*, *location*, and *level* from the dataframe you already created.</span></span>

        val specificColumnsDf = df.select("firstname", "lastname", "gender", "location", "level")
        specificColumnsDf.show()

    <span data-ttu-id="cc0e2-307">You get an output as shown in the following snippet:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-307">You get an output as shown in the following snippet:</span></span>

        +---------+----------+------+--------------------+-----+
        |firstname|  lastname|gender|            location|level|
        +---------+----------+------+--------------------+-----+
        | Annalyse|Montgomery|     F|  Killeen-Temple, TX| free|
        |   Dylann|    Thomas|     M|       Anchorage, AK| paid|
        |     Liam|     Watts|     M|New York-Newark-J...| paid|
        |     Tess|  Townsend|     F|Nashville-Davidso...| free|
        |  Margaux|     Smith|     F|Atlanta-Sandy Spr...| free|
        |     Alan|     Morse|     M|Chicago-Napervill...| paid|
        |Gabriella|   Shelton|     F|San Jose-Sunnyval...| free|
        |   Elijah|  Williams|     M|Detroit-Warren-De...| paid|
        |  Margaux|     Smith|     F|Atlanta-Sandy Spr...| free|
        |     Tess|  Townsend|     F|Nashville-Davidso...| free|
        |     Alan|     Morse|     M|Chicago-Napervill...| paid|
        |     Liam|     Watts|     M|New York-Newark-J...| paid|
        |     Liam|     Watts|     M|New York-Newark-J...| paid|
        |   Dylann|    Thomas|     M|       Anchorage, AK| paid|
        |     Alan|     Morse|     M|Chicago-Napervill...| paid|
        |   Elijah|  Williams|     M|Detroit-Warren-De...| paid|
        |  Margaux|     Smith|     F|Atlanta-Sandy Spr...| free|
        |     Alan|     Morse|     M|Chicago-Napervill...| paid|
        |   Dylann|    Thomas|     M|       Anchorage, AK| paid|
        |  Margaux|     Smith|     F|Atlanta-Sandy Spr...| free|
        +---------+----------+------+--------------------+-----+

2.  <span data-ttu-id="cc0e2-308">You can further transform this data to rename the column **level** to **subscription_type**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-308">You can further transform this data to rename the column **level** to **subscription_type**.</span></span>

        val renamedColumnsDf = specificColumnsDf.withColumnRenamed("level", "subscription_type")
        renamedColumnsDf.show()

    <span data-ttu-id="cc0e2-309">You get an output as shown in the following snippet.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-309">You get an output as shown in the following snippet.</span></span>

        +---------+----------+------+--------------------+-----------------+
        |firstname|  lastname|gender|            location|subscription_type|
        +---------+----------+------+--------------------+-----------------+
        | Annalyse|Montgomery|     F|  Killeen-Temple, TX|             free|
        |   Dylann|    Thomas|     M|       Anchorage, AK|             paid|
        |     Liam|     Watts|     M|New York-Newark-J...|             paid|
        |     Tess|  Townsend|     F|Nashville-Davidso...|             free|
        |  Margaux|     Smith|     F|Atlanta-Sandy Spr...|             free|
        |     Alan|     Morse|     M|Chicago-Napervill...|             paid|
        |Gabriella|   Shelton|     F|San Jose-Sunnyval...|             free|
        |   Elijah|  Williams|     M|Detroit-Warren-De...|             paid|
        |  Margaux|     Smith|     F|Atlanta-Sandy Spr...|             free|
        |     Tess|  Townsend|     F|Nashville-Davidso...|             free|
        |     Alan|     Morse|     M|Chicago-Napervill...|             paid|
        |     Liam|     Watts|     M|New York-Newark-J...|             paid|
        |     Liam|     Watts|     M|New York-Newark-J...|             paid|
        |   Dylann|    Thomas|     M|       Anchorage, AK|             paid|
        |     Alan|     Morse|     M|Chicago-Napervill...|             paid|
        |   Elijah|  Williams|     M|Detroit-Warren-De...|             paid|
        |  Margaux|     Smith|     F|Atlanta-Sandy Spr...|             free|
        |     Alan|     Morse|     M|Chicago-Napervill...|             paid|
        |   Dylann|    Thomas|     M|       Anchorage, AK|             paid|
        |  Margaux|     Smith|     F|Atlanta-Sandy Spr...|             free|
        +---------+----------+------+--------------------+-----------------+

## <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="cc0e2-310">Load data into Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="cc0e2-310">Load data into Azure SQL Data Warehouse</span></span>

<span data-ttu-id="cc0e2-311">In this section, you upload the transformed data into Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-311">In this section, you upload the transformed data into Azure SQL Data Warehouse.</span></span> <span data-ttu-id="cc0e2-312">Using the Azure SQL Data Warehouse connector for Azure Databricks, you can directly upload a dataframe as a table in SQL data warehouse.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-312">Using the Azure SQL Data Warehouse connector for Azure Databricks, you can directly upload a dataframe as a table in SQL data warehouse.</span></span>

<span data-ttu-id="cc0e2-313">As mentioned earlier, the SQL date warehouse connector uses Azure Blob Storage as temporary storage location to upload data between Azure Databricks and Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-313">As mentioned earlier, the SQL date warehouse connector uses Azure Blob Storage as temporary storage location to upload data between Azure Databricks and Azure SQL Data Warehouse.</span></span> <span data-ttu-id="cc0e2-314">So, you start by providing the configuration to connect to the storage account.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-314">So, you start by providing the configuration to connect to the storage account.</span></span> <span data-ttu-id="cc0e2-315">You must have already created the account as part of the prerequisites for this article.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-315">You must have already created the account as part of the prerequisites for this article.</span></span>

1. <span data-ttu-id="cc0e2-316">Provide the configuration to access the Azure Storage account from Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-316">Provide the configuration to access the Azure Storage account from Azure Databricks.</span></span>

        val blobStorage = "<STORAGE ACCOUNT NAME>.blob.core.windows.net"
        val blobContainer = "<CONTAINER NAME>"
        val blobAccessKey =  "<ACCESS KEY>"

2. <span data-ttu-id="cc0e2-317">Specify a temporary folder that will be used while moving data between Azure Databricks and Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-317">Specify a temporary folder that will be used while moving data between Azure Databricks and Azure SQL Data Warehouse.</span></span>

        val tempDir = "wasbs://" + blobContainer + "@" + blobStorage +"/tempDirs"

3. <span data-ttu-id="cc0e2-318">Run the following snippet to store Azure Blob storage access keys in the configuration.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-318">Run the following snippet to store Azure Blob storage access keys in the configuration.</span></span> <span data-ttu-id="cc0e2-319">This ensures that you do not have to keep the access key in the notebook in plain text.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-319">This ensures that you do not have to keep the access key in the notebook in plain text.</span></span>

        val acntInfo = "fs.azure.account.key."+ blobStorage
        sc.hadoopConfiguration.set(acntInfo, blobAccessKey)

4. <span data-ttu-id="cc0e2-320">Provide the values to connect to the Azure SQL Data Warehouse instance.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-320">Provide the values to connect to the Azure SQL Data Warehouse instance.</span></span> <span data-ttu-id="cc0e2-321">You must have created a SQL data warehouse as part of the prerequisites.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-321">You must have created a SQL data warehouse as part of the prerequisites.</span></span>

        //SQL Data Warehouse related settings
        val dwDatabase = "<DATABASE NAME>"
        val dwServer = "<DATABASE SERVER NAME>" 
        val dwUser = "<USER NAME>"
        val dwPass = "<PASSWORD>"
        val dwJdbcPort =  "1433"
        val dwJdbcExtraOptions = "encrypt=true;trustServerCertificate=true;hostNameInCertificate=*.database.windows.net;loginTimeout=30;"
        val sqlDwUrl = "jdbc:sqlserver://" + dwServer + ".database.windows.net:" + dwJdbcPort + ";database=" + dwDatabase + ";user=" + dwUser+";password=" + dwPass + ";$dwJdbcExtraOptions"
        val sqlDwUrlSmall = "jdbc:sqlserver://" + dwServer + ".database.windows.net:" + dwJdbcPort + ";database=" + dwDatabase + ";user=" + dwUser+";password=" + dwPass

5. Run the following snippet to load the transformed dataframe, **renamedColumnsDf**, as a table in SQL data warehouse. This snippet creates a table called **SampleTable** in the SQL database. Please note that Azure SQL DW requires a master key.  <span data-ttu-id="cc0e2-325">You can create a master key by executing "CREATE MASTER KEY;" command in SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-325">You can create a master key by executing "CREATE MASTER KEY;" command in SQL Server Management Studio.</span></span>

        spark.conf.set(
          "spark.sql.parquet.writeLegacyFormat",
          "true")
        
        renamedColumnsDf.write
            .format("com.databricks.spark.sqldw")
            .option("url", sqlDwUrlSmall) 
            .option("dbtable", "SampleTable")
            .option( "forward_spark_azure_storage_credentials","True")
            .option("tempdir", tempDir)
            .mode("overwrite")
            .save()

6. <span data-ttu-id="cc0e2-326">Connect to the SQL database and verify that you see a **SampleTable**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-326">Connect to the SQL database and verify that you see a **SampleTable**.</span></span>

    <span data-ttu-id="cc0e2-327">![Verify sample table](./media/databricks-extract-load-sql-data-warehouse/verify-sample-table.png "Verify sample table")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-327">![Verify sample table](./media/databricks-extract-load-sql-data-warehouse/verify-sample-table.png "Verify sample table")</span></span>

7. <span data-ttu-id="cc0e2-328">Run a select query to verify the contents of the table.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-328">Run a select query to verify the contents of the table.</span></span> <span data-ttu-id="cc0e2-329">It should have the same data as the **renamedColumnsDf** dataframe.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-329">It should have the same data as the **renamedColumnsDf** dataframe.</span></span>

    <span data-ttu-id="cc0e2-330">![Verify sample table content](./media/databricks-extract-load-sql-data-warehouse/verify-sample-table-content.png "Verify sample table content")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-330">![Verify sample table content](./media/databricks-extract-load-sql-data-warehouse/verify-sample-table-content.png "Verify sample table content")</span></span>

## <a name="clean-up-resources"></a><span data-ttu-id="cc0e2-331">Clean up resources</span><span class="sxs-lookup"><span data-stu-id="cc0e2-331">Clean up resources</span></span>

<span data-ttu-id="cc0e2-332">After you have finished running the tutorial, you can terminate the cluster.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-332">After you have finished running the tutorial, you can terminate the cluster.</span></span> <span data-ttu-id="cc0e2-333">To do so, from the Azure Databricks workspace, from the left pane, select **Clusters**.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-333">To do so, from the Azure Databricks workspace, from the left pane, select **Clusters**.</span></span> <span data-ttu-id="cc0e2-334">For the cluster you want to terminate, move the cursor over the ellipsis under **Actions** column, and select the **Terminate** icon.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-334">For the cluster you want to terminate, move the cursor over the ellipsis under **Actions** column, and select the **Terminate** icon.</span></span>

<span data-ttu-id="cc0e2-335">![Stop a Databricks cluster](./media/databricks-extract-load-sql-data-warehouse/terminate-databricks-cluster.png "Stop a Databricks cluster")</span><span class="sxs-lookup"><span data-stu-id="cc0e2-335">![Stop a Databricks cluster](./media/databricks-extract-load-sql-data-warehouse/terminate-databricks-cluster.png "Stop a Databricks cluster")</span></span>

<span data-ttu-id="cc0e2-336">If you do not manually terminate the cluster it will automatically stop, provided you selected the **Terminate after __ minutes of inactivity** checkbox while creating the cluster.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-336">If you do not manually terminate the cluster it will automatically stop, provided you selected the **Terminate after __ minutes of inactivity** checkbox while creating the cluster.</span></span> <span data-ttu-id="cc0e2-337">In such a case, the cluster automatically stops if it has been inactive for the specified time.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-337">In such a case, the cluster automatically stops if it has been inactive for the specified time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc0e2-338">Next steps</span><span class="sxs-lookup"><span data-stu-id="cc0e2-338">Next steps</span></span> 
<span data-ttu-id="cc0e2-339">In this tutorial, you learned how to:</span><span class="sxs-lookup"><span data-stu-id="cc0e2-339">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cc0e2-340">Create an Azure Databricks workspace</span><span class="sxs-lookup"><span data-stu-id="cc0e2-340">Create an Azure Databricks workspace</span></span>
> * <span data-ttu-id="cc0e2-341">Create a Spark cluster in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="cc0e2-341">Create a Spark cluster in Azure Databricks</span></span>
> * <span data-ttu-id="cc0e2-342">Create an Azure Data Lake Store account</span><span class="sxs-lookup"><span data-stu-id="cc0e2-342">Create an Azure Data Lake Store account</span></span>
> * <span data-ttu-id="cc0e2-343">Upload data to Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cc0e2-343">Upload data to Azure Data Lake Store</span></span>
> * <span data-ttu-id="cc0e2-344">Create a notebook in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="cc0e2-344">Create a notebook in Azure Databricks</span></span>
> * <span data-ttu-id="cc0e2-345">Extract data from Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="cc0e2-345">Extract data from Data Lake Store</span></span>
> * <span data-ttu-id="cc0e2-346">Transform data in Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="cc0e2-346">Transform data in Azure Databricks</span></span>
> * <span data-ttu-id="cc0e2-347">Load data into Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="cc0e2-347">Load data into Azure SQL Data Warehouse</span></span>

<span data-ttu-id="cc0e2-348">Advance to the next tutorial to learn about streaming real-time data into Azure Databricks using Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="cc0e2-348">Advance to the next tutorial to learn about streaming real-time data into Azure Databricks using Azure Event Hubs.</span></span>

> [!div class="nextstepaction"]
>[<span data-ttu-id="cc0e2-349">Stream data into Azure Databricks using Event Hubs</span><span class="sxs-lookup"><span data-stu-id="cc0e2-349">Stream data into Azure Databricks using Event Hubs</span></span>](databricks-stream-from-eventhubs.md)
