---
title: Data model compatibility level in Azure Analysis Services | Microsoft Docs
description: Understanding tabular data model compatibility level.
author: minewiskan
manager: kfile
ms.service: azure-analysis-services
ms.topic: conceptual
ms.date: 07/03/2018
ms.author: owend
ms.reviewer: minewiskan
ms.openlocfilehash: 17a75e86d5539427c8837b3077aacf85b4681ad6
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44965933"
---
# <a name="compatibility-level-for-analysis-services-tabular-models"></a><span data-ttu-id="1a46f-103">Compatibility level for Analysis Services tabular models</span><span class="sxs-lookup"><span data-stu-id="1a46f-103">Compatibility level for Analysis Services tabular models</span></span>

<span data-ttu-id="1a46f-104">*Compatibility level* refers to release-specific behaviors in the Analysis Services engine.</span><span class="sxs-lookup"><span data-stu-id="1a46f-104">*Compatibility level* refers to release-specific behaviors in the Analysis Services engine.</span></span> <span data-ttu-id="1a46f-105">Changes to the compatibility level typically coincide with major releases of SQL Server.</span><span class="sxs-lookup"><span data-stu-id="1a46f-105">Changes to the compatibility level typically coincide with major releases of SQL Server.</span></span> <span data-ttu-id="1a46f-106">These changes are also implemented in Azure Analysis Services to maintain parity between both platforms.</span><span class="sxs-lookup"><span data-stu-id="1a46f-106">These changes are also implemented in Azure Analysis Services to maintain parity between both platforms.</span></span> <span data-ttu-id="1a46f-107">Compatibility level changes also effect features available in your tabular models.</span><span class="sxs-lookup"><span data-stu-id="1a46f-107">Compatibility level changes also effect features available in your tabular models.</span></span> <span data-ttu-id="1a46f-108">For example, DirectQuery and tabular object metadata have different implementations depending on the compatibility level.</span><span class="sxs-lookup"><span data-stu-id="1a46f-108">For example, DirectQuery and tabular object metadata have different implementations depending on the compatibility level.</span></span> <span data-ttu-id="1a46f-109">Compatibility level is specified in the tabular model project in Visual Studio (SSDT).</span><span class="sxs-lookup"><span data-stu-id="1a46f-109">Compatibility level is specified in the tabular model project in Visual Studio (SSDT).</span></span> <span data-ttu-id="1a46f-110">Tabular models created in and imported from Power BI Desktop are at the 1400 compatibility level only.</span><span class="sxs-lookup"><span data-stu-id="1a46f-110">Tabular models created in and imported from Power BI Desktop are at the 1400 compatibility level only.</span></span>

<span data-ttu-id="1a46f-111">Azure Analysis Services supports tabular models at the 1200 and 1400 compatibility levels.</span><span class="sxs-lookup"><span data-stu-id="1a46f-111">Azure Analysis Services supports tabular models at the 1200 and 1400 compatibility levels.</span></span> 

<span data-ttu-id="1a46f-112">The latest compatibility level is 1400.</span><span class="sxs-lookup"><span data-stu-id="1a46f-112">The latest compatibility level is 1400.</span></span> <span data-ttu-id="1a46f-113">This level coincides with SQL Server 2017 Analysis Services.</span><span class="sxs-lookup"><span data-stu-id="1a46f-113">This level coincides with SQL Server 2017 Analysis Services.</span></span> <span data-ttu-id="1a46f-114">Major features in the 1400 compatibility level include:</span><span class="sxs-lookup"><span data-stu-id="1a46f-114">Major features in the 1400 compatibility level include:</span></span>

*  <span data-ttu-id="1a46f-115">New features for data connectivity and import with support for TOM APIs and TMSL scripting.</span><span class="sxs-lookup"><span data-stu-id="1a46f-115">New features for data connectivity and import with support for TOM APIs and TMSL scripting.</span></span> 
*  <span data-ttu-id="1a46f-116">Data transformation and data mashup capabilities by using Get Data and M expressions.</span><span class="sxs-lookup"><span data-stu-id="1a46f-116">Data transformation and data mashup capabilities by using Get Data and M expressions.</span></span>
*  <span data-ttu-id="1a46f-117">Measures support a Detail Rows property with a DAX expression.</span><span class="sxs-lookup"><span data-stu-id="1a46f-117">Measures support a Detail Rows property with a DAX expression.</span></span> <span data-ttu-id="1a46f-118">This property enables client tools like Microsoft Excel to drill down to detailed data from an aggregated report.</span><span class="sxs-lookup"><span data-stu-id="1a46f-118">This property enables client tools like Microsoft Excel to drill down to detailed data from an aggregated report.</span></span> <span data-ttu-id="1a46f-119">For example, when users view total sales for a region and month, they can view the associated order details.</span><span class="sxs-lookup"><span data-stu-id="1a46f-119">For example, when users view total sales for a region and month, they can view the associated order details.</span></span> 
*  <span data-ttu-id="1a46f-120">Object-level security for table and column names, in addition to the data within them.</span><span class="sxs-lookup"><span data-stu-id="1a46f-120">Object-level security for table and column names, in addition to the data within them.</span></span>
*  <span data-ttu-id="1a46f-121">Enhanced support for ragged hierarchies.</span><span class="sxs-lookup"><span data-stu-id="1a46f-121">Enhanced support for ragged hierarchies.</span></span>
*  <span data-ttu-id="1a46f-122">Performance and monitoring improvements.</span><span class="sxs-lookup"><span data-stu-id="1a46f-122">Performance and monitoring improvements.</span></span>
  
