---
title: Use Windows client images in Azure | Microsoft Docs
description: How to use Visual Studio subscription benefits to deploy Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios
services: virtual-machines-windows
documentationcenter: ''
author: iainfoulds
manager: timlt
editor: ''
ms.assetid: 91c3880a-cede-44f1-ae25-f8f9f5b6eaa4
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/14/2017
ms.author: iainfou
ms.openlocfilehash: 1954e37092d7d755522ebcccd9b52c56819c0a88
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44661438"
---
# <a name="use-windows-client-in-azure-for-devtest-scenarios"></a>Use Windows client in Azure for dev/test scenarios
You can use Windows 7, Windows 8, or Windows 10 in Azure for dev/test scenarios provided you have an appropriate Visual Studio (formerly MSDN) subscription. This article outlines the eligibility requirements for running Windows client in Azure and use of the Azure Gallery images.

## <a name="subscription-eligibility"></a>Subscription eligibility
Active Visual Studio subscribers (people who have acquired a Visual Studio subscription license) can use Windows client for development and testing purposes. Windows client can be used on your own hardware and Azure virtual machines running in any type of Azure subscription. Windows client may not be deployed to or used on Azure for normal production use, or used by people who are not active Visual Studio subscribers.

For your convenience, we have made certain Windows 10 images available from the Azure Gallery within [eligible dev/test offers](#eligible-offers). Visual Studio subscribers within any type of offer can also [adequately prepare and create](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a 64-bit Windows 7, Windows 8, or Windows 10 image and then [upload to Azure](upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). The use remains limited to dev/test by active Visual Studio subscribers.

## <a name="eligible-offers"></a>Eligible offers
The following table details the offer IDs that are eligible to deploy Windows 10 through the Azure Gallery. The Windows 10 images are only visible to the following offers. Visual Studio subscribers who need to run Windows client in a different offer type require you to [adequately prepare and create](prepare-for-upload-vhd-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) a 64-bit Windows 7, Windows 8, or Windows 10 image and [then upload to Azure](upload-image.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

| Offer Name | Offer Number | Available client images |
|:--- |:---:|:---:|
| [Pay-As-You-Go Dev/Test](https://azure.microsoft.com/offers/ms-azr-0023p/) |0023P |Windows 10 |
| [Visual Studio Enterprise (MPN) subscribers](https://azure.microsoft.com/offers/ms-azr-0029p/) |0029P |Windows 10 |
| [Visual Studio Professional subscribers](https://azure.microsoft.com/offers/ms-azr-0059p/) |0059P |Windows 10 |
| [Visual Studio Test Professional subscribers](https://azure.microsoft.com/offers/ms-azr-0060p/) |0060P |Windows 10 |
| [Visual Studio Premium with MSDN (benefit)](https://azure.microsoft.com/offers/ms-azr-0061p/) |0061P |Windows 10 |
| [Visual Studio Enterprise subscribers](https://azure.microsoft.com/offers/ms-azr-0063p/) |0063P |Windows 10 |
| [Visual Studio Enterprise (BizSpark) subscribers](https://azure.microsoft.com/offers/ms-azr-0064p/) |0064P |Windows 10 |
| [Enterprise Dev/Test](https://azure.microsoft.com/ofers/ms-azr-0148p/) |0148P |Windows 10 |

## <a name="check-your-azure-subscription"></a>Check your Azure subscription
If you do not know your offer ID, you can obtain it through the Azure portal or the Account portal.

The subscription offer ID is noted on the 'Subscriptions' blade within the Azure portal:

![Offer ID details from the Azure portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/client-images/offer_id_azure_portal.png) 

You can also view the offer ID from the ['Subscriptions' tab](http://account.windowsazure.com/Subscriptions) of the Azure Account portal:

![Offer ID details from the Azure Account portal](https://docstestmedia1.blob.core.windows.net/azure-media/articles/virtual-machines/windows/media/client-images/offer_id_azure_account_portal.png) 

## <a name="next-steps"></a>Next steps
You can now deploy your VMs using [PowerShell](../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), [Resource Manager templates](ps-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), or [Visual Studio](../../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).



