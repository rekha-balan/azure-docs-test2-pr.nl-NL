---
title: Common parameters and headers
description: The parameters and headers common to all operations that you might do related to Key Vault resources.
services: key-vault
documentationcenter: ''
author: bryanla
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: a715d13ca9-d6e8-4e54-ac5e-0ed9400fb15b15d13ca9-d6e8-4e54-ac5e-0ed9400fb15b
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/09/2018
ms.author: bryanla
ms.openlocfilehash: dae5e1ab6244d2898bc218ed5db3b6b2b90150cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866653"
---
# <a name="common-parameters-and-headers"></a><span data-ttu-id="01ba3-103">Common parameters and headers</span><span class="sxs-lookup"><span data-stu-id="01ba3-103">Common parameters and headers</span></span>

<span data-ttu-id="01ba3-104">The following information is common to all operations that you might do related to Key Vault resources:</span><span class="sxs-lookup"><span data-stu-id="01ba3-104">The following information is common to all operations that you might do related to Key Vault resources:</span></span>

- <span data-ttu-id="01ba3-105">Replace `{api-version}` with the api-version in the URI.</span><span class="sxs-lookup"><span data-stu-id="01ba3-105">Replace `{api-version}` with the api-version in the URI.</span></span>
- <span data-ttu-id="01ba3-106">Replace `{subscription-id}` with your subscription identifier in the URI</span><span class="sxs-lookup"><span data-stu-id="01ba3-106">Replace `{subscription-id}` with your subscription identifier in the URI</span></span>
- <span data-ttu-id="01ba3-107">Replace `{resource-group-name}` with the resource group.</span><span class="sxs-lookup"><span data-stu-id="01ba3-107">Replace `{resource-group-name}` with the resource group.</span></span> <span data-ttu-id="01ba3-108">For more information, see Using Resource groups to manage your Azure resources.</span><span class="sxs-lookup"><span data-stu-id="01ba3-108">For more information, see Using Resource groups to manage your Azure resources.</span></span>
- <span data-ttu-id="01ba3-109">Replace `{vault-name}` with your key vault name in the URI.</span><span class="sxs-lookup"><span data-stu-id="01ba3-109">Replace `{vault-name}` with your key vault name in the URI.</span></span>
- <span data-ttu-id="01ba3-110">Set the Content-Type header to application/json.</span><span class="sxs-lookup"><span data-stu-id="01ba3-110">Set the Content-Type header to application/json.</span></span>
- <span data-ttu-id="01ba3-111">Set the Authorization header to a JSON Web Token that you obtain from Azure Active Directory (AAD).</span><span class="sxs-lookup"><span data-stu-id="01ba3-111">Set the Authorization header to a JSON Web Token that you obtain from Azure Active Directory (AAD).</span></span> <span data-ttu-id="01ba3-112">For more information, see [Authenticating Azure Resource Manager](authentication-requests-and-responses.md) requests.</span><span class="sxs-lookup"><span data-stu-id="01ba3-112">For more information, see [Authenticating Azure Resource Manager](authentication-requests-and-responses.md) requests.</span></span>

## <a name="common-error-response"></a><span data-ttu-id="01ba3-113">Common error response</span><span class="sxs-lookup"><span data-stu-id="01ba3-113">Common error response</span></span>
<span data-ttu-id="01ba3-114">The service will use HTTP status codes to indicate success or failure.</span><span class="sxs-lookup"><span data-stu-id="01ba3-114">The service will use HTTP status codes to indicate success or failure.</span></span> <span data-ttu-id="01ba3-115">In addition, failures contain a response in the following format:</span><span class="sxs-lookup"><span data-stu-id="01ba3-115">In addition, failures contain a response in the following format:</span></span>

   <span data-ttu-id="01ba3-116">{</span><span class="sxs-lookup"><span data-stu-id="01ba3-116">{</span></span>  
     <span data-ttu-id="01ba3-117">"error": {</span><span class="sxs-lookup"><span data-stu-id="01ba3-117">"error": {</span></span>  
     <span data-ttu-id="01ba3-118">"code": "BadRequest",</span><span class="sxs-lookup"><span data-stu-id="01ba3-118">"code": "BadRequest",</span></span>  
     <span data-ttu-id="01ba3-119">"message": "The key vault sku is invalid."</span><span class="sxs-lookup"><span data-stu-id="01ba3-119">"message": "The key vault sku is invalid."</span></span>  
     <span data-ttu-id="01ba3-120">}</span><span class="sxs-lookup"><span data-stu-id="01ba3-120">}</span></span>  
   <span data-ttu-id="01ba3-121">}</span><span class="sxs-lookup"><span data-stu-id="01ba3-121">}</span></span>  

|<span data-ttu-id="01ba3-122">Element name</span><span class="sxs-lookup"><span data-stu-id="01ba3-122">Element name</span></span> | <span data-ttu-id="01ba3-123">Type</span><span class="sxs-lookup"><span data-stu-id="01ba3-123">Type</span></span> | <span data-ttu-id="01ba3-124">Description</span><span class="sxs-lookup"><span data-stu-id="01ba3-124">Description</span></span> |
|---|---|---|
| <span data-ttu-id="01ba3-125">code</span><span class="sxs-lookup"><span data-stu-id="01ba3-125">code</span></span> | <span data-ttu-id="01ba3-126">string</span><span class="sxs-lookup"><span data-stu-id="01ba3-126">string</span></span> | <span data-ttu-id="01ba3-127">The type of error that occurred.</span><span class="sxs-lookup"><span data-stu-id="01ba3-127">The type of error that occurred.</span></span>|
| <span data-ttu-id="01ba3-128">message</span><span class="sxs-lookup"><span data-stu-id="01ba3-128">message</span></span> | <span data-ttu-id="01ba3-129">string</span><span class="sxs-lookup"><span data-stu-id="01ba3-129">string</span></span> | <span data-ttu-id="01ba3-130">A description of what caused the error.</span><span class="sxs-lookup"><span data-stu-id="01ba3-130">A description of what caused the error.</span></span> |



## <a name="see-also"></a><span data-ttu-id="01ba3-131">See Also</span><span class="sxs-lookup"><span data-stu-id="01ba3-131">See Also</span></span>
 [<span data-ttu-id="01ba3-132">Azure Key Vault REST API Reference</span><span class="sxs-lookup"><span data-stu-id="01ba3-132">Azure Key Vault REST API Reference</span></span>](/rest/api/keyvault/)
