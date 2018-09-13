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
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: eb4579c2d94ae610d21b7221c0b410b07268d419
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44865100"
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="a0c78-103">Azure Data Factory - naming rules</span><span class="sxs-lookup"><span data-stu-id="a0c78-103">Azure Data Factory - naming rules</span></span>
> [!NOTE]
> <span data-ttu-id="a0c78-104">This article applies to version 1 of Data Factory.</span><span class="sxs-lookup"><span data-stu-id="a0c78-104">This article applies to version 1 of Data Factory.</span></span> <span data-ttu-id="a0c78-105">If you are using the current version of the Data Factory service, see [naming rules in Data Factory](../naming-rules.md).</span><span class="sxs-lookup"><span data-stu-id="a0c78-105">If you are using the current version of the Data Factory service, see [naming rules in Data Factory](../naming-rules.md).</span></span>

<span data-ttu-id="a0c78-106">The following table provides naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="a0c78-106">The following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="a0c78-107">Name</span><span class="sxs-lookup"><span data-stu-id="a0c78-107">Name</span></span> | <span data-ttu-id="a0c78-108">Name Uniqueness</span><span class="sxs-lookup"><span data-stu-id="a0c78-108">Name Uniqueness</span></span> | <span data-ttu-id="a0c78-109">Validation Checks</span><span class="sxs-lookup"><span data-stu-id="a0c78-109">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="a0c78-110">Data Factory</span><span class="sxs-lookup"><span data-stu-id="a0c78-110">Data Factory</span></span> |<span data-ttu-id="a0c78-111">Unique across Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c78-111">Unique across Microsoft Azure.</span></span> <span data-ttu-id="a0c78-112">Names are case-insensitive, that is, `MyDF` and `mydf` refer to the same data factory.</span><span class="sxs-lookup"><span data-stu-id="a0c78-112">Names are case-insensitive, that is, `MyDF` and `mydf` refer to the same data factory.</span></span> |<ul><li><span data-ttu-id="a0c78-113">Each data factory is tied to exactly one Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="a0c78-113">Each data factory is tied to exactly one Azure subscription.</span></span></li><li><span data-ttu-id="a0c78-114">Object names must start with a letter or a number, and can contain only letters, numbers, and the dash (-) character.</span><span class="sxs-lookup"><span data-stu-id="a0c78-114">Object names must start with a letter or a number, and can contain only letters, numbers, and the dash (-) character.</span></span></li><li><span data-ttu-id="a0c78-115">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span><span class="sxs-lookup"><span data-stu-id="a0c78-115">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="a0c78-116">Consecutive dashes are not permitted in container names.</span><span class="sxs-lookup"><span data-stu-id="a0c78-116">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="a0c78-117">Name can be 3-63 characters long.</span><span class="sxs-lookup"><span data-stu-id="a0c78-117">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="a0c78-118">Linked Services/Tables/Pipelines</span><span class="sxs-lookup"><span data-stu-id="a0c78-118">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="a0c78-119">Unique with in a data factory.</span><span class="sxs-lookup"><span data-stu-id="a0c78-119">Unique with in a data factory.</span></span> <span data-ttu-id="a0c78-120">Names are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="a0c78-120">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="a0c78-121">Maximum number of characters in a table name: 260.</span><span class="sxs-lookup"><span data-stu-id="a0c78-121">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="a0c78-122">Object names must start with a letter, number, or an underscore (_).</span><span class="sxs-lookup"><span data-stu-id="a0c78-122">Object names must start with a letter, number, or an underscore (_).</span></span></li><li><span data-ttu-id="a0c78-123">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”\*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="a0c78-123">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”\*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="a0c78-124">Resource Group</span><span class="sxs-lookup"><span data-stu-id="a0c78-124">Resource Group</span></span> |<span data-ttu-id="a0c78-125">Unique across Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="a0c78-125">Unique across Microsoft Azure.</span></span> <span data-ttu-id="a0c78-126">Names are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="a0c78-126">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="a0c78-127">Maximum number of characters: 1000.</span><span class="sxs-lookup"><span data-stu-id="a0c78-127">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="a0c78-128">Name can contain letters, digits, and the following characters: “-”, “_”, “,” and “.”</span><span class="sxs-lookup"><span data-stu-id="a0c78-128">Name can contain letters, digits, and the following characters: “-”, “_”, “,” and “.”</span></span></li></ul> |

