---
title: Azure API managment policy sample - Generate Shared Access Signature  | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to generate Shared Access Signature using expressions and forward the request to Azure storage with rewrite-uri policy..
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
ms.openlocfilehash: c8a4d25211a0030c013628e69865406bb6e8899e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44864787"
---
# <a name="generate-shared-access-signature"></a><span data-ttu-id="cf863-103">Generate Shared Access Signature</span><span class="sxs-lookup"><span data-stu-id="cf863-103">Generate Shared Access Signature</span></span>

<span data-ttu-id="cf863-104">This article shows an Azure API management policy sample that demonstrates how to generate [Shared Access Signature](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) using expressions and forward the request to Azure storage with rewrite-uri policy.</span><span class="sxs-lookup"><span data-stu-id="cf863-104">This article shows an Azure API management policy sample that demonstrates how to generate [Shared Access Signature](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1) using expressions and forward the request to Azure storage with rewrite-uri policy.</span></span> <span data-ttu-id="cf863-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span><span class="sxs-lookup"><span data-stu-id="cf863-105">To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md).</span></span> <span data-ttu-id="cf863-106">To see other examples, see [policy samples](../policy-samples.md).</span><span class="sxs-lookup"><span data-stu-id="cf863-106">To see other examples, see [policy samples](../policy-samples.md).</span></span>

## <a name="policy"></a><span data-ttu-id="cf863-107">Policy</span><span class="sxs-lookup"><span data-stu-id="cf863-107">Policy</span></span>

<span data-ttu-id="cf863-108">Paste the code into the **inbound** block.</span><span class="sxs-lookup"><span data-stu-id="cf863-108">Paste the code into the **inbound** block.</span></span>

[!code-xml[Main](../../../api-management-policy-samples/examples/Generate Shared Access Signature and forward request to Azure storage.policy.xml)]

## <a name="next-steps"></a><span data-ttu-id="cf863-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="cf863-109">Next steps</span></span>

<span data-ttu-id="cf863-110">Learn more about APIM policies:</span><span class="sxs-lookup"><span data-stu-id="cf863-110">Learn more about APIM policies:</span></span>

+ [<span data-ttu-id="cf863-111">Transformation policies</span><span class="sxs-lookup"><span data-stu-id="cf863-111">Transformation policies</span></span>](../api-management-transformation-policies.md)
+ [<span data-ttu-id="cf863-112">Policy samples</span><span class="sxs-lookup"><span data-stu-id="cf863-112">Policy samples</span></span>](../policy-samples.md)

