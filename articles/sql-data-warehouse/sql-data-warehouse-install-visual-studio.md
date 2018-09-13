---
title: Install Visual Studio and SSDT for SQL Data Warehouse | Microsoft Docs
description: Install Visual Studio and SQL Server Development Tools (SSDT) for Azure SQL Data Warehouse
services: sql-data-warehouse
ms.custom: vs-azure
ms.workload: azure-vs
author: kavithaj
manager: craigg
ms.service: sql-data-warehouse
ms.topic: conceptual
ms.component: consume
ms.date: 04/17/2018
ms.author: kavithaj
ms.reviewer: igorstan
ms.openlocfilehash: ba84b64afb1d5ebcd5ec153787ddc7d0739bd8d8
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44797607"
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="8095e-103">Install Visual Studio and SSDT for SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8095e-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="8095e-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="8095e-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="8095e-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span><span class="sxs-lookup"><span data-stu-id="8095e-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="8095e-106">Using Visual Studio with SSDT allows you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures, and many more objects in your SQL Data Warehouse as well as run queries.</span><span class="sxs-lookup"><span data-stu-id="8095e-106">Using Visual Studio with SSDT allows you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures, and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="8095e-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span><span class="sxs-lookup"><span data-stu-id="8095e-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span> <span data-ttu-id="8095e-108">To receive periodic updates on this feature, please vote on [UserVoice].</span><span class="sxs-lookup"><span data-stu-id="8095e-108">To receive periodic updates on this feature, please vote on [UserVoice].</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="8095e-109">Step 1: Install Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8095e-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="8095e-110">Follow these links to download and install Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8095e-110">Follow these links to download and install Visual Studio.</span></span> <span data-ttu-id="8095e-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span><span class="sxs-lookup"><span data-stu-id="8095e-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span></span>

1. <span data-ttu-id="8095e-112">[Download Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="8095e-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="8095e-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span><span class="sxs-lookup"><span data-stu-id="8095e-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="8095e-114">Step 2: Install SSDT</span><span class="sxs-lookup"><span data-stu-id="8095e-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="8095e-115">To install SSDT for Visual Studio, first check for an SSDT update from within Visual Studio by following these steps.</span><span class="sxs-lookup"><span data-stu-id="8095e-115">To install SSDT for Visual Studio, first check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="8095e-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span><span class="sxs-lookup"><span data-stu-id="8095e-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="8095e-117"> / *\*Updates**</span><span class="sxs-lookup"><span data-stu-id="8095e-117"> / *\*Updates**</span></span>
2. <span data-ttu-id="8095e-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span><span class="sxs-lookup"><span data-stu-id="8095e-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="8095e-119">If an update is not found, then you should have the latest version installed.</span><span class="sxs-lookup"><span data-stu-id="8095e-119">If an update is not found, then you should have the latest version installed.</span></span>  <span data-ttu-id="8095e-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span><span class="sxs-lookup"><span data-stu-id="8095e-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span></span> <span data-ttu-id="8095e-121">The latest version of SSDT is 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="8095e-121">The latest version of SSDT is 14.0.60525.0.</span></span> <span data-ttu-id="8095e-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span><span class="sxs-lookup"><span data-stu-id="8095e-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8095e-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="8095e-123">Next steps</span></span>
<span data-ttu-id="8095e-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="8095e-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Download Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
[UserVoice]: https://feedback.azure.com/forums/307516-sql-data-warehouse/suggestions/13313247-database-project-from-visual-studio-to-support-azu
