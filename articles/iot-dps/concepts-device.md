---
title: Device concepts in Azure device provisioning | Microsoft Docs
description: Describes device provisioning concepts specific to devices with Device Provisioning Service and IoT Hub
author: nberdy
ms.author: nberdy
ms.date: 09/05/2017
ms.topic: conceptual
ms.service: iot-dps
services: iot-dps
manager: briz
ms.openlocfilehash: bd77a56acee948995bb2fcbb5beea60f69cda9ee
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44857152"
---
# <a name="iot-hub-device-provisioning-service-device-concepts"></a><span data-ttu-id="ccee9-103">IoT Hub Device Provisioning Service device concepts</span><span class="sxs-lookup"><span data-stu-id="ccee9-103">IoT Hub Device Provisioning Service device concepts</span></span>

<span data-ttu-id="ccee9-104">IoT Hub Device Provisioning Service is a helper service for IoT Hub that you use to configure zero-touch device provisioning to a specified IoT hub.</span><span class="sxs-lookup"><span data-stu-id="ccee9-104">IoT Hub Device Provisioning Service is a helper service for IoT Hub that you use to configure zero-touch device provisioning to a specified IoT hub.</span></span> <span data-ttu-id="ccee9-105">With the Device Provisioning Service, you can provision millions of devices in a secure and scalable manner.</span><span class="sxs-lookup"><span data-stu-id="ccee9-105">With the Device Provisioning Service, you can provision millions of devices in a secure and scalable manner.</span></span>

