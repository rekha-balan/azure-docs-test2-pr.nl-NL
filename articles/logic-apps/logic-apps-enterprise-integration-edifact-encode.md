---
title: Encode EDIFACT messages - Azure Logic Apps | Microsoft Docs
description: Validate EDI and generate XML with EDIFACT message encoder in the Enterprise Integration Pack for Azure Logic Apps
services: logic-apps
documentationcenter: .net,nodejs,java
author: padmavc
manager: anneta
editor: ''
ms.assetid: 974ac339-d97a-4715-bc92-62d02281e900
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: padmavc
ms.openlocfilehash: b0fe1902a75927a7cd92acbe2ae782996784dfe1
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563039"
---
# <a name="encode-edifact-messages-for-azure-logic-apps-with-the-enterprise-integration-pack"></a>Encode EDIFACT messages for Azure Logic Apps with the Enterprise Integration Pack

With the Encode EDIFACT message connector, you can validate EDI and partner-specific properties, generate an XML document for each transaction set, and request a Technical Acknowledgement, Functional Acknowledgment, or both.
To use this connector, you must add the connector to an existing trigger in your logic app.

## <a name="before-you-start"></a>Before you start

Here's the items you need:

* An Azure account; you can create a [free account](https://azure.microsoft.com/free)
* An [integration account](logic-apps-enterprise-integration-create-integration-account.md) that's already defined and associated with your Azure subscription. You must have an integration account to use the Encode EDIFACT message connector. 
* At least two [partners](logic-apps-enterprise-integration-partners.md) that are already defined in your integration account
* An [EDIFACT agreement](logic-apps-enterprise-integration-edifact.md) that's already defined in your integration account

## <a name="encode-edifact-messages"></a>Encode EDIFACT messages

1. [Create a logic app](logic-apps-create-a-logic-app.md).

2. The Encode EDIFACT message connector doesn't have triggers, so you must add a trigger for starting your logic app, like a Request trigger. In the Logic App Designer, add a trigger, and then add an action to your logic app.

3.  In the search box, enter "EDIFACT" as your filter. Select either **Encode EDIFACT Message by agreement name** or **Encode to EDIFACT message by identities**.
   
    ![search EDIFACT](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactdecodeimage1.png)  

3. If you didn't previously create any connections to your integration account, you're prompted to create that connection now. Name your connection, and select the integration account that you want to connect.

    ![create integration account connection](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage1.png)  

    Properties with an asterisk are required.

    | Property | Details |
    | --- | --- |
    | Connection Name * |Enter any name for your connection. |
    | Integration Account * |Enter a name for your integration account. Make sure that your integration account and logic app are in the same Azure location. |

5.  When you're done, your connection details should look similar to this example. To finish creating your connection, choose **Create**.

    ![integration account connection details](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage2.png)

    Your connection is now created.

    ![integration account connection created](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage4.png)

#### <a name="encode-edifact-message-by-agreement-name"></a>Encode EDIFACT Message by agreement name

If you chose to encode EDIFACT messages by agreement name, open the **Name of EDIFACT agreement** list, enter or select your EDIFACT agreement name. Enter the XML message to encode.

![Enter EDIFACT agreement name and XML message to encode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage6.png)

#### <a name="encode-edifact-message-by-identities"></a>Encode EDIFACT Message by identities

If you choose to encode EDIFACT messages by identities, enter the sender identifier, sender qualifier, receiver identifier, and receiver qualifier as configured in your EDIFACT agreement. Select the XML message to encode.

![Provide identities for sender and receiver, select XML message to encode](https://docstestmedia1.blob.core.windows.net/azure-media/articles/logic-apps/media/logic-apps-enterprise-integration-edifact-encode/edifactencodeimage7.png)

## <a name="edifact-encode-details"></a>EDIFACT Encode details

The Encode EDIFACT connector performs these tasks: 

* Resolve the agreement by matching the sender qualifier & identifier and receiver qualifier and identifier
* Serializes the EDI interchange, converting XML-encoded messages into EDI transaction sets in the interchange.
* Applies transaction set header and trailer segments
* Generates an interchange control number, a group control number, and a transaction set control number for each outgoing interchange
* Replaces separators in the payload data
* Validates EDI and partner-specific properties
  * Schema validation of the transaction-set data elements against the message schema.
  * EDI validation performed on transaction-set data elements.
  * Extended validation performed on transaction-set data elements
* Generates an XML document for each transaction set.
* Requests a Technical and/or Functional acknowledgment (if configured).
  * As a technical acknowledgment, the CONTRL message indicates receipt of an interchange.
  * As a functional acknowledgment, the CONTRL message indicates acceptance or rejection of the received interchange, group, or message, with a list of errors or unsupported functionality

## <a name="next-steps"></a>Next steps
[Learn more about the Enterprise Integration Pack](logic-apps-enterprise-integration-overview.md "Learn about Enterprise Integration Pack") 







