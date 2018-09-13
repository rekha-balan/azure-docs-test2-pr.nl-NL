---
title: Manage performance and connectivity on Azure China 21Vianet | Microsoft Docs
description: When deploying and operating an application or workload on Microsoft Azure China 21Vianet, we recommend performance and network testing. If your Azure application provides services to users outside of China, there are other considerations as well.
services: china
cloud: na
documentationcenter: na
author: v-wimarc
manager: edprice
ms.assetid: na
ms.service: china
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 09/29/2017
ms.author: v-wimarc
ms.openlocfilehash: 51c3e610468a8721d05e3a14cf2215a5d0295b4d
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866241"
---
# <a name="manage-performance-and-connectivity"></a><span data-ttu-id="e0ec2-104">Manage performance and connectivity</span><span class="sxs-lookup"><span data-stu-id="e0ec2-104">Manage performance and connectivity</span></span>
<span data-ttu-id="e0ec2-105">When deploying and operating an application or workload on Microsoft Azure operated by 21Vianet (Azure China 21Vianet), we recommend performance and network testing.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-105">When deploying and operating an application or workload on Microsoft Azure operated by 21Vianet (Azure China 21Vianet), we recommend performance and network testing.</span></span> <span data-ttu-id="e0ec2-106">In addition, if your Azure application provides services to users outside of China, consider the following:</span><span class="sxs-lookup"><span data-stu-id="e0ec2-106">In addition, if your Azure application provides services to users outside of China, consider the following:</span></span>
- <span data-ttu-id="e0ec2-107">For users in China, host workloads on Microsoft Azure China 21Vianet.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-107">For users in China, host workloads on Microsoft Azure China 21Vianet.</span></span>
- <span data-ttu-id="e0ec2-108">For users outside of China, deploy workloads to the closest Azure region.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-108">For users outside of China, deploy workloads to the closest Azure region.</span></span>

## <a name="performance-considerations"></a><span data-ttu-id="e0ec2-109">Performance considerations</span><span class="sxs-lookup"><span data-stu-id="e0ec2-109">Performance considerations</span></span>
<span data-ttu-id="e0ec2-110">To fine-tune and optimize your Azure application, conduct performance tests and consider the following recommendations:</span><span class="sxs-lookup"><span data-stu-id="e0ec2-110">To fine-tune and optimize your Azure application, conduct performance tests and consider the following recommendations:</span></span> 
- <span data-ttu-id="e0ec2-111">Conduct your performance testing in China Standard Time, instead of your own time zone.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-111">Conduct your performance testing in China Standard Time, instead of your own time zone.</span></span> 
- <span data-ttu-id="e0ec2-112">Conduct testing in mainland China to better reflect the response times and the real user experience.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-112">Conduct testing in mainland China to better reflect the response times and the real user experience.</span></span>
- <span data-ttu-id="e0ec2-113">Test during the Internet rush hours to measure the performance of your application under high workloads.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-113">Test during the Internet rush hours to measure the performance of your application under high workloads.</span></span> 

## <a name="network-latency-in-china"></a><span data-ttu-id="e0ec2-114">Network latency in China</span><span class="sxs-lookup"><span data-stu-id="e0ec2-114">Network latency in China</span></span>
<span data-ttu-id="e0ec2-115">The network latency between China and the rest of the world is inevitable given the intermediary technologies that regulate cross-border Internet traffic.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-115">The network latency between China and the rest of the world is inevitable given the intermediary technologies that regulate cross-border Internet traffic.</span></span> <span data-ttu-id="e0ec2-116">Website users and administrators may experience slow performance.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-116">Website users and administrators may experience slow performance.</span></span> <span data-ttu-id="e0ec2-117">These tips may help:</span><span class="sxs-lookup"><span data-stu-id="e0ec2-117">These tips may help:</span></span> 
- <span data-ttu-id="e0ec2-118">For websites with streaming media and other rich media content, the [Azure Content Delivery Network](/azure/china/china-get-started-service-cdn) (CDN) may be able to help improve responsiveness.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-118">For websites with streaming media and other rich media content, the [Azure Content Delivery Network](/azure/china/china-get-started-service-cdn) (CDN) may be able to help improve responsiveness.</span></span> <span data-ttu-id="e0ec2-119">Under Chinese law, using the CDN service in China may also subject an offshore website to [ICP filing](/azure/china/china-overview-policies).</span><span class="sxs-lookup"><span data-stu-id="e0ec2-119">Under Chinese law, using the CDN service in China may also subject an offshore website to [ICP filing](/azure/china/china-overview-policies).</span></span> <span data-ttu-id="e0ec2-120">Do not use a global CDN service that does not have a point of presence (PoP) inside mainland China.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-120">Do not use a global CDN service that does not have a point of presence (PoP) inside mainland China.</span></span>
- <span data-ttu-id="e0ec2-121">For the best user experience, host a website in China to serve users in China.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-121">For the best user experience, host a website in China to serve users in China.</span></span>
- <span data-ttu-id="e0ec2-122">For website administrators outside of China, use Secure Shell (SSH) to connect to your remote server for a faster network connection to Microsoft Azure China 21Vianet.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-122">For website administrators outside of China, use Secure Shell (SSH) to connect to your remote server for a faster network connection to Microsoft Azure China 21Vianet.</span></span> <span data-ttu-id="e0ec2-123">For example, use SSH to access a local Azure virtual machine, and from there, use SSH to connect to an Azure China 21Vianet virtual machine.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-123">For example, use SSH to access a local Azure virtual machine, and from there, use SSH to connect to an Azure China 21Vianet virtual machine.</span></span> 

