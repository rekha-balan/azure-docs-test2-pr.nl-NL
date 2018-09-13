---
title: Rules for naming Azure Data Factory entities | Microsoft Docs
description: Describes naming rules for Data Factory entities.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: craigg
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 01/16/2018
ms.author: shlo
ms.openlocfilehash: cfab1a82c7da0ad596c9989e5a9f3ed800c58e4a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865918"
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="52c59-103">Azure Data Factory - naming rules</span><span class="sxs-lookup"><span data-stu-id="52c59-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="52c59-104">The following table provides naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="52c59-104">The following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="52c59-105">Name</span><span class="sxs-lookup"><span data-stu-id="52c59-105">Name</span></span> | <span data-ttu-id="52c59-106">Name Uniqueness</span><span class="sxs-lookup"><span data-stu-id="52c59-106">Name Uniqueness</span></span> | <span data-ttu-id="52c59-107">Validation Checks</span><span class="sxs-lookup"><span data-stu-id="52c59-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="52c59-108">Data Factory</span><span class="sxs-lookup"><span data-stu-id="52c59-108">Data Factory</span></span> |<span data-ttu-id="52c59-109">Unique across Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="52c59-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="52c59-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer to the same data factory.</span><span class="sxs-lookup"><span data-stu-id="52c59-110">Names are case-insensitive, that is, `MyDF` and `mydf` refer to the same data factory.</span></span> |<ul><li><span data-ttu-id="52c59-111">Each data factory is tied to exactly one Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="52c59-111">Each data factory is tied to exactly one Azure subscription.</span></span></li><li><span data-ttu-id="52c59-112">Object names must start with a letter or a number, and can contain only letters, numbers, and the dash (-) character.</span><span class="sxs-lookup"><span data-stu-id="52c59-112">Object names must start with a letter or a number, and can contain only letters, numbers, and the dash (-) character.</span></span></li><li><span data-ttu-id="52c59-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span><span class="sxs-lookup"><span data-stu-id="52c59-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="52c59-114">Consecutive dashes are not permitted in container names.</span><span class="sxs-lookup"><span data-stu-id="52c59-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="52c59-115">Name can be 3-63 characters long.</span><span class="sxs-lookup"><span data-stu-id="52c59-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="52c59-116">Linked Services/Datasets/Pipelines</span><span class="sxs-lookup"><span data-stu-id="52c59-116">Linked Services/Datasets/Pipelines</span></span> |<span data-ttu-id="52c59-117">Unique with in a data factory.</span><span class="sxs-lookup"><span data-stu-id="52c59-117">Unique with in a data factory.</span></span> <span data-ttu-id="52c59-118">Names are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="52c59-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="52c59-119">Object names must start with a letter, number, or an underscore (_).</span><span class="sxs-lookup"><span data-stu-id="52c59-119">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="52c59-120">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”\*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="52c59-120">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”\*”,”%”,”&”,”:”,”\\”</span></span></li><li><span data-ttu-id="52c59-121">Dashes ("-") are not allowed in the names of linked services and of datasets only.</span><span class="sxs-lookup"><span data-stu-id="52c59-121">Dashes ("-") are not allowed in the names of linked services and of datasets only.</span></span></li></ul>  |
| <span data-ttu-id="52c59-122">Resource Group</span><span class="sxs-lookup"><span data-stu-id="52c59-122">Resource Group</span></span> |<span data-ttu-id="52c59-123">Unique across Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="52c59-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="52c59-124">Names are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="52c59-124">Names are case-insensitive.</span></span> | <span data-ttu-id="52c59-125">For more info, see [Azure naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions#naming-rules-and-restrictions).</span><span class="sxs-lookup"><span data-stu-id="52c59-125">For more info, see [Azure naming rules and restrictions](https://docs.microsoft.com/azure/architecture/best-practices/naming-conventions#naming-rules-and-restrictions).</span></span> |

## <a name="next-steps"></a><span data-ttu-id="52c59-126">Next steps</span><span class="sxs-lookup"><span data-stu-id="52c59-126">Next steps</span></span>
<span data-ttu-id="52c59-127">Learn how to create data factories by following step-by-step instructions in [Quickstart: create a data factory](quickstart-create-data-factory-powershell.md) article.</span><span class="sxs-lookup"><span data-stu-id="52c59-127">Learn how to create data factories by following step-by-step instructions in [Quickstart: create a data factory](quickstart-create-data-factory-powershell.md) article.</span></span> 
