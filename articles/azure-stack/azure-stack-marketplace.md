---
title: Publish a custom marketplace item in Azure Stack (service administrator) | Microsoft Docs
description: As a service administrator, learn how to publish a custom marketplace item in Azure Stack.
services: azure-stack
documentationcenter: ''
author: rupisure
manager: byronr
editor: ''
ms.assetid: 60871cbb-eed2-433c-a76d-d605c7aec06c
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/26/2016
ms.author: rupisure
ms.openlocfilehash: cf55ddab05fefa5b7a1b96ef2f02bcb0f83894c2
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44552557"
---
# <a name="the-azure-stack-marketplace"></a>The Azure Stack Marketplace
The Marketplace is a collection of items customized for Azure Stack, like services, applications, and resources. It's the place where tenants come to create new resources and deploy new applications. Service administrators can add custom items to the Marketplace and tenants will see them right away.

To open the Marketplace, click **New**.

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/azure-stack/media/azure-stack-publish-custom-marketplace-item/image1.png)

The Marketplace is updated every five minutes.

## <a name="marketplace-items"></a>Marketplace items
Every Marketplace item has:

* An Azure Resource Manager template for resource provisioning
* Metadata, like strings, icons, and other marketing collateral
* Formatting information to display the item in the portal

Every item published to the Marketplace uses a format called the Azure Gallery Package (azpkg). Deployment or runtime resources (like code, zip files with software, or virtual machine images) should be added to Azure Stack separately, not as part of the Marketplace Item. 

## <a name="next-steps"></a>Next steps
[Create and publish a marketplace item](azure-stack-create-and-publish-marketplace-item.md)


