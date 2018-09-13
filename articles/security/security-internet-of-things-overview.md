---
title: Secure your Internet of Things (IoT) in Azure | Microsoft Docs
description: " Azure internet of things (IoT) services offer a broad range of capabilities. This article helps you understand how to secure your IoT solutions in Azure. "
services: security
documentationcenter: na
author: TomShinder
manager: MBaldwin
editor: TomSh
ms.assetid: 1473c8dd-8669-48fb-86db-b3c50e2eaf59
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/23/2017
ms.author: terrylan
ms.openlocfilehash: 3793f5453b74b6c06d9e58b426d89099298e1288
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556264"
---
# <a name="internet-of-things-security-overview"></a><span data-ttu-id="256f6-104">Internet of Things security overview</span><span class="sxs-lookup"><span data-stu-id="256f6-104">Internet of Things security overview</span></span>
<span data-ttu-id="256f6-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span><span class="sxs-lookup"><span data-stu-id="256f6-105">Azure internet of things (IoT) services offer a broad range of capabilities.</span></span> <span data-ttu-id="256f6-106">These enterprise grade services enable you to:</span><span class="sxs-lookup"><span data-stu-id="256f6-106">These enterprise grade services enable you to:</span></span>

* <span data-ttu-id="256f6-107">Collect data from devices</span><span class="sxs-lookup"><span data-stu-id="256f6-107">Collect data from devices</span></span>
* <span data-ttu-id="256f6-108">Analyze data streams in-motion</span><span class="sxs-lookup"><span data-stu-id="256f6-108">Analyze data streams in-motion</span></span>
* <span data-ttu-id="256f6-109">Store and query large data sets</span><span class="sxs-lookup"><span data-stu-id="256f6-109">Store and query large data sets</span></span>
* <span data-ttu-id="256f6-110">Visualize both real-time and historical data</span><span class="sxs-lookup"><span data-stu-id="256f6-110">Visualize both real-time and historical data</span></span>
* <span data-ttu-id="256f6-111">Integrate with back-office systems</span><span class="sxs-lookup"><span data-stu-id="256f6-111">Integrate with back-office systems</span></span>

<span data-ttu-id="256f6-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span><span class="sxs-lookup"><span data-stu-id="256f6-112">To deliver these capabilities, Azure IoT Suite packages together multiple Azure services with custom extensions as preconfigured solutions.</span></span> <span data-ttu-id="256f6-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span><span class="sxs-lookup"><span data-stu-id="256f6-113">These preconfigured solutions are base implementations of common IoT solution patterns that help to reduce the time you take to deliver your IoT solutions.</span></span> <span data-ttu-id="256f6-114">Using the IoT software development kits, you can customize and extend these solutions to meet your own requirements.</span><span class="sxs-lookup"><span data-stu-id="256f6-114">Using the IoT software development kits, you can customize and extend these solutions to meet your own requirements.</span></span> <span data-ttu-id="256f6-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span><span class="sxs-lookup"><span data-stu-id="256f6-115">You can also use these solutions as examples or templates when you are developing new IoT solutions.</span></span>

<span data-ttu-id="256f6-116">The Azure IoT suite is a powerful solution for your IoT needs.</span><span class="sxs-lookup"><span data-stu-id="256f6-116">The Azure IoT suite is a powerful solution for your IoT needs.</span></span> <span data-ttu-id="256f6-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from the start.</span><span class="sxs-lookup"><span data-stu-id="256f6-117">However, it’s of upmost importance that your IoT solutions are designed with security in mind from the start.</span></span> <span data-ttu-id="256f6-118">Because of the sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span><span class="sxs-lookup"><span data-stu-id="256f6-118">Because of the sheer number of IoT devices, any security incident can quickly become a widespread event with significant consequences.</span></span>

<span data-ttu-id="256f6-119">To help you understand how to secure your IoT solutions, we have the following information.</span><span class="sxs-lookup"><span data-stu-id="256f6-119">To help you understand how to secure your IoT solutions, we have the following information.</span></span>

## <a name="security-architecture"></a><span data-ttu-id="256f6-120">Security architecture</span><span class="sxs-lookup"><span data-stu-id="256f6-120">Security architecture</span></span>
<span data-ttu-id="256f6-121">When designing a system, it is important to understand the potential threats to that system, and add appropriate defenses accordingly, as the system is designed and architected.</span><span class="sxs-lookup"><span data-stu-id="256f6-121">When designing a system, it is important to understand the potential threats to that system, and add appropriate defenses accordingly, as the system is designed and architected.</span></span> <span data-ttu-id="256f6-122">It is important to design the product from the start with security in mind because understanding how an attacker might be able to compromise a system helps make sure appropriate mitigations are in place from the beginning.</span><span class="sxs-lookup"><span data-stu-id="256f6-122">It is important to design the product from the start with security in mind because understanding how an attacker might be able to compromise a system helps make sure appropriate mitigations are in place from the beginning.</span></span>

<span data-ttu-id="256f6-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span><span class="sxs-lookup"><span data-stu-id="256f6-123">You can learn about IoT security architecture by reading [Internet of Things Security Architecture](../iot-suite/iot-security-architecture.md).</span></span>

<span data-ttu-id="256f6-124">This article discusses the following topics:</span><span class="sxs-lookup"><span data-stu-id="256f6-124">This article discusses the following topics:</span></span>

