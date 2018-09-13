---
title: Azure API managment policy sample - Add a Forwarded header  | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to add a Forwarded header in the inbound request to allow the backend API to construct proper URLs.
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
ms.openlocfilehash: a9dfcbf4be4b659d761d66d67d2ae4c7b70a245e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866471"
---
# <a name="add-a-forwarded-header"></a><span data-ttu-id="e9493-103">Add a Forwarded header</span><span class="sxs-lookup"><span data-stu-id="e9493-103">Add a Forwarded header</span></span>

<span data-ttu-id="e9493-104">This article shows an Azure API management policy sample that demonstrates how to add a Forwarded header in the inbound request to allow the backend API to construct proper URLs.</span><span class="sxs-lookup"><span data-stu-id="e9493-104">This article shows an Azure API management policy sample that demonstrates how to add a Forwarded header in the inbound request to allow the backend API to construct proper URLs.</span></span> <span data-ttu-id="e9493-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e9493-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="e9493-106">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e9493-106">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="code"></a><span data-ttu-id="e9493-107">Code</span><span class="sxs-lookup"><span data-stu-id="e9493-107">Code</span></span>

<span data-ttu-id="e9493-108">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="e9493-108">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Forward gateway hostname to backend for generating correct urls in responses.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="e9493-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="e9493-109">Next steps</span></span>

<span data-ttu-id="e9493-110">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="e9493-110">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="e9493-111">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="e9493-111">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="e9493-112">Policy samples</span><span class="sxs-lookup"><span data-stu-id="e9493-112">Policy samples</span></span>](../policy-samples.md)
