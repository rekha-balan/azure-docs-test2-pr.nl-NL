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
# <a name="how-to-view-related-data-assets-in-azure-data-catalog"></a>How to view related data assets in Azure Data Catalog?
Azure Data Catalog allows you to view data assets related to a selected data asset and view relationships between them. 

## <a name="supported-data-sources"></a>Supported data sources 
When you register data assets from the following data sources, Azure Data Catalog automatically registers metadata about join relationships between the selected data assets. 

- SQL Server
- Azure SQL Database
- MySQL
- Oracle

> [!NOTE]
> For Data Catalog to import relationship between two data assets, you must register both the assets at the same time. If you had added one of them separately, add it again and the other data asset to import relationship between them.

## <a name="view-related-data-assets"></a>View related data assets
To view data assets that are related to a selected dataset, use the **Relationships** tab as shown in the following image: 

![Azure Data Catalog - View related data assets](media\data-catalog-how-to-view-related-data-assets\relationships-tab.png)

In this example, there are two relationships for the selected **ProductSubcategory** data asset: 

- ProductSubcategoryID column of the Product table has a foreign key relationship with ProductSubcategoryID column of the selected ProductSubcategory table. 
- ProductCategoryID column of the ProductSubCategory table has a foreign key relationship with ProductCategoryID column of the selected ProductCategory table.

> [!NOTE]
> Notice the direction of the arrow in the relationships tree view.  

To see more details such as the fully qualified name of the column, move the mouse over and you see a popup similar to the following image: 

![Azure Data Catalog - Relationship popup](media\data-catalog-how-to-view-related-data-assets\relationship-popup.png)

To include relationships between assets that have already been registered, re-register those assets.

## <a name="next-steps"></a>Next steps
- [How to manage data assets](data-catalog-how-to-manage.md)