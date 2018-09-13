---
title: Use Power BI with SQL Data Warehouse | Microsoft Docs
description: Tips for using Power BI with Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: b12bee87-2268-40c2-81bf-ab27588b32e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: eccfc6706385dc0c51eedbc9048bed91c493d837
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44555335"
---
# <a name="use-power-bi-with-sql-data-warehouse"></a><span data-ttu-id="db3ac-103">Use Power BI with SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="db3ac-103">Use Power BI with SQL Data Warehouse</span></span>
<span data-ttu-id="db3ac-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user to leverage powerful logical pushdown alongside the analytical capabilities of Power BI.</span><span class="sxs-lookup"><span data-stu-id="db3ac-104">As with Azure SQL Database, SQL Data Warehouse Direct Connect allows user to leverage powerful logical pushdown alongside the analytical capabilities of Power BI.</span></span>  <span data-ttu-id="db3ac-105">With Direct Connect, queries are sent back to your Azure SQL Data Warehouse in real time as you explore the data.</span><span class="sxs-lookup"><span data-stu-id="db3ac-105">With Direct Connect, queries are sent back to your Azure SQL Data Warehouse in real time as you explore the data.</span></span>  <span data-ttu-id="db3ac-106">This, combined with the scale of SQL Data Warehouse, enables users to create dynamic reports in minutes against terabytes of data.</span><span class="sxs-lookup"><span data-stu-id="db3ac-106">This, combined with the scale of SQL Data Warehouse, enables users to create dynamic reports in minutes against terabytes of data.</span></span>  <span data-ttu-id="db3ac-107">In addition, the introduction of the Open in Power BI button allows users to directly connect Power BI to their SQL Data Warehouse without collecting information from other parts of Azure.</span><span class="sxs-lookup"><span data-stu-id="db3ac-107">In addition, the introduction of the Open in Power BI button allows users to directly connect Power BI to their SQL Data Warehouse without collecting information from other parts of Azure.</span></span>

<span data-ttu-id="db3ac-108">When using Direct Connect please note:</span><span class="sxs-lookup"><span data-stu-id="db3ac-108">When using Direct Connect please note:</span></span>

* <span data-ttu-id="db3ac-109">Specify the fully qualified server name when connecting (see below for more details)</span><span class="sxs-lookup"><span data-stu-id="db3ac-109">Specify the fully qualified server name when connecting (see below for more details)</span></span>
* <span data-ttu-id="db3ac-110">Ensure firewall rules for the database are configured to "Allow access to Azure services".</span><span class="sxs-lookup"><span data-stu-id="db3ac-110">Ensure firewall rules for the database are configured to "Allow access to Azure services".</span></span>
* <span data-ttu-id="db3ac-111">Every action such as selecting a column or adding a filter will  directly query the data warehouse</span><span class="sxs-lookup"><span data-stu-id="db3ac-111">Every action such as selecting a column or adding a filter will  directly query the data warehouse</span></span>
* <span data-ttu-id="db3ac-112">Tiles are refreshed approximately every 15 minutes (refresh does not need to be scheduled)</span><span class="sxs-lookup"><span data-stu-id="db3ac-112">Tiles are refreshed approximately every 15 minutes (refresh does not need to be scheduled)</span></span>
* <span data-ttu-id="db3ac-113">Q&A is not available for Direct Connect datasets</span><span class="sxs-lookup"><span data-stu-id="db3ac-113">Q&A is not available for Direct Connect datasets</span></span>
* <span data-ttu-id="db3ac-114">Schema changes are not picked up automatically</span><span class="sxs-lookup"><span data-stu-id="db3ac-114">Schema changes are not picked up automatically</span></span>
* <span data-ttu-id="db3ac-115">All Direct Connect queries will time out after 2 minutes</span><span class="sxs-lookup"><span data-stu-id="db3ac-115">All Direct Connect queries will time out after 2 minutes</span></span>

<span data-ttu-id="db3ac-116">These restrictions and notes may change as we continue to improve the experiences.</span><span class="sxs-lookup"><span data-stu-id="db3ac-116">These restrictions and notes may change as we continue to improve the experiences.</span></span> <span data-ttu-id="db3ac-117">The steps to connect are detailed below.</span><span class="sxs-lookup"><span data-stu-id="db3ac-117">The steps to connect are detailed below.</span></span>  

