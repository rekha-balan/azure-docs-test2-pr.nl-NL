---
title: Manage integration account artifact metadata - Azure Logic Apps | Microsoft Docs
description: Add or retrieve artifact metadata from integration accounts for Azure Logic Apps
author: padmavc
manager: anneta
editor: ''
services: logic-apps
documentationcenter: ''
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 11/21/2016
ms.author: padmavc
ms.openlocfilehash: 25623fe8585b696e2c88cb564c60cd442c150f3c
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44660977"
---
# <a name="manage-artifact-metadata-in-integration-accounts-for-logic-apps"></a>Manage artifact metadata in integration accounts for logic apps

You can define custom metadata for artifacts in integration accounts and retrieve that metadata during runtime for your logic app. For example, you can specify metadata for artifacts like partners, agreements, schemas, and maps - all store metadata using key-value pairs. Currently, artifacts can't create metadata through UI, but you can use REST APIs to create metadata. To add metadata when you create or select a partner, agreement, or schema in the Azure portal, choose **Edit as JSON**. To retrieve artifact metadata in logic apps, you can use the Integration Account Artifact Lookup feature.

## <a name="add-metadata-to-artifacts-in-integration-accounts"></a>Add metadata to artifacts in integration accounts

1. Create an [integration account](logic-apps-enterprise-integration-create-integration-account.md).

2. Add an artifact to your integration account, for example, a [partner](logic-apps-enterprise-integration-partners.md#how-to-create-a-partner), [agreement](logic-apps-enterprise-integration-agreements.md#how-to-create-agreements), or [schema](logic-apps-enterprise-integration-schemas.md).

3.  Select the artifact, choose **Edit as JSON**, and enter metadata details.

    ![Enter metadata](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image1.png)

## <a name="retrieve-metadata-from-artifacts-for-logic-apps"></a>Retrieve metadata from artifacts for logic apps

1. Create a [logic app](logic-apps-create-a-logic-app.md).

2. Create a [link from your logic app to your integration account](logic-apps-enterprise-integration-create-integration-account.md#link-an-integration-account-to-a-logic-app). 

3. In Logic App Designer, add a trigger like *Request* or *HTTP* to your logic app.

4.  Choose **Next Step** > **Add an action**. Search for *integration* so you can find and then select **Integration Account - Integration Account Artifact Lookup**.

    ![Select Integration Account Artifact Lookup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image2.png)

5. Select the **Artifact Type**, and provide the **Artifact Name**.

    ![Select artifact type and specify artifact name](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image3.png)

## <a name="example-retrieve-partner-metadata"></a>Example: Retrieve partner metadata

Partner metadata has these `routingUrl` details:

![Find partner "routingURL" metadata](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image6.png)

1. In your logic app, add your trigger, an **Integration Account - Integration Account Artifact Lookup** action for your partner, and an **HTTP**.

    ![Add trigger, artifact lookup, and "HTTP" to your logic app](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image4.png)

2. To retrieve the URI, go to Code View for your logic app. Your logic app definition should look like this example:

    ![Search lookup](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-metadata/image5.png)


## <a name="next-steps"></a>Next steps
* [Learn more about agreements](logic-apps-enterprise-integration-agreements.md "Learn about enterprise integration agreements")  






