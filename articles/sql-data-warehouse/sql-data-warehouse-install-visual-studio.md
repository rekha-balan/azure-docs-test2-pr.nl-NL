---
title: Install Visual Studio and SSDT for SQL Data Warehouse | Microsoft Docs
description: Install Visual Studio and SQL Server Development Tools (SSDT) for Azure SQL Data Warehouse
services: sql-data-warehouse
documentationcenter: NA
author: barbkess
manager: jhubbard
editor: ''
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: barbkess
ms.openlocfilehash: ae025ee2e6865b225efc5e225e261ac579a339aa
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564543"
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="2960b-103">Install Visual Studio and SSDT for SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="2960b-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="2960b-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="2960b-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="2960b-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span><span class="sxs-lookup"><span data-stu-id="2960b-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="2960b-106">Using Visual Studio with SSDT will allow you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span><span class="sxs-lookup"><span data-stu-id="2960b-106">Using Visual Studio with SSDT will allow you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="2960b-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span><span class="sxs-lookup"><span data-stu-id="2960b-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="2960b-108">This feature will be added in a future version.</span><span class="sxs-lookup"><span data-stu-id="2960b-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="2960b-109">Step 1: Install Visual Studio</span><span class="sxs-lookup"><span data-stu-id="2960b-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="2960b-110">Follow these links to download and install Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2960b-110">Follow these links to download and install Visual Studio.</span></span> <span data-ttu-id="2960b-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span><span class="sxs-lookup"><span data-stu-id="2960b-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span></span>

1. <span data-ttu-id="2960b-112">[Download Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="2960b-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="2960b-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span><span class="sxs-lookup"><span data-stu-id="2960b-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="2960b-114">Step 2: Install SSDT</span><span class="sxs-lookup"><span data-stu-id="2960b-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="2960b-115">To install SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span><span class="sxs-lookup"><span data-stu-id="2960b-115">To install SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="2960b-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span><span class="sxs-lookup"><span data-stu-id="2960b-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="2960b-117"> / *\*Updates**</span><span class="sxs-lookup"><span data-stu-id="2960b-117"> / *\*Updates**</span></span>
2. <span data-ttu-id="2960b-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span><span class="sxs-lookup"><span data-stu-id="2960b-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="2960b-119">If an update is not found, then you should have the latest version installed.</span><span class="sxs-lookup"><span data-stu-id="2960b-119">If an update is not found, then you should have the latest version installed.</span></span>  <span data-ttu-id="2960b-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span><span class="sxs-lookup"><span data-stu-id="2960b-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span></span>  <span data-ttu-id="2960b-121">The latest version of SSDT is 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="2960b-121">The latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="2960b-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span><span class="sxs-lookup"><span data-stu-id="2960b-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2960b-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="2960b-123">Next steps</span></span>
<span data-ttu-id="2960b-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="2960b-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Download Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
