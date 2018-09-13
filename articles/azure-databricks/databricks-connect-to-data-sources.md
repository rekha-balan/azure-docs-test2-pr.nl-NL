---
title: Connect to different data sources from Azure Databricks | Microsoft Docs
description: Learn how to connect to different data sources from Azure Databricks.
services: azure-databricks
documentationcenter: ''
author: nitinme
manager: cgronlun
editor: cgronlun
ms.service: azure-databricks
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2018
ms.author: nitinme
ms.openlocfilehash: 865313a7c6eabd847529b88ff5fff0b7db438fa5
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856220"
---
# <a name="connect-to-data-sources-from-azure-databricks"></a><span data-ttu-id="20a4f-103">Connect to data sources from Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="20a4f-103">Connect to data sources from Azure Databricks</span></span>

<span data-ttu-id="20a4f-104">This article provides links to all the different data sources in Azure that can be connected to Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="20a4f-104">This article provides links to all the different data sources in Azure that can be connected to Azure Databricks.</span></span> <span data-ttu-id="20a4f-105">Follow the examples in these links to extract data from the Azure data sources (for example, Azure Blob Storage, Azure Event Hubs, etc.) into an Azure Databricks cluster, and run analytical jobs on them.</span><span class="sxs-lookup"><span data-stu-id="20a4f-105">Follow the examples in these links to extract data from the Azure data sources (for example, Azure Blob Storage, Azure Event Hubs, etc.) into an Azure Databricks cluster, and run analytical jobs on them.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="20a4f-106">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="20a4f-106">Prerequisites</span></span>

* <span data-ttu-id="20a4f-107">You must have an Azure Databricks workspace and a Spark cluster.</span><span class="sxs-lookup"><span data-stu-id="20a4f-107">You must have an Azure Databricks workspace and a Spark cluster.</span></span> <span data-ttu-id="20a4f-108">Follow the instructions at [Get started with Azure Databricks](quickstart-create-databricks-workspace-portal.md).</span><span class="sxs-lookup"><span data-stu-id="20a4f-108">Follow the instructions at [Get started with Azure Databricks](quickstart-create-databricks-workspace-portal.md).</span></span>

## <a name="data-sources-for-azure-databricks"></a><span data-ttu-id="20a4f-109">Data sources for Azure Databricks</span><span class="sxs-lookup"><span data-stu-id="20a4f-109">Data sources for Azure Databricks</span></span>

<span data-ttu-id="20a4f-110">The following list provides the data sources in Azure that you can use with Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="20a4f-110">The following list provides the data sources in Azure that you can use with Azure Databricks.</span></span> <span data-ttu-id="20a4f-111">For a complete list of data sources that can be used with Azure Databricks, see [Data sources for Azure Databricks](https://docs.azuredatabricks.net/spark/latest/data-sources/index.html).</span><span class="sxs-lookup"><span data-stu-id="20a4f-111">For a complete list of data sources that can be used with Azure Databricks, see [Data sources for Azure Databricks](https://docs.azuredatabricks.net/spark/latest/data-sources/index.html).</span></span>

- [<span data-ttu-id="20a4f-112">Azure SQL database</span><span class="sxs-lookup"><span data-stu-id="20a4f-112">Azure SQL database</span></span>](https://docs.azuredatabricks.net/spark/latest/data-sources/sql-databases.html)

    <span data-ttu-id="20a4f-113">This link provides the DataFrame API for connecting to SQL databases using JDBC and how to control the parallelism of reads through the JDBC interface.</span><span class="sxs-lookup"><span data-stu-id="20a4f-113">This link provides the DataFrame API for connecting to SQL databases using JDBC and how to control the parallelism of reads through the JDBC interface.</span></span> <span data-ttu-id="20a4f-114">This topic provides detailed examples using the Scala API, with abbreviated Python and Spark SQL examples at the end.</span><span class="sxs-lookup"><span data-stu-id="20a4f-114">This topic provides detailed examples using the Scala API, with abbreviated Python and Spark SQL examples at the end.</span></span>
- [<span data-ttu-id="20a4f-115">Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="20a4f-115">Azure Data Lake Store</span></span>](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/azure-datalake.html)

    <span data-ttu-id="20a4f-116">This link provides examples on how to use the Azure Active Directory service principal to authenticate with Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="20a4f-116">This link provides examples on how to use the Azure Active Directory service principal to authenticate with Data Lake Store.</span></span> <span data-ttu-id="20a4f-117">It also provides instructions on how to access the data in Data Lake Store from Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="20a4f-117">It also provides instructions on how to access the data in Data Lake Store from Azure Databricks.</span></span>

- [<span data-ttu-id="20a4f-118">Azure Blob Storage</span><span class="sxs-lookup"><span data-stu-id="20a4f-118">Azure Blob Storage</span></span>](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/azure-storage.html)

    <span data-ttu-id="20a4f-119">This link provides examples on how to directly access Azure Blob Storage from Azure Databricks using access key or the SAS for a given container.</span><span class="sxs-lookup"><span data-stu-id="20a4f-119">This link provides examples on how to directly access Azure Blob Storage from Azure Databricks using access key or the SAS for a given container.</span></span> <span data-ttu-id="20a4f-120">The link also provides info on how to access the Azure Blob Storage from Azure Databricks using the RDD API.</span><span class="sxs-lookup"><span data-stu-id="20a4f-120">The link also provides info on how to access the Azure Blob Storage from Azure Databricks using the RDD API.</span></span>

- [<span data-ttu-id="20a4f-121">Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="20a4f-121">Azure Cosmos DB</span></span>](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/cosmosdb-connector.html)

    <span data-ttu-id="20a4f-122">This link provides instructions on how to use the [Azure Cosmos DB Spark connector](https://github.com/Azure/azure-cosmosdb-spark) from Azure Databricks to access data in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="20a4f-122">This link provides instructions on how to use the [Azure Cosmos DB Spark connector](https://github.com/Azure/azure-cosmosdb-spark) from Azure Databricks to access data in Azure Cosmos DB.</span></span>

- [<span data-ttu-id="20a4f-123">Azure Event Hubs</span><span class="sxs-lookup"><span data-stu-id="20a4f-123">Azure Event Hubs</span></span>](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/eventhubs-connector.html)

    <span data-ttu-id="20a4f-124">This link provides instructions on how to use the [Azure Event Hubs Spark connector](https://github.com/Azure/azure-event-hubs-spark) from Azure Databricks to access data in Azure Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="20a4f-124">This link provides instructions on how to use the [Azure Event Hubs Spark connector](https://github.com/Azure/azure-event-hubs-spark) from Azure Databricks to access data in Azure Event Hubs.</span></span>

- [<span data-ttu-id="20a4f-125">Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="20a4f-125">Azure SQL Data Warehouse</span></span>](https://docs.azuredatabricks.net/spark/latest/data-sources/azure/sql-data-warehouse.html)

    <span data-ttu-id="20a4f-126">This link provides instructions on how to use the Azure SQL Data Warehouse connector to connect from Azure Databricks.</span><span class="sxs-lookup"><span data-stu-id="20a4f-126">This link provides instructions on how to use the Azure SQL Data Warehouse connector to connect from Azure Databricks.</span></span>
    

## <a name="next-steps"></a><span data-ttu-id="20a4f-127">Next steps</span><span class="sxs-lookup"><span data-stu-id="20a4f-127">Next steps</span></span>

<span data-ttu-id="20a4f-128">To learn about sources from where you can import data into Azure Databricks, see [Data sources for Azure Databricks](https://docs.azuredatabricks.net/spark/latest/data-sources/index.html#).</span><span class="sxs-lookup"><span data-stu-id="20a4f-128">To learn about sources from where you can import data into Azure Databricks, see [Data sources for Azure Databricks](https://docs.azuredatabricks.net/spark/latest/data-sources/index.html#).</span></span>


