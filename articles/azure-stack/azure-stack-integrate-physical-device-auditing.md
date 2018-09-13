---
title: Azure Stack physical device auditing
description: Learn how to integrate physical device access auditing in Azure Stack
services: azure-stack
author: PatAltimore
manager: femila
ms.service: azure-stack
ms.topic: article
ms.date: 08/01/2018
ms.author: patricka
ms.reviewer: fiseraci
keywords: ''
ms.openlocfilehash: 459cdf4e1a70ee02d818dd6abe101e4fc3475b68
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44871103"
---
# <a name="azure-stack-datacenter-integration---physical-device-auditing"></a><span data-ttu-id="3d874-103">Azure Stack datacenter integration - physical device auditing</span><span class="sxs-lookup"><span data-stu-id="3d874-103">Azure Stack datacenter integration - physical device auditing</span></span>

<span data-ttu-id="3d874-104">All physical devices in Azure Stack, like the baseboard management controllers (BMCs) and network switches, emit audit logs, and they should be integrated into your overall auditing solution.</span><span class="sxs-lookup"><span data-stu-id="3d874-104">All physical devices in Azure Stack, like the baseboard management controllers (BMCs) and network switches, emit audit logs, and they should be integrated into your overall auditing solution.</span></span> <span data-ttu-id="3d874-105">Since the devices vary across the different Azure Stack OEM hardware vendors, contact your vendor for the documentation on auditing integration.</span><span class="sxs-lookup"><span data-stu-id="3d874-105">Since the devices vary across the different Azure Stack OEM hardware vendors, contact your vendor for the documentation on auditing integration.</span></span> <span data-ttu-id="3d874-106">The sections below provide some general information for physical device auditing in Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="3d874-106">The sections below provide some general information for physical device auditing in Azure Stack.</span></span>  

## <a name="physical-device-access-auditing"></a><span data-ttu-id="3d874-107">Physical device access auditing</span><span class="sxs-lookup"><span data-stu-id="3d874-107">Physical device access auditing</span></span>

<span data-ttu-id="3d874-108">All physical devices in Azure Stack support the use of TACACS or RADIUS.</span><span class="sxs-lookup"><span data-stu-id="3d874-108">All physical devices in Azure Stack support the use of TACACS or RADIUS.</span></span> <span data-ttu-id="3d874-109">This includes access to the baseboard management controller (BMC) and network switches.</span><span class="sxs-lookup"><span data-stu-id="3d874-109">This includes access to the baseboard management controller (BMC) and network switches.</span></span>

<span data-ttu-id="3d874-110">Azure Stack solutions do not ship with either RADIUS or TACACS built in.</span><span class="sxs-lookup"><span data-stu-id="3d874-110">Azure Stack solutions do not ship with either RADIUS or TACACS built in.</span></span> <span data-ttu-id="3d874-111">However, the solutions have been validated to support the use of existing RADIUS or TACACS solutions available in the market.</span><span class="sxs-lookup"><span data-stu-id="3d874-111">However, the solutions have been validated to support the use of existing RADIUS or TACACS solutions available in the market.</span></span>

<span data-ttu-id="3d874-112">For RADIUS only, MSCHAPv2 was validated.</span><span class="sxs-lookup"><span data-stu-id="3d874-112">For RADIUS only, MSCHAPv2 was validated.</span></span> <span data-ttu-id="3d874-113">This represents the most secure implementation using RADIUS.</span><span class="sxs-lookup"><span data-stu-id="3d874-113">This represents the most secure implementation using RADIUS.</span></span>
<span data-ttu-id="3d874-114">Consult with your OEM hardware vendor to enable TACAS or RADIUS in the devices included with your Azure Stack solution.</span><span class="sxs-lookup"><span data-stu-id="3d874-114">Consult with your OEM hardware vendor to enable TACAS or RADIUS in the devices included with your Azure Stack solution.</span></span>

## <a name="syslog-forwarding-for-network-devices"></a><span data-ttu-id="3d874-115">Syslog forwarding for network devices</span><span class="sxs-lookup"><span data-stu-id="3d874-115">Syslog forwarding for network devices</span></span>

<span data-ttu-id="3d874-116">All physical networking devices in Azure Stack support syslog messages.</span><span class="sxs-lookup"><span data-stu-id="3d874-116">All physical networking devices in Azure Stack support syslog messages.</span></span> <span data-ttu-id="3d874-117">Azure Stack solutions do not ship with a syslog server.</span><span class="sxs-lookup"><span data-stu-id="3d874-117">Azure Stack solutions do not ship with a syslog server.</span></span> <span data-ttu-id="3d874-118">However, the devices have been validated to support sending messages to existing syslog solutions available in the market.</span><span class="sxs-lookup"><span data-stu-id="3d874-118">However, the devices have been validated to support sending messages to existing syslog solutions available in the market.</span></span>

<span data-ttu-id="3d874-119">The syslog destination address is an optional parameter collected for deployment, but it can also be added post deployment.</span><span class="sxs-lookup"><span data-stu-id="3d874-119">The syslog destination address is an optional parameter collected for deployment, but it can also be added post deployment.</span></span> <span data-ttu-id="3d874-120">Consult with your OEM hardware vendor to configure syslog forwarding on your networking devices.</span><span class="sxs-lookup"><span data-stu-id="3d874-120">Consult with your OEM hardware vendor to configure syslog forwarding on your networking devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d874-121">Next steps</span><span class="sxs-lookup"><span data-stu-id="3d874-121">Next steps</span></span>

[<span data-ttu-id="3d874-122">Servicing policy</span><span class="sxs-lookup"><span data-stu-id="3d874-122">Servicing policy</span></span>](azure-stack-servicing-policy.md)
