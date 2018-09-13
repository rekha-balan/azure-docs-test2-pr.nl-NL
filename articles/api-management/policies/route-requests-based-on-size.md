---
title: Azure API managment policy sample - Route the request based on the size of its body | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to route requests based on the size of their bodies.
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
ms.openlocfilehash: a93e1d9fecea59ebb68c512b96c8381b5b1a9346
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867318"
---
# <a name="route-the-request-based-on-the-size-of-its-body"></a><span data-ttu-id="c1d34-103">Route the request based on the size of its body</span><span class="sxs-lookup"><span data-stu-id="c1d34-103">Route the request based on the size of its body</span></span>

<span data-ttu-id="c1d34-104">This article shows an Azure API management policy sample that demonstrates how to route requests based on the size of their bodies.</span><span class="sxs-lookup"><span data-stu-id="c1d34-104">This article shows an Azure API management policy sample that demonstrates how to route requests based on the size of their bodies.</span></span> <span data-ttu-id="c1d34-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="c1d34-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="c1d34-106">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="c1d34-106">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="c1d34-107">Policy</span><span class="sxs-lookup"><span data-stu-id="c1d34-107">Policy</span></span>

<span data-ttu-id="c1d34-108">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="c1d34-108">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Route requests based on size.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="c1d34-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="c1d34-109">Next steps</span></span>

<span data-ttu-id="c1d34-110">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="c1d34-110">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="c1d34-111">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="c1d34-111">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="c1d34-112">Policy samples</span><span class="sxs-lookup"><span data-stu-id="c1d34-112">Policy samples</span></span>](../policy-samples.md)

