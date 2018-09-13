---
title: Azure API managment policy sample - Filter response content | Microsoft Docs
description: Azure API managment policy sample - Demonstrates how to filter data elements from the response payload based on the product associated with the request.
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
ms.openlocfilehash: af362ac51fb8b7d1689451d49f2ed831c5f9ee2e
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44868524"
---
# <a name="filter-response-content"></a>Filter response content

This article shows an Azure API management policy sample that demonstrates how to filter data elements from the response payload based on the product associated with the request. To set or edit a policy code, follow the steps described in [Set or edit a policy](../set-edit-policies.md). To see other examples, see [policy samples](../policy-samples.md).

## <a name="policy"></a>Policy

Paste the code into the **outbound** block.

[!code-xml[Main](../../../api-management-policy-samples/examples/Filter response content based on product name.policy.xml)]

## <a name="next-steps"></a>Next steps

Learn more about APIM policies:

+ [Transformation policies](../api-management-transformation-policies.md)
+ [Policy samples](../policy-samples.md)

