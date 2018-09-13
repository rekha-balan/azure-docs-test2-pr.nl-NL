---
title: Azure API managment policy sample - Send errors to Stackify for logging | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to add an error logging policy to send errors to Stackify for logging..
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
ms.openlocfilehash: 5daf21cb55289c874d56910b1240e1433f3d55d0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869772"
---
# <a name="send-errors-to-stackify-for-logging"></a><span data-ttu-id="80455-103">Send errors to Stackify for logging</span><span class="sxs-lookup"><span data-stu-id="80455-103">Send errors to Stackify for logging</span></span>

<span data-ttu-id="80455-104">This article shows an Azure API management policy sample that demonstrates how to add an error logging policy to send errors to Stackify for logging.</span><span class="sxs-lookup"><span data-stu-id="80455-104">This article shows an Azure API management policy sample that demonstrates how to add an error logging policy to send errors to Stackify for logging.</span></span> <span data-ttu-id="80455-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="80455-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="80455-106">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="80455-106">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="80455-107">Policy</span><span class="sxs-lookup"><span data-stu-id="80455-107">Policy</span></span>

<span data-ttu-id="80455-108">Paste the code into the **on-error** block.</span><span class="sxs-lookup"><span data-stu-id="80455-108">Paste the code into the **on-error** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Log errors to Stackify.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="80455-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="80455-109">Next steps</span></span>

<span data-ttu-id="80455-110">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="80455-110">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="80455-111">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="80455-111">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="80455-112">Policy samples</span><span class="sxs-lookup"><span data-stu-id="80455-112">Policy samples</span></span>](../policy-samples.md)

