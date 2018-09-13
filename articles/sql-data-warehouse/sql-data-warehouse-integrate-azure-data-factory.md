---
title: Use Azure Data Factory with SQL Data Warehouse | Microsoft Docs
description: Tips for using Azure Data Factory (ADF) with Azure SQL Data Warehouse for developing solutions.
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: 492de762-c7a2-4cdb-943f-3135230e94f1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: integrate
ms.date: 10/31/2016
ms.author: barbkess
ms.openlocfilehash: 12743b3594a0a62b0b974fb6dd1c39972c1bd3fa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556309"
---
# <a name="use-azure-data-factory-with-sql-data-warehouse"></a><span data-ttu-id="d528c-103">Use Azure Data Factory with SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="d528c-103">Use Azure Data Factory with SQL Data Warehouse</span></span>
<span data-ttu-id="d528c-104">Azure Data Factory provides a fully managed method for orchestrating the transfer of data and execution of stored procedures on SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d528c-104">Azure Data Factory provides a fully managed method for orchestrating the transfer of data and execution of stored procedures on SQL Data Warehouse.</span></span>  <span data-ttu-id="d528c-105">This will allow you to more easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d528c-105">This will allow you to more easily set-up and schedule complex Extract Transform and Load (ETL) procedures with SQL Data Warehouse.</span></span> <span data-ttu-id="d528c-106">For a more complete overview of Azure Data Factory, see the [Azure Data Factory documentation][Azure Data Factory documentation].</span><span class="sxs-lookup"><span data-stu-id="d528c-106">For a more complete overview of Azure Data Factory, see the [Azure Data Factory documentation][Azure Data Factory documentation].</span></span>

## <a name="data-movement"></a><span data-ttu-id="d528c-107">Data Movement</span><span class="sxs-lookup"><span data-stu-id="d528c-107">Data Movement</span></span>
<span data-ttu-id="d528c-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span><span class="sxs-lookup"><span data-stu-id="d528c-108">Azure Data Factory enables data movement between both on-premises sources and different Azure services.</span></span>  <span data-ttu-id="d528c-109">Overall, current integration with Azure Data Factory supports data movement to and from the following locations:</span><span class="sxs-lookup"><span data-stu-id="d528c-109">Overall, current integration with Azure Data Factory supports data movement to and from the following locations:</span></span>

* <span data-ttu-id="d528c-110">Azure blob storage</span><span class="sxs-lookup"><span data-stu-id="d528c-110">Azure blob storage</span></span>
* <span data-ttu-id="d528c-111">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="d528c-111">Azure SQL Database</span></span>
* <span data-ttu-id="d528c-112">On-premises SQL Server</span><span class="sxs-lookup"><span data-stu-id="d528c-112">On-premises SQL Server</span></span>
* <span data-ttu-id="d528c-113">SQL Server on IaaS</span><span class="sxs-lookup"><span data-stu-id="d528c-113">SQL Server on IaaS</span></span>

<span data-ttu-id="d528c-114">For information on how to set up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span><span class="sxs-lookup"><span data-stu-id="d528c-114">For information on how to set up a data copy activity see [Copy data with Azure Data Factory][Copy data with Azure Data Factory]</span></span>

## <a name="stored-procedures"></a><span data-ttu-id="d528c-115">Stored Procedures</span><span class="sxs-lookup"><span data-stu-id="d528c-115">Stored Procedures</span></span>
 <span data-ttu-id="d528c-116">In the same way it can be used to schedule data transfer, Azure Data Factory can also be used to orchestrate the execution of stored procedures.</span><span class="sxs-lookup"><span data-stu-id="d528c-116">In the same way it can be used to schedule data transfer, Azure Data Factory can also be used to orchestrate the execution of stored procedures.</span></span>  <span data-ttu-id="d528c-117">This allows more complex pipelines to be created and extends Azure Data Factory's ability to leverage the computational power of SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="d528c-117">This allows more complex pipelines to be created and extends Azure Data Factory's ability to leverage the computational power of SQL Data Warehouse.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d528c-118">Next steps</span><span class="sxs-lookup"><span data-stu-id="d528c-118">Next steps</span></span>
<span data-ttu-id="d528c-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span><span class="sxs-lookup"><span data-stu-id="d528c-119">For an overview of integration, see [SQL Data Warehouse integration overview][SQL Data Warehouse integration overview].</span></span>
<span data-ttu-id="d528c-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="d528c-120">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>

<!--Image references-->

<!--Article references-->

[Copy data with Azure Data Factory]: ../data-factory/data-factory-data-movement-activities.md
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md
[SQL Data Warehouse integration overview]: ./sql-data-warehouse-overview-integrate.md

<!--MSDN references-->

<!--Other Web references-->
[Azure Data Factory documentation]:https://azure.microsoft.com/documentation/services/data-factory/

