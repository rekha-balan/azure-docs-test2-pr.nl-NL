---
title: Azure API managment policy sample - Authorize request using external authorizer | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how authorize requests using external authorizer encapsulating a custom or legacy authentication/authorization logic.
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
ms.date: 06/06/2018
ms.author: apimpm
ms.openlocfilehash: 7d172a40f2aad65b595026fc656634060a1f7193
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868833"
---
# <a name="authorize-requests-using-external-authorizer"></a><span data-ttu-id="4214f-103">Authorize requests using external authorizer</span><span class="sxs-lookup"><span data-stu-id="4214f-103">Authorize requests using external authorizer</span></span>

<span data-ttu-id="4214f-104">This article shows an Azure API management policy sample that demonstrates how to secure API access by using an external authorizer encapsulating custom authentication/authorization logic.</span><span class="sxs-lookup"><span data-stu-id="4214f-104">This article shows an Azure API management policy sample that demonstrates how to secure API access by using an external authorizer encapsulating custom authentication/authorization logic.</span></span> <span data-ttu-id="4214f-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="4214f-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="4214f-106">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4214f-106">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="4214f-107">Policy</span><span class="sxs-lookup"><span data-stu-id="4214f-107">Policy</span></span>

<span data-ttu-id="4214f-108">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="4214f-108">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Authorize requests using external authorizer.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="4214f-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="4214f-109">Next steps</span></span>

<span data-ttu-id="4214f-110">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="4214f-110">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="4214f-111">Access restrictions policies</span><span class="sxs-lookup"><span data-stu-id="4214f-111">Access restrictions policies</span></span>](../api-management-access-restriction-policies.md)
+ [<span data-ttu-id="4214f-112">Policy samples</span><span class="sxs-lookup"><span data-stu-id="4214f-112">Policy samples</span></span>](../policy-samples.md)