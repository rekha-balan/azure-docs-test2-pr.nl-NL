---
title: Build integrated solutions with SQL Data Warehouse | Microsoft Docs
description: 'Tools and partners with solutions that integrate with SQL Data Warehouse. '
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: e2dc8f3f-10e3-4589-a4e2-50c67dfcf67f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: d1cd23eac464d48ebc6dd618c52c252444b47e21
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555726"
---
# <a name="leverage-other-services-with-sql-data-warehouse"></a><span data-ttu-id="9ebcd-103">Leverage other services with SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="9ebcd-103">Leverage other services with SQL Data Warehouse</span></span>
<span data-ttu-id="9ebcd-104">In addition to its core functionality, SQL Data Warehouse enables users to leverage many of the other services in Azure alongside it.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-104">In addition to its core functionality, SQL Data Warehouse enables users to leverage many of the other services in Azure alongside it.</span></span>  <span data-ttu-id="9ebcd-105">Specifically, we have currently taken steps to deeply integrate with the following:</span><span class="sxs-lookup"><span data-stu-id="9ebcd-105">Specifically, we have currently taken steps to deeply integrate with the following:</span></span>

* <span data-ttu-id="9ebcd-106">Power BI</span><span class="sxs-lookup"><span data-stu-id="9ebcd-106">Power BI</span></span>
* <span data-ttu-id="9ebcd-107">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9ebcd-107">Azure Data Factory</span></span>
* <span data-ttu-id="9ebcd-108">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9ebcd-108">Azure Machine Learning</span></span>
* <span data-ttu-id="9ebcd-109">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9ebcd-109">Azure Stream Analytics</span></span>

<span data-ttu-id="9ebcd-110">We are working to connect with more services across the Azure ecosystem.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-110">We are working to connect with more services across the Azure ecosystem.</span></span>

## <a name="power-bi"></a><span data-ttu-id="9ebcd-111">Power BI</span><span class="sxs-lookup"><span data-stu-id="9ebcd-111">Power BI</span></span>
<span data-ttu-id="9ebcd-112">Power BI integration allows you to leverage the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-112">Power BI integration allows you to leverage the compute power of SQL Data Warehouse with the dynamic reporting and visualization of Power BI.</span></span> <span data-ttu-id="9ebcd-113">Power BI integration currently includes:</span><span class="sxs-lookup"><span data-stu-id="9ebcd-113">Power BI integration currently includes:</span></span>

* <span data-ttu-id="9ebcd-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-114">**Direct Connect**: A more advanced connection with logical pushdown against SQL Data Warehouse.</span></span>  <span data-ttu-id="9ebcd-115">This provides faster analysis on a larger scale.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-115">This provides faster analysis on a larger scale.</span></span>
* <span data-ttu-id="9ebcd-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI, allowing for a more seamless connection.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-116">**Open in Power BI**: The 'Open in Power BI' button passes instance information to Power BI, allowing for a more seamless connection.</span></span>

<span data-ttu-id="9ebcd-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-117">See [Integrate with Power BI](sql-data-warehouse-integrate-power-bi.md) or the [Power BI documentation](http://blogs.msdn.com/b/powerbi/archive/2015/06/24/exploring-azure-sql-data-warehouse-with-power-bi.aspx) for more information.</span></span>

## <a name="azure-data-factory"></a><span data-ttu-id="9ebcd-118">Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="9ebcd-118">Azure Data Factory</span></span>
<span data-ttu-id="9ebcd-119">Azure Data Factory gives users a managed platform to create complex Extract-Load pipelines.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-119">Azure Data Factory gives users a managed platform to create complex Extract-Load pipelines.</span></span>  <span data-ttu-id="9ebcd-120">SQL Data Warehouse's integration with Azure Data Factory includes the following:</span><span class="sxs-lookup"><span data-stu-id="9ebcd-120">SQL Data Warehouse's integration with Azure Data Factory includes the following:</span></span>

* <span data-ttu-id="9ebcd-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-121">**Stored Procedures**: Orchestrate the execution of stored procedures on SQL Data Warehouse.</span></span>
* <span data-ttu-id="9ebcd-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-122">**Copy**: Use ADF to move data into SQL Data Warehouse.</span></span>  <span data-ttu-id="9ebcd-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-123">This operation can use ADF's standard data movement mechanism or PolyBase under the covers.</span></span> 

<span data-ttu-id="9ebcd-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-124">See [Integrate with Azure Data Factory](sql-data-warehouse-integrate-azure-data-factory.md) or the [Azure Data Factory documentation](https://azure.microsoft.com/documentation/services/data-factory/) for more information.</span></span>

## <a name="azure-machine-learning"></a><span data-ttu-id="9ebcd-125">Azure Machine Learning</span><span class="sxs-lookup"><span data-stu-id="9ebcd-125">Azure Machine Learning</span></span>
<span data-ttu-id="9ebcd-126">Azure Machine Learning is a fully managed analytics service which allows users to create intricate models leveraging a large set of predictive tools.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-126">Azure Machine Learning is a fully managed analytics service which allows users to create intricate models leveraging a large set of predictive tools.</span></span>  <span data-ttu-id="9ebcd-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span><span class="sxs-lookup"><span data-stu-id="9ebcd-127">SQL Data Warehouse is supported as both a source and destination for these models with the following functionality:</span></span>

* <span data-ttu-id="9ebcd-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-128">**Read Data:** Drive models at scale using T-SQL against SQL Data Warehouse.</span></span>
* <span data-ttu-id="9ebcd-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-129">**Write Data:** Commit changes from any model back to SQL Data Warehouse.</span></span>

<span data-ttu-id="9ebcd-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or the [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-130">See [Integrate with Azure Machine Learning](sql-data-warehouse-integrate-azure-machine-learning.md) or the [Azure Machine Learning documentation](https://azure.microsoft.com/services/machine-learning/) for more information.</span></span>

## <a name="azure-stream-analytics"></a><span data-ttu-id="9ebcd-131">Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9ebcd-131">Azure Stream Analytics</span></span>
<span data-ttu-id="9ebcd-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-132">Azure Stream Analytics is a complex, fully managed infrastructure for processing and consuming event data generated from Azure Event Hub.</span></span>  <span data-ttu-id="9ebcd-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-133">Integration with SQL Data Warehouse allows for streaming data to be effectively processed and stored alongside relational data enabling deeper, more advanced analysis.</span></span>  

* <span data-ttu-id="9ebcd-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-134">**Job Output:** Send output from Stream Analytics jobs directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="9ebcd-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or the [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span><span class="sxs-lookup"><span data-stu-id="9ebcd-135">See [Integrate with Azure Stream Analytics](sql-data-warehouse-integrate-azure-stream-analytics.md) or the [Azure Stream Analytics documentation](https://azure.microsoft.com/documentation/services/stream-analytics/) for more information.</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop/

[Azure Data Factory]: sql-data-warehouse-integrate-azure-data-factory.md
[Azure Machine Learning]: sql-data-warehouse-integrate-azure-machine-learning.md
[Azure Stream Analytics]: sql-data-warehouse-integrate-azure-stream-analytics.md
[Power BI]: sql-data-warehouse-integrate-power-bi.md
[Partners]: sql-data-warehouse-partner-business-intelligence.md

<!--MSDN references-->

<!--Other Web references-->
