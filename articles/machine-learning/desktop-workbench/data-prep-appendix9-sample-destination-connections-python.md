---
title: Example destinations/outputs possible with Azure Machine Learning data preparation | Microsoft Docs
description: This document provides a set of examples of custom data destinations/outputs with Azure Machine Learning data preparation
services: machine-learning
author: euangMS
ms.author: euang
manager: lanceo
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: ''
ms.devlang: ''
ms.topic: article
ms.date: 02/01/2018
ms.openlocfilehash: 2173ff15906940b8628aba3615f31e3f7137e3e2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44968087"
---
# <a name="sample-of-destination-connections-python"></a>Sample of destination connections (Python) 
Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).


## <a name="write-to-excel"></a>Write to Excel 


Writing to Excel requires an additional library. Adding new libraries is documented in the extensibility overview. `openpyxl` is the library that you need to add.

Before you write to Excel, some other changes might be needed. Some of the data types that are used in data preparation are not supported in some destination formats. For example, if "Error" objects exist, they won't serialize correctly to Excel. Thus, before you attempt to write to Excel, you need a "Replace Error Values" transform, which removes errors from any columns.

If all of the previous work is complete, the following line writes the data table to a single sheet in an Excel document. Add a Transform DataFlow (Script) transform. Then enter the following code in an expression section.


### <a name="on-windows"></a>On Windows 
```python
df.to_excel('c:\dev\data\Output\Customer.xlsx', sheet_name='Sheet1')
```

### <a name="on-macosos-x"></a>On macOS/OS X ###
```python
df.to_excel('c:/dev/data/Output/Customer.xlsx', sheet_name='Sheet1')
```
