---
title: Create partners for business-to-business (B2B) messages - Azure Logic Apps | Microsoft Docs
description: Learn how to add partners to your integration account with the Enterprise Integration Pack and Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: ''
ms.assetid: b179325c-a511-4c1b-9796-f7484b4f6873
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/08/2016
ms.author: estfan
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 93b3d778d52c8d842b69d30c89853bf038189f04
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563037"
---
# <a name="add-or-update-partners-in-business-to-business-agreements-in-your-workflow"></a>Add or update partners in business-to-business agreements in your workflow

Partners are entities that participate in business-to-business (B2B) transactions and exchange messages between each other. Before you can create partners that represent you and another organization in these transactions, you must both share information that identifies and validates messages sent by each other. After you discuss these details and are ready to start your business relationship, you can create partners in your integration account to represent you both.

## <a name="what-roles-do-partners-have-in-your-integration-account"></a>What roles do partners have in your integration account?

To define details about the messages exchanged between partners, you create agreements between those partners. However, before you can create an agreement, you must have added at least two partners to your integration account. Your organization must be part of the agreement as the **host partner**. The other partner, or **guest partner** represents the organization that exchanges messages with your organization. The guest partner can be another company, or even a department in your own organization.

After you add these partners, you can create an agreement.

Receive and Send settings are oriented from the point of view of the Hosted Partner. For example, the receive settings in an agreement determine how the hosted partner receives messages sent from a guest partner. Likewise, the send settings on the agreement indicate how the hosted partner sends messages to the guest partner.

## <a name="how-to-create-a-partner"></a>How to create a partner?

1. In the Azure portal, select **Browse**.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-overview/overview-1.png)

2. In the filter search box, enter **integration**, then select **Integration Accounts** in the results list.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-overview/overview-2.png)

3. Select the integration account where you want to add your partners.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-overview/overview-3.png)

4. Select the **Partners** tile.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-1.png)

5. In the Partners blade, choose **Add**.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-2.png)

6. Enter a name for your partner, then select a **Qualifier**. Finally, enter a **Value** to help identify documents that come into your apps.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-3.png)

7. To see the progress for your partner creation process, select the *bell* notification icon.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-4.png)

8. To confirm that your new partners were successfully added, select the **Partners** tile.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-5.png)

    After you select the Partners tile, you'll also see  newly added partners in the Partners blade.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/partner-6.png)

## <a name="how-to-edit-existing-partners-in-your-integration-account"></a>How to edit existing partners in your integration account

1. Select the **Partners** tile.
2. After the Partners blade opens, select the partner you want to edit.
3. On the **Update Partner** tile, make your changes.
4. After you're done, choose **Save**, or to cancel your changes, select **Discard**.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/edit-1.png)

## <a name="how-to-delete-a-partner"></a>How to delete a partner

1. Select the **Partners** tile.
2. After the Partner blade opens, select the partner that you want to delete.
3. Choose **Delete**.

    ![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-partners/delete-1.png)

## <a name="next-steps"></a>Next steps
* [Learn more about agreements](../logic-apps/logic-apps-enterprise-integration-agreements.md "Learn about enterprise integration agreements")  












