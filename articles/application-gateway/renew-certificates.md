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
# <a name="renew-application-gateway-certificates"></a>Renew Application Gateway certificates

At some point, you'll need to renew your certificates if you configured your application gateway for SSL encryption.

You can renew a certificate associated with a listener using either the Azure portal, Azure PowerShell, or Azure CLI:

## <a name="azure-portal"></a>Azure portal

To renew a listener certificate from the portal, navigate to your application gateway listeners. Click the listener that has a certificate that needs to be renewed, and then click **Renew or edit selected certificate**.

![Renew certificate](media/renew-certificate/ssl-cert.png)

Upload your new PFX certificate, give it a name, type the password, and then click **Save**.

## <a name="azure-powershell"></a>Azure PowerShell

To renew your certificate using Azure PowerShell, use the following script:

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
## <a name="azure-cli"></a>Azure CLI

```azurecli-interactive
az network application-gateway ssl-cert update \
  -n "<CertName>" \
  --gateway-name "<AppGatewayName>" \
  -g "ResourceGroupName>" \
  --cert-file <PathToCerFile> \
  --cert-password "<password>"
```

## <a name="next-steps"></a>Next steps

To learn how to configure SSL Offloading with Azure Application Gateway, see [Configure SSL Offload](application-gateway-ssl-portal.md)
