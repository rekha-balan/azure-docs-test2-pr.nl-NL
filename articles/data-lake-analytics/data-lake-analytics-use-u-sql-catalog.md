---
title: Introduce Azure Data Lake Analytics U-SQL catalog | Microsoft Docs
description: Introduce Azure Data Lake Analytics U-SQL catalog
services: data-lake-analytics
documentationcenter: ''
author: edmacauley
manager: jhubbard
editor: cgronlun
ms.assetid: 55fef96f-e941-4d09-af5e-dd7c88c502b2
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/05/2016
ms.author: edmaca
ms.openlocfilehash: d5ad3616c23e5e1dfd0833841bb89b65354a39ec
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44550961"
---
# <a name="use-azure-data-lake-analytics-u-sql-catalog"></a><span data-ttu-id="3990e-103">Use Azure Data Lake Analytics (U-SQL) catalog</span><span class="sxs-lookup"><span data-stu-id="3990e-103">Use Azure Data Lake Analytics (U-SQL) catalog</span></span>
<span data-ttu-id="3990e-104">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="3990e-104">The U-SQL catalog is used to structure data and code so they can be shared by U-SQL scripts.</span></span> <span data-ttu-id="3990e-105">The catalog enables the highest performance possible with data in Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="3990e-105">The catalog enables the highest performance possible with data in Azure Data Lake.</span></span>

<span data-ttu-id="3990e-106">Each Azure Data Lake Analytics account has exactly one U-SQL Catalog associated with it.</span><span class="sxs-lookup"><span data-stu-id="3990e-106">Each Azure Data Lake Analytics account has exactly one U-SQL Catalog associated with it.</span></span> <span data-ttu-id="3990e-107">You cannot delete the U-SQL Catalog.</span><span class="sxs-lookup"><span data-stu-id="3990e-107">You cannot delete the U-SQL Catalog.</span></span> <span data-ttu-id="3990e-108">Currently U-SQL Catalogs cannot be shared between Data Lake Store accounts.</span><span class="sxs-lookup"><span data-stu-id="3990e-108">Currently U-SQL Catalogs cannot be shared between Data Lake Store accounts.</span></span>

<span data-ttu-id="3990e-109">Each U-SQL Catalog contains a database called **Master**.</span><span class="sxs-lookup"><span data-stu-id="3990e-109">Each U-SQL Catalog contains a database called **Master**.</span></span> <span data-ttu-id="3990e-110">The Master Database cannot be deleted.</span><span class="sxs-lookup"><span data-stu-id="3990e-110">The Master Database cannot be deleted.</span></span>  <span data-ttu-id="3990e-111">Each U-SQL Catalog can contain more additional databases.</span><span class="sxs-lookup"><span data-stu-id="3990e-111">Each U-SQL Catalog can contain more additional databases.</span></span>

<span data-ttu-id="3990e-112">U-SQL database contains:</span><span class="sxs-lookup"><span data-stu-id="3990e-112">U-SQL database contains:</span></span>

* <span data-ttu-id="3990e-113">Assemblies – share .NET code among U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="3990e-113">Assemblies – share .NET code among U-SQL scripts.</span></span>
* <span data-ttu-id="3990e-114">Table-values functions – share U-SQL code among U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="3990e-114">Table-values functions – share U-SQL code among U-SQL scripts.</span></span>
* <span data-ttu-id="3990e-115">Tables – share data among U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="3990e-115">Tables – share data among U-SQL scripts.</span></span>
* <span data-ttu-id="3990e-116">Schemas - share table schemas among U-SQL scripts.</span><span class="sxs-lookup"><span data-stu-id="3990e-116">Schemas - share table schemas among U-SQL scripts.</span></span>

## <a name="manage-catalogs"></a><span data-ttu-id="3990e-117">Manage catalogs</span><span class="sxs-lookup"><span data-stu-id="3990e-117">Manage catalogs</span></span>
<span data-ttu-id="3990e-118">Each Azure Data Lake Analytics account has a default Azure Data Lake Store account associated with it.</span><span class="sxs-lookup"><span data-stu-id="3990e-118">Each Azure Data Lake Analytics account has a default Azure Data Lake Store account associated with it.</span></span> <span data-ttu-id="3990e-119">This Data Lake Store account is referred as the default Data Lake Store account.</span><span class="sxs-lookup"><span data-stu-id="3990e-119">This Data Lake Store account is referred as the default Data Lake Store account.</span></span> <span data-ttu-id="3990e-120">U-SQL catalog is stored in the default Data Lake Store account under the /catalog folder.</span><span class="sxs-lookup"><span data-stu-id="3990e-120">U-SQL catalog is stored in the default Data Lake Store account under the /catalog folder.</span></span> <span data-ttu-id="3990e-121">Do not delete any files in the /catalog folder.</span><span class="sxs-lookup"><span data-stu-id="3990e-121">Do not delete any files in the /catalog folder.</span></span>

