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
# <a name="sample-of-custom-column-transforms-python"></a><span data-ttu-id="62450-103">Sample of custom column transforms (Python)</span><span class="sxs-lookup"><span data-stu-id="62450-103">Sample of custom column transforms (Python)</span></span> 
<span data-ttu-id="62450-104">The name of this transform in the menu is **Add Column (Script)**.</span><span class="sxs-lookup"><span data-stu-id="62450-104">The name of this transform in the menu is **Add Column (Script)**.</span></span>

<span data-ttu-id="62450-105">Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).</span><span class="sxs-lookup"><span data-stu-id="62450-105">Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).</span></span>

## <a name="test-equivalence-and-replace-values"></a><span data-ttu-id="62450-106">Test equivalence and replace values</span><span class="sxs-lookup"><span data-stu-id="62450-106">Test equivalence and replace values</span></span> 
<span data-ttu-id="62450-107">If the value in Col1 is less than 4, then the new column should have a value of 1.</span><span class="sxs-lookup"><span data-stu-id="62450-107">If the value in Col1 is less than 4, then the new column should have a value of 1.</span></span> <span data-ttu-id="62450-108">If the value in Col1 is more than 4, the new column has the value 2.</span><span class="sxs-lookup"><span data-stu-id="62450-108">If the value in Col1 is more than 4, the new column has the value 2.</span></span> 

```python
    1 if row["Col1"] < 4 else 2
```
## <a name="current-date-and-time"></a><span data-ttu-id="62450-109">Current date and time</span><span class="sxs-lookup"><span data-stu-id="62450-109">Current date and time</span></span> 

```python
    datetime.datetime.now()
```
## <a name="typecasting"></a><span data-ttu-id="62450-110">Typecasting</span><span class="sxs-lookup"><span data-stu-id="62450-110">Typecasting</span></span> 
```python
    float(row["Col1"]) / float(row["Col2"] - 1)
```
## <a name="evaluate-for-nullness"></a><span data-ttu-id="62450-111">Evaluate for nullness</span><span class="sxs-lookup"><span data-stu-id="62450-111">Evaluate for nullness</span></span> 
<span data-ttu-id="62450-112">If Col1 contains a null, then mark the new column as **Bad**.</span><span class="sxs-lookup"><span data-stu-id="62450-112">If Col1 contains a null, then mark the new column as **Bad**.</span></span> <span data-ttu-id="62450-113">If not, mark it as **Good.**</span><span class="sxs-lookup"><span data-stu-id="62450-113">If not, mark it as **Good.**</span></span> 

```python
    'Bad' if pd.isnull(row["Col1"]) else 'Good'
```
## <a name="new-computed-column"></a><span data-ttu-id="62450-114">New computed column</span><span class="sxs-lookup"><span data-stu-id="62450-114">New computed column</span></span> 
```python
    np.log(row["Col1"])
```
## <a name="epoch-computation"></a><span data-ttu-id="62450-115">Epoch computation</span><span class="sxs-lookup"><span data-stu-id="62450-115">Epoch computation</span></span> 
<span data-ttu-id="62450-116">Number of seconds since the Unix Epoch (assuming Col1 is already a date):</span><span class="sxs-lookup"><span data-stu-id="62450-116">Number of seconds since the Unix Epoch (assuming Col1 is already a date):</span></span> 
```python
    row["Col1"] - datetime.datetime.utcfromtimestamp(0)).total_seconds()
```

## <a name="hash-a-column-value-into-a-new-column"></a><span data-ttu-id="62450-117">Hash a column value into a new column</span><span class="sxs-lookup"><span data-stu-id="62450-117">Hash a column value into a new column</span></span>
```python
    import hashlib
    hash(row["MyColumnToHashCol1"])

```




