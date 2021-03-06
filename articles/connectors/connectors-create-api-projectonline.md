---
title: Connect to Project Online from Azure Logic Apps | Microsoft Docs
description: Automate workflows that monitor, create, and manage Project Online projects, tasks, and resources by using Azure Logic Apps
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
ms.reviewer: klam, LADocs
ms.suite: integration
ms.topic: article
ms.assetid: 40ce621e-4925-4653-93bb-71ab9abcbdf1
tags: connectors
ms.date: 08/24/2018
ms.openlocfilehash: cfcb53b6e95250a1ccbebfdfcfbff5ec8479504b
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44782332"
---
# <a name="manage-project-online-projects-tasks-and-resources-by-using-azure-logic-apps"></a>Manage Project Online projects, tasks, and resources by using Azure Logic Apps

With Azure Logic Apps and the Project Online connector, you can create automated tasks and workflows for your projects, tasks, and resources in Project Online through Office 365. Your workflows can perform these actions and others, for example:

* Monitor when new projects, tasks, or resources are created. Or, monitor when new projects are published.
* Create new projects, tasks, or resources.
* List existing projects or tasks.
* Check out, check in, or publish projects.

Project Online helps you plan, prioritize, and manage projects and project portfolio investments from almost anywhere on almost any device by providing powerful project management capabilities. You can use Project Online triggers that get responses from Project Online and make the output available to other actions. You can use actions in your logic apps to perform various tasks in Project Online. If you're new to logic apps, review [What is Azure Logic Apps?](../logic-apps/logic-apps-overview.md)

## <a name="prerequisites"></a>Prerequisites

* An Azure subscription. If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a>. 

* Project Online, available through an [Office 365 account](https://www.office.com/), 

* Basic knowledge about [how to create logic apps](../logic-apps/quickstart-create-first-logic-app-workflow.md)

* The logic app where you want to access your Project Online data. To start with a Project Online trigger, [create a blank logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md). To use Project Online actions, start your logic app with another trigger, for example, the **Recurrence** trigger.

## <a name="connect-to-project-online"></a>Connect to Project Online

[!INCLUDE [Create connection general intro](../../includes/connectors-create-connection-general-intro.md)]

1. Sign in to the [Azure portal](https://portal.azure.com), and open your logic app in Logic App Designer, if not open already.

1. Choose a path: 

   * For blank logic apps, in the search box, enter "Project Online" as your filter. 
   Under the triggers list, select the trigger you want. 

     -or-

   * For existing logic apps, under the step where you want to add an action, choose **New step**. In the search box, enter "Project Online" as your filter. Under the actions list, select the action you want.

1. If you're prompted to sign in to Project Online, sign in now.

   Your credentials authorize your logic app to create a connection to Project Online and access your data.

1. Provide the necessary details for your selected trigger or action and continue building your logic app's workflow.

## <a name="connector-reference"></a>Connector reference

For technical details about triggers, actions, and limits, which are described by the connector's OpenAPI (formerly Swagger) description, review the connector's [reference page](/connectors/projectonline/).

## <a name="get-support"></a>Get support

* For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).
* To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Next steps

* Learn about other [Logic Apps connectors](../connectors/apis-list.md)