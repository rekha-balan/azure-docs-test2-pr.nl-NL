---
title: Secure your Internet of Things deployment | Microsoft Docs
description: This article details how to secure your IoT deployment
author: dominicbetts
manager: timlt
ms.service: iot-accelerators
services: iot-accelerators
ms.topic: conceptual
ms.date: 01/17/2018
ms.author: dobett
ms.openlocfilehash: 00acb08f567dbd50522d0e8a0b7b9a18a6658000
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44856703"
---
[!INCLUDE [iot-secure-your-deployment](../../includes/iot-secure-your-deployment.md)]

## <a name="iot-solution-accelerator-cipher-suites"></a><span data-ttu-id="cf776-103">IoT solution accelerator cipher suites</span><span class="sxs-lookup"><span data-stu-id="cf776-103">IoT solution accelerator cipher suites</span></span>

<span data-ttu-id="cf776-104">The IoT solution accelerators support the following Cipher Suites, in this order.</span><span class="sxs-lookup"><span data-stu-id="cf776-104">The IoT solution accelerators support the following Cipher Suites, in this order.</span></span>

| <span data-ttu-id="cf776-105">Cipher Suite</span><span class="sxs-lookup"><span data-stu-id="cf776-105">Cipher Suite</span></span> | <span data-ttu-id="cf776-106">Length</span><span class="sxs-lookup"><span data-stu-id="cf776-106">Length</span></span> |
| --- | --- |
| <span data-ttu-id="cf776-107">TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (eq.</span><span class="sxs-lookup"><span data-stu-id="cf776-107">TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA384 (0xc028) ECDH secp384r1 (eq.</span></span> <span data-ttu-id="cf776-108">7680 bits RSA) FS</span><span class="sxs-lookup"><span data-stu-id="cf776-108">7680 bits RSA) FS</span></span> |<span data-ttu-id="cf776-109">256</span><span class="sxs-lookup"><span data-stu-id="cf776-109">256</span></span> |
| <span data-ttu-id="cf776-110">TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (eq.</span><span class="sxs-lookup"><span data-stu-id="cf776-110">TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0xc027) ECDH secp256r1 (eq.</span></span> <span data-ttu-id="cf776-111">3072 bits RSA) FS</span><span class="sxs-lookup"><span data-stu-id="cf776-111">3072 bits RSA) FS</span></span> |<span data-ttu-id="cf776-112">128</span><span class="sxs-lookup"><span data-stu-id="cf776-112">128</span></span> |
| <span data-ttu-id="cf776-113">TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (eq.</span><span class="sxs-lookup"><span data-stu-id="cf776-113">TLS\_ECDHE\_RSA\_WITH\_AES\_256\_CBC\_SHA (0xc014) ECDH secp384r1 (eq.</span></span> <span data-ttu-id="cf776-114">7680 bits RSA) FS</span><span class="sxs-lookup"><span data-stu-id="cf776-114">7680 bits RSA) FS</span></span> |<span data-ttu-id="cf776-115">256</span><span class="sxs-lookup"><span data-stu-id="cf776-115">256</span></span> |
| <span data-ttu-id="cf776-116">TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (eq.</span><span class="sxs-lookup"><span data-stu-id="cf776-116">TLS\_ECDHE\_RSA\_WITH\_AES\_128\_CBC\_SHA (0xc013) ECDH secp256r1 (eq.</span></span> <span data-ttu-id="cf776-117">3072 bits RSA) FS</span><span class="sxs-lookup"><span data-stu-id="cf776-117">3072 bits RSA) FS</span></span> |<span data-ttu-id="cf776-118">128</span><span class="sxs-lookup"><span data-stu-id="cf776-118">128</span></span> |
| <span data-ttu-id="cf776-119">TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d)</span><span class="sxs-lookup"><span data-stu-id="cf776-119">TLS\_RSA\_WITH\_AES\_256\_GCM\_SHA384 (0x9d)</span></span> |<span data-ttu-id="cf776-120">256</span><span class="sxs-lookup"><span data-stu-id="cf776-120">256</span></span> |
| <span data-ttu-id="cf776-121">TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c)</span><span class="sxs-lookup"><span data-stu-id="cf776-121">TLS\_RSA\_WITH\_AES\_128\_GCM\_SHA256 (0x9c)</span></span> |<span data-ttu-id="cf776-122">128</span><span class="sxs-lookup"><span data-stu-id="cf776-122">128</span></span> |
| <span data-ttu-id="cf776-123">TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d)</span><span class="sxs-lookup"><span data-stu-id="cf776-123">TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA256 (0x3d)</span></span> |<span data-ttu-id="cf776-124">256</span><span class="sxs-lookup"><span data-stu-id="cf776-124">256</span></span> |
| <span data-ttu-id="cf776-125">TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c)</span><span class="sxs-lookup"><span data-stu-id="cf776-125">TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA256 (0x3c)</span></span> |<span data-ttu-id="cf776-126">128</span><span class="sxs-lookup"><span data-stu-id="cf776-126">128</span></span> |
| <span data-ttu-id="cf776-127">TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35)</span><span class="sxs-lookup"><span data-stu-id="cf776-127">TLS\_RSA\_WITH\_AES\_256\_CBC\_SHA (0x35)</span></span> |<span data-ttu-id="cf776-128">256</span><span class="sxs-lookup"><span data-stu-id="cf776-128">256</span></span> |
| <span data-ttu-id="cf776-129">TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f)</span><span class="sxs-lookup"><span data-stu-id="cf776-129">TLS\_RSA\_WITH\_AES\_128\_CBC\_SHA (0x2f)</span></span> |<span data-ttu-id="cf776-130">128</span><span class="sxs-lookup"><span data-stu-id="cf776-130">128</span></span> |
| <span data-ttu-id="cf776-131">TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa)</span><span class="sxs-lookup"><span data-stu-id="cf776-131">TLS\_RSA\_WITH\_3DES\_EDE\_CBC\_SHA (0xa)</span></span> |<span data-ttu-id="cf776-132">112</span><span class="sxs-lookup"><span data-stu-id="cf776-132">112</span></span> |

## <a name="see-also"></a><span data-ttu-id="cf776-133">See also</span><span class="sxs-lookup"><span data-stu-id="cf776-133">See also</span></span>

<span data-ttu-id="cf776-134">Read about IoT Hub security in [Control access to IoT Hub](../iot-hub/iot-hub-devguide-security.md) in the IoT Hub developer guide.</span><span class="sxs-lookup"><span data-stu-id="cf776-134">Read about IoT Hub security in [Control access to IoT Hub](../iot-hub/iot-hub-devguide-security.md) in the IoT Hub developer guide.</span></span> 