* [<span data-ttu-id="256f6-125">Security Starts with a Threat Model</span><span class="sxs-lookup"><span data-stu-id="256f6-125">Security Starts with a Threat Model</span></span>](../iot-suite/iot-security-architecture.md#security-starts-with-a-threat-model)
* [<span data-ttu-id="256f6-126">Security in IoT</span><span class="sxs-lookup"><span data-stu-id="256f6-126">Security in IoT</span></span>](../iot-suite/iot-security-architecture.md#security-in-iot)
* [<span data-ttu-id="256f6-127">Threat Modeling the Azure IoT Reference Architecture</span><span class="sxs-lookup"><span data-stu-id="256f6-127">Threat Modeling the Azure IoT Reference Architecture</span></span>](../iot-suite/iot-security-architecture.md#threat-modeling-the-azure-iot-reference-architecture)

## <a name="security-from-the-ground-up"></a><span data-ttu-id="256f6-128">Security from the ground up</span><span class="sxs-lookup"><span data-stu-id="256f6-128">Security from the ground up</span></span>
<span data-ttu-id="256f6-129">The IoT poses unique security, privacy, and compliance challenges to businesses worldwide.</span><span class="sxs-lookup"><span data-stu-id="256f6-129">The IoT poses unique security, privacy, and compliance challenges to businesses worldwide.</span></span> <span data-ttu-id="256f6-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when the cyber and the physical worlds converge.</span><span class="sxs-lookup"><span data-stu-id="256f6-130">Unlike traditional cyber technology where these issues revolve around software and how it is implemented, IoT concerns what happens when the cyber and the physical worlds converge.</span></span> <span data-ttu-id="256f6-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and the cloud, and secure data protection in the cloud during processing and storage.</span><span class="sxs-lookup"><span data-stu-id="256f6-131">Protecting IoT solutions requires ensuring secure provisioning of devices, secure connectivity between these devices and the cloud, and secure data protection in the cloud during processing and storage.</span></span> <span data-ttu-id="256f6-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span><span class="sxs-lookup"><span data-stu-id="256f6-132">Working against such functionality, however, are resource-constrained devices, geographic distribution of deployments, and many devices within a solution.</span></span>

<span data-ttu-id="256f6-133">You can learn how to handle security in these areas by reading [Internet of Things security from the ground up](../iot-suite/securing-iot-ground-up.md).</span><span class="sxs-lookup"><span data-stu-id="256f6-133">You can learn how to handle security in these areas by reading [Internet of Things security from the ground up](../iot-suite/securing-iot-ground-up.md).</span></span>

<span data-ttu-id="256f6-134">The article discusses the following topics:</span><span class="sxs-lookup"><span data-stu-id="256f6-134">The article discusses the following topics:</span></span>

* [<span data-ttu-id="256f6-135">Secure infrastructure from the ground up</span><span class="sxs-lookup"><span data-stu-id="256f6-135">Secure infrastructure from the ground up</span></span>](../iot-suite/securing-iot-ground-up.md#secure-infrastructure-from-the-ground-up)
* [<span data-ttu-id="256f6-136">Microsoft Azure – secure IoT infrastructure for your business</span><span class="sxs-lookup"><span data-stu-id="256f6-136">Microsoft Azure – secure IoT infrastructure for your business</span></span>](../iot-suite/securing-iot-ground-up.md#microsoft-azure---secure-iot-infrastructure-for-your-business)

## <a name="best-practices"></a><span data-ttu-id="256f6-137">Best Practices</span><span class="sxs-lookup"><span data-stu-id="256f6-137">Best Practices</span></span>
<span data-ttu-id="256f6-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span><span class="sxs-lookup"><span data-stu-id="256f6-138">Securing an IoT infrastructure requires a rigorous security-in-depth strategy.</span></span> <span data-ttu-id="256f6-139">From securing data in the cloud, protecting data integrity while in transit over the public internet, to securely provisioning devices, each layer builds greater security assurance in the overall infrastructure.</span><span class="sxs-lookup"><span data-stu-id="256f6-139">From securing data in the cloud, protecting data integrity while in transit over the public internet, to securely provisioning devices, each layer builds greater security assurance in the overall infrastructure.</span></span>

<span data-ttu-id="256f6-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span><span class="sxs-lookup"><span data-stu-id="256f6-140">You can learn about Internet of Things security best practices by reading [Internet of Things security best practices](../iot-suite/iot-security-best-practices.md).</span></span>

<span data-ttu-id="256f6-141">The article discusses the following topics:</span><span class="sxs-lookup"><span data-stu-id="256f6-141">The article discusses the following topics:</span></span>

* [<span data-ttu-id="256f6-142">IoT hardware manufacturer/integrator</span><span class="sxs-lookup"><span data-stu-id="256f6-142">IoT hardware manufacturer/integrator</span></span>](../iot-suite/iot-security-best-practices.md#iot-hardware-manufacturerintegrator)
* [<span data-ttu-id="256f6-143">IoT solution developer</span><span class="sxs-lookup"><span data-stu-id="256f6-143">IoT solution developer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-developer)
* [<span data-ttu-id="256f6-144">IoT solution deployer</span><span class="sxs-lookup"><span data-stu-id="256f6-144">IoT solution deployer</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-deployer)
* [<span data-ttu-id="256f6-145">IoT solution operator</span><span class="sxs-lookup"><span data-stu-id="256f6-145">IoT solution operator</span></span>](../iot-suite/iot-security-best-practices.md#iot-solution-operator)
