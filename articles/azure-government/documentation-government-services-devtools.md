---
title: Azure Government Developer Tools | Microsoft Docs
description: This provides a comparison of features and guidance on developing applications for Azure Government.
services: azure-government
cloud: gov
documentationcenter: ''
author: gsacavdm
manager: pathuff
ms.assetid: 4b7720c1-699e-432b-9246-6e49fb77f497
ms.service: azure-government
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: azure-government
ms.date: 3/30/2018
ms.author: gsacavdm
ms.openlocfilehash: 012e9e8e4d84845edef2983876cbeac6f2293e13
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869966"
---
# <a name="azure-government-developer-tools"></a>Azure Government Developer Tools
This article outlines the developer tools services variations and considerations for the Azure Government environment.

## <a name="devtest-labs"></a>DevTest Labs
DevTest Labs is generally available in Azure Government.
For more information, see [DevTest Labs public documentation](../lab-services/devtest-lab-overview.md).

### <a name="variations"></a>Variations
The following DevTest Labs features are not currently available in Azure Government:
* [Azure Resource Manager templates to create multi-VM environments and PaaS resources within a Lab](../lab-services/devtest-lab-create-environment-from-arm.md).
* Connect to an external GitHub repository to add Azure Resource Manager Templates, however [adding artifact repositories to leverage custom artifacts](../lab-services/devtest-lab-add-artifact-repo.md) is available.
* Auto shutdown feature for Azure compute VMs, however, setting auto shutdown for [Labs](https://azure.microsoft.com/updates/azure-devtest-labs-auto-shutdown-notification/) and [Lab Virtual Machines](https://azure.microsoft.com/updates/azure-devtest-labs-set-auto-shutdown-for-a-single-lab-vm/) is available.  
 

## <a name="next-steps"></a>Next steps
* Subscribe to the [Azure Government blog](https://blogs.msdn.microsoft.com/azuregov/)
* Get help on Stack Overflow by using the [azure-gov](https://stackoverflow.com/questions/tagged/azure-gov)
* Give feedback or request new features via the [Azure Government feedback forum](https://feedback.azure.com/forums/558487-azure-government) 
