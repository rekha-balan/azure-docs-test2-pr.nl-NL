---
title: Azure API managment policy sample - Authorize access using Google OAuth token | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to authorize access to your endpoints using Google as an OAuth token provider.
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
ms.openlocfilehash: 22aed976ef69288aa0e49215a739174786843527
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869387"
---
# <a name="authorize-access-using-google-oauth-token"></a><span data-ttu-id="93740-103">Authorize access using Google OAuth token</span><span class="sxs-lookup"><span data-stu-id="93740-103">Authorize access using Google OAuth token</span></span>

<span data-ttu-id="93740-104">This article shows an Azure API management policy sample that demonstrates how to authorize access to your endpoints using Google as an OAuth token provider.</span><span class="sxs-lookup"><span data-stu-id="93740-104">This article shows an Azure API management policy sample that demonstrates how to authorize access to your endpoints using Google as an OAuth token provider.</span></span> <span data-ttu-id="93740-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="93740-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="93740-106">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="93740-106">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="93740-107">Policy</span><span class="sxs-lookup"><span data-stu-id="93740-107">Policy</span></span>

<span data-ttu-id="93740-108">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="93740-108">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Simple Google OAuth validate-jwt.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="93740-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="93740-109">Next steps</span></span>

<span data-ttu-id="93740-110">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="93740-110">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="93740-111">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="93740-111">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="93740-112">Policy samples</span><span class="sxs-lookup"><span data-stu-id="93740-112">Policy samples</span></span>](../policy-samples.md)

