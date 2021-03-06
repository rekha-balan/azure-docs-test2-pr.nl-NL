---
title: Define and use workflows in Azure Content Moderator | Microsoft Docs
description: Learn how to create custom workflows based on your content policies.
services: cognitive-services
author: sanjeev3
manager: mikemcca
ms.service: cognitive-services
ms.component: content-moderator
ms.topic: article
ms.date: 01/07/2018
ms.author: sajagtap
ms.openlocfilehash: dfe3ba8a2ef1bcbc69ef585b504a9367d9420bf0
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44803716"
---
# <a name="define-test-and-use-workflows"></a>Define, test, and use workflows

You can use the Azure Content Moderator workflow designer and APIs to define custom workflows and thresholds based on your content policies.

Workflows "connect" to the Content Moderator API by using connectors. You can use other APIs if a connector for that API is available. The example here uses the Content Moderator connector that is included by default.

## <a name="browse-to-the-workflows-section"></a>Browse to the Workflows section

On the **Settings** tab, select **Workflows**.

  ![Workflows setting](images/2-workflows-0.png)

## <a name="start-a-new-workflow"></a>Start a new workflow

Select **Add Workflow**.

  ![Add a workflow](images/2-workflows-1.png)

## <a name="assign-a-name-and-description"></a>Assign a name and description

Name your workflow, enter a description, and choose whether the workflow handles images or text.

  ![Workflow name and description](images/ocr-workflow-step-1.PNG)

## <a name="define-the-evaluation-criteria-condition"></a>Define the evaluation criteria ("condition")

In the following screenshot, you see the fields and the If-Then-Else selections that you need to define for your workflows. Choose a connector. This example uses **Content Moderator**. Depending on the connector you choose, the available options for output change.

  ![Define workflow condition](images/ocr-workflow-step-2-condition.PNG)

After you choose the connector and its output that you want, select an operator and the value for the condition.

## <a name="define-the-action-to-take"></a>Define the action to take

Select the action to take and the condition to meet. The following example creates an image review, assigns a tag `a`, and highlights it for the condition shown. You also can combine multiple conditions to get the results you want. Optionally, add an alternative (Else) path.

  ![Define workflow action](images/ocr-workflow-step-3-action.PNG)

## <a name="save-your-workflow"></a>Save your workflow

Finally, save the workflow, and note the workflow name. You need the name to start a moderation job by using the Review API.

## <a name="test-the-workflow"></a>Test the workflow

Now that you defined a custom workflow, test it with sample content.

Select the corresponding **Execute Workflow** button.

  ![Workflow test](images/ocr-workflow-step-6-list.PNG)

### <a name="upload-a-file"></a>Upload a file

Save the [sample image](https://moderatorsampleimages.blob.core.windows.net/samples/sample5.png) to your local drive. To test the workflow, select **Choose File(s)** and upload the image.

  ![Upload image file](images/ocr-workflow-step-7-upload.PNG)

### <a name="track-the-workflow"></a>Track the workflow

Track the workflow as it executes.

  ![Track workflow execution](images/ocr-workflow-step-4-test.PNG)

### <a name="review-any-images-flagged-for-human-moderation"></a>Review any images flagged for human moderation

To see the image review, go to the **Image** tab under **Review**.

  ![Review images](images/ocr-sample-image-workflow1.PNG)

## <a name="next-steps"></a>Next steps 

To invoke the workflow from code, use custom workflows with the [`Job` API console quickstart](../try-review-api-job.md) and the [.NET SDK quickstart](../moderation-jobs-quickstart-dotnet.md).
