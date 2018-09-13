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
# <a name="sample-of-destination-connections-python"></a><span data-ttu-id="3aac2-103">Sample of destination connections (Python)</span><span class="sxs-lookup"><span data-stu-id="3aac2-103">Sample of destination connections (Python)</span></span> 
<span data-ttu-id="3aac2-104">Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).</span><span class="sxs-lookup"><span data-stu-id="3aac2-104">Before you read this appendix, read [Python extensibility overview](data-prep-python-extensibility-overview.md).</span></span>


## <a name="write-to-excel"></a><span data-ttu-id="3aac2-105">Write to Excel</span><span class="sxs-lookup"><span data-stu-id="3aac2-105">Write to Excel</span></span> 


<span data-ttu-id="3aac2-106">Writing to Excel requires an additional library.</span><span class="sxs-lookup"><span data-stu-id="3aac2-106">Writing to Excel requires an additional library.</span></span> <span data-ttu-id="3aac2-107">Adding new libraries is documented in the extensibility overview.</span><span class="sxs-lookup"><span data-stu-id="3aac2-107">Adding new libraries is documented in the extensibility overview.</span></span> <span data-ttu-id="3aac2-108">`openpyxl` is the library that you need to add.</span><span class="sxs-lookup"><span data-stu-id="3aac2-108">`openpyxl` is the library that you need to add.</span></span>

<span data-ttu-id="3aac2-109">Before you write to Excel, some other changes might be needed.</span><span class="sxs-lookup"><span data-stu-id="3aac2-109">Before you write to Excel, some other changes might be needed.</span></span> <span data-ttu-id="3aac2-110">Some of the data types that are used in data preparation are not supported in some destination formats.</span><span class="sxs-lookup"><span data-stu-id="3aac2-110">Some of the data types that are used in data preparation are not supported in some destination formats.</span></span> <span data-ttu-id="3aac2-111">For example, if "Error" objects exist, they won't serialize correctly to Excel.</span><span class="sxs-lookup"><span data-stu-id="3aac2-111">For example, if "Error" objects exist, they won't serialize correctly to Excel.</span></span> <span data-ttu-id="3aac2-112">Thus, before you attempt to write to Excel, you need a "Replace Error Values" transform, which removes errors from any columns.</span><span class="sxs-lookup"><span data-stu-id="3aac2-112">Thus, before you attempt to write to Excel, you need a "Replace Error Values" transform, which removes errors from any columns.</span></span>

<span data-ttu-id="3aac2-113">If all of the previous work is complete, the following line writes the data table to a single sheet in an Excel document.</span><span class="sxs-lookup"><span data-stu-id="3aac2-113">If all of the previous work is complete, the following line writes the data table to a single sheet in an Excel document.</span></span> <span data-ttu-id="3aac2-114">Add a Transform DataFlow (Script) transform.</span><span class="sxs-lookup"><span data-stu-id="3aac2-114">Add a Transform DataFlow (Script) transform.</span></span> <span data-ttu-id="3aac2-115">Then enter the following code in an expression section.</span><span class="sxs-lookup"><span data-stu-id="3aac2-115">Then enter the following code in an expression section.</span></span>


### <a name="on-windows"></a><span data-ttu-id="3aac2-116">On Windows</span><span class="sxs-lookup"><span data-stu-id="3aac2-116">On Windows</span></span> 
```python
df.to_excel('c:\dev\data\Output\Customer.xlsx', sheet_name='Sheet1')
```

### <a name="on-macosos-x"></a><span data-ttu-id="3aac2-117">On macOS/OS X</span><span class="sxs-lookup"><span data-stu-id="3aac2-117">On macOS/OS X</span></span> ###
```python
df.to_excel('c:/dev/data/Output/Customer.xlsx', sheet_name='Sheet1')
```
