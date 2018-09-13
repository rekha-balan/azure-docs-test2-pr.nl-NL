---
title: Common parameters and headers
description: The parameters and headers common to all operations that you might do related to Key Vault resources.
services: key-vault
documentationcenter: ''
author: bryanla
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: a715d13ca9-d6e8-4e54-ac5e-0ed9400fb15b15d13ca9-d6e8-4e54-ac5e-0ed9400fb15b
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 05/09/2018
ms.author: bryanla
ms.openlocfilehash: dae5e1ab6244d2898bc218ed5db3b6b2b90150cf
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44866653"
---
# <a name="common-parameters-and-headers"></a>Common parameters and headers

The following information is common to all operations that you might do related to Key Vault resources:

- Replace `{api-version}` with the api-version in the URI.
- Replace `{subscription-id}` with your subscription identifier in the URI
- Replace `{resource-group-name}` with the resource group. For more information, see Using Resource groups to manage your Azure resources.
- Replace `{vault-name}` with your key vault name in the URI.
- Set the Content-Type header to application/json.
- Set the Authorization header to a JSON Web Token that you obtain from Azure Active Directory (AAD). For more information, see [Authenticating Azure Resource Manager](authentication-requests-and-responses.md) requests.

## <a name="common-error-response"></a>Common error response
The service will use HTTP status codes to indicate success or failure. In addition, failures contain a response in the following format:

   {  
     "error": {  
     "code": "BadRequest",  
     "message": "The key vault sku is invalid."  
     }  
   }  

|Element name | Type | Description |
|---|---|---|
| code | string | The type of error that occurred.|
| message | string | A description of what caused the error. |



## <a name="see-also"></a>See Also
 [Azure Key Vault REST API Reference](/rest/api/keyvault/)
