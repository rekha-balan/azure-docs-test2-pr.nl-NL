---
title: How to view related data assets in Azure Data Catalog
description: This article explains how to view related data assets of a selected data asset in Azure Data Catalog.
services: data-catalog
author: steelanddata
ms.author: maroche
ms.service: data-catalog
ms.topic: conceptual
ms.date: 01/18/2018
ms.openlocfilehash: d680cc69d27681883014a414255ad0ea4d022cd4
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856620"
---
# <a name="how-to-view-related-data-assets-in-azure-data-catalog"></a><span data-ttu-id="e2370-103">How to view related data assets in Azure Data Catalog?</span><span class="sxs-lookup"><span data-stu-id="e2370-103">How to view related data assets in Azure Data Catalog?</span></span>
<span data-ttu-id="e2370-104">Azure Data Catalog allows you to view data assets related to a selected data asset and view relationships between them.</span><span class="sxs-lookup"><span data-stu-id="e2370-104">Azure Data Catalog allows you to view data assets related to a selected data asset and view relationships between them.</span></span> 

## <a name="supported-data-sources"></a><span data-ttu-id="e2370-105">Supported data sources</span><span class="sxs-lookup"><span data-stu-id="e2370-105">Supported data sources</span></span> 
<span data-ttu-id="e2370-106">When you register data assets from the following data sources, Azure Data Catalog automatically registers metadata about join relationships between the selected data assets.</span><span class="sxs-lookup"><span data-stu-id="e2370-106">When you register data assets from the following data sources, Azure Data Catalog automatically registers metadata about join relationships between the selected data assets.</span></span> 

- <span data-ttu-id="e2370-107">SQL Server</span><span class="sxs-lookup"><span data-stu-id="e2370-107">SQL Server</span></span>
- <span data-ttu-id="e2370-108">Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="e2370-108">Azure SQL Database</span></span>
- <span data-ttu-id="e2370-109">MySQL</span><span class="sxs-lookup"><span data-stu-id="e2370-109">MySQL</span></span>
- <span data-ttu-id="e2370-110">Oracle</span><span class="sxs-lookup"><span data-stu-id="e2370-110">Oracle</span></span>

> [!NOTE]
> <span data-ttu-id="e2370-111">For Data Catalog to import relationship between two data assets, you must register both the assets at the same time.</span><span class="sxs-lookup"><span data-stu-id="e2370-111">For Data Catalog to import relationship between two data assets, you must register both the assets at the same time.</span></span> <span data-ttu-id="e2370-112">If you had added one of them separately, add it again and the other data asset to import relationship between them.</span><span class="sxs-lookup"><span data-stu-id="e2370-112">If you had added one of them separately, add it again and the other data asset to import relationship between them.</span></span>

## <a name="view-related-data-assets"></a><span data-ttu-id="e2370-113">View related data assets</span><span class="sxs-lookup"><span data-stu-id="e2370-113">View related data assets</span></span>
<span data-ttu-id="e2370-114">To view data assets that are related to a selected dataset, use the **Relationships** tab as shown in the following image:</span><span class="sxs-lookup"><span data-stu-id="e2370-114">To view data assets that are related to a selected dataset, use the **Relationships** tab as shown in the following image:</span></span> 

![Azure Data Catalog - View related data assets](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

<span data-ttu-id="e2370-116">In this example, there are two relationships for the selected **ProductSubcategory** data asset:</span><span class="sxs-lookup"><span data-stu-id="e2370-116">In this example, there are two relationships for the selected **ProductSubcategory** data asset:</span></span> 

- <span data-ttu-id="e2370-117">ProductSubcategoryID column of the Product table has a foreign key relationship with ProductSubcategoryID column of the selected ProductSubcategory table.</span><span class="sxs-lookup"><span data-stu-id="e2370-117">ProductSubcategoryID column of the Product table has a foreign key relationship with ProductSubcategoryID column of the selected ProductSubcategory table.</span></span> 
- <span data-ttu-id="e2370-118">ProductCategoryID column of the ProductSubCategory table has a foreign key relationship with ProductCategoryID column of the selected ProductCategory table.</span><span class="sxs-lookup"><span data-stu-id="e2370-118">ProductCategoryID column of the ProductSubCategory table has a foreign key relationship with ProductCategoryID column of the selected ProductCategory table.</span></span>

> [!NOTE]
> <span data-ttu-id="e2370-119">Notice the direction of the arrow in the relationships tree view.</span><span class="sxs-lookup"><span data-stu-id="e2370-119">Notice the direction of the arrow in the relationships tree view.</span></span>  

<span data-ttu-id="e2370-120">To see more details such as the fully qualified name of the column, move the mouse over and you see a popup similar to the following image:</span><span class="sxs-lookup"><span data-stu-id="e2370-120">To see more details such as the fully qualified name of the column, move the mouse over and you see a popup similar to the following image:</span></span> 

![Azure Data Catalog - Relationship popup](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

<span data-ttu-id="e2370-122">To include relationships between assets that have already been registered, re-register those assets.</span><span class="sxs-lookup"><span data-stu-id="e2370-122">To include relationships between assets that have already been registered, re-register those assets.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e2370-123">Next steps</span><span class="sxs-lookup"><span data-stu-id="e2370-123">Next steps</span></span>
- [<span data-ttu-id="e2370-124">How to manage data assets</span><span class="sxs-lookup"><span data-stu-id="e2370-124">How to manage data assets</span></span>](data-catalog-how-to-manage.md)