## <a name="using-the-open-in-power-bi-button"></a><span data-ttu-id="db3ac-118">Using the ‘Open in Power BI’ button</span><span class="sxs-lookup"><span data-stu-id="db3ac-118">Using the ‘Open in Power BI’ button</span></span>
<span data-ttu-id="db3ac-119">The easiest way to move between your SQL Data Warehouse and Power BI is with the Open in Power BI button.</span><span class="sxs-lookup"><span data-stu-id="db3ac-119">The easiest way to move between your SQL Data Warehouse and Power BI is with the Open in Power BI button.</span></span> <span data-ttu-id="db3ac-120">This button allows you to seamlessly begin creating new dashboards in Power BI.</span><span class="sxs-lookup"><span data-stu-id="db3ac-120">This button allows you to seamlessly begin creating new dashboards in Power BI.</span></span>  

1. <span data-ttu-id="db3ac-121">To get started navigate to your SQL Data Warehouse instance in the Azure Classic Portal.</span><span class="sxs-lookup"><span data-stu-id="db3ac-121">To get started navigate to your SQL Data Warehouse instance in the Azure Classic Portal.</span></span>
2. <span data-ttu-id="db3ac-122">Click the 'Open in Power BI' button.</span><span class="sxs-lookup"><span data-stu-id="db3ac-122">Click the 'Open in Power BI' button.</span></span>
3. <span data-ttu-id="db3ac-123">If we are not able to sign you in directly, or if you do not have a Power BI account, you will need to sign-in.</span><span class="sxs-lookup"><span data-stu-id="db3ac-123">If we are not able to sign you in directly, or if you do not have a Power BI account, you will need to sign-in.</span></span>  
4. <span data-ttu-id="db3ac-124">You will be directed to the SQL Data Warehouse connection page, with the information from your SQL Data Warehouse pre-populated.</span><span class="sxs-lookup"><span data-stu-id="db3ac-124">You will be directed to the SQL Data Warehouse connection page, with the information from your SQL Data Warehouse pre-populated.</span></span>
5. <span data-ttu-id="db3ac-125">After entering your credentials you will be fully connected to your SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="db3ac-125">After entering your credentials you will be fully connected to your SQL Data Warehouse.</span></span>

## <a name="connecting-through-the-power-bi-portal"></a><span data-ttu-id="db3ac-126">Connecting through the Power BI portal</span><span class="sxs-lookup"><span data-stu-id="db3ac-126">Connecting through the Power BI portal</span></span>
<span data-ttu-id="db3ac-127">In addition to using the Open in Power BI button, users can also connect to their SQL Data Warehouse through the Power BI Portal.</span><span class="sxs-lookup"><span data-stu-id="db3ac-127">In addition to using the Open in Power BI button, users can also connect to their SQL Data Warehouse through the Power BI Portal.</span></span>

1. <span data-ttu-id="db3ac-128">Click 'Get Data' at the bottom of the navigation pane.</span><span class="sxs-lookup"><span data-stu-id="db3ac-128">Click 'Get Data' at the bottom of the navigation pane.</span></span>
2. <span data-ttu-id="db3ac-129">Select 'Databases'.</span><span class="sxs-lookup"><span data-stu-id="db3ac-129">Select 'Databases'.</span></span>
3. <span data-ttu-id="db3ac-130">Once on the Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span><span class="sxs-lookup"><span data-stu-id="db3ac-130">Once on the Databases page, select 'Azure SQL Data Warehouse' and then click 'Connect'.</span></span>
4. <span data-ttu-id="db3ac-131">Enter the necessary connection information.</span><span class="sxs-lookup"><span data-stu-id="db3ac-131">Enter the necessary connection information.</span></span>  <span data-ttu-id="db3ac-132">Your server name and database name can be found in the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="db3ac-132">Your server name and database name can be found in the Azure Portal.</span></span>
5. <span data-ttu-id="db3ac-133">You will be directed back to the main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with the name of your instance.</span><span class="sxs-lookup"><span data-stu-id="db3ac-133">You will be directed back to the main page of Power BI and after your connection is made a new entry under 'Datasets' will appear with the name of your instance.</span></span>  
6. <span data-ttu-id="db3ac-134">You can click on the new dataset to explore all of the tables and views in your database.</span><span class="sxs-lookup"><span data-stu-id="db3ac-134">You can click on the new dataset to explore all of the tables and views in your database.</span></span> <span data-ttu-id="db3ac-135">Selecting a column will send a query back to the source, dynamically creating your visual.</span><span class="sxs-lookup"><span data-stu-id="db3ac-135">Selecting a column will send a query back to the source, dynamically creating your visual.</span></span> <span data-ttu-id="db3ac-136">These visuals can be saved in a new report and pinned back to your dashboard.</span><span class="sxs-lookup"><span data-stu-id="db3ac-136">These visuals can be saved in a new report and pinned back to your dashboard.</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]:  ./sql-data-warehouse-overview-develop/
[SQL Data Warehouse integration overview]:  ./sql-data-warehouse-overview-integration/

<!--MSDN references-->

<!--Other Web references-->
