---
redirect_url: https://docs.microsoft.com/azure/documentdb/documentdb-change-feed-hl7-fhir-logic-apps
ROBOTS: NOINDEX, NOFOLLOW
ms.openlocfilehash: 4aad8b4355607b69772c3eab3120531050571ce9
ms.sourcegitcommit: 5b9d839c0c0a94b293fdafe1d6e5429506c07e05
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 08/02/2018
ms.locfileid: "44563555"
---
# <a name="notifications-for-new-or-changed-documentdb-resources-using-logic-apps"></a><span data-ttu-id="a5532-101">Notifications for new or changed DocumentDB resources using Logic Apps</span><span class="sxs-lookup"><span data-stu-id="a5532-101">Notifications for new or changed DocumentDB resources using Logic Apps</span></span>
<span data-ttu-id="a5532-102">This article came about from a question I saw posted one of the Azure DocumentDB community forums.</span><span class="sxs-lookup"><span data-stu-id="a5532-102">This article came about from a question I saw posted one of the Azure DocumentDB community forums.</span></span> <span data-ttu-id="a5532-103">The question was **Does DocumentDB support notifications for modified resources**?</span><span class="sxs-lookup"><span data-stu-id="a5532-103">The question was **Does DocumentDB support notifications for modified resources**?</span></span>