### <a name="use-azure-portal"></a><span data-ttu-id="3990e-122">Use Azure portal</span><span class="sxs-lookup"><span data-stu-id="3990e-122">Use Azure portal</span></span>
<span data-ttu-id="3990e-123">See [Manage Data Lake Analytics using portal](data-lake-analytics-manage-use-portal.md#view-u-sql-catalog)</span><span class="sxs-lookup"><span data-stu-id="3990e-123">See [Manage Data Lake Analytics using portal](data-lake-analytics-manage-use-portal.md#view-u-sql-catalog)</span></span>

### <a name="use-data-lake-tools-for-visual-studio"></a><span data-ttu-id="3990e-124">Use Data Lake Tools for Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="3990e-124">Use Data Lake Tools for Visual Studio.</span></span>
<span data-ttu-id="3990e-125">You can use Data Lake Tools for Visual Studio to manage the catalog.</span><span class="sxs-lookup"><span data-stu-id="3990e-125">You can use Data Lake Tools for Visual Studio to manage the catalog.</span></span>  <span data-ttu-id="3990e-126">For more information about the tools, see [Using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="3990e-126">For more information about the tools, see [Using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

<span data-ttu-id="3990e-127">**To manage the catalog**</span><span class="sxs-lookup"><span data-stu-id="3990e-127">**To manage the catalog**</span></span>

1. <span data-ttu-id="3990e-128">Open Visual Studio, and connect to azure.</span><span class="sxs-lookup"><span data-stu-id="3990e-128">Open Visual Studio, and connect to azure.</span></span> <span data-ttu-id="3990e-129">For the instructions, see [Connect to Azure](data-lake-analytics-data-lake-tools-get-started.md#connect-to-azure).</span><span class="sxs-lookup"><span data-stu-id="3990e-129">For the instructions, see [Connect to Azure](data-lake-analytics-data-lake-tools-get-started.md#connect-to-azure).</span></span>
2. <span data-ttu-id="3990e-130">Open **Server Explorer** by press **CTRL+ALT+S**.</span><span class="sxs-lookup"><span data-stu-id="3990e-130">Open **Server Explorer** by press **CTRL+ALT+S**.</span></span>
3. <span data-ttu-id="3990e-131">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Databases**, and then expand **master**.</span><span class="sxs-lookup"><span data-stu-id="3990e-131">From **Server Explorer**, expand **Azure**, expand **Data Lake Analytics**, expand your Data Lake Analytics account, expand **Databases**, and then expand **master**.</span></span>

    - <span data-ttu-id="3990e-132">To add a new Database, right-click **Database**, and then click **Create Database**.</span><span class="sxs-lookup"><span data-stu-id="3990e-132">To add a new Database, right-click **Database**, and then click **Create Database**.</span></span>
    - <span data-ttu-id="3990e-133">To add a new assembly, right-click **Assemblies**, and then click **Register Assembly**.</span><span class="sxs-lookup"><span data-stu-id="3990e-133">To add a new assembly, right-click **Assemblies**, and then click **Register Assembly**.</span></span>
    - <span data-ttu-id="3990e-134">To add a new schema, right-click **Schemas**, and then click **Create Schema**.</span><span class="sxs-lookup"><span data-stu-id="3990e-134">To add a new schema, right-click **Schemas**, and then click **Create Schema**.</span></span>
    - <span data-ttu-id="3990e-135">To add a new table, right-click **Tables**, and then click **Create Table**.</span><span class="sxs-lookup"><span data-stu-id="3990e-135">To add a new table, right-click **Tables**, and then click **Create Table**.</span></span>
    - <span data-ttu-id="3990e-136">To add a new table-valued function, see [Develop U-SQL user-defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span><span class="sxs-lookup"><span data-stu-id="3990e-136">To add a new table-valued function, see [Develop U-SQL user-defined operators for Data Lake Analytics jobs](data-lake-analytics-u-sql-develop-user-defined-operators.md).</span></span>


![Browse U-SQL Visual Studio catalogs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-lake-analytics/media/data-lake-analytics-use-u-sql-catalog/data-lake-analytics-browse-catalogs.png)

## <a name="see-also"></a><span data-ttu-id="3990e-138">See also</span><span class="sxs-lookup"><span data-stu-id="3990e-138">See also</span></span>
* <span data-ttu-id="3990e-139">Get started</span><span class="sxs-lookup"><span data-stu-id="3990e-139">Get started</span></span>
  
  * [<span data-ttu-id="3990e-140">Get started with Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="3990e-140">Get started with Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-get-started-portal.md)
  * [<span data-ttu-id="3990e-141">Get started with Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3990e-141">Get started with Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-get-started-powershell.md)
  * [<span data-ttu-id="3990e-142">Get started with Data Lake Analytics using Azure .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3990e-142">Get started with Data Lake Analytics using Azure .NET SDK</span></span>](data-lake-analytics-get-started-net-sdk.md)
  * [<span data-ttu-id="3990e-143">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span><span class="sxs-lookup"><span data-stu-id="3990e-143">Develop U-SQL scripts using Data Lake Tools for Visual Studio</span></span>](data-lake-analytics-data-lake-tools-get-started.md)
  * [<span data-ttu-id="3990e-144">Get started with Azure Data Lake Analytics U-SQL language</span><span class="sxs-lookup"><span data-stu-id="3990e-144">Get started with Azure Data Lake Analytics U-SQL language</span></span>](data-lake-analytics-u-sql-get-started.md)
* <span data-ttu-id="3990e-145">U-SQL & development</span><span class="sxs-lookup"><span data-stu-id="3990e-145">U-SQL & development</span></span>
  
  * [<span data-ttu-id="3990e-146">Get started with Azure Data Lake Analytics U-SQL language</span><span class="sxs-lookup"><span data-stu-id="3990e-146">Get started with Azure Data Lake Analytics U-SQL language</span></span>](data-lake-analytics-u-sql-get-started.md)
  * [<span data-ttu-id="3990e-147">Use U-SQL window functions for Azure Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="3990e-147">Use U-SQL window functions for Azure Data Lake Analytics jobs</span></span>](data-lake-analytics-use-window-functions.md)
  * [<span data-ttu-id="3990e-148">Develop U-SQL user-defined operators for Data Lake Analytics jobs</span><span class="sxs-lookup"><span data-stu-id="3990e-148">Develop U-SQL user-defined operators for Data Lake Analytics jobs</span></span>](data-lake-analytics-u-sql-develop-user-defined-operators.md)
* <span data-ttu-id="3990e-149">Management</span><span class="sxs-lookup"><span data-stu-id="3990e-149">Management</span></span>
  
  * [<span data-ttu-id="3990e-150">Manage Azure Data Lake Analytics using Azure portal</span><span class="sxs-lookup"><span data-stu-id="3990e-150">Manage Azure Data Lake Analytics using Azure portal</span></span>](data-lake-analytics-manage-use-portal.md)
  * [<span data-ttu-id="3990e-151">Manage Azure Data Lake Analytics using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3990e-151">Manage Azure Data Lake Analytics using Azure PowerShell</span></span>](data-lake-analytics-manage-use-powershell.md)
  * [<span data-ttu-id="3990e-152">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span><span class="sxs-lookup"><span data-stu-id="3990e-152">Monitor and troubleshoot Azure Data Lake Analytics jobs using Azure portal</span></span>](data-lake-analytics-monitor-and-troubleshoot-jobs-tutorial.md)
* <span data-ttu-id="3990e-153">End-to-end tutorial</span><span class="sxs-lookup"><span data-stu-id="3990e-153">End-to-end tutorial</span></span>
  
  * [<span data-ttu-id="3990e-154">Use Azure Data Lake Analytics interactive tutorials</span><span class="sxs-lookup"><span data-stu-id="3990e-154">Use Azure Data Lake Analytics interactive tutorials</span></span>](data-lake-analytics-use-interactive-tutorials.md)
  * [<span data-ttu-id="3990e-155">Analyze Website logs using Azure Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="3990e-155">Analyze Website logs using Azure Data Lake Analytics</span></span>](data-lake-analytics-analyze-weblogs.md)


