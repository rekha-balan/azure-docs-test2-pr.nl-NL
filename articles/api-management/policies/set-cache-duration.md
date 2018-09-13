---
title: Azure API managment policy sample - Set response cache duration | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to set response cache duration using maxAge value in Cache-Control header sent by the backend..
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
ms.openlocfilehash: 8f7126f5cd6bf6f142c603e4b1baee4a6c20dea2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44967667"
---
# <a name="set-response-cache-duration"></a>Set response cache duration

This article shows an Azure API management policy sample that demonstrates how to set response cache duration using maxAge value in Cache-Control header sent by the backend. To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md). To see other examples, see [policy samples](../policy-samples.md).

## <a name="policy"></a>Policy

Paste the code into the **inbound** block.

[!code-xml[Main](../../../api-management-policy-samples/examples/Set cache duration using response cache control header.policy.xml)]

## <a name="next-steps"></a>Next steps

Learn more about APIM policies:

+ [Transformation policies](../api-management-transformation-policies.md)
+ [Policy samples](../policy-samples.md)

