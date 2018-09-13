---
title: China content delivery with Azure CDN | Microsoft Docs
description: Learn about using Azure Content Delivery Network (CDN) to deliver content to China users.
services: cdn
documentationcenter: ''
author: dksimpson
manager: cfowler
editor: ''
ms.assetid: ''
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/16/2018
ms.author: v-deasim
ms.custom: mvc
ms.openlocfilehash: 59788f301bb501103babd55a2ac37102932f4dcf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856660"
---
# <a name="china-content-delivery-with-azure-cdn"></a><span data-ttu-id="4832e-103">China content delivery with Azure CDN</span><span class="sxs-lookup"><span data-stu-id="4832e-103">China content delivery with Azure CDN</span></span>

<span data-ttu-id="4832e-104">Azure Content Delivery Network (CDN) global can serve content to China users with point-of-presence (POP) locations near China or any POP that provides the best performance to requests originating from China.</span><span class="sxs-lookup"><span data-stu-id="4832e-104">Azure Content Delivery Network (CDN) global can serve content to China users with point-of-presence (POP) locations near China or any POP that provides the best performance to requests originating from China.</span></span> <span data-ttu-id="4832e-105">However, if China is a significant market for your customers and they need fast performance, consider using Azure CDN China instead.</span><span class="sxs-lookup"><span data-stu-id="4832e-105">However, if China is a significant market for your customers and they need fast performance, consider using Azure CDN China instead.</span></span>

<span data-ttu-id="4832e-106">Azure CDN China differs from Azure CDN global in that it delivers content from POPs inside of China by partnering with a number of local providers.</span><span class="sxs-lookup"><span data-stu-id="4832e-106">Azure CDN China differs from Azure CDN global in that it delivers content from POPs inside of China by partnering with a number of local providers.</span></span> <span data-ttu-id="4832e-107">Due to Chinese compliance and regulation, you must register a separate subscription to use Azure CDN China and your websites need to have an ICP license.</span><span class="sxs-lookup"><span data-stu-id="4832e-107">Due to Chinese compliance and regulation, you must register a separate subscription to use Azure CDN China and your websites need to have an ICP license.</span></span> <span data-ttu-id="4832e-108">The portal and API experience to enable and manage content delivery is identical between Azure CDN global and Azure CDN China.</span><span class="sxs-lookup"><span data-stu-id="4832e-108">The portal and API experience to enable and manage content delivery is identical between Azure CDN global and Azure CDN China.</span></span>

## <a name="comparison-of-azure-cdn-global-and-azure-cdn-china"></a><span data-ttu-id="4832e-109">Comparison of Azure CDN global and Azure CDN China</span><span class="sxs-lookup"><span data-stu-id="4832e-109">Comparison of Azure CDN global and Azure CDN China</span></span>

<span data-ttu-id="4832e-110">Azure CDN global and Azure CDN China have the following features:</span><span class="sxs-lookup"><span data-stu-id="4832e-110">Azure CDN global and Azure CDN China have the following features:</span></span>

- <span data-ttu-id="4832e-111">Azure CDN global:</span><span class="sxs-lookup"><span data-stu-id="4832e-111">Azure CDN global:</span></span>

     - <span data-ttu-id="4832e-112">Portal: https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="4832e-112">Portal: https://portal.azure.com</span></span>  

     - <span data-ttu-id="4832e-113">Performs content delivery outside of China</span><span class="sxs-lookup"><span data-stu-id="4832e-113">Performs content delivery outside of China</span></span>

     - <span data-ttu-id="4832e-114">Four pricing tiers: Microsoft standard, Verizon standard, Verizon premium, and Akamai standard</span><span class="sxs-lookup"><span data-stu-id="4832e-114">Four pricing tiers: Microsoft standard, Verizon standard, Verizon premium, and Akamai standard</span></span>

     - [<span data-ttu-id="4832e-115">Documentation</span><span class="sxs-lookup"><span data-stu-id="4832e-115">Documentation</span></span>](https://docs.microsoft.com/en-us/azure/cdn/)

- <span data-ttu-id="4832e-116">Azure CDN China:</span><span class="sxs-lookup"><span data-stu-id="4832e-116">Azure CDN China:</span></span>

     - <span data-ttu-id="4832e-117">Portal: https://portal.azure.cn</span><span class="sxs-lookup"><span data-stu-id="4832e-117">Portal: https://portal.azure.cn</span></span>

     - <span data-ttu-id="4832e-118">Performs content delivery inside of China</span><span class="sxs-lookup"><span data-stu-id="4832e-118">Performs content delivery inside of China</span></span>

     - <span data-ttu-id="4832e-119">Two pricing tiers: Standard and premium</span><span class="sxs-lookup"><span data-stu-id="4832e-119">Two pricing tiers: Standard and premium</span></span>

     - [<span data-ttu-id="4832e-120">Documentation</span><span class="sxs-lookup"><span data-stu-id="4832e-120">Documentation</span></span>](https://docs.azure.cn/en-us/cdn/)
 

## <a name="next-steps"></a><span data-ttu-id="4832e-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="4832e-121">Next steps</span></span>

<span data-ttu-id="4832e-122">To learn more about Azure CDN China, see:</span><span class="sxs-lookup"><span data-stu-id="4832e-122">To learn more about Azure CDN China, see:</span></span>

- [<span data-ttu-id="4832e-123">Content Delivery Network features</span><span class="sxs-lookup"><span data-stu-id="4832e-123">Content Delivery Network features</span></span>](https://www.azure.cn/en-us/home/features/cdn/)

- [<span data-ttu-id="4832e-124">Overview of Azure Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="4832e-124">Overview of Azure Content Delivery Network</span></span>](https://docs.azure.cn/en-us/cdn/cdn-overview)

- [<span data-ttu-id="4832e-125">Use the Azure Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="4832e-125">Use the Azure Content Delivery Network</span></span>](https://docs.azure.cn/en-us/cdn/cdn-how-to-use)

- [<span data-ttu-id="4832e-126">Azure service availability in China</span><span class="sxs-lookup"><span data-stu-id="4832e-126">Azure service availability in China</span></span>](https://docs.microsoft.com/en-us/azure/china/china-get-started-service-availability)