## <a name="set-compatibility-level"></a><span data-ttu-id="1a46f-123">Set compatibility level</span><span class="sxs-lookup"><span data-stu-id="1a46f-123">Set compatibility level</span></span> 
 <span data-ttu-id="1a46f-124">When creating a new tabular model project in SSDT, you can specify the compatibility level on the **Tabular model designer** dialog.</span><span class="sxs-lookup"><span data-stu-id="1a46f-124">When creating a new tabular model project in SSDT, you can specify the compatibility level on the **Tabular model designer** dialog.</span></span> 
  
 ![ssas_tabularproject_compat1200](./media/analysis-services-compat-level/aas-tabularproject-compat.png)  
  
 <span data-ttu-id="1a46f-126">If you select the **Do not show this message again** option, all subsequent projects use the compatibility level you specified as the default.</span><span class="sxs-lookup"><span data-stu-id="1a46f-126">If you select the **Do not show this message again** option, all subsequent projects use the compatibility level you specified as the default.</span></span> <span data-ttu-id="1a46f-127">You can change the default compatibility level in SSDT in **Tools** > **Options**.</span><span class="sxs-lookup"><span data-stu-id="1a46f-127">You can change the default compatibility level in SSDT in **Tools** > **Options**.</span></span>  
  
 <span data-ttu-id="1a46f-128">To upgrade an existing tabular model project in SSDT, set  the **Compatibility Level** property in the model **Properties** window.</span><span class="sxs-lookup"><span data-stu-id="1a46f-128">To upgrade an existing tabular model project in SSDT, set  the **Compatibility Level** property in the model **Properties** window.</span></span> <span data-ttu-id="1a46f-129">Keep in-mind, upgrading the compatibility level is irreversible.</span><span class="sxs-lookup"><span data-stu-id="1a46f-129">Keep in-mind, upgrading the compatibility level is irreversible.</span></span>
  
## <a name="check-compatibility-level-for-a-tabular-model-database-in-sql-server-management-studio"></a><span data-ttu-id="1a46f-130">Check compatibility level for a tabular model database in SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="1a46f-130">Check compatibility level for a tabular model database in SQL Server Management Studio</span></span> 
 <span data-ttu-id="1a46f-131">In SSMS, right-click the database name > **Properties** > **Compatibility Level**.</span><span class="sxs-lookup"><span data-stu-id="1a46f-131">In SSMS, right-click the database name > **Properties** > **Compatibility Level**.</span></span>  
  
## <a name="check-supported-compatibility-level-for-a-server-in-ssms"></a><span data-ttu-id="1a46f-132">Check supported compatibility level for a server in SSMS</span><span class="sxs-lookup"><span data-stu-id="1a46f-132">Check supported compatibility level for a server in SSMS</span></span>  
 <span data-ttu-id="1a46f-133">In SSMS, right-click the server name>  **Properties** > **Supported Compatibility Level**.</span><span class="sxs-lookup"><span data-stu-id="1a46f-133">In SSMS, right-click the server name>  **Properties** > **Supported Compatibility Level**.</span></span>  
  
 <span data-ttu-id="1a46f-134">This property specifies the highest compatibility level of a database that will run on the server (excluding preview).</span><span class="sxs-lookup"><span data-stu-id="1a46f-134">This property specifies the highest compatibility level of a database that will run on the server (excluding preview).</span></span> <span data-ttu-id="1a46f-135">The supported compatibility level cannot be changed.</span><span class="sxs-lookup"><span data-stu-id="1a46f-135">The supported compatibility level cannot be changed.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1a46f-136">Next steps</span><span class="sxs-lookup"><span data-stu-id="1a46f-136">Next steps</span></span>
  <span data-ttu-id="1a46f-137">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span><span class="sxs-lookup"><span data-stu-id="1a46f-137">[Create a model in Azure portal](analysis-services-create-model-portal.md) </span></span>  
  [<span data-ttu-id="1a46f-138">Manage Analysis Services</span><span class="sxs-lookup"><span data-stu-id="1a46f-138">Manage Analysis Services</span></span>](analysis-services-manage.md)  
