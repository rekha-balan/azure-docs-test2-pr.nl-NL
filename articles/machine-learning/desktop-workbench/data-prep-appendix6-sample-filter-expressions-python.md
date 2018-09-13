---
title: Example filter expressions possible with Azure Machine Learning data preparation  | Microsoft Docs
description: This document provides a set of examples of filter expressions possible with Azure Machine Learning data preparation
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
ms.openlocfilehash: a960197c89e1d051de0e9b8b73cbab231982cf52
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857393"
---
# <a name="sample-of-filter-expressions-python"></a>Sample of filter expressions (Python) 
Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).

## <a name="filter-with-equivalence-test"></a>Filter with equivalence test
Filter in only those rows where the value of (numeric) Col2 is greater than 4. 

```python
    row["Col2"] > 4
```

## <a name="filter-with-multiple-columns"></a>Filter with multiple columns 
Filter in only those rows where Col1 contains the value **Good** and Col2 contains the (numeric) value 1. 
```python
    row["Col1"] == 'Good' and row["Col2"] == 1
```

## <a name="test-filter-against-null"></a>Test filter against null
Filter in only those rows where Col1 has a null value. 
```python
    pd.isnull(row["Col1"])
```
