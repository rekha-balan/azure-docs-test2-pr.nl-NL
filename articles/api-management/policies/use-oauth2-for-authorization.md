---
title: Azure API managment policy sample - Use OAuth2 for authorization between the gateway and a backend | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to use OAuth2 for authorization between the gateway and a backend. It shows how to obtain an access token from AAD and forward it to the backend.
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
ms.openlocfilehash: d064e918d514b9be1b9fa2dbf30c10edf5167908
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44867556"
---
# <a name="use-oauth2-for-authorization-between-the-gateway-and-a-backend"></a><span data-ttu-id="3facd-104">Use OAuth2 for authorization between the gateway and a backend</span><span class="sxs-lookup"><span data-stu-id="3facd-104">Use OAuth2 for authorization between the gateway and a backend</span></span>

<span data-ttu-id="3facd-105">This article shows an Azure API management policy sample that demonstrates how to use OAuth2 for authorization between the gateway and a backend.</span><span class="sxs-lookup"><span data-stu-id="3facd-105">This article shows an Azure API management policy sample that demonstrates how to use OAuth2 for authorization between the gateway and a backend.</span></span> <span data-ttu-id="3facd-106">It shows how to obtain an access token from AAD and forward it to the backend.</span><span class="sxs-lookup"><span data-stu-id="3facd-106">It shows how to obtain an access token from AAD and forward it to the backend.</span></span> 

<span data-ttu-id="3facd-107">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="3facd-107">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="3facd-108">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="3facd-108">To see other examples, see [policy samples](../policy-samples.md).</span></span>

<span data-ttu-id="3facd-109">The following script uses properties that appear in {{property}}.</span><span class="sxs-lookup"><span data-stu-id="3facd-109">The following script uses properties that appear in {{property}}.</span></span> <span data-ttu-id="3facd-110">To learn about properties and how to use them in API Management policies, see [this](../api-management-howto-properties.md) topic.</span><span class="sxs-lookup"><span data-stu-id="3facd-110">To learn about properties and how to use them in API Management policies, see [this](../api-management-howto-properties.md) topic.</span></span>
 
## <a name="policy"></a><span data-ttu-id="3facd-111">Policy</span><span class="sxs-lookup"><span data-stu-id="3facd-111">Policy</span></span>

<span data-ttu-id="3facd-112">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="3facd-112">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Get OAuth2 access token from AAD and forward it to the backend.policy.xml)]
  
## <a name="next-steps"></a><span data-ttu-id="3facd-113">Next steps</span><span class="sxs-lookup"><span data-stu-id="3facd-113">Next steps</span></span>

<span data-ttu-id="3facd-114">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="3facd-114">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="3facd-115">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="3facd-115">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="3facd-116">Policy samples</span><span class="sxs-lookup"><span data-stu-id="3facd-116">Policy samples</span></span>](../policy-samples.md)