## <a name="global-connectivity-and-interoperability"></a><span data-ttu-id="e0ec2-124">Global connectivity and interoperability</span><span class="sxs-lookup"><span data-stu-id="e0ec2-124">Global connectivity and interoperability</span></span>
<span data-ttu-id="e0ec2-125">A hybrid cloud can extend your applications or workloads on Microsoft Azure China 21Vianet and provide global connectivity and interoperability.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-125">A hybrid cloud can extend your applications or workloads on Microsoft Azure China 21Vianet and provide global connectivity and interoperability.</span></span> <span data-ttu-id="e0ec2-126">The following connections are supported:</span><span class="sxs-lookup"><span data-stu-id="e0ec2-126">The following connections are supported:</span></span>
- <span data-ttu-id="e0ec2-127">Use a virtual private network (VPN) or Azure ExpressRoute to create a direct network connection between Azure and your on-premises private cloud or backend systems within China.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-127">Use a virtual private network (VPN) or Azure ExpressRoute to create a direct network connection between Azure and your on-premises private cloud or backend systems within China.</span></span>
- <span data-ttu-id="e0ec2-128">Set up a site-to-site VPN to connect an Azure site in China to your on-premises location outside of China.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-128">Set up a site-to-site VPN to connect an Azure site in China to your on-premises location outside of China.</span></span> <span data-ttu-id="e0ec2-129">ExpressRoute is not supported for direct network connectivity to an external (outside of China) site.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-129">ExpressRoute is not supported for direct network connectivity to an external (outside of China) site.</span></span> <span data-ttu-id="e0ec2-130">Even global Azure is considered external.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-130">Even global Azure is considered external.</span></span>

> [!NOTE]
> <span data-ttu-id="e0ec2-131">Approval by the Ministry of Industry and Information Technology (MIIT) of the Chinese government is needed to set up a VPN or ExpressRoute connection between your services hosted on Azure, your ICP-registered hosting location, and an outside location.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-131">Approval by the Ministry of Industry and Information Technology (MIIT) of the Chinese government is needed to set up a VPN or ExpressRoute connection between your services hosted on Azure, your ICP-registered hosting location, and an outside location.</span></span> <span data-ttu-id="e0ec2-132">You must register, report, and obtain for approval from the MIIT.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-132">You must register, report, and obtain for approval from the MIIT.</span></span> <span data-ttu-id="e0ec2-133">Contact [21Vianet](mailto:icpsupport@oe.21vianet.com) for help in the approval process.</span><span class="sxs-lookup"><span data-stu-id="e0ec2-133">Contact [21Vianet](mailto:icpsupport@oe.21vianet.com) for help in the approval process.</span></span>

<span data-ttu-id="e0ec2-134">For a VPN setup, apply for an exception through 21Vianet and provide the following information:</span><span class="sxs-lookup"><span data-stu-id="e0ec2-134">For a VPN setup, apply for an exception through 21Vianet and provide the following information:</span></span>
- <span data-ttu-id="e0ec2-135">Overseas IP address for the overseas VPN endpoint</span><span class="sxs-lookup"><span data-stu-id="e0ec2-135">Overseas IP address for the overseas VPN endpoint</span></span>
- <span data-ttu-id="e0ec2-136">VPN protocol and ports</span><span class="sxs-lookup"><span data-stu-id="e0ec2-136">VPN protocol and ports</span></span>
- <span data-ttu-id="e0ec2-137">Location of overseas IP</span><span class="sxs-lookup"><span data-stu-id="e0ec2-137">Location of overseas IP</span></span>
- <span data-ttu-id="e0ec2-138">Owner of overseas IP</span><span class="sxs-lookup"><span data-stu-id="e0ec2-138">Owner of overseas IP</span></span>
- <span data-ttu-id="e0ec2-139">Relationship between the overseas IP owner and the Azure customer</span><span class="sxs-lookup"><span data-stu-id="e0ec2-139">Relationship between the overseas IP owner and the Azure customer</span></span>

<span data-ttu-id="e0ec2-140">For more details, please contact [21Vianet](mailto:icpsupport@oe.21vianet.com).</span><span class="sxs-lookup"><span data-stu-id="e0ec2-140">For more details, please contact [21Vianet](mailto:icpsupport@oe.21vianet.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e0ec2-141">Next steps</span><span class="sxs-lookup"><span data-stu-id="e0ec2-141">Next steps</span></span>
- [<span data-ttu-id="e0ec2-142">Azure Content Delivery Network</span><span class="sxs-lookup"><span data-stu-id="e0ec2-142">Azure Content Delivery Network</span></span>](/azure/china/china-get-started-service-cdn)
- [<span data-ttu-id="e0ec2-143">ICP filing</span><span class="sxs-lookup"><span data-stu-id="e0ec2-143">ICP filing</span></span>](/azure/china/china-overview-policies)


