---
title: Create a function that runs on a schedule in Azure | Microsoft Docs
description: Learn how to create a function in Azure that runs based on a schedule that you define.
services: functions
documentationcenter: na
author: ggailey777
manager: jeconnoc
ms.assetid: ba50ee47-58e0-4972-b67b-828f2dc48701
ms.service: azure-functions
ms.devlang: multiple
ms.topic: quickstart
ms.date: 03/28/2018
ms.author: glenga
ms.custom: mvc, cc996988-fb4f-47
ms.openlocfilehash: 5a5e14c2a8501ce2672923545df8d32a32dee8fa
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44966041"
---
# <a name="create-a-function-in-azure-that-is-triggered-by-a-timer"></a>Create a function in Azure that is triggered by a timer

Learn how to use Azure Functions to create a [serverless](https://azure.microsoft.com/overview/serverless-computing/) function that runs based a schedule that you define.

![Create function app in the Azure portal](./media/functions-create-scheduled-function/function-app-in-portal-editor.png)

## <a name="prerequisites"></a>Prerequisites

To complete this tutorial:

+ If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.

## <a name="create-an-azure-function-app"></a>Create an Azure Function app

[!INCLUDE [Create function app Azure portal](../../includes/functions-create-function-app-portal.md)]

![Function app successfully created.](./media/functions-create-first-azure-function/function-app-create-success.png)

Next, you create a function in the new function app.

<a name="create-function"></a>

## <a name="create-a-timer-triggered-function"></a>Create a timer triggered function

1. Expand your function app and click the **+** button next to **Functions**. If this is the first function in your function app, select **Custom function**. This displays the complete set of function templates.

    ![Functions quickstart page in the Azure portal](./media/functions-create-scheduled-function/add-first-function.png)

2. In the search field, type `timer` and then choose your desired language for the timer trigger template. 

    ![Choose the timer triggered function template.](./media/functions-create-scheduled-function/functions-create-timer-trigger.png)

3. Configure the new trigger with the settings as specified in the table below the image.

    ![Create a timer triggered function in the Azure portal.](./media/functions-create-scheduled-function/functions-create-timer-trigger-2.png)

    | Setting | Suggested value | Description |
    |---|---|---|
    | **Name** | Default | Defines the name of your timer triggered function. |
    | **Schedule** | 0 \*/1 \* \* \* \* | A six field [CRON expression](functions-bindings-timer.md#cron-expressions) that schedules your function to run every minute. |

2. Click **Create**. A function is created in your chosen language that runs every minute.

3. Verify execution by viewing trace information written to the logs.

    ![Functions log viewer in the Azure portal.](./media/functions-create-scheduled-function/functions-timer-trigger-view-logs2.png)

Now, you change the function's schedule so that it runs once every hour instead of every minute. 

## <a name="update-the-timer-schedule"></a>Update the timer schedule

1. Expand your function and click **Integrate**. This is where you define input and output bindings for your function and also set the schedule. 

2. Enter a new hourly **Schedule** value of `0 0 */1 * * *` and then click **Save**.  

![Functions update timer schedule in the Azure portal.](./media/functions-create-scheduled-function/functions-timer-trigger-change-schedule.png)

You now have a function that runs once every hour. 

## <a name="clean-up-resources"></a>Clean up resources

[!INCLUDE [Next steps note](../../includes/functions-quickstart-cleanup.md)]

## <a name="next-steps"></a>Next steps

You have created a function that runs based on a schedule.

[!INCLUDE [Next steps note](../../includes/functions-quickstart-next-steps.md)]

For more information timer triggers, see [Schedule code execution with Azure Functions](functions-bindings-timer.md).
