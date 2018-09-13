---
title: Azure Kubernetes Service (AKS) quotas and region availability
description: The default quotas and region availability of the Azure Kubernetes Service (AKS).
services: container-service
author: iainfoulds
manager: jeconnoc
ms.service: container-service
ms.topic: overview
ms.date: 08/01/2018
ms.author: iainfou
ms.openlocfilehash: 266e2c1f986ba78c9aac40887bc9a7dee1cbff82
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866190"
---
# <a name="quotas-and-region-availability-for-azure-kubernetes-service-aks"></a>Quotas and region availability for Azure Kubernetes Service (AKS)

All Azure services include certain default limits and quotas for resources and features. The following sections detail the default resource limits for several Azure Kubernetes Service (AKS) resources, as well as the availability of the AKS service in Azure regions.

## <a name="service-quotas-and-limits"></a>Service quotas and limits

[!INCLUDE [container-service-limits](../../includes/container-service-limits.md)]

## <a name="provisioned-infrastructure"></a>Provisioned infrastructure

All other network, compute, and storage limitations apply to the provisioned infrastructure. See [Azure subscription and service limits](../azure-subscription-service-limits.md) for the relevant limits.

## <a name="region-availability"></a>Region availability

Azure Kubernetes Service (AKS) is available in the following regions:

- Australia East
- Canada Central
- Canada East
- Central US
- East US
- East US2
- Japan East
- North Europe
- Southeast Asia
- UK South
- West Europe
- West US
- West US 2

## <a name="next-steps"></a>Next steps

Certain default limits and quotas can be increased. To request an increase of one or more resources that support such an increase, submit an [Azure support request][azure-support] (select "Quota" for **Issue type**).

<!-- LINKS - External -->
[azure-support]: https://ms.portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest
