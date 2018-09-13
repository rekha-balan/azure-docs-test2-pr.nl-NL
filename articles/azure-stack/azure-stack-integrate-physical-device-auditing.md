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
# <a name="azure-stack-datacenter-integration---physical-device-auditing"></a>Azure Stack datacenter integration - physical device auditing

All physical devices in Azure Stack, like the baseboard management controllers (BMCs) and network switches, emit audit logs, and they should be integrated into your overall auditing solution. Since the devices vary across the different Azure Stack OEM hardware vendors, contact your vendor for the documentation on auditing integration. The sections below provide some general information for physical device auditing in Azure Stack.  

## <a name="physical-device-access-auditing"></a>Physical device access auditing

All physical devices in Azure Stack support the use of TACACS or RADIUS. This includes access to the baseboard management controller (BMC) and network switches.

Azure Stack solutions do not ship with either RADIUS or TACACS built in. However, the solutions have been validated to support the use of existing RADIUS or TACACS solutions available in the market.

For RADIUS only, MSCHAPv2 was validated. This represents the most secure implementation using RADIUS.
Consult with your OEM hardware vendor to enable TACAS or RADIUS in the devices included with your Azure Stack solution.

## <a name="syslog-forwarding-for-network-devices"></a>Syslog forwarding for network devices

All physical networking devices in Azure Stack support syslog messages. Azure Stack solutions do not ship with a syslog server. However, the devices have been validated to support sending messages to existing syslog solutions available in the market.

The syslog destination address is an optional parameter collected for deployment, but it can also be added post deployment. Consult with your OEM hardware vendor to configure syslog forwarding on your networking devices.

## <a name="next-steps"></a>Next steps

[Servicing policy](azure-stack-servicing-policy.md)
