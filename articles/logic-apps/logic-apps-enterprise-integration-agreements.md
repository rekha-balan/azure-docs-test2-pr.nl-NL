---
title: Agreements for B2B communication - Azure Logic Apps | Microsoft Docs
description: Create agreements for B2B trading partner communication with Azure Logic Apps and Enterprise Integration Pack
services: logic-apps
ms.service: logic-apps
ms.suite: integration
author: divyaswarnkar
ms.author: divswa
ms.reviewer: jonfan, estfan, LADocs
ms.topic: article
ms.assetid: 447ffb8e-3e91-4403-872b-2f496495899d
ms.date: 06/29/2016
ms.openlocfilehash: 09bee10649e2bc0d745e42b8aa13ae9c21df35aa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44772934"
---
# <a name="partner-agreements-for-b2b-communication-with-azure-logic-apps-and-enterprise-integration-pack"></a>Partner agreements for B2B communication with Azure Logic Apps and Enterprise Integration Pack

Agreements let business entities communicate seamlessly using industry standard protocols and are the cornerstone for business-to-business (B2B) communication. When enabling B2B scenarios for logic apps with the Enterprise Integration Pack, an agreement is a communications arrangement between B2B trading partners. This agreement is based on the communications that the partners want to establish and is protocol or transport-specific.

Enterprise integration supports these protocol or transport standards:

* [AS2](logic-apps-enterprise-integration-as2.md)
* [X12](logic-apps-enterprise-integration-x12.md)
* [EDIFACT](logic-apps-enterprise-integration-edifact.md)

## <a name="why-use-agreements"></a>Why use agreements

Here are some common benefits when using agreements:

* Enables different organizations and businesses to exchange information in a well-known format.
* Improves efficiency when conducting B2B transactions
* Easy to create, manage, and use when creating enterprise integration apps

## <a name="how-to-create-agreements"></a>How to create agreements

* [Create an AS2 agreement](logic-apps-enterprise-integration-as2.md)
* [Create an X12 agreement](logic-apps-enterprise-integration-x12.md)
* [Create an EDIFACT agreement](logic-apps-enterprise-integration-edifact.md)

## <a name="how-to-use-an-agreement"></a>How to use an agreement

You can create [logic apps](logic-apps-overview.md "Learn about Logic apps") with B2B capabilities by using an agreement that you created.

## <a name="how-to-edit-an-agreement"></a>How to edit an agreement

You can edit any agreement by following these steps:

1. Select the integration account that has the agreement you want to update.

2. Choose the **Agreements** tile.

3. On the **Agreements** blade, select the agreement.

4. Choose **Edit**. Make your changes.

5. To save your changes, choose **OK**.

## <a name="how-to-delete-an-agreement"></a>How to delete an agreement

You can delete any agreement by following these steps:

1. Select the integration account that has the agreement you want to delete.
2. Choose the **Agreements** tile.
3. On the **Agreements** blade, select the agreement.
4. Choose **Delete**.
5. Confirm that you want to delete the selected agreement.

    The Agreements blade no longer shows the deleted agreement.

## <a name="next-steps"></a>Next steps
* [Create an AS2 agreement](logic-apps-enterprise-integration-as2.md)
