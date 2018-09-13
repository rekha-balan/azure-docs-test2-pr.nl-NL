---
title: Configure the Review Tool | Microsoft Docs
description: Configure or get your team, tags, connectors, workflows, and credentials.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.technology: content-moderator
ms.topic: article
ms.date: 02/03/2017
ms.author: sajagtap
ms.openlocfilehash: c8f8eed308e7b3ef618d9289d3ac0b3f1a424ff9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44549441"
---
# <a name="configure-or-get-review-tool-settings"></a>Configure or Get Review Tool Settings #

## <a name="team"></a>Team ##

After you have sent out invites, you can monitor them, change permissions for team members, and invite additional users on the screens shown below. You can also create subteams and assign existing members. The users can be either administrators or reviewers. The difference between the two roles is that administrators can invite other users, while reviewers cannot.

![Teams](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/7-Settings-Team.PNG)

## <a name="tags"></a>Tags ##

This is where you can define your custom tags by entering the short code, name, and description for your tags and using the **Add** button. You will see your new tag on the screen. Click the **Save** button to save your new tag and make it available during reviews.

![Tags](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/7-Settings-Tags-Combined.PNG)

## <a name="connectors"></a>Connectors ##

The Content Moderator review tool calls the Content Moderator APIs with the **default** workflow to moderate content. It will auto-provision the Moderator API credentials for you when you sign up for the review tool.

It also supports integrating other APIs as long as a connector is available. We have made a few connectors available out of the box. You can enter your credentials for these APIs by using the **Connect** button. You can then use these connectors in your custom workflows, as shown in the next section.

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/7-Settings-Connectors.PNG)

## <a name="workflows"></a>Workflows ##

This is where you can see the **default** workflow. You can also define custom workflows for image and text by using the API Connectors available under the Connectors section. For a detailed example of how to define custom workflows, please see the **[Workflows](workflows.md)** section.

![Workflows](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/7-Settings-Workflows.PNG)

## <a name="credentials"></a>Credentials ##

In this section, you can access your Content Moderator subscription key to use with the APIs (Image, Text, List, Workflow, and Review APIs) included with Content Moderator. You will use these APIs to integrate your content with the various Content Moderator capabilities, whether for scanning or for both scanning and enabling human review workflows.

![Credentials](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/7-Settings-Credentials3.PNG)





