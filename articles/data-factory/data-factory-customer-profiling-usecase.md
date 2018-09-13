---
title: Use Case - Customer Profiling
description: Learn how Azure Data Factory is used to create a data-driven workflow (pipeline) to profile gaming customers.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: e07d55cf-8051-4203-9966-bdfa1035104b
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/24/2017
ms.author: shlo
ms.openlocfilehash: 510af827ddf82970d9570babdc63e84aad40a961
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563182"
---
# <a name="use-case---customer-profiling"></a><span data-ttu-id="88c5d-103">Use Case - Customer Profiling</span><span class="sxs-lookup"><span data-stu-id="88c5d-103">Use Case - Customer Profiling</span></span>
<span data-ttu-id="88c5d-104">Azure Data Factory is one of many services used to implement the Cortana Intelligence Suite of solution accelerators.</span><span class="sxs-lookup"><span data-stu-id="88c5d-104">Azure Data Factory is one of many services used to implement the Cortana Intelligence Suite of solution accelerators.</span></span>  <span data-ttu-id="88c5d-105">For more information about Cortana Intelligence, visit [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics).</span><span class="sxs-lookup"><span data-stu-id="88c5d-105">For more information about Cortana Intelligence, visit [Cortana Intelligence Suite](http://www.microsoft.com/cortanaanalytics).</span></span> <span data-ttu-id="88c5d-106">In this document, we describe a simple use case to help you get started with understanding how Azure Data Factory can solve common analytics problems.</span><span class="sxs-lookup"><span data-stu-id="88c5d-106">In this document, we describe a simple use case to help you get started with understanding how Azure Data Factory can solve common analytics problems.</span></span>

## <a name="scenario"></a><span data-ttu-id="88c5d-107">Scenario</span><span class="sxs-lookup"><span data-stu-id="88c5d-107">Scenario</span></span>
<span data-ttu-id="88c5d-108">Contoso is a gaming company that creates games for multiple platforms: game consoles, hand held devices, and personal computers (PCs).</span><span class="sxs-lookup"><span data-stu-id="88c5d-108">Contoso is a gaming company that creates games for multiple platforms: game consoles, hand held devices, and personal computers (PCs).</span></span> <span data-ttu-id="88c5d-109">As players play these games, large volume of log data is produced that tracks the usage patterns, gaming style, and preferences of the user.</span><span class="sxs-lookup"><span data-stu-id="88c5d-109">As players play these games, large volume of log data is produced that tracks the usage patterns, gaming style, and preferences of the user.</span></span>  <span data-ttu-id="88c5d-110">When combined with demographic, regional, and product data, Contoso can perform analytics to guide them about how to enhance players’ experience and target them for upgrades and in-game purchases.</span><span class="sxs-lookup"><span data-stu-id="88c5d-110">When combined with demographic, regional, and product data, Contoso can perform analytics to guide them about how to enhance players’ experience and target them for upgrades and in-game purchases.</span></span> 

<span data-ttu-id="88c5d-111">Contoso’s goal is to identify up-sell/cross-sell opportunities based on the gaming history of its players and add compelling features to drive business growth and provide a better experience to customers.</span><span class="sxs-lookup"><span data-stu-id="88c5d-111">Contoso’s goal is to identify up-sell/cross-sell opportunities based on the gaming history of its players and add compelling features to drive business growth and provide a better experience to customers.</span></span> <span data-ttu-id="88c5d-112">For this use case, we use a gaming company as an example of a business.</span><span class="sxs-lookup"><span data-stu-id="88c5d-112">For this use case, we use a gaming company as an example of a business.</span></span> <span data-ttu-id="88c5d-113">The company wants to optimize its games based on players’ behavior.</span><span class="sxs-lookup"><span data-stu-id="88c5d-113">The company wants to optimize its games based on players’ behavior.</span></span> <span data-ttu-id="88c5d-114">These principles apply to any business that wants to engage its customers around its goods and services and enhance their customers’ experience.</span><span class="sxs-lookup"><span data-stu-id="88c5d-114">These principles apply to any business that wants to engage its customers around its goods and services and enhance their customers’ experience.</span></span>

<span data-ttu-id="88c5d-115">In this solution, Contoso wants to evaluate the effectiveness of a marketing campaign it has recently launched.</span><span class="sxs-lookup"><span data-stu-id="88c5d-115">In this solution, Contoso wants to evaluate the effectiveness of a marketing campaign it has recently launched.</span></span> <span data-ttu-id="88c5d-116">We start with the raw gaming logs, process and enrich them with geolocation data, join it with advertising reference data, and lastly copy them into an Azure SQL Database to analyze the campaign’s impact.</span><span class="sxs-lookup"><span data-stu-id="88c5d-116">We start with the raw gaming logs, process and enrich them with geolocation data, join it with advertising reference data, and lastly copy them into an Azure SQL Database to analyze the campaign’s impact.</span></span>

## <a name="deploy-solution"></a><span data-ttu-id="88c5d-117">Deploy Solution</span><span class="sxs-lookup"><span data-stu-id="88c5d-117">Deploy Solution</span></span>
<span data-ttu-id="88c5d-118">All you need to access and try out this simple use case is an [Azure subscription](https://azure.microsoft.com/pricing/free-trial/), an [Azure Blob storage account](../storage/storage-create-storage-account.md#create-a-storage-account), and an [Azure SQL Database](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="88c5d-118">All you need to access and try out this simple use case is an [Azure subscription](https://azure.microsoft.com/pricing/free-trial/), an [Azure Blob storage account](../storage/storage-create-storage-account.md#create-a-storage-account), and an [Azure SQL Database](../sql-database/sql-database-get-started.md).</span></span> <span data-ttu-id="88c5d-119">You deploy the customer profiling pipeline from the **Sample pipelines** tile on the home page of your data factory.</span><span class="sxs-lookup"><span data-stu-id="88c5d-119">You deploy the customer profiling pipeline from the **Sample pipelines** tile on the home page of your data factory.</span></span>

1. <span data-ttu-id="88c5d-120">Create a data factory or open an existing data factory.</span><span class="sxs-lookup"><span data-stu-id="88c5d-120">Create a data factory or open an existing data factory.</span></span> <span data-ttu-id="88c5d-121">See [Copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for steps to create a data factory.</span><span class="sxs-lookup"><span data-stu-id="88c5d-121">See [Copy data from Blob Storage to SQL Database using Data Factory](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) for steps to create a data factory.</span></span>
2. <span data-ttu-id="88c5d-122">In the **DATA FACTORY** blade for the data factory, click the **Sample pipelines** tile.</span><span class="sxs-lookup"><span data-stu-id="88c5d-122">In the **DATA FACTORY** blade for the data factory, click the **Sample pipelines** tile.</span></span>

    ![Sample pipelines tile](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-samples/SamplePipelinesTile.png)
3. <span data-ttu-id="88c5d-124">In the **Sample pipelines** blade, click the **Customer profiling** that you want to deploy.</span><span class="sxs-lookup"><span data-stu-id="88c5d-124">In the **Sample pipelines** blade, click the **Customer profiling** that you want to deploy.</span></span>

    ![Sample pipelines blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-samples/SampleTile.png)
4. <span data-ttu-id="88c5d-126">Specify configuration settings for the sample.</span><span class="sxs-lookup"><span data-stu-id="88c5d-126">Specify configuration settings for the sample.</span></span> <span data-ttu-id="88c5d-127">For example, your Azure storage account name and key, Azure SQL server name, database, User ID, and password.</span><span class="sxs-lookup"><span data-stu-id="88c5d-127">For example, your Azure storage account name and key, Azure SQL server name, database, User ID, and password.</span></span>

    ![Sample blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-samples/SampleBlade.png)
5. <span data-ttu-id="88c5d-129">After you are done with specifying the configuration settings, click **Create** to create/deploy the sample pipelines and linked services/tables used by the pipelines.</span><span class="sxs-lookup"><span data-stu-id="88c5d-129">After you are done with specifying the configuration settings, click **Create** to create/deploy the sample pipelines and linked services/tables used by the pipelines.</span></span>
6. <span data-ttu-id="88c5d-130">You see the status of deployment on the sample tile you clicked earlier on the **Sample pipelines** blade.</span><span class="sxs-lookup"><span data-stu-id="88c5d-130">You see the status of deployment on the sample tile you clicked earlier on the **Sample pipelines** blade.</span></span>

    ![Deployment status](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-samples/DeploymentStatus.png)
7. <span data-ttu-id="88c5d-132">When you see the **Deployment succeeded** message on the tile for the sample, close the **Sample pipelines** blade.</span><span class="sxs-lookup"><span data-stu-id="88c5d-132">When you see the **Deployment succeeded** message on the tile for the sample, close the **Sample pipelines** blade.</span></span>  
8. <span data-ttu-id="88c5d-133">On **DATA FACTORY** blade, you see that linked services, data sets, and pipelines are added to your data factory.</span><span class="sxs-lookup"><span data-stu-id="88c5d-133">On **DATA FACTORY** blade, you see that linked services, data sets, and pipelines are added to your data factory.</span></span>  

    ![Data Factory blade](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-samples/DataFactoryBladeAfter.png)

## <a name="solution-overview"></a><span data-ttu-id="88c5d-135">Solution Overview</span><span class="sxs-lookup"><span data-stu-id="88c5d-135">Solution Overview</span></span>
<span data-ttu-id="88c5d-136">This simple use case can be used as an example of how you can use Azure Data Factory to ingest, prepare, transform, analyze, and publish data.</span><span class="sxs-lookup"><span data-stu-id="88c5d-136">This simple use case can be used as an example of how you can use Azure Data Factory to ingest, prepare, transform, analyze, and publish data.</span></span>

![End-to-end workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-factory/media/data-factory-customer-profiling-usecase/EndToEndWorkflow.png)

<span data-ttu-id="88c5d-138">This Figure depicts how the data pipelines appear in the Azure portal after they have been deployed.</span><span class="sxs-lookup"><span data-stu-id="88c5d-138">This Figure depicts how the data pipelines appear in the Azure portal after they have been deployed.</span></span>

1. <span data-ttu-id="88c5d-139">The **PartitionGameLogsPipeline** reads the raw game events from blob storage and creates partitions based on year, month, and day.</span><span class="sxs-lookup"><span data-stu-id="88c5d-139">The **PartitionGameLogsPipeline** reads the raw game events from blob storage and creates partitions based on year, month, and day.</span></span>
2. <span data-ttu-id="88c5d-140">The **EnrichGameLogsPipeline** joins partitioned game events with geo code reference data and enriches the data by mapping IP addresses to the corresponding geo-locations.</span><span class="sxs-lookup"><span data-stu-id="88c5d-140">The **EnrichGameLogsPipeline** joins partitioned game events with geo code reference data and enriches the data by mapping IP addresses to the corresponding geo-locations.</span></span>
3. <span data-ttu-id="88c5d-141">The **AnalyzeMarketingCampaignPipeline** pipeline uses the enriched data and processes it with the advertising data to create the final output that contains marketing campaign effectiveness.</span><span class="sxs-lookup"><span data-stu-id="88c5d-141">The **AnalyzeMarketingCampaignPipeline** pipeline uses the enriched data and processes it with the advertising data to create the final output that contains marketing campaign effectiveness.</span></span>

<span data-ttu-id="88c5d-142">In this example, Data Factory is used to orchestrate activities that copy input data, transform, and process the data, and output the final data to an Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="88c5d-142">In this example, Data Factory is used to orchestrate activities that copy input data, transform, and process the data, and output the final data to an Azure SQL Database.</span></span>  <span data-ttu-id="88c5d-143">You can also visualize the network of data pipelines, manage them, and monitor their status from the UI.</span><span class="sxs-lookup"><span data-stu-id="88c5d-143">You can also visualize the network of data pipelines, manage them, and monitor their status from the UI.</span></span>

## <a name="benefits"></a><span data-ttu-id="88c5d-144">Benefits</span><span class="sxs-lookup"><span data-stu-id="88c5d-144">Benefits</span></span>
<span data-ttu-id="88c5d-145">By optimizing their user profile analytics and aligning it with business goals, gaming company is able to quickly collect usage patterns, and analyze the effectiveness of its marketing campaigns.</span><span class="sxs-lookup"><span data-stu-id="88c5d-145">By optimizing their user profile analytics and aligning it with business goals, gaming company is able to quickly collect usage patterns, and analyze the effectiveness of its marketing campaigns.</span></span>







