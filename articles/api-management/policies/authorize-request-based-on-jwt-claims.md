---
title: Azure API managment policy sample - authorize acces based on JWT claims| Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to authorize access to specific HTTP methods on an API based on JWT claims.
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
ms.openlocfilehash: 78ea1b51dea0a65aede0e75e3a8c1d424689854e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866767"
---
# <a name="authorize-access-based-on-jwt-claims"></a><span data-ttu-id="d727d-103">Authorize access based on JWT claims</span><span class="sxs-lookup"><span data-stu-id="d727d-103">Authorize access based on JWT claims</span></span>

<span data-ttu-id="d727d-104">This article shows an Azure API management policy sample that demonstrates how to authorize access to specific HTTP methods on an API based on JWT claims.</span><span class="sxs-lookup"><span data-stu-id="d727d-104">This article shows an Azure API management policy sample that demonstrates how to authorize access to specific HTTP methods on an API based on JWT claims.</span></span> <span data-ttu-id="d727d-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d727d-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="d727d-106">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="d727d-106">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="d727d-107">Policy</span><span class="sxs-lookup"><span data-stu-id="d727d-107">Policy</span></span>

<span data-ttu-id="d727d-108">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="d727d-108">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Pre-authorize requests based on HTTP method with validate-jwt.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="d727d-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="d727d-109">Next steps</span></span>

<span data-ttu-id="d727d-110">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="d727d-110">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="d727d-111">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="d727d-111">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="d727d-112">Policy samples</span><span class="sxs-lookup"><span data-stu-id="d727d-112">Policy samples</span></span>](../policy-samples.md)

