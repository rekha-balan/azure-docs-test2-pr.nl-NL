---
title: Define and use workflows in Content Moderator | Microsoft Docs
description: Content Moderator includes default workflows, and you can create your own based on content policies that are specific to your business.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.technology: content-moderator
ms.topic: article
ms.date: 02/03/2017
ms.author: sajagtap
ms.openlocfilehash: 7609622a3b4ad1b03f3757916aae649618ba5472
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: HT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44556775"
---
# <a name="defining-and-using-workflows"></a>Defining and using workflows  #

In addition to default workflow used for generating reviews, you can define custom workflows and thresholds based on content policies that are specific to your business. Content Moderator allows you to use other APIs in addition to its own API as long as a connector for that API is available.

## <a name="make-sure-you-have-valid-credentials"></a>Make sure you have valid credentials ##

To get started on defining a workflow, make sure you have valid credentials for the API you intend to use in your workflow. Content Moderator includes a small set of Connectors by default.

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows.PNG)

## <a name="navigate-to-the-workflows-section"></a>Navigate to the Workflows section ##

Select the **Workflows** option under **Settings**.

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-0.PNG)

## <a name="start-a-new-workflow"></a>Start a new workflow ##

Use the **Add Workflows** option to get started.

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-1.PNG)

## <a name="name-your-workflow"></a>Name your workflow ##

Name your workflow, provide a description, and select whether you want to process images or text.
In the screenshot below, you can see the fields and view the If-Then-Else selections that you need to make to define your custom workflows.

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-2.PNG)

## <a name="define-the-evaluation-criteria-condition"></a>Define the evaluation criteria (condition) ##

As a first step, enter all the information needed to define your criteria for executing the workflow. As shown in the screen below, this includes selecting the API you want to get results from. When you select one of the available APIs (that you have entered your credentials for in the very first step), the next drop-down will show the available outputs from the API. The next two fields allow you to specify the check to be performed.

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-3.PNG)

## <a name="define-the-action"></a>Define the action ##

Once you have defined the condition, you will tell Content Moderator what action to perform if the condition is met. The example shown below creates an image review and assigns it to a subteam. It also specifies an aditional criteria that must be fulfilled for the assigned 'a' tag to be selected. In this way, you can combine multiple conditions to get the results you want.

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-5.PNG)

## <a name="optionally-define-the-else-section"></a>Optionally, define the Else section ##

Optionally, expand the **Else** section to provide similar information like you did for the **If** section.

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-6.PNG)

## <a name="save-the-workflow"></a>Save the workflow ##

Finally, save your workflow and note the workflow name. You will need it to invoke the workflow with the Review API.

![Connectors](https://docstestmedia1.blob.core.windows.net/azure-media/articles/cognitive-services/Content-Moderator/Review-Tool-User-Guide/images/2-Workflows-7.PNG)

## <a name="use-the-review-api"></a>Use the Review API ##

Now that you have a custom workflow defined, use the [**Review API**](https://westus.dev.cognitive.microsoft.com/docs/services/580519463f9b070e5c591178/operations/580519483f9b0709fc47f9c5) to start a moderation job with the workflow name as one of the parameters. This should be the workflow name that you noted in the previous step.








