---
title: Azure API managment policy sample - Send request context information to the backend service | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to send request context information to the backend service.
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
ms.openlocfilehash: d6cfd6e63dbc8a56179197b2942c52d15539ae74
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44855907"
---
# <a name="send-request-context-information-to-the-backend-service"></a><span data-ttu-id="7ea2e-103">Send request context information to the backend service</span><span class="sxs-lookup"><span data-stu-id="7ea2e-103">Send request context information to the backend service</span></span>

<span data-ttu-id="7ea2e-104">This article shows an Azure API management policy sample that demonstrates how to send request context information to the backend service.</span><span class="sxs-lookup"><span data-stu-id="7ea2e-104">This article shows an Azure API management policy sample that demonstrates how to send request context information to the backend service.</span></span> <span data-ttu-id="7ea2e-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="7ea2e-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="7ea2e-106">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7ea2e-106">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="7ea2e-107">Policy</span><span class="sxs-lookup"><span data-stu-id="7ea2e-107">Policy</span></span>

<span data-ttu-id="7ea2e-108">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="7ea2e-108">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Send request context information to the backend service.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="7ea2e-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="7ea2e-109">Next steps</span></span>

<span data-ttu-id="7ea2e-110">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="7ea2e-110">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="7ea2e-111">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="7ea2e-111">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="7ea2e-112">Policy samples</span><span class="sxs-lookup"><span data-stu-id="7ea2e-112">Policy samples</span></span>](../policy-samples.md)

