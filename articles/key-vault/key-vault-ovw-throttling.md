---
title: Azure Key Vault throttling guidance
description: Key Vault throttling limits the number of concurrent calls to prevent overuse of resources.
services: key-vault
documentationcenter: ''
author: bryanla
manager: mbaldwin
tags: ''
ms.assetid: 9b7d065e-1979-4397-8298-eeba3aec4792
ms.service: key-vault
ms.workload: identity
ms.topic: conceptual
ms.date: 05/10/2018
ms.author: bryanla
ms.openlocfilehash: 4906be4dc6315d8b4dd3c1e640b40caec28b7743
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857176"
---
# <a name="azure-key-vault-throttling-guidance"></a><span data-ttu-id="9259f-103">Azure Key Vault throttling guidance</span><span class="sxs-lookup"><span data-stu-id="9259f-103">Azure Key Vault throttling guidance</span></span>

<span data-ttu-id="9259f-104">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span><span class="sxs-lookup"><span data-stu-id="9259f-104">Throttling is a process you initiate that limits the number of concurrent calls to the Azure service to prevent overuse of resources.</span></span> <span data-ttu-id="9259f-105">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span><span class="sxs-lookup"><span data-stu-id="9259f-105">Azure Key Vault (AKV) is designed to handle a high volume of requests.</span></span> <span data-ttu-id="9259f-106">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span><span class="sxs-lookup"><span data-stu-id="9259f-106">If an overwhelming number of requests occurs, throttling your client's requests helps maintain optimal performance and reliability of the AKV service.</span></span>

<span data-ttu-id="9259f-107">Throttling limits vary based on the scenario.</span><span class="sxs-lookup"><span data-stu-id="9259f-107">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="9259f-108">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span><span class="sxs-lookup"><span data-stu-id="9259f-108">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="how-does-key-vault-handle-its-limits"></a><span data-ttu-id="9259f-109">How does Key Vault handle its limits?</span><span class="sxs-lookup"><span data-stu-id="9259f-109">How does Key Vault handle its limits?</span></span>

<span data-ttu-id="9259f-110">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span><span class="sxs-lookup"><span data-stu-id="9259f-110">Service limits in Key Vault are there to prevent misuse of resources and ensure quality of service for all of Key Vault’s clients.</span></span> <span data-ttu-id="9259f-111">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span><span class="sxs-lookup"><span data-stu-id="9259f-111">When a service threshold is exceeded, Key Vault limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="9259f-112">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span><span class="sxs-lookup"><span data-stu-id="9259f-112">When this happens, Key Vault returns HTTP status code 429 (Too many requests), and the requests fail.</span></span> <span data-ttu-id="9259f-113">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span><span class="sxs-lookup"><span data-stu-id="9259f-113">Also, failed requests that return a 429 count towards the throttle limits tracked by Key Vault.</span></span> 

<span data-ttu-id="9259f-114">If you have a valid business case for higher throttle limits, please contact us.</span><span class="sxs-lookup"><span data-stu-id="9259f-114">If you have a valid business case for higher throttle limits, please contact us.</span></span>


## <a name="how-to-throttle-your-app-in-response-to-service-limits"></a><span data-ttu-id="9259f-115">How to throttle your app in response to service limits</span><span class="sxs-lookup"><span data-stu-id="9259f-115">How to throttle your app in response to service limits</span></span>

<span data-ttu-id="9259f-116">The following are **best practices** for throttling your app:</span><span class="sxs-lookup"><span data-stu-id="9259f-116">The following are **best practices** for throttling your app:</span></span>
- <span data-ttu-id="9259f-117">Reduce the number of operations per request.</span><span class="sxs-lookup"><span data-stu-id="9259f-117">Reduce the number of operations per request.</span></span>
- <span data-ttu-id="9259f-118">Reduce the frequency of requests.</span><span class="sxs-lookup"><span data-stu-id="9259f-118">Reduce the frequency of requests.</span></span>
- <span data-ttu-id="9259f-119">Avoid immediate retries.</span><span class="sxs-lookup"><span data-stu-id="9259f-119">Avoid immediate retries.</span></span> 
    - <span data-ttu-id="9259f-120">All requests accrue against your usage limits.</span><span class="sxs-lookup"><span data-stu-id="9259f-120">All requests accrue against your usage limits.</span></span>

<span data-ttu-id="9259f-121">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span><span class="sxs-lookup"><span data-stu-id="9259f-121">When you implement your app's error handling, use the HTTP error code 429 to detect the need for client-side throttling.</span></span> <span data-ttu-id="9259f-122">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span><span class="sxs-lookup"><span data-stu-id="9259f-122">If the request fails again with an HTTP 429 error code, you are still encountering an Azure service limit.</span></span> <span data-ttu-id="9259f-123">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span><span class="sxs-lookup"><span data-stu-id="9259f-123">Continue to use the recommended client-side throttling method, retrying the request until it succeeds.</span></span>

### <a name="recommended-client-side-throttling-method"></a><span data-ttu-id="9259f-124">Recommended client-side throttling method</span><span class="sxs-lookup"><span data-stu-id="9259f-124">Recommended client-side throttling method</span></span>

<span data-ttu-id="9259f-125">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span><span class="sxs-lookup"><span data-stu-id="9259f-125">On HTTP error code 429, begin throttling your client using an exponential backoff approach:</span></span>

1. <span data-ttu-id="9259f-126">Wait 1 second, retry request</span><span class="sxs-lookup"><span data-stu-id="9259f-126">Wait 1 second, retry request</span></span>
2. <span data-ttu-id="9259f-127">If still throttled wait 2 seconds, retry request</span><span class="sxs-lookup"><span data-stu-id="9259f-127">If still throttled wait 2 seconds, retry request</span></span>
3. <span data-ttu-id="9259f-128">If still throttled wait 4 seconds, retry request</span><span class="sxs-lookup"><span data-stu-id="9259f-128">If still throttled wait 4 seconds, retry request</span></span>
4. <span data-ttu-id="9259f-129">If still throttled wait 8 seconds, retry request</span><span class="sxs-lookup"><span data-stu-id="9259f-129">If still throttled wait 8 seconds, retry request</span></span>
5. <span data-ttu-id="9259f-130">If still throttled wait 16 seconds, retry request</span><span class="sxs-lookup"><span data-stu-id="9259f-130">If still throttled wait 16 seconds, retry request</span></span>

<span data-ttu-id="9259f-131">At this point, you should not be getting HTTP 429 response codes.</span><span class="sxs-lookup"><span data-stu-id="9259f-131">At this point, you should not be getting HTTP 429 response codes.</span></span>

## <a name="see-also"></a><span data-ttu-id="9259f-132">See also</span><span class="sxs-lookup"><span data-stu-id="9259f-132">See also</span></span>

<span data-ttu-id="9259f-133">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span><span class="sxs-lookup"><span data-stu-id="9259f-133">For a deeper orientation of throttling on the Microsoft Cloud, see [Throttling Pattern](https://docs.microsoft.com/azure/architecture/patterns/throttling).</span></span>

