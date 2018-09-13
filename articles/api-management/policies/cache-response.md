---
title: Azure API managment policy sample - Add capabilities to a backend service | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to add capabilities to a backend service. For example, accept a name of the place instead of latitude and longitude in a weather forecast API.
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
ms.openlocfilehash: a019eb4556dc7cde34d51af6858f576e8ea9abcf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871740"
---
# <a name="add-capabilities-to-a-backend-service"></a><span data-ttu-id="df4d7-104">Add capabilities to a backend service</span><span class="sxs-lookup"><span data-stu-id="df4d7-104">Add capabilities to a backend service</span></span>

<span data-ttu-id="df4d7-105">This article shows an Azure API management policy sample that demonstrates how to add capabilities to a backend service.</span><span class="sxs-lookup"><span data-stu-id="df4d7-105">This article shows an Azure API management policy sample that demonstrates how to add capabilities to a backend service.</span></span> <span data-ttu-id="df4d7-106">For example, accept a name of the place instead of latitude and longitude in a weather forecast API.</span><span class="sxs-lookup"><span data-stu-id="df4d7-106">For example, accept a name of the place instead of latitude and longitude in a weather forecast API.</span></span> <span data-ttu-id="df4d7-107">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="df4d7-107">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="df4d7-108">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="df4d7-108">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="df4d7-109">Policy</span><span class="sxs-lookup"><span data-stu-id="df4d7-109">Policy</span></span>

<span data-ttu-id="df4d7-110">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="df4d7-110">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Call out to an HTTP endpoint and cache the response.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="df4d7-111">Next steps</span><span class="sxs-lookup"><span data-stu-id="df4d7-111">Next steps</span></span>

<span data-ttu-id="df4d7-112">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="df4d7-112">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="df4d7-113">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="df4d7-113">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="df4d7-114">Policy samples</span><span class="sxs-lookup"><span data-stu-id="df4d7-114">Policy samples</span></span>](../policy-samples.md)