<span data-ttu-id="a5532-104">I have worked with BizTalk Server for many years, and this is a very common scenario when using the [WCF LOB Adapter](https://msdn.microsoft.com/library/bb798128.aspx).</span><span class="sxs-lookup"><span data-stu-id="a5532-104">I have worked with BizTalk Server for many years, and this is a very common scenario when using the [WCF LOB Adapter](https://msdn.microsoft.com/library/bb798128.aspx).</span></span> <span data-ttu-id="a5532-105">So I decided to see if I could duplicate this functionality in DocumentDB for new and/or modified documents.</span><span class="sxs-lookup"><span data-stu-id="a5532-105">So I decided to see if I could duplicate this functionality in DocumentDB for new and/or modified documents.</span></span>

<span data-ttu-id="a5532-106">This article provides an overview of the components of the change notification solution, which includes a [trigger](documentdb-programming.md#trigger) and a [Logic App](../logic-apps/logic-apps-what-are-logic-apps.md).</span><span class="sxs-lookup"><span data-stu-id="a5532-106">This article provides an overview of the components of the change notification solution, which includes a [trigger](documentdb-programming.md#trigger) and a [Logic App](../logic-apps/logic-apps-what-are-logic-apps.md).</span></span> <span data-ttu-id="a5532-107">Important code snippets are provided inline and the entire solution is available on [GitHub](https://github.com/HEDIDIN/DocDbNotifications).</span><span class="sxs-lookup"><span data-stu-id="a5532-107">Important code snippets are provided inline and the entire solution is available on [GitHub](https://github.com/HEDIDIN/DocDbNotifications).</span></span>

## <a name="use-case"></a><span data-ttu-id="a5532-108">Use case</span><span class="sxs-lookup"><span data-stu-id="a5532-108">Use case</span></span>
<span data-ttu-id="a5532-109">The following story is the use case for this article.</span><span class="sxs-lookup"><span data-stu-id="a5532-109">The following story is the use case for this article.</span></span>

<span data-ttu-id="a5532-110">DocumentDB is the repository for Health Level Seven International (HL7) Fast Healthcare Interoperability Resources (FHIR)  documents.</span><span class="sxs-lookup"><span data-stu-id="a5532-110">DocumentDB is the repository for Health Level Seven International (HL7) Fast Healthcare Interoperability Resources (FHIR)  documents.</span></span> <span data-ttu-id="a5532-111">Let's assume that your DocumentDB database combined with your API and Logic App make up an HL7 FHIR Server.</span><span class="sxs-lookup"><span data-stu-id="a5532-111">Let's assume that your DocumentDB database combined with your API and Logic App make up an HL7 FHIR Server.</span></span>  <span data-ttu-id="a5532-112">A healthcare facility is storing patient data in the DocumentDB "Patients" database.</span><span class="sxs-lookup"><span data-stu-id="a5532-112">A healthcare facility is storing patient data in the DocumentDB "Patients" database.</span></span> <span data-ttu-id="a5532-113">There are several collections within the patient database; Clinical, Identification, etc. Patient information falls under identification.</span><span class="sxs-lookup"><span data-stu-id="a5532-113">There are several collections within the patient database; Clinical, Identification, etc. Patient information falls under identification.</span></span>  <span data-ttu-id="a5532-114">You have a collection named "Patient".</span><span class="sxs-lookup"><span data-stu-id="a5532-114">You have a collection named "Patient".</span></span>

<span data-ttu-id="a5532-115">The Cardiology department is tracking personal heath and exercise data.</span><span class="sxs-lookup"><span data-stu-id="a5532-115">The Cardiology department is tracking personal heath and exercise data.</span></span> <span data-ttu-id="a5532-116">Searching for new or modified Patient records is time consuming.</span><span class="sxs-lookup"><span data-stu-id="a5532-116">Searching for new or modified Patient records is time consuming.</span></span> <span data-ttu-id="a5532-117">They asked the IT department if there was a way that they could receive a notification for new or modified Patient records.</span><span class="sxs-lookup"><span data-stu-id="a5532-117">They asked the IT department if there was a way that they could receive a notification for new or modified Patient records.</span></span>  

<span data-ttu-id="a5532-118">The IT department said that they could easily provide this.</span><span class="sxs-lookup"><span data-stu-id="a5532-118">The IT department said that they could easily provide this.</span></span> <span data-ttu-id="a5532-119">They also said that they could push the documents to [Azure Blob Storage](https://azure.microsoft.com/services/storage/) so the Cardiology department could easily access them.</span><span class="sxs-lookup"><span data-stu-id="a5532-119">They also said that they could push the documents to [Azure Blob Storage](https://azure.microsoft.com/services/storage/) so the Cardiology department could easily access them.</span></span>

## <a name="how-the-it-department-solved-the-problem"></a><span data-ttu-id="a5532-120">How the IT department solved the problem</span><span class="sxs-lookup"><span data-stu-id="a5532-120">How the IT department solved the problem</span></span>
<span data-ttu-id="a5532-121">In order to create this application, the IT department decided to model it first.</span><span class="sxs-lookup"><span data-stu-id="a5532-121">In order to create this application, the IT department decided to model it first.</span></span>  <span data-ttu-id="a5532-122">The nice thing about using Business Process Model and Notation (BPMN) is that both technical and non-technical people can easily understand it.</span><span class="sxs-lookup"><span data-stu-id="a5532-122">The nice thing about using Business Process Model and Notation (BPMN) is that both technical and non-technical people can easily understand it.</span></span> <span data-ttu-id="a5532-123">This whole notification process is considered a business process.</span><span class="sxs-lookup"><span data-stu-id="a5532-123">This whole notification process is considered a business process.</span></span> 

## <a name="high-level-view-of-notification-process"></a><span data-ttu-id="a5532-124">High-Level view of notification process</span><span class="sxs-lookup"><span data-stu-id="a5532-124">High-Level view of notification process</span></span>
1. <span data-ttu-id="a5532-125">You start with a Logic App that has a timer trigger.</span><span class="sxs-lookup"><span data-stu-id="a5532-125">You start with a Logic App that has a timer trigger.</span></span> <span data-ttu-id="a5532-126">By default, the trigger runs every hour.</span><span class="sxs-lookup"><span data-stu-id="a5532-126">By default, the trigger runs every hour.</span></span>
2. <span data-ttu-id="a5532-127">Next you do an HTTP POST to the Logic App.</span><span class="sxs-lookup"><span data-stu-id="a5532-127">Next you do an HTTP POST to the Logic App.</span></span>
3. <span data-ttu-id="a5532-128">The Logic App does all the work.</span><span class="sxs-lookup"><span data-stu-id="a5532-128">The Logic App does all the work.</span></span>

![High level view](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/high-level-view.png)

### <a name="lets-take-a-look-at-what-this-logic-app-does"></a><span data-ttu-id="a5532-130">Let's take a look at what this Logic App does</span><span class="sxs-lookup"><span data-stu-id="a5532-130">Let's take a look at what this Logic App does</span></span>
<span data-ttu-id="a5532-131">If you look at the following figure there are several steps in the LogicApp workflow.</span><span class="sxs-lookup"><span data-stu-id="a5532-131">If you look at the following figure there are several steps in the LogicApp workflow.</span></span>

![Main Logic Process](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/main-logic-app-process.png)

<span data-ttu-id="a5532-133">The steps are as follows:</span><span class="sxs-lookup"><span data-stu-id="a5532-133">The steps are as follows:</span></span>

1. <span data-ttu-id="a5532-134">You need to get the current UTC DateTime from an API App.</span><span class="sxs-lookup"><span data-stu-id="a5532-134">You need to get the current UTC DateTime from an API App.</span></span>  <span data-ttu-id="a5532-135">The default value is one hour previous.</span><span class="sxs-lookup"><span data-stu-id="a5532-135">The default value is one hour previous.</span></span>
2. <span data-ttu-id="a5532-136">The UTC DateTime is converted to a Unix Timestamp format.</span><span class="sxs-lookup"><span data-stu-id="a5532-136">The UTC DateTime is converted to a Unix Timestamp format.</span></span> <span data-ttu-id="a5532-137">This is the default format for timestamps in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="a5532-137">This is the default format for timestamps in DocumentDB.</span></span>
3. <span data-ttu-id="a5532-138">You POST the value to an API App, which does a DocumentDB query.</span><span class="sxs-lookup"><span data-stu-id="a5532-138">You POST the value to an API App, which does a DocumentDB query.</span></span> <span data-ttu-id="a5532-139">The value is used in a query.</span><span class="sxs-lookup"><span data-stu-id="a5532-139">The value is used in a query.</span></span>
   
    ```SQL
         SELECT * FROM Patients p WHERE (p._ts >= @unixTimeStamp)
    ```
   
   > [!NOTE]
   > <span data-ttu-id="a5532-140">The _ts represents the TimeStamp metadata for all DocumentDB resources.</span><span class="sxs-lookup"><span data-stu-id="a5532-140">The _ts represents the TimeStamp metadata for all DocumentDB resources.</span></span>
   > 
   > 
4. <span data-ttu-id="a5532-141">If there are documents found, the response body is sent to your Azure Blob Storage.</span><span class="sxs-lookup"><span data-stu-id="a5532-141">If there are documents found, the response body is sent to your Azure Blob Storage.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="a5532-142">Blob storage requires an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="a5532-142">Blob storage requires an Azure Storage account.</span></span> <span data-ttu-id="a5532-143">You need to provision an Azure Blob storage account and add a new Blob named patients.</span><span class="sxs-lookup"><span data-stu-id="a5532-143">You need to provision an Azure Blob storage account and add a new Blob named patients.</span></span> <span data-ttu-id="a5532-144">For more information, see [About Azure storage accounts](../storage/storage-create-storage-account.md) and [Get started with Azure Blob storage](../storage/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="a5532-144">For more information, see [About Azure storage accounts](../storage/storage-create-storage-account.md) and [Get started with Azure Blob storage](../storage/storage-dotnet-how-to-use-blobs.md).</span></span>
   > 
   > 
5. <span data-ttu-id="a5532-145">Finally, an email is sent that notifies the recipient of the number of documents found.</span><span class="sxs-lookup"><span data-stu-id="a5532-145">Finally, an email is sent that notifies the recipient of the number of documents found.</span></span> <span data-ttu-id="a5532-146">If no documents were found, the email body would be "0 Documents Found".</span><span class="sxs-lookup"><span data-stu-id="a5532-146">If no documents were found, the email body would be "0 Documents Found".</span></span> 

<span data-ttu-id="a5532-147">Now that you have an idea of what the workflow does, let's take a look at how you implement it.</span><span class="sxs-lookup"><span data-stu-id="a5532-147">Now that you have an idea of what the workflow does, let's take a look at how you implement it.</span></span>

### <a name="lets-start-with-the-main-logic-app"></a><span data-ttu-id="a5532-148">Let's start with the main Logic App</span><span class="sxs-lookup"><span data-stu-id="a5532-148">Let's start with the main Logic App</span></span>
<span data-ttu-id="a5532-149">If you're not familiar with Logic Apps, they are available in the [Azure Marketplace](https://portal.azure.com/), and you can learn more about them in [What are Logic Apps?](../logic-apps/logic-apps-what-are-logic-apps.md)</span><span class="sxs-lookup"><span data-stu-id="a5532-149">If you're not familiar with Logic Apps, they are available in the [Azure Marketplace](https://portal.azure.com/), and you can learn more about them in [What are Logic Apps?](../logic-apps/logic-apps-what-are-logic-apps.md)</span></span>

<span data-ttu-id="a5532-150">When you create a new Logic App, you are asked **How would you like to start?**</span><span class="sxs-lookup"><span data-stu-id="a5532-150">When you create a new Logic App, you are asked **How would you like to start?**</span></span>

<span data-ttu-id="a5532-151">When you click inside the text box, you have a choice of events.</span><span class="sxs-lookup"><span data-stu-id="a5532-151">When you click inside the text box, you have a choice of events.</span></span> <span data-ttu-id="a5532-152">For this Logic App, select **Manual - When an HTTP request is received** as shown below.</span><span class="sxs-lookup"><span data-stu-id="a5532-152">For this Logic App, select **Manual - When an HTTP request is received** as shown below.</span></span>

![Starting Off](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/starting-off.png)

### <a name="design-view-of-your-completed-logic-app"></a><span data-ttu-id="a5532-154">Design View of your completed Logic App</span><span class="sxs-lookup"><span data-stu-id="a5532-154">Design View of your completed Logic App</span></span>
<span data-ttu-id="a5532-155">Let's jump ahead and look at the completed design view for the Logic App, which is named DocDB.</span><span class="sxs-lookup"><span data-stu-id="a5532-155">Let's jump ahead and look at the completed design view for the Logic App, which is named DocDB.</span></span>

![Logic App Workflow](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/workflow-expanded.png)

<span data-ttu-id="a5532-157">When editing the actions in the Logic App Designer, you have the option of selecting **Outputs** from the HTTP Request or from the previous action as shown in the sendMail action below.</span><span class="sxs-lookup"><span data-stu-id="a5532-157">When editing the actions in the Logic App Designer, you have the option of selecting **Outputs** from the HTTP Request or from the previous action as shown in the sendMail action below.</span></span>

![Choose outputs](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/choose-outputs.png)

<span data-ttu-id="a5532-159">Before each action in your workflow, you can make a decision; **Add an action** or **Add a condition** as shown in the following figure.</span><span class="sxs-lookup"><span data-stu-id="a5532-159">Before each action in your workflow, you can make a decision; **Add an action** or **Add a condition** as shown in the following figure.</span></span>

![Make a decision](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/add-action-or-condition.png)

<span data-ttu-id="a5532-161">If you select **Add a condition**, you are presented with a form, as shown in the following figure, to enter your logic.</span><span class="sxs-lookup"><span data-stu-id="a5532-161">If you select **Add a condition**, you are presented with a form, as shown in the following figure, to enter your logic.</span></span>  <span data-ttu-id="a5532-162">This is in essence, a business rule.</span><span class="sxs-lookup"><span data-stu-id="a5532-162">This is in essence, a business rule.</span></span>  <span data-ttu-id="a5532-163">If you click inside a field, you have a choice of selecting parameters from the previous action.</span><span class="sxs-lookup"><span data-stu-id="a5532-163">If you click inside a field, you have a choice of selecting parameters from the previous action.</span></span> <span data-ttu-id="a5532-164">You can also enter the values directly.</span><span class="sxs-lookup"><span data-stu-id="a5532-164">You can also enter the values directly.</span></span>

![Add a condition](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/condition1.png)

> [!NOTE]
> <span data-ttu-id="a5532-166">You also have the capability to enter everything in Code View.</span><span class="sxs-lookup"><span data-stu-id="a5532-166">You also have the capability to enter everything in Code View.</span></span>
> 
> 

<span data-ttu-id="a5532-167">Let's take a look at the completed Logic App in code view.</span><span class="sxs-lookup"><span data-stu-id="a5532-167">Let's take a look at the completed Logic App in code view.</span></span>  

```JSON

       "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
    "actions": {
        "Conversion": {
            "conditions": [
                {
                    "dependsOn": "GetUtcDate"
                }
            ],
            "inputs": {
                "method": "post",
                "queries": {
                    "currentdateTime": "@{body('GetUtcDate')}"
                },
                "uri": "https://docdbnotificationapi-debug.azurewebsites.net/api/Conversion"
            },
            "metadata": {
                "apiDefinitionUrl": "https://docdbnotificationapi-debug.azurewebsites.net/swagger/docs/v1",
                "swaggerSource": "custom"
            },
            "type": "Http"
        },
        "Createfile": {
            "conditions": [
                {
                    "expression": "@greater(length(body('GetDocuments')), 0)"
                },
                {
                    "dependsOn": "GetDocuments"
                }
            ],
            "inputs": {
                "body": "@body('GetDocuments')",
                "host": {
                    "api": {
                        "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['azureblob']['connectionId']"
                    }
                },
                "method": "post",
                "path": "/datasets/default/files",
                "queries": {
                    "folderPath": "/patients",
                    "name": "Patient_@{guid()}.json"
                }
            },
            "type": "ApiConnection"
        },
        "GetDocuments": {
            "conditions": [
                {
                    "dependsOn": "Conversion"
                }
            ],
            "inputs": {
                "method": "post",
                "queries": {
                    "unixTimeStamp": "@body('Conversion')"
                },
                "uri": "https://docdbnotificationapi-debug.azurewebsites.net/api/Patient"
            },
            "metadata": {
                "apiDefinitionUrl": "https://docdbnotificationapi-debug.azurewebsites.net/swagger/docs/v1",
                "swaggerSource": "custom"
            },
            "type": "Http"
        },
        "GetUtcDate": {
            "conditions": [],
            "inputs": {
                "method": "get",
                "queries": {
                    "hoursBack": "@{int(triggerBody()['GetUtcDate_HoursBack'])}"
                },
                "uri": "https://docdbnotificationapi-debug.azurewebsites.net/api/Authorization"
            },
            "metadata": {
                "apiDefinitionUrl": "https://docdbnotificationapi-debug.azurewebsites.net/swagger/docs/v1",
                "swaggerSource": "custom"
            },
            "type": "Http"
        },
        "sendMail": {
            "conditions": [
                {
                    "dependsOn": "GetDocuments"
                }
            ],
            "inputs": {
                "body": "api_user=@{triggerBody()['sendgridUsername']}&api_key=@{triggerBody()['sendgridPassword']}&from=@{parameters('fromAddress')}&to=@{triggerBody()['EmailTo']}&subject=@{triggerBody()['Subject']}&text=@{int(length(body('GetDocuments')))} Documents Found",
                "headers": {
                    "Content-type": "application/x-www-form-urlencoded"
                },
                "method": "POST",
                "uri": "https://api.sendgrid.com/api/mail.send.json"
            },
            "type": "Http"
        }
    },
    "contentVersion": "1.0.0.0",
    "outputs": {
        "Results": {
            "type": "String",
            "value": "@{int(length(body('GetDocuments')))} Records Found"
        }
    },
    "parameters": {
        "$connections": {
            "defaultValue": {},
            "type": "Object"
        },
        "fromAddress": {
            "defaultValue": "user@msn.com",
            "type": "String"
        },
        "toAddress": {
            "defaultValue": "XXXXX@XXXXXXX.net",
            "type": "String"
        }
    },
    "triggers": {
        "manual": {
            "inputs": {
                "schema": {
                    "properties": {},
                    "required": [],
                    "type": "object"
                }
            },
            "type": "Manual"
        }

```

<span data-ttu-id="a5532-168">If you are not familiar with what the different sections in the code represents, you can view the [Logic App Workflow Definition Language](http://aka.ms/logicappsdocs) documentation.</span><span class="sxs-lookup"><span data-stu-id="a5532-168">If you are not familiar with what the different sections in the code represents, you can view the [Logic App Workflow Definition Language](http://aka.ms/logicappsdocs) documentation.</span></span>

<span data-ttu-id="a5532-169">For this workflow you are using an [HTTP Webhook Trigger](https://sendgrid.com/blog/whats-webhook/).</span><span class="sxs-lookup"><span data-stu-id="a5532-169">For this workflow you are using an [HTTP Webhook Trigger](https://sendgrid.com/blog/whats-webhook/).</span></span> <span data-ttu-id="a5532-170">If you look at the code above, you will see parameters like the following example.</span><span class="sxs-lookup"><span data-stu-id="a5532-170">If you look at the code above, you will see parameters like the following example.</span></span>

```C#

    =@{triggerBody()['Subject']}

```

<span data-ttu-id="a5532-171">The `triggerBody()` represents the parameters that are included in the body of an REST POST to the Logic App REST API.</span><span class="sxs-lookup"><span data-stu-id="a5532-171">The `triggerBody()` represents the parameters that are included in the body of an REST POST to the Logic App REST API.</span></span> <span data-ttu-id="a5532-172">The `()['Subject']` represents the field.</span><span class="sxs-lookup"><span data-stu-id="a5532-172">The `()['Subject']` represents the field.</span></span> <span data-ttu-id="a5532-173">All these parameters make up the JSON formatted body.</span><span class="sxs-lookup"><span data-stu-id="a5532-173">All these parameters make up the JSON formatted body.</span></span> 

> [!NOTE]
> <span data-ttu-id="a5532-174">By using a Web hook, you can have full access to the header and body of the trigger's request.</span><span class="sxs-lookup"><span data-stu-id="a5532-174">By using a Web hook, you can have full access to the header and body of the trigger's request.</span></span> <span data-ttu-id="a5532-175">In this application you want the body.</span><span class="sxs-lookup"><span data-stu-id="a5532-175">In this application you want the body.</span></span>
> 
> 

<span data-ttu-id="a5532-176">As mentioned previously, you can use the designer to assign parameters or do it in code view.</span><span class="sxs-lookup"><span data-stu-id="a5532-176">As mentioned previously, you can use the designer to assign parameters or do it in code view.</span></span>
<span data-ttu-id="a5532-177">If you do it in code view, then you define which properties require a value as shown in the following code sample.</span><span class="sxs-lookup"><span data-stu-id="a5532-177">If you do it in code view, then you define which properties require a value as shown in the following code sample.</span></span> 

```JSON

    "triggers": {
        "manual": {
            "inputs": {
            "schema": {
                "properties": {
            "Subject": {
                "type" : "String"    

            }
            },
                "required": [
            "Subject"
                 ],
                "type": "object"
            }
            },
            "type": "Manual"
        }
        }
```

<span data-ttu-id="a5532-178">What you are doing is creating a JSON schema that will be passed in from the body of the HTTP POST.</span><span class="sxs-lookup"><span data-stu-id="a5532-178">What you are doing is creating a JSON schema that will be passed in from the body of the HTTP POST.</span></span>
<span data-ttu-id="a5532-179">To fire your trigger, you will need a Callback URL.</span><span class="sxs-lookup"><span data-stu-id="a5532-179">To fire your trigger, you will need a Callback URL.</span></span>  <span data-ttu-id="a5532-180">You will learn how to generate it later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="a5532-180">You will learn how to generate it later in the tutorial.</span></span>  

## <a name="actions"></a><span data-ttu-id="a5532-181">Actions</span><span class="sxs-lookup"><span data-stu-id="a5532-181">Actions</span></span>
<span data-ttu-id="a5532-182">Let's see what each action in our Logic App does.</span><span class="sxs-lookup"><span data-stu-id="a5532-182">Let's see what each action in our Logic App does.</span></span>

### <a name="getutcdate"></a><span data-ttu-id="a5532-183">GetUTCDate</span><span class="sxs-lookup"><span data-stu-id="a5532-183">GetUTCDate</span></span>
<span data-ttu-id="a5532-184">**Designer View**</span><span class="sxs-lookup"><span data-stu-id="a5532-184">**Designer View**</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/getutcdate.png)

<span data-ttu-id="a5532-185">**Code View**</span><span class="sxs-lookup"><span data-stu-id="a5532-185">**Code View**</span></span>

```JSON

    "GetUtcDate": {
            "conditions": [],
            "inputs": {
            "method": "get",
            "queries": {
                "hoursBack": "@{int(triggerBody()['GetUtcDate_HoursBack'])}"
            },
            "uri": "https://docdbnotificationapi-debug.azurewebsites.net/api/Authorization"
            },
            "metadata": {
            "apiDefinitionUrl": "https://docdbnotificationapi-debug.azurewebsites.net/swagger/docs/v1"
            },
            "type": "Http"
        },

```

<span data-ttu-id="a5532-186">This HTTP action performs a GET operation.</span><span class="sxs-lookup"><span data-stu-id="a5532-186">This HTTP action performs a GET operation.</span></span>  <span data-ttu-id="a5532-187">It calls the API APP GetUtcDate method.</span><span class="sxs-lookup"><span data-stu-id="a5532-187">It calls the API APP GetUtcDate method.</span></span> <span data-ttu-id="a5532-188">The Uri uses the 'GetUtcDate_HoursBack' property passed into the Trigger body.</span><span class="sxs-lookup"><span data-stu-id="a5532-188">The Uri uses the 'GetUtcDate_HoursBack' property passed into the Trigger body.</span></span>  <span data-ttu-id="a5532-189">The 'GetUtcDate_HoursBack' value is set in the first Logic App.</span><span class="sxs-lookup"><span data-stu-id="a5532-189">The 'GetUtcDate_HoursBack' value is set in the first Logic App.</span></span> <span data-ttu-id="a5532-190">You will learn more about the Trigger Logic App later in the tutorial.</span><span class="sxs-lookup"><span data-stu-id="a5532-190">You will learn more about the Trigger Logic App later in the tutorial.</span></span>

<span data-ttu-id="a5532-191">This action calls your API App to return the UTC Date string value.</span><span class="sxs-lookup"><span data-stu-id="a5532-191">This action calls your API App to return the UTC Date string value.</span></span>

#### <a name="operations"></a><span data-ttu-id="a5532-192">Operations</span><span class="sxs-lookup"><span data-stu-id="a5532-192">Operations</span></span>
<span data-ttu-id="a5532-193">**Request**</span><span class="sxs-lookup"><span data-stu-id="a5532-193">**Request**</span></span>

```JSON

    {
        "uri": "https://docdbnotificationapi-debug.azurewebsites.net/api/Authorization",
        "method": "get",
        "queries": {
          "hoursBack": "24"
        }
    }

```

<span data-ttu-id="a5532-194">**Response**</span><span class="sxs-lookup"><span data-stu-id="a5532-194">**Response**</span></span>

```JSON

    {
        "statusCode": 200,
        "headers": {
          "pragma": "no-cache",
          "cache-Control": "no-cache",
          "date": "Fri, 26 Feb 2016 15:47:33 GMT",
          "server": "Microsoft-IIS/8.0",
          "x-AspNet-Version": "4.0.30319",
          "x-Powered-By": "ASP.NET"
        },
        "body": "Fri, 15 Jan 2016 23:47:33 GMT"
    }

```

<span data-ttu-id="a5532-195">The next step is to convert the UTC DateTime value to the Unix TimeStamp, which is a .NET double type.</span><span class="sxs-lookup"><span data-stu-id="a5532-195">The next step is to convert the UTC DateTime value to the Unix TimeStamp, which is a .NET double type.</span></span>

### <a name="conversion"></a><span data-ttu-id="a5532-196">Conversion</span><span class="sxs-lookup"><span data-stu-id="a5532-196">Conversion</span></span>
##### <a name="designer-view"></a><span data-ttu-id="a5532-197">Designer View</span><span class="sxs-lookup"><span data-stu-id="a5532-197">Designer View</span></span>
![Conversion](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/conversion.png)

##### <a name="code-view"></a><span data-ttu-id="a5532-199">Code View</span><span class="sxs-lookup"><span data-stu-id="a5532-199">Code View</span></span>
```JSON

    "Conversion": {
        "conditions": [
        {
            "dependsOn": "GetUtcDate"
        }
        ],
        "inputs": {
        "method": "post",
        "queries": {
            "currentDateTime": "@{body('GetUtcDate')}"
        },
        "uri": "https://docdbnotificationapi-debug.azurewebsites.net/api/Conversion"
        },
        "metadata": {
        "apiDefinitionUrl": "https://docdbnotificationapi-debug.azurewebsites.net/swagger/docs/v1"
        },
        "type": "Http"
    },

```

<span data-ttu-id="a5532-200">In this step you pass in the value returned from the GetUTCDate.</span><span class="sxs-lookup"><span data-stu-id="a5532-200">In this step you pass in the value returned from the GetUTCDate.</span></span>  <span data-ttu-id="a5532-201">There is a dependsOn condition, which means that the GetUTCDate action must complete successfully.</span><span class="sxs-lookup"><span data-stu-id="a5532-201">There is a dependsOn condition, which means that the GetUTCDate action must complete successfully.</span></span> <span data-ttu-id="a5532-202">If not, then this action is skipped.</span><span class="sxs-lookup"><span data-stu-id="a5532-202">If not, then this action is skipped.</span></span> 

<span data-ttu-id="a5532-203">This action calls your API App to handle the conversion.</span><span class="sxs-lookup"><span data-stu-id="a5532-203">This action calls your API App to handle the conversion.</span></span>

#### <a name="operations"></a><span data-ttu-id="a5532-204">Operations</span><span class="sxs-lookup"><span data-stu-id="a5532-204">Operations</span></span>
##### <a name="request"></a><span data-ttu-id="a5532-205">Request</span><span class="sxs-lookup"><span data-stu-id="a5532-205">Request</span></span>
```JSON

    {
        "uri": "https://docdbnotificationapi-debug.azurewebsites.net/api/Conversion",
        "method": "post",
        "queries": {
        "currentDateTime": "Fri, 15 Jan 2016 23:47:33 GMT"
        }
    }   
```

##### <a name="response"></a><span data-ttu-id="a5532-206">Response</span><span class="sxs-lookup"><span data-stu-id="a5532-206">Response</span></span>
```JSON

    {
        "statusCode": 200,
        "headers": {
          "pragma": "no-cache",
          "cache-Control": "no-cache",
          "date": "Fri, 26 Feb 2016 15:47:33 GMT",
          "server": "Microsoft-IIS/8.0",
          "x-AspNet-Version": "4.0.30319",
          "x-Powered-By": "ASP.NET"
        },
        "body": 1452901653
    }
```

<span data-ttu-id="a5532-207">In the next action, you will do a POST operation to our API App.</span><span class="sxs-lookup"><span data-stu-id="a5532-207">In the next action, you will do a POST operation to our API App.</span></span>

### <a name="getdocuments"></a><span data-ttu-id="a5532-208">GetDocuments</span><span class="sxs-lookup"><span data-stu-id="a5532-208">GetDocuments</span></span>
##### <a name="designer-view"></a><span data-ttu-id="a5532-209">Designer View</span><span class="sxs-lookup"><span data-stu-id="a5532-209">Designer View</span></span>
![Get Documents](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/getdocuments.png)

##### <a name="code-view"></a><span data-ttu-id="a5532-211">Code View</span><span class="sxs-lookup"><span data-stu-id="a5532-211">Code View</span></span>
```JSON

    "GetDocuments": {
        "conditions": [
        {
            "dependsOn": "Conversion"
        }
        ],
        "inputs": {
        "method": "post",
        "queries": {
            "unixTimeStamp": "@{body('Conversion')}"
        },
        "uri": "https://docdbnotificationapi-debug.azurewebsites.net/api/Patient"
        },
        "metadata": {
        "apiDefinitionUrl": "https://docdbnotificationapi-debug.azurewebsites.net/swagger/docs/v1"
        },
        "type": "Http"
    },

```

<span data-ttu-id="a5532-212">For the GetDocuments action you are going to pass in the response body from the Conversion action.</span><span class="sxs-lookup"><span data-stu-id="a5532-212">For the GetDocuments action you are going to pass in the response body from the Conversion action.</span></span> <span data-ttu-id="a5532-213">This is a parameter in the Uri:</span><span class="sxs-lookup"><span data-stu-id="a5532-213">This is a parameter in the Uri:</span></span>

```C#

    unixTimeStamp=@{body('Conversion')}

```

<span data-ttu-id="a5532-214">The QueryDocuments action does a HTTP POST operation to the API App.</span><span class="sxs-lookup"><span data-stu-id="a5532-214">The QueryDocuments action does a HTTP POST operation to the API App.</span></span> 

<span data-ttu-id="a5532-215">The method called is **QueryForNewPatientDocuments**.</span><span class="sxs-lookup"><span data-stu-id="a5532-215">The method called is **QueryForNewPatientDocuments**.</span></span>

#### <a name="operations"></a><span data-ttu-id="a5532-216">Operations</span><span class="sxs-lookup"><span data-stu-id="a5532-216">Operations</span></span>
##### <a name="request"></a><span data-ttu-id="a5532-217">Request</span><span class="sxs-lookup"><span data-stu-id="a5532-217">Request</span></span>
```JSON

    {
        "uri": "https://docdbnotificationapi-debug.azurewebsites.net/api/Patient",
        "method": "post",
        "queries": {
        "unixTimeStamp": "1452901653"
        }
    }
```

##### <a name="response"></a><span data-ttu-id="a5532-218">Response</span><span class="sxs-lookup"><span data-stu-id="a5532-218">Response</span></span>
```JSON

    {
        "statusCode": 200,
        "headers": {
        "pragma": "no-cache",
        "cache-Control": "no-cache",
        "date": "Fri, 26 Feb 2016 15:47:35 GMT",
        "server": "Microsoft-IIS/8.0",
        "x-AspNet-Version": "4.0.30319",
        "x-Powered-By": "ASP.NET"
        },
        "body": [
        {
            "id": "xcda",
            "_rid": "vCYLAP2k6gAXAAAAAAAAAA==",
            "_self": "dbs/vCYLAA==/colls/vCYLAP2k6gA=/docs/vCYLAP2k6gAXAAAAAAAAAA==/",
            "_ts": 1454874620,
            "_etag": "\"00007d01-0000-0000-0000-56b79ffc0000\"",
            "resourceType": "Patient",
            "text": {
            "status": "generated",
            "div": "<div>\n      \n      <p>Henry Levin the 7th</p>\n    \n    </div>"
            },
            "identifier": [
            {
                "use": "usual",
                "type": {
                "coding": [
                    {
                    "system": "http://hl7.org/fhir/v2/0203",
                    "code": "MR"
                    }
                ]
                },
                "system": "urn:oid:2.16.840.1.113883.19.5",
                "value": "12345"
            }
            ],
            "active": true,
            "name": [
            {
                    "family": [
                        "Levin"
                    ],
                    "given": [
                        "Henry"
                    ]
                }
            ],
            "gender": "male",
            "birthDate": "1932-09-24",
            "managingOrganization": {
                "reference": "Organization/2.16.840.1.113883.19.5",
                "display": "Good Health Clinic"
            }
        },

```

<span data-ttu-id="a5532-219">The next action is to save the documents to [Azure Blog storage](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="a5532-219">The next action is to save the documents to [Azure Blog storage](https://azure.microsoft.com/services/storage/).</span></span> 

> [!NOTE]
> <span data-ttu-id="a5532-220">Blob storage requires an Azure Storage account.</span><span class="sxs-lookup"><span data-stu-id="a5532-220">Blob storage requires an Azure Storage account.</span></span> <span data-ttu-id="a5532-221">You need to provision an Azure Blob storage account and add a new Blob named patients.</span><span class="sxs-lookup"><span data-stu-id="a5532-221">You need to provision an Azure Blob storage account and add a new Blob named patients.</span></span> <span data-ttu-id="a5532-222">For more information, see [Get started with Azure Blob storage](../storage/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="a5532-222">For more information, see [Get started with Azure Blob storage](../storage/storage-dotnet-how-to-use-blobs.md).</span></span>
> 
> 

### <a name="create-file"></a><span data-ttu-id="a5532-223">Create File</span><span class="sxs-lookup"><span data-stu-id="a5532-223">Create File</span></span>
##### <a name="designer-view"></a><span data-ttu-id="a5532-224">Designer View</span><span class="sxs-lookup"><span data-stu-id="a5532-224">Designer View</span></span>
![Create File](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/createfile.png)

##### <a name="code-view"></a><span data-ttu-id="a5532-226">Code View</span><span class="sxs-lookup"><span data-stu-id="a5532-226">Code View</span></span>
```JSON

    {
    "host": {
        "api": {
            "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
        },
        "connection": {
            "name": "subscriptions/fxxxxxc079-4e5d-b002-xxxxxxxxxx/resourceGroups/Api-Default-Central-US/providers/Microsoft.Web/connections/azureblob"
        }
    },
    "method": "post",
    "path": "/datasets/default/files",
    "queries": {
        "folderPath": "/patients",
        "name": "Patient_17513174-e61d-4b56-88cb-5cf383db4430.json"
    },
    "body": [
        {
            "id": "xcda",
            "_rid": "vCYLAP2k6gAXAAAAAAAAAA==",
            "_self": "dbs/vCYLAA==/colls/vCYLAP2k6gA=/docs/vCYLAP2k6gAXAAAAAAAAAA==/",
            "_ts": 1454874620,
            "_etag": "\"00007d01-0000-0000-0000-56b79ffc0000\"",
            "resourceType": "Patient",
            "text": {
                "status": "generated",
                "div": "<div>\n      \n      <p>Henry Levin the 7th</p>\n    \n    </div>"
            },
            "identifier": [
                {
                    "use": "usual",
                    "type": {
                        "coding": [
                            {
                                "system": "http://hl7.org/fhir/v2/0203",
                                "code": "MR"
                            }
                        ]
                    },
                    "system": "urn:oid:2.16.840.1.113883.19.5",
                    "value": "12345"
                }
            ],
            "active": true,
            "name": [
                {
                    "family": [
                        "Levin"
                    ],
                    "given": [
                        "Henry"
                    ]
                }
            ],
            "gender": "male",
            "birthDate": "1932-09-24",
            "managingOrganization": {
                "reference": "Organization/2.16.840.1.113883.19.5",
                "display": "Good Health Clinic"
            }
        },

```

<span data-ttu-id="a5532-227">The code is generated from action in the designer.</span><span class="sxs-lookup"><span data-stu-id="a5532-227">The code is generated from action in the designer.</span></span> <span data-ttu-id="a5532-228">You don't have to modify the code.</span><span class="sxs-lookup"><span data-stu-id="a5532-228">You don't have to modify the code.</span></span>

<span data-ttu-id="a5532-229">If you are not familiar with using the Azure Blob API, see [Get started with the Azure blob storage API](../connectors/connectors-create-api-azureblobstorage.md).</span><span class="sxs-lookup"><span data-stu-id="a5532-229">If you are not familiar with using the Azure Blob API, see [Get started with the Azure blob storage API](../connectors/connectors-create-api-azureblobstorage.md).</span></span>

#### <a name="operations"></a><span data-ttu-id="a5532-230">Operations</span><span class="sxs-lookup"><span data-stu-id="a5532-230">Operations</span></span>
##### <a name="request"></a><span data-ttu-id="a5532-231">Request</span><span class="sxs-lookup"><span data-stu-id="a5532-231">Request</span></span>
```JSON

    "host": {
        "api": {
            "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
        },
        "connection": {
            "name": "subscriptions/fxxxxxc079-4e5d-b002-xxxxxxxxxx/resourceGroups/Api-Default-Central-US/providers/Microsoft.Web/connections/azureblob"
        }
    },
    "method": "post",
    "path": "/datasets/default/files",
    "queries": {
        "folderPath": "/patients",
        "name": "Patient_17513174-e61d-4b56-88cb-5cf383db4430.json"
    },
    "body": [
        {
            "id": "xcda",
            "_rid": "vCYLAP2k6gAXAAAAAAAAAA==",
            "_self": "dbs/vCYLAA==/colls/vCYLAP2k6gA=/docs/vCYLAP2k6gAXAAAAAAAAAA==/",
            "_ts": 1454874620,
            "_etag": "\"00007d01-0000-0000-0000-56b79ffc0000\"",
            "resourceType": "Patient",
            "text": {
                "status": "generated",
                "div": "<div>\n      \n      <p>Henry Levin the 7th</p>\n    \n    </div>"
            },
            "identifier": [
                {
                    "use": "usual",
                    "type": {
                        "coding": [
                            {
                                "system": "http://hl7.org/fhir/v2/0203",
                                "code": "MR"
                            }
                        ]
                    },
                    "system": "urn:oid:2.16.840.1.113883.19.5",
                    "value": "12345"
                }
            ],
            "active": true,
            "name": [
                {
                    "family": [
                        "Levin"
                    ],
                    "given": [
                        "Henry"
                    ]
                }
            ],
            "gender": "male",
            "birthDate": "1932-09-24",
            "managingOrganization": {
                "reference": "Organization/2.16.840.1.113883.19.5",
                "display": "Good Health Clinic"
            }
        },….


```

##### <a name="response"></a><span data-ttu-id="a5532-232">Response</span><span class="sxs-lookup"><span data-stu-id="a5532-232">Response</span></span>
```JSON

    {
        "statusCode": 200,
        "headers": {
        "pragma": "no-cache",
        "x-ms-request-id": "2b2f7c57-2623-4d71-8e53-45c26b30ea9d",
        "cache-Control": "no-cache",
        "date": "Fri, 26 Feb 2016 15:47:36 GMT",
        "set-Cookie": "ARRAffinity=29e552cea7db23196f7ffa644003eaaf39bc8eb6dd555511f669d13ab7424faf;Path=/;Domain=127.0.0.1",
        "server": "Microsoft-HTTPAPI/2.0",
        "x-AspNet-Version": "4.0.30319",
        "x-Powered-By": "ASP.NET"
        },
        "body": {
        "Id": "0B0nBzHyMV-_NRGRDcDNMSFAxWFE",
        "Name": "Patient_47a2a0dc-640d-4f01-be38-c74690d085cb.json",
        "DisplayName": "Patient_47a2a0dc-640d-4f01-be38-c74690d085cb.json",
        "Path": "/Patient/Patient_47a2a0dc-640d-4f01-be38-c74690d085cb.json",
        "LastModified": "2016-02-26T15:47:36.215Z",
        "Size": 65647,
        "MediaType": "application/octet-stream",
        "IsFolder": false,
        "ETag": "\"c-g_a-1OtaH-kNQ4WBoXLp3Zv9s/MTQ1NjUwMTY1NjIxNQ\"",
        "FileLocator": "0B0nBzHyMV-_NRGRDcDNMSFAxWFE"
        }
    }
```

<span data-ttu-id="a5532-233">Your last step is to send an email notification</span><span class="sxs-lookup"><span data-stu-id="a5532-233">Your last step is to send an email notification</span></span>

### <a name="sendemail"></a><span data-ttu-id="a5532-234">sendEmail</span><span class="sxs-lookup"><span data-stu-id="a5532-234">sendEmail</span></span>
##### <a name="designer-view"></a><span data-ttu-id="a5532-235">Designer View</span><span class="sxs-lookup"><span data-stu-id="a5532-235">Designer View</span></span>
![Send Email](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/sendemail.png)

##### <a name="code-view"></a><span data-ttu-id="a5532-237">Code View</span><span class="sxs-lookup"><span data-stu-id="a5532-237">Code View</span></span>
```JSON


    "sendMail": {
        "conditions": [
        {
            "dependsOn": "GetDocuments"
        }
        ],
        "inputs": {
        "body": "api_user=@{triggerBody()['sendgridUsername']}&api_key=@{triggerBody()['sendgridPassword']}&from=@{parameters('fromAddress')}&to=@{triggerBody()['EmailTo']}&subject=@{triggerBody()['Subject']}&text=@{int(length(body('GetDocuments')))} Documents Found",
        "headers": {
            "Content-type": "application/x-www-form-urlencoded"
        },
        "method": "POST",
        "uri": "https://api.sendgrid.com/api/mail.send.json"
        },
        "type": "Http"
    }
```

<span data-ttu-id="a5532-238">In this action you send an email notification.</span><span class="sxs-lookup"><span data-stu-id="a5532-238">In this action you send an email notification.</span></span>  <span data-ttu-id="a5532-239">You are using [SendGrid](https://sendgrid.com/marketing/sendgrid-services?cvosrc=PPC.Bing.sendgrib&cvo_cid=SendGrid%20-%20US%20-%20Brand%20-%20&mc=Paid%20Search&mcd=BingAds&keyword=sendgrib&network=o&matchtype=e&mobile=&content=&search=1&utm_source=bing&utm_medium=cpc&utm_term=%5Bsendgrib%5D&utm_content=%21acq%21v2%2134335083397-8303227637-1649139544&utm_campaign=SendGrid+-+US+-+Brand+-+%28English%29).</span><span class="sxs-lookup"><span data-stu-id="a5532-239">You are using [SendGrid](https://sendgrid.com/marketing/sendgrid-services?cvosrc=PPC.Bing.sendgrib&cvo_cid=SendGrid%20-%20US%20-%20Brand%20-%20&mc=Paid%20Search&mcd=BingAds&keyword=sendgrib&network=o&matchtype=e&mobile=&content=&search=1&utm_source=bing&utm_medium=cpc&utm_term=%5Bsendgrib%5D&utm_content=%21acq%21v2%2134335083397-8303227637-1649139544&utm_campaign=SendGrid+-+US+-+Brand+-+%28English%29).</span></span>   

<span data-ttu-id="a5532-240">The code for this was generated using a template for Logic App and SendGrid that is in the [101-logic-app-sendgrid GitHub repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-logic-app-sendgrid).</span><span class="sxs-lookup"><span data-stu-id="a5532-240">The code for this was generated using a template for Logic App and SendGrid that is in the [101-logic-app-sendgrid GitHub repository](https://github.com/Azure/azure-quickstart-templates/tree/master/101-logic-app-sendgrid).</span></span>

<span data-ttu-id="a5532-241">The HTTP operation is a POST.</span><span class="sxs-lookup"><span data-stu-id="a5532-241">The HTTP operation is a POST.</span></span> 

<span data-ttu-id="a5532-242">The authorization parameters are in the trigger properties</span><span class="sxs-lookup"><span data-stu-id="a5532-242">The authorization parameters are in the trigger properties</span></span>

```JSON

    },
        "sendgridPassword": {
             "type": "SecureString"
         },
         "sendgridUsername": {
            "type": "String"
         }

        In addition, other parameters are static values set in the Parameters section of the Logic App. These are:
        },
        "toAddress": {
            "defaultValue": "XXXX@XXXX.com",
            "type": "String"
        },
        "fromAddress": {
            "defaultValue": "XXX@msn.com",
            "type": "String"
        },
        "emailBody": {
            "defaultValue": "@{string(concat(int(length(actions('QueryDocuments').outputs.body)) Records Found),'/n', actions('QueryDocuments').outputs.body)}",
            "type": "String"
        },

```

<span data-ttu-id="a5532-243">The emailBody is concatenating the number of documents returned from the query, which can be "0" or more, along with, "Records Found".</span><span class="sxs-lookup"><span data-stu-id="a5532-243">The emailBody is concatenating the number of documents returned from the query, which can be "0" or more, along with, "Records Found".</span></span> <span data-ttu-id="a5532-244">The rest of the parameters are set from the Trigger parameters.</span><span class="sxs-lookup"><span data-stu-id="a5532-244">The rest of the parameters are set from the Trigger parameters.</span></span>

<span data-ttu-id="a5532-245">This action depends on the **GetDocuments** action.</span><span class="sxs-lookup"><span data-stu-id="a5532-245">This action depends on the **GetDocuments** action.</span></span>

#### <a name="operations"></a><span data-ttu-id="a5532-246">Operations</span><span class="sxs-lookup"><span data-stu-id="a5532-246">Operations</span></span>
##### <a name="request"></a><span data-ttu-id="a5532-247">Request</span><span class="sxs-lookup"><span data-stu-id="a5532-247">Request</span></span>
```JSON

    {
        "uri": "https://api.sendgrid.com/api/mail.send.json",
        "method": "POST",
        "headers": {
        "Content-type": "application/x-www-form-urlencoded"
        },
        "body": "api_user=azureuser@azure.com&api_key=Biz@Talk&from=user@msn.com&to=XXXX@XXXX.com&subject=New Patients&text=37 Documents Found"
    }

```

##### <a name="response"></a><span data-ttu-id="a5532-248">Response</span><span class="sxs-lookup"><span data-stu-id="a5532-248">Response</span></span>
```JSON

    {
        "statusCode": 200,
        "headers": {
        "connection": "keep-alive",
        "x-Frame-Options": "DENY,DENY",
        "access-Control-Allow-Origin": "https://sendgrid.com",
        "date": "Fri, 26 Feb 2016 15:47:35 GMT",
        "server": "nginx"
        },
        "body": {
        "message": "success"
        }
    }
```

<span data-ttu-id="a5532-249">Lastly you want to be able to see the results from your Logic App on the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a5532-249">Lastly you want to be able to see the results from your Logic App on the Azure Portal.</span></span> <span data-ttu-id="a5532-250">To do that, you add a parameter to the outputs section.</span><span class="sxs-lookup"><span data-stu-id="a5532-250">To do that, you add a parameter to the outputs section.</span></span>

```JSON

    "outputs": {
        "Results": {
            "type": "String",
            "value": "@{int(length(actions('QueryDocuments').outputs.body))} Records Found"
        }

```

<span data-ttu-id="a5532-251">This returns the same value that is sent in the email body.</span><span class="sxs-lookup"><span data-stu-id="a5532-251">This returns the same value that is sent in the email body.</span></span> <span data-ttu-id="a5532-252">The following figure shows an example where "29 Records Found".</span><span class="sxs-lookup"><span data-stu-id="a5532-252">The following figure shows an example where "29 Records Found".</span></span>

![Results](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/logic-app-run.png)

## <a name="metrics"></a><span data-ttu-id="a5532-254">Metrics</span><span class="sxs-lookup"><span data-stu-id="a5532-254">Metrics</span></span>
<span data-ttu-id="a5532-255">You can configure monitoring for the main Logic App in the portal.</span><span class="sxs-lookup"><span data-stu-id="a5532-255">You can configure monitoring for the main Logic App in the portal.</span></span> <span data-ttu-id="a5532-256">This enables you to view the Run Latency and other events as show in the following figure.</span><span class="sxs-lookup"><span data-stu-id="a5532-256">This enables you to view the Run Latency and other events as show in the following figure.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/metrics.png)

## <a name="docdb-trigger"></a><span data-ttu-id="a5532-257">DocDb Trigger</span><span class="sxs-lookup"><span data-stu-id="a5532-257">DocDb Trigger</span></span>
<span data-ttu-id="a5532-258">This Logic App is the trigger that starts the workflow on your main Logic App.</span><span class="sxs-lookup"><span data-stu-id="a5532-258">This Logic App is the trigger that starts the workflow on your main Logic App.</span></span>

<span data-ttu-id="a5532-259">The following figure shows the Designer View.</span><span class="sxs-lookup"><span data-stu-id="a5532-259">The following figure shows the Designer View.</span></span>

![](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/trigger-recurrence.png)

```JSON

    {
        "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
        "actions": {
        "Http": {
            "conditions": [],
            "inputs": {
            "body": {
                "EmailTo": "XXXXXX@XXXXX.net",
                "GetUtcDate_HoursBack": "24",
                "Subject": "New Patients",
                "sendgridPassword": "********",
                "sendgridUsername": "azureuser@azure.com"
            },
            "method": "POST",
            "uri": "https://prod-01.westus.logic.azure.com:443/workflows/12a1de57e48845bc9ce7a247dfabc887/triggers/manual/run?api-version=2015-08-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=ObTlihr529ATIuvuG-dhxOgBL4JZjItrvPQ8PV6973c"
            },
            "type": "Http"
        }
        },
        "contentVersion": "1.0.0.0",
        "outputs": {
        "Results": {
            "type": "String",
            "value": "@{body('Http')['status']}"
        }
        },
        "parameters": {},
        "triggers": {
        "recurrence": {
            "recurrence": {
            "frequency": "Hour",
            "interval": 24
            },
            "type": "Recurrence"
        }
        }
    }

```

<span data-ttu-id="a5532-260">The Trigger is set for a recurrence of twenty-four hours.</span><span class="sxs-lookup"><span data-stu-id="a5532-260">The Trigger is set for a recurrence of twenty-four hours.</span></span> <span data-ttu-id="a5532-261">The Action is an HTTP POST that uses the Callback URL for the main Logic App.</span><span class="sxs-lookup"><span data-stu-id="a5532-261">The Action is an HTTP POST that uses the Callback URL for the main Logic App.</span></span> <span data-ttu-id="a5532-262">The body contains the parameters that are specified in the JSON Schema.</span><span class="sxs-lookup"><span data-stu-id="a5532-262">The body contains the parameters that are specified in the JSON Schema.</span></span> 

#### <a name="operations"></a><span data-ttu-id="a5532-263">Operations</span><span class="sxs-lookup"><span data-stu-id="a5532-263">Operations</span></span>
##### <a name="request"></a><span data-ttu-id="a5532-264">Request</span><span class="sxs-lookup"><span data-stu-id="a5532-264">Request</span></span>
```JSON

    {
        "uri": "https://prod-01.westus.logic.azure.com:443/workflows/12a1de57e48845bc9ce7a247dfabc887/triggers/manual/run?api-version=2015-08-01-preview&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=ObTlihr529ATIuvuG-dhxOgBL4JZjItrvPQ8PV6973c",
        "method": "POST",
        "body": {
        "EmailTo": "XXXXXX@XXXXX.net",
        "GetUtcDate_HoursBack": "24",
        "Subject": "New Patients",
        "sendgridPassword": "********",
        "sendgridUsername": "azureuser@azure.com"
        }
    }

```

##### <a name="response"></a><span data-ttu-id="a5532-265">Response</span><span class="sxs-lookup"><span data-stu-id="a5532-265">Response</span></span>
```JSON

    {
        "statusCode": 202,
        "headers": {
        "pragma": "no-cache",
        "x-ms-ratelimit-remaining-workflow-writes": "7486",
        "x-ms-ratelimit-burst-remaining-workflow-writes": "1248",
        "x-ms-request-id": "westus:2d440a39-8ba5-4a9c-92a6-f959b8d2357f",
        "cache-Control": "no-cache",
        "date": "Thu, 25 Feb 2016 21:01:06 GMT"
        }
    }
```

<span data-ttu-id="a5532-266">Now let's look at the API App.</span><span class="sxs-lookup"><span data-stu-id="a5532-266">Now let's look at the API App.</span></span>

## <a name="docdbnotificationapi"></a><span data-ttu-id="a5532-267">DocDBNotificationApi</span><span class="sxs-lookup"><span data-stu-id="a5532-267">DocDBNotificationApi</span></span>
<span data-ttu-id="a5532-268">Although there are several operations in the app, you are only going to use three.</span><span class="sxs-lookup"><span data-stu-id="a5532-268">Although there are several operations in the app, you are only going to use three.</span></span>

* <span data-ttu-id="a5532-269">GetUtcDate</span><span class="sxs-lookup"><span data-stu-id="a5532-269">GetUtcDate</span></span>
* <span data-ttu-id="a5532-270">ConvertToTimeStamp</span><span class="sxs-lookup"><span data-stu-id="a5532-270">ConvertToTimeStamp</span></span>
* <span data-ttu-id="a5532-271">QueryForNewPatientDocuments</span><span class="sxs-lookup"><span data-stu-id="a5532-271">QueryForNewPatientDocuments</span></span>

### <a name="docdbnotificationapi-operations"></a><span data-ttu-id="a5532-272">DocDBNotificationApi Operations</span><span class="sxs-lookup"><span data-stu-id="a5532-272">DocDBNotificationApi Operations</span></span>
<span data-ttu-id="a5532-273">Let's take a look at the Swagger documentation</span><span class="sxs-lookup"><span data-stu-id="a5532-273">Let's take a look at the Swagger documentation</span></span>

> [!NOTE]
> <span data-ttu-id="a5532-274">To allow you to call the operations externally, you need to add a CORS allowed origin value of "\*" (without quotes) in the settings of your API App as shown in the following figure.</span><span class="sxs-lookup"><span data-stu-id="a5532-274">To allow you to call the operations externally, you need to add a CORS allowed origin value of "\*" (without quotes) in the settings of your API App as shown in the following figure.</span></span>
> 
> 

![Cors Configuration](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/cors.png)

#### <a name="getutcdate"></a><span data-ttu-id="a5532-276">GetUtcDate</span><span class="sxs-lookup"><span data-stu-id="a5532-276">GetUtcDate</span></span>
![G](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/getutcdateswagger.png)

#### <a name="converttotimestamp"></a><span data-ttu-id="a5532-278">ConvertToTimeStamp</span><span class="sxs-lookup"><span data-stu-id="a5532-278">ConvertToTimeStamp</span></span>
![Get UTC Date](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/converion-swagger.png)

#### <a name="queryfornewpatientdocuments"></a><span data-ttu-id="a5532-280">QueryForNewPatientDocuments</span><span class="sxs-lookup"><span data-stu-id="a5532-280">QueryForNewPatientDocuments</span></span>
![Query](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/patientswagger.png)

<span data-ttu-id="a5532-282">Let's take a look at the code behind this operation.</span><span class="sxs-lookup"><span data-stu-id="a5532-282">Let's take a look at the code behind this operation.</span></span>

#### <a name="getutcdate"></a><span data-ttu-id="a5532-283">GetUtcDate</span><span class="sxs-lookup"><span data-stu-id="a5532-283">GetUtcDate</span></span>
```C#

    /// <summary>
    /// Gets the current UTC Date value
    /// </summary>
    /// <returns></returns>
    [H ttpGet]
    [Metadata("GetUtcDate", "Gets the current UTC Date value minus the Hours Back")]
    [SwaggerOperation("GetUtcDate")]
    [SwaggerResponse(HttpStatusCode.OK, type: typeof (string))]
    [SwaggerResponse(HttpStatusCode.InternalServerError, "Internal Server Operation Error")]
    public string GetUtcDate(
       [Metadata("Hours Back", "How many hours back from the current Date Time")] int hoursBack)
    {


        return DateTime.UtcNow.AddHours(-hoursBack).ToString("r");
    }
```

<span data-ttu-id="a5532-284">This operation simply returns the returns the current UTC DateTime minus the HoursBack value.</span><span class="sxs-lookup"><span data-stu-id="a5532-284">This operation simply returns the returns the current UTC DateTime minus the HoursBack value.</span></span>

#### <a name="converttotimestamp"></a><span data-ttu-id="a5532-285">ConvertToTimeStamp</span><span class="sxs-lookup"><span data-stu-id="a5532-285">ConvertToTimeStamp</span></span>
``` C#

        /// <summary>
        ///     Converts DateTime to double
        /// </summary>
        /// <param name="currentdateTime"></param>
        /// <returns></returns>
        [Metadata("Converts Universal DateTime to number")]
        [SwaggerResponse(HttpStatusCode.OK, null, typeof (double))]
        [SwaggerResponse(HttpStatusCode.BadRequest, "DateTime is invalid")]
        [SwaggerResponse(HttpStatusCode.InternalServerError)]
        [SwaggerOperation(nameof(ConvertToTimestamp))]
        public double ConvertToTimestamp(
            [Metadata("currentdateTime", "DateTime value to convert")] string currentdateTime)
        {
            double result;

            try
            {
                var uncoded = HttpContext.Current.Server.UrlDecode(currentdateTime);

                var newDateTime = DateTime.Parse(uncoded);
                //create Timespan by subtracting the value provided from the Unix Epoch
                var span = newDateTime - new DateTime(1970, 1, 1, 0, 0, 0, 0).ToLocalTime();

                //return the total seconds (which is a UNIX timestamp)
                result = span.TotalSeconds;
            }
            catch (Exception e)
            {
                throw new Exception("unable to convert to Timestamp", e.InnerException);
            }

            return result;
        }

```

<span data-ttu-id="a5532-286">This operation converts the response from the GetUtcDate operation to a double value.</span><span class="sxs-lookup"><span data-stu-id="a5532-286">This operation converts the response from the GetUtcDate operation to a double value.</span></span>

#### <a name="queryfornewpatientdocuments"></a><span data-ttu-id="a5532-287">QueryForNewPatientDocuments</span><span class="sxs-lookup"><span data-stu-id="a5532-287">QueryForNewPatientDocuments</span></span>
```C#

        /// <summary>
        ///     Query for new Patient Documents
        /// </summary>
        /// <param name="unixTimeStamp"></param>
        /// <returns>IList</returns>
        [Metadata("QueryForNewDocuments",
            "Query for new Documents where the Timestamp is greater than or equal to the DateTime value in the query parameters."
            )]
        [SwaggerOperation("QueryForNewDocuments")]
        [SwaggerResponse(HttpStatusCode.OK, type: typeof (Task<IList<Document>>))]
        [SwaggerResponse(HttpStatusCode.BadRequest, "The syntax of the SQL Statement is incorrect")]
        [SwaggerResponse(HttpStatusCode.NotFound, "No Documents were found")]
        [SwaggerResponse(HttpStatusCode.InternalServerError, "Internal Server Operation Error")]
        // ReSharper disable once ConsiderUsingAsyncSuffix
        public IList<Document> QueryForNewPatientDocuments(
            [Metadata("UnixTimeStamp", "The DateTime value used to search from")] double unixTimeStamp)
        {
            var context = new DocumentDbContext();
            var filterQuery = string.Format(InvariantCulture, "SELECT * FROM Patient p WHERE p._ts >=  {0}",
                unixTimeStamp);
            var options = new FeedOptions {MaxItemCount = -1};


            var collectionLink = UriFactory.CreateDocumentCollectionUri(DocumentDbContext.DatabaseId,
                DocumentDbContext.CollectionId);

            var response =
                context.Client.CreateDocumentQuery<Document>(collectionLink, filterQuery, options).AsEnumerable();

            return response.ToList();
    }

```

<span data-ttu-id="a5532-288">This operation uses the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) to create a document query.</span><span class="sxs-lookup"><span data-stu-id="a5532-288">This operation uses the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md) to create a document query.</span></span> 

```C#
     CreateDocumentQuery<Document>(collectionLink, filterQuery, options).AsEnumerable();
```

<span data-ttu-id="a5532-289">The response from the ConvertToTimeStamp operation (unixTimeStamp) is passed in.</span><span class="sxs-lookup"><span data-stu-id="a5532-289">The response from the ConvertToTimeStamp operation (unixTimeStamp) is passed in.</span></span> <span data-ttu-id="a5532-290">The operation returns a List of documents, `IList<Document>`.</span><span class="sxs-lookup"><span data-stu-id="a5532-290">The operation returns a List of documents, `IList<Document>`.</span></span>

<span data-ttu-id="a5532-291">Previously we talked about the CallbackURL.</span><span class="sxs-lookup"><span data-stu-id="a5532-291">Previously we talked about the CallbackURL.</span></span> <span data-ttu-id="a5532-292">In order to start the workflow in your main Logic App, you will need to call it using the CallbackURL.</span><span class="sxs-lookup"><span data-stu-id="a5532-292">In order to start the workflow in your main Logic App, you will need to call it using the CallbackURL.</span></span>

## <a name="callbackurl"></a><span data-ttu-id="a5532-293">CallbackURL</span><span class="sxs-lookup"><span data-stu-id="a5532-293">CallbackURL</span></span>
<span data-ttu-id="a5532-294">To start off, you will need your Azure AD Token.</span><span class="sxs-lookup"><span data-stu-id="a5532-294">To start off, you will need your Azure AD Token.</span></span>  <span data-ttu-id="a5532-295">It can be difficult to get this token.</span><span class="sxs-lookup"><span data-stu-id="a5532-295">It can be difficult to get this token.</span></span> <span data-ttu-id="a5532-296">I was looking for an easy method and Jeff Hollan, who is an Azure Logic App program manager, recommended using the [armclient](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) in PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a5532-296">I was looking for an easy method and Jeff Hollan, who is an Azure Logic App program manager, recommended using the [armclient](http://blog.davidebbo.com/2015/01/azure-resource-manager-client.html) in PowerShell.</span></span>  <span data-ttu-id="a5532-297">You can install it following the directions provided.</span><span class="sxs-lookup"><span data-stu-id="a5532-297">You can install it following the directions provided.</span></span>

<span data-ttu-id="a5532-298">The operations you want to use are Login and Call ARM API.</span><span class="sxs-lookup"><span data-stu-id="a5532-298">The operations you want to use are Login and Call ARM API.</span></span>

<span data-ttu-id="a5532-299">Login: You use the same credentials for logging in to the Azure Portal.</span><span class="sxs-lookup"><span data-stu-id="a5532-299">Login: You use the same credentials for logging in to the Azure Portal.</span></span> 

<span data-ttu-id="a5532-300">The Call ARM Api operation is the one that will generate your CallBackURL.</span><span class="sxs-lookup"><span data-stu-id="a5532-300">The Call ARM Api operation is the one that will generate your CallBackURL.</span></span>

<span data-ttu-id="a5532-301">In PowerShell, you call it as follows:</span><span class="sxs-lookup"><span data-stu-id="a5532-301">In PowerShell, you call it as follows:</span></span>    

```powershell

    ArmClient.exe post https://management.azure.com/subscriptions/[YOUR SUBSCRIPTION ID/resourcegroups/[YOUR RESOURCE GROUP]/providers/Microsoft.Logic/workflows/[YOUR LOGIC APP NAME/triggers/manual/listcallbackurl?api-version=2015-08-01-preview

```

<span data-ttu-id="a5532-302">Your result should look like this:</span><span class="sxs-lookup"><span data-stu-id="a5532-302">Your result should look like this:</span></span>

```powershell

    https://prod-02.westus.logic.azure.com:443/workflows/12a1de57e48845bc9ce7a247dfabc887/triggers/manual/run?api-version=2015-08-01-prevaiew&sp=%2Ftriggers%2Fmanual%2Frun&sv=1.0&sig=XXXXXXXXXXXXXXXXXXX

```

<span data-ttu-id="a5532-303">You can use a tool like [postman](http://www.getpostman.com/) to test you main Logic App as shown in the following figure.</span><span class="sxs-lookup"><span data-stu-id="a5532-303">You can use a tool like [postman](http://www.getpostman.com/) to test you main Logic App as shown in the following figure.</span></span>

![Postman](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/newpostman.png)

<span data-ttu-id="a5532-305">The following table lists the Trigger parameters that make up the body of the DocDB Trigger Logic App.</span><span class="sxs-lookup"><span data-stu-id="a5532-305">The following table lists the Trigger parameters that make up the body of the DocDB Trigger Logic App.</span></span>

| <span data-ttu-id="a5532-306">Parameter</span><span class="sxs-lookup"><span data-stu-id="a5532-306">Parameter</span></span> | <span data-ttu-id="a5532-307">Description</span><span class="sxs-lookup"><span data-stu-id="a5532-307">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a5532-308">GetUtcDate_HoursBack</span><span class="sxs-lookup"><span data-stu-id="a5532-308">GetUtcDate_HoursBack</span></span> |<span data-ttu-id="a5532-309">Used to set the number of hours for the search start date</span><span class="sxs-lookup"><span data-stu-id="a5532-309">Used to set the number of hours for the search start date</span></span> |
| <span data-ttu-id="a5532-310">sendgridUsername</span><span class="sxs-lookup"><span data-stu-id="a5532-310">sendgridUsername</span></span> |<span data-ttu-id="a5532-311">Used to set the number of hours for the search start date</span><span class="sxs-lookup"><span data-stu-id="a5532-311">Used to set the number of hours for the search start date</span></span> |
| <span data-ttu-id="a5532-312">sendgridPassword</span><span class="sxs-lookup"><span data-stu-id="a5532-312">sendgridPassword</span></span> |<span data-ttu-id="a5532-313">The user name for Send Grid email</span><span class="sxs-lookup"><span data-stu-id="a5532-313">The user name for Send Grid email</span></span> |
| <span data-ttu-id="a5532-314">EmailTo</span><span class="sxs-lookup"><span data-stu-id="a5532-314">EmailTo</span></span> |<span data-ttu-id="a5532-315">The email address that will receive the email notification</span><span class="sxs-lookup"><span data-stu-id="a5532-315">The email address that will receive the email notification</span></span> |
| <span data-ttu-id="a5532-316">Subject</span><span class="sxs-lookup"><span data-stu-id="a5532-316">Subject</span></span> |<span data-ttu-id="a5532-317">The Subject for the email</span><span class="sxs-lookup"><span data-stu-id="a5532-317">The Subject for the email</span></span> |

## <a name="viewing-the-patient-data-in-the-azure-blob-service"></a><span data-ttu-id="a5532-318">Viewing the patient data in the Azure Blob service</span><span class="sxs-lookup"><span data-stu-id="a5532-318">Viewing the patient data in the Azure Blob service</span></span>
<span data-ttu-id="a5532-319">Go to your Azure Storage account, and select Blobs under services as shown in the following figure.</span><span class="sxs-lookup"><span data-stu-id="a5532-319">Go to your Azure Storage account, and select Blobs under services as shown in the following figure.</span></span>

![Storage account](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/docdbstorageaccount.png) 

<span data-ttu-id="a5532-321">You will be able to view the Patient blob file information as shown below.</span><span class="sxs-lookup"><span data-stu-id="a5532-321">You will be able to view the Patient blob file information as shown below.</span></span>

![Blob service](https://docstestmedia1.blob.core.windows.net/azure-media/articles/documentdb/media/documentdb-change-notification/blobservice.png)

## <a name="summary"></a><span data-ttu-id="a5532-323">Summary</span><span class="sxs-lookup"><span data-stu-id="a5532-323">Summary</span></span>
<span data-ttu-id="a5532-324">In this walkthrough, you've learned the following:</span><span class="sxs-lookup"><span data-stu-id="a5532-324">In this walkthrough, you've learned the following:</span></span>

* <span data-ttu-id="a5532-325">It is possible to implement notifications in DocumentDB.</span><span class="sxs-lookup"><span data-stu-id="a5532-325">It is possible to implement notifications in DocumentDB.</span></span>
* <span data-ttu-id="a5532-326">By using Logic Apps, you can automate the process.</span><span class="sxs-lookup"><span data-stu-id="a5532-326">By using Logic Apps, you can automate the process.</span></span>
* <span data-ttu-id="a5532-327">By using Logic Apps, you can reduce the time it takes to deliver an application.</span><span class="sxs-lookup"><span data-stu-id="a5532-327">By using Logic Apps, you can reduce the time it takes to deliver an application.</span></span>
* <span data-ttu-id="a5532-328">By using HTTP you can easy consume an API App within a Logic App.</span><span class="sxs-lookup"><span data-stu-id="a5532-328">By using HTTP you can easy consume an API App within a Logic App.</span></span>
* <span data-ttu-id="a5532-329">You can easily create a CallBackURL that replaces the HTTP Listener.</span><span class="sxs-lookup"><span data-stu-id="a5532-329">You can easily create a CallBackURL that replaces the HTTP Listener.</span></span>
* <span data-ttu-id="a5532-330">You can easily create custom workflows with Logic Apps Designer.</span><span class="sxs-lookup"><span data-stu-id="a5532-330">You can easily create custom workflows with Logic Apps Designer.</span></span>

<span data-ttu-id="a5532-331">The key is to plan ahead and model your workflow.</span><span class="sxs-lookup"><span data-stu-id="a5532-331">The key is to plan ahead and model your workflow.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5532-332">Next steps</span><span class="sxs-lookup"><span data-stu-id="a5532-332">Next steps</span></span>
<span data-ttu-id="a5532-333">Please download and use the Logic App code provided on [GitHub](https://github.com/HEDIDIN/DocDbNotifications).</span><span class="sxs-lookup"><span data-stu-id="a5532-333">Please download and use the Logic App code provided on [GitHub](https://github.com/HEDIDIN/DocDbNotifications).</span></span> <span data-ttu-id="a5532-334">I invite you to build on the application and submit changes to the repo.</span><span class="sxs-lookup"><span data-stu-id="a5532-334">I invite you to build on the application and submit changes to the repo.</span></span> 

<span data-ttu-id="a5532-335">To learn more about DocumentDB, visit the [Learning Path](https://azure.microsoft.com/documentation/learning-paths/documentdb/).</span><span class="sxs-lookup"><span data-stu-id="a5532-335">To learn more about DocumentDB, visit the [Learning Path](https://azure.microsoft.com/documentation/learning-paths/documentdb/).</span></span>























