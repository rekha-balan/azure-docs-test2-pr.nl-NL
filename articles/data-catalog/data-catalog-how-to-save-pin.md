---
title: How to save searches and pin data assets | Microsoft Docs
description: How-to article highlighting capabilities in Azure Data Catalog for saving data sources and data assets for later reuse.
services: data-catalog
documentationcenter: ''
author: steelanddata
manager: NA
editor: ''
tags: ''
ms.assetid: 6bd00a81-820d-4b7c-91fa-ab09e575474c
ms.service: data-catalog
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-catalog
ms.date: 01/23/2017
ms.author: maroche
ms.openlocfilehash: be22fa576d4896239a6fed803f9b5d3fd023efc9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44564472"
---
# <a name="how-to-save-searches-and-pin-data-assets"></a>How to save searches and pin data assets
## <a name="introduction"></a>Introduction
Microsoft Azure Data Catalog provides capabilities for data source discovery. Users can quickly search and filter the catalog to locate data sources and understand their intended purpose, making it easier to find the right data for the job at hand.

But what about when users need to regularly work with the same data? What about when users regularly contribute their knowledge to the same data sources in the catalog? In these situations, having to repeatedly issue the same searches can be inefficient – this is where saved search and pinned data assets can help.

## <a name="saved-searches"></a>Saved searches
A saved search in Azure Data Catalog is a reusable, per-user search definition. Once a user has defined a search – including search terms, tags, and other filters – he can save it for later use. The saved search definition can then be re-run at a later date, to return any data assets that match its search criteria.

### <a name="creating-a-saved-search"></a>Creating a saved search
To create a saved search, first enter the search criteria to be reused. Then click the “Save” link in the “Current Search” box in the Azure Data Catalog portal.

 ![Select 'Save' to save the current search settings](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/01-save-option.png)

When prompted, enter a name for the saved search. Pick a name that is meaningful and descriptive of the data assets that will be returned by the search.

 ![Provide a name for the saved search](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/02-name.png)

### <a name="managing-saved-searches"></a>Managing saved searches
Once a user has saved one or more searches, a “Saved Searches” option will appear in the Azure Data Catalog portal under the “Current Search” box. When expanded, the complete list of saves searches will be displayed.

 ![List of saved searches](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/03-list.png)

Selecting a saved search from the list will cause the search to be executed.

Selecting the drop-down menu will provide a set of management options:

 ![Options for managing saved searches](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/04-managing.png)

Selecting “Rename” will prompt the user to enter a new name for the saved search. The search definition will not be changed.

Selecting “Delete” will prompt the user for confirmation, and will then remove the saved search from the user’s list.

Selecting “Save as Default” will mark the chosen saved search as the default search for the user. If the user performs an “empty” search from the Azure Data Catalog home page, the user’s default search will be executed. In addition, the search marked as default will appear at the top of the saved search list.

### <a name="organizational-saved-searches"></a>Organizational saved searches
Every user can save searches for their own use. Data Catalog administrators can also save searches for all users within the organization. When saving a search, administrators are presented with an option to share the saved search within the company. If this option is selected, the saved search will be included in the list of available searches for all users.

 ![Organizational saved searches](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/08-organizational-saved-search.png)

## <a name="pinned-data-assets"></a>Pinned data assets
Saved searches allow users to save and reuse search definitions; the data assets returned by the searches may change over time as the contents of the catalog change. Pinning data assets allows users to explicitly identify specific data assets to make them easier to access without needing to use a search.

Pinning a data asset is straightforward – users can simply click the “pin” icon for the data asset to add it to their pinned list. This icon appears in the corner of the asset tile in the tile view, and in the left-most column in the list view in the Azure Data Catalog portal.

![Pinning a data asset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/05-pinning.png)

Unpinning an asset is equally straightforward – users simply click the “pin” icon again to toggle the setting for the selected asset.

![Unpinning a data asset](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/06-unpinning.png)

## <a name="my-assets"></a>“My Assets”
The Azure Data Catalog portal home page includes a “My Assets” section that displays assets of interest to the current user. This section includes both pinned assets and saved searches.

!['My Assets' on the home page](https://docstestmedia1.blob.core.windows.net/azure-media/articles/data-catalog/media/data-catalog-how-to-save-pin/07-my-assets.png)

## <a name="summary"></a>Summary
Azure Data Catalog provides capabilities that make it easier for users to discover the data sources they need, so they can spend less time looking for data and more time working with it. Saved searches and pinned data assets build on these core capabilities so users can easily identify data sources with which they will work repeatedly.








