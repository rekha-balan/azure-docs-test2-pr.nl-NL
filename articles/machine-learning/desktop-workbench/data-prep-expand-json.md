---
title: Expand JSON Transformation using Azure Machine Learning Workbench
description: The reference document for the 'Expand JSON' transform
services: machine-learning
author: ranvijaykumar
ms.author: ranku
manager: mwinkle
ms.reviewer: jmartens, jasonwhowell, mldocs
ms.service: machine-learning
ms.component: core
ms.workload: data-services
ms.custom: mvc, reference
ms.topic: article
ms.date: 09/14/2017
ms.openlocfilehash: dbda4b7b6d82e8cf1e89dc78ce82efbac08b9933
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864966"
---
# <a name="expand-json-transformation"></a><span data-ttu-id="fff35-103">Expand JSON transformation</span><span class="sxs-lookup"><span data-stu-id="fff35-103">Expand JSON transformation</span></span>
<span data-ttu-id="fff35-104">The **Expand JSON** transform enables users to expand an existing column that contains valid JSON text into multiple columns.</span><span class="sxs-lookup"><span data-stu-id="fff35-104">The **Expand JSON** transform enables users to expand an existing column that contains valid JSON text into multiple columns.</span></span>

## <a name="how-to-perform-this-transformation"></a><span data-ttu-id="fff35-105">How to perform this transformation</span><span class="sxs-lookup"><span data-stu-id="fff35-105">How to perform this transformation</span></span>

<span data-ttu-id="fff35-106">Follow these steps to perform this transform:</span><span class="sxs-lookup"><span data-stu-id="fff35-106">Follow these steps to perform this transform:</span></span>
1. <span data-ttu-id="fff35-107">Select the source column that contains JSON text.</span><span class="sxs-lookup"><span data-stu-id="fff35-107">Select the source column that contains JSON text.</span></span>
2. <span data-ttu-id="fff35-108">Select **Expand JSON** from the **Transforms** menu.</span><span class="sxs-lookup"><span data-stu-id="fff35-108">Select **Expand JSON** from the **Transforms** menu.</span></span> <span data-ttu-id="fff35-109">Or, Right click on the header of the source column and select **Expand JSON** from the context menu.</span><span class="sxs-lookup"><span data-stu-id="fff35-109">Or, Right click on the header of the source column and select **Expand JSON** from the context menu.</span></span> 
3. <span data-ttu-id="fff35-110">Click **OK**.</span><span class="sxs-lookup"><span data-stu-id="fff35-110">Click **OK**.</span></span> 
 
<span data-ttu-id="fff35-111">New columns are added next to the source column.</span><span class="sxs-lookup"><span data-stu-id="fff35-111">New columns are added next to the source column.</span></span> <span data-ttu-id="fff35-112">These columns contain properties from the next level of hierarchy in the JSON text.</span><span class="sxs-lookup"><span data-stu-id="fff35-112">These columns contain properties from the next level of hierarchy in the JSON text.</span></span> <span data-ttu-id="fff35-113">Property Key, if present, is used to create the name of the corresponding column.</span><span class="sxs-lookup"><span data-stu-id="fff35-113">Property Key, if present, is used to create the name of the corresponding column.</span></span> <span data-ttu-id="fff35-114">Nested properties are preserved as JSON text that user can iteratively expand or discard as needed.</span><span class="sxs-lookup"><span data-stu-id="fff35-114">Nested properties are preserved as JSON text that user can iteratively expand or discard as needed.</span></span>

## <a name="examples"></a><span data-ttu-id="fff35-115">Examples</span><span class="sxs-lookup"><span data-stu-id="fff35-115">Examples</span></span>

<span data-ttu-id="fff35-116">The source columnn *Customer* is expanded into two columns *Customer.Name* and *Customer.Phone*.</span><span class="sxs-lookup"><span data-stu-id="fff35-116">The source columnn *Customer* is expanded into two columns *Customer.Name* and *Customer.Phone*.</span></span>

| <span data-ttu-id="fff35-117">Customer</span><span class="sxs-lookup"><span data-stu-id="fff35-117">Customer</span></span>                                                | <span data-ttu-id="fff35-118">Customer.Name</span><span class="sxs-lookup"><span data-stu-id="fff35-118">Customer.Name</span></span>   | <span data-ttu-id="fff35-119">Customer.Phone</span><span class="sxs-lookup"><span data-stu-id="fff35-119">Customer.Phone</span></span> |
|---------------------------------------------------------|-----------------|----------------|
| <span data-ttu-id="fff35-120">{ "Name" : "Carrie Dodson", "Phone" : "123-4567-890"}</span><span class="sxs-lookup"><span data-stu-id="fff35-120">{ "Name" : "Carrie Dodson", "Phone" : "123-4567-890"}</span></span>   | <span data-ttu-id="fff35-121">Carrie Dodson</span><span class="sxs-lookup"><span data-stu-id="fff35-121">Carrie Dodson</span></span>   | <span data-ttu-id="fff35-122">123-4567-890</span><span class="sxs-lookup"><span data-stu-id="fff35-122">123-4567-890</span></span>   |
| <span data-ttu-id="fff35-123">{ "Name" : "Leonard Robledo", "Phone" : "456-7890-123"}</span><span class="sxs-lookup"><span data-stu-id="fff35-123">{ "Name" : "Leonard Robledo", "Phone" : "456-7890-123"}</span></span> | <span data-ttu-id="fff35-124">Leonard Robledo</span><span class="sxs-lookup"><span data-stu-id="fff35-124">Leonard Robledo</span></span> | <span data-ttu-id="fff35-125">456-7890-123</span><span class="sxs-lookup"><span data-stu-id="fff35-125">456-7890-123</span></span>   |