<span data-ttu-id="ccee9-106">This article gives an overview of the *device* concepts involved in device provisioning.</span><span class="sxs-lookup"><span data-stu-id="ccee9-106">This article gives an overview of the *device* concepts involved in device provisioning.</span></span> <span data-ttu-id="ccee9-107">This article is most relevant to personas involved in the [manufacturing step](about-iot-dps.md#manufacturing-step) of getting a device ready for deployment.</span><span class="sxs-lookup"><span data-stu-id="ccee9-107">This article is most relevant to personas involved in the [manufacturing step](about-iot-dps.md#manufacturing-step) of getting a device ready for deployment.</span></span>

## <a name="attestation-mechanism"></a><span data-ttu-id="ccee9-108">Attestation mechanism</span><span class="sxs-lookup"><span data-stu-id="ccee9-108">Attestation mechanism</span></span>

<span data-ttu-id="ccee9-109">The attestation mechanism is the method used for confirming a device's identity.</span><span class="sxs-lookup"><span data-stu-id="ccee9-109">The attestation mechanism is the method used for confirming a device's identity.</span></span> <span data-ttu-id="ccee9-110">The attestation mechanism is also relevant to the enrollment list, which tells the provisioning service which method of attestation to use with a given device.</span><span class="sxs-lookup"><span data-stu-id="ccee9-110">The attestation mechanism is also relevant to the enrollment list, which tells the provisioning service which method of attestation to use with a given device.</span></span>

> [!NOTE]
> <span data-ttu-id="ccee9-111">IoT Hub uses "authentication scheme" for a similar concept in that service.</span><span class="sxs-lookup"><span data-stu-id="ccee9-111">IoT Hub uses "authentication scheme" for a similar concept in that service.</span></span>

<span data-ttu-id="ccee9-112">The Device Provisioning Service supports two forms of attestation:</span><span class="sxs-lookup"><span data-stu-id="ccee9-112">The Device Provisioning Service supports two forms of attestation:</span></span>
* <span data-ttu-id="ccee9-113">**X.509 certificates** based on the standard X.509 certificate authentication flow.</span><span class="sxs-lookup"><span data-stu-id="ccee9-113">**X.509 certificates** based on the standard X.509 certificate authentication flow.</span></span>
* <span data-ttu-id="ccee9-114">**Trusted Platform Module (TPM)** based on a nonce challenge, using the TPM standard for keys to present a signed Shared Access Signature (SAS) token.</span><span class="sxs-lookup"><span data-stu-id="ccee9-114">**Trusted Platform Module (TPM)** based on a nonce challenge, using the TPM standard for keys to present a signed Shared Access Signature (SAS) token.</span></span> <span data-ttu-id="ccee9-115">This does not require a physical TPM on the device, but the service expects to attest using the endorsement key per the [TPM spec](https://trustedcomputinggroup.org/work-groups/trusted-platform-module/).</span><span class="sxs-lookup"><span data-stu-id="ccee9-115">This does not require a physical TPM on the device, but the service expects to attest using the endorsement key per the [TPM spec](https://trustedcomputinggroup.org/work-groups/trusted-platform-module/).</span></span>

## <a name="hardware-security-module"></a><span data-ttu-id="ccee9-116">Hardware security module</span><span class="sxs-lookup"><span data-stu-id="ccee9-116">Hardware security module</span></span>

<span data-ttu-id="ccee9-117">The hardware security module, or HSM, is used for secure, hardware-based storage of device secrets, and is the most secure form of secret storage.</span><span class="sxs-lookup"><span data-stu-id="ccee9-117">The hardware security module, or HSM, is used for secure, hardware-based storage of device secrets, and is the most secure form of secret storage.</span></span> <span data-ttu-id="ccee9-118">Both X.509 certificates and SAS tokens can be stored in the HSM.</span><span class="sxs-lookup"><span data-stu-id="ccee9-118">Both X.509 certificates and SAS tokens can be stored in the HSM.</span></span> <span data-ttu-id="ccee9-119">HSMs can be used with both attestation mechanisms the provisioning service supports.</span><span class="sxs-lookup"><span data-stu-id="ccee9-119">HSMs can be used with both attestation mechanisms the provisioning service supports.</span></span>

> [!TIP]
> <span data-ttu-id="ccee9-120">We strongly recommend using an HSM with devices to securely store secrets on your devices.</span><span class="sxs-lookup"><span data-stu-id="ccee9-120">We strongly recommend using an HSM with devices to securely store secrets on your devices.</span></span>

<span data-ttu-id="ccee9-121">Device secrets may also be stored in software (memory), but it is a less secure form of storage than an HSM.</span><span class="sxs-lookup"><span data-stu-id="ccee9-121">Device secrets may also be stored in software (memory), but it is a less secure form of storage than an HSM.</span></span>

## <a name="registration-id"></a><span data-ttu-id="ccee9-122">Registration ID</span><span class="sxs-lookup"><span data-stu-id="ccee9-122">Registration ID</span></span>

<span data-ttu-id="ccee9-123">The registration ID is used to uniquely identify a device in the Device Provisioning Service.</span><span class="sxs-lookup"><span data-stu-id="ccee9-123">The registration ID is used to uniquely identify a device in the Device Provisioning Service.</span></span> <span data-ttu-id="ccee9-124">The device ID must be unique in the provisioning service [ID scope](#id-scope).</span><span class="sxs-lookup"><span data-stu-id="ccee9-124">The device ID must be unique in the provisioning service [ID scope](#id-scope).</span></span> <span data-ttu-id="ccee9-125">Each device must have a registration ID.</span><span class="sxs-lookup"><span data-stu-id="ccee9-125">Each device must have a registration ID.</span></span> <span data-ttu-id="ccee9-126">The registration ID is alphanumeric, lowercase, and may contain hyphens.</span><span class="sxs-lookup"><span data-stu-id="ccee9-126">The registration ID is alphanumeric, lowercase, and may contain hyphens.</span></span>

* <span data-ttu-id="ccee9-127">In the case of TPM, the registration ID is provided by the TPM itself.</span><span class="sxs-lookup"><span data-stu-id="ccee9-127">In the case of TPM, the registration ID is provided by the TPM itself.</span></span>
* <span data-ttu-id="ccee9-128">In the case of X.509-based attestation, the registration ID is provided as the subject name of the certificate.</span><span class="sxs-lookup"><span data-stu-id="ccee9-128">In the case of X.509-based attestation, the registration ID is provided as the subject name of the certificate.</span></span>

## <a name="device-id"></a><span data-ttu-id="ccee9-129">Device ID</span><span class="sxs-lookup"><span data-stu-id="ccee9-129">Device ID</span></span>

<span data-ttu-id="ccee9-130">The device ID is the ID as it appears in IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="ccee9-130">The device ID is the ID as it appears in IoT Hub.</span></span> <span data-ttu-id="ccee9-131">The desired device ID may be set in the enrollment entry, but it is not required to be set.</span><span class="sxs-lookup"><span data-stu-id="ccee9-131">The desired device ID may be set in the enrollment entry, but it is not required to be set.</span></span> <span data-ttu-id="ccee9-132">If no desired device ID is specified in the enrollment list, the registration ID is used as the device ID when registering the device.</span><span class="sxs-lookup"><span data-stu-id="ccee9-132">If no desired device ID is specified in the enrollment list, the registration ID is used as the device ID when registering the device.</span></span> <span data-ttu-id="ccee9-133">Learn more about [device IDs in IoT Hub](../iot-hub/iot-hub-devguide-identity-registry.md).</span><span class="sxs-lookup"><span data-stu-id="ccee9-133">Learn more about [device IDs in IoT Hub](../iot-hub/iot-hub-devguide-identity-registry.md).</span></span>

## <a name="id-scope"></a><span data-ttu-id="ccee9-134">ID scope</span><span class="sxs-lookup"><span data-stu-id="ccee9-134">ID scope</span></span>

<span data-ttu-id="ccee9-135">The ID scope is assigned to a Device Provisioning Service when it is created by the user and is used to uniquely identify the specific provisioning service the device will register through.</span><span class="sxs-lookup"><span data-stu-id="ccee9-135">The ID scope is assigned to a Device Provisioning Service when it is created by the user and is used to uniquely identify the specific provisioning service the device will register through.</span></span> <span data-ttu-id="ccee9-136">The ID scope is generated by the service and is immutable, which guarantees uniqueness.</span><span class="sxs-lookup"><span data-stu-id="ccee9-136">The ID scope is generated by the service and is immutable, which guarantees uniqueness.</span></span>

> [!NOTE]
> <span data-ttu-id="ccee9-137">Uniqueness is important for long-running deployment operations and merger and acquisition scenarios.</span><span class="sxs-lookup"><span data-stu-id="ccee9-137">Uniqueness is important for long-running deployment operations and merger and acquisition scenarios.</span></span>
