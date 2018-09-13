---
title: Renew an Azure Application Gateway certificate
description: Learn how to renew a certificate associated with an application gateway listener.
services: application-gateway
author: vhorne
manager: jpconnock
ms.service: application-gateway
ms.topic: article
ms.date: 8/15/2018
ms.author: victorh
ms.openlocfilehash: 48bd548ec977d2dc4dd3b5b2f34df04562a6e918
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967273"
---
# <a name="renew-application-gateway-certificates"></a><span data-ttu-id="9b684-103">Renew Application Gateway certificates</span><span class="sxs-lookup"><span data-stu-id="9b684-103">Renew Application Gateway certificates</span></span>

<span data-ttu-id="9b684-104">At some point, you'll need to renew your certificates if you configured your application gateway for SSL encryption.</span><span class="sxs-lookup"><span data-stu-id="9b684-104">At some point, you'll need to renew your certificates if you configured your application gateway for SSL encryption.</span></span>

<span data-ttu-id="9b684-105">You can renew a certificate associated with a listener using either the Azure portal, Azure PowerShell, or Azure CLI:</span><span class="sxs-lookup"><span data-stu-id="9b684-105">You can renew a certificate associated with a listener using either the Azure portal, Azure PowerShell, or Azure CLI:</span></span>

## <a name="azure-portal"></a><span data-ttu-id="9b684-106">Azure portal</span><span class="sxs-lookup"><span data-stu-id="9b684-106">Azure portal</span></span>

<span data-ttu-id="9b684-107">To renew a listener certificate from the portal, navigate to your application gateway listeners.</span><span class="sxs-lookup"><span data-stu-id="9b684-107">To renew a listener certificate from the portal, navigate to your application gateway listeners.</span></span> <span data-ttu-id="9b684-108">Click the listener that has a certificate that needs to be renewed, and then click **Renew or edit selected certificate**.</span><span class="sxs-lookup"><span data-stu-id="9b684-108">Click the listener that has a certificate that needs to be renewed, and then click **Renew or edit selected certificate**.</span></span>

![Renew certificate](media/renew-certificate/ssl-cert.png)

<span data-ttu-id="9b684-110">Upload your new PFX certificate, give it a name, type the password, and then click **Save**.</span><span class="sxs-lookup"><span data-stu-id="9b684-110">Upload your new PFX certificate, give it a name, type the password, and then click **Save**.</span></span>

## <a name="azure-powershell"></a><span data-ttu-id="9b684-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="9b684-111">Azure PowerShell</span></span>

<span data-ttu-id="9b684-112">To renew your certificate using Azure PowerShell, use the following script:</span><span class="sxs-lookup"><span data-stu-id="9b684-112">To renew your certificate using Azure PowerShell, use the following script:</span></span>

```azurepowershell-interactive
$appgw = Get-AzureRmApplicationGateway `
  -ResourceGroupName <ResourceGroup> `
  -Name <AppGatewayName>

$password = ConvertTo-SecureString `
  -String "<password>" `
  -Force `
  -AsPlainText

set-azureRmApplicationGatewaySSLCertificate -Name <oldcertname> `
-ApplicationGateway $appgw -CertificateFile <newcertPath> -Password $password

Set-AzureRmApplicationGateway -ApplicationGateway $appgw
```
## <a name="azure-cli"></a><span data-ttu-id="9b684-113">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="9b684-113">Azure CLI</span></span>

```azurecli-interactive
az network application-gateway ssl-cert update \
  -n "<CertName>" \
  --gateway-name "<AppGatewayName>" \
  -g "ResourceGroupName>" \
  --cert-file <PathToCerFile> \
  --cert-password "<password>"
```

## <a name="next-steps"></a><span data-ttu-id="9b684-114">Next steps</span><span class="sxs-lookup"><span data-stu-id="9b684-114">Next steps</span></span>

<span data-ttu-id="9b684-115">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span><span class="sxs-lookup"><span data-stu-id="9b684-115">To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)</span></span>
