---
title: Azure API managment policy sample - Add a header containing a correlation id | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to add a header containing a correlation id to the inbound request.
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
ms.openlocfilehash: 68f42124369194124ae1f8ebb93834a5be4e0128
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857715"
---
# <a name="add-a-header-containing-a-correlation-id"></a><span data-ttu-id="70ff1-103">Add a header containing a correlation id</span><span class="sxs-lookup"><span data-stu-id="70ff1-103">Add a header containing a correlation id</span></span>

<span data-ttu-id="70ff1-104">This article shows an Azure API management policy sample that demonstrates how to add a header containing a correlation id to the inbound request.</span><span class="sxs-lookup"><span data-stu-id="70ff1-104">This article shows an Azure API management policy sample that demonstrates how to add a header containing a correlation id to the inbound request.</span></span> <span data-ttu-id="70ff1-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="70ff1-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="70ff1-106">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="70ff1-106">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="70ff1-107">Policy</span><span class="sxs-lookup"><span data-stu-id="70ff1-107">Policy</span></span>

<span data-ttu-id="70ff1-108">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="70ff1-108">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Add correlation id to inbound request.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="70ff1-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="70ff1-109">Next steps</span></span>

<span data-ttu-id="70ff1-110">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="70ff1-110">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="70ff1-111">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="70ff1-111">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="70ff1-112">Policy samples</span><span class="sxs-lookup"><span data-stu-id="70ff1-112">Policy samples</span></span>](../policy-samples.md)

