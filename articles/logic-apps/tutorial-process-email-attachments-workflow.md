---
title: Build workflows that process emails and attachments - Azure Logic Apps | Microsoft Docs
description: This tutorial shows how to create automated workflows so you can process emails and attachments with Azure Logic Apps, Azure Storage, and Azure Functions
services: logic-apps
ms.service: logic-apps
author: ecfan
ms.author: estfan
manager: jeconnoc
ms.topic: tutorial
ms.custom: mvc
ms.date: 07/20/2018
ms.reviewer: klam, LADocs
ms.openlocfilehash: d07342bac3f76472a4783c28cac0741906049bb2
ms.sourcegitcommit: d1451406a010fd3aa854dc8e5b77dc5537d8050e
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 09/13/2018
ms.locfileid: "44869279"
---
# <a name="process-emails-and-attachments-with-azure-logic-apps"></a>Process emails and attachments with Azure Logic Apps

Azure Logic Apps helps you automate workflows and integrate data across Azure services, Microsoft services, other software-as-a-service (SaaS) apps, and on-premises systems. This tutorial shows how you can build a [logic app](../logic-apps/logic-apps-overview.md) that handles incoming emails and any attachments. This logic app processes that content, saves the content to Azure storage, and sends notifications for reviewing that content. 

In this tutorial, you learn how to:

> [!div class="checklist"]
> * Set up [Azure storage](../storage/common/storage-introduction.md) and Storage Explorer for checking saved emails and attachments.
> * Create an [Azure function](../azure-functions/functions-overview.md) that removes HTML from emails. This tutorial includes the code that you can use for this function.
> * Create a blank logic app.
> * Add a trigger that monitors emails for attachments.
> * Add a condition that checks whether emails have attachments.
> * Add an action that calls the Azure function when an email has attachments.
> * Add an action that creates storage blobs for emails and attachments.
> * Add an action that sends email notifications.

When you're done, your logic app looks like this workflow at a high level:

![High-level finished logic app](./media/tutorial-process-email-attachments-workflow/overview.png)

If you don't have an Azure subscription, <a href="https://azure.microsoft.com/free/" target="_blank">sign up for a free Azure account</a> before you begin. 

## <a name="prerequisites"></a>Prerequisites

