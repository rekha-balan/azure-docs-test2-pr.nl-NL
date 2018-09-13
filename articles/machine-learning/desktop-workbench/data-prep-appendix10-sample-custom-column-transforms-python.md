---
title: Sample Python for deriving new columns in Azure Machine Learning data preparation  | Microsoft Docs
description: This document provides Python code examples for creating new columns in Azure Machine Learning data preparation.
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
ms.openlocfilehash: d9f8bb20325ff15b6ba67253de5e66d1d1d8e643
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866317"
---
# <a name="sample-of-custom-column-transforms-python"></a>Sample of custom column transforms (Python) 
The name of this transform in the menu is **Add Column (Script)**.

Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).

## <a name="test-equivalence-and-replace-values"></a>Test equivalence and replace values 
If the value in Col1 is less than 4, then the new column should have a value of 1. If the value in Col1 is more than 4, the new column has the value 2. 

```python
    1 if row["Col1"] < 4 else 2
```
## <a name="current-date-and-time"></a>Current date and time 

```python
    datetime.datetime.now()
```
## <a name="typecasting"></a>Typecasting 
```python
    float(row["Col1"]) / float(row["Col2"] - 1)
```
## <a name="evaluate-for-nullness"></a>Evaluate for nullness 
If Col1 contains a null, then mark the new column as **Bad**. If not, mark it as **Good.** 

```python
    'Bad' if pd.isnull(row["Col1"]) else 'Good'
```
## <a name="new-computed-column"></a>New computed column 
```python
    np.log(row["Col1"])
```
## <a name="epoch-computation"></a>Epoch computation 
Number of seconds since the Unix Epoch (assuming Col1 is already a date): 
```python
    row["Col1"] - datetime.datetime.utcfromtimestamp(0)).total_seconds()
```

## <a name="hash-a-column-value-into-a-new-column"></a>Hash a column value into a new column
```python
    import hashlib
    hash(row["MyColumnToHashCol1"])

```




