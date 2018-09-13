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
# <a name="sample-of-filter-expressions-python"></a><span data-ttu-id="d1a93-103">Sample of filter expressions (Python)</span><span class="sxs-lookup"><span data-stu-id="d1a93-103">Sample of filter expressions (Python)</span></span> 
<span data-ttu-id="d1a93-104">Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d1a93-104">Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).</span></span>

## <a name="filter-with-equivalence-test"></a><span data-ttu-id="d1a93-105">Filter with equivalence test</span><span class="sxs-lookup"><span data-stu-id="d1a93-105">Filter with equivalence test</span></span>
<span data-ttu-id="d1a93-106">Filter in only those rows where the value of (numeric) Col2 is greater than 4.</span><span class="sxs-lookup"><span data-stu-id="d1a93-106">Filter in only those rows where the value of (numeric) Col2 is greater than 4.</span></span> 

```python
    row["Col2"] > 4
```

## <a name="filter-with-multiple-columns"></a><span data-ttu-id="d1a93-107">Filter with multiple columns</span><span class="sxs-lookup"><span data-stu-id="d1a93-107">Filter with multiple columns</span></span> 
<span data-ttu-id="d1a93-108">Filter in only those rows where Col1 contains the value **Good** and Col2 contains the (numeric) value 1.</span><span class="sxs-lookup"><span data-stu-id="d1a93-108">Filter in only those rows where Col1 contains the value **Good** and Col2 contains the (numeric) value 1.</span></span> 
```python
    row["Col1"] == 'Good' and row["Col2"] == 1
```

## <a name="test-filter-against-null"></a><span data-ttu-id="d1a93-109">Test filter against null</span><span class="sxs-lookup"><span data-stu-id="d1a93-109">Test filter against null</span></span>
<span data-ttu-id="d1a93-110">Filter in only those rows where Col1 has a null value.</span><span class="sxs-lookup"><span data-stu-id="d1a93-110">Filter in only those rows where Col1 has a null value.</span></span> 
```python
    pd.isnull(row["Col1"])
```