* An email account from an email provider supported by Logic Apps, such as Office 365 Outlook, Outlook.com, or Gmail. For other providers, [review the connectors list here](https://docs.microsoft.com/connectors/).

  This logic app uses an Office 365 Outlook account. 
  If you use a different email account, the general steps stay the same, but your UI might appear slightly different.

* Download and install the <a href="https://storageexplorer.com/" target="_blank">free Microsoft Azure Storage Explorer</a>. This tool helps you check that your storage container is correctly set up.

## <a name="sign-in-to-azure-portal"></a>Sign in to Azure portal

Sign in to the <a href="https://portal.azure.com" target="_blank">Azure portal</a> with your Azure account credentials.

## <a name="set-up-storage-to-save-attachments"></a>Set up storage to save attachments

You can save incoming emails and attachments as blobs in an [Azure storage container](../storage/common/storage-introduction.md). 

1. Before you can create a storage container, [Create a storage account](../storage/common/storage-quickstart-create-account.md) with these settings:

   | Setting | Value | Description | 
   |---------|-------|-------------| 
   | **Name** | attachmentstorageacct | The name for your storage account | 
   | **Deployment model** | Resource manager | The [deployment model](../azure-resource-manager/resource-manager-deployment-model.md) for managing resource deployment | 
   | **Account kind** | General purpose | The [storage account type](../storage/common/storage-introduction.md#types-of-storage-accounts) | 
   | **Location** | West US | The region where to store information about your storage account | 
   | **Replication** | Locally redundant storage (LRS) | This setting specifies how your data is copied, stored, managed, and synchronized. See [Replication](../storage/common/storage-introduction.md#replication). | 
   | **Performance** | Standard | This setting specifies the data types supported and media for storing data. See [Types of storage accounts](../storage/common/storage-introduction.md#types-of-storage-accounts). | 
   | **Secure transfer required** | Disabled | This setting specifies the security required for requests from connections. See [Require secure transfer](../storage/common/storage-require-secure-transfer.md). | 
   | **Subscription** | <*your-Azure-subscription-name*> | The name for your Azure subscription | 
   | **Resource group** | LA-Tutorial-RG | The name for the [Azure resource group](../azure-resource-manager/resource-group-overview.md) used to organize and manage related resources. <p>**Note:** A resource group exists inside a specific region. Although the items in this tutorial might not be available in all regions, try to use the same region when possible. | 
   | **Configure virtual networks** | Disabled | For this tutorial, keep the **Disabled** setting. | 
   |||| 

   To create your storage account, you can also use [Azure PowerShell](../storage/common/storage-quickstart-create-storage-account-powershell.md) or [Azure CLI](../storage/common/storage-quickstart-create-storage-account-cli.md).

2. After Azure deploys your storage account, get your storage account's access key:

   1. On your storage account menu, under **Settings**, select **Access keys**. 

   2. Copy your storage account name and **key1**, and then save those values somewhere safe.

      ![Copy and save storage account name and key](./media/tutorial-process-email-attachments-workflow/copy-save-storage-name-key.png)

   To get your storage account's access key, you can also use [Azure PowerShell](https://docs.microsoft.com/powershell/module/azurerm.storage/get-azurermstorageaccountkey) or [Azure CLI](https://docs.microsoft.com/cli/azure/storage/account/keys?view=azure-cli-latest.md#az-storage-account-keys-list). 

3. Create a blob storage container for your email attachments.
   
   1. On your storage account menu, select **Overview**. 
   Under **Services**, select **Blobs**.

      ![Add blob storage container](./media/tutorial-process-email-attachments-workflow/create-storage-container.png)

   2. After the **Containers** page opens, on the toolbar, select **Container**. 

   3. Under **New container**, enter "attachments" as your container name. 
   Under **Public access level**, select **Container (anonymous read access for containers and blobs)**, and then choose **OK**.

      When you're done, you can find your storage container in your storage account here in the Azure portal:

      ![Finished storage container](./media/tutorial-process-email-attachments-workflow/created-storage-container.png)

   To create a storage container, you can also use [Azure PowerShell](https://docs.microsoft.com/powershell/module/azure.storage/new-azurestoragecontainer), or [Azure CLI](https://docs.microsoft.com/cli/azure/storage/container?view=azure-cli-latest#az-storage-container-create). 

Next, connect Storage Explorer to your storage account.

## <a name="set-up-storage-explorer"></a>Set up Storage Explorer

Now, connect Storage Explorer to your storage account so you can confirm that your logic app can correctly save attachments as blobs in your storage container.

1. Open Microsoft Azure Storage Explorer. 

   Storage Explorer prompts you for a connection to your storage account. 

2. In the **Connect to Azure Storage** pane, select **Use a storage account name and key**, and then choose **Next**. 

   ![Storage Explorer - Connect to storage account](./media/tutorial-process-email-attachments-workflow/storage-explorer-choose-storage-account.png)

   > [!TIP]
   > If no prompt appears, on the Storage Explorer toolbar, choose **Add account**.

3. Under **Account name**, provide your storage account name. Under **Account key**, provide the access key you previously saved. Choose **Next**.

4. Confirm your connection information, and then choose **Connect**. 

   Storage Explorer creates the connection, and shows your storage account in the Explorer window under **(Local and Attached)** > **Storage Accounts**. 

5. To find your blob storage container, under **Storage Accounts**, expand your storage account, which is **attachmentstorageacct** here, and then expand **Blob Containers** where you find the **attachments** container, for example: 

   ![Storage Explorer - find storage container](./media/tutorial-process-email-attachments-workflow/storage-explorer-check-contianer.png)

Next, create an [Azure function](../azure-functions/functions-overview.md) that removes HTML from incoming email.

## <a name="create-function-to-clean-html"></a>Create function to clean HTML

Now, use the code snippet provided by these steps to create an Azure function that removes HTML from each incoming email. That way, the email content is cleaner and easier to process. You can then call this function from your logic app.

1. Before you can create a function, [create a function app](../azure-functions/functions-create-function-app-portal.md) with these settings:

   | Setting | Value | Description | 
   | ------- | ----- | ----------- | 
   | **App name** | CleanTextFunctionApp | A globally unique and descriptive name for your function app | 
   | **Subscription** | <*your-Azure-subscription-name*> | The same Azure subscription that you previously used | 
   | **Resource Group** | LA-Tutorial-RG | The same Azure resource group that you previously used | 
   | **Hosting Plan** | Consumption Plan | This setting determines how to allocate and scale resources, such as computing power, for running your function app. See [hosting plans comparison](../azure-functions/functions-scale.md). | 
   | **Location** | West US | The same region that you previously used | 
   | **Storage** | cleantextfunctionstorageacct | Create a storage account for your function app. Use only lowercase letters and numbers. <p>**Note:** This storage account contains your function apps, and differs from your previously created storage account for email attachments. | 
   | **Application Insights** | Off | Turns on application monitoring with [Application Insights](../application-insights/app-insights-overview.md), but for this tutorial, choose the **Off** setting. | 
   |||| 

   If your function app doesn't automatically open after deployment, find your app in the <a href="https://portal.azure.com" target="_blank">Azure portal</a>. On the main Azure menu, select **Function Apps**, and select your function app. 

   ![Select function app](./media/tutorial-process-email-attachments-workflow/select-function-app.png)

   If **Function Apps** doesn't appear on the Azure menu, go to **All services** instead. In the search box, find and select **Function Apps**. For more information, see [Create your function](../azure-functions/functions-create-first-azure-function.md).

   Otherwise, Azure automatically opens your function app as shown here:

   ![Created function app](./media/tutorial-process-email-attachments-workflow/function-app-created.png)

   To create a function app, you can also use [Azure CLI](../azure-functions/functions-create-first-azure-function-azure-cli.md), or [PowerShell and Resource Manager templates](../azure-resource-manager/resource-group-template-deploy.md).

2. Under **Function Apps**, expand **CleanTextFunctionApp**, and select **Functions**. On the functions toolbar, select **New function**.

   ![Create new function](./media/tutorial-process-email-attachments-workflow/function-app-new-function.png)

3. Under **Choose a template below or go to the quickstart**, open the **Scenario** list, and select **Core**. In the **HTTP Trigger** template, select **C#**.

   ![Select function template](./media/tutorial-process-email-attachments-workflow/function-select-httptrigger-csharp-function-template.png)

   > [!NOTE]
   > This example provides you the C# sample code so you can follow the example without having to know C#.

4. In the **New Function** pane, under **Name**, enter ```RemoveHTMLFunction```. Keep **Authorization level** set to **Function**, and choose **Create**.

   ![Name your function](./media/tutorial-process-email-attachments-workflow/function-provide-name.png)

5. After the editor opens, replace the template code with this sample code, which removes the HTML and returns results to the caller:

   ``` CSharp
   using System.Net;
   using System.Text.RegularExpressions;

   public static async Task<HttpResponseMessage> Run(HttpRequestMessage req, TraceWriter log)
   {
      log.Info($"HttpWebhook triggered");

      // Parse query parameter
      string emailBodyContent = await req.Content.ReadAsStringAsync();

      // Replace HTML with other characters
      string updatedBody = Regex.Replace(emailBodyContent, "<.*?>", string.Empty);
      updatedBody = updatedBody.Replace("\\r\\n", " ");
      updatedBody = updatedBody.Replace(@"&nbsp;", " ");

      // Return cleaned text
      return req.CreateResponse(HttpStatusCode.OK, new { updatedBody });
   }
   ```

6. When you're done, choose **Save**. To test your function, at the editor's right edge, under the arrow (**<**) icon, choose **Test**. 

   ![Open the "Test" pane](./media/tutorial-process-email-attachments-workflow/function-choose-test.png)

7. In the **Test** pane, under **Request body**, enter this line, and choose **Run**.

   ```json
   {"name": "<p><p>Testing my function</br></p></p>"}
   ```

   ![Test your function](./media/tutorial-process-email-attachments-workflow/function-run-test.png)

   The **Output** window shows the function's result:

   ```json
   {"updatedBody":"{\"name\": \"Testing my function\"}"}
   ```

After checking that your function works, create your logic app. Although this tutorial shows how to create a function that removes HTML from emails, Logic Apps also provides an **HTML to Text** connector.

## <a name="create-your-logic-app"></a>Create your logic app

1. On the main Azure menu, select **Create a resource** > 
**Integration** > **Logic App**.

   ![Create logic app](./media/tutorial-process-email-attachments-workflow/create-logic-app.png)

2. Under **Create logic app**, provide this information about your logic app as shown and described. When you're done, choose **Pin to dashboard** > **Create**.

   ![Provide logic app information](./media/tutorial-process-email-attachments-workflow/create-logic-app-settings.png)

   | Setting | Value | Description | 
   | ------- | ----- | ----------- | 
   | **Name** | LA-ProcessAttachment | The name for your logic app | 
   | **Subscription** | <*your-Azure-subscription-name*> | The same Azure subscription that you previously used | 
   | **Resource group** | LA-Tutorial-RG | The same Azure resource group that you previously used |
   | **Location** | West US | The same region that you previously used | 
   | **Log Analytics** | Off | For this tutorial, choose the **Off** setting. | 
   |||| 

3. After Azure deploys your app, the Logic Apps Designer opens and shows a page with an introduction video and templates for common logic app patterns. Under **Templates**, choose **Blank Logic App**.

   ![Choose blank logic app template](./media/tutorial-process-email-attachments-workflow/choose-logic-app-template.png)

Next, add a [trigger](../logic-apps/logic-apps-overview.md#logic-app-concepts) that listens for incoming emails that have attachments. Every logic app must start with a trigger, which fires when a specific event happens or when new data meets a specific condition. For more information, see [Create your first logic app](../logic-apps/quickstart-create-first-logic-app-workflow.md).

## <a name="monitor-incoming-email"></a>Monitor incoming email

1. On the designer in the search box, enter "when new email arrives" as your filter. Select this trigger for your email provider: **When a new email arrives - <*your-email-provider*>**

   For example:

   ![Select this trigger for email provider: "When a new email arrives"](./media/tutorial-process-email-attachments-workflow/add-trigger-when-email-arrives.png)

   * For Azure work or school accounts, select Office 365 Outlook. 
   * For personal Microsoft accounts, select Outlook.com. 

2. If you're asked for credentials, sign in to your email account so Logic Apps can connect to your email account.

3. Now provide the criteria the trigger uses to filter new email.

   1. Specify the folder, interval, and frequency for checking emails.

      ![Specify folder, interval, and frequency for checking mails](./media/tutorial-process-email-attachments-workflow/set-up-email-trigger.png)

      | Setting | Value | Description | 
      | ------- | ----- | ----------- | 
      | **Folder** | Inbox | The email folder to check | 
      | **Interval** | 1 | The number of intervals to wait between checks | 
      | **Frequency** | Minute | The unit of time for each interval between checks | 
      |  |  |  | 
  
   2. Choose **Show advanced options** and specify these settings:

      | Setting | Value | Description | 
      | ------- | ----- | ----------- | 
      | **Has Attachment** | Yes | Get only emails with attachments. <p>**Note:** The trigger doesn't remove any emails from your account, checking only new messages and processing only emails that match the subject filter. | 
      | **Include Attachments** | Yes | Get the attachments as input for your workflow, rather than just check for attachments. | 
      | **Subject Filter** | ```Business Analyst 2 #423501``` | The text to find in the email subject | 
      |  |  |  | 

4. To hide the trigger's details for now, click inside the trigger's title bar.

   ![Collapse shape to hide details](./media/tutorial-process-email-attachments-workflow/collapse-trigger-shape.png)

5. Save your logic app. On the designer toolbar, choose **Save**.

   Your logic app is now live but doesn't do anything other check your emails. 
   Next, add a condition that specifies criteria to continue workflow.

## <a name="check-for-attachments"></a>Check for attachments

Now add a condition that selects only emails that have attachments.

1. Under the trigger, choose **New step** > **Add a condition**.

   !["New step", "Add a condition"](./media/tutorial-process-email-attachments-workflow/add-condition-under-trigger.png)

2. Rename the condition with a better description.

   1. On the condition's title bar, choose **ellipses** (**...**) button > **Rename**.

      ![Rename condition](./media/tutorial-process-email-attachments-workflow/condition-rename.png)

   2. Rename your condition with this description: ```If email has attachments and key subject phrase```

3. Create a condition that checks for emails that have attachments. 

   1. On the first row under **And**, click inside the left box. 
   From the dynamic content list that appears, select the **Has Attachment** property.

      ![Build condition](./media/tutorial-process-email-attachments-workflow/build-condition.png)

   2. In the middle box, keep the operator **is equal to**.

   3. In the right box, enter **True** as the value to compare with the **Has Attachment** property value from the trigger.

      ![Build condition](./media/tutorial-process-email-attachments-workflow/finished-condition.png)

      If both values are equal, the email has at least one attachment, the condition passes, and the workflow continues.

   In your underlying logic app definition, which you can view in the code editor window, this condition looks like this example:

   ```json
   "Condition": {
      "actions": { <actions-to-run-when-condition-passes> },
      "expression": {
         "and": [ {
            "equals": [
               "@triggerBody()?['HasAttachment']",
                 "True"
            ]
         } ]
      },
      "runAfter": {},
      "type": "If"
   }
   ```

4. Save your logic app. On the designer toolbar, choose **Save**.

### <a name="test-your-condition"></a>Test your condition

Now, test whether the condition works correctly:

1. If your logic app isn't running already, choose **Run** on the designer toolbar.

   This step manually starts your logic app without having to wait until your specified interval passes. 
   However, nothing happens until the test email arrives in your inbox. 

2. Send yourself an email that meets this criteria:

   * Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```

   * Your email has one attachment. 
   For now, just create one empty text file and attach that file to your email.

   When the email arrives, your logic app checks for attachments and the specified subject text.
   If the condition passes, the trigger fires and causes the Logic Apps engine to create a logic app instance and start the workflow. 

3. To check that the trigger fired and the logic app ran successfully, on the logic app menu, choose **Overview**.

   ![Check trigger and runs history](./media/tutorial-process-email-attachments-workflow/checkpoint-run-history.png)

   If your logic app didn't trigger or run despite a successful trigger, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).

Next, define the actions to take for the **If true** branch. To save the email along with any attachments, remove any HTML from the email body, then create blobs in the storage container for the email and attachments.

> [!NOTE]
> Your logic app doesn't have to do anything for the **If false** branch when an email doesn't have attachments. As a bonus exercise after you finish this tutorial, you can add any appropriate action that you want to take for the **If false** branch.

## <a name="call-removehtmlfunction"></a>Call RemoveHTMLFunction

This step adds your previously created Azure function to your logic app and passes the email body content from email trigger to your function.

1. On the logic app menu, select **Logic App Designer**. In the **If true** branch, choose **Add an action**.

   ![Inside "If true", add action](./media/tutorial-process-email-attachments-workflow/if-true-add-action.png)

2. In the search box, find "azure functions", and select this action: **Choose an Azure function - Azure Functions**

   ![Select action for "Choose an Azure function"](./media/tutorial-process-email-attachments-workflow/add-action-azure-function.png)

3. Select your previously created function app: **CleanTextFunctionApp**

   ![Select your Azure function app](./media/tutorial-process-email-attachments-workflow/add-action-select-azure-function-app.png)

4. Now select your function: **RemoveHTMLFunction**

   ![Select your Azure function](./media/tutorial-process-email-attachments-workflow/add-action-select-azure-function.png)

5. Rename your function shape with this description: ```Call RemoveHTMLFunction to clean email body```

6. Now specify the input for your function to process. 

   1. Under **Request Body**, enter this text with a trailing space: 
   
      ```{ "emailBody": ``` 

      While you work on this input in the next steps, an error about invalid JSON appears until your input is correctly formatted as JSON.
      When you previously tested this function, the input specified for this function used JavaScript Object Notation (JSON). 
      So, the request body must also use the same format.

      Also, when your cursor is inside the **Request body** box, the dynamic content list appears so you can select property values available from previous actions. 
      
   2. From the dynamic content list, under **When a new email arrives**, select the **Body** property. After this property, remember to add the closing curly brace: ```}```

      ![Specify the request body for passing to the function](./media/tutorial-process-email-attachments-workflow/add-email-body-for-function-processing.png)

   When you're done, the input to your function looks like this example:

   ![Finished request body to pass to your function](./media/tutorial-process-email-attachments-workflow/add-email-body-for-function-processing-2.png)

7. Save your logic app.

Next, add an action that creates a blob in your storage container so you can save the email body.

## <a name="create-blob-for-email-body"></a>Create blob for email body

1. In the **If true** block and under your Azure function, choose **Add an action**. 

2. In the search box, enter "create blob" as your filter, and select this action: **Create blob - Azure Blob Storage**

   ![Add action to create blob for email body](./media/tutorial-process-email-attachments-workflow/create-blob-action-for-email-body.png)

3. Create a connection to your storage account with these settings as shown and described here. When you're done, choose **Create**.

   ![Create connection to storage account](./media/tutorial-process-email-attachments-workflow/create-storage-account-connection-first.png)

   | Setting | Value | Description | 
   | ------- | ----- | ----------- | 
   | **Connection Name** | AttachmentStorageConnection | A descriptive name for the connection | 
   | **Storage Account** | attachmentstorageacct | The name for the storage account that you previously created for saving attachments | 
   |||| 

4. Rename the **Create blob** action with this description: ```Create blob for email body```

5. In the **Create blob** action, provide this information, and select these fields to create the blob as shown and described:

   ![Provide blob information for email body](./media/tutorial-process-email-attachments-workflow/create-blob-for-email-body.png)

   | Setting | Value | Description | 
   | ------- | ----- | ----------- | 
   | **Folder path** | /attachments | The path and name for the container that you previously created. For this example, click the folder icon, and then select the "/attachments" container. | 
   | **Blob name** | **From** field | For this example, use the sender's name as the blob's name. Click inside this box so that the dynamic content list appears, and then select the **From** field under the **When a new email arrives** action. | 
   | **Blob content** | **Content** field | For this example, use the HTML-free email body as the blob content. Click inside this box so that the dynamic content list appears, and then select **Body** under the **Call RemoveHTMLFunction to clean email body** action. |
   |||| 

   When you're done, the action looks like this example:

   ![Finished "Create blob" action](./media/tutorial-process-email-attachments-workflow/create-blob-for-email-body-done.png)

6. Save your logic app. 

### <a name="check-attachment-handling"></a>Check attachment handling

Now test whether your logic app handles emails the way that you specified:

1. If your logic app isn't running already, choose **Run** on the designer toolbar.

2. Send yourself an email that meets this criteria:

   * Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```

   * Your email has at least one attachment. 
   For now, just create one empty text file and attach that file to your email.

   * Your email has some test content in the body, for example: 

     ```
     Testing my logic app
     ```

   If your logic app didn't trigger or run despite a successful trigger, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).

3. Check that your logic app saved the email to the correct storage container. 

   1. In Storage Explorer, expand **(Local and Attached)** > 
   **Storage Accounts** > **attachmentstorageacct (External)** > 
   **Blob Containers** > **attachments**.

   2. Check the **attachments** container for the email. 

      At this point, only the email appears in the container because the logic app doesn't process the attachments yet.

      ![Check Storage Explorer for saved email](./media/tutorial-process-email-attachments-workflow/storage-explorer-saved-email.png)

   3. When you're done, delete the email in Storage Explorer.

4. Optionally, to test the **If false** branch, which does nothing at this time, you can send an email that doesn't meet the criteria.

Next, add a loop to process all the email attachments.

## <a name="process-attachments"></a>Process attachments

To process each attachment in the email, add a **For each** loop to your logic app's workflow.

1. Under the **Create blob for email body** shape, select **More** > **Add a for each**.

   ![Add "for each" loop](./media/tutorial-process-email-attachments-workflow/add-for-each-loop.png)

2. Rename your loop with this description: ```For each email attachment```

3. Now specify the data for the loop to process. Click inside the **Select an output from previous steps** box so that the dynamic content list opens, and then select **Attachments**. 

   ![Select "Attachments"](./media/tutorial-process-email-attachments-workflow/select-attachments.png)

   The **Attachments** field passes in an array that contains all the attachments included with an email. 
   The **For each** loop repeats actions on each item that's passed in with the array.

4. Save your logic app.

Next, add the action that saves each attachment as a blob in your **attachments** storage container.

## <a name="create-blob-for-each-attachment"></a>Create blob for each attachment

1. In the **For each email attachment** loop, choose **Add an action** so you can specify the task to perform on each found attachment.

   ![Add action to loop](./media/tutorial-process-email-attachments-workflow/for-each-add-action.png)

2. In the search box, enter "create blob" as your filter, and then select this action: **Create blob - Azure Blob Storage**

   ![Add action to create blob](./media/tutorial-process-email-attachments-workflow/create-blob-action-for-attachments.png)

3. Rename the **Create blob 2** action with this description: ```Create blob for each email attachment```

4. In the **Create blob for each email attachment** action, provide this information, and select the properties for each blob you want to create as shown and described:

   ![Provide blob information](./media/tutorial-process-email-attachments-workflow/create-blob-per-attachment.png)

   | Setting | Value | Description | 
   | ------- | ----- | ----------- | 
   | **Folder path** | /attachments | The path and name for the container that you previously created. For this example, click the folder icon, and then select the "/attachments" container. | 
   | **Blob name** | **Name** field | For this example, use the attachment's name as the blob's name. Click inside this box so that the dynamic content list appears, and then select the **Name** field under the **When a new email arrives** action. | 
   | **Blob content** | **Content** field | For this example, use the **Content** field as the blob content. Click inside this box so that the dynamic content list appears, and then select **Content** under the **When a new email arrives** action. |
   |||| 

   When you're done, the action looks like this example:

   ![Finished "Create blob" action](./media/tutorial-process-email-attachments-workflow/create-blob-per-attachment-done.png)

5. Save your logic app. 

### <a name="check-attachment-handling"></a>Check attachment handling

Next, test whether your logic app handles the attachments the way that you specified:

1. If your logic app isn't running already, choose **Run** on the designer toolbar.

2. Send yourself an email that meets this criteria:

   * Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```

   * Your email has at least two attachments. 
   For now, just create two empty text files and attach those files to your email.

   If your logic app didn't trigger or run despite a successful trigger, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).

3. Check that your logic app saved the email and attachments to the correct storage container. 

   1. In Storage Explorer, expand **(Local and Attached)** > 
   **Storage Accounts** > **attachmentstorageacct (External)** > 
   **Blob Containers** > **attachments**.

   2. Check the **attachments** container for both the email and the attachments.

      ![Check for saved email and attachments](./media/tutorial-process-email-attachments-workflow/storage-explorer-saved-attachments.png)

   3. When you're done, delete the email and attachments in Storage Explorer.

Next, add an action so that your logic app sends email to review the attachments.

## <a name="send-email-notifications"></a>Send email notifications

1. In the **if true** branch, under the **For each email attachment** loop, choose **Add an action**. 

   ![Add action under "for each" loop](./media/tutorial-process-email-attachments-workflow/add-action-send-email.png)

2. In the search box, enter "send email" as your filter, and then select the "send email" action for your email provider. 

   To filter the actions list to a specific service, you can select the connector first.

   ![Select "send email" action for your email provider](./media/tutorial-process-email-attachments-workflow/add-action-select-send-email.png)

   * For Azure work or school accounts, select Office 365 Outlook. 
   * For personal Microsoft accounts, select Outlook.com. 

3. If you're asked for credentials, sign in to your email account so that Logic Apps creates a connection to your email account.

4. Rename the **Send an email** action with this description: ```Send email for review```

5. Provide the information for this action and select the fields you want to include in the email as shown and described. To add blank lines in an edit box, press Shift + Enter.  

   ![Send email notification](./media/tutorial-process-email-attachments-workflow/send-email-notification.png)

   If you can't find an expected field in the dynamic content list, choose **See more** next to **When a new email arrives**. 

   | Setting | Value | Notes | 
   | ------- | ----- | ----- | 
   | **Body** | ```Please review new applicant:``` <p>```Applicant name: ``` **From** <p>```Application file location: ``` **Path** <p>```Application email content: ``` **Body** | The email's body content. Click inside this box, enter the example text, and from the dynamic content list, select these fields: <p>- The **From** field under **When a new email arrives** </br>- The **Path** field under **Create blob for email body** </br>- The **Body** field under **Call RemoveHTMLFunction to clean email body** | 
   | **Subject**  | ```ASAP - Review applicant for position: ``` **Subject** | The email subject that you want to include. Click inside this box, enter the example text, and from the dynamic content list, select the **Subject** field under **When a new email arrives**. | 
   | **To** | <*recipient-email-address*> | For testing purposes, you can use your own email address. | 
   |||| 

   > [!NOTE] 
   > If you select a field that contains an array, such as the **Content** field, which is an array that contains attachments, the designer automatically adds a "For each" loop around the action that references that field. That way, your logic app can perform that action on each array item. To remove the loop, remove the field for the array, move the referencing action to outside the loop, choose the ellipses (**...**) on the loop's title bar, and choose **Delete**.
     
6. Save your logic app. 

Now, test your logic app, which now looks like this example:

![Finished logic app](./media/tutorial-process-email-attachments-workflow/complete.png)

## <a name="run-your-logic-app"></a>Run your logic app

1. Send yourself an email that meets this criteria:

   * Your email's subject has the text that you specified in the trigger's **Subject filter**: ```Business Analyst 2 #423501```

   * Your email has at one or more attachments. 
   You can reuse an empty text file from your previous test. 
   For a more realistic scenario, attach a resume file.

   * The email body has this text, which you can copy and paste:

     ```
     Name: Jamal Hartnett   
     
     Street address: 12345 Anywhere Road   
     
     City: Any Town   
     
     State or Country: Any State   
     
     Postal code: 00000   
     
     Email address: jamhartnett@outlook.com   
     
     Phone number: 000-000-0000   
     
     Position: Business Analyst 2 #423501   

     Technical skills: Dynamics CRM, MySQL, Microsoft SQL Server, JavaScript, Perl, Power BI, Tableau, Microsoft Office: Excel, Visio, Word, PowerPoint, SharePoint, and Outlook   

     Professional skills: Data, process, workflow, statistics, risk analysis, modeling; technical writing, expert communicator and presenter, logical and analytical thinker, team builder, mediator, negotiator, self-starter, self-managing  
     
     Certifications: Six Sigma Green Belt, Lean Project Management   
     
     Language skills: English, Mandarin, Spanish   
     
     Education: Master of Business Administration   
     ```

2. Run your logic app. If successful, your logic app sends you an email that looks like this example:

   ![Email notification sent by logic app](./media/tutorial-process-email-attachments-workflow/email-notification.png)

   If you don't get any emails, check your email's junk folder. 
   Your email junk filter might redirect these kinds of mails. 
   Otherwise, if you're unsure that your logic app ran correctly, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).

Congratulations, you've now created and run a logic app that automates tasks across different Azure services and calls some custom code.

## <a name="clean-up-resources"></a>Clean up resources

When no longer needed, delete the resource group that contains your logic app and related resources. On the main Azure menu, go to **Resource groups**, and then select the resource group for your logic app. Choose **Delete resource group**. Enter the resource group name as confirmation, and choose **Delete**.

![Delete logic app resource group](./media/tutorial-process-email-attachments-workflow/delete-resource-group.png)

## <a name="get-support"></a>Get support

* For questions, visit the [Azure Logic Apps forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=azurelogicapps).
* To submit or vote on feature ideas, visit the [Logic Apps user feedback site](http://aka.ms/logicapps-wish).

## <a name="next-steps"></a>Next steps

In this tutorial, you created a logic app that processes and stores email attachments by integrating Azure services, such as Azure Storage and Azure Functions. Now, learn more about other connectors that you can use to build logic apps.

> [!div class="nextstepaction"]
> [Learn more about connectors for Logic Apps](../connectors/apis-list.md)