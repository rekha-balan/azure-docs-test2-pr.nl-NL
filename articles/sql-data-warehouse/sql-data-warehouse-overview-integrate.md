---
title: Build integrated solutions with SQL Data Warehouse | Microsoft Docs
description: 'Tools and partners with solutions that integrate with SQL Data Warehouse. '
services: sql-data-warehouse
author: kavithaj
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: consume
ms.date: 04/17/2018
ms.author: kavithaj
ms.reviewer: igorstan
ms.openlocfilehash: 221d5d05906e7e162013c0d4cdddc01a95f4024c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44808631"
---
# <a name="integrate-other-services-with-sql-data-warehouse"></a><span data-ttu-id="26782-103">Integrate other services with SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="26782-103">Integrate other services with SQL Data Warehouse</span></span>
<span data-ttu-id="26782-104">In addition to its core functionality, SQL Data Warehouse enables users to integrate with many of the other services in Azure.</span><span class="sxs-lookup"><span data-stu-id="26782-104">In addition to its core functionality, SQL Data Warehouse enables users to integrate with many of the other services in Azure.</span></span> <span data-ttu-id="26782-105">Some of these services include:</span><span class="sxs-lookup"><span data-stu-id="26782-105">Some of these services include:</span></span>

* <span data-ttu-id="26782-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="26782-106">Power BI</span></span>
* <span data-ttu-id="26782-107">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="26782-107">Azure Data Factory</span></span>
* <span data-ttu-id="26782-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="26782-108">Azure Machine Learning</span></span>
* <span data-ttu-id="26782-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="26782-109">Azure Stream Analytics</span></span>

<span data-ttu-id="26782-110">SQL Data Warehouse continues to integrate with more services across Azure, and more [Integration partners](sql-data-warehouse-partner-data-integration.md).</span><span class="sxs-lookup"><span data-stu-id="26782-110">SQL Data Warehouse continues to integrate with more services across Azure, and more [Integration partners](sql-data-warehouse-partner-data-integration.md).</span></span>

## <a name="power-bi"></a><span data-ttu-id="26782-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="26782-111">Power BI</span></span>
<span data-ttu-id="26782-112">Power BI integration allows you to combine the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span><span class="sxs-lookup"><span data-stu-id="26782-112">Power BI integration allows you to combine the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="26782-113">Power BI integration currently includes:</span><span class="sxs-lookup"><span data-stu-id="26782-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="26782-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="26782-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span> <span data-ttu-id="26782-115">Pushdown provides faster analysis on a larger scale.</span><span class="sxs-lookup"><span data-stu-id="26782-115">Pushdown provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="26782-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI for a simplifed way to connect.</span><span class="sxs-lookup"><span data-stu-id="26782-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI for a simplifed way to connect.</span></span>

<span data-ttu-id="26782-117">For more information, see [Integrate with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md), or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx).</span><span class="sxs-lookup"><span data-stu-id="26782-117">For more information, see [Integrate with Power BI](sql-data-warehouse-get-started-visualize-with-power-bi.md), or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx).</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="26782-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="26782-118">Azure Data Factory</span></span>
<span data-ttu-id="26782-119">Azure Data Factory gives users a managed platform to create complex extract and load pipelines.</span><span class="sxs-lookup"><span data-stu-id="26782-119">Azure Data Factory gives users a managed platform to create complex extract and load pipelines.</span></span> <span data-ttu-id="26782-120">SQL Data Warehouse's integration with Azure Data Factory includes:</span><span class="sxs-lookup"><span data-stu-id="26782-120">SQL Data Warehouse's integration with Azure Data Factory includes:</span></span>

* <span data-ttu-id="26782-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="26782-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="26782-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="26782-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span></span> <span data-ttu-id="26782-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span><span class="sxs-lookup"><span data-stu-id="26782-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span></span> 

<span data-ttu-id="26782-124">For more information, see [Integrate with Azure Data Factory](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="26782-124">For more information, see [Integrate with Azure Data Factory](sql-data-warehouse-get-started-visualize-with-power-bi.md).</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="26782-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="26782-125">Azure Machine Learning</span></span>
<span data-ttu-id="26782-126">Azure Machine Learning is a fully managed analytics service, which allows you to create intricate models using a large set of predictive tools.</span><span class="sxs-lookup"><span data-stu-id="26782-126">Azure Machine Learning is a fully managed analytics service, which allows you to create intricate models using a large set of predictive tools.</span></span> <span data-ttu-id="26782-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span><span class="sxs-lookup"><span data-stu-id="26782-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span></span>

* <span data-ttu-id="26782-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="26782-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="26782-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="26782-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span></span>

<span data-ttu-id="26782-130">For more information, see [Integrate with Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md).</span><span class="sxs-lookup"><span data-stu-id="26782-130">For more information, see [Integrate with Azure Machine Learning](sql-data-warehouse-get-started-analyze-with-azure-machine-learning.md).</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="26782-131">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="26782-131">Azure Stream Analytics</span></span>
<span data-ttu-id="26782-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="26782-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="26782-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span><span class="sxs-lookup"><span data-stu-id="26782-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="26782-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="26782-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="26782-135">For more information, see [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="26782-135">For more information, see [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="26782-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="26782-136">Next steps</span></span>
<span data-ttu-id="26782-137">To integrate with Azure SQL Database, see [Configure SQL Database elastic query](tutorial-elastic-query-with-sql-datababase-and-sql-data-warehouse.md)</span><span class="sxs-lookup"><span data-stu-id="26782-137">To integrate with Azure SQL Database, see [Configure SQL Database elastic query](tutorial-elastic-query-with-sql-datababase-and-sql-data-warehouse.md)</span></span>

