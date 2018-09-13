---
title: Azure API managment policy sample - Implement X-CSRF pattern | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to implement X-CSRF pattern used by many APIs. This example is specific to SAP Gateway.
services: api-management
documentationcenter: ''
author: vladvino
manager: cfowler
editor: ''
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/13/2017
ms.author: apimpm
ms.openlocfilehash: 3a2067836a1488d117dced96f3935f2d1f8b1b48
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44858068"
---
# <a name="implement-x-csrf-pattern"></a>Implement X-CSRF pattern

This article shows an Azure API management policy sample that demonstrates how to implement X-CSRF pattern used by many APIs. This example is specific to SAP Gateway. To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md). To see other examples, see [policy samples](../policy-samples.md).

## <a name="policy"></a>Policy

Paste the code into the **inbound** block.

[!code-xml[Main](../../../api-management-policy-samples/examples/Get X-CSRF token from SAP gateway using send request.policy.xml)]

## <a name="next-steps"></a>Next steps

Learn more about APIM policies:

+ [Transformation policies](../api-management-transformation-policies.md)
+ [Policy samples](../policy-samples.md)

