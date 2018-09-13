---
title: Enable the Azure Firewall public preview
description: Use Azure PowerShell to enable the Azure Firewall public preview
author: vhorne
ms.service: firewall
services: firewall
ms.topic: article
ms.date: 7/11/2018
ms.author: victorh
ms.openlocfilehash: 263b16a419b5ff20a9b6d62860385f92c2a18f9c
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967979"
---
# <a name="enable-the-azure-firewall-public-preview"></a><span data-ttu-id="fef09-103">Enable the Azure Firewall public preview</span><span class="sxs-lookup"><span data-stu-id="fef09-103">Enable the Azure Firewall public preview</span></span>

[!INCLUDE [firewall-preview-notice](../../includes/firewall-preview-notice.md)]

## <a name="enable-using-azure-powershell"></a><span data-ttu-id="fef09-104">Enable using Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="fef09-104">Enable using Azure PowerShell</span></span>

<span data-ttu-id="fef09-105">To enable the Azure Firewall public preview, use the following Azure PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="fef09-105">To enable the Azure Firewall public preview, use the following Azure PowerShell commands:</span></span>

```PowerShell
Register-AzureRmProviderFeature -FeatureName AllowRegionalGatewayManagerForSecureGateway -ProviderNamespace Microsoft.Network

Register-AzureRmProviderFeature -FeatureName AllowAzureFirewall -ProviderNamespace Microsoft.Network
```

<span data-ttu-id="fef09-106">It takes up to 30 minutes for feature registration to complete.</span><span class="sxs-lookup"><span data-stu-id="fef09-106">It takes up to 30 minutes for feature registration to complete.</span></span> <span data-ttu-id="fef09-107">You can check your registration status by running the following Azure PowerShell commands:</span><span class="sxs-lookup"><span data-stu-id="fef09-107">You can check your registration status by running the following Azure PowerShell commands:</span></span>

```PowerShell

Get-AzureRmProviderFeature -FeatureName AllowRegionalGatewayManagerForSecureGateway -ProviderNamespace Microsoft.Network

Get-AzureRmProviderFeature -FeatureName AllowAzureFirewall -ProviderNamespace Microsoft.Network
```
<span data-ttu-id="fef09-108">After the registration is complete, run the following command:</span><span class="sxs-lookup"><span data-stu-id="fef09-108">After the registration is complete, run the following command:</span></span>

```PowerShell
Register-AzureRmResourceProvider -ProviderNamespace Microsoft.Network
```

## <a name="next-steps"></a><span data-ttu-id="fef09-109">Next steps</span><span class="sxs-lookup"><span data-stu-id="fef09-109">Next steps</span></span>

- [<span data-ttu-id="fef09-110">Tutorial: Deploy and configure Azure Firewall using the Azure portal</span><span class="sxs-lookup"><span data-stu-id="fef09-110">Tutorial: Deploy and configure Azure Firewall using the Azure portal</span></span>](tutorial-firewall-deploy-portal.md)

