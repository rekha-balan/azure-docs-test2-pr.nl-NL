---
title: Azure API managment policy sample - Filter response content | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to filter data elements from the response payload based on the product associated with the request.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/13/2017
ms.author: apimpm
ms.openlocfilehash: af362ac51fb8b7d1689451d49f2ed831c5f9ee2e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868524"
---
# <a name="filter-response-content"></a><span data-ttu-id="c0129-103">Filter response content</span><span class="sxs-lookup"><span data-stu-id="c0129-103">Filter response content</span></span>

<span data-ttu-id="c0129-104">This article shows an Azure API management policy sample that demonstrates how to filter data elements from the response payload based on the product associated with the request.</span><span class="sxs-lookup"><span data-stu-id="c0129-104">This article shows an Azure API management policy sample that demonstrates how to filter data elements from the response payload based on the product associated with the request.</span></span> <span data-ttu-id="c0129-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c0129-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="c0129-106">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c0129-106">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="c0129-107">Policy</span><span class="sxs-lookup"><span data-stu-id="c0129-107">Policy</span></span>

<span data-ttu-id="c0129-108">Paste the code into the **outbound** block.</span><span class="sxs-lookup"><span data-stu-id="c0129-108">Paste the code into the **outbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Filter response content based on product name.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="c0129-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="c0129-109">Next steps</span></span>

<span data-ttu-id="c0129-110">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="c0129-110">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="c0129-111">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="c0129-111">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="c0129-112">Policy samples</span><span class="sxs-lookup"><span data-stu-id="c0129-112">Policy samples</span></span>](../policy-samples.md)

