---
title: Azure API managment policy sample - Implement X-CSRF pattern | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to implement X-CSRF pattern used by many APIs. This example is specific to SAP Gateway.
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
ms.openlocfilehash: 3a2067836a1488d117dced96f3935f2d1f8b1b48
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858068"
---
# <a name="implement-x-csrf-pattern"></a><span data-ttu-id="1d8c5-104">Implement X-CSRF pattern</span><span class="sxs-lookup"><span data-stu-id="1d8c5-104">Implement X-CSRF pattern</span></span>

<span data-ttu-id="1d8c5-105">This article shows an Azure API management policy sample that demonstrates how to implement X-CSRF pattern used by many APIs.</span><span class="sxs-lookup"><span data-stu-id="1d8c5-105">This article shows an Azure API management policy sample that demonstrates how to implement X-CSRF pattern used by many APIs.</span></span> <span data-ttu-id="1d8c5-106">This example is specific to SAP Gateway.</span><span class="sxs-lookup"><span data-stu-id="1d8c5-106">This example is specific to SAP Gateway.</span></span> <span data-ttu-id="1d8c5-107">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="1d8c5-107">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="1d8c5-108">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1d8c5-108">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="1d8c5-109">Policy</span><span class="sxs-lookup"><span data-stu-id="1d8c5-109">Policy</span></span>

<span data-ttu-id="1d8c5-110">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="1d8c5-110">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Get X-CSRF token from SAP gateway using send request.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="1d8c5-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="1d8c5-111">Next steps</span></span>

<span data-ttu-id="1d8c5-112">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="1d8c5-112">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="1d8c5-113">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="1d8c5-113">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="1d8c5-114">Policy samples</span><span class="sxs-lookup"><span data-stu-id="1d8c5-114">Policy samples</span></span>](../policy-samples.md)

