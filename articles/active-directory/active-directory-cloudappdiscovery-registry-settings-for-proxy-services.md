---
title: Cloud App Discovery Registry Settings for Proxy Services | Microsoft Docs
description: The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.
services: active-directory
documentationcenter: ''
author: MarkusVi
manager: femila
ms.assetid: 8d78e925-e331-40ba-904a-e4ef14260cac
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/06/2017
ms.author: markvi
ms.openlocfilehash: 002a60f22cc05984c96897d424ceb3150d4ee14b
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44551476"
---
# <a name="cloud-app-discovery-registry-settings-for-proxy-services"></a><span data-ttu-id="7ea7a-103">Cloud App Discovery Registry Settings for Proxy Services</span><span class="sxs-lookup"><span data-stu-id="7ea7a-103">Cloud App Discovery Registry Settings for Proxy Services</span></span>
<span data-ttu-id="7ea7a-104">By default, the Cloud App Discovery agent is configured to use only the ports 80 or 443.</span><span class="sxs-lookup"><span data-stu-id="7ea7a-104">By default, the Cloud App Discovery agent is configured to use only the ports 80 or 443.</span></span> <span data-ttu-id="7ea7a-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need to configure your agents to use this port.</span><span class="sxs-lookup"><span data-stu-id="7ea7a-105">If you are planning on installing Cloud App Discovery in an environment with a proxy server that is using a custom port (neither 80 nor 443), you need to configure your agents to use this port.</span></span> <span data-ttu-id="7ea7a-106">The configuration is based on a registry key.</span><span class="sxs-lookup"><span data-stu-id="7ea7a-106">The configuration is based on a registry key.</span></span>

<span data-ttu-id="7ea7a-107">The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.</span><span class="sxs-lookup"><span data-stu-id="7ea7a-107">The objective of this topic is to provide you with the steps you need to perform to set the required port on the computers running the Cloud App Discovery agent.</span></span>

<span data-ttu-id="7ea7a-108">**To modify the port used by the computer running the Cloud App Discovery agent, perform the following steps:**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-108">**To modify the port used by the computer running the Cloud App Discovery agent, perform the following steps:**</span></span>

1. <span data-ttu-id="7ea7a-109">Start the registry editor.</span><span class="sxs-lookup"><span data-stu-id="7ea7a-109">Start the registry editor.</span></span> <br> ![Run](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy01.png)
2. <span data-ttu-id="7ea7a-111">Navigate to or create the following registry key:</span><span class="sxs-lookup"><span data-stu-id="7ea7a-111">Navigate to or create the following registry key:</span></span> <br> <span data-ttu-id="7ea7a-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-112">**HKLM_LOCAL_MACHINE\Software\Microsoft\Cloud App Discovery\Endpoint**</span></span> 
3. <span data-ttu-id="7ea7a-113">Create a new **multi-string** value called **Ports**.</span><span class="sxs-lookup"><span data-stu-id="7ea7a-113">Create a new **multi-string** value called **Ports**.</span></span> <span data-ttu-id="7ea7a-114">![New](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span><span class="sxs-lookup"><span data-stu-id="7ea7a-114">![New](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy02.png)</span></span>
4. <span data-ttu-id="7ea7a-115">To open the **Edit Multi-String** dialog, double-click the Ports value.</span><span class="sxs-lookup"><span data-stu-id="7ea7a-115">To open the **Edit Multi-String** dialog, double-click the Ports value.</span></span>
5. <span data-ttu-id="7ea7a-116">In the Value data textbox, type the following values and add all custom ports that are used by your organization:</span><span class="sxs-lookup"><span data-stu-id="7ea7a-116">In the Value data textbox, type the following values and add all custom ports that are used by your organization:</span></span> <br><br>
   <span data-ttu-id="7ea7a-117">**80**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-117">**80**</span></span> <br>
   <span data-ttu-id="7ea7a-118">**8080**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-118">**8080**</span></span> <br>
   <span data-ttu-id="7ea7a-119">**8118**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-119">**8118**</span></span> <br>
   <span data-ttu-id="7ea7a-120">**8888**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-120">**8888**</span></span> <br>
   <span data-ttu-id="7ea7a-121">**81**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-121">**81**</span></span> <br>
   <span data-ttu-id="7ea7a-122">**12080**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-122">**12080**</span></span> <br>
   <span data-ttu-id="7ea7a-123">**6999**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-123">**6999**</span></span> <br>
   <span data-ttu-id="7ea7a-124">**30606**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-124">**30606**</span></span> <br>
   <span data-ttu-id="7ea7a-125">**31595**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-125">**31595**</span></span> <br>
   <span data-ttu-id="7ea7a-126">**4080**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-126">**4080**</span></span> <br>
   <span data-ttu-id="7ea7a-127">**443**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-127">**443**</span></span> <br>
   <span data-ttu-id="7ea7a-128">**1110**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-128">**1110**</span></span> <br><br>
   <span data-ttu-id="7ea7a-129">![Edit Multi-String](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span><span class="sxs-lookup"><span data-stu-id="7ea7a-129">![Edit Multi-String](https://docstestmedia1.blob.core.windows.net/azure-media/articles/active-directory/media/active-directory-cloudappdiscovery-registry-settings-for-proxy-services/proxy03.png)</span></span>
6. <span data-ttu-id="7ea7a-130">Click **OK** to close the **Edit Multi-String** dialog.</span><span class="sxs-lookup"><span data-stu-id="7ea7a-130">Click **OK** to close the **Edit Multi-String** dialog.</span></span>

<span data-ttu-id="7ea7a-131">**Additional Resources**</span><span class="sxs-lookup"><span data-stu-id="7ea7a-131">**Additional Resources**</span></span>

* [<span data-ttu-id="7ea7a-132">How can I discover unsanctioned cloud apps that are used within my organization</span><span class="sxs-lookup"><span data-stu-id="7ea7a-132">How can I discover unsanctioned cloud apps that are used within my organization</span></span>](active-directory-cloudappdiscovery-whatis.md) 




