---
title: Azure API managment policy sample - Set response cache duration | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to set response cache duration using maxAge value in Cache-Control header sent by the backend..
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
ms.openlocfilehash: 8f7126f5cd6bf6f142c603e4b1baee4a6c20dea2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967667"
---
# <a name="set-response-cache-duration"></a><span data-ttu-id="25dad-103">Set response cache duration</span><span class="sxs-lookup"><span data-stu-id="25dad-103">Set response cache duration</span></span>

<span data-ttu-id="25dad-104">This article shows an Azure API management policy sample that demonstrates how to set response cache duration using maxAge value in Cache-Control header sent by the backend.</span><span class="sxs-lookup"><span data-stu-id="25dad-104">This article shows an Azure API management policy sample that demonstrates how to set response cache duration using maxAge value in Cache-Control header sent by the backend.</span></span> <span data-ttu-id="25dad-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="25dad-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="25dad-106">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="25dad-106">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="25dad-107">Policy</span><span class="sxs-lookup"><span data-stu-id="25dad-107">Policy</span></span>

<span data-ttu-id="25dad-108">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="25dad-108">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Set cache duration using response cache control header.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="25dad-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="25dad-109">Next steps</span></span>

<span data-ttu-id="25dad-110">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="25dad-110">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="25dad-111">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="25dad-111">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="25dad-112">Policy samples</span><span class="sxs-lookup"><span data-stu-id="25dad-112">Policy samples</span></span>](../policy-samples.md)

