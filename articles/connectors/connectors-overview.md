---
title: Overview of Logic Apps Connectors | Microsoft Docs
description: Overview of connectors that can be used in a logic app
services: ''
documentationcenter: ''
author: jeffhollan
manager: erikre
editor: ''
tags: connectors
ms.assetid: ca8dab2e-9b69-4b1e-865d-1facd9f0cdac
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/15/2016
ms.author: jehollan
ms.openlocfilehash: 6f7d8f99bfa09847c01831a06efa8b94c1c0a89a
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803743"
---
# <a name="using-connectors-in-a-logic-app"></a>Using connectors in a logic app
Connectors provide quick access to events, data, and actions across services, protocols, and platforms.  The full list of connectors that Logic Apps supports can [be found here](apis-list.md).  Connectors can be used as a trigger or an action in a logic app, and may require a configured *connection* to use (for example: authorizing a Twitter account to access or post on your behalf).

## <a name="basics"></a>Basics
Connectors are hosted services you can access as part of a logic app to integrate with other services like Dynamics, Azure, Salesforce, [and more](apis-list.md).  They are deployed and managed by Microsoft, so you can build your integration workflows with scale, throughput, and security taken care of.  You can add a connector to a logic app by searching and selecting a connector action or trigger under **Show Microsoft managed APIs**.

![Action menu for selecting trigger][1]

Each connector action or trigger will have its set of properties to configure.  You can click on the info buttons to learn more about action, or reference its documentation [to learn more](apis-list.md).

If you want to integrate with a service or API that isn't yet a connector, you can also extend logic apps through a [custom connector](../logic-apps/logic-apps-create-api-app.md) or just call directly to the service over a protocol like HTTP.

## <a name="triggers"></a>Triggers
Some connectors have a trigger, which means an event from that connector will fire a logic app and pass in any data as part of the trigger.  A trigger is always the first step in a logic app.  Popular triggers include operations like:

* Recurrence - run every hour
* When an HTTP request is received
* When an item is added to a queue
* When an email is received

Some triggers will fire the instant an event happens through a notification to the logic app, and others will need a recurrence interval configured on how often the logic app will check the service for an event (up to every 15 seconds).  

Once an event is received, the logic app run will fire and the actions in the workflow will start.  You will also be able to access any data from the trigger throughout the workflow (for example the 'On a new tweet' trigger will pass the tweet into the run).

## <a name="actions"></a>Actions
Most connectors have one or many actions that can be executed as part of the workflow.  Actions are any steps that happen after the run has fired from a trigger.  To add an action click the **New Step** button and search for the connector you want to use.  Once selected (and after configuring any [connections](#connections) that may be required) you will see the action card you can configure.  You can select data from previous steps by clicking on any of the tokens for outputs, or enter in any other configuration as needed.

![Configuring a connector action][2]

## <a name="connections"></a>Connections
Most connectors require you to configure a *connection* before you can use the connector.  A *connection* is any login or connection configuration needed to access the connector.  For connectors that use OAuth, create a connection means signing into the service (like Office 365, Salesforce, or GitHub) where your access token can be encrypted and securely stored in an Azure secret store.  Other connectors (like FTP and SQL) require a connection that contains configuration like server address, username, and password.  These connection configuration details are also encrypted and securely stored.  Connections will be able to access the service for as long as the service allows.  For Azure Active Directory OAuth connections (like Office 365 and Dynamics) we can continue to refresh the access token indefinitely.  Other services may put limits on how long we can use a token without it being refreshed.  In general certain actions like changing a password will invalidate all access tokens.  

Connections can be viewed and managed in Azure by clicking **Browse** and selecting **API Connections**.  From the API Connections resource you can view, edit, update, or re-authorize any connections you have created.

## <a name="next-steps"></a>Next Steps
* [Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md)
* [Learn common uses and examples of logic apps](../logic-apps/logic-apps-examples-and-scenarios.md)
* [Get started with enterprise integration triggers and actions](../logic-apps/logic-apps-enterprise-integration-overview.md)

<!--Image References -->
[1]: ./media/connectors-overview/addAction.png
[2]: ./media/connectors-overview/configureAction.png
