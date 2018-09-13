---
title: Rules for naming Azure Data Factory entities | Microsoft Docs
description: Describes naming rules for Data Factory entities.
services: data-factory
documentationcenter: ''
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/24/2017
ms.author: shlo
ms.openlocfilehash: 57c0cb70abeee6b23b2e164877ee8a9bd628e504
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44562882"
---
# <a name="azure-data-factory---naming-rules"></a><span data-ttu-id="22b3a-103">Azure Data Factory - naming rules</span><span class="sxs-lookup"><span data-stu-id="22b3a-103">Azure Data Factory - naming rules</span></span>
<span data-ttu-id="22b3a-104">The following table provides naming rules for Data Factory artifacts.</span><span class="sxs-lookup"><span data-stu-id="22b3a-104">The following table provides naming rules for Data Factory artifacts.</span></span>

| <span data-ttu-id="22b3a-105">Name</span><span class="sxs-lookup"><span data-stu-id="22b3a-105">Name</span></span> | <span data-ttu-id="22b3a-106">Name Uniqueness</span><span class="sxs-lookup"><span data-stu-id="22b3a-106">Name Uniqueness</span></span> | <span data-ttu-id="22b3a-107">Validation Checks</span><span class="sxs-lookup"><span data-stu-id="22b3a-107">Validation Checks</span></span> |
|:--- |:--- |:--- |
| <span data-ttu-id="22b3a-108">Data Factory</span><span class="sxs-lookup"><span data-stu-id="22b3a-108">Data Factory</span></span> |<span data-ttu-id="22b3a-109">Unique across Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="22b3a-109">Unique across Microsoft Azure.</span></span> <span data-ttu-id="22b3a-110">Names are case-insensitive, that is, MyDF and mydf refer to the same data factory.</span><span class="sxs-lookup"><span data-stu-id="22b3a-110">Names are case-insensitive, that is, MyDF and mydf refer to the same data factory.</span></span> |<ul><li><span data-ttu-id="22b3a-111">Each data factory is tied to exactly one Azure subscription.</span><span class="sxs-lookup"><span data-stu-id="22b3a-111">Each data factory is tied to exactly one Azure subscription.</span></span></li><li><span data-ttu-id="22b3a-112">Object names must start with a letter or a number, and can contain only letters, numbers, and the dash (-) character.</span><span class="sxs-lookup"><span data-stu-id="22b3a-112">Object names must start with a letter or a number, and can contain only letters, numbers, and the dash (-) character.</span></span></li><li><span data-ttu-id="22b3a-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span><span class="sxs-lookup"><span data-stu-id="22b3a-113">Every dash (-) character must be immediately preceded and followed by a letter or a number.</span></span> <span data-ttu-id="22b3a-114">Consecutive dashes are not permitted in container names.</span><span class="sxs-lookup"><span data-stu-id="22b3a-114">Consecutive dashes are not permitted in container names.</span></span></li><li><span data-ttu-id="22b3a-115">Name can be 3-63 characters long.</span><span class="sxs-lookup"><span data-stu-id="22b3a-115">Name can be 3-63 characters long.</span></span></li></ul> |
| <span data-ttu-id="22b3a-116">Linked Services/Tables/Pipelines</span><span class="sxs-lookup"><span data-stu-id="22b3a-116">Linked Services/Tables/Pipelines</span></span> |<span data-ttu-id="22b3a-117">Unique with in a data factory.</span><span class="sxs-lookup"><span data-stu-id="22b3a-117">Unique with in a data factory.</span></span> <span data-ttu-id="22b3a-118">Names are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="22b3a-118">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="22b3a-119">Maximum number of characters in a table name: 260.</span><span class="sxs-lookup"><span data-stu-id="22b3a-119">Maximum number of characters in a table name: 260.</span></span></li><li><span data-ttu-id="22b3a-120">Object names must start with a letter number, or an underscore (_).</span><span class="sxs-lookup"><span data-stu-id="22b3a-120">Object names must start with a letter number, or an underscore (_).</span></span></li><li><span data-ttu-id="22b3a-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”\*”,”%”,”&”,”:”,”\\”</span><span class="sxs-lookup"><span data-stu-id="22b3a-121">Following characters are not allowed: “.”, “+”, “?”, “/”, “<”, ”>”,”\*”,”%”,”&”,”:”,”\\”</span></span></li></ul> |
| <span data-ttu-id="22b3a-122">Resource Group</span><span class="sxs-lookup"><span data-stu-id="22b3a-122">Resource Group</span></span> |<span data-ttu-id="22b3a-123">Unique across Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="22b3a-123">Unique across Microsoft Azure.</span></span> <span data-ttu-id="22b3a-124">Names are case-insensitive.</span><span class="sxs-lookup"><span data-stu-id="22b3a-124">Names are case-insensitive.</span></span> |<ul><li><span data-ttu-id="22b3a-125">Maximum number of characters: 1000.</span><span class="sxs-lookup"><span data-stu-id="22b3a-125">Maximum number of characters: 1000.</span></span></li><li><span data-ttu-id="22b3a-126">Name can contain letters, digits, and the following characters: “-”, “_”, “,” and “.”.</span><span class="sxs-lookup"><span data-stu-id="22b3a-126">Name can contain letters, digits, and the following characters: “-”, “_”, “,” and “.”.</span></span></li></ul> |